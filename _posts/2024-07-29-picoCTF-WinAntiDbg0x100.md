---
layout: blog_item
title:  "WinAntiDbg0x100 CTF - Walkthrough"
date:   2024-07-29 11:00:60
author: Dhruv Ambaliya
description: 'picoCTF2024 WinAntiDbg0x100 - Walkthrough Guide'
categories: [walkthroughs]
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

This challenge will introduce you to 'Anti-Debugging.' Malware developers don't like it when you attempt to debug their executable files because debugging these files reveals many of their secrets! That's why, they include a lot of code logic specifically designed to interfere with your debugging process.

**Download:** [Binary](https://artifacts.picoctf.net/c_titan/85/WinAntiDbg0x100.zip)


## Enumeration

![WinAntiDbg0x100_des](/img/blog/WinAntiDbg0x100/WinAntiDbg0x100_des.webp)

From the challenge name and description we know that we will use a debugger on this challenge, But lets first run it and see what’ll happen.

![exec](/img/blog/WinAntiDbg0x100/exec.jpg)

ok, now lets open it using x32dbg

## Open it in Debugger

![x32dbg](/img/blog/WinAntiDbg0x100/x32dbg.webp)

After we reach the EntryPoint lets search for strings in all user modules

![x32dbg2](/img/blog/WinAntiDbg0x100/x32dbg2.webp)

Lets jump to the string that looks like the “picoCTF” drawing and set a break point there

![x32dbg3](/img/blog/WinAntiDbg0x100/x32dbg3.webp)

## Extracting Flag

We see that after some instruction there is a call for **isDebuggerPresent** function, lets step until it and see how can we bypass this check

![x32dbg4](/img/blog/WinAntiDbg0x100/x32dbg4.webp)

We see that the function returned 1 and the jump won’t be taken because the ZeroFlag wasn’t set to 1, so we can easily bypass this by setting the ZeroFlag to 1 so we can take the jump.

![x32dbg5](/img/blog/WinAntiDbg0x100/x32dbg5.webp)

after some steps we see that the flag got decrypted and it’s visible to us.

