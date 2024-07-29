You can switch to any font available here:

    ls  /usr/share/kbd/consolefonts | less

with:

    setfont <fontname.psfu.gz>

If you just want a larger font, I usually go with something like "sun12x22.psfu.gz". You can also double the font size with setfont -d.

setfont manpage quote:

> -d     Doubles the size of the font, by replicating all of its pixels vertically and horizontally.  This is  suitable  for  high  pixel
>             density (e.g. "4k") displays on which the standard fonts are too small to be easily legible.  Due to kernel limitations, this is
>             suitable only for 16x16 or smaller fonts.

**EDIT:**

Testing the latest iso ....

Also useful, press [tab] in the boot loader menu and append "vga=ask" to the kernel command line parameters. Then press [enter] for a list of available video modes (resolution options). Select one and press [enter] to work in a more suitable terminal resolution.

Options "z" and "setfont ter-122n" are pretty easy on my eyes for this system.