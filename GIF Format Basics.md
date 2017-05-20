# GIF Format Basics

Note: multi-byte ints are Little Endian

# Header Block:
47 49 46 - signature: G I F
38 39 61 - version: 8 9 a

# Logical Screen Descriptor:
0a00 - canvas width: unsigned int
0a00 - height
91 - packed byte: 1001 0001
    1 - color table flag: indicates presence of color table as next section
    001 - color depth (3 bit int): number of colors each pixel can display, 2^n
        This image has two colors (red and blue), so 2^1=2. Max 111 = 7 bits.
    0 - sort flag: are values in the color table sorted by decreasing frequency
    001 - color table size (3 bit int): color table = 2^(n+1)
00 - background color index: which color in the table to use for unspecified pixels
    Should be 0 if no color table.
00 - pixel aspect ratio: For values other than 0, this gives (n + 15) / 64.

# Global Color Table:
3*2^(n+1) where n is "color depth" from prev section, so max size 768 bytes.
ff ff ff - white: index 0
ff 00 00 - red: index 1
00 00 ff - blue: index 2
00 00 00 - black: index 3

# Graphics Control Extension: Optional
21 - extension inducer: always 21
f9 - graphic control label: what kind of extension is this block
04 - length of extension in bytes
00 - packed byte: 0000 0000
    000 - reserved (3 bits)
    000 - disposal method
    0 - user input flag
    0 transparent color flag
0000 - delay time
00 - transparent color index
00 - block terminator: always 00

# Image Descriptor:
2c - image separator: all image blocks begin with 2c
0000 - position left
0000 - position top
0a00 - width
0a00 - height
00 - packed byte: 0000 0000
    0 - local color table flag
    0 - interlace flag
    0 - sort flag
    00 - reserved
    000 - local color table size: same rules as global?

# Local Color Table: Optional, same syntax and rules as global

# Image Data
LZW Encoded
02 168c 2d99
872a 1cdc 33a0 0275 ec95 faa8 de60 8c04
914c 0100

# Trailer
3b - this is the end of file: always 3b