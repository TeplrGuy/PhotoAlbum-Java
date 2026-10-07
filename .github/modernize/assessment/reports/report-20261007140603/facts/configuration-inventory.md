# Configuration & Externalized Settings Inventory

Configuration is split across three Spring property files, container build/orchestration files, environment-variable templates, database initialization scripts, and an Azure provisioning script. Secrets are supplied through environment variables or generated during provisioning; every literal credential, including development/test defaults and usernames, is masked below.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| Base application settings | Spring properties | `src/main/resources/application.properties` | Default configuration; Oracle connection, encoding, persistence settings, upload settings, logging. |
| Docker profile | Spring properties | `src/main/resources/application-docker.properties` | Overrides/additions when `docker` is active; several upload properties are repeated with identical values. |
| Test profile | Spring properties, test classpath | `src/test/resources/application-test.properties` | H2 and test-only credentials; activated by `src/test/java/com/photoalbum/PhotoAlbumApplicationTests.java:8`. |
| Code-level settings | Spring `@Value`, bean configuration | `src/main/java/com/photoalbum/config/SecurityConfig.java:28-60`; `src/main/java/com/photoalbum/service/impl/PhotoServiceImpl.java:35-44` | Admin credential defaults exist in source; upload size and MIME settings are injected. Image-pixel cap is a source constant, not externalized. |
| Build settings | Maven XML | `pom.xml` | Single module; Java compiler settings and dependency/plugin declarations. |
| Container settings | Dockerfile | `Dockerfile` | Build/runtime images, JVM environment variable, startup command and exposed port. |
| Local orchestration | Compose YAML | `docker-compose.yml` | Two services, environment bindings, startup health dependency, persistent database volume and bridge network. |
| Local secret template | Environment file | `.env.example`; operator-created `.env` | Compose automatically reads local `.env`; `.gitignore:201-204` excludes `.env` and `.env.*`, except the template. No live `.env` was discovered in the source listing. |
| Oracle initialization | SQL/shell | `oracle-init/01-create-user.sql`, `oracle-init/02-verify-user.sql`, `oracle-init/create-user.sh`, `oracle-init/healthcheck.sql` | Mounted into the database image's initialization directory. SQL uses a fixed schema identity, whereas shell initialization uses environment variables. |
| Azure provisioning | PowerShell and generated environment file | `azure-setup.ps1` | Creates ACR, AKS and PostgreSQL; writes resource metadata and plaintext PostgreSQL credentials into root `.env`. It is not an application runtime profile. |
| Azure cleanup | PowerShell parameters | `azure-reset.ps1` | `ResourceGroupName` required; `Force`, `ACROnly`, `AKSOnly` control cleanup. Uses existing Azure CLI/Kubernetes credentials. |
| Operational reference | Documentation | `README.md` | Local commands and resource guidance; some Oracle image/version/port descriptions differ from current Compose configuration. Credential examples are not reproduced. |
| Browser library configuration | Template CDN links | `src/main/resources/templates/{index,detail,layout}.html` | Bootstrap version pinned in external CDN URLs; not a startup dependency. |
| Repository automation | GitHub Actions YAML | `.github/workflows/{squad-ci,squad-docs,squad-heartbeat,squad-insider-release,squad-issue-assign,squad-label-enforce,squad-preview,squad-promote,squad-release,squad-triage,sync-squad-labels}.yml` | Repository lifecycle automation, not Spring configuration. Credential reference names are cataloged below. `squad-ci.yml` has no executable Maven build/test command configured. |
| Dependency automation | Dependabot configuration | `.github/dependabot.yml` | Repository maintenance configuration; not consumed by the application. |
| Optional assistant integration | MCP JSON | `.copilot/mcp-config.json` | Example Trello integration using `npx` and `@trello/mcp-server`; credential fields are masked. Not an application dependency. |

No application `bootstrap.*`, Spring YAML, remote configuration repository, Spring Cloud Config, Azure App Configuration, Vault, Key Vault, AWS secret-store integration, Kubernetes workload manifest, or Helm configuration was discovered among the inspected source/deployment files. Restricted `.github/agents` content was not accessed.

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| Default Maven build; no named profiles | Ordinary `mvn` invocation | Compile/package the single JAR module | Spring Boot Maven plugin; web, Thymeleaf, JPA, validation, security and JSON starters; Oracle runtime driver; Commons IO; optional DevTools; test starter and H2. |
| Docker build mode; not a Maven profile | Dockerfile build stage | Resolve dependencies, then package without executing tests | `mvn dependency:go-offline -B`; `mvn clean package -DskipTests`. |
| Test dependency scopes; not a Maven profile | Maven test lifecycle | Add test-classpath dependencies | `spring-boot-starter-test`, H2. |

`pom.xml` contains no `<profiles>` section and no profile-specific dependency/plugin changes. Compiler/build properties are `java.version=1.8`, `maven.compiler.source=8`, `maven.compiler.target=8`, and `project.build.sourceEncoding=UTF-8` (`pom.xml:23-28`). Runtime `docker` and `test` profiles do not change Maven dependency resolution.

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| Default/base | No explicit profile needed | `application.properties` | Oracle settings, port/encoding/upload limits, DEBUG application/web logging. No explicit `spring.profiles.active` in this file. |
| `docker` | Compose sets `SPRING_PROFILES_ACTIVE=docker` | Base plus `application-docker.properties` | Application logging INFO, web logging WARN, Hibernate SQL logging DEBUG; Oracle and other values mostly repeated. |
| `test` | `@ActiveProfiles("test")` on application test | Base plus test-classpath `application-test.properties` | H2 connection/driver/dialect, `create-drop`, SQL logging disabled, upload-path setting and masked test admin credentials. |

No `@Profile` bean selectors, additional environment-specific property files, or repository-configured combined profile activation were found. Spring supports externally supplied profile lists, but no composition is defined here.

## Properties Inventory

### Application module (`photo-album`)

Defaults below are file/code defaults, not a dump of live environment values. `base`, `docker`, and `test` denote the files above. Sensitive values are masked even when empty or intended only for development.

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `server.port` | `8080` (integer port) | base, docker; inherited by test | Base:2; docker:25. |
| `server.servlet.encoding.charset` | `UTF-8` (string) | base, docker | Base:5; docker:9. |
| `server.servlet.encoding.enabled` | `true` (boolean) | base, docker | Base:6; docker:10. |
| `server.servlet.encoding.force` | `true` (boolean) | base, docker | Base:7; docker:11. |
| `spring.datasource.url` | `${SPRING_DATASOURCE_URL:jdbc:oracle:thin:@oracle-db:1521/FREEPDB1}` (JDBC URL) | base, docker; test overrides to `jdbc:h2:mem:testdb` | Base:12; docker:3; test:2. |
| `spring.datasource.username` | `${SPRING_DATASOURCE_USERNAME:[MASKED]}` (credential string) | base, docker; test literal `[MASKED]` | Base:13; docker:4; test:4. |
| `spring.datasource.password` | `${SPRING_DATASOURCE_PASSWORD}`; no file fallback | base, docker; test `[MASKED]` (empty test credential) | Base:14; docker:5; test:5. |
| `spring.datasource.driver-class-name` | `oracle.jdbc.OracleDriver` (class name) | base, docker; test `org.h2.Driver` | Base:15; docker:6; test:3. |
| `spring.jpa.database-platform` | `org.hibernate.dialect.OracleDialect` (class name) | base, docker; test `org.hibernate.dialect.H2Dialect` | Base:18; docker:14; test:8. |
| `spring.jpa.hibernate.ddl-auto` | `create` (enum-like string) | base, docker; test `create-drop` | Base:19; docker:15; test:9. |
| `spring.jpa.show-sql` | `true` (boolean) | base, docker; test `false` | Base:20; docker:16; test:10. |
| `spring.jpa.properties.hibernate.format_sql` | `true` (boolean) | base, docker; inherited by test | Base:21; docker:17. |
| `spring.servlet.multipart.max-file-size` | `10MB` (data size) | base, docker; inherited by test | Base:24; docker:26. |
| `spring.servlet.multipart.max-request-size` | `50MB` (data size) | base, docker; inherited by test | Base:25; docker:27. |
| `app.file-upload.max-file-size-bytes` | `10485760` (long, bytes) | base, docker, test | Base:28; docker:20,28; test:14; injected in `PhotoServiceImpl.java:43`. |
| `app.file-upload.allowed-mime-types` | `image/jpeg,image/png,image/gif,image/webp` (comma-separated string array) | base, docker, test | Base:29; docker:21,29; test:15; injected in `PhotoServiceImpl.java:44`. |
| `app.file-upload.max-files-per-upload` | `10` (integer) | base, docker, test | Base:30; docker:22,30; test:16. No corresponding source-level injection was found; presence in configuration does not prove enforcement. |
| `app.file-upload.upload-path` | `target/test-uploads` (path); no base default | test only | Test:13. No corresponding source-level injection was found. |
| `logging.level.com.photoalbum` | `DEBUG` (log level) | base, test; docker `INFO` | Base:33; docker:33; test:19. |
| `logging.level.org.springframework.web` | `DEBUG` (log level) | base; docker `WARN`; inherited by test | Base:34; docker:34. |
| `logging.level.org.hibernate.SQL` | `DEBUG` (log level); not explicitly set in base | docker | Docker:35. |
| `app.admin.username` | Source-level development default `[MASKED]` (credential string) | all; test explicit `[MASKED]`; Compose supplies `APP_ADMIN_USERNAME` | `SecurityConfig.java:36`; test:22; Compose:35. |
| `app.admin.password` | Source-level development default `[MASKED]` (credential string) | all; test explicit `[MASKED]`; Compose requires `APP_ADMIN_PASSWORD` | `SecurityConfig.java:37`; test:23; Compose:36. |

Resolution: Maven packages main resources; Spring loads base settings and activated profile files. Environment variables, system properties and command-line properties can override packaged settings; profile-specific files override base files. The database placeholders explicitly consult `SPRING_DATASOURCE_*`. Admin settings use Spring relaxed environment binding from `APP_ADMIN_USERNAME`/`APP_ADMIN_PASSWORD`. Test properties are only packaged on the test classpath.

Compose interpolation occurs before application startup: shell variables override local `.env`; `:?` requires a nonempty supplied value and `:-` supplies a fallback. Compose maps `APP_USER` to both Oracle `APP_USER` and application `SPRING_DATASOURCE_USERNAME`, and `APP_USER_PASSWORD` to both database and application password variables. Changing only `SPRING_DATASOURCE_*` in the host environment does not replace Compose's explicit assignments.

### Deployment and database configuration

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `ORACLE_PASSWORD` | Required, no Compose default; `[MASKED]` | Compose/database initialization | Compose:7 uses required-value interpolation; `.env.example`; shell initializer. |
| `APP_USER` | Credential default `[MASKED]` | Compose/database initialization | Compose:8,33; `.env.example`; `create-user.sh`. |
| `APP_USER_PASSWORD` | Required, no Compose default; `[MASKED]` | Compose/database initialization | Compose:9,34; `.env.example`; shell initializer. |
| `APP_ADMIN_USERNAME` | Credential default `[MASKED]` | Compose/application | Compose:35; `.env.example`. |
| `APP_ADMIN_PASSWORD` | Required, no Compose default; `[MASKED]` | Compose/application | Compose:36; `.env.example`. |
| `RESOURCE_GROUP` | `photo-album-resources-${RANDOM_SUFFIX}`; suffix generated per run | Azure provisioning | `azure-setup.ps1:26-27`; written into `.env`. |
| `LOCATION` | `westus3` | Azure provisioning | Script:28; written into `.env`. |
| `ACR_NAME` | `photoalbumacr` plus random numeric suffix | Azure provisioning | Script:29; written into `.env`. |
| `POSTGRES_SERVER_NAME` | Resource-group name plus `-postgresql` | Azure provisioning | Script:31. |
| `POSTGRES_DATABASE_NAME` | `photoalbum` (database name, not credential) | Azure provisioning | Script:33. |
| `POSTGRES_ADMIN_USER`, `POSTGRES_APP_USER` | Environment override; otherwise credential defaults `[MASKED]` | Azure provisioning | Script:38,40. |
| `POSTGRES_ADMIN_PASSWORD`, `POSTGRES_APP_PASSWORD` | Environment override; otherwise separately generated 24-character passwords `[MASKED]` | Azure provisioning | Script:15-22,39,41. |
| `DATASOURCE_URL` | `jdbc:postgresql://${SERVER_FQDN}:5432/$POSTGRES_DATABASE_NAME` | Azure provisioning | Script:267; constructed locally, not shown bound into Spring workload settings. |
| `POSTGRES_SERVER` | Provisioned PostgreSQL hostname | Generated environment | Script:274,287. |
| `POSTGRES_USER`, `POSTGRES_PASSWORD` | Application credential values `[MASKED]` | Generated environment | Script:275-276,288-289. |
| `POSTGRES_CONNECTION_STRING` | Credential-bearing connection string `[MASKED]` | Generated environment | Script:277,290. |
| `AKS_CLUSTER_NAME` | Resource-group name plus `-aks` | Generated environment | Script:295. |
| Oracle initialization session property `_ORACLE_SCRIPT` | `true` | Database SQL initialization | `01-create-user.sql:12`; `02-verify-user.sql:2`. |
| Oracle initialization tablespaces | Default `USERS`; temporary `TEMP`; unlimited quota in initializer | Database initialization | `01-create-user.sql:25-30`; `create-user.sh:34-35`; literal account names omitted. |
| Trello `TRELLO_API_KEY`, `TRELLO_TOKEN` | Example credential placeholders `[MASKED]` | Optional tooling only | `.copilot/mcp-config.json:9-12`; not Spring properties. |

No valid numeric ranges beyond framework types/units are declared for most settings. Upload validation details and database model/behavior are intentionally outside this inventory.

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| Java container | `JAVA_OPTS="-Xmx512m -Xms256m"`; `java $JAVA_OPTS -jar app.jar`; `SPRING_PROFILES_ACTIVE=docker`; datasource/admin environment bindings listed above | Initial heap 256 MiB; maximum heap 512 MiB. No Compose memory/CPU limits; heap is not total process memory. | One Compose service instance; no configured autoscaling; `restart: on-failure`. |
| Oracle container | `gvenzl/oracle-free:latest`; database environment bindings; exposed host/container port `1521`; named volume `oracle_data` at `/opt/oracle/oradata`; initialization bind mount | No Compose memory/CPU limits. README recommends at least 4 GB available for the database container; guidance, not enforcement. | One Compose service instance; no explicit restart policy or scaling settings. |
| Local Java invocation | README: `mvn spring-boot:run` or `java -jar target/photo-album-1.0.0.jar`; externally supplied datasource/admin settings | No local heap/CPU limits documented | Manual process; unspecified. |
| Azure AKS infrastructure | `AKS_NODE_VM_SIZE=Standard_D8ds_v5`; `--node-count 2`; `--generate-ssh-keys`; ACR attachment | VM SKU controls node resources; no application pod requests/limits provided | Two infrastructure nodes; no application replica count/autoscaler configured. |
| Azure PostgreSQL infrastructure | PostgreSQL `15`; `PostgreSQL_SKU=Standard_D4ads_v5`; storage `32` GB; backup retention `7` days | SKU-defined resources; no separate custom memory/CPU value | One provisioned server. |
| Azure registry infrastructure | ACR `Basic`; `--admin-enabled true` | Not specified | One registry. |

No startup `-D` system properties are specified for the deployed application. Docker publishes Java port `8080`; both Compose services join the `photoalbum-network` bridge. README's Oracle port `5500`, XE image and XE limits are not current Compose settings.

## Startup Dependency Chain

1. **Compose environment resolution → required secret values**: `ORACLE_PASSWORD`, `APP_USER_PASSWORD` and `APP_ADMIN_PASSWORD` must be supplied before Compose can create services; username fallbacks are masked.
2. **Oracle database → image initialization and mounted scripts**: database state uses the named volume. The image initializes the application account from its environment; SQL adds privileges and verifies the fixed schema account. `create-user.sh` additionally sleeps 30 seconds before a SQLPlus connection and requires the database/application password variables. Initialization is not a versioned migration mechanism.
3. **Java application → Oracle `service_healthy`**: `docker-compose.yml:17-22,39-41` uses the image's `healthcheck.sh`, every 30 seconds, 10-second timeout, 15 retries, 180-second start period. The mounted `oracle-init/healthcheck.sql` is not the Compose healthcheck command.
4. **Java process → resolvable configuration and accessible database**: no dedicated application readiness/liveness probe, wait-for-TCP wrapper, Spring Cloud Config retry, or application startup timeout is configured. Application `on-failure` restart is the only explicit restart mechanism.
5. **Test context → in-memory H2**: the test profile does not require the Oracle container.
6. **Azure script → Azure CLI login/context → resource group → ACR → AKS → ACR attachment → PostgreSQL/database/firewall rules → 30-second sleep → application-account SQL setup → generated `.env`**. A fixed sleep is not an active readiness probe. Azure setup provisions resources; no workload deployment/binding or application readiness verification is present in the inspected script.

The SQL initialization files target a literal account `[MASKED]`, whereas the shell initializer and Compose permit changing `APP_USER`; overrides therefore require keeping SQL account references aligned. No config-server/discovery-service startup chain exists.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| `ORACLE_PASSWORD` | Database administrator password | Operator environment/local `.env`; template placeholder `[MASKED]`; no Compose default. |
| `APP_USER`, `SPRING_DATASOURCE_USERNAME` | Database login identity | Environment/Compose defaults/base and Docker property fallbacks `[MASKED]`; SQL also contains a fixed identity `[MASKED]`. |
| `APP_USER_PASSWORD`, `SPRING_DATASOURCE_PASSWORD`, `spring.datasource.password` | Application database password | Local environment/`.env` → container environment; required for production-style Oracle configuration; all values `[MASKED]`. |
| `APP_ADMIN_USERNAME`, `app.admin.username` | HTTP Basic admin login identity | Compose/code defaults and test literals `[MASKED]`. |
| `APP_ADMIN_PASSWORD`, `app.admin.password` | HTTP Basic admin password | Compose requires operator input, but non-Compose startup has a literal source fallback `[MASKED]`; test literal `[MASKED]`. |
| Test `spring.datasource.username` / `spring.datasource.password` | H2 test credentials | `application-test.properties:4-5`, `[MASKED]`; password is empty, not reproduced as a usable value. |
| `POSTGRES_ADMIN_USER`, `POSTGRES_APP_USER` | Azure database login identities | Environment or script defaults `[MASKED]`. |
| `POSTGRES_ADMIN_PASSWORD`, `POSTGRES_APP_PASSWORD` | Azure database passwords | Environment or generated values `[MASKED]`; passed to Azure CLI/SQL statements. |
| `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_CONNECTION_STRING` | Exported application credentials/connection string | Process environment and plaintext generated root `.env`, `[MASKED]`. |
| AKS SSH key material | Cluster setup credential | Azure CLI `--generate-ssh-keys`; actual generated key locations/material not inspected. |
| ACR administrator credentials | Registry credential capability | Administrator access enabled; actual values not retrieved. AKS uses explicit registry attachment. |
| `COPILOT_ASSIGN_TOKEN` | GitHub automation token reference | GitHub Actions secrets; referenced by `squad-heartbeat.yml` and `squad-issue-assign.yml`; `[MASKED]`. |
| `GITHUB_TOKEN` | GitHub workflow token reference | GitHub Actions; explicit secret references in heartbeat, insider-release, promote and release workflows; `[MASKED]`. |
| `TRELLO_API_KEY`, `TRELLO_TOKEN` | Optional tooling API credentials | `.copilot/mcp-config.json` example fields `[MASKED]`; not used by the application. |

Risks observed: literal development admin fallbacks remain usable outside Compose unless overridden; test/example credential values must not be reused; generated Azure `.env` contains plaintext credentials; provisioning commands embed credentials in command arguments/SQL; environment values are accessible to suitably privileged host/container operators. Git-ignore prevents ordinary tracking, not filesystem disclosure or accidental log exposure. ACR admin access expands the credential surface. Azure setup writes its own `.env` contents rather than merging Oracle/admin Compose settings.

### Secrets Provisioning Workflow

- **Local containers:** operator copies `.env.example` to ignored `.env` and supplies new secret values → Compose interpolation validates required password variables → Oracle image receives administrator/application credentials → Java receives matching datasource credentials and HTTP Basic admin credentials. `create-user.sh` uses database administrator credentials to create the application account if absent; SQL initialization grants schema creation privileges. No secret manager or managed-identity database authentication is configured.
- **Application authentication:** `SecurityConfig` builds one in-memory admin account and BCrypt-encodes its supplied password during bean initialization. HTTP Basic is stateless; CSRF is explicitly disabled. BCrypt protects the in-memory encoded password, not the original environment/property secret; HTTPS/TLS termination is not configured in the inspected application/container files.
- **Azure provisioning:** preauthenticated Azure CLI identity → infrastructure creation → AKS ACR attachment → PostgreSQL administrator password from environment or generated random value → application account/password and SQL grants → process environment and ignored plaintext `.env`. Script generation uses `RandomNumberGenerator`, with a default length of 24. No Key Vault, encrypted property workflow, Kubernetes Secret binding, database managed identity, or explicit workload RBAC assignment is shown. Azure CLI identity type and its granted permissions are not declared by the script.
- **Configuration gap:** generated `POSTGRES_*` names do not automatically bind to `spring.datasource.*`; application properties and Maven dependencies remain Oracle-oriented. The script constructs a PostgreSQL JDBC URL but no inspected workload consumes it. Treat Azure provisioning output as separate infrastructure configuration, not evidence of a completed database migration or deployment.
- **Repository/tooling:** GitHub-hosted token references are used by repository automation; optional MCP fields are an example. Neither provides application database/admin secrets.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| Dedicated feature-flag framework / remote rollout flags | None discovered | No LaunchDarkly, Unleash, feature-management configuration or A/B rollout settings found. |
| `@ConditionalOnProperty`, `@ConditionalOnExpression`, `@Profile` application selectors | None discovered | Inspected application Java source contains no such selectors. |
| `spring.servlet.encoding.enabled`, `spring.servlet.encoding.force` | `true` | Base/Docker property files or Spring external overrides; technical configuration toggles, not business flags. |
| `spring.jpa.show-sql`, `spring.jpa.properties.hibernate.format_sql` | `true`; test overrides `show-sql=false` | Property files and external overrides; technical logging switches. |
| Azure-reset `Force`, `ACROnly`, `AKSOnly` | Optional switches, inactive when omitted | `azure-reset.ps1` command-line parameters; cleanup controls, not runtime flags. |

Upload size/MIME/count settings are configuration values, not documented rollout flags. `MAX_IMAGE_PIXELS=40000000` is a nonexternalized source constant in `PhotoServiceImpl.java:35`.

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Spring Boot parent/framework/starter management | `2.7.18` | `pom.xml:8-12`; starters have no independent version declarations. |
| Java language/compiler target | Java `8` / `1.8` | `pom.xml:23-26`. |
| Maven container build tool | `3.9.6` | Docker build image `maven:3.9.6-eclipse-temurin-8`. No Maven wrapper found; host Maven version unspecified. |
| Java build runtime | Eclipse Temurin `8` | Docker build image; exact JDK patch unpinned. |
| Java container runtime | Eclipse Temurin `8-jre` | `Dockerfile:17`; exact patch unpinned. |
| Application artifact | `1.0.0` | `pom.xml:17`; JAR packaging. |
| Commons IO | `2.11.0` | `pom.xml:68-73`. |
| Spring Security / Spring Framework / Hibernate / Thymeleaf / Jackson | Spring Boot parent-managed; resolved versions not independently verified | Starter declarations in `pom.xml`; no local version overrides or resolved dependency report inspected. |
| Oracle JDBC `ojdbc8` | Parent-managed; resolved version not independently verified | `pom.xml:49-54`, runtime scope. |
| H2 and test libraries | Parent-managed; resolved versions not independently verified | `pom.xml:81-93`, test scope. |
| Spring Boot DevTools | Parent-managed | `pom.xml:95-100`; optional dependency. |
| Oracle container | `gvenzl/oracle-free:latest` | `docker-compose.yml:4`; comment identifies Oracle Free 23ai, but mutable `latest` does not pin a database release. |
| Oracle in README | XE `21.3.0-xe` / 21c | README documents a different image than current Compose; not authoritative for the active container. |
| Azure PostgreSQL | `15` | `azure-setup.ps1:123`; provisioned infrastructure, not current application's JDBC dependency. |
| Bootstrap | `5.3.0` | CDN links in `index.html`, `detail.html`, `layout.html`. |
| Docker / Compose / Azure CLI / kubectl / PowerShell | Not pinned | Used by Dockerfile, Compose, operational documentation and provisioning/cleanup scripts. |
| Optional Trello MCP / Node tooling | Package/runtime version not pinned | `.copilot/mcp-config.json` uses `npx -y @trello/mcp-server`; tooling only. |

> Note: This is a source/configuration inventory, not a live environment audit. Parent-managed resolved dependency versions, deployed Azure state, actual secret values and host tool versions were not retrieved.
