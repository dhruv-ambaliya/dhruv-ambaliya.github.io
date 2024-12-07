---
layout: blog_item
title:  "FactCheck CTF - Walkthrough"
date:   2024-08-02 11:00:60
author: Dhruv Ambaliya
description: 'picoCTF2024 FactCheck - Walkthrough Guide'
categories: [walkthroughs]
keywords: "penetration testing, security research, CTF, hacking, reverse engineering, pen testing tools, cheat sheet, hacking blog, security blog, hacking tutorials, security tutorials, CTFS walkthroughs, boot2root, walkthroughs, hacking tools, hacking tools documentation, testing tools" 
tags:
- CTF
- reverse-engineering
---


<div class="coffee-rating">
<table>
      <tbody>
        <tr>
           <td>
               <p><code>Difficulty Rating:</code></p>
           </td>
           <td>
               <p><i class="fa fa-solid fa-fire"> Medium</i></p>
           </td>
        </tr>
      </tbody>
</table>
</div>

* list element with functor item
{:toc}

## Description

This binary is putting together some important piece of information... Can you uncover that information? Examine this file. Do you understand its inner workings? In this challenge, you are presented with an executable file named “bin”. Since it was a
64-bit ELF executable. When running the program, nothing is printed on the shell, and the process just terminates.

**Download:** [Binary](https://artifacts.picoctf.net/c_titan/191/bin)


## Enumeration

![factcheck_des](/img/blog/factCheck/factcheck_des.webp)

I ran the strings command and found an incomplete flag in the output. Adding hello world and closing the brackets didn't work.

![exec](/img/blog/factCheck/exec.png)

I used Ghidra, an open-source binary analysis tool, to examine the disassembled code and gain insights into the compiled binary's structure and functionality.

## Open it in Disassembler

![ghidra](/img/blog/factCheck/ghidra.png)

I analyzed the file in Ghidra and found a main function with calls to std::allocator&lt;char&gt;. The code likely dynamically allocates memory for strings, but without further understanding, it's difficult to determine its purpose.

![decompile](/img/blog/factCheck/decompile.png)

I found the allocator using the incomplete flag from the strings command. Clicking on it revealed additional characters at different memory addresses.

![incomplete_flag](/img/blog/factCheck/incomplete_flag.png)

I discovered the incomplete flag and other data stored in memory, including the strings "Hello" and "World." After attempting to concatenate these elements to the flag and submitting it, I realized that the flag was likely being dynamically loaded during runtime. 

This led me to debug the code and identify a specific line ending with the character '}' that appeared to be the point where the program completed writing the flag to memory. This insight was crucial in understanding the flag's formation and ultimately solving the challenge.

![incomplete_flag2](/img/blog/factCheck/incomplete_flag2.png)

Assembly view. 0x7d is the ascii value for the ‘}’ character

![assembly_view](/img/blog/factCheck/assembly_view.png)

## Extracting Flag

Assuming RDI holds the memory location, I checked its contents before the CALL to find the missing piece.Then calculating the breakpoint address using relative addressing (main + 0x5D2) to account for runtime address changes.

I used GDB to set a breakpoint at main + 0x5D2 and examined the instructions and RDI contents before and after the CALL.

![flag](/img/blog/factCheck/flag.png)

