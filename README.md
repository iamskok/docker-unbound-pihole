# 2x Unbound DNS + Pi-hole (Docker compose)

## Setup

1. Update `.env` file:
  * Set secure `WEBPASSWORD`.
  * Set gateway IP address `REV_SERVER_TARGET`.
  * Set local network in CIDR notation `REV_SERVER_CIDR`.
  * Set PiHole local IP address `ServerIP`.
2. Update `hosts` file to match your local devices (alternatively remove all records).
3. Update `etc-dnsmasq.d/custom-dns-records.conf` to configure local domains resolutions (alternatively remove all records).

## Install

```
docker-compose up -d
```

## DNS Benchmark

To check performace of this setup vs popular DNS server:

* Login into PiHole.
* Navigate to Settings > DNS.
* Select predefined upstream DNS servers you want to benchmark against.
* Install [namebench](https://github.com/catap/namebench) or similar script
and execute it. Alternatively use PiHole for 24 hours.
* Find PiHole container id `docker ps -a`.
* Access PiHole container `docker exec -it <container-id> sh`.
* Execute `echo ">forward-dest >quit" | nc 127.0.0.1 4711` to get percentage
of forwards to each server (PiHole has an algorithm which will favor
the best performers. The best performers will get the most forwards.)

## Links

* [Pi-Hole telnet API](https://docs.pi-hole.net/ftldns/telnet-api/)