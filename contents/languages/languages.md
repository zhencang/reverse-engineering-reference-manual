## *<p align='center'>.languages</p>*

__Historical Context__
* Back in the 50s, people were still programming in assembly. It was also at this time that programming languages were being developed left and right with the hope of reducing costs (programming in assembly was a tedious and time-consuming task and not to mention also a maintenance nightmare). The transition from programming in assembly to programming in a higher-level language was not as easy as the transition from programming in machine code to programming in assembly from a decade earlier. The transition to programming in assembly from programming in machine code was intuitive since it made the software development lifecycle faster, but most importantly, with zero performance penalty since one assembly instruction translate to exactly one machine code instruction. Programming in a higher-level language was a completely different story. A higher-level programming statement can be translated to multiple machine code instructions and different compiler implementations for the same language also meant different sets of machine code output. Early skepticism of compiled langauges was inevitable since compiler was not able to generate code as efficient as hand-written assembly. One of the first compiler writers, Grace Hopper, was no stranger to such skepticism as she had said: "I had a running compiler and nobody would touch it...they carefully told me, computers could only do arithmetic; they could not do programs..." Fortunately over times, people slowly came into acceptance of compiled languages since the upsides (reduced programming and mantenance costs) outvalue their downsides (performance). And through decades of compiler research since the 50s, compilers' output had became as efficient as hand-written assembly, if not more.   

__The Catalyst For Modern Computing__
* Programming in a higher-level language frees programmers from having to worry about how to interact with the underlying hardware. For example, in assembly there is no notion of variables, only registers and memory locations and to it even harder to program you only have a limited amount of general-purpose registers that you can modify. Programming languages abstract away those hardware interactions, allowing programmers to focus more on the computational task that they wanted to solve. This, in my opinion, is the catalyst that leads to the proliferation of various computing sub-fields, from technology that enables web development to technology that implements machine learning. A lot of what's possible today will not be availiable if we are still programming in assembly.

__Compiled vs Interpreted Programming Languages From A Reversing Perspective__
* Although there are many differences between a compiled and interpreted language, the most glaring difference is that an interpreted language doesn't compile all the way down to machine code. It compiles to an intermediate language that is then interpreted (translated to machine code and then executed) during runtime. This property also means that interpreted languages are platform independent: the same source code can be ran anywhere as long as the corresponding interpreter is present. So what does this means to a reverse engineer? __(1)__ When you are reversing an executable file, not all of them will contain machine code corresponding to x86, x64, or ARM instruction set. __(2)__ A bad reversing habit is to drop an executable file you wanted to analyze into IDA first without doing other basic static and/or dynamic analysis tools to get a feel for what kind of executable file it is. IDA may still be the best universal disassembler out there, but it is actually not that great at disassembling code compiled to an intermediate language. Instead, use a disassembler targeting that specific interpreted language. For example, with compiled Python (.pyc) use the built-in Python dis module. __(3)__ Since they are only compiled down to an intermediate form, a lot less information for the source level is lost compared to those that get compiled down to machine code. This is why a decompiler targeting an interpreted language like Python, or .NET works better than a decompiler targeting a compiled language. 
* Although compiled languages targeting the same CPU all compile down to the same instruction set, their outputs differ greatly in that they are still idiosyncratic to the original source languages. For example, because C++ supports method overloading its function names will be mangled (technique: name mangling) and since C doesn't support method overloading it will be easy to identify if a compiled code is compiled from C++ by just looking at the import section. If you can, you always want to try to identify the original source language. Knowing the source language makes it easier for you to relate a block assembly code back to a higher level construct, allowing you to piece together what the assembly code is doing quicker.     

---
### *<p align='center'> section overview </p>*
---
* [C++ Reversing](C++_Reversing.md)
  * [thiscall](C++_Reversing.md#-thiscall-)
  * [How An Object Is Represented](C++_Reversing.md#-how-an-object-is-represented-)
  * [Name Mangling](C++_Reversing.md#-name-mangling-)
* [Python Reversing](Python_Reversing.md)
  * [PVM (Python Virtual Machine)](Python_Reversing.md#-pvm-python-virtual-machine-)
  * [The 3 Tuples Associated With Function Object](Python_Reversing.md#-the-3-tuples-associated-with-function-object-)
  * [Python Bytecode Instructions](Python_Reversing.md#-python-bytecode-instructions-)

---
### *<p align='center'> further readings </p>*
---
*work in progress...*

#
<p align='center'><a href="/contents/instruction-sets/instruction-sets.md">.instruction-sets</a> <~ <a href="/README.md#table-of-contents">RERM</a> ~> <a href="/contents/file-formats/file-formats.md">.file-formats</a></p>
