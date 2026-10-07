# Configuration & Externalized Settings Inventory

The checked-in configuration comprises three property files, Compose, a Dockerfile, an environment example and Oracle/Azure provisioning scripts. Runtime profiles are separate from build configuration, and credentials below are references or `[MASKED]`, never literal values.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| Base configuration | Spring properties | `src/main/resources/application.properties` | Defaults and required datasource password reference |
| Docker overrides | Spring properties | `src/main/resources/application-docker.properties` | Docker runtime profile; duplicate upload entries have identical values |
| Test overrides | Spring properties | `src/test/resources/application-test.properties` | Test classpath; H2 and masked local admin credential |
| Build | Maven POM | `pom.xml` | Parent version, Java target and JAR packaging |
| Container | Dockerfile | `Dockerfile` | Build/runtime images, heap options and port |
| Local orchestration | Compose | `docker-compose.yml` | Environment bindings, database health gate, volume and network |
| Secret variable template | Environment example | `.env.example` | Operator copies to ignored `.env` and supplies credentials |
| Bean property injection | Java configuration | `src/main/java/com/photoalbum/config/SecurityConfig.java:34-42` | Admin username default; required admin password |
| Upload property injection | Java constructor | `src/main/java/com/photoalbum/service/impl/PhotoServiceImpl.java:41-47` | Byte limit and MIME list |
| Oracle initialization | Shell/SQL | `oracle-init/create-user.sh`, `01-create-user.sql`, `02-verify-user.sql`, `healthcheck.sql` | Container init mount; grants and verification |
| Azure provisioning | PowerShell | `azure-setup.ps1` | ACR, AKS, PostgreSQL and generated `.env`; not proof of deployment |
| Azure teardown | PowerShell | `azure-reset.ps1` | Resource group/ACR/AKS cleanup options; not run |
| Operator guidance | Markdown | `README.md` | Contains stale Oracle XE/image details; current Compose is authoritative for local container definition |

No bootstrap config, config-server repository, Key Vault/App Configuration binding, Kubernetes application manifests, Helm chart or Terraform/Bicep files were found in application/deployment sources. Existing `.env` content was not read.

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| Default Maven build | Normal Maven invocation | Java 8 target, JAR | Boot Maven plugin; no named profiles declared |
| Docker build stage (not a Maven profile) | Image build | Maven packaging without executing tests | `mvn dependency:go-offline -B`; `mvn clean package -DskipTests` |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| Default | No active profile | `application.properties` | Oracle, DEBUG app/web logging |
| `docker` | Compose `SPRING_PROFILES_ACTIVE=docker` | Base plus `application-docker.properties` | Oracle; app INFO, web WARN, Hibernate SQL DEBUG |
| `test` | `PhotoAlbumApplicationTests` uses `@ActiveProfiles("test")` | Base plus test-classpath `application-test.properties` | H2, create-drop, SQL display disabled, masked admin setting |

No `@Profile` bean branches or combined application profile activation was found. Standard Boot property precedence applies; explicit environment bindings can override property-file defaults.

## Properties Inventory

### Photo Album property files and injection defaults

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `server.port` | `8080` integer | Default/docker; inherited by test | Base and Docker files |
| `server.servlet.encoding.charset` | `UTF-8` string | Default/docker | Base and Docker |
| `server.servlet.encoding.enabled` | `true` boolean | Default/docker | Base and Docker |
| `server.servlet.encoding.force` | `true` boolean | Default/docker | Base and Docker |
| `spring.datasource.url` | `${SPRING_DATASOURCE_URL:jdbc:oracle:thin:@oracle-db:1521/FREEPDB1}` | Default/docker; test `jdbc:h2:mem:testdb` | Property files; Compose supplies Oracle URL |
| `spring.datasource.username` | `${SPRING_DATASOURCE_USERNAME:photoalbum}` | Default/docker; test `sa` | Property files and Compose |
| `spring.datasource.password` | Required `SPRING_DATASOURCE_PASSWORD` reference; value `[MASKED]` | Default/docker; test-local `[MASKED]` | Files/Compose; no production default |
| `spring.datasource.driver-class-name` | `oracle.jdbc.OracleDriver` | Default/docker; test `org.h2.Driver` | Property files |
| `spring.jpa.database-platform` | `org.hibernate.dialect.OracleDialect` | Default/docker; test `org.hibernate.dialect.H2Dialect` | Property files |
| `spring.jpa.hibernate.ddl-auto` | `create` | Default/docker; test `create-drop` | Property files |
| `spring.jpa.show-sql` | `true` boolean | Default/docker; test `false` | Property files |
| `spring.jpa.properties.hibernate.format_sql` | `true` boolean | Default/docker; inherited by test | Base and Docker |
| `spring.servlet.multipart.max-file-size` | `10MB` data size | Default/docker; inherited by test | Base and Docker |
| `spring.servlet.multipart.max-request-size` | `50MB` data size | Default/docker; inherited by test | Base and Docker |
| `app.file-upload.max-file-size-bytes` | `10485760` long | All three | Property files and service injection |
| `app.file-upload.allowed-mime-types` | `image/jpeg,image/png,image/gif,image/webp` string list | All three | Property files and service injection |
| `app.file-upload.max-files-per-upload` | `10` integer | All three | Property files; no server consumer found |
| `app.file-upload.upload-path` | Not declared in main files; test `target/test-uploads` | Test only | Test properties; no active service consumer found |
| `logging.level.com.photoalbum` | `DEBUG` | Docker `INFO`; test `DEBUG` | Property files |
| `logging.level.org.springframework.web` | `DEBUG` | Docker `WARN`; inherited by test | Base and Docker |
| `logging.level.org.hibernate.SQL` | Not explicitly set in base | Docker `DEBUG` | Docker properties |
| `app.admin.username` | `admin` injection default; env `APP_ADMIN_USERNAME` | Default/docker; test `admin` | SecurityConfig and Compose/test |
| `app.admin.password` | Required property; env `APP_ADMIN_PASSWORD`; `[MASKED]` | Default/docker; test-local `[MASKED]` | SecurityConfig and Compose/test |

Property types are inferred from values/injection, not declared schemas. Credentials are redacted even when test/example values are not production secrets. Evidence: full contents of the three property files and `SecurityConfig.java:34-42`.

### Compose environment and Azure script settings

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `ORACLE_PASSWORD` | Required environment reference, `[MASKED]` | Oracle container | `.env.example` → Compose |
| `APP_USER` | `photoalbum` | Oracle container/application username binding | `.env.example`, Compose |
| `APP_USER_PASSWORD` | Required environment reference, `[MASKED]` | Oracle container; mapped to app `SPRING_DATASOURCE_PASSWORD` | `.env.example` → Compose |
| `SPRING_DATASOURCE_URL` | Compose `jdbc:oracle:thin:@oracle-db:1521/FREEPDB1` | Docker app | Compose |
| `SPRING_DATASOURCE_USERNAME` | Compose `${APP_USER:-photoalbum}` | Docker app | Compose |
| `APP_ADMIN_USERNAME` | Compose `admin` | Docker app | `.env.example` → Compose |
| `APP_ADMIN_PASSWORD` | Required environment reference, `[MASKED]` | Docker app | `.env.example` → Compose |
| `POSTGRES_ADMIN_USER` / `POSTGRES_APP_USER` | Environment or script defaults `photoalbum_admin` / `photoalbum` | Azure provisioning, not Spring profiles | `azure-setup.ps1:38-41` |
| `POSTGRES_ADMIN_PASSWORD` / `POSTGRES_APP_PASSWORD` | Environment or cryptographically generated; `[MASKED]` | Azure provisioning | Same script |
| `POSTGRES_SERVER`, `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_CONNECTION_STRING` | Derived server/user/JDBC URL; password `[MASKED]` | Generated `.env`, not bound by current Spring files | `azure-setup.ps1:267-299` |
| `RESOURCE_GROUP` | `photo-album-resources-<random suffix>` | Azure provisioning | Script |
| `LOCATION` | `westus3` | Azure provisioning | Script |
| `ACR_NAME` / `AKS_CLUSTER_NAME` | Randomized registry; resource-group-based cluster name | Azure provisioning | Script/generated `.env` |
| `POSTGRES_SERVER_NAME` / `POSTGRES_DATABASE_NAME` | Resource-group-based server; `photoalbum` database | Azure provisioning | Script |
| PostgreSQL server version/storage/backup/public access | `15` / `32` GB / `7` days / `0.0.0.0` CLI argument | Azure provisioning | `azure-setup.ps1:117-127` |
| Azure reset options | Mandatory `ResourceGroupName`; switches `Force`, `ACROnly`, `AKSOnly` | Teardown only | `azure-reset.ps1:6-18` |

Azure script output variables and Compose input variables are different; no mapping to a working PostgreSQL application configuration is present. Oracle SQL grants/verification assume schema `photoalbum`, while the shell helper derives an uppercase username from `APP_USER`; changing the user requires reconciling these sources.

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| Photo Album container | `JAVA_OPTS="-Xmx512m -Xms256m"`; `java $JAVA_OPTS -jar app.jar`; Compose `SPRING_PROFILES_ACTIVE=docker` | Heap 256 MiB initial, 512 MiB max; no container CPU/memory limit | One Compose service instance; no scaling definition |
| Oracle container | Container entrypoint; init mount | No Compose resource limit; README recommends 4 GB available RAM, not enforced allocation | One Compose instance |
| AKS provisioning | Node VM `Standard_D8ds_v5` | VM SKU only; no application pod resources | Two nodes, not evidence of two app replicas |
| PostgreSQL provisioning | SKU `Standard_D4ads_v5` | SKU/storage only; no app heap setting | One provisioned server; HA not specified |

Evidence: `Dockerfile:27-31`, `docker-compose.yml`, `README.md:30`, `azure-setup.ps1:30-32,85-91,117-127`. No app readiness/liveness probes, JVM system-property arguments or autoscaler settings were found.

## Startup Dependency Chain

1. Operator supplies required Oracle/application/admin passwords before Compose starts; required Compose substitutions fail early when unset.
2. Oracle container initializes its data volume and executes mounted `oracle-init` files. The shell helper includes a 30-second sleep; SQL grants and verification are not separate service readiness checks.
3. Oracle health runs container `healthcheck.sh`: 30-second interval, 10-second timeout, 15 retries, 180-second start period.
4. `photoalbum-java-app` waits on Oracle `service_healthy`, then starts its JVM. It uses `restart: on-failure`; there is no app healthcheck.
5. Azure setup separately provisions group → ACR → AKS and registry attachment → PostgreSQL/database/grants → local `.env`. It waits 30 seconds before SQL setup, but it does not define an application startup/readiness chain.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| `ORACLE_PASSWORD` | Oracle administrative credential | Operator `.env` / container environment, `[MASKED]` |
| `APP_USER_PASSWORD` → `SPRING_DATASOURCE_PASSWORD` | Application DB credential | Operator `.env` / container environment, `[MASKED]` |
| `APP_ADMIN_PASSWORD` → `app.admin.password` | HTTP Basic credential | Operator environment; BCrypt in-memory encoding, `[MASKED]` |
| Test datasource/admin passwords | Test-only settings | Test properties, `[MASKED]` |
| `POSTGRES_ADMIN_PASSWORD`, `POSTGRES_APP_PASSWORD` → `POSTGRES_PASSWORD` | Azure database credentials | Script environment/generated local `.env`, `[MASKED]` |

No application secret-store integration, encrypted property framework or field-level secret encryption was found. JDBC URLs listed above contain no password.

### Secrets Provisioning Workflow

Local flow: operator copies `.env.example` to ignored `.env` → supplies values → Compose substitutes them into Oracle and app environments → Spring binds datasource/admin properties. Oracle initialization receives database credentials; the web app receives its schema password and admin password. SecurityConfig BCrypt-encodes the admin password when constructing the in-memory user; that is not encryption of the source environment variable.

Azure flow: an already authenticated Azure CLI session is checked → environment-supplied or cryptographically generated PostgreSQL credentials are used to create admin/app identities → database grants are issued → app credential/server information is written to local `.env`. AKS is attached to ACR for image pull authorization. No Key Vault, database managed-identity authentication, deployed Kubernetes Secret binding or completed app deployment is shown. The generated PostgreSQL `.env` is not the Oracle/admin `.env` schema Compose requires.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| No business feature flag framework or conditional-bean toggle found | Not applicable | No relevant declarations |

Runtime profile activation and logging/upload configuration are settings, not evidence of feature rollout.

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Java compilation target | 8 / `java.version=1.8` | `pom.xml:23-28` |
| Spring Boot parent | 2.7.18 | `pom.xml:8-13` |
| Spring MVC/Data JPA/Security/Thymeleaf/validation/Jackson/Hibernate | Parent-managed; precise transitive versions not resolved | `pom.xml` |
| Oracle JDBC ojdbc8 / H2 | Parent-managed; child versions absent | `pom.xml` |
| Commons IO | 2.11.0 | `pom.xml:68-73` |
| Maven build image | `maven:3.9.6-eclipse-temurin-8` | `Dockerfile:2` |
| JRE image | `eclipse-temurin:8-jre` | `Dockerfile:17` |
| Oracle container | `gvenzl/oracle-free:latest`; exact runtime release not pinned | `docker-compose.yml:4` |
| PostgreSQL Azure provisioning | 15 | `azure-setup.ps1:123` |
| Bootstrap browser assets | 5.3.0 | Templates' jsDelivr references |

Static file inspection only: no live secrets, infrastructure, runtime versions, readiness or configuration binding was exercised. README Oracle XE descriptions conflict with current Compose Oracle Free; deployment intent and actual resources must not be conflated.
