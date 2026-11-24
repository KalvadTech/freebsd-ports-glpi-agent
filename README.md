# freebsd-ports-glpi-agent

A FreeBSD port for the [GLPI Agent](https://github.com/glpi-project/glpi-agent), forked from
<https://codeberg.org/mazhe/freebsd-ports-glpi-agent>.

## Status

This repository is a playground port. It is not an official FreeBSD port.

- Port: `net-mgmt/glpi-agent`
- Version: `1.21`
- Upstream: <https://github.com/glpi-project/glpi-agent>
- Original port maintainer: `mazhe@alkumuna.eu`
- Tested: `env BATCH=yes make package` and package install/inventory run on FreeBSD 15.1-RELEASE (amd64, Incus VM)

## Repository layout

```text
net-mgmt/glpi-agent/
  Makefile
  distinfo
  pkg-descr
  pkg-plist
  files/
    glpi_agent.in
```

## Build and install

Build this port inside a FreeBSD ports tree.

```sh
# Clone the FreeBSD ports tree if it is not present
git clone --depth 1 https://git.freebsd.org/ports.git /usr/ports

# Copy this port into the ports tree
mkdir -p /usr/ports/net-mgmt/glpi-agent
cp -R net-mgmt/glpi-agent/* /usr/ports/net-mgmt/glpi-agent/

# Build and install
cd /usr/ports/net-mgmt/glpi-agent
env BATCH=yes make install clean
```

To build a package only:

```sh
cd /usr/ports/net-mgmt/glpi-agent
env BATCH=yes make package
```

When you change `DISTVERSION`, update checksums:

```sh
cd /usr/ports/net-mgmt/glpi-agent
make makesum
```

## Port options

Options defined in `net-mgmt/glpi-agent/Makefile`:

| Option | Default | Description |
|---|---:|---|
| `CUPS` | off | Add CUPS support for inventory |
| `DAEMON` | on | Install rc.d script |
| `HTTPS` | on | Add HTTPS support |
| `WEBSERVER` | off | Add embedded web server support |

Task options (`OPTIONS_GROUP_TASKS`):

| Option | Default | Description |
|---|---:|---|
| `COLLECT` | off | Collect task |
| `DEPLOY` | off | Deploy task |
| `ESX` | off | ESX task |
| `INVENTORY` | on | Inventory task |
| `NETDISCOVERY` | off | NetDiscovery task |
| `NETINVENTORY` | off | NetInventory task |
| `REMOTEINVENTORY` | off | RemoteInventory task |
| `WAKEONLAN` | off | WakeOnLan task |

## Service

The rc.d script is `files/glpi_agent.in`. When the `DAEMON` option is enabled, the port installs it as `glpi_agent`.

Example configuration in `/etc/rc.conf`:

```sh
glpi_agent_enable="YES"
```

Start the service:

```sh
service glpi_agent start
```

## Notes

- The port installs the configuration sample as `%%ETCDIR%%/agent.cfg.sample`.
- `LOCALSTATEDIR` is set to `/var/glpi-agent`.
- The upstream GLPI Agent project issue for BSD packaging is [glpi-project/glpi-agent#164](https://github.com/glpi-project/glpi-agent/issues/164).
