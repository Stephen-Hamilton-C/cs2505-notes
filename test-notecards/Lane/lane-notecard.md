# CS 2505 Exam 2 Notecard

## 32 bit Registers
| | |
| :-----: | :-------: |
| %eax | %ax (%ah \| %al) |
| %ecx | %cx (%ch \| %cl) |
| %edx | %dx (%dh \| %dl) |
| %ebx | %bx (%bh \| %bl) |
| %esi | %si |
| %edi | %di |
| %esp | %sp |
| %ebp | %bp |

## 64 bit Registers
| | |
| :-----: | :-------: |
| %rax | %eax |
| %rcx | %ecx |
| %rdx | %edx |
| %rbx | %ebx |
| %rsi | %esi |
| %rdi | %edi |
| %rsp | %esp |
| %rbp | %ebp |

 * Designer of computer arch: John Von Neuman, Processor based off of: Intel 8086

| char | name | size |
| :--: | :--: | :--: |
| b    | byte | 8 bits |
| s    | short | 16 bits |
| w    | word | 32 bits |
| l    | long | 32/64 bit floating point |
| q    | quad | 64 bits |

 * %rsp - keeps track of the "top" of the stack
 * %rbp - keeps track of the current func's stack frame
 * General format for cmds: cmd? src, dest
 * (registry) = dereference

* Math Commands: add, sub, imul, neg, inc, dec
* sal - shift left
* sar - shift right and preserve most significant bit (sign)
* shr - sar without preserving significant bit

* left shift - multiply by 2^n where n is the amount you shift by
* right shift - divide by 2^n unreliably

## Jump Instructions

| Instruction | When it Jumpts |
| :---------: | :------------: |
| je/jz | == 0 |
| jne/jnz | !== 0 |
| js | < 0 |
| jns | <= 0 |
| jg/jnl | > (signed) |
| jge/jnl | >= (signed) |
| jl/jnge | < (signed) |
| jle/jng | <= (signed) |
| jq/jnbe | > (unsigned) |
| jae/jnb | >= (unsigned) |
| jb/jnae | < (unsigned) |
| jbe/jna | <= (unsigned) |

 * call: stores the address of the next instruction on the stack then enters the function

 * pushq: pushes a pointer onto the stack so the address can be returned to later
 * popq removes a pointer from the top of the stack so it can be returned to

 * leave: sets %rsp to %rbp, then pops the top of the stack into %rbp

* ret: pops the top of the stack into %rip (sets the address of the next instruction)

## Registers used for Parameters and Return Values
| 32 bit | 64 bit |
| :----: | :----: |
| %edi   | %rdi   |
| %esi   | %rsi   |
| %edx   | %rdx   |
| %ecx   | %rcx   |
| %ebx   | %r8   |
| %eax   | %r9   |

 * General form for Pointers:
```
D (Rb, Ri, S) = Rb + (Ri * S) + D
```
where:
 * D = displacement
 * Rb = base register
 * Ri = index register
 * S = scale(1, 2, 4, or 8)
 * () = dereference
 * **Note:** if a value is missing, it is simply left out of the calc

 * leaq: loads the effective address of src into dest