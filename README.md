# Akvorado: flow collector, enricher and visualizer &middot; [![Build status](https://img.shields.io/github/actions/workflow/status/akvorado/akvorado/ci.yml?branch=main&style=flat-square)](https://github.com/akvorado/akvorado/actions/workflows/ci.yml) [![Codecov](https://img.shields.io/codecov/c/github/akvorado/akvorado?style=flat-square)](https://codecov.io/gh/akvorado/akvorado) [![License](https://img.shields.io/github/license/akvorado/akvorado?style=flat-square)](LICENSE.txt) [![Latest release](https://img.shields.io/github/v/release/akvorado/akvorado?style=flat-square)](https://github.com/akvorado/akvorado/releases)

This program receives flows (currently Netflow/IPFIX and sFlow), enriches them
with interface names (using SNMP), geo information (using IPinfo.io),
and exports them to Kafka, then ClickHouse. It also exposes a web
interface to browse the collected data.

![Timeseries graph](console/data/docs/timeseries.png)

![Sankey graph](console/data/docs/sankey.png)

*Akvorado* is developed by [Free](https://www.free.fr), a French ISP,
and is licensed under the [AGPLv3 license](LICENSE.txt).

A demo site using fake data and running the latest stable version is
available on [demo.akvorado.net](https://demo.akvorado.net). It is the
direct result of running `docker compose up` on a fresh checkout but
port 2055 is not accessible (you cannot send you own flows). Please,
be gentle with this resource. The demo site also enables you to browse
the [documentation](https://demo.akvorado.net/docs) for the current version
(the one in `docs/` is for the next version).

By default, *Akvorado* is using [IPinfo](https://ipinfo.io) databases for
geolocation data.

Be aware that *Akvorado* is still young and should be considered as beta
quality. Be sure to always read the
[changelog](console/data/docs/99-changelog.md) before upgrading.

A [Grafana plugin](https://github.com/ovh/grafana-akvorado) is available.

## Installation

There are three ways to install **Akvorado**:

1. **Docker** (recommended for a quick start)

   Ensure Docker and Docker Compose are installed and run:

   ```console
   mkdir akvorado
   cd akvorado
   curl -sL https://github.com/akvorado/akvorado/releases/latest/download/docker-compose-quickstart.tar.gz | tar zxvf -
   docker compose up -d
   ```

   When `akvorado-console` is reported as *healthy* by `docker compose ps`, the
   web interface is available on port 8081.

2. **Pre-built binary**

   Download the archive from the [release page](https://github.com/akvorado/akvorado/releases) and
   extract it:

   ```console
   curl -L -o akvorado.tar.gz https://github.com/akvorado/akvorado/releases/latest/download/akvorado-linux-amd64.tar.gz
   tar xzf akvorado.tar.gz
   ./akvorado --help
   ```

3. **Build from source**

   Install [Go](https://go.dev/doc/install) 1.24+ and [NodeJS](https://nodejs.org/) 20+ with NPM.
   Then clone the repository and run `make`:

   ```console
   git clone https://github.com/akvorado/akvorado.git
   cd akvorado
   make
   ```

Kafka and ClickHouse need to be available in all cases. Refer to the
[documentation](docs/01-install.md) for additional details and configuration
options.
