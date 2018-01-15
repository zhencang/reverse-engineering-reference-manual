## *<p align='center'>.anti-analysis</p>*

---
### *<p align='center'> section overview </p>*
---
* [Obfuscation](Obfuscation.md)
  * [Definition](Obfuscation.md#-definition-)
  * [Original Entry Point (OEP) Hiding](Obfuscation.md#-original-entry-point-oep-hiding-)
  * [Functions In/Out-Lining](Obfuscation.md-functions-inout-lining-)
  * [Opcode Obfuscation](Obfuscation.md#-opcode-obfuscation-)
  * [Dynamically Computed Target Addresses](Obfuscation.md#-dynamically-computed-target-addresses-)
  * [Dead Code Insertion](Obfuscation.md#-dead-code-insertion-)
  * [Junk Code Insertion](Obfuscation.md#-junk-code-insertion-)
  * [Pattern-Based Obfuscation](Obfuscation.md#-pattern-based-obfuscation-)
  * [Destruction of Sequential and Temporal Locality (Spaghetti Code)](Obfuscation.md#-destruction-of-sequential-and-temporal-locality-spaghetti-code-)
  * [Opaque Predicate](Obfuscation.md#-opaque-predicate-)
  * [Control-Flow Graph Flattening](Obfuscation.md#-control-flow-graph-flattening-)
  * [Irreducible Programs](Obfuscation.md#-irreducible-programs-)
  * [Constant Unfolding](Obfuscation.md#-constant-unfolding-)
  * [Arithmetic Substitution via Identities](Obfuscation.md#-arithmetic-substitution-via-identities-)
  * [Array-Based Obfuscation](Obfuscation.md#-array-based-obfuscation-)
  * [Imported Function Obfuscation](Obfuscation.md#-imported-function-obfuscation-)
* [Anti-Disassembly](Anti-Disassembly.md)
  * [Disassembly Techniques](Anti-Disassembly.md#-disassembly-technique-)
  * [Disassembly Desynchronization](Anti-Disassembly.md#-disassembly-desynchronization-)
  * [Function Pointer Problem](Anti-Disassembly.md#-function-pointer-problem-)
  * [Processer-Based Control Indirection](Anti-Disassembly.md#-processer-based-control-indirection-)
  * [Thwarting Stack-Frame Analysis](Anti-Disassembly.md#-thwarting-stack-frame-analysis-)
  * [Parser Differential Attack (File Format Hacks)](Anti-Disassembly.md#-parser-differential-attack-file-format-hacks-)
* [Anti-Debugging](Anti-Debugging.md)
  * [Using Functions from Dynamically Linked Libraries to Detect Debugger's Presence](Anti-Debugging.md#-using-functions-from-dynamically-linked-libraries-to-detect-debuggers-presence-)
  * [Using Flags within the PEB structure to Detect Debugger's Presence (Windows)](Anti-Debugging.md#-using-flags-within-the-peb-structure-to-detect-debuggers-presence-windows-)
  * [Breakpoint Detection](Anti-Debugging.md#-breakpoint-detection-)
  * [Interrupts](Anti-Debugging.md#-interrupts-)
  * [Timing Checks](Anti-Debugging.md#-timing-checks-)
  * [Detection Before main()](Anti-Debugging.md#-detection-before-main-)
* [Anti-Emulation](Anti-Emulation.md)
  * [Definition](Anti-Emulation.md#-definition-)
  * [Detection through Syscall](Anti-Emulation.md#-detection-through-syscall-)
  * [CPU Inconsistencies Detection](Anti-Emulation.md#-cpu-inconsistencies-detection-)
  * [Timing Delays](Anti-Emulation.md#-timing-delays-)
  * [Number of Cores](Anti-Emulation.md#-number-of-cores-)
* [Bonus](Bonus.md)
  * [Quote To Remember](Bonus.md#-quote-to-remember-)

---
### *<p align='center'> further readings </p>*
---
* [The "Ultimate" Anti-Debugging Reference](http://anti-reversing.com/Downloads/Anti-Reversing/The_Ultimate_Anti-Reversing_Reference.pdf): a comprehensive Windows anti-debugging guide by Peter Ferrie 

#
<p align='center'><a href="/contents/file-formats/file-formats.md">.file-formats</a> <~ <a href="/README.md#table-of-contents">RERM</a> ~> <a href="/contents/encodings/encodings.md">.encodings</a></p>
