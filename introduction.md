---
title: Introduction to HTool
---

HTool is a static analysis tool derived from `otool(1)` that is shipped with the Xcode Developer Tools, and inspired by `jtool(1)`. In the long term the aim for HTool is to have significant functionality such as analysing Mach-O's, FAT/Universal Binaries, DYLD Shared Cache, macOS and iOS Kernel's, iBoot, SEPOS, SecureROM and future firmware files, quick and easy disassembly, and an lldb-like interface for analysing and disassembling Mach-O files. 

There are no dependencies. You will be able to download and run with (hopefully) no issues. HTool heavily relies on Libhelper for it's Mach-O capabilities, which is Opensource. You can check out Libhelper [here](/projects/libhelper). However, unlike Libhelper I have no current plans to Opensource HTool, but please refer to the [FAQ](#expected-frequently-asked-questions) for more on this. You can also skip to [Downloads](#downloads) if you aren't interested in the docs. 

HTool is designed to run on macOS, both x86_64 and arm64, with iOS and Linux support planned for final release. 

A few quick notes:
 - **Opensource?**     
 -- No, I have no plans to opensource HTool at any point. Libhelper probably makes up 40-50% of HTool's source code, and that's opensource and free for you to use and modify! HTool just builds on the functionality provided by libhelper.

 - **Mash**
 -- Mash, or Mach-O Shell, is experimental functionality of HTool intended to act like lldb for dynamically analysing Mach-O files. It was very buggy in the previous versions, and significant changes made to libhelper to improve memory usage have broken it entirely. I have new plans for Mash, although it will still perform the same function. There may be another beta for Mash soon, it may even take shape as it's own tool, I haven't quite decided yet. 

 - **Supported file formats**
 -- HTool supports any 64 bit Mach-O, whether that be arm64 or x86. In terms of firmware files, any 64 bit firmware is supported up to the iPhone 12. If future devices or iOS/macOS versions break anything, I'll release an update addressing that.

 - **Operating Systems**
 -- Currently HTool supports macOS on both arm64 and x86_64. There will be iOS support in an upcoming Beta, however Linux support may be delayed until a later version.

 - **Distribution**
 -- For now HTool will be distributed via this website, however I'm planning on adding it to some package manager, probably Homebrew. When this happens, I'll most likely opt to ship libhelper as a dynamically-linked, rather than statically-linked, library so bugs that only occur in libhelper and do not require changes in HTool can be patched that way. This might change though.

### Downloads

All versions of HTool are available here! Even the old Beta's in case something is wrong in a newer version. Once the final version is released, I'll remove beta's for that version from this list. 

**Version 1.2.0**

This version of HTool is the latest and supports macOS on both arm64 and x86_64 architectures. The executable is bundled as a Universal Binary, so no need to download separate versions for Apple Silicon. Once downloaded, please run the `install.sh` script so the `man` page is installed correctly - otherwise you may opt to copy the files yourself.

**Please Note:** This is a beta version and may have issues and/or missing functionality.

| Platform | Version | Link |
| -------- | ------- | ---- |
| macOS | `htool-v1.2.0-b1` | [Download](https://s3.cloud-itouk.org/dnlds/releases/htool/htool-1.2.0-beta1-darwin-universal.zip) |


**Version 1.0.0**

Initial release of HTool. In these versions functionality is very limited. No arm64 support is present for macOS, nor iOS on beta 2. These downloads are available for debugging and testing purposes, and I discourage you from using them. Please refer to the versions above for the latest.

| Platform | Version | Link |
| -------- | ------- | ---- |
| macOS | `htool-v1.0.0-b2 | [Download](https://s3.cloud-itouk.org/dnlds/releases/htool/htool-1.0.0-beta2-darwinx86.zip) |
| macOS | `htool-v1.0.0-b1 | [Download](https://s3.cloud-itouk.org/dnlds/releases/htool/htool-1.0.0-beta1-darwinx86.zip) |
| iOS | `htool-v1.0.0-b1 | [Download](https://s3.cloud-itouk.org/dnlds/releases/htool/htool-1.0.0-beta1-darwin-arm64.zip) |
