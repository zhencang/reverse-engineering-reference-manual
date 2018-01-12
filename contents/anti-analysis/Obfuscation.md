### [.anti-analysis](anti-analysis.md)[__Obfuscation__]

---
#### *<p align='center'> Definition </p>*
---
* __Definition__: Program transformation techniques that output a program that is semantically equivalent (execute the same) to the original program but is more difficult to analyze

---
#### *<p align='center'> Original Entry Point (OEP) Hiding </p>*
---
* OEP can be hidden through packing. A packer can compress or encrypt a whole executable and inject an unpacking stub that unpack (decompress or decrypt) the executable during runtime. This will hide the OEP and also the original executable (such as the text, data, rsrc sections) from static analysis
* __Tail Jump__: an instruction that jumps from the unpacking stub to OEP after the unpacking stub finishes
* __Signs Of Packer Usage__: 
  * Unusually high file entropy 
  * Program behavior that mimics the way system loader loads a executable file into memory
* __How To Hide From Detection__: 
  * Instead of encrypting/packing the whole binary, only encrypt/pack a small section of it (e.g. .text section) to avoid high file entropy

---
#### *<p align='center'> Functions In/Out-Lining </p>*
---
* Performs operations that create inline and outline functions randomly and through multiple passes to obfuscate the call graph  
* __Inline Functions__: a function that is merged into the body of its caller 
* __Outline Functions__: inverse of Inline function where a subportion of a function is extracted to create another function. The subportion of this function is then replaced with a CALL instruction that calls the new function 

---
#### *<p align='center'> Opcode Obfuscation </p>*
---
* An effective technique for preventing correct disassembly by displaying opcodes that need to be re-interpreted/altered during runtime before being executed by the CPU 
* __Self-Modifying Code__: disassembly shows the encoded/encrypted opcodes. During runtime, the encoded/encrypted opcodes are decoded/decrypted, revealing the opcodes that will actually be executed. Encoding/encrypting portions of a program can hinder static analysis because disassembly is not possible (if it is, it will show false disassembly instead) and hinder debugging because placing breakpoints is difficult. For example, even if the start of an instructions is known, breakpoint cannot be placed until the instruction have been decoded/decrypted
* __Virtual Obfuscation (Runtime Code Generation)__: parts of the program are compiled to the bytecode that corresponds to the instruction set of an undocumented interpreter (usually one that the obfuscator wrote him or herself). The interpreter will be a part of the protected program such that during runtime, the interpreter will translate those bytecode into machine code that corresponds to the original architecture (e.g. x86). This method can also prevent the dumping of a whole section of de-obfuscated opcodes from memory during runtime like the Self-Modifying Code method would

---
#### *<p align='center'> Dynamically Computed Target Addresses </p>*
---
* An address to which execution will go to is computed at runtime. This makes it hard to tell what the call destination is statically

---
#### *<p align='center'> Dead Code Insertion </p>*
---
* Inserts useless code that doesn't affect a program's functionalities. To do this, an obfuscator needs to know which registers are dead (e.g. does not contain important values) so that it can insert instructions that modify those dead registers 
  * Can be resolved by applying dead code elimination

---
#### *<p align='center'> Junk Code Insertion </p>*
---
* Inserts code that never get executed 

---
#### *<p align='center'> Pattern-Based Obfuscation </p>*
---
* Transforms a sequence of instructions into another sequence of instructions that is more complicated but semantically the same
* This task could be difficult since the obfuscated sequence can look semantically the same but does not preserve CPU state, which can cause later program behavior to be semantically nonequivalent. This can happen if the new sequence's side effects (modify/didn't modify the flags or modify/didn't modify the stack) is opposite that of the original sequence's side effects  
* [Reverser's Living Nightmare](https://0x00sec.org/t/what-a-living-nightmare-looks-like/2087)
* Can be resolved by applying peephole optimization

---
#### *<p align='center'> Destruction of Sequential and Temporal Locality (Spaghetti Code) </p>*
---
* Code within a basic block will be right next to each other __(sequential locality)__ and basic blocks relating to each other will be placed in close proximity to maximize instruction cache locality __(temporal locality)__. To obstruct this property and make disassembly harder to understand, a basic block can be further divided and randomized using unconditional jumps

---
#### *<p align='center'> Opaque Predicate </p>*
---
* Transforms a trivial opaque predicate into a non-trivial opaque predicate. On the source code level, a trivial opaque predicate's conditional construct will be optimized away if compiler knows that it will always be evaluated to either True or False. For a non-trivial opaque predicate, even though the predicate will always evaluate to either True or False, the underlying code construct makes it hard to figure that out statically. As a result, compiler doesn't optimize away the conditional construct
* [Environment-Based Opaque Predicates](https://reverseengineering.stackexchange.com/questions/2340/how-to-design-opaque-predicates)
* Uses global variables instead of constants in the predicates. Compiler won't be able to optimize the conditional construct since it can't assume the value of global variables 
* Introduces entropy into the predicate (e.g. using rand() function)

---
#### *<p align='center'> Control-Flow Graph Flattening </p>*
---
* Obfuscates control flow by replacing a group of control structures with a dispatcher. Each basic block updates the dispatcher's context so it knows which basic block to execute next

---
#### *<p align='center'> Irreducible Programs </p>*
---
* Transform a loop into more complicated construct on the source code level. Duplicate the loop and insert a conditional construct that could reach either loop. Obsfucate each loop accordingly. When compiled, compiler cannot optimize away the conditional construct since even though both path are functionally the same they are syntactically different, so both obfuscated loops remain in compiled binary

---
#### *<p align='center'> Constant Unfolding </p>*
---
* Replaces constant with unnecessary computations that will output the same constant
* This can be accomplished on the source code level if the variable is assigned as volatile in C. The volatile keyword tells the compiler to not optimize this variable so you can perform unnecessary computations on it without worrying that the compiler will optimize those computations away 
* Can be resolved by applying constant folding optimization on the obfuscated sequence of instructions that performs constant unfolding

---
#### *<p align='center'> Arithmetic Substitution via Identities </p>*
---
* Replaces a mathematical statement with one that is more complicated but semantically the same

---
#### *<p align='center'> Array-Based Obfuscation </p>*
---
* Alters the data structures used in the program to make it harder to analyze 
* __Aggregation__: splits, merges, folds, or flattens an array. [This technique can be used to hide the intended string](https://youtu.be/7IKIzsXr3Z8?t=1964) or simply makes an array harder to analyze by merging junk array with the actual array
* __Re-Ordering__: obfuscation technique that re-orders the array. The indices used to access elements in the array now needs to be updated and can be made more complicated by using a function that maps indice i to the new indice
* __Encoding__: alters how the program interprets stored data. For example, initialize an index i by 2i instead. When the index i needs to be used, use the expression i/2 instead. It is also commonly used to hide readable strings by only storing the encoded strings in the binary and decode those strings during runtime 
* __Table Interpretation__: loads an array with call destinations and junk data. Instead of directly calling those functions, call them indirectly by indexing the array  

---
#### *<p align='center'> Imported Function Obfuscation (makes it difficult to determine which shared libraries or library functions are used) </p>*
---
* Have the program’s import table be initialized by the program itself. The program itself loads any additional libraries it depends on, and once the libraries are loaded, the program locates any required functions within those libraries
* (Windows) use LoadLibrary function to load required libraries by name and then perform function address lookups within each library using GetProcAddress
* (Linux) use dlopen function to load the dynamic shared object and use dlsym function to find the address of a specific function within the shared object
