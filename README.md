
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

Utilize this image as a base for further builds. Please visit the [s6 overlay repository](https://github.com/just-containers/s6-overlay) for
instructions on how to enable the S6 init system when using this base or look at some of my other images
which use this as a base.

### Persistent Storage

The following directories are used for configuration and can be mapped for persistent storage.

| Directory                           | Description                               |
| ----------------------------------- | ----------------------------------------- |
| `/etc/fluent-bit/conf.d/`           | Fluent-Bit custom configuration directory |
| `/etc/fluent-bit/parsers.d/`        | Fluent-Bit custom parsers directory       |
| `/etc/zabbix/zabbix_agentd.conf.d/` | Zabbix Agent configuration directory      |
| `/etc/fail2ban/filter.d`            | Custom Fail2ban Filter configuration      |
| `/etc/fail2ban/jail.d`              | Custom Fail2ban Jail configuration        |
| `/var/log`                          | Container, Cron, Zabbix, other log files  |
| `/assets/cron`                      | Drop custom crontabs here                 |
| `/assets/iptables`                  | Drop custom IPTables rules here           |

### Environment Variables

Below is the complete list of available options that can be used to customize your installation.
Variables showing an 'x' under the `_FILE` column can be used for storing the information inside of a file, useful for secrets.

#### Container Options
| Parameter                             | Description                                                                                                                           | Default                            |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| `CONAINER_ENABLE_LOG_TIMESTAMP`       | Prefix this images container logs with timestamp                                                                                      | `TRUE`                             |
| `CONTAINER_COLORIZE_OUTPUT`           | Enable/Disable colorized console output                                                                                               | `TRUE`                             |
| `CONTAINER_CUSTOM_BASH_PROMPT`        | If you wish to set a different bash prompt then '(imagename):(version) HH:MM:SS # '                                                   |                                    |
| `CONTAINER_CUSTOM_PATH`               | Used for adding custom files into the image upon startup                                                                              | `/assets/custom`                   |
| `CONTAINER_CUSTOM_SCRIPTS_PATH`       | Used for adding custom scripts to execute upon startup                                                                                | `/assets/custom-scripts`           |
| `CONTAINER_ENABLE_PROCESS_COUNTER`    | Show how many times process has executed in console log                                                                               | `TRUE`                             |
| `CONTAINER_LOG_LEVEL`                 | Control level of output of container `INFO`, `WARN`, `NOTICE`, `DEBUG`                                                                | `NOTICE`                           |
| `CONTAINER_LOG_PREFIX_TIME_FMT`       | Timestamp Time Format                                                                                                                 | `%H:%M:%S`                         |
| `CONTAINER_LOG_PREFIX_DATE_FMT`       | Timestamp Date Format                                                                                                                 | `%Y-%m-%d`                         |
| `CONTAINER_LOG_PREFIX_SEPERATOR`      | Timestamp seperator                                                                                                                   | `-`                                |
| `CONTAINER_LOG_FILE_LEVEL`            | Control level of output of container `INFO`, `WARN`, `NOTICE`, `DEBUG`                                                                | `DEBUG`                            |
| `CONTAINER_LOG_FILE_NAME`             | Internal Container Logs filename                                                                                                      | `/var/log/container/container.log` |
| `CONTAINER_LOG_FILE_PATH`             | Path where to find the internal container logs                                                                                        | `/var/log/container/`              |
| `CONTAINER_LOG_FILE_PREFIX_TIME_FMT`  | Timestamp Time Format                                                                                                                 | `%H:%M:%S`                         |
| `CONTAINER_LOG_FILE_PREFIX_DATE_FMT`  | Timestamp Date Format                                                                                                                 | `%Y-%m-%d`                         |
| `CONTAINER_LOG_FILE_PREFIX_SEPERATOR` | Timestamp seperator                                                                                                                   | `-`                                |
| `CONTAINER_NAME`                      | Used for setting entries in Monnitoring and Log Shipping                                                                              | (hostname)                         |
| `CONTAINER_POST_INIT_COMMAND`         | If you wish to execute a command in the container after all services have initialized enter it here. Seperate multiple by commas      |                                    |
| `CONTAINER_POST_INIT_SCRIPT`          | If you wish to execute a script in the container after all services have initialized enter the path here. Seperate multiple by commas |                                    |
| `TIMEZONE`                            | Set Timezone                                                                                                                          | `Etc/GMT`                          |
