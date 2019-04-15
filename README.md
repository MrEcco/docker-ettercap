
# Ettercap

Special build for in-docker use for [ettercap](https://github.com/Ettercap/ettercap) project. Arp-spoofing module ideal work for present configuration!

Dont be shy to contribute it or me! :)

## Usage

### Docker

```bash
docker run --rm -it           \
      --cap-add SYS_ADMIN     \
      --cap-add NET_ADMIN     \
      --network host          \
   mrecco/ettercap            \
      -TbqM arp               \
      -oi interface_name
```

### Docker-compose

```docker-compose
version: '3.0'
services:
  ettercap:
    container_name: hack-ettercap
    image: mrecco/ettercap:latest
    command:
    - "-TbqM"
    - "arp"
    - "-oi"
    - "interface_name"
    network_mode: host
    pid: host
    # privileged: true
    cap_add:
    - NET_ADMIN
    - SYS_ADMIN
    stop_grace_period: 3s
```
## Preconfigure

You need to prepare host mashine for this trick. Use it smart!!!

```bash
# Say kernel "lets forward packets!"
echo 1 > /proc/sys/net/ipv4/ip_forward
# Say firewall "lets nat forward connections"
iptables -t nat -I POSTROUTING -s 192.168.1.0/24 -j MASQUERADE
```

## Documentation

[https://linux.die.net/man/8/ettercap](https://linux.die.net/man/8/ettercap) [EN]
[https://pentestmag.com/ettercap-tutorial-for-windows/](https://pentestmag.com/ettercap-tutorial-for-windows/) [EN]
[https://kali.tools/?p=830](https://kali.tools/?p=830) [RU]