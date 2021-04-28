Image files are a good way to incorporate hacker culture, so a variety of images are used in CTFs.

Image files come in a variety of complex formats. Some methods used to solve CTF challenges involve finding metadata and hidden information, decoding lossless compression, checking validation, performing steganography, or extracting printable characters. All of those are important topics of Misc, involving understanding basic file formats, common steganography techniques, and steganography software.


## Metadata


> Metadata is "data that provides information about other data". In other words, it is "data about data". Many distinct types of metadata exist, including descriptive metadata, structural metadata, administrative metadata, reference metadata, statistical metadata, and legal metadata.

Hiding information in metadata is one of the most basic techniques CTFs, usually used to hide some key information like a `hint` or `password`.

You can view the metadata of an image by right-clicking on Properties or by using the `strings` command. In general, some hidden information (strange-looking strings) often appears at the beginning or end of the file.

Next, we introduce an `identify` command, which is used to get the format and characteristics of one or more image files.

`-format` is used to specify the information displayed, and the `-format` option can make a problem easier to solve.

For more details, see [Format Option Usage](https://www.imagemagick.org/script/escape.php)


### CTF Example

#### Break In 2017 - Mysterious GIF

> Download the challenge file [here](https://github.com/ctfs/write-ups-2017/blob/master/breakin-ctf-2017/misc/Mysterious-GIF/Question.gif)

One of the difficulties in this problem is to find and extract the metadata in GIF.

First, use the `strings` command to see the text strings and find abnormal text.

```console
GIF89a
   !!!"""###$$$%%%&&&'''((()))***+++,,,---...///000111222333444555666777888999:::;;;<<<===>>>???@@@AAABBBCCCDDDEEEFFFGGGHHHIIIJJJKKKLLLMMMNNNOOOPPPQQQRRRSSSTTTUUUVVVWWWXXXYYYZZZ[[[\\\]]]^^^___```aaabbbcccdddeeefffggghhhiiijjjkkklllmmmnnnooopppqqqrrrssstttuuuvvvwwwxxxyyyzzz{{{|||}}}~~~
4d494945767749424144414e42676b71686b6947397730424151454641415343424b6b776767536c41674541416f4942415144644d4e624c3571565769435172
NETSCAPE2.0
ImageMagick
...
```

Here, the strings of hexadecimal are hidden in the GIF metadata.

The next step is extraction, you can use Python, but it is more convenient to use `identify`

```shell
root@linux:~/Desktop/tmp# identify -format "%s %c \n" Question.gif
0 4d494945767749424144414e42676b71686b6947397730424151454641415343424b6b776767536c41674541416f4942415144644d4e624c3571565769435172
1 5832773639712f377933536849507565707478664177525162524f72653330633655772f6f4b3877655a547834346d30414c6f75685634364b63514a6b687271
...
24 484b7735432b667741586c4649746d30396145565458772b787a4c4a623253723667415450574d35715661756278667362356d58482f77443969434c684a536f
25 724b3052485a6b745062457335797444737142486435504646773d3d
```

Other steps are not described here, please refer to the [writeup](https://github.com/ctfs/write-ups-2017/tree/master/breakin-ctf-2017/misc/Mysterious-GIF).


## Pixel Values Conversion


Look at the data in this file, does it reminds you of anything?

```
255,255,255,255,255...........
```

It's a string of RGB values. Let's try to turn it into an image.

```python
from PIL import Image
import re

x = 307 #x coordinate
y = 311 #y coordinate  
# x*y = row number
rgb1 = [****]
print len(rgb1)/3
m=0
for i in xrange(0,x):
    for j in xrange(0,y):

        line = rgb1[(3*m):(3*(m+1))]# get line
        m+=1
        rgb = line

        im.putpixel((i,j),(int(rgb[0]),int(rgb[1]),int(rgb[2])))#rgb values converted to pixels
im.show()
im.save("flag.png")
```

On the other hand, the RGB value is extracted from an image, and then the RGB values are converted to get the final Flag.


Most of these questions are pictures composed of pixel blocks, as shown in the figure below:


![](./figure/brainfun.png)


## Related CTF Challenges


- [CSAW-2016-quals:brainfun](https://github.com/ctfs/write-ups-2016/tree/master/csaw-ctf-2016-quals/forensics/brainfun-50)
- [breakin-ctf-2017:A-dance-partner](https://github.com/ctfs/write-ups-2017/tree/master/breakin-ctf-2017/misc/A-dance-partner)
