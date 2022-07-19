---
title: Dump Mach-O Shared Libraries
---

While Shared/Dynamically linked libraries are shown with the `LC_LOAD_DYLIB` load command, they can be viewed separately with the `-L` or `--libs` command. Some extra version information is printed with this method:

{% include image.html image = "/img/2020/htool/htool-macho-libs-1.png" title = "HTool `-L` command example." caption = "HTool `-L` command example." %}

#### List Symbols

HTool's symbol functionality is derived partly from the design of `nm(1)`. You can list all symbols, as defined by `LC_SYMTAB` with the `-S` option, or `--symbols`. 

{% include image.html image = "/img/2020/htool/htool-macho-symbols-1.png" title = "HTool `-S` command example." caption = "HTool `-S` command example." %}

There are two optional flags for the `-S` option: `-sym-sect` and `-sym-dbg`. The first displays the section the symbol is defined in, and the latter display and debug symbols. Currently, these cannot be used together, but this is planned.

{% include image.html image = "/img/2020/htool/htool-macho-symbols-2.png" title = "HTool `-S` command example with `-sym-sect`." caption = "HTool `-S` command example with `-sym-sect`." %}
