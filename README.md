# 2x Unbound DNS + Pi-hole with Docker compose

## Setup

* Edit `WEBPASSWORD` in `.env`.
* Edit `hosts` file to match your local devices.
* Edit `etc-dnsmasq.d/custom-dns-records.conf` to configure local domains.
* Change `REV_SERVER_TARGET` on your gateway IP address in `docker-compose.yml`.
* Change `ServerIP` on your local IP address in `docker-compose.yml`.

## Install

```
docker-compose up -d
```

## DNS Benchmark

To check performace of this setup versus popular DNS server:

* login into PiHole
* navigate to Settings > DNS
* select predefined Upstream DNS Servers you want to benchmark against
* install [namebench](https://github.com/catap/namebench) script(or similar)
and execute it.
* execute `docker ps -a` and find PiHole container id
* execute `docker exec -it <container-id> sh` to access the container
* execute `echo ">forward-dest >quit" | nc 127.0.0.1 4711` to get percentage
of forwards to each server (There is a performance algorithm that will favor
the best performers. The best performers will get the most forwards.)

## Links

* [Pi-Hole telnet API](https://docs.pi-hole.net/ftldns/telnet-api/)