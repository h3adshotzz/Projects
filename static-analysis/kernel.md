---
title: Kernel Static Analysis
---

HTool has static analysis functionality aimed at analysing firmware files for macOS, iOS, watchOS, tvOS, iBridgeOS, etc. The eventual aim is for the Kernel, Kernelcache, iBoot, SEPOS, SecureROM and probably Device Tree to be supported, however it's currently limited to the iOS Kernelcache, macOS Kernel (not to be confused with the M1 IPSW Kernelcaches) & iOS iBoot.

The analysis function can be run by passing `--analyse` when running HTool. There are other flags, `-la` and `-e` which I'll explain in the relevant sections.

Currently, HTool can analyse either an iOS Kernelcache (meaning from an IPSW), or a macOS Kernel (/System/Library/Kernels/*). Support for macOS Apple Silicon Kernelcaches, and for other Darwin Operating Systems, is planned.

As an example, I'll run `--analyse` using the `kernel.release.t8101` kernel on macOS, which is for the M1-based Mac's.

{% include image.html image = "/img/2020/htool/htool-analysis-1.png" title = "HTool `--analyse` for M1 macOS Kernel." caption = "HTool `--analyse` for M1 macOS Kernel." %}

HTool will run some checks to determine which type of Kernel it has been given. There are five types of Kernel that it can detect: xnu-arm64 (macOS), xnu-dtk (macOS), xnu-x86 (macOS), Merged new-style (iOS) and Split old-style (iOS). This type both determines how the Kernel is handled, and is displayed besides the "XNU Type:" label.

Looking further up, we start with "Darwin Version" and "XNU Version". This is extracted from the file and is the same information that would be printed by `uname -a`. Next is the "Compile Time" showing when the kernel was last compiled.

The "Device Type" label is a tricky one to calculate. There is a flaw in macOS arm64 Kernels in that they do not contain the correct platform identifier - whereas the Kernel Extension do. This, as S1guza kindly pointed out, is because Apple likely just reuse the build config used for other SoC's of the same type. In reality, the M1's are T8027's. 

Despite that, HTool will attempt to work out the SoC Brand name. In the case of the T8101 macOS kernel, HTool knows that this is used by both the M1 Mac's, and A14 Bionic iPhone's, so it prints the string "M1/A14 Bionic" to represent them both. Where there is an "Unknown" string, this is intended to show the platform identifier, which would be T8101, however this is still inaccurate and I'm working on a way where it will show the correct identifier for M1 Mac's.

Now, iOS Kernel caches are bundled with their Kernel Extensions (KEXTs), whereas macOS Kernel's aren't. If we analyse an iOS kernel, it will also list the number of KEXTs. There are two options here, we can list all the KEXT names, using `-la`, or extract a specific one with `-e [name]`.

{% include image.html image = "/img/2020/htool/htool-analysis-2.png" title = "HTool `--analyse` with `-la`." caption = "HTool `--analyse` with `-la`." %}

{% include image.html image = "/img/2020/htool/htool-analysis-3.png" title = "HTool `--analyse` with `-e com.apple.driver.AppleDiskImages2`." caption = "HTool `--analyse` with `-e com.apple.driver.AppleDiskImages2`." %}

That KEXT, `com.apple.driver.AppleDiskImages2`, will be extracted to your current directory. As they are Mach-O's, you can go ahead and run `-h` or `-l` to inspect it. (Note: new-style iOS Kernel's have KEXT segment merged with the rest of the kernel, see [here](/2020/01/handle-kernel-extensions/)).

{% include image.html image = "/img/2020/htool/htool-analysis-4.png" title = "HTool `-h -l com.apple.driver.AppleDiskImages2`." caption = "HTool `-h -l com.apple.driver.AppleDiskImages2`." %}
