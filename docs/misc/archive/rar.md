## File Structure


A RAR file mainly consists of tag block, file header block, file header block, and end block.

Each block is roughly divided into the following fields:

| Name | Size | Description |
| ---------- | ---- | --------------------- |
| HEAD_CRC | 2 | CRC of total block or block part  |
| HEAD_TYPE | 1 | Block Type |
| HEAD_FLAGS | 2 | Block Flags |
| HEAD_SIZE | 2 | Block Size |
| ADD_SIZE | 4 | Optional Field - added block size |


The file header of the RAR archive is `0x 52 61 72 21 1A 07 00`.

Following the file header (`0x526172211A0700`) the MARK_HEAD.

File Header (File in Archive):

| Name | Size | Description |
| ------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------ |
| HEAD_CRC      | 2               | CRC of fields from HEAD_TYPE to FILEATTR and file name |
| HEAD_TYPE     | 1               | Header Type: 0x74 |
| HEAD_FLAGS    | 2               | Bit Flags (Please see 'Bit Flags for File in Archive' table for all possibilities) |
| HEAD_SIZE     | 2               |	File header full size including file name and comments |
| PACK_SIZE     | 4               | Compressed file size |
| UNP_SIZE      | 4               | Uncompressed file size |
| HOST_OS       | 1               | Operating system used for archiving (See the 'Operating System Indicators' table for the flags used) |
| FILE_CRC      | 4               | File CRC |
| FTIME         | 4               | Date and time in standard MS DOS format |
| UNP_VER       | 1               | RAR version needed to extract file (Version number is encoded as 10 * Major version + minor version.) |
| METHOD        | 1               | Packing method (Please see 'Packing Method' table for all possibilities |
| NAME_SIZE     | 2               | File name size |
| ATTR          | 4               | File attributes |
| HIGH_PACK_SIZ | 4               | High 4 bytes of 64-bit value of compressed file size. Optional value, presents only if bit 0x100 in HEAD_FLAGS is set. |
| HIGH_UNP_SIZE | 4               | High 4 bytes of 64-bit value of uncompressed file size. Optional value, presents only if bit 0x100 in HEAD_FLAGS is set. |
| FILE_NAME     | NAME_SIZE bytes | File name - string of NAME_SIZE bytes size |
| SALT          | 8               | present if (HEAD_FLAGS & 0x400) != 0 |
| EXT_TIME      | variable size   |	present if (HEAD_FLAGS & 0x1000) != 0 |


The end of each RAR file is fixed (Terminator):

| Field Name | Size (bytes) | Possibilities       |
| ---------- | ------------ | ------------------- |
| HEAD_CRC   | 2            | Always 0x3DC4       |
| HEAD_TYPE  | 1            | Header type: 0x7b   |
| HEAD_FLAGS | 2            | Always 0x4000       |
| HEAD_SIZE  | 2            | Block size = 0x0007 |


The RAR terminator or trailer bytes is thus always `0x C4 3D 7B 00 40 07 00`

See more details [here](http://www.forensicswiki.org/wiki/RAR)


## Attack Methods


### Brute Force


- [RarCrack](http://rarcrack.sourceforge.net/)


### Pseudo encryption


The pseudo-encryption of a RAR file is on the bit mark field in the header of the file. This bit is clearly visible with the 010 Editor. Modifying this bit can create pseudo-encryption.


![](./figure/6.png)


Other techniques, such as plaintext attacks, remain the same as described in ZIP.
