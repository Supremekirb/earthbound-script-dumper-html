# earthbound-script-dumper-html
An Earthbound/Mother 2 text script dumper that outputs in HTML.

The output is several HTML files. They link between each other, so they should all be placed in the same directory if you plan on using the output.

Also note that, due to this just being a quick hack, the html is a bit sloppy. Specifically there's an extra `</section>` at the start and no closing tag on the final `<section>`.

## Running
This program requires Python 3.

To run, simply use the following command on the command line:  
`python3 script_dumper.py earthbound_rom groups_file [symbols_file]`

Where:
- `earthbound_rom` is the filepath to an Earthbound or Mother 2 ROM
- `groupd_file` is the filepath to a file containing info on how to split data into multiple files (see below)
- `symbols_file` is an optional filepath to a file containing symbol definitions (see below)

## Group files
Allows the dumper to output into several files based on address ranges. The syntax is.

`FILENAME = START, END[, START, END...]
(*e.g.* `onett = C80000, C875EF, EF340B, EF3600`
A filename may only contain numbers, letters, and underscores (`_`)

A semicolon (`;`) can also be used to start a comment. 

This repository contains a groupz file for the US version at `groups/groups_US.txt`.

## Symbol files
Symbol files allow for an even more readable text dump by defining labels and comments. The general syntax for those files is the following:

`LABEL = ADDRESS_IN_HEXADECIMAL[, OPTIONAL COMMENT]`  
(*e.g.* `TEXT_PMemberPoliteUpper = C7E6C5, "Sir/Ma'am" depending on party member`)  
A label name may only contain numbers, letters and underscores (`_`)

A semicolon (`;`) can also be used to start a comment in the symbols file. Everything after it will be ignored.

Invalid lines are ignored, but are also shown as a warning when read.


This repository contains a symbols file to be used with the US version of Earthbound at `symbols/symbols_US.txt`

## Features
- Translates control codes to a human-readable format (*e.g.* `[04 69 00]` becomes `[SET_FLAG PATH_TO_TWOSON_OPEN]`)
- Symbol files, allowing for custom labels and comments at a certain addresses (described above)
- Dumps the **entire** text script, including unused lines
- Works with Mother 2, Earthbound and the Earthbound localization prototype
