### [.anti-analysis](anti-analysis.md)[__Anti-Emulation__]

---
#### *<p align='center'> Definition </p>*
---
* Using emulation allows reverse engineer to bypass many anti-debugging techniques

---
#### *<p align='center'> Detection through Syscall </p>*
---
* Invoke various uncommon syscalls and check if it contains expected value. Since there are OS features not properly implemented, it means that the process is running under emulation

---
#### *<p align='center'> CPU Inconsistencies Detection </p>*
---
* Try executing privileged instructions in user mode. If it succeeded, then it is under emulation
* WRMSR is a privileged instruction (Ring 0) that is used to write values to a MSR register. Values in MSR registers are very important. For example, the SYSCALL instruction invokes the system-call handler by loading RIP from IA32_LSTAR MSR. As a result, WRMSR instruction cannot be executed in user-mode  

---
#### *<p align='center'> Timing Delays </p>*
---
* Execution under emulation will be slower than running under real CPU

---
#### *<p align='center'> Number of Cores </p>*
---
* The number of cores under emulation could be smaller than the number of cores on the host machine
