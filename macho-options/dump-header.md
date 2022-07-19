---
title: Dump a Mach-O Header
---

My first article on this blog was discussing the Mach-O file format. As I mention there, they have carefully constructed headers so DYLD and the launchd can understand how to load it. There are different types of Mach-O so this header is extremely important - as with any executable format. 

One can get this information by adding the `-h` or `--help` flag when running HTool. See this example:

{% include image.html image = "/img/2020/htool/htool-macho-header-1.png" title = "HTool `-h` command example." caption = "HTool `-h` command example." %}

There are six properties in a Mach-O header: Magic, type, cpu type, cpu subtype, number of load commands, and the size of the load commands. HTool attempts to fetch a string descriptor of these values, so where we have the header magic, we have "0xfeedfacf (Mach-O 64 bit)" to make it clear the file is a 64 bit Mach-O. The type shows clearly that this is a Mach Executable, whereas if you were to run HTool on something such as a Kernel Extension, you would get the string "Mach Kernel Extension Bundle". The CPU type is described in two parts, the `cputype` and `cpusubtype`, and these are both displayed, although HTool will make an attempt at working out the actual name. In the event this fails, for example a newly released iOS Kernel with a new CPU subtype, the string "arm64_unk" would be displayed. Lastly is the number of Load Commands, and the size the load command region takes up following the header.

In some cases, especially with macOS 11.0, we have FAT/Universal Binaries. These archives contain one or more Mach-O's, and have their own FAT header. This header details the number of architectures within the archive, and their offset. HTool can handle these too:

{% include image.html image = "/img/2020/htool/htool-macho-header-2.png" title = "HTool `-h` command example with FAT archive." caption = "HTool `-h` command example with FAT archive." %}