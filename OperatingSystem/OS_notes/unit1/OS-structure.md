# OS structure

• General-purpose OS is very large program
• Various ways to group them
- Simple structure – MS-DOS
- More complex - UNIX
- Layered – an abstraction
- Microkernel -Mach

---

## MS -DOS - simple structure
is written to provide the most functionality in the least space
- Not divided into modules
- Although MS-DOS has

some structure, its interfaces and levels of functionality are not well separated

![](ms-dos.png)

---

## Unix - monolithic structure (non simple struct)
UNIX – limited by hardware functionality, the original UNIX operating system had limited structuring. The UNIX OS consists of two separable parts
- Systems programs
- The kernel

Consists of everything below the system-call interface and above the physical hardware.

Provides the file system, CPU scheduling, memory management, and other operating-system functions; a large number of functions for one level

![](unix-structure.png)

---

# layered approach

The operating system is divided into a number of layers (levels), each built on top of lower layers. The bottom layer (layer 0), is the hardware; the highest (layer N) is the user interface. 
With modularity, layers are selected such that each uses functions (operations) and services of only lower-level layers.

![](layered-approach.png)

---

## Microkernel System Structure
Moves as much from the kernel into user space
• Mach example of microkernel - Mac OS X kernel (Darwin) partly based on Mach
• Communication takes place between user modules using message passing

<br>

• Benefits:
- Easier to extend a microkernel
- Easier to port the operating system to new architectures
- More reliable (less code is running in kernel mode)
- More secure

<br>

• disadvantage - Performance overhead of user space to kernel space
communication

![](microkernel-structure.png)

---

# modules (modular approach)
Many modern operating systems implement loadable kernel modules
- Uses object-oriented approach
- Each core component is separate
- Each talks to the others over known interfaces
- Each is loadable as needed within the kernel

Overall, similar to layers but with more flexible -> Linux, Solaris, etc

![](solaris-modular-approach.png)

