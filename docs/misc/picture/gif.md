## File Structure


The file structure of a GIF file:

- File Header
  - File Signature
  - Version Number
- Data Stream
  - Control Identifier
  - Image Block
  - Other Extension Blocks
- File Trailer


A diagram for the structure of a GIF file:


![file structure diagram](./figure/gif.png)


### File header


Signature and Version Number. The signature, which consists of three bytes `GIF`, is used to confirm whether a file is in GIF format.
The file version number is also composed of three bytes, `87a` or `89a`.


### Logical Screen Descriptor


Logical Screen Descriptor always located right after the header. This tells the decoder how big the image will be. It is exactly 7 bytes long. It starts with the canvas width and canvas height.


### Global Color Table


The GIF format can have a global color table or local color tables for each sub-image. Each color table contains a list of RGB (Red, Green, Blue) color component intensities, for example, (255，0，0) represents red.


### Image Descriptor


A single GIF file may contain multiple images. In the original GIF rendering model, these were meant to be composited onto a larger virtual canvas. Nowadays multiple images are normally used for animations.

Each image begins with an image descriptor block, which is exactly 10 bytes long.


![image descriptor](./figure/imagesdescription.png)


### Image Data


Finally, we get to the actual image data. The image data is composed of a series of output codes which tell the decoder which colors to emit to the canvas. These codes are combined into the bytes that make up the block.


### File Trailer


The trailer block indicates when you've reached the end of the file. It is always a byte `3B`.

For more details, see [what is in a GIF](http://giflib.sourceforge.net/whatsinagif/bits_and_bytes.html)



## CTF Examples


### WDCTF-2017:3-2


The animation in GIFs are made up of a sequence of frames, each frame can be an image that contains hidden information.

You can use the `convert` command to separate each frame in the GIF file.



Run this command to split each frame of the GIF file: `ffmpeg -i cake.gif cake-%d.png`


After opening and separating each frame of the GIF image, it's clear that each frame was a part of a QR code, so let's combine the frames into a complete QR code using `Python`.

```python
from  PIL import Image

flag = Image.new("RGB",(450,450))

for i in range(2):
    for j in range(2):
        pot = "cake-{}.png".format(j+i*2+1)

        potImage = Image.open(pot)

        crop = potImage.crop(((j * 225, i * 225, (j+1)*225, (i+1)*225)))

        flag.paste(crop, (j * 225, i * 225))     

flag.save('./flag.png')
```

After scanning the QR code, you get a string of hexadecimal strings.

`03f30d0ab8c1aa5 .... 74080006030908`

The beginning `03f3` is the header of a `pyc` file, restore it to `python` executable and run it to get the flag.

Here is the decompiled code using uncompyle6:

```python
# uncompyle6 version 3.7.4
# Python bytecode 2.7 (62211)
# Decompiled from: Python 3.7.3 (v3.7.3:ef4ec6ed12, Mar 25 2019, 22:22:05) [MSC v.1916 64 bit (AMD64)]
# Embedded file name: /home/ctf/bbb.py
# Compiled at: 2017-09-02 09:35:36
import random

key = 'ctf'
strr = '186,98,180,154,139,192,114,14,102,168,43,136,52,218,85,100,43'

def func1(str1, key):
    random.seed(key)
    str2 = ''
    for c in str1:
        str2 += str(ord(c) ^ random.randint(0, 255)) + ','

    str2 = str2.strip(',')
    return str2


def func2(str2, key):
    random.seed(key)
    str1 = ''
    for i in str2.split(','):
        i = int(i)
        n = random.randint(0, 255)
        str1 += chr(i ^ n)
        print(n)

    return str1

print(func2(strr,key))
```

!!! note
Run the script using python2.7


```shell
python2.7 bbb.py

flag{U_r_Greatt!}
```

### XMAN-2017:100.gif


> Download the challenge [here](https://github.com/ctf-wiki/ctf-challenges/blob/master/misc/picture/gif/2017-xman-100.gif/100_KHf05OI.gif)

The time interval between each frame of a GIF file can also be used hide information.

By using the `identify` command, we printed the time interval of each frame.


```shell
$ identify -format "%s %T \n" 100.gif

0 66
1 66
2 20
3 10
4 20
5 10
6 10
7 20
8 20
9 20
10 20
11 10
12 20
13 20
14 10
15 10
```


Here we inferred that 20 & 10 represent 0 & 1, each frame interval is extracted and transformed into 1s and 0s.

```shell
cat flag | cut -d ' ' -f 2 | tr -d '66' | tr -d '\n' | tr -d '0' | tr '2' '0'

0101100001001101010000010100111001111011001110010011011000110101001101110011010101100010011001010110010101100100001101000110010001100101011000010011000100111000011001000110010101100100001101000011011100110011001101010011011000110100001100110110000101100101011000110110011001100001001100110011010101111101#
```

Finally, convert the binary to ASCII to get the flag.


## Tools


- [F5-steganography](https://github.com/matthewgao/F5-steganography)
