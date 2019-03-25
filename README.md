archwrt-ss.sh
---

A simple Shadowsocks transparent proxy setup script.

## Depends

* shadowsocks-libev
* simple-obfs (optional)
* shadowsocks-v2ray-plugin (optional)
* dnsmasq
* ipset
* iptables
* bind-tools
* [AdguardTeam/dnsproxy](https://github.com/AdguardTeam/dnsproxy) - [PKGBUILD](https://github.com/archwrt/repo/tree/master/archwrt/dnsproxy)



## Usage

```
$ archwrt-ss.sh --help
Info:
  Contibuted by monlor & edward-p
Usage:
  archwrt-ss.sh {Command} {Option}
Commands:
  start | stop | restart | status | config | update
Options:
  gfwlist | bypass | gamemode | global
Example:
  archwrt-ss.sh start bypass          Start with bypass mode
  archwrt-ss.sh restart gfwlist       Restart with gfwlist mode
  archwrt-ss.sh start                 Start with default mode[gfwlist]
  archwrt-ss.sh config                Modify server config
  archwrt-ss.sh update                Update rules
```

## Installation

```
$ git clone https://github.com/archwrt/archwrt-ss.sh
$ cd archwrt-ss.sh
$ sudo install -Dm755 archwrt-ss.sh /usr/bin/archwrt-ss.sh
$ sudo install -Dm644 archwrt-ss.conf /opt/archwrt-ss/archwrt-ss.conf
$ sudo install -Dm644 archwrt-ss.service /usr/lib/systemd/system/archwrt-ss.service
$ sudo systemctl daemon-reload
```

## Start

Before using `systemctl start archwrt-ss.service`, you need a valid `config.json` for shadowsocks, the following command will start a wizzard for that.

```
$ sudo archwrt-ss.sh config
```

When it is done, your `config.json` will be located at `/opt/archwrt-ss/config.json`.

It is recommend to check if there's any error in your `config.json` by running:

```
$ ss-redir -c /opt/archwrt-ss/config.json
```

Not yet, you may want to have a look on `/opt/archwrt-ss/archwrt-ss.conf`. Change some configs if you like.

Now you can start by

```
$ sudo systemctl start archwrt-ss.service
```

For auto start

```
systemctl enable archwrt-ss.service
```

