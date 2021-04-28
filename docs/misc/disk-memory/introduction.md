## Common tools


- EasyRecovery
- MedAnalyze
- FTK
- Volatility


## Disk


Common disk partition formats are as follows


-   Windows: FAT12 -> FAT16 -> FAT32 -> NTFS

-   Linux: EXT2 -> EXT3 -> EXT4

-   FAT file structure

    | Boot Sector | File Allocation Table | Root Directory | File Data Region

- Delete file: The first byte of the file name in the directory table is `e5`.


## VMDK


VMDK files are essentially a virtual version of the physical hard disk. It can also exist with the physical hard disk partition and sector of similar filled areas. We can use these filled areas to hide data. You can avoid the hidden files increasing the size of the VMDK files and virtual machine errors that may result from changes in the size of VMDK files. Also, VMDK files are generally large, so it’s suitable for hiding large files.


## RAM


- Analyze Windows / Linux / Mac OS X memory structure
- Analyze processes, memory data
- Use the given challenge prompt to extract specific memory data for the specified process.


## CTF Example


### 2018 Net Ding Cup - clip


> Download the challenge file [here](https://github.com/ctf-wiki/ctf-challenges/blob/master/misc/disk%26memory/2018-%E7%BD%91%E9%BC%8E%E6%9D%AF-clip/damaged.disk_bak)

Through the `010 hex editor`, you can see that the header of the file contains the word cloop. After searching, we found that this is an old linux-compressed device. The problem is that the device is damaged, so we will find a normal one.

To compress to get a cloop file, we can run the following command


```shell
mkisofs -r test | create_compressed_fs - 65536 > test.cloop
```

Refer [here](https://github.com/KlausKnopper/cloop) to compress the file, then we found errors within the file header in the damaged file and fixed it.


Here is how to extract files from the cloop file:

```
extract_compressed_fs test.cloop now
```

See [here](https://manned.org/create_compressed_fs/f2f838da) for more information.


We got an ext4 type file.

Next, we need to find a way to get the contents of this file system.


```shell
➜ losetup -d /dev/loop0
losetup: /dev/loop0: detach failed: Permission denied

➜ sudo losetup -d /dev/loop0

➜ sudo losetup /dev/loop0 now                                                 
losetup: now: failed to set up loop device: Device or resource busy

➜ sudo losetup /dev/loop0 /home/iromise/ctf/2018/0820网鼎杯/misc/clip/now        
losetup: /home/iromise/ctf/2018/0820网鼎杯/misc/clip/now: failed to set up loop device: Device or resource busy

➜ losetup -f           
/ dev / loop10

➜ sudo losetup /dev/loop10 /home/iromise/ctf/2018/0820网鼎杯/misc/clip/now

➜ sudo mount /dev/loop10 /mnt/now

➜ cd /mnt/now

➜  ls        
clip-clip.png  clip-clop.png  clop-clip.png  clop-clop.jpg  flag.png
```


The final step is to fix the flag.png header, where some bytes are missing.

Flag: `flag{0b008070-eb72-4b99-abed-092075d72a40}`
