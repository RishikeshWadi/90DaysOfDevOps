# Week 1: Networking Challenge
## Task 2

**Protocols and Ports for DevOps**
Networking Protocols and Ports enable communication between systems, ensure secure data transmission, and facilitate automation.

**Hypertext Transfer Protocol (HTTP)**
  - used to transfer data over the web, web communication, transferring web pages, and REST API interactions.
  - **Port** 80 (Port 80 is the default port for HTTP traffic.)
  - *Example:*
    - Enables CI/CD pipelines to interact with web applications.
    - Used for monitoring services and fetching build artifacts.
---
**Hypertext Transfer Protocol Secure (HTTPS)**
  - Secure version of HTTP that encrypts communication using SSL/TLS.
  - **Port:** 443
  - *Example:*
    - Ensures secure API interactions.
    - Critical for deploying applications securely over the web
---
**File Transfer Protocol (FTP)**
  - FTP is used to transfer files between systems over a network.
  - **Port:** 21
  - *Example:*
    - Used for automating file transfers in legacy systems.
    - Sometimes used for deploying artifacts in non-cloud environments.
---
**Secure Shell (SSH)**
  - SSH is used to provide secure remote access to systems.
  - **Port:** 22
  - *Example:*
    - Essential for automating deployments and managing infrastructure.
    - Used in remote server administration and configuration management.
---
**Domain Name System (DNS)**
  - resolves and translates domain names into IP addresses
  - **Port:** 53
  - *Example:*
    - Used in service discovery for microservices.
    -  Helps automate DNS configurations in infrastructure-as-code setups.
---
**Simple Mail Transfer Protocol (SMTP)**
  - Sends emails between mail servers.
  - **Port:** 25
  - *Example:*
   - Used for sending automated notifications and alerts from CI/CD pipelines.
---
**Lightweight Directory Access Protocol (LDAP)**
  - Manages and accesses directory information.
  - **Port:** 389 (unencrypted), 636 (SSL/TLS encrypted)
  - *Example:*
    - Used for authentication and access control in DevOps pipelines.
---
**Network Time Protocol (NTP)**
  - Synchronizes system clocks.
  - **Port:** 123
  - *Example:*
    - Ensures time consistency across distributed systems and logs.