#PostGIF

PostGIF is a basic animated GIF renderer written in PostScript. It uses PS builtins for raster rendering to the page.

Supports: interlacing, transparency, animation timing, and looping. Should be robust enough to ignore XMPP comments and other metadata/Extension blocks.

Caveats: uses Ghostscript's `flushpage` to bypass frame buffering; this doesn't play nice with real printers. This could be addressed by the use of showpage to effectively generate a flipbook, but this wouldn't play nice with transparency (often used to optimize frame encoding). Infinite looping isn't catastrophic (this file shouldn't generate more than a single page without modification), and should result in a memory or execution overflow if passed such a GIF and rendered on a physical printer.

## Usage

Invocation is recommended from the command line:

    gs reviewgif.ps -c "(image.gif) viewGIF"

`image.gif` must reside in the same directory as `reviewgif.ps`

## Misc

Copyright 2016 Dakota Schneider. License MIT.
