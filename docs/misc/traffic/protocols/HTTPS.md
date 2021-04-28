### HTTPS



`HTTPs = HTTP + SSL / TLS`. In HTTPS, the communication protocol is encrypted using Transport Layer Security (TLS) or, formerly, Secure Sockets Layer (SSL). The protocol is therefore also referred to as HTTP over TLS, or HTTP over SSL.


### CTF Example


#### hack-dat-kiwi-ctf-2015: ssl-sniff-2


> Download the challenge files [here](https://github.com/ctf-wiki/ctf-challenges/tree/master/misc/cap/hack-dat-kiwi-ctf-2015-ssl-sniff-2)

Open the PCAP file in Wireshark, you will find `TLS` encrypted data.

We are given the `server.key.insecure` key, so we need to import that key in order to decrypt the packets.


There are two ways to get to the `TLS` Preferences page:

1. `Edit --> Preferences --> Protocols --> TLS`

2. `Right click on a TSL packet --> Transport Layer Security --> Open Transport Layer Security preferences`


After you get to the `TLS` Preferences page, click on `Edit...` next to the RSA keys list.

Then, add the `server.key.insecure` file to `Key File` and hit `OK`.

![](./figure/import-tls-key.png)

Now, you can see the decrypted packets. You will find the flag in the HTTP packets.

![](./figure/https-decrypted.png)
