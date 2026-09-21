# Umineko
A development community for a next-generation operating system designed with an emphasis on safety, functionality, and efficiency.

## Overview
Umineko is a community that develops the fully open-source microkernel implementation "uKernel", its official distribution "NekOS", and the bootloader implementation "FiRSTBOOT" for booting uKernel.

## About uKernel
uKernel is a uNique kernel implementation.

For instance, it features a proprietary function called altcall. altcall is a mechanism that "delegates the interpretation and processing of a syscall from a process to the altcall handler specified at the time the process is launched."
This is extremely convenient; for example, by creating an altcall handler that behaves like an existing OS, you can easily run software for that OS simply by specifying that handler when launching the process. Furthermore, applying this feature should allow you to easily build sandbox-like mechanisms as well.

There is also a feature called uLimit. uLimit is a function designed to highly customize and restrict user and process privileges.
In short, it functions as a firewall for syscalls.
It processes only operations explicitly permitted for both users and processes, and immediately rejects them if they are not permitted.
This ensures the reliable blocking of unwanted processing.

The fact that it is a microkernel is also rare.
A microkernel executes kernel functions as several processes running in user space.
Because of this, even if a vulnerability exists in a specific function, the problem is unlikely to spread to the entire kernel. Basically, the impact should be limited strictly to the very narrow area involving that function.
This makes it easier to ensure safety.

> As an aside, the "u" prefix in uKernel, uLimit, and other terms comes from "U"mineko. It is also a play on the word micro (μ) kernel.
> You can pronounce this prefix as either "uu" or "micro", but since uKernel and microkernel would be pronounced the same way and cause confusion, it is generally recommended to pronounce it as "uu".
> Additionally, uKernel distributions are also referred to as Umineko distributions.

## About NekOS
NekOS is an operating system based on uKernel.

It maximizes the characteristics of uKernel to deliver a practical and comfortable environment.

## About FiRSTBOOT
FiRSTBOOT is a bootloader implementation for uKernel.
