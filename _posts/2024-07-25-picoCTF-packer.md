---
layout: blog_item
title:  "packer CTF - Walkthrough"
date:   2024-07-25 11:00:60
author: Dhruv Ambaliya
description: 'picoCTF2024 packer - Walkthrough Guide'
categories: [walkthroughs]
tags:
- CTF
- reverse-engineering
---


<div class="rating">
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

In this challenge, you would be asked to reverse a linux executable. They provided a file
named “out”. It definitely seemed like an ELF executable, which is the main executable format for Linux binaries (Windows uses another
format, named PE).

**Download:** [Binary](https://artifacts.picoctf.net/c_titan/101/out)


## Enumeration

![packer](/img/blog/packer/packer_des.webp)
We see one ELF File and It’s packed using UPX

## Unpack the file

![unpack](/img/blog/packer/unpack.webp)

Opening it in IDA and looking at main, it’s a Straightforward challenge we see the flag is hard coded in Hex.

![ida1](/img/blog/packer/ida1.webp)

![ida2](/img/blog/packer/ida2.webp)

