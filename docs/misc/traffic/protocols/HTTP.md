### HTTP


HTTP (Hyper Text Transfer Protocol) is an application layer protocol for distributed, collaborative, and hypermedia information systems. HTTP is the foundation of data communication for the World Wide Web, where hypertext documents include hyperlinks to other resources that the user can easily access, for example by a mouse click or by tapping the screen in a web browser.


### CTF Example


#### Jiangsu Province Navigator Cup - 2017: hack


> Download the challenge [here](https://github.com/ctf-wiki/ctf-challenges/blob/master/misc/cap/%E6%B1%9F%E8%8B%8F%E7%9C%81%E9%A2%86%E8%88%AA%E6%9D%AF-2017-hack/hack.pcap)

These observations can be drawn:

- `HTTP` is used
- `102.168.173.134` is the client
- No attachments exist


![linghang_hack](./figure/linghang_hack.png)


From this picture, we can see blind SQL injection is in traffic packets.


At this point, you can determine the direction to obtain the flag: extracting all the URLs, then use `Python`.

- Extract URLs: `tshark -r hack.pcap -T fields  -e http.request.full_uri|tr -s '\n' | grep flag > log`

- Parse blind SQL injection requests


```python
import re

with open('log') as f:
    tmp = f.read()
    flag = ''
    data = re.findall(r'=(\d*)%23',tmp)
    data = [(int(i)) for i in data]

    for i,num in enumerate(data):
        try:
            if num > data[i+1]:    
                flag += chr(num)
        except Exception:
            pass

    print(flag)
```
