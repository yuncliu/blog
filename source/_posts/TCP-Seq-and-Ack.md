title: TCP Seq and Ack
date: 2015-09-23 16:01:38
tags: [Network]
---

**Sequence** and **Acknowlegement** number is very import in TCP protocol. 
They are used to detect if the packet is out of order or if there are any missing pakcets.
The **Seq** in the **SYN** packet is called **ISN**(Initial Sequence Number)

Wireshark will calculate relative sequence nuber = real Seq - ISN

```bash
1.  36724 > 9999  [SYN] Seq=0 Win=43690 Len=0
    36724 send a TCP header with SYN flag to 9999, ISN = 0. try to establish a TCP connection

2.  9999  > 36724 [SYN, ACK] Seq=0 Ack=1 Win=43690 Len=0
    9999 reply with SYN flag and Seq = ISN,  Ack = (ISN + 1)

3.  36724 > 9999  [ACK] Seq=1 Ack=1 Win=43776 Len=0
    36724 send with  Seq = ISN + 1, Ack = ISN + 1.  
    TCP connection is estableshed 

4.  36724 > 9999  [PSH, ACK] Seq=1 Ack=1 Win=43776 Len=3
    Seq = ISN  = 1
    Ack = Packet(3).Ack = 1

5.  9999  > 36724 [ACK] Seq=1 Ack=4 Win=43776 Len=0
    Seq = ISN  = 1
    Ack = Packet(4).Seq + Packet(4).Len = 1 + 3 = 4

6.  9999  > 36724 [PSH, ACK] Seq=1 Ack=4 Win=43776 Len=3
    Seq = Packet(5).Seq + Packet(5).Len = 1 + 0 = 1          Packet(5) is last packet sent from 9999 to 36724
    Ack = Packet(5).Ack = Packet(4).Seq + Packet(4).Len = 4  Packet(4) is latest packet received from 36724

7.  36724 > 9999  [ACK] Seq=4 Ack=4 Win=43776 Len=0
    Seq = Packet(4).Seq + Packet(4).Len = 1 + 3 = 4    Packet(4) is last packet sent from 36723 to 9999
    Ack = Packet(6).Seq + Packet(6).Len = 1 + 3 = 4

8.  36724 > 9999  [PSH, ACK] Seq=4 Ack=4 Win=43776 Len=4
    Seq = Packet(7).Seq + Packet(7).Len = 4 + 0 = 4                   Packet(7) is last packet sent from 36724 to 9999
    Ack = Packet(7).Ack = Packet(6).Seq + Packet(6).Len = 1 + 3 = 4   Packet(6) is latest packet received from 9999

9.  9999  > 36724 [PSH, ACK] Seq=? Ack=? Win=43776 Len=4
    So do you know here the Seq and Ack ?
    Seq is related with packet 6 and Ack is related with pakcet 8
```

So, the **relative Seq** can reflect how many bytes is already sent, and **relative Ack** could reflect 
how many bytes is already received.
