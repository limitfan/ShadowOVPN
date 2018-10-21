# ShadowOVPN

ShadowOVPN bridges shadowsocks and OpenVPN based on Docker.

## Getting Started

These instructions are for deploying ShadowOVPN on your own compute instance.

### Prerequisites

You need Docker running on your compute instance or install it using following command.

```
curl -sSL https://get.docker.com/ | sh
```

### Installing

Make sure requests module of python is installed and firstly grab an ovpn configuration file from [vpngate.net](https://www.vpngate.net/en/) using following command.
The argument for vpngate.py is two letter country code for available countries.

```
python first_vpngate.py jp
```

Make sure ovpn file is successfully generated and then secondly start ovpnsocks Docker instance.

```
bash second_start_ovpnsocks.sh
```

And then thirdly start pproxy Docker instance using your own shadowsocks configuration.

```
docker run -d --network="host" \
--name=pproxy leenwu/pproxy \
pproxy -l ss://chacha20:abc@:8080 -r socks5://localhost:1081
```

Now you can connect OpenVPN server with your designated ovpn file with shadowsocks clients.

## Swithing servers

Explain how to switch servers when you want or previous server is down.

### Extracting new server from vpngate.

Choose new ovpn location.
```
python first_vpngate.py kr
```

### And restart ovpnsocks Docker instance.

Docker restarts ovpnsocks instance.
```
docker restart ovpnsocks
```

## Built With

* [openvpn-client-socks](https://github.com/kizzx2/docker-openvpn-client-socks) - Used in ovpnsocks Docker instance
* [python-proxy](https://github.com/qwj/python-proxy) - Used in pproxy Docker instance

## Authors

* **Ligang Wu** - *Initial work* - [limitfan](https://github.com/limitfan)


## License

This project is licensed under the MIT License.

