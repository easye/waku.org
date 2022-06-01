---
title: Quick start
---
## overview
The quickest way to start a node is using our Makefile scripts. You can read about that [here](/run-a-node).

In simple terms you clone the [status-go](https://waku.org/node) repo and run:
```shell
make run-mailserver-docker
```
or
```shell
make run-mailserver-systemd
```

## Building
First you’ll have to build a `20.04` binary.
```shell
mkdir ~/go/src/github.com/status-im
git clone https://github.com/status-im/status-go
~/go/src/github.com/status-im/status-go
cd ~/go/src/github.com/status-im/status-go
make statusgo
```

## Running
You can check the available options using the `-h` / `--help` flags
```shell
./build/bin/statusd -h
```

## Configuration
The configuration is provided as a JSON file. A basic config that will let you run a Waku node that also stores historical messages would look like this: `./config.json`
```json
{
    "AdvertiseAddr": "< YOUR_PUBLIC_IP >",
    "ListenAddr": "0.0.0.0:30303",
    "HTTPEnabled": true,
    "HTTPHost": "127.0.0.1",
    "HTTPPort": 8545,
    "APIModules": "eth,net,web3,admin,mailserver",
    "RegisterTopics": ["whispermail"],
    "WakuConfig": {
      "Enabled": true,
      "EnableMailServer": true,
      "DataDir": "/var/tmp/statusd/waku",
      "MailServerPassword": "status-offline-inbox"
    }
}
```