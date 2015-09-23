title: "iptables example"
date: 2015-05-20 16:45:50
tags: [Network, Linux]
---

- block output sctp packet
``` bash
iptables -A OUTPUT -p sctp -s 192.168.166.250 -d 192.168.165.86  -j DROP
```

- block COOKIE_ECHO of sctp
``` bash
iptables  -A INPUT -i lo -p sctp --dport 10000 --chunk-types  ALL COOKIE_ECHO -j DROP
```
