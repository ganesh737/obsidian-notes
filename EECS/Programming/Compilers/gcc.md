# gcc

## objcopy

```bash
objcopy
    Usage: /opt/tooling/bosch/OSTC_5.1/aarch64-none-linux-gnueabi/bin/aarch64-none-linux-gnueabi-objcopy [option(s)] in-file [out-file]
     Copies a binary file, possibly transforming it in the process
     The options are:
      -I --input-target <bfdname>      Assume input file is in format <bfdname>
      -O --output-target <bfdname>     Create an output file in format <bfdname>
      -B --binary-architecture <arch>  Set output arch, when input is arch-less
      -F --target <bfdname>            Set both input and output format to <bfdname>
         --debugging                   Convert debugging information, if possible
      -p --preserve-dates              Copy modified/access timestamps to the output
      -D --enable-deterministic-archives
                                       Produce deterministic output when stripping archives
      -U --disable-deterministic-archives
                                       Disable -D behavior (default)
      -j --only-section <name>         Only copy section <name> into the output
         --add-gnu-debuglink=<file>    Add section .gnu_debuglink linking to <file>
      -R --remove-section <name>       Remove section <name> from the output
      -S --strip-all                   Remove all symbol and relocation information
      -g --strip-debug                 Remove all debugging symbols & sections
         --strip-dwo                   Remove all DWO sections
         --strip-unneeded              Remove all symbols not needed by relocations
      -N --strip-symbol <name>         Do not copy symbol <name>
         --strip-unneeded-symbol <name>
                                       Do not copy symbol <name> unless needed by
                                         relocations
         --only-keep-debug             Strip everything but the debug information
         --extract-dwo                 Copy only DWO sections
         --extract-symbol              Remove section contents but keep symbols
      -K --keep-symbol <name>          Do not strip symbol <name>
         --keep-file-symbols           Do not strip file symbol(s)
         --localize-hidden             Turn all ELF hidden symbols into locals
      -L --localize-symbol <name>      Force symbol <name> to be marked as a local
         --globalize-symbol <name>     Force symbol <name> to be marked as a global
      -G --keep-global-symbol <name>   Localize all symbols except <name>
      -W --weaken-symbol <name>        Force symbol <name> to be marked as a weak
         --weaken                      Force all global symbols to be marked as weak
      -w --wildcard                    Permit wildcard in symbol comparison
      -x --discard-all                 Remove all non-global symbols
      -X --discard-locals              Remove any compiler-generated symbols
      -i --interleave[=<number>]       Only copy N out of every <number> bytes
         --interleave-width <number>   Set N for --interleave
      -b --byte <num>                  Select byte <num> in every interleaved block
         --gap-fill <val>              Fill gaps between sections with <val>
         --pad-to <addr>               Pad the last section up to address <addr>
         --set-start <addr>            Set the start address to <addr>
        {--change-start|--adjust-start} <incr>
                                       Add <incr> to the start address
        {--change-addresses|--adjust-vma} <incr>
                                       Add <incr> to LMA, VMA and start addresses
        {--change-section-address|--adjust-section-vma} <name>{=|+|-}<val>
                                       Change LMA and VMA of section <name> by <val>
         --change-section-lma <name>{=|+|-}<val>
                                       Change the LMA of section <name> by <val>
         --change-section-vma <name>{=|+|-}<val>
                                       Change the VMA of section <name> by <val>
        {--[no-]change-warnings|--[no-]adjust-warnings}
                                       Warn if a named section does not exist
         --set-section-flags <name>=<flags>
                                       Set section <name>'s properties to <flags>
         --add-section <name>=<file>   Add section <name> found in <file> to output
         --update-section <name>=<file>
                                       Update contents of section <name> with
                                       contents found in <file>
         --dump-section <name>=<file>  Dump the contents of section <name> into <file>
         --rename-section <old>=<new>[,<flags>] Rename section <old> to <new>
         --long-section-names {enable|disable|keep}
                                       Handle long section names in Coff objects.
         --change-leading-char         Force output format's leading character style
         --remove-leading-char         Remove leading character from global symbols
         --reverse-bytes=<num>         Reverse <num> bytes at a time, in output sections with content
         --redefine-sym <old>=<new>    Redefine symbol name <old> to <new>
         --redefine-syms <file>        --redefine-sym for all symbol pairs
                                         listed in <file>
         --srec-len <number>           Restrict the length of generated Srecords
         --srec-forceS3                Restrict the type of generated Srecords to S3
         --strip-symbols <file>        -N for all symbols listed in <file>
         --strip-unneeded-symbols <file>
                                       --strip-unneeded-symbol for all symbols listed
                                         in <file>
         --keep-symbols <file>         -K for all symbols listed in <file>
         --localize-symbols <file>     -L for all symbols listed in <file>
         --globalize-symbols <file>    --globalize-symbol for all in <file>
         --keep-global-symbols <file>  -G for all symbols listed in <file>
         --weaken-symbols <file>       -W for all symbols listed in <file>
         --add-symbol <name>=[<section>:]<value>[,<flags>]  Add a symbol
         --alt-machine-code <index>    Use the target's <index>'th alternative machine
         --writable-text               Mark the output text as writable
         --readonly-text               Make the output text write protected
         --pure                        Mark the output file as demand paged
         --impure                      Mark the output file as impure
         --prefix-symbols <prefix>     Add <prefix> to start of every symbol name
         --prefix-sections <prefix>    Add <prefix> to start of every section name
         --prefix-alloc-sections <prefix>
                                       Add <prefix> to start of every allocatable
                                         section name
         --file-alignment <num>        Set PE file alignment to <num>
         --heap <reserve>[,<commit>]   Set PE reserve/commit heap to <reserve>/
                                       <commit>
         --image-base <address>        Set PE image base to <address>
         --section-alignment <num>     Set PE section alignment to <num>
         --stack <reserve>[,<commit>]  Set PE reserve/commit stack to <reserve>/
                                       <commit>
         --subsystem <name>[:<version>]
                                       Set PE subsystem to <name> [& <version>]
         --compress-debug-sections[={none|zlib|zlib-gnu|zlib-gabi}]
                                       Compress DWARF debug sections using zlib
         --decompress-debug-sections   Decompress DWARF debug sections using zlib
      -v --verbose                     List all object files modified
      @<file>                          Read options from <file>
      -V --version                     Display this program's version number
      -h --help                        Display this output
         --info                        List object formats & architectures supported
    /opt/tooling/bosch/OSTC_5.1/aarch64-none-linux-gnueabi/bin/aarch64-none-linux-gnueabi-objcopy: supported targets: elf64-littleaarch64 elf64-bigaarch64 elf32-littleaarch64 elf32-bigaarch64 elf32-littlearm elf32-bigarm elf64-little elf64-big elf32-little elf32-big plugin srec symbolsrec verilog tekhex binary ihex
```

## objdump

```bash
objdump
    Usage: /opt/tooling/bosch/OSTC_5.1/aarch64-none-linux-gnueabi/bin/aarch64-none-linux-gnueabi-objdump <option(s)> <file(s)>
     Display information from object <file(s)>.
     At least one of the following switches must be given:
      -a, --archive-headers    Display archive header information
      -f, --file-headers       Display the contents of the overall file header
      -p, --private-headers    Display object format specific file header contents
      -P, --private=OPT,OPT... Display object format specific contents
      -h, --[section-]headers  Display the contents of the section headers
      -x, --all-headers        Display the contents of all headers
      -d, --disassemble        Display assembler contents of executable sections
      -D, --disassemble-all    Display assembler contents of all sections
      -S, --source             Intermix source code with disassembly
      -s, --full-contents      Display the full contents of all sections requested
      -g, --debugging          Display debug information in object file
      -e, --debugging-tags     Display debug information using ctags style
      -G, --stabs              Display (in raw form) any STABS info in the file
      -W[lLiaprmfFsoRt] or
      --dwarf[=rawline,=decodedline,=info,=abbrev,=pubnames,=aranges,=macro,=frames,
              =frames-interp,=str,=loc,=Ranges,=pubtypes,
              =gdb_index,=trace_info,=trace_abbrev,=trace_aranges,
              =addr,=cu_index]
                               Display DWARF info in the file
      -t, --syms               Display the contents of the symbol table(s)
      -T, --dynamic-syms       Display the contents of the dynamic symbol table
      -r, --reloc              Display the relocation entries in the file
      -R, --dynamic-reloc      Display the dynamic relocation entries in the file
      @<file>                  Read options from <file>
      -v, --version            Display this program's version number
      -i, --info               List object formats and architectures supported
      -H, --help               Display this information
```

## readelf

```bash
readelf
    /opt/tooling/bosch/OSTC_5.1/aarch64-none-linux-gnueabi/bin/aarch64-none-linux-gnueabi-readelf -a swu_common_base_checksum_tool_out.out | less
    Usage: readelf <option(s)> elf-file(s)
     Display information about the contents of ELF format files
     Options are:
      -a --all               Equivalent to: -h -l -S -s -r -d -V -A -I
      -h --file-header       Display the ELF file header
      -l --program-headers   Display the program headers
         --segments          An alias for --program-headers
      -S --section-headers   Display the sections' header
         --sections          An alias for --section-headers
      -g --section-groups    Display the section groups
      -t --section-details   Display the section details
      -e --headers           Equivalent to: -h -l -S
      -s --syms              Display the symbol table
         --symbols           An alias for --syms
      --dyn-syms             Display the dynamic symbol table
      -n --notes             Display the core notes (if present)
      -r --relocs            Display the relocations (if present)
      -u --unwind            Display the unwind info (if present)
      -d --dynamic           Display the dynamic section (if present)
      -V --version-info      Display the version sections (if present)
      -A --arch-specific     Display architecture specific information (if any)
      -c --archive-index     Display the symbol/file index in an archive
      -D --use-dynamic       Use the dynamic section info when displaying symbols
      -x --hex-dump=<number|name>
                             Dump the contents of section <number|name> as bytes
      -p --string-dump=<number|name>
                             Dump the contents of section <number|name> as strings
      -R --relocated-dump=<number|name>
                             Dump the contents of section <number|name> as relocated bytes
      -z --decompress        Decompress section before dumping it
      -w[lLiaprmfFsoRt] or
      --debug-dump[=rawline,=decodedline,=info,=abbrev,=pubnames,=aranges,=macro,=frames,
                   =frames-interp,=str,=loc,=Ranges,=pubtypes,
                   =gdb_index,=trace_info,=trace_abbrev,=trace_aranges,
                   =addr,=cu_index]
                             Display the contents of DWARF2 debug sections
      --dwarf-depth=N        Do not display DIEs at depth N or greater
      --dwarf-start=N        Display DIEs starting with N, at the same depth
                             or deeper
      -I --histogram         Display histogram of bucket list lengths
      -W --wide              Allow output width to exceed 80 characters
      @<file>                Read options from <file>
      -H --help              Display this information
      -v --version           Display the version number of readelf
```

# HashTags
#gcc #objcopy #objdump #readelf