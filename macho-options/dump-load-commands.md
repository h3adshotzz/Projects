---
title: Dump Mach-O Load Commands
---

Load Commands describe to the Kernel how to load a given Mach-O file. Commands range from simply describing hte source version and tools used to compile the executable, to how the kernel should map the file into memory, where the `main()` function is, and what dynamic libraries to load.

Listing the load commands can be done with `-l` or `--loadcmds` which, along with basically every other option, can be run together so you could run `-h -l` to print both the header info and load commands together.

{% include image.html image = "/img/2020/htool/htool-macho-load-commands-1.png" title = "HTool `-l` command example." caption = "HTool `-l` command example." %}

This can also be used on a FAT archive. By passing the `-arch` flag as well, you can choose the architecture within the FAT file to inspect, take `xcrun` as an example, where it contains both x86_64 and arm64e architectures:

{% include image.html image = "/img/2020/htool/htool-macho-load-commands-2.png" title = "HTool `-l` command example on FAT file." caption = "HTool `-l` command example on FAT file." %}

Running `-l` on a FAT archive without specifying the architecture with `-arch` will print the FAT header again, but instead expanding the Mach-O headers for all the contained architectures.

A significant amount of detail for each load command is presented using this option, especially with segment commands. If we look at the above image, take the `__TEXT` segment. Firstly we have the LC index, showing as `LC 01`, and the area of the file/memory that segment will take up. Directly underneath that we have the load command name, the mapping for the segment once loading into memory, in this case the `__TEXT` segment is readable and executable, but not writable - you most likely wouldn't find a writeable and executable segment. And next to that is the name of the segment.

Underneath that we have a small table detailing all the sections contained within the segment. The name, size and offset, showing the range, are displayed. 

If we now turn our attention to something like LC_SYMTAB, this lists the regular symbol information contained in the Mach-O, detailing the offset of the symbol and string table within the file, and the size of the string table. 

There may be some load commands that aren't yet implemented, these are work in progress as there is dozens of them.
