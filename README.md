<p align="center">
  <img src="branding/logo.jpg" alt="Alfresco Process Services SDK Logo" width="160" style="border-radius: 24px;" />
</p>

<h1 align="center">Alfresco Process Services SDK Project (APS SDK 3.x)</h1>

<p align="center">
  <a href="https://github.com/OpenPj/alfresco-process-services-project-sdk/releases"><img src="https://img.shields.io/github/v/release/OpenPj/alfresco-process-services-project-sdk?logo=github&color=blue" alt="GitHub Release" /></a>
  <a href="LICENSE.txt"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg?logo=apache" alt="License" /></a>
  <a href="https://openjdk.org/"><img src="https://img.shields.io/badge/Java-17%20%7C%2021-orange.svg?logo=openjdk&logoColor=white" alt="Java" /></a>
  <a href="https://maven.apache.org/"><img src="https://img.shields.io/badge/Maven-3.9%2B-C71A36.svg?logo=apachemaven&logoColor=white" alt="Maven" /></a>
  <a href="https://www.docker.com/"><img src="https://img.shields.io/badge/Docker-Multi--Arch%20(x86__64%20%7C%20ARM64)-2496ED.svg?logo=docker&logoColor=white" alt="Docker Multi-Arch" /></a>
  <a href="https://github.com/OpenPj/alfresco-process-services-project-sdk/wiki/Supported-APS-Versions-and-Maven-Profiles"><img src="https://img.shields.io/badge/APS-24.x%20%7C%2025.x%20%7C%2026.x-009900.svg" alt="APS Support" /></a>
  <a href="https://github.com/OpenPj/alfresco-process-services-project-sdk/wiki"><img src="https://img.shields.io/badge/Documentation-Wiki-informational.svg?logo=github" alt="Wiki Documentation" /></a>
  <a href="https://github.com/OpenPj/alfresco-process-services-project-sdk/stargazers"><img src="https://img.shields.io/github/stars/OpenPj/alfresco-process-services-project-sdk?style=flat&logo=github" alt="GitHub Stars" /></a>
  <a href="https://github.com/OpenPj/alfresco-process-services-project-sdk/issues"><img src="https://img.shields.io/github/issues/OpenPj/alfresco-process-services-project-sdk?logo=github" alt="GitHub Issues" /></a>
  <a href="https://www.ziaconsulting.com"><img src="https://img.shields.io/badge/Enterprise%20Support-Zia%20Consulting-red.svg" alt="Enterprise Support" /></a>
</p>

The **Alfresco Process Services SDK (APS SDK)** is an enterprise development acceleration kit for building, extending, testing, and deploying custom solutions on **Alfresco Process Services (powered by Activiti)**.

---

## 📖 Full Documentation & Wiki

Comprehensive documentation, architecture deep dives, tutorials, and configuration guides are available on the project wiki:

👉 **[APS SDK GitHub Wiki](https://github.com/OpenPj/alfresco-process-services-project-sdk/wiki)**

### Quick Links to Wiki Guides:
* 🚀 **[Getting Started & Prerequisites](https://github.com/OpenPj/alfresco-process-services-project-sdk/wiki/Getting-Started-and-Prerequisites)** — JDK requirements, Nexus credentials, and license setup.
* 🏗️ **[Project Architecture & Modules](https://github.com/OpenPj/alfresco-process-services-project-sdk/wiki/Project-Architecture-and-Modules)** — Detailed breakdown of Maven submodules and build lifecycle.
* 💻 **[Development & Extension Guide](https://github.com/OpenPj/alfresco-process-services-project-sdk/wiki/Development-and-Extension-Guide)** — Writing Java delegates, listeners, Spring beans, REST APIs, and whitelisting.
* ⚡ **[Running & Deployment](https://github.com/OpenPj/alfresco-process-services-project-sdk/wiki/Running-and-Deployment)** — Run scripts command reference (`run.sh` / `run.bat`) and full Maven lifecycles.
* 🐳 **[Docker & Environment Configuration](https://github.com/OpenPj/alfresco-process-services-project-sdk/wiki/Docker-and-Environment-Configuration)** — Container topology, persistence volumes, Apple Silicon (ARM64) support, and remote debugging.
* 🧪 **[Testing Guide](https://github.com/OpenPj/alfresco-process-services-project-sdk/wiki/Testing-Guide)** — Embedded H2 unit tests and containerized Swagger integration tests.
* 📋 **[Supported APS Versions & Profiles](https://github.com/OpenPj/alfresco-process-services-project-sdk/wiki/Supported-APS-Versions-and-Maven-Profiles)** — Compatibility matrix covering APS 24.x through 26.x.

---

## Capabilities

* **Native ARM64 & Apple Silicon Support**: Native container execution on Apple Silicon (M1/M2/M3/M4) and x86_64 architectures without emulation overhead.
* **Persistent Storage Architecture**: Dedicated persistent Docker volumes for the database (`aps-db-volume`), contentstore attachments (`aps-contentstore-volume`), and Elasticsearch (`aps-es-volume`).
* **Dual Execution Modes**: Fast terminal run scripts (`./run.sh` / `run.bat`) or direct Maven lifecycles (`mvn clean install docker:build docker:start`).
* **Two-Tier Testing Framework**: Embedded in-memory H2 unit testing and end-to-end integration testing driven by an official Swagger/OpenAPI Java client.
* **Remote Debugging**: Out-of-the-box JDWP remote debugging over port `5005`.

---

## Submodules Overview

The project consists of four Maven submodules:

* **`aps-extensions-jar`**: Core Java module for custom business logic (`JavaDelegate`, listeners, Spring services, custom authenticated/public REST controllers, and embedded unit tests).
* **`activiti-app-overlay-war`**: Generates the final `activiti-app.war` overlay combining the enterprise base WAR from Alfresco with your `aps-extensions-jar`.
* **`activiti-app-overlay-docker`**: Builds the custom APS Docker image and orchestrates multi-container stacks (Tomcat, PostgreSQL, Elasticsearch, and optional Activiti Admin).
* **`activiti-app-integration-tests`**: End-to-end integration test suite interacting with live containers via the generated Swagger REST client.

---

## Prerequisites

1. **Java Development Kit**:
   * **OpenJDK 17** for APS versions `<= 25.x`
   * **OpenJDK 21** for APS versions `>= 26.x`
2. **Apache Maven**: version `3.9.0` or higher.
3. **Docker & Docker Compose**: Docker Desktop or Docker Engine with Docker Compose v2.
4. **License Files**: Place valid `activiti.lic` and `transform.lic` (or `Aspose.Total.Java.lic`) into the root `/license/` directory.
5. **Alfresco Nexus Credentials**: Configure `~/.m2/settings.xml` with your Alfresco customer or partner repository credentials:

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                              https://maven.apache.org/xsd/settings-1.0.0.xsd">
  <servers>
    <server>
      <id>activiti-enterprise-releases</id>
      <username>yourAlfrescoUsername</username>
      <password>yourAlfrescoPassword</password>
    </server>
    <server>
      <id>enterprise-releases</id>
      <username>yourAlfrescoUsername</username>
      <password>yourAlfrescoPassword</password>
    </server>
    <server>
      <id>internal-thirdparty</id>
      <username>yourAlfrescoUsername</username>
      <password>yourAlfrescoPassword</password>
    </server>
  </servers>
</settings>
```

---

## Quickstart: Run Scripts

Run scripts simplify everyday development:
* **Linux / macOS**: `./run.sh <command>`
* **Windows**: `run.bat <command>`

### Common Commands:

| Command | Description |
| :--- | :--- |
| `./run.sh build_start` | Clean build, provision volumes, start containers, and stream logs |
| `./run.sh reload_aps` | Fast rebuild of extensions and WAR without resetting DB or ES |
| `./run.sh start` | Start existing containers without rebuilding |
| `./run.sh stop` | Stop all running containers |
| `./run.sh purge` | Remove all persistent Docker volumes |
| `./run.sh tail` | Follow container logs in real time |
| `./run.sh build_test` | Build, start containers, execute integration tests, and shut down |
| `./run.sh test` | Run unit tests for `aps-extensions-jar` |

*Append `_admin` to any command (e.g. `./run.sh build_start_admin`) to include the Activiti Admin console.*

---

## Quickstart: Full Maven Lifecycle

### Build, Package, and Deploy Stack:
```bash
mvn clean install docker:build docker:start
```

### Stop Containers:
```bash
mvn docker:stop
```

### Deploy Stack with Activiti Admin Console:
```bash
mvn clean install docker:build docker:start -Pactiviti-admin
```

To stop with admin:
```bash
mvn docker:stop -Pactiviti-admin
```

### Subsequent Fast Builds (Skipping Admin Rebuild):
```bash
mvn clean install docker:build docker:start -Pactiviti-admin,skip.admin
```

### Purge Persistent Volumes:
```bash
mvn clean -Ppurge-volumes
```

---

## Remote Debugging

Remote debugging is enabled by default via port **`5005`** on the `aps-current-project` container:
* **Host**: `localhost`
* **Port**: `5005`
* **JDWP Transport**: `dt_socket`

To disable remote debugging for production, comment the `CATALINA_OPTS` and debug port mapping in `activiti-app-overlay-docker/pom.xml`.

---

## Extension Conventions & Packages

Develop your business logic in `aps-extensions-jar`:

* `com.activiti.extension.api`: Authenticated enterprise REST endpoints (`/api/enterprise/...`).
* `com.activiti.extension.rest`: Public / internal utility endpoints (`/app/rest/...`).
* `com.activiti.extension.bean`: Shared Spring components and services.
* `com.activiti.extension.<app>.service.tasks`: BPMN Service Tasks implementing `JavaDelegate`.
* `com.activiti.extension.<app>.listeners`: Execution and Task listeners.
* `org.alfresco.activiti.unit.tests`: Embedded unit tests (`*Test.java`).

---

## Supported APS Versions

Select an APS version by passing its profile flag (e.g. `-Paps26.2.0`):

| APS Version | Profile ID | Required JDK |
| :--- | :--- | :--- |
| **26.2.0** *(default)* | `aps26.2.0` | **Java 21** |
| **26.1.0** | `aps26.1.0` | **Java 21** |
| **25.5.0** | `aps25.5.0` | **Java 17** |
| **25.4.1** | `aps25.4.1` | **Java 17** |
| **25.4.0** | `aps25.4.0` | **Java 17** |
| **25.3.0** | `aps25.3.0` | **Java 17** |
| **25.2.4** | `aps25.2.4` | **Java 17** |
| **25.2.0 - 25.2.3** | `aps25.2.0` - `aps25.2.3` | **Java 17** |
| **25.1.0 - 25.1.1** | `aps25.1.0`, `aps25.1.1` | **Java 17** |
| **24.7.1** | `aps24.7.1` | **Java 17** |
| **24.7.0** | `aps24.7.0` | **Java 17** |
| **24.6.0** | `aps24.6.0` | **Java 17** |
| **24.5.0** | `aps24.5.0` | **Java 17** |
| **24.4.0 - 24.4.7** | `aps24.4.0` through `aps24.4.7` | **Java 17** |
| **24.3.0 - 24.3.1** | `aps24.3.0`, `aps24.3.1` | **Java 17** |
| **24.2.0 - 24.2.1** | `aps24.2.0`, `aps24.2.1` | **Java 17** |
| **24.1.0** | `aps24.1.0` | **Java 17** |

---

## Contributors

* **Piergiorgio Lucidi** (`piergiorgio@apache.org`) — Project Creator & Maintainer
* **Jeff Potts** — Documentation updates
* **Luca Stancapiano** — Testing & feature improvements
* **Bindu Wavell** — Testing & tooling extensions
* **Stanley Arnold** — Maven configuration enhancements

---

## Enterprise Support

This project is maintained as an open-source community effort. Enterprise maintenance, support, and consulting are provided by **TAI Solutions**.
