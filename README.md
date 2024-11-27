
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
   - [Getting Started](#getting-started)
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

### Getting Started
You can use this image either by building it locally or pulling prebuilt images from trusted registries.

#### Build from Source
If you want to build the image locally:
```bash
docker build <arguments> (imagename) .
```

#### Prebuilt Images
Prebuilt images are available in the following registries:

- **Docker Hub**:
  ```bash
  docker pull docker.io/focela/alpine:(imagetag)
  ```

- **GitHub Container Registry**:
  ```bash
  docker pull ghcr.io/focela/alpine:(imagetag)
  ```

### Multi Architecture Support
This image is primarily built for `amd64` architecture. Variants for `arm/v7`, `arm64`, and others are available but not officially supported.

To verify the architecture compatibility of a specific image:
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

## Configuration

### Quick Start

Use this image as a base for your builds. For more details on enabling the S6 init system, visit the [s6 overlay repository](https://github.com/just-containers/s6-overlay). You can also refer to other images based on this setup for additional examples.

### Persistent Storage

The following directories can be mapped to the host machine to retain configuration and log files:

| Directory                           | Description                               |
| ----------------------------------- | ----------------------------------------- |
| `/etc/fluent-bit/conf.d/`           | Fluent-Bit custom configuration directory |
| `/etc/fluent-bit/parsers.d/`        | Fluent-Bit custom parsers directory       |
| `/etc/zabbix/zabbix_agentd.conf.d/` | Zabbix Agent configuration directory      |
| `/etc/fail2ban/filter.d`            | Custom Fail2ban filter configuration      |
| `/etc/fail2ban/jail.d`              | Custom Fail2ban jail configuration        |
| `/var/log`                          | Logs for container, cron, Zabbix, etc.    |
| `/assets/cron`                      | Drop custom crontabs here                 |
| `/assets/iptables`                  | Drop custom IPTables rules here           |

**Note:** Mapping these directories ensures data persistence between container restarts.

### Environment Variables

Below is a list of variables available for customizing the container. Variables marked with 'x' in the `_FILE` column can load values from files, which is useful for managing sensitive information.

#### **Container Options**

| Parameter                             | Description                                                                                                                           | Default                            |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| `CONTAINER_ENABLE_LOG_TIMESTAMP`      | Add timestamps to container logs                                                                                                      | `TRUE`                             |
| `CONTAINER_COLORIZE_OUTPUT`           | Enable/Disable colorized console output                                                                                               | `TRUE`                             |
| `CONTAINER_CUSTOM_BASH_PROMPT`        | Set a custom bash prompt (e.g., '(imagename):(version) HH:MM:SS # ')                                                                  |                                    |
| `CONTAINER_CUSTOM_PATH`               | Path to custom files loaded at startup                                                                                               | `/assets/custom`                   |
| `CONTAINER_CUSTOM_SCRIPTS_PATH`       | Path to custom scripts executed at startup                                                                                           | `/assets/custom-scripts`           |
| `CONTAINER_ENABLE_PROCESS_COUNTER`    | Display the execution count of a process in logs                                                                                     | `TRUE`                             |
| `CONTAINER_LOG_LEVEL`                 | Log level (`INFO`, `WARN`, `NOTICE`, `DEBUG`)                                                                                        | `NOTICE`                           |
| `CONTAINER_LOG_PREFIX_TIME_FMT`       | Format for log timestamps (time)                                                                                                      | `%H:%M:%S`                         |
| `CONTAINER_LOG_PREFIX_DATE_FMT`       | Format for log timestamps (date)                                                                                                      | `%Y-%m-%d`                         |
| `CONTAINER_LOG_PREFIX_SEPERATOR`      | Separator for timestamp components                                                                                                    | `-`                                |
| `CONTAINER_LOG_FILE_LEVEL`            | Log level for internal container logs                                                                                                | `DEBUG`                            |
| `CONTAINER_LOG_FILE_NAME`             | File name for container logs                                                                                                         | `/var/log/container/container.log` |
| `CONTAINER_LOG_FILE_PATH`             | Path for container logs                                                                                                              | `/var/log/container/`              |
| `CONTAINER_LOG_PREFIX_TIME_FMT`       | Format for log timestamps (time)                                                                                                      | `%H:%M:%S`                         |
| `CONTAINER_LOG_PREFIX_DATE_FMT`       | Format for log timestamps (date)                                                                                                      | `%Y-%m-%d`                         |
| `CONTAINER_LOG_PREFIX_SEPARATOR`      | Separator for timestamp components                                                                                                    | `-`                                
| `CONTAINER_NAME`                      | Custom container name for monitoring and log shipping                                                                                | (hostname)                         |
| `CONTAINER_POST_INIT_COMMAND`         | Commands to run after all services have initialized (comma-separated)                                                                |                                    |
| `CONTAINER_POST_INIT_SCRIPT`          | Scripts to execute after all services have initialized (comma-separated paths)                                                       |                                    |
| `TIMEZONE`                            | Set container timezone                                                                                                               | `Etc/GMT`                          |

**Example Usage:**
To set a post-initialization script:
```bash
docker run -e CONTAINER_POST_INIT_SCRIPT="/assets/scripts/init.sh" my-container
