By the analyzing of the protocols, you can narrow down the where data exfiltration occurred.

Next, you need to know how to extract the data, which is an important part of network traffic analysis.

## Wireshark


- Wireshark automatic extraction: `file -> export objects -> http`

- Manual data extraction: `file->export selected Packet Bytes`


## tshark


As a command-line version of wireshark, `tshark` is an efficient and fast. It can be used flexibly with other command-line tools (`awk`, `grep`) to quickly locate and extract data, thus eliminating the need for complicated scripting.


### Common methods


> `tshark -r **.pcap –Y ** -T fields –e ** | **** > data`


```
Usage:
  -Y <display filter>      packet displaY filter in Wireshark display filter syntax
  -T pdml | ps | psml | json | jsonraw | ek | tabs | text | fields | ? format of text output (def: text)
  -e <field>               field to print if -Tfields selected (e.g. tcp.port, _ws.col.Info)
```

Passing the `-Y` option allows you to apply display filters (same filter as Wireshark), then `-T fields -e` will let to extract specific fields (such as `usb.capdata`).

!!! Tips
    If you are not sure about the field name, you can right-click on the field in `Wireshark` of a packet, then Apply as Filter --> Selected.
    You should then see the field name in the filter bar.


## CTF Examples


### Google CTF 2016 - a cute stegosaurus

> Download the challenge [here](https://github.com/ctf-wiki/ctf-challenges/blob/master/misc/cap/2016-google-ctf-a-cute-stegosaurus-100/stego.pcap)

The data was hidden very cleverly. There was an image, but it's a rabbit hole and caused a lot of confusion.

For this challenge, you needs to be familiar with the `tcp` protocol.

There are 6 bits of status code in the TCP message segment:

- URG: Urgent bit. When URG=1, it means the packet is an urgent packet. It tells the system that there is urgent data in this segment and that it should be sent as soon as possible (equivalent to high-priority data)
- ACK: Acknowledge bit. When ACK=1, it means the packet is an acknowledgment packet. When ACK=0, the packet is not a acknowledgment packet. The server acknowledges data is received by sending ACK=1 to the sender or client.
- PSH: Push bit. When PSH=1, it means the other parity asks the packets in the buffer to be sent immediately, without waiting for the buffer to be full.
- RST: Reset bit. When RST=1, it means to aborts a connection due to errors, then the connection must be released and re-established.
- SYN: Synchronous bit. When SYN=1, it means the packet is making an initiation request to connect. Usually, the packet with the SYN flag means the client is trying to make a connection to the server.
- FIN: Final bit. When FIN=1, it means to release or close a connection.


![urg](figure/urg.png)


Extract the `tcp.urg` (Urgent pointer in the image above) with tshark, then remove the `0` field and replace the newline to `,`. Use Python to convert the numbers into ASCII to get the flag.


```shell
tshark -r stego.pcap -T fields -e  tcp.urgent_pointer | egrep -vi "^0$" | tr '\n' ','

67,84,70,123,65,110,100,95,89,111,117,95,84,104,111,117,103,104,116,95,73,116,95,87,97,115,95,73,110,95,84,104,101,95,80,105,99,116,117,114,101,125
```

Use Python to convert to ASCII:


```python
arr = [67,84,70,123,65,110,100,95,89,111,117,95,84,104,111,117,103,104,116,95,73,116,95,87,97,115,95,73,110,95,84,104,101,95,80,105,99,116,117,114,101,125]
print("".join([chr(x) for x in arr]))
```

Flag: `CTF{And_You_Thought_It_Was_In_The_Picture}`


## Related CTF Challenges


- [HITCON-2018 - ev3 basic](https://www.osusec.org/hitcon-ctf-2018-ev3-basic/)

- [HITCON-2018 - ev3 scanner](https://w0y.at/writeup/2018/10/22/hitcon-2018-ev3-scanner.html)
