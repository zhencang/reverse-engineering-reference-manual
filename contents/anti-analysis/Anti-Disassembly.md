### [.anti-analysis](anti-analysis.md)[__Anti-Disassembly__]

---
#### *<p align='center'> Disassembly Techniques </p>*
---
* __Linear Sweep__: disassembling one instruction at a time linearly. Problem: code section of nearly all binaries will also contain data that isn’t instructions 
* __Recursive Descent__: disassembling program based on control flow 
  * __Example Implementation__: for conditional branch, it will process false branch first and note to disassemble true branch later. For unconditional branch, it will add destination to the end of list of places to disassemble in future and then disassemble from that list. For call instruction, most will disassemble the bytes after the call first and then the called location. If there is conflict between the true and false branch when disassembling, disassembler will trust the one it disassembles first
* [Binary Ninja disassembler uses both linear sweep and recursive descent to identify functions](https://binary.ninja/2017/11/06/architecture-agnostic-function-detection-in-binaries.html)

---
#### *<p align='center'> Disassembly Desynchronization </p>*
---
* Causes disassembly tools to produce an incorrect program listing. Works by taking advantage of the assumptions made by flow-oriented disassemblers. For every assumption it makes (e.g. process false branch first), there is a corresponding anti-disassembly technique. Desynchronization has the greatest impact on the disassembly, but it is easily defeated by reformatting the disassembly to reflect the correct instruction flow
* __Opaque Predicate__: conditional construct that looks like conditional code but actually always evaluates to either true or false 
  * __Jump Instructions With The Same Target__: JZ follows by JNZ. Essentially an unconditional jump. The bytes following JNZ instruction could be data but will be disassembled as code
  * __Jump Instructions With A Constant Condition__: XOR follows by JZ. It will always jump so bytes following false branch could be data but will be disassembled as code
* __Impossible Disassembly__: a byte is part of multiple instructions. Disassembler cannot represent a byte as part of two instructions. Either can the processor, but it doesn't have to because it just needs to execute the instructions 

---
#### *<p align='center'> Function Pointer Problem </p>*
---
* If a function is called indirectly through pointers (on the stack), IDA xref will only record the first usage (i.e. when the offset is loaded onto the stack). As a result, xref will not show the various locations that the function could have been called from

---
#### *<p align='center'> Processer-Based Control Indirection </p>*
---
* __CALL Instruction Abuse__: Using CALL instruction to jump to new location instead of a function's entry point. The address pushed onto the stack by CALL can be discarded with the instruction ADD ESP, 4. This will cause false disassembly since the disassembler will try label the CALL location as a function's entry point when it's not
* __Return Pointer Abuse__: RET is used to jump to function or other location instead of returning from function using the PUSH, RET sequence. Disassembler won’t show any code cross-reference to the target being jumped to. Also, disassembler will prematurely terminate the function since RET is supposed to be used for returning from function, resulting in false disassembly

---
#### *<p align='center'> Thwarting Stack-Frame Analysis </p>*
---
* Technique to mess with IDA when deducing numbers of parameters and local variables. For example, the code makes a conditional jump that's always false but in true branch add absurd amount to ESP. If the disassembler chooses to believe the true branch, the numbers of local variables will be incorrect

---
#### *<p align='center'> Parser Differential Attack (File Format Hacks) </p>*
---
* Makes modifications to the ELF file such that it will still execute fine, but the disassembler/debugger will not work properly if you loads a binary into it. Similar techniques can be done on other file format like Portable Executable (PE) as well
* __Tampering/Removing Section Headers (Linux)__: makes tools such as gdb and objdump useless since they rely on the section headers to locate information regarding the various sections. Segments are necessary for program execution, not sections. Section headers table is for linking and debugging
  * "The biggest fuck up that (most) analysis tools are doing is that they are using the section headers table of the ELF file to get information about the binary...[because] sections contain more detailed information" - Andre Pawlowski
  * Modifying section headers' flag fields will make disassembler like IDA Pro to display incorrect disassembly listings. For example, changing .text section's flag from AX (alloc and execute) to WA (write and alloc), even though it still maps to the LOAD segment with flags RE (read and execute), will trick IDA into not disassembling main along with other local functions. It's because the section headers table tells IDA that the area those functions reside in is not executable
  * In addition to changing the section headers' flags, if we include fake .init section we can trick IDA into not disassembling any of the code starting from the entry point. This can happen since IDA will try to disassemble the .init section before the entry point. But if the .init section overlaps with the entry point, then entry point will not get disassembled at all, especially when the entry point is not marked as executable in the section headers (by messing with the section flag)
  * The entry point provided in the ELF Header is in virtual address. To get the actual offset, find the section that the entry point's virtual address fall under. Once you identified the section, use the section header to figure out entry point's offset: (e_entry - sh_addr) + sh_offset. So if you alter sh_addr (virtual address) field of the section that contains the entry point, disassembler that relys too much on the section headers table (e.g. IDA) won't be able to find the correct entry point in the file. This technique won't work on Radare2 since it prefers information in program headers even if the section headers exist 
  * __Mixing Symbols__: appends a fake dynamic string table to the end of the binary and overwrite offset of .dynstr entry in section headers table with offset of the fake dynamic string table. This will make imported functions display the fake symbol names
  * If you remove the section headers table, disassembler/debugger will have to rely on program headers even though program headers give us less information. For example, .text, .rodata, and dynsym all belong to the same segment. And without section headers table, we won't be able to differentiate between the sections within a segment. But fully relying on program headers can also lead to failure. For example, another technique to make IDA fail to load an ELF file is to find a program header that is not required for loading and change the offset field to point to a location that is outside the binary
  * __ELF Header Modification__: inserting false information into ELF Header to discourage analysis
    * Simply zero-ing out information regarding section headers table in the ELF Header (e_shoff, e_shentsize, e_shnum, e_shstrndx) can make tools such as readelf and Radare2 unable to display sections even though Section Headers Table still exists within the binary
    * The 6th byte of the ELF Header is EI_DATA, residing within e_ident array, which makes up the first 16 bytes of the ELF Header. EI_DATA specifies the data encoding of the processor-specific data in the file (unknown, little-endian, big-endian). Modifying EI_DATA after compilation will not affect program execution, but will make tools such as readelf, gdb, and radare2 to not work properly since they use this value to interpret the binary

#
<p align='center'><a href="Obfuscation.md">Obfuscation</a> <~ <a href="/README.md#-reverse-engineering-reference-manual-beta-">RERM</a>[<a href="anti-analysis.md">.anti-analysis</a>] ~> <a href="Anti-Debugging.md">Anti-Debugging</a></p>
