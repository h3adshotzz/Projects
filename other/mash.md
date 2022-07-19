---
title: Legacy Mach-O Shell (Mash)
---

<style>
	.aside-important {
		background-color: #fbf8e8;
		border-color: #fee450;
		border-right: 6px solid transparent;
	}

	.aside-warning {
		background-color: #fbe8e8;
		border-color: #fc5203;
		border-right: 6px solid transparent;
	}

	.aside-new {
		background-color: #e8fbe9;
		border-color: #73fe50;
		border-right: 4px solid transparent;
	}

	.aside-single {
		display: block;
		border-left-style: solid;
		border-left-width: 4px;
		border-radius: 4px;
		padding: 0.94118rem;
	}
	
	.aside {
		display: block;
		border-left-style: solid;
		border-left-width: 6px;
		border-radius: 6px;
		padding: 0.94118rem;
	}
</style>

<aside class="aside-single aside-warning">Introduced in: v1.0.0 Beta 2 (No longer valid)</aside>

Mach-O Shell, or Mash, is console for interacting and manipulating Mach-O files. There are a number of features planned for Mash, including an in-depth disassembler and possibly decompiler, however for now, the following features are available.

**Please note:** Mash is versioned differently to HTool, and may be split into a seperate binary in the future. It is currently in Alpha, so commands are likely to be changed, added or removed. More documentation on how to use Mash will be released once it has entered either the Beta stage, or fully released.

Mash has a number of primary commands, with some of those having "sub-commands". Most commands have both full, and short-hand types, for example the command `print segment all` can also be written as `p s all`. Mash also makes use of Editline, so has tab-completion when working with files. 

Mash uses "sessions", so currently you cannot reload, nor load a new file while in the same session. To begin working on a new file, either quit out of the current session, or open a new command line window. The aim of sessions is to be able to save progress and/or changes to a file while working in Mash.

Forgive the fairly brief overview of commands, the reason for this is that I'm constantly changing how Mash works, so command names and functionality change. With it's release I will include The following is the current set of Mash Commands that I will discuss:

{% include image.html image = "/img/2020/htool-beta-release-12.png" title = "HTool `--mash` command example." caption = "HTool `--mash` command example." %}

#### Generic commands.

There are a few generic commands to know about first of all. Starting with, `help`, or `h`. This will simply print a help menu with a summary of all the primary commands, this includes the full command name, the short name, and a description.

Next is `list`, or `ls`. This is simply a wrapper around `ls(1)` and allows one to use `ls` for finding files when trying to load a Mach-O into Mash.

The `version` command gives a version summary for mash in a similar format of HTool's `--version` command.

The `quit` or `q` command does what it says on the tin - it will quit back to the command line - and `load`, or `l`, will load and verify a Mach-O file for that particular session. A file can also be loaded when running the command, like so: `htool --mash <file>`.

#### Print commands.

The Print command is used to print particular parts of a load Mach-O file, and is the first of the primary commands for working with Mach-O files that I'm implementing. Firstly, is the Help command, similarly called with either `print help` or `p h`. **Note:** When using the short names, they are interchangable, for example the command `print h` will work just fine. If you enter a command without it's option flag, for example `print segment`, a small help menu will be shown to guide you to entering the correct option.

To start, the Load Commands of a Mach-O can be printed using `print commands <opt>`, or `p lc <opt>`, with the `<opt>` being either the keyword `all`, or the name of a load command, such as `LC_SOURCE_VERSION`. The output of this will be similar to the output of `htool -l <file>` just with Segment Commands removed.

Segment commands can be printed in a similar way using `print segment <opt>`, or `p s <opt>`. Again, with `<opt>` being either `all` or all segments, or the name of the segment, e.g. `__TEXT`. And again, the output will be similar to `htool -l <file>` with the Load Commands removed. 

A loaded file's Symbols can be printed using `print symbol <opt>` or `p sym <opt>`. In this case, `<opt>` has a few more options. With the standard `htool -S` option, there are flags for printing debug symbols and for including the section each symbol is defined in. With Mash, that same functionality is included. To print all symbols, replace `<opt>` with `all`, for debug symbols replace with `all-dbg`, and for section defines, replace with `all-sect`. Again, with the `-S` option, these cannot be used together - yet.

Finally, libraries. This is a very simple command, as there is not options to give it. It will print all linked libraries, like the `htool -L` command. It can be invoked either with `print libs`, or `p l`.