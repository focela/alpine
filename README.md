
# Focela Alpine: Lightweight and Flexible Docker Image

[![GitHub release](https://img.shields.io/github/v/tag/focela/alpine?style=flat-square)](https://github.com/focela/alpine/releases/latest)
[![Build Status](https://img.shields.io/github/actions/workflow/status/focela/alpine/main.yml?branch=main&style=flat-square)](https://github.com/focela/alpine/actions)
[![Docker Stars](https://img.shields.io/docker/stars/focela/alpine.svg?style=flat-square&logo=docker)](https://hub.docker.com/r/focela/alpine/)
[![Docker Pulls](https://img.shields.io/docker/pulls/focela/alpine.svg?style=flat-square&logo=docker)](https://hub.docker.com/r/focela/alpine/)
[![Become a sponsor](https://img.shields.io/badge/sponsor-focela-181717.svg?logo=github&style=flat-square)](https://github.com/sponsors/focela)
[![Paypal Donate](https://img.shields.io/badge/donate-paypal-00457c.svg?logo=paypal&style=flat-square)](https://www.paypal.me/focela)

---

## Table of Contents
1. [About](#about)
2. [Features](#features)
3. [Installation](#installation)
    - [Build from Source](#build-from-source)
    - [Prebuilt Images](#prebuilt-images)
    - [Multi Architecture Support](#multi-architecture-support)
4. [Available Tags](#available-tags)

---

## About

A lightweight and flexible [Alpine Linux](https://www.alpinelinux.org/) container image optimized for various use cases such as monitoring, logging, scheduling, and security. This image integrates essential tools to simplify container management.

---

## Features

- **Init System**: [s6 overlay](https://github.com/just-containers/s6-overlay) for PID 1 init capabilities.
- **Monitoring**: Includes [Zabbix Agent](https://zabbix.org) (Classic and Modern) for container monitoring.
- **Scheduling**: Integrated `cron` for task automation.
- **Utilities**: Comes with helpful tools like `bash`, `curl`, `less`, `logrotate`, `nano`, and `vi`.
- **Messaging**: Built-in MSMTP for sending emails via an external SMTP server.
- **Firewall**: Configured with [Fail2ban](https://github.com/fail2ban/fail2ban) to block malicious hosts based on log analysis.
- **Logging**: Supports log shipping to remote servers using [Fluent-Bit](https://github.com/fluent/fluent-bit).
- **Permission Management**: Dynamically updates User ID and Group ID permissions.

---

## Installation

### Build from Source
To build the image locally:
```bash
docker build <arguments> (imagename) .
```

### Prebuilt Images
Prebuilt images are available on [Docker Hub](https://hub.docker.com/r/focela/alpine):
```bash
docker pull docker.io/focela/alpine:(imagetag)
```

Alternatively, images are also hosted on the [GitHub Container Registry](https://github.com/focela/docker-alpine/pkgs/container/docker-alpine):
```bash
docker pull ghcr.io/focela/alpine:(imagetag)
```

---

### Multi Architecture Support
This image primarily supports `amd64` architecture. Variants for `arm/v7`, `arm64`, and others may be available but are unsupported. To verify architecture compatibility:
```bash
docker manifest inspect (image):(tag)
```

---

## Available Tags

| Alpine Version | Tag     |
|----------------|---------|
| `edge`         | `:edge` |
| `3.20`         | `:3.20` |
| `3.19`         | `:3.19` |
| `3.18`         | `:3.18` |
| `3.17`         | `:3.17` |
| `3.16`         | `:3.16` |
| `3.15`         | `:3.15` |
| `3.14`         | `:3.14` |
| `3.13`         | `:3.13` |
| `3.12`         | `:3.12` |
| `3.11`         | `:3.11` |
| `3.10`         | `:3.10` |
| `3.9`          | `:3.9`  |
| `3.8`          | `:3.8`  |
| `3.7`          | `:3.7`  |
| `3.6`          | `:3.6`  |
| `3.5`          | `:3.5`  |

---

