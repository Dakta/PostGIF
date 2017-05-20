# GIF Application Extension: NETSCAPE2.0

## Programming Reference

Netscape Navigator has an Application Extension Block that tells Navigator to loop the entire GIF file. The Netscape block must appear immediately after the global color table of the logical screen descriptor. Only Navigator 2.0 Beta4 or better willl recognize this Extension block. The block is 19 bytes long composed off: (note: hexadecimal equivalent supplied for programmers)

    byte   1       : 33 (hex 0x21) GIF Extension code
    byte   2       : 255 (hex 0xFF) Application Extension Label
    byte   3       : 11 (hex 0x0B) Length of Application Block
                     (eleven bytes of data to follow)
    bytes  4 to 11 : "NETSCAPE"
    bytes 12 to 14 : "2.0"
    byte  15       : 3 (hex 0x03) Length of Data Sub-Block
                     (three bytes of data to follow)
    byte  16       : 1 (hex 0x01)
    bytes 17 to 18 : 0 to 65535, an unsigned integer in
                     lo-hi byte format. This indicate the
                     number of iterations the loop should
                     be executed.
    byte  19       : 0 (hex 0x00) a Data Sub-Block Terminator.
