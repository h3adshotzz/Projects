---
title: iBoot Static Analysis
---

Analysis of iBoot file is currently limited, as I'm still learning about their format myself. Currently, HTool can determine similar details about iBoot as it can about the Kernel (version, device, etc), plus embedded firmwares that it contains. The embedded firmware are for co-processors on iOS devices, for example the Power Management Unit (PMU). These embedded images are either in RAW or LZFSE format. HTool can currently find, decompress, show details and extract the LZFSE images.

The `-la` option has no effect here as there are so few embedded images that it's not required to hide them by default. The `-e` still has the same effect, as show here:

{% include image.html image = "/img/2020/htool/htool-analysis-5.png" title = "HTool `--analyse` command example with `-e AppleSMCFirmware-1631.102.1.d42_whitney.REL`." caption = "HTool `--analyse` command example with `-e AppleSMCFirmware-1631.102.1.d42_whitney.REL`." %}