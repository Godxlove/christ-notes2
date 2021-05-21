## Introduction to Virtual memory concepts

Virtual Memory is a storage scheme that provides user an illusion of having a very big main memory. This is done by treating a part of secondary memory as the main memory. In this scheme, User can load the bigger size processes than the available main memory by having the illusion that the memory is available to load the process.

Instead of loading one big process in the main memory, the Operating System loads the different parts of more than one process in the main memory. By doing this, the degree of multiprogramming will be increased and therefore, the CPU utilization will also be increased.

**Virtual memory is mostly implemented with demand paging and demand segmentation.**

<br>

### When does the Operating System use Virtual Memory?
- Whenever computer doesn't have space in the physical memory it writes what it needs to remember to the hard disk in a swap file as virtual memory.
- If a computer running Windows needs more memory/RAM, than installed in the system, it uses a small portion of the hard drive for this purpose.

<br>

### Benefits of using the Virtual Memory
Virtual memory also allows the sharing of files and memory by multiple processes, with several benefits:
- System libraries can be shared by mapping them into the virtual address space of more than one process.
- Processes can also share virtual memory by mapping the same block of memory to more than one process.
- Process pages can be shared during a fork( ) system call, eliminating the need to copy all of the pages of the original ( parent ) process.
- More processes should be maintained in the main memory, which increases the effective use of CPU.
- Each page is stored on a disk until it is required after that, it will be removed.
- It allows more applications to be run at the same time.
- There is no specific limit on the degree of multiprogramming.

<br>

### Disadvantages of Virtual Memory

Some cons of using virtual memory:
- Applications may run slower if the system is using virtual memory.
- Likely takes more time to switch between applications.
- Offers lesser hard drive space for your use.
- It reduces system stability.
- It allows larger applications to run in systems that don't offer enough physical RAM alone to run them.
- It doesn't offer the same performance as RAM.

<br>
<br>

## Memory Paging
Memory paging is a memory management scheme by which a computer stores and retrieves data from secondary storage for use in main memory. In this scheme, the operating system retrieves data from secondary storage in same-size blocks called pages.

The main memory is divided into small fixed-size blocks of physical memory, which is called frames. The size of a frame should be kept the same as that of a page to have maximum utilization of the main memory and to avoid external fragmentation. Paging is used for faster access to data, and it is a logical concept.

<br>
<br>

## Demand Paging

![](Pasted%20image%2020210414141302.png)

Demand Paging is a popular method of virtual memory management. In demand paging, the pages of a process which are least used, get stored in the secondary memory.

A page is copied to the main memory when its demand is made or page fault occurs.
So, when a context switch occurs, the OS never copy any of the old program's pages from the disk or any of the new program's pages into the main memory. Instead, it will start executing the new program after loading the first page and fetches the program's pages, which are referenced.

During the program execution, if the program references a page that may not be available in the main memory because it was swapped, then the processor considers it as an invalid memory reference. That's because the page fault and transfers send control back from the program to the OS, which demands to store page back into the memory.

<br>
<br>

## Page Replacement Algorithm

Page replacement algorithms are the techniques using which an Operating System decides which memory pages to swap out, write to disk when a page of memory needs to be allocated. Paging happens whenever a page fault occurs and a free page cannot be used for allocation purpose accounting to reason that pages are not available or the number of free pages is lower than required pages.

When the page that was selected for replacement and was paged out, is referenced again, it has to read in from disk, and this requires for I/O completion. This process determines the quality of the page replacement algorithm: the lesser the time waiting for page-ins, the better is the algorithm.

A page replacement algorithm looks at the limited information about accessing the pages provided by hardware, and tries to select which pages should be replaced to minimize the total number of page misses, while balancing it with the costs of primary storage and processor time of the algorithm itself. There are many different page replacement algorithms. We evaluate an algorithm by running it on a particular string of memory reference and computing the number of page faults.

<br>

There are various page replacement algorithms which are used to determine the pages which will be replaced:
- First In First Out (FIFO) algorithm
- Optimal Algorithm
- LRU Page Replacement
- Page Buffering algorithm
- Least frequently Used(LFU) algorithm
- Most frequently Used(MFU) algorithm

<br>

### Fault rate
Fault rate is a frequency with which a designed system or component fails. It is expressed in failures per unit of time.

<br>
<br>

### First In First Out (FIFO) algorithm

![](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter9/9_12_FIFO_PageReplacement.jpg)

FIFO is a simple implementation method. In this method, memory selects the page for a replacement that has been in the virtual address of the memory for the longest time.

<br>

#### Features:
- Whenever a new page loaded, the page recently comes in the memory is removed. So, it is easy to decide which page requires to be removed as its identification number is always at the FIFO stack.
- The oldest page in the main memory is one that should be selected for replacement first.

![](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter9/9_13_PageFaultCurve.jpg)

<br>
<br>

### Optimal Algorithm

![](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter9/9_14_OptimalPageReplacement.jpg)

The optimal page replacement method selects that page for a replacement for which the time to the next reference is the longest.

<br>

#### Features:

- Optimal algorithm results in the fewest number of page faults. This algorithm is difficult to implement.
- An optimal page-replacement algorithm method has the lowest page-fault rate of all algorithms. This algorithm exists and which should be called MIN or OPT.
- Replace the page which unlike to use for a longer period of time. It only uses the time when a page needs to be used.

<br>
<br>

### Least Recently Used (LRU) Algorithm

![](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter9/9_15_LRU_PageReplacement.jpg)

This method helps OS to find page usage over a short period of time. This algorithm should be implemented by associating a counter with an even- page.

#### Working of LRU Algorithm
- Page, which has not been used for the longest time in the main memory, is the one that will be selected for replacement.
- Easy to implement, keep a list, replace pages by looking back into time.

<br>

#### Features:
- The LRU replacement method has the highest count. This counter is also called aging registers, which specify their age and how much their associated pages should also be referenced.
- The page which hasn't been used for the longest time in the main memory is the one that should be selected for replacement.
- It also keeps a list and replaces pages by looking back into time.

<br>
<br>

### Page Buffering algorithm
- To get a process start quickly, keep a pool of free frames.
- On page fault, select a page to be replaced.
- Write the new page in the frame of free pool, mark the page table and restart the process.
- Now write the dirty page out of disk and place the frame holding replaced page in free pool.

<br>
<br>

### Least frequently Used(LFU) algorithm
- The page with the smallest count is the one which will be selected for replacement. 
- This algorithm suffers from the situation in which a page is used heavily during the initial phase of a process, but then is never used again.

<br>
<br>

### Most frequently Used(MFU) algorithm
- This algorithm is based on the argument that the page with the smallest count was probably just brought in and has yet to be used.


<br>
<br>

### Disadvantages of using Demand Paging
- May cause Internal fragmentation
- Complex memory management algorithm
- Page tables consume additonal memory.
- Multi-level paging may lead to memory reference overhead.
- Too much reliance on memory paging can **impair performance**, because random access memory operates much faster than disk memory. This means the operating system has to wait for the disk to catch up every time a page is swapped; the more a workload relies on swap files, the more it will negatively impact performance.

<br>
<br>

## Segmentation
Segmentation method works almost similarly to paging, only difference between the two is that segments are of variable-length whereas, in the paging method, pages are always of fixed size.

A program segment includes the program's main function, data structures, utility functions, etc. The OS maintains a segment map table for all the processes. It also includes a list of free memory blocks along with its size, segment numbers, and its memory locations in the main memory or virtual memory.

<br>

### Advantages of a Segmentation method
The benefits of segmentation include:
- Offer protection within the segments
- You can achieve sharing by segments referencing multiple processes.
- Not offers internal fragmentation
- Segment tables use lesser memory than paging

<br>

### Disadvantages of Segmentation
Some drawback of segmentation:
- In segmentation method, processes are loaded/ removed from the main memory. Therefore, the free memory space is separated into small pieces which may create a problem of external fragmentation
- Costly memory management algorithm

<br>
<br>

# Mobile Operating Systems

### Introduction
A mobile operating system is an operating system for mobile phones, tablets, smartwatches, 2-in-1 PCs, smart speakers, or other mobile devices. While computers such as typical laptops are 'mobile', the operating systems used on them are generally not considered mobile ones, as they were originally designed for desktop computers that historically did not have or need specific mobile features. But for some time now, smartphones have used operating systems too and it's this development that has brought advanced functions to mobiles that were previously only available on our computers.

<br>

![Mobile Phone Operating Systems](https://1.bp.blogspot.com/-AHdpm3ZyR0M/UXE3wUFlgfI/AAAAAAAADI4/nXfU1UL9Myo/s1600/mobile+phone+os.jpeg)

This distinction is becoming blurred in some newer operating systems that are hybrids made for both uses. Mobile operating systems combine features of a personal computer operating system with other features useful for mobile or handheld use, and usually including a wireless inbuilt modem and SIM tray for telephony and data connection. 

Mobile devices, with mobile communications abilities (e.g., smartphones), contain two mobile operating systems – the main user-facing software platform is supplemented by a second low-level proprietary real-time operating system which operates the radio and other hardware.


<br>
<br>

## Features of mobile operating system

**An excellent intuitive UI **
- A good smartphone OS should boot quickly and allow for a quick and beautiful UI that is both fully functional and yet not overwhelming to the users.

<br>

**App Store / App Ecosystem** 
- This is probably the most important success reasons for a Mobile OS. Android, though was not very simple to operate has a great App Market as well as great developer ecosystem and that is the reason for its success.
- Smartphones are nothing without good and functional apps, and an app store is where you get the apps, but the prospect of getting quick cash drives some developers to make irrelevant apps and so a good and curated app store is vital for the smartphone to function as intended.

<br>

**Battery Management** 
- As smartphones include more sensors and processor cores and gpu, in general more processing power, the amount of power required by the smartphone keeps on ever increasing, so smartphones need to have a good battery management which can help battery to last through the day, with moderate to high usage.
- Graphene batteries may help with that in the future, but currently only a few phones last through an entire day of average use.
- This is in part a fault of the processor and wireless radio management systems that are used in the operating system which are not ‘smart’ enough to turn of the radio when not in use for an extended period of time.

<br>

**Stable Performance on Various Devices**
- Users of this operating system may experience performance issues on weaker mobile devices

<br>
<br>

## Comparison between different mobile operating systems

![](Pasted%20image%2020210414144033.png)
![](Pasted%20image%2020210414144304.png)


<br>
<br>

## Examples of different mobile operating systems

1. Android OS: The Android operating system is the most popular operating system today. It is a mobile OS based on the Linux Kernel and open-source software. The android operating system was developed by Google. The first Android device was launched in 2008.
2. Bada (Samsung Electronics): Bada is a Samsung mobile operating system that was launched in 2010. The Samsung wave was the first mobile to use the bada operating system. The bada operating system offers many mobile features, such as 3-D graphics, application installation, and multipoint-touch.
3. BlackBerry OS: The BlackBerry operating system is a mobile operating system developed by Research In Motion (RIM). This operating system was designed specifically for BlackBerry handheld devices. This operating system is beneficial for the corporate users because it provides synchronization with Microsoft Exchange, Novell GroupWise email, Lotus Domino, and other business software when used with the BlackBerry Enterprise Server.
4. iPhone OS / iOS: The iOS was developed by the Apple inc for the use on its device. The iOS operating system is the most popular operating system today. It is a very secure operating system. The iOS operating system is not available for any other mobiles.
5. Symbian OS: Symbian operating system is a mobile operating system that provides a high-level of integration with communication. The Symbian operating system is based on the java language. It combines middleware of wireless communications and personal information management (PIM) functionality. The Symbian operating system was developed by Symbian Ltd in 1998 for the use of mobile phones. Nokia was the first company to release Symbian OS on its mobile phone at that time.
6. Windows Mobile OS: The window mobile OS is a mobile operating system that was developed by Microsoft. It was designed for the pocket PCs and smart mobiles.
7. Harmony OS: The harmony operating system is the latest mobile operating system that was developed by Huawei for the use of its devices. It is designed primarily for IoT devices.
8. Palm OS: The palm operating system is a mobile operating system that was developed by Palm Ltd for use on personal digital assistants (PADs). It was introduced in 1996. Palm OS is also known as the Garnet OS.
9. WebOS (Palm/HP): The WebOS is a mobile operating system that was developed by Palm. It based on the Linux Kernel. The HP uses this operating system in its mobile and touchpads.