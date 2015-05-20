title: "iptables example"
date: 2015-05-20 16:45:50
tags: [network, linux]
---

- block output sctp packet
``` bash
iptables -A OUTPUT -p sctp -s 192.168.166.250 -d 192.168.165.86  -j DROP
```
