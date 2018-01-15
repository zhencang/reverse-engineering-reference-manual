## *<p align='center'>.file-formats</p>*

---
### *<p align='center'> section overview </p>*
---
* [ELF Files](ELF_Files.md)
  * [Overview](ELF_Files.md#-overview-)
  * [Linking VS Execution](ELF_Files.md#-linking-vs-execution-)
  * [ELF File Header](ELF_Files.md#-elf-file-header-)
  * [Program Header Table](ELF_Files.md#-program-header-table-)
  * [Section Header Table](ELF_Files.md#-section-header-table-)
  * [Useful Compilation Options To Know For GCC](ELF_Files.md#-useful-compilation-options-to-know-for-gcc-)
  * [Stripped Binary](ELF_Files.md#-stripped-binary-)
  * [Useful Tools To Analyze ELF File](ELF_Files.md#-useful-tools-to-analyze-elf-file-)
* [PE Files](PE_Files.md)
  * [Overview](PE_Files.md#-overview-)
  * [PE File In Memory](PE_Files.md#-pe-file-in-memory-)
  * [Virtual Address(VA) To File Offset Translation](PE_Files.md#-virtual-addressva-to-file-offset-translation-)
  * [DOS Header](PE_Files.md#-dos-header-)
  * [PE Header (IMAGE_NT_HEADERS)](PE_Files.md#-pe-header-image_nt_headers-)
  * [Section Header Table (IMAGE_SECTION_HEADERs)](PE_Files.md#-section-header-table-image_section_headers-)
  * [Overlay](PE_Files.md#-overlay-)

---
### *<p align='center'> further readings </p>*
---
* [Kaitai Struct](http://kaitai.io/): a declarative language for visualizing binary file formats. Once you describes a file format in Kaitai Struct you can compile it into one of the supported languages. The compiled module will expose a straightforward API to access fields in that file format
* [Visual Reverse Engineering](https://www.youtube.com/watch?v=4bM3Gut1hIk): With binary visualization, it doesn't need to know how to parse the file format but each file format will have its own unique form. Peculiarities within the same file format (e.g. packed vs not packed PE executable) will also cause resulting visualizations to differ, allowing you to identify the peculiar traits. An example of a popular, free-to-use binary visualization tool is [VELES](https://codisec.com/veles/)

#
<p align='center'><a href="/contents/languages/languages.md">.languages</a> <~ <a href="/README.md#table-of-contents">RERM</a> ~> <a href="/contents/anti-analysis/anti-analysis.md">.anti-analysis</a></p>
