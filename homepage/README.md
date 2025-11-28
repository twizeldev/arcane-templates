# Homepage Docker Stack Template

A modern, fully static, fast, secure fully proxied, highly customizable application dashboard with integrations for over 100 services and translations into multiple languages. Easily configured via YAML files or through docker label discovery.

[Official Github Repo](https://github.com/gethomepage/homepage)

This template provides both homepage and docker socket proxy for more secure docker integration but requires some manual setup after install.

---

## Requirements

* Docker & Docker Compose installed
* Linux host (preferred for UID/GID compatibility)
* Basic knowledge of Docker and networking

---

## Setup
### 1. Use template within Arcane

Ensure to configure the appropriate environment variables for your setup

### 2. Configure docker connection

Edit the docker.yaml file within your homepage config directory and add the following:
```yaml
local-docker:
  host: homepage-dsp
  port: 2375
```
