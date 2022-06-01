---
title: Requirements
category: page
---
A machine running Linux or MacOS is required. It is entirely possible to run a Status Node on a physical machine in a local network, but for full functionality it would require a public and static IP address via which the service can be accessed.

An alternative would be to use a cloud service provider which would provide you with a public and static IP out of the box in most cases. Using a cloud service would also provide you with the high uptime necessary to collect as many envelopes as possible for later retrieval.

**A single instance with 1GB of RAM and 1 vCPU should be enough to run Status Node reliably.**

> In terms of software the minimum would include `make` and `jq`.
> If you want to build `status-go` you will also need `golang`, version 1.13 or higher. A nice-to-have is `qrencode` to display a `QR Code` with your `enode://` adress.
>
> For Ubuntu `20.04` you can just do:
> ```shell
> sudo apt install make jq golang qrencode
> ```

| PORT    	| FUNCTION                             	|                            	|
|---------	|--------------------------------------	|----------------------------	|
| `8545`  	| TCP - JSON RPC management port.      	| Must **NEVER** be public.  	|
| `30303` 	| TCP/UDP - DevP2P wire protocol port. 	| Must **ALWAYS** be public. 	|
| `9090`  	| TCP - Prometheus metrics port.       	| Should not be public.      	|