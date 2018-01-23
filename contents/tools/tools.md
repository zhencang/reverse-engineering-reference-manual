## *<p align='center'>.tools</p>*

<div align='center'> 
<img src="https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/images/tools/tools.jpg" width="500" height="430"> 
<p align='center'><sub><strong>drawing by <a href="http://www.leejohnphillips.com/">Lee John Phillips</a></strong></sub></p>
</div>

__The Power Of Two__
* When reversing a target, you will likely run various basic static analysis, dynamic analysis, and/or automation tools to identify points of interest for further manual analysis. Some of those tools may also be ran throughout the reversing process to ascertain particular suspicion, but either way, you will be spending the majority of your time inside a disassembler and a debugger. As a result, at least __know how to use a [disassembler](https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/contents/tools/IDA_Tips.md) and a [debugger](https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/contents/tools/GDB_Tips.md) well__.

__Be Cautious...__
* Never be too reliant on any one tool. For most popular tools, depending on their usages, there are ways to [detect their presences](https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/contents/anti-analysis/Anti-Debugging.md#-using-functions-from-dynamically-linked-libraries-to-detect-debuggers-presence-), [hide certain program properties from them](http://www.hexacorn.com/blog/2018/01/04/yet-another-way-to-hide-from-sysinternals-tools/), or [make them not function properly](https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/contents/anti-analysis/Anti-Disassembly.md#-parser-differential-attack-file-format-hacks-). 

---
### *<p align='center'> section overview </p>*
---
* [IDA Tips](IDA_Tips.md)
  * [Addresses Shown In IDA](IDA_Tips.md#-addresses-shown-in-ida-)
  * [Import Address Table (IAT)](IDA_Tips.md#-import-address-table-iat-)
  * [Saving Memory Snapshot From Your Debugger Session](IDA_Tips.md#-saving-memory-snapshot-from-your-debugger-session-)
  * [Useful Shortcuts](IDA_Tips.md#-useful-shortcuts-)
* [GDB Tips](GDB_Tips.md)
  * [Changing Default Settings](GDB_Tips.md#-changing-default-settings-)
  * [User Inputs](GDB_Tips.md#-user-inputs-)
  * [Automation](GDB_Tips.md#-automation-)
  * [Ways To Pause Debuggee](GDB_Tips.md#-ways-to-pause-debuggee-)
  * [Useful Commands](GDB_Tips.md#-useful-commands-)

---
### *<p align='center'> further readings </p>*
---
* [Free Reverse Engineering Tools by Wiremask](https://wiremask.eu/articles/free-reverse-engineering-tools/): list of relevant (still maintained) and FREE reverse engineering tools
* [IDA Alternatives](https://reverseengineering.stackexchange.com/questions/1817/is-there-any-disassembler-to-rival-ida-pro): there is no disassembler that rivals IDA, but getting a IDA license does costs a fortune. Personally, for alternatives, I would recommand [Binary Ninja](https://binary.ninja/) since it only costs 150 dollars instead of a few thousands in comparison to IDA and has an equally clean and interactive GUI interface or [Radare2](https://github.com/radare/radare2) if you don't mind working in the command-line and spending a little more time learning how to use the tool. Plus, Radare2 is FREE

#
<p align='center'><a href="/contents/general/general.md">.general</a> <~ <a href="/README.md#table-of-contents">RERM</a> ~> <a href="/contents/instruction-sets/instruction-sets.md">.instruction-sets</a></p>
