## Switch statements

* Case without "break" will goes on (Fall Through)

* ``` c
  switch(x){
    case val_0:
      #Block 1
    case val_1:
      #Block 2
    case val_2:
      #Block 3
  }
  ```

* A jump table

* use $x$ as index to jump

  ```assembly
  movq %rdx, %rcx
  cmpq $6, %rdi # x:6
  ja .L8
  jmp *.L4(,%rdi,8) #address took 8 bytes 
  # .L4 jump table
  ```
* Indirection method

# Machine-Level Programming III: Procedures

## Mechanisms in Procedures

- What dose "return" mean ?
  - Back to **return point** (the next line) / return control
  - Passing data
    - value / arguments
  - Memory management

## Stack Structure

+ Stack grows down (to lower address)
+ `%rsp` Stack pointer
+ `pushq Src` 
+ `popq Dest`  Value is not deleted in stack 

## Control Flow

+ Call & Ret
  + `call label` 
    + Push **retuen address** on stack
    + Jump to label
  +  `ret` 
    + Pop the address
    + Jump to address

## Stack Frame 

* Frame Pointer : `%rsp` 
* Contents in one frame
  * Return information 
  * Local storage (if needed)
  * Temporary space (if needed)

* ````assembly
  subq $16, %rsp #get 16 byte space
  movq $15213, 8(%rsp)
  movl $3000, %esi
  leaq 8(%rsp), %rdi
  call incr
  addq 8(%rsp), %rax
  addq $16, %rsp
  ret

> [!NOTE]
>
> Question: where is 15213 ?  X-8 to X-16 / X to X-8  



---

`moveq movl` "q" means quadword  "l" means "long"

---

## Register Saving Conventions

* Register may be overwritten by callee, so we need to save them before overwritten
* Conventions
  * "Caller Saved" Caller took the responsibility to save 
  * "Callee Saved" Callee took the responsibility to save
  * Determined by ABI



