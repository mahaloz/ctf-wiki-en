# PNG

## File Structure

For a PNG file, the header is always represented by fixed bytes, and the remaining parts consist of three or more chunks of PNG data in a specific order.

File header: `89 50 4E 47 0D 0A 1A 0A` + chunk + chunk + chunk...


### Chunks


PNG contains two types of chunks: one called critical chunks that are the standard chunks, another called ancillary chunks that are optional. Critical chunks define four standard chucks that must be included in every PNG file, and a PNG reader must support these blocks.

| Chunk Characters | Chunk Name | Multiple Chucks | Optional | Position Limitation |
| ------------------ | ------------------ | ------------------ | ------------------ | ------------------ |
| IHDR | Image Header | False | False | First Chunk |
| cHRM | Primary Chromaticities and White Point | False | True | Before PLTE and IDAT |
| gAMA | Image Gamma | False | True | Before PLTE and IDAT |
| sBIT | Significant Bits | False | True | Before PLTE and IDAT |
| PLTE | Palette | False | True | Before IDAT |
| bKGD | Background Color | False | True | Before PLTE and IDAT |
| hIST | Image Histogram | False | True | Before PLTE and IDAT |
| tRNS | Transparency | False | True | Before PLTE and IDAT |
| oFFs | Image Offset | False | True | Before IDAT |
| pHYs | Physical Pixel Dimensions | False | True | Before IDAT |
| sCAL | Physical Scale | False | True | Before IDAT |
| IDAT | Image Data | True | False | Consecutive with Other IDATs |
| tIME | Image Last Modification Time | False | True | No limit |
| tEXt | Textual Data | True | True | No limit |
| zTXt | Compressed Textual Data | True | True | No limit |
| fRAc | Fractal Parameters | True | True | No limit |
| gIFg | GIF Conversion Info | True | True | No limit |
| gIFt | GIF Plain Text | True | True | No limit |
| gIFx | GIF Conversion Info | True | True | No limit |
| IEND | Image Trailer | False | False | End of PNG Data Stream |

There is a unified structure for each chunk, and each chunk is composed of four parts:

| Name | Length in Bytes | Description |
| -------- | -------- | -------- |
| Length | 4 Bytes | Specifies the length of the data field in the chunk, which does not exceed (231-1) bytes |
| Chunk Type Code | 4 Bytes | Consists of ASCII letters (A-Z and A-Z) |
| Chunk Data | length Varies | Stores the data specified by the Chunk Type Code |
| CRC | 4 Bytes | Stores the Cyclic Redundancy Check information |

CRC（Cyclic Redundancy Check）value is calculated based on the Chunk Type Code and Chunk Data.

For more details see [PNG Chunks](http://www.libpng.org/pub/png/spec/1.2/PNG-Chunks.html)


### IHDR


IHDR (Image Header Chunk): It stores basic image information, 13-bytes long, must be the first chunk in a PNG data stream, and there must be only one file header chunk in a PNG data stream.

| Name | Number of Bytes | Description |
| -------- | ------- | ---------------------- |
| Width    | 4 bytes | Image width (in pixels) |
| Height   | 4 bytes | Image height (in pixels) |


We often change the height or width of an image to corrupt it to hide information.


![](./figure/pngihdr.png)


You can see here Kali won’t open the image, showing the `IHDR CRC error`. This is a sign that the IHDR chunk was modified.

You might be able to restore the corrupted image by changing the image’s width and length, or file header back to the correct values.


#### CTF Examples


##### WDCTF-finals-2017


If you look at the [file](https://github.com/susers/Writeups/blob/master/2017/WDCTF-finals/Misc/2-1/misc4.png), you can see that the header and width of the PNG file are incorrect.

```hex
00000000  80 59 4e 47 0d 0a 1a 0a  00 00 00 0d 49 48 44 52  |.YNG........IHDR|
00000010  00 00 00 00 00 00 02 f8  08 06 00 00 00 93 2f 8a  |............../.|
00000020  6b 00 00 00 04 67 41 4d  41 00 00 9c 40 20 0d e4  |k....gAMA...@ ..|
00000030  cb 00 00 00 20 63 48 52  4d 00 00 87 0f 00 00 8c  |.... cHRM.......|
00000040  0f 00 00 fd 52 00 00 81  40 00 00 7d 79 00 00 e9  |....R...@..}y...|
...
```

Note that you can't just randomly change the image's width, you need to brute force the width based on the IHDR chunk's CRC value (see Python script blow).


```python
import os
import binascii
import struct

misc = open("misc4.png","rb").read()

for i in range(1024):
    data = misc[12:16] + struct.pack('>i',i)+ misc[20:29]
    crc32 = binascii.crc32(data) & 0xffffffff
    if crc32 == 0x932f8a6b:
        print(i)
```


The script returned `709`, so changing the image's width to `709` will restore the image and get you the flag.


![](./figure/misc4.png)


### PLTE


PLTE (Palette Chunk): It contains from 1 to 256 palette entries, each a three-byte series of the form.
   - Red:   1 byte (0 = black, 255 = red)
   - Green: 1 byte (0 = black, 255 = green)
   - Blue:  1 byte (0 = black, 255 = blue)


### IDAT


IDAT (Image Data Chunk):It stores the actual image data which contains multiple image chucks in the data stream.
-   Stores image data
-   Contains multiple image chucks in the data stream
-   Uses a derivative of LZ77 algorithm to perform compression
-   Uses zlib to perform decompression


Note that IDAT will only continue to a new chunk when the previous chunk is full.


## Example


Use `pngcheck` display information about the PNG file

```
.\pngcheck.exe -v sctf.png
File: sctf.png (1421461 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1000 x 562 image, 32-bit RGB+alpha, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 3780x3780 pixels/meter (96 dpi)
  chunk IDAT at offset 0x00057, length 65445
    zlib: deflated, 32K window, fast compression
  chunk IDAT at offset 0x10008, length 65524
...
  chunk IDAT at offset 0x150008, length 45027
  chunk IDAT at offset 0x15aff7, length 138
  chunk IEND at offset 0x15b08d, length 0
No errors detected in sctf.png (28 chunks, 36.8% compression).
```

We can see when the first IDAT is full (length `65524`), it continued to the second IDAT. Now, we know the length for a full IDAT. Try to compare the last two IDAT (offset `0x150008` and `0x15aff7` ), do you see anything strange?

The second to last IDAT length is `45027` and the last IDAT length is `138`.

Clearly, something is wrong at the last IDAT because the second to last IDAT is not full.


Use `python` and `zlib` to decompress the content of the last IDAT. Note that **length, chunk type and CRC check value at the end** are excluded.

```python
import zlib
import binascii
IDAT = "789...667".decode('hex')
result = binascii.hexlify(zlib.decompress(IDAT))
print result
```


### IEND


IEND (Image Trailer Chunk): It is used to mark the end of a PNG data stream or file, and it must be placed at the end of the file.


## Example


- IEND's chunk length is always `00 00 00 00`
- IEND's chunk type is always IEND `49 45 4E 44`
- IEND'S CRC value is always `AE 42 60 82`

That means a PNG file will always end with these bytes:

`00 00 00 00 49 45 4E 44 AE 42 60 82`


## LSB

LSB stands for Least Significant Bit. Each pixel in a PNG image is generally composed of RGB three primary colors (red, green, and blue), each color occupies 8 bits, and the value range is from '0x00' to '0xFF', so there are 256 colors. The total number of colors is equal to 256 to the third power or 16777216.

The human eye can distinguish about 10 million different colors, which means the human eye cannot distinguish the remaining 6,777,216 colors.

LSB steganography is to modify the Least Significant Bit of each color, containing 8 bits, in an RGB value.


![](./figure/lsb.jpg)


If you want to find informing hidden using LSB, you can use this tool [Stegsolve](http://www.caesum.com/handbook/Stegsolve.jar) to perform analysis.

Use the buttons at the bottom of Stegsolve to see information extracted from each color channel.

In the following image, we found the hidden information by checking LSB on the red channel:


![Stegsolve Example](./figure/lsb1.png)


With the help of StegSolve, you can find hidden information by checking LSB each color channel.


### CTF Examples

#### HCTF - 2016 - Misc

There is information hidden in the LSB of a color channel. Use `Stegsolve-->Analyse-->Data Extract` to extract it.

![](./figure/hctfsolve.png)

We can see `zip` file header, use `save bin` to save the zip file. Then, run the ELF executable to get the flag.
