# .general-knowledge

## *<p align='center'> int 0x7374617274 </p>*
* __What is Reverse Engineering?__: [the science of man-made things](https://medium.com/@againsthimself/in-defense-of-reverse-engineering-e07fe19b26c)
* __Threads__: a process is a container for execution. A thread is what the OS executes
  * A process that doesn't utilizes multi-threading still contains a single thread

<div align='center'> 
<img src="https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/images/general-knowledge/int_0x7374617274/4_01_ThreadDiagram.png" width="469" height="270">
<p align='center'><sub><strong>single threaded vs multi-threaded process</strong></sub></p>
</div>

* __start IS NOT main__: entry point of a binary (start function) is not main. A program's startup code (how main is set up and called) depends on the compiler and the platform that the binary is compiled for
  * Even if no library is statically compiled into the binary, part of the .text section will contain code that is irrelevant to the source code

<div align='center'> 
<img src="https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/images/general-knowledge/int_0x7374617274/start_v_main.PNG"> 
<p align='center'><sub><strong>32-bit ELF binary compiled by gcc</strong></sub></p>
</div>

* __Random Number Generator__: randomness requires a source of entropy (seed), which is an unpredictable sequence of bits that can come from the OS observing its internal operations or ambient factors. Algorithms using a seemingly unpredictable sequence of bits as seed are known as pseudorandom number generators, because while their output are not random, they still pass the statistical tests of randomness
  * [basic pseudorandom number generator using srand, rand, and time](https://gist.github.com/yellowbyte/4c36b9fffa73d79fa739f75a5ea951c9)
* __Software Breakpoint__: debugger reads and stores the first byte of instruction and then overwrites that first byte with 0xCC (INT3). When CPU hits the breakpoint (0xCC), OS kernel sends SIGTRAP signal to process, process execution is paused by the debugger, and debugger's internal lookup occurs to flip the original byte back

<div align='center'> 
<img src="https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/images/general-knowledge/int_0x7374617274/soft_bp.png"> 
<p align='center'><sub><strong>software breakpoint</strong></sub></p>
</div>

* __Hardware Breakpoint__: set at CPU level in special registers called debug registers
  * Debug registers (DR0 through DR7)
    * DR0-DR3: stores addresses of hardware breakpoints
    * DR4-DR5: reserved
    * DR6: status register that contains information on which debugging event has occurred
    * DR7: stores breakpoint conditions and the lengths of breakpoints for DR0-DR3
  + Before CPU attempts to execute an instruction, it first checks whether the address is currently enabled for a hardware breakpoint. If the address is stored in debug registers DR0–DR3 and the read, write, or execute conditions are met, an INT1 is fired and the process halts

<div align='center'> 
<img src="https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/images/general-knowledge/int_0x7374617274/hardware_bp.png" width="469" height="270"> 
<p align='center'><sub><strong>hardware breakpoint</strong></sub></p>
</div>

* __Memory Breakpoint__: changes the permissions on a region, or page, of memory
  + Guard page: Any access to a guard page results in a one-time exception, and then the page returns to its original status. Memory breakpoint changes permission of the page to guard

<div align='center'> 
<img src="https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/images/general-knowledge/int_0x7374617274/memory_bp.png"> 
<p align='center'><sub><strong>memory breakpoint</strong></sub></p>
</div>

* __Endianness__: Intel x86 and x86-64 use little-endian format. It is a format where multi-bytes datatype (e.g. integer) has its least significant byte stored in the lower address of main memory 
  * Value stored in RAM is in little-endian but when moved into a register will be in big-endian. This is why even though bytes representing an integer is flipped in memory, it will be in its original form when moved into a register

<div align='center'> 
<img src="https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/images/general-knowledge/int_0x7374617274/endianness.png"> 
<p align='center'><sub><strong>integer 599 (0x257) in memory vs in register</strong></sub></p>
</div>