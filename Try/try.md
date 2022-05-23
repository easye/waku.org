
Run a node

By running your own node you provide additional nodes for the Status community. We encourage anyone to publish the enode addresses of their nodes for others to use.

We also recommend running them as a permanent service or a docker container, so that it keeps running after system restart or a runtime node error.
Types of node
relay node

A regular Waku Node which relays messages between nodes, including mobile or desktop clients.
history node

Also known as a Mailserver, stores historical messages and delivers them when queried. Around 1 GB of free space would be a start for storing last 30 days.
Running a status node

Status Node is a modified go-ethereum node called status-go running on a server and supporting the Status app. As we operate in a decentralized model, we need multiple peers scattered around the globe to provide a reliable service.

When correctly configured a Status Node supports relaying Waku messages - helps propagate them between nodes - and storing them for devices that were offline when it was sent.
Requirements

A machine running Linux or MacOS is required. It is entirely possible to run a Status Node on a physical machine in a local network, but for full functionality it would require a public and static IP address via which the service can be accessed.

An alternative would be to use a cloud service provider which would provide you with a public and static IP out of the box in most cases. Using a cloud service would also provide you with the high uptime necessary to collect as many envelopes as possible for later retrieval.

A single instance with 1GB of RAM and 1 vCPU should be enough to run Status Node reliably.

In terms of software the minimum would include make and jq.
If you want to build status-go you will also need golang, version 1.13 or higher. A nice-to-have is qrencode to display a QR Code with your enode:// adress.

For Ubuntu 20.04 you can just do:
```sudo apt install make jq golang qrencode
Ports
8545

TCP - JSON RPC management port.

Must NEVER be public.
30303

TCP/UDP - DevP2P wire protocol port.

Must ALWAYS be public.
9090

TCP - Prometheus metrics port.

Should not be public.
Quick Start

The quickest way to start a node is using our Makefile scripts. You can read about that here.

In simple terms you clone the status-go repo and run:
make run-mailserver-docker or make run-mailserver-systemd
Building

First you’ll have to build a 20.04 binary.

```r ~/go/src/github.com/status-im

git clone https://github.com/status-im/status-go

~/go/src/github.com/status-im/status-go

cd ~/go/src/github.com/status-im/status-go

make statusgo```
Running

You can check the available options using the -h / --help flags

./build/bin/statusd -h

Configuration

The configuration is provided as a JSON file. A basic config that will let you run a Waku node 
that also stores historical messages would look like this: ./config.json


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
            

