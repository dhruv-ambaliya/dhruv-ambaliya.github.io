---
layout: blog_item
title:  "vault-door-training CTF - Walkthrough"
date:   2024-07-22 11:00:60
author: Dhruv Ambaliya
description: 'picoCTF2019 vault-door-training - Walkthrough Guide'
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

Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility. 

**Download:** [VaultDoorTraining.java](https://jupiter.challenges.picoctf.org/static/03c960ddcc761e6f7d1722d8e6212db3/VaultDoorTraining.java)


## Enumeration

![vault-door-training_des](/img/blog/vault-door-training/vault-door-training_des.png)

## Extracting Flag

Upon examining the provided Java file using the JD-GUI decompiler, we were able to uncover the concealed flag. The flag, likely intended to be hidden or protected, was directly embedded within the source code itself. 

![flag](/img/blog/vault-door-training/flag.png)

