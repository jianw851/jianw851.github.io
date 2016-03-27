---
layout: post
category: [learn]
title:  Assembly on Mac
tagline: by Jian
tags: [Assembly]
---

 Assembly language is the very basic programming language in a Computer. First it is more detailed. Second it is more effcient. Today I am going to try it on my macbook. Although it is not my first time to try assembly, I feel more comfortable and engaged to do so. This airticle will record some of method and tools.  


<!--more-->

## Tool

+ NASM
  
```
  brew install nasm
```

+ Xcode
which contains gcc

this link is a very good materail to learn 64 bit assembly on mac
http://www.idryman.org/blog/2014/12/02/writing-64-bit-assembly-on-mac-os-x/

here is a short example

```
_asm.s
# as hello_asm.s -o hello_asm.o
# ld hello_asm.o -e _main -o hello_asm
.section __DATA,__data
str:
  .asciz "Hello world!\n"

.section __TEXT,__text
.globl _main
_main:
  movl $0x2000004, %eax           # preparing system call 4
  movl $1, %edi                    # STDOUT file descriptor is 1
  movq str@GOTPCREL(%rip), %rsi   # The value to print
  movq $100, %rdx                 # the size of the value to print
  syscall

  movl $0, %ebx
  movl $0x2000001, %eax           # exit 0
  syscall

```
I have already installed gcc on my computer, so I will not install nasm.

---
