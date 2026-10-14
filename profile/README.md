# Umineco
This is a development community for software designed with an emphasis on safety, functionality, and efficiency.

## uKernel
uKernel is a unique kernel implementation.

For example, it features a unique function called "altcall". Altcall is a mechanism that delegates the interpretation and processing of a process's system calls to an altcall handler specified at the time the process is launched.
This is extremely useful. For instance, by creating an altcall handler that behaves like an existing OS, you can easily run software for that OS simply by specifying that handler when launching the process. Furthermore, by applying this feature, it should be possible to easily build mechanisms such as sandboxes.

There is also a feature called "uLimit". uLimit is designed to highly customize and restrict user and process privileges.
In essence, it functions as a system call firewall.
It processes only operations explicitly permitted for both users and processes, and immediately rejects them if they are not permitted.[^3]
This reliably blocks unwanted processing.

The fact that it is a microkernel is also an unusual feature.
A microkernel runs kernel functions as multiple processes executed in user space.
Because of this, even if a vulnerability exists in a specific function, the problem rarely spreads to the entire kernel. Basically, the impact is strictly limited to a very narrow scope related to that function.
This makes it easier to ensure safety.

It is *NIX-like, providing an experience similar to Linux for users of common distributions.
However, you can use altcall to run Windows faster and more comfortably (than with tools like Wine).
Additionally, developers can use ukmod[^1] for handling processes such as HTTP, TLS, and geolocation, allowing them to use advanced protocols and features without additional libraries like OpenSSL.

> As an aside, the prefix "u" in terms like uKernel and uLimit derives from "Umineco". It is also a pun on the word micro (μ) kernel.
> The pronunciation of this prefix can be either "you" or "micro", but since uKernel and microkernel would be pronounced the same and cause confusion, it is usually recommended to be pronounced as "you". (It is pronounced "you", not "uu")
> Note that uKernel distributions are also referred to as Umineco distributions.

[^1]: A ukmod (userland kernel module) is a kernel module executed in user space. The bare uKernel contains only the most basic functions such as loading ukmods, a syscall router, and functions to parse and execute ELF binaries, and is designed so that functions such as USB, PCI-E, and TCP/IP are all added via ukmods. Drivers are also distributed as ukmods, functioning by registering themselves with an abstract driver[^2].
[^2]: An abstract driver is a ukmod for API abstraction. For example, if the APIs of USB controllers from Company A and Company B differ, without something to abstract and unify them, software using USB would need to support each API. In most operating systems, including uKernel, the kernel or kernel modules provide easy-to-use APIs and solve this by converting them into each API format. In uKernel, ukmods that provide a common API are called **abstract drivers**. By distributing ukmods that act as backends for abstract drivers, companies can easily support uKernel, and software developers and users can handle hardware such as USB and Bluetooth without worrying about individual company APIs.
[^3]: By default, uKernel grants no privileges whatsoever. In other words, a process cannot display a window, check the time, or display text. Instead, the desktop environment or the like grants a minimal set of default privileges when starting a process. If you need to interactively allow features such as notifications or a camera (i.e., displaying something like "Allow notifications?" as on a smartphone), you can implement this by allowing the process to "request privileges" and having the desktop environment display a pop-up when the process requests privileges.

## About NecOS
NecOS is the official uKernel distribution of Umineco.

It maximizes the characteristics of uKernel to provide a practical and comfortable environment.

## About FiRSTBOOT
FiRSTBOOT is a bootloader implementation for uKernel.
