---
layout: blog_item
title:  "vault-door-1 CTF - Walkthrough"
date:   2024-07-23 11:00:60
author: Dhruv Ambaliya
description: 'picoCTF2019 vault-door-1 - Walkthrough Guide'
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
               <p><i class="fa fa-coffee">Easy</i></p>
           </td>
        </tr>
      </tbody>
</table>
</div>

* list element with functor item
{:toc}

## Description

This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: 

**Download:** [VaultDoor1.java](https://jupiter.challenges.picoctf.org/static/87e103a8db01087de9ccf5a7a022ddf8/VaultDoor1.java)


## Enumeration

We encountered another Java file that claimed to hide the flag in a more complex manner. 

![vault-door-1](/img/blog/vault-door-1/vault-door-1_des.png)

Upon inspecting the Java file using JD-GUI, a popular decompiler, we discovered a clever obfuscation technique. Each element within an array held a single character, and when these characters were sequentially concatenated, the hidden flag was revealed right before our eyes.

![java_file](/img/blog/vault-door-1/java_file.png)

## Extracting Flag

Below a python script that solve the challenge. 

{% highlight bash %}

myPass = [None] * 32

myPass[0]  = 'd'
myPass[29] = 'f'
myPass[4]  = 'r'
myPass[2]  = '5'
myPass[23] = 'r'
myPass[3]  = 'c'
myPass[17] = '4'
myPass[1]  = '3'
myPass[7]  = 'b'
myPass[10] = '_'
myPass[5]  = '4'
myPass[9]  = '3'
myPass[11] = 't'
myPass[15] = 'c'
myPass[8]  = 'l'
myPass[12] = 'H'
myPass[20] = 'c'
myPass[14] = '_'
myPass[6]  = 'm'
myPass[24] = '5'
myPass[18] = 'r'
myPass[13] = '3'
myPass[19] = '4'
myPass[21] = 'T'
myPass[16] = 'H'
myPass[27] = '3'
myPass[30] = '3'
myPass[25] = '_'
myPass[22] = '3'
myPass[28] = 'e'
myPass[26] = '6'
myPass[31] = 'a'

print("" + ''.join(myPass))

{% endhighlight %}

