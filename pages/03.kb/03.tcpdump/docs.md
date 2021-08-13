---
title: Tcpdump
date: '12:50 13-08-2021'
taxonomy:
    category:
        - docs
---

#### TCPDump usage

* Capture HTTP (80) traffic and print headers

```bash
tcpdump -A -s 10240 'tcp port 80 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)' | egrep --line-buffered "^........(GET |HTTP\/|POST |HEAD )|^[A-Za-z0-9-]+: " | sed -r 's/^........(GET |HTTP\/|POST |HEAD )/\n\1/g'
```

* Filter packets with a TTL less than 32 (TTL is the 8th byte in the header):

```bash 
tcpdump -v ip and 'ip[8]<32'
```

* Capture traffic encapsulated IPIP traffic based on IP address:

First convert the IP to hex [here](https://www.browserling.com/tools/ip-to-hex)

```bash
tcpdump -l ip[32:4] = 0x0a6fc802  or ip[36:4] = 0x0a6fc802”
```

* Capture traffic and send it to a remote location:

First listen on port 12345 on the remote:

```
nc -l -p 12345 > /home/user/somefile.pcap
```

Then use tcpdump and pipe it to the remote with netcat (or nc):

```bash
# nc
tcpdump -n -U -s 0 -i <interface> not port 12345 -w - | nc <remote IP> 12345

#  ncat
tcpdump -n -U -s 0 -i <interface> not port 12345 -w - | ncat <remote IP> 12345
```

===

#### Working with pcaps

* Summarise IPs from a pcap:

```bash
tcpdump -ntr file.pcap | awk '{print $2}' | tr . ' ' | awk '{print $1"."$2"."$3"."$4}' | sort | uniq -c | awk ' {print $2}'
```

* Summarise IPs from a pcap (with packet count per IP):

```bash
tcpdump -ntr file.pcap | awk '{print $2}' | tr . ' ' | awk '{print $1"."$2"."$3"."$4}' | sort | uniq -c | awk ' {print $2 "\t" $1 }'
```
