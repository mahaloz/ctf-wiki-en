### DNS



`DNS` uses `UDP` protocol.

Message format:

```
+----------------------------------------------------------+
| Message Header                                           |
+----------------------------------------------------------+
| Question (record of query to the server)                 |
+----------------------------------------------------------+
| Answer (record of server reply)                          |
+----------------------------------------------------------+
| Authorization (NS record for authoritative zone servers) |
+----------------------------------------------------------+
| Additional (additional useful information)               |
+----------------------------------------------------------+
```


The query packet only has two parts: the header and the question. After receiving the query packet, DNS parses answer information, the authorized organization, the additional resource record according to the query information, and modify the relevant identification of the header and then return it to the client.

The query header has a fixed length of 12 bytes and contains the query/reply packet information in the following format:


```
                                1  1  1  1  1  1
  0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
|                      ID                       |
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
|QR|   Opcode  |AA|TC|RD|RA|   Z    |   RCODE   |
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
|                    QDCOUNT                    |
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
|                    ANCOUNT                    |
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
|                    NSCOUNT                    |
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
|                    ARCOUNT                    |
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

- `ID`: ID set by the client, the reply message must have the same id to distinguish which query the reply message belongs to.
- `QR`: Indicates if the message is a query (0) or a reply (1).
- `AA`: Authoritative Answer, in a response, indicates if the DNS server is authoritative for the queried hostname.
- `TC`: Truncation, indicates that this message was truncated due to excessive length.
- `RD`: Recursion Desired, indicates if the client means a recursive query.
- `RA`: Recursion Available, in a response, indicates if the replying DNS server supports recursion.
- `Z`: Zero, reserved for future use.
- `RCODE`: Response code, can be NOERROR (0), FORMERR (1, Format error), SERVFAIL (2), NXDOMAIN (3, Nonexistent domain)...


Every question selection format:

```
  0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
|                                               |
/                     QNAME                     /
/                                               /
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
|                     QTYPE                     |
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
|                     QCLASS                    |
+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```


- `QNAME`: Name of the requested resource.
- `QTYPE`: Type of RR (A, AAAA, MX, TXT, etc.).
- `QCLASS`: Class code.



### CTF Examples


#### BSides San Francisco CTF 2017 - dnscap


> Download the PCAP file [here](https://github.com/ctf-wiki/ctf-challenges/blob/master/misc/cap/BSides-San-Francisco-CTF-2017-dnscap/dnscap.pcap)

We opened the PCAP file in `Wireshark` and found all the traffics is using the `DNS` protocol.

There are many bytes in the DNS query domain name.

We can use this Regex to find all the requested domain names:  `([\w\.]+)\.skullseclabs\.org`




Remove the rest of the fields in `qry.name`, leaving only `data` part, thus merging the data, then retrieving `89504e.....6082` in hex.


!!! note

run this script in Python2.7


```python
import re

find = []

with open('hex','rb') as f:
    for i in f:
        text = re.findall(r'([\w\.]+)\.skull',i)
        if text:
            tmp =  text[0].replace('.','')
            find.append(tmp[18:])
last = []

for i in find:
    if i not in last:
        last.append(i)

print  ''.join(last)
```

Now, convert the hex to file and then extract the png file from it.

Using CyberChef to convert and extract the file, we got the flag.

Flag:


![dnscat_flag](./figure/dnscat_flag.png)


### Related CTF Challenges


- [IceCTF-2016:Search](https://mrpnkt.github.io/2016/icectf-2016-search/)

- [EIS-2017:DNS 101](https://github.com/susers/Writeups/blob/master/2017/EIS/Misc/DNS%20101/Write-up.md)



### References


- https://github.com/lisijie/homepage/blob/master/posts/tech/dns%E5%8D%8F%E8%AE%AE%E8%A7%A3%E6%9E%90.md

- https://xpnsec.tumblr.com/post/157479786806/bsidessf-ctf-dnscap-walkthrough
