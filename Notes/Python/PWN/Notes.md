pwntools is a CTF framework and exploit development library. Written in Python, it is designed for rapid prototyping and development, and intended to make
exploit writing as simple as possible.

Compiling is used to make the computer understand human-readable code
-> objdump = gives us the assembly code

-> when pc runs a program, and encounters a variable, it needs to store this in memory called stack

-> stacks are lifo = last in-first out
-> push to stack and pop from stack
-> 2 registers(store a single value) for stack =
    -> rsp(stack pointer) = points to the top of the stack
    -> rbp(base pointer) = points to the base of the current stack frame = stack in relation to a function
        -> every-time we enter a function, a new stack frame is created
        -> variables are always at an offset from the base-pointer
        
   -> push -> rsp decreases
   -> pop -> rsp increase
    
-> when we push something to the top of the stack, the stack pointer is decreased, stacks grow downwards
-> when we pop an item from the stack, the stack pointer is increased
    
-------------------------------------------------------------------------------------------

-> word = a unit of data 
        = have increased in size over the decodes
        = now fixed at 16 bits = 2 bytes
        
-> word = 2 bytes
-> dword = 4 bytes
-> qword = 8 bytes


Registers > store a single value > limited number of registers > super fast
Stacks > store many values > stores a lot of info > much slower

Registers can be used for lots of purposes
  > RSP = Stack Pointer
  > RBP = Base Pointer
  > RIP = Instruction Pointer
  
Registers have a size of 8 bytes
  > RBP = Full 8 bytes
  > EBP = 4 bytes
  > BP = 2 bytes
  > BPL = single byte

> when we call a function, we can pass arguments using registers
> rdi -> rsi -> rdx -> rcx -> r8 -> r9  = order of passing upto 6 arguments in a function
> if we have more than 6 arguments, we can store them in the stack
> this is in a 64 bit system
> in a 32 bit system, all arguments are passed onto the stack


> flag register - contains flags - can be 1 or 0
  00: carry flag
  01: always 1
  02: parity flag
  03: always 0
  04: adjust flag
  05: always 0
  06: zero flag
  07: sign flag
  08: trap flag
  09: interrupt flag
  10: direction flag
  11: overflow flag
  12: I/O Privilege Field Lower bit
  13: I/O Privilege Field Higher bit
  14: Nested Task Flag
  15: Resume Flag


