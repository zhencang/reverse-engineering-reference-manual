## *<p align='center'>.encodings</p>*

<div align='center'> 
<img src="https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/reorganize/images/instruction-sets/isa.png"> 
<p align='center'><sub><strong>courtesy of <a href="https://www.eeweb.com/quizzes/instruction-set-architecture">EEWeb</a></strong></sub></p>
</div>

__The Interface Between Software And Hardware__
* An instruction set provides an interface for programmer to instruct a re-programmable (general-purpose) computer on how to interact with its underlying hardware while abstracting away the implementation details of those hardware components. Although the idea of a general purpose computer was conceived in 1837 by Charles Babbage, a working general purpose computer (ENIAC) was not built until 1945. Earlier computers such as Atanasoff–Berry (used to solve linear equations) and Bombe (used for deciphering Enigma encrypted messages) are special-purpose computers that
 are hard-wired to perform a specific task, which means that you are unable to utilize their underlying hardware to do anything else. An instruction set is the gateway to utilize a general purpose computer's flexibility, allowing one to create programs aim at accomplishing varying tasks, from space shuttle guidance to weather prediction. It presents that gateway in human-readable mnemonics (English words), where each mnemonic has an unique set of zeros and ones that corresponds to an operation a CPU with the same instruction set implementation would know how to perform. An instruction set is said to be Turing Complete if it can perform any computational task. The followings instruction sets I will talk about are all Turing Complete. On a funny note, it turns out that [one instruction from x86 is enough to be Turing Complete](https://www.cl.cam.ac.uk/~sd601/papers/mov.pdf).

---
### *<p align='center'> section overview </p>*
---
* [String Encoding](String_Encoding.md)
  * [ASCII](String_Encoding.md#)
  * [Unicode](String_Encoding.md#)
  * [Cause Of Garbled Text](String_Encoding.md#)
* [Data Encoding](Data_Encoding.md)
  * [Overview](Data_Encoding.md#)
  * [PE File In Memory](Data_Encoding.md#)
  * [Virtual Address(VA) To File Offset Translation](Data_Encoding.md#)
  * [DOS Header](Data_Encoding.md#)
  * [PE Header (IMAGE_NT_HEADERS)](Data_Encoding.md#)

---
### *<p align='center'> further readings </p>*
---
*work in progress...*

#
<p align='center'><a href="/contents/anti-analysis/anti-analysis.md">.anti-analysis</a> <~ <a href="/README.md#table-of-contents">RERM</a> ~> <a href="/README.md#table-of-contents">RERM</a></p>
