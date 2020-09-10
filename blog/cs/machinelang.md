---
layout: notes
section-type: notes
title: System Software II
category: cs
---

* TOC
{:toc}
---

## Slide 6 Machine-Level Programming I: Basics(Cont) 

### Assembly Basics: Registers, Operands, Move

* Assembly Characteristics: Data Types
    * "Integer" data of 1,2,4,8 bytes
    * Instruction Suffixed with **b**(byte), **w**(word), **l**(long), **q**(quad).
    * Acutal size of operand determined by register names
    * Address are always 8 bytes.
 
* x86-64 Integer Registers

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware012.png" height="50%" width="50%">
</center>

* Some history

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware013.png" height="50%" width="50%">
</center>

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware014.png" height="50%" width="50%">
</center>

### Moving Data

* Moving data syntax:

```
movq Source, Dest;
(ALSO movl,movw,movb)
```

* x86-64 can still use 32-bit instructions

```
movl %eax %ebx
```

* Operand Types
    * Immediate: Constant integer data
        * $0x400, $-533
        * Like C constant, but prefixed with '$'
    * Register: One of 16 integer registers
        * Example: %rax, %r13
        * But %rsp reserved for special use
    * Memory
        * Immediate (constant) but NOT prefixed with '$'
        * Have to use 8-byte form for the register! (e.g. %rax)

* movq Operand Combinations

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware015.png" height="50%" width="50%">
</center>

### Simple Memory Addressing Modes

<span id = "jump3"></span>
### Complete Memory Addressing Modes
* Most General Form

D(Rb, Ri, S)

Mem[Reg[Rb]+S*Reg[Ri]+D]

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware016.png" height="50%" width="50%">
</center>

### Example 

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware017.png" height="50%" width="50%">
</center>

**Next Few Slides in this lecture should read carefully**

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware018.png" height="50%" width="50%">
</center>

* In the picture above, we can see that

```
%rax = xp = 0x120 ( which is the address of xp)
(%rax) =  *xp = 123 
(which is looking for the value in the address)
```

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware021.png" height="50%" width="50%">
</center>

* Translate the code above in C
    * %edi shows that variable **a** is 4 bytes
    * 4(%rsi) means from the address now, add 4 bytes for it
    * In array, this means move forward 1 index in int type

```C
int a;
p[1] = a;
```

### Some Arithmetic Operations
* addq a,b => b = b+a
* subq a,b => b = b-a
* imulq;
* salq; <<
* sarq; >> Arithmetic Shift
* shrq; >> Logical Shift
* ...

### Address Computation Instruction
* leaq a,b => b = \& a;
* leaq Src, Dest
    * Src is address move expression(i.e., in the form of D(Ri, Rb, S))
* Uses
    * Computing addresses without a memory reference
    * E.g., translation of **p = &x[i];**

## Slide 7 Machine-Level Programming II: Control

### Control: Condition Codes
* Processor State(x86-84, Partial)
* Information about currently executing program
    * Temporary data(%rax)
    * Location of runtime stack(%rsp)
    * Location of current code control point(%rip)
    * Status of recent tests(CF, ZF, SF, OF)

* Single bit registers
    * CF Carry Flag(for unsigned)
    * SF Sign Flag(for signed)
    * ZF Zero Flag
    * OF Overflow Flag(for signed)

* Setting: Compare
    * cmpq Src1, Src2
    * cmpq b, a like computing a-b without setting destination

* Setting: Test
    * testq Src2, Src1
    * testq b, a like computing a&b

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware022.png" height="50%" width="60%">
</center>

### Conditional Branches
* Conditional Branches
    * If else
    * While
    * For
* Unconditional Branches
    * Break
    * Continue
* In x86, we will refer to branches as "jump" (either condition or unconditional)

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware024.png" height="50%" width="60%">
</center>

* Expressing with Goto Code

* Using Conditional Move

### Loops

* Og is compact but more branches
* O1 is more efficient but larger code size

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware026.png" height="50%" width="60%">
</center>

### Switch Cases
* Jump Table Structure

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware027.png" height="50%" width="60%">
</center>

* Tips: ja sign means that we will compare them as unsigned value 

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware028.png" height="50%" width="40%">
</center>

* Table Structure
    * Each target requires 8 bytes
    * base address at .L4
* Jumping
    * Direct: jmp .L8
    * Indirect: jmp *.L4(,%rdi, 8) => (L4+%rdi\*8)
    * We will get the content(memory) in address above
    * Start of jump table: .L4
    * Scale by factor of 8(address are 8 bytes)
    * Using [Memory Addressing Modes](#jump3)

* Using of Jump Table
    * Allows for very efficient implementation of multi-way branches
    * The time taken to perform switch is independent of the number of switch cases

## Slide 8 Machine-Level Programming III: Procedures

### Mechanisms in Procedures
* Passing control
    * To beginning of procedure code
    * Back to return point
* Passing data
    * Procedure arguments
    * return value
* Memory Management
    * Allocate during procedure execution
    * Deallocate upon return
* Mechanisms all implemented with machine instructions
* **Machine instructions implement the mechanisms, but the choices are determined by designers(called Application Binary Interface, or ABI)**

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware029.png" height="50%" width="60%">
</center>

### Procedures
* Stack structure
* Stack Base Language
    * C/C++, Pascal, Java
* Stack allocated in Frames
* Stack discipline
    * State for given procedure needed for limited time
    * Callee returns before caller does
    * FILO(First In Last Out)

### Stack Frames
* Contents
    * Return Information
    * Local storage
* Stack Pointer
    * %rsp (Address of Stack Top)
* Management
    * Space allocated when enter procedure
        * "Set-Up" code
    * Deallocated whrn return
        * "Clean-Up" code

### x86-64 Stack
...

### Call Chain Example
* After a callee return, the stack pointer will move above

### Instruction that Manipulate the Stack
* pushq Src
    * Fetch operand at Src
    * Decrement %rsp by 8 bytes
* popq Dest
    * Read Value at address given by %rsp
    * Increment %rsp by 8 bytes
    * Store value at Dest

```
popq %rax
movq (%rsp) %rax
```

movq will not change %rsp

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware033.png" height="50%" width="100%">
</center>




### Calling Conventions- Passing Control
* Use stack support procedure call and return
* Procedure call: **Call Label**
    * Push return address on stack
    * Jump to Label
* Return Address:
    * Address of the next instruction right after call
* Procedure return: **ret**
    * Pop address from stack
    * Jump to address

Instruction ***call*** and ***ret*** implicitly manipulate the stack

* %rip updated to point to the next instruction
* %rsp 

(1) When enter into callee, we increase the stack and put the address of %rip into stack top;  
(2) Then the %rip will store the address where callee start and move when procedures in callee goes.  
(3) When callee are done with **ret**, we will fetch the address from %rsp to get next procedure's address

### Calling Convention- Passing Data
<center>
<img class="center medium" src=".//cs_pictures/systemsoftware030.png" height="50%" width="60%">
</center>

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware035.png" height="50%" width="60%">
</center>


* Register Saving Conventions
    * "Caller Saved"/ Call-Clobbering
        * Caller saves temporary values in its frame before the call
    * "Callee Saved"/ Call-Preserving
        * Callee saves temporary values in its frame before using
        * Callee restores them before returning to caller

<span id="jump5"></span>
SUMMARY:
* In a word, caller saved registers can be used as global variable in callee;
* And callee saved registers will be considered as a local variable in callee.
* This means callee can overwrite the callor saved register but cannot do this for callee saved register.
* [Slides make it easier to understand this](https://courses.cs.washington.edu/courses/cse410/17wi/lectures/CSE410-L13-procedures-II_17wi.pdf)

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware031.png" height="50%" width="60%">
</center>
<center>
<img class="center medium" src=".//cs_pictures/systemsoftware032.png" height="50%" width="60%">
</center>

### Managing Local Data

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware036.png" height="50%" width="60%">
</center>

* Example:

<center>
<img class="center medium" src=".//cs_pictures/systemsoftware037.png" height="50%" width="60%">
</center>

* The example above shows that 
    * subq $16, %rsp => allocate 16 bytes for callor
    * When we call the incr() function, we will automatically add the return address for that callee
    * After ret, those space will be destoryed automatically.

### Illustration of recursion

* Saved Recursive Function 
* Callee use [callee-saved](#jump5) register to holds certain value for it in all procedures

<center>
<img class="center medium" class="large"  src=".//cs_pictures/systemsoftware038.png" height="50%" width="70%">
</center>

* Say if we get global long x=0xf in this recursive function, we will have 4 recursive loops in this function. Each loop will create a %rbx in the stack.
* When we finally use ret, we will run every few lines of code (addq, popq) to finally move %rsp to the return address.