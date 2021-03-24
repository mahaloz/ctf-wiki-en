In most CTF competitions, both forensics and steganography are inseparable. The knowledge required for the two is also complementary, so both will be introduced here.

Any requirement that requires finding hidden information in a static file is considered a forensics steganography question (unless it’s purely cryptography). Some low-point questions do combine forensics steganography and classic ciphers. The high score questions, however, are usually combined with some more complex modern cryptography. This well reflects the characteristics of Misc questions.


## Pre-skills


- Familiar with common encodings. Able to decode encoded text found in files. Can identify some special encodings (base64, hexadecimal, binary, etc.) and convert them to obtain the flags.
- Ability to manipulate binary data using scripting languages (Python, etc.)
- Familiar with file formats of common files, especially the various [file headers](https://en.wikipedia.org/wiki/List_of_file_signatures), protocols, structures, etc
- Can effectively use common tools


## Manipulate Binary Data in Python


### `struct` Module


Sometimes you need to use Python to process binary data, such as, when saving a file or using a socket. Python’s struct module can help you complete those tasks.


The three most important functions in the struct module are `pack()`, `unpack()`, and `calcsize()`

- `pack(fmt, v1, v2, ...)` Packs a list of values into a string according to the given format `fmt` (similar to a C structure's byte stream)
- `unpack(fmt, string)` Unpacks the packed value into its original representation according to the given format `fmt` and returns the unpacked tuple
- `calcsize(fmt)` Calculates and returns the size of the String representation of struct according to the given format `fmt`


The packing format `fmt` here determines how the variable is packaged as a byte stream, which contains a series of format strings. For details the meanings of the different formatted strings, please refer to [Python Doc](https://docs.python.org/3/library/struct.html) for more details.


```python
>>> import struct
>>> struct.pack('>I',16)
b'\x00\x00\x00\x10'
```

The first argument of `pack` is the packing instruction. `'>I'` means: `>` indicates that the byte order is Big-Endian, which is the network byte order. `I` indicates a 4-byte unsigned integer.
The number of arguments must match the number of format characters used in the packing instruction. In this case, because only one format characters are used(`I`), there can only be one remaining argument.


To read the first 30 bytes of a BMP file, the structure of the file header is as follows:
- Two bytes: `BM` for Windows bitmap, `BA` for OS/2 bitmap
- a 4-byte integer: size of the BMP file in bytes
- a 4-byte integer: reserved bits, always 0
- a 4-byte integer: offset of the byte where the bitmap image data (pixel array) can be found
- a 4-byte integer: size of this header
- a 4-byte integer: bitmap width in pixels
- a 4-byte integer: bitmap height in pixels
- a 2-byte integer: number of color planes (always 1)
- a 2 byte integer: number of bits per pixel, which is the color depth of the image (Typically 1, 4, 8, 16, 24, 32)

For more details, see [BMP file format - Wikipedia](https://en.wikipedia.org/wiki/BMP_file_format#Bitmap_file_header)

```python
>>> import struct
>>> bmp = b'\x42\x4d\x38\x8c\x0a\x00\x00\x00\x00\x00\x36\x00\x00\x00\x28\x00\x00\x00\x80\x02\x00\x00\x68\x01\x00\x00\x01\x00\x18\x00'
>>> struct.unpack('<ccIIIIIIHH',bmp)
(b'B', b'M', 691256, 0, 54, 40, 640, 360, 1, 24)
```


### `bytearray`


Read a file into a `bytearray`
```python
data = bytearray(open('challenge.png', 'rb').read())
```

A `bytearray` is a mutable version of bytes
```python
data[0] = '\x89'
```


## Common tools


### [010 Editor](http://www.sweetscape.com/010editor/)


Sweetscape 010 Editor is a new hex file Editor that differs from traditional hex editors in that it uses "templates" to parse binary files so you can read and edit them. It can also be used to compare any other binary file.

Its templating feature makes it very easy to observe the internal structure of a file and quickly change the content accordingly.


![010 Editor](figure/010.png)


### `file` command


The `file` command identifies the file type of a file based on the file header (magic bytes).

```shell
root@linux:~/Desktop/tmp# file flag
flag: PNG image data, 450 x 450, 8-bit grayscale, non-interlaced
```


### `strings` command


Print or display the printable characters of a file. Often you can discover hints or encoded information in the printable characters.

- You can extract specific  information with the `grep` command

    ```shell
    strings test|grep -i XXCTF
    ```

- You can get all ASCII character offsets with the `-o` option

    ```shell
    root@linux:~/Desktop/tmp# strings -o flag | head
        14 IHDR
        45 gAMA
        64  cHRM
        141 bKGD
        157 tIME
        202 IDATx
        223 NFdVK3
        361 |;*-
        410 Ge%<W
        431 5duX@%
    ```


### `binwalk` command


`binwalk` is a firmware analysis tool. In CTFs, `binwalk` is often used to discover multiple files hidden in a file. Furthermore, the tool uses the file header (magic bytes) to find other files contained in a file. Sometimes, there are false positives (especially for a PCAP, packet capture, file).


```shell
root@linux:~/Desktop/tmp# binwalk flag

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 450 x 450, 8-bit grayscale, non-interlaced
134           0x86            Zlib compressed data, best compression
25683         0x6453          Zip archive data, at least v2.0 to extract, compressed size: 675, uncompressed size: 1159, name: readme.txt
26398         0x671E          Zip archive data, at least v2.0 to extract, compressed size: 430849, uncompressed size: 1027984, name: trid
457387        0x6FAAB         End of Zip archive
```


- Automatic extraction with the `-e` option:
    `binwalk -e flag`

- Manual file carving can also be done with the `dd` command:
    ```shell
    root@linux:~/Desktop/tmp# dd if=flag of=1.zip bs=1 skip=25683
    431726+0 records in
    431726+0 records out
    431726 bytes (432 kB, 422 KiB) copied, 0.900973 s, 479 kB/s
    ```
