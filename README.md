# XV Quiz (CSL 3030)

Welcome to the XV Quiz for CSL 3030 - Operating Systems!



## Instructions
- Answer the multiple-choice questions by selecting the correct option.
- For theoretical questions, provide concise and accurate explanations.
- Feel free to use this quiz for self-assessment or educational purposes.

## Multiple-Choice Questions

#### Question 1: Basics
1. What is XV6?
   - a. A programming language
   - b. A Unix-like operating system
   - c. A file system
   - d. An assembly language

#### Question 2: Architecture
2. XV6 is based on which earlier operating system?
   - a. Windows
   - b. Linux
   - c. BSD
   - d. DOS

#### Question 3: File System
3. Which file system is used in XV6?
   - a. FAT32
   - b. NTFS
   - c. ext4
   - d. simple

#### Question 4: System Calls
4. How are system calls implemented in XV6?
   - a. As functions in the C standard library
   - b. As interrupts
   - c. Through the command line
   - d. As external programs

#### Question 5: Processes
5. In XV6, what is the maximum number of processes that can run simultaneously?
   - a. 128
   - b. 256
   - c. 512
   - d. 1024

#### Question 6: Shell
6. What is the name of the shell used in XV6?
   - a. Bash
   - b. Zsh
   - c. Sh
   - d. Fish

#### Question 7: Scheduling
7. How does XV6 handle process scheduling?
   - a. Round-robin scheduling
   - b. Priority-based scheduling
   - c. First-Come-First-Serve (FCFS)
   - d. Random scheduling

#### Question 8: Memory Management
8. Which memory management technique is used in XV6?
   - a. Paging
   - b. Segmentation
   - c. Virtual Memory
   - d. None of the above

#### Question 9: Interrupts
9. How are interrupts handled in XV6?
   - a. Through polling
   - b. Using hardware interrupts
   - c. Using software interrupts
   - d. Both b and c

#### Question 10: Multithreading
10. Does XV6 support multithreading?
    - a. Yes
    - b. No

#### Bonus Question:
11. Who developed XV6?
    - a. Microsoft
    - b. Google
    - c. MIT
    - d. IBM

## Theoretical Questions

#### Question 12: Process States
12. Briefly explain the different states a process can be in within the XV6 operating system.

#### Question 13: File System Structure
13. Describe the structure of the file system in XV6. Include the key components and their roles.

#### Question 14: System Calls vs. Library Functions
14. Explain the difference between system calls and library functions in the context of XV6. Provide examples of each.

#### Question 15: Memory Paging
15. How does memory paging work in XV6? Discuss the benefits of using paging in memory management.

#### Question 16: Shell Commands
16. Name and briefly explain three essential shell commands in the XV6 operating system.

#### Question 17: Process Synchronization
17. Discuss the concept of process synchronization in XV6. Why is it essential, and what mechanisms are used to achieve it?

#### Question 18: Interrupt Handling
18. Explain the role of interrupts in the XV6 operating system. How are interrupts handled, and what is their significance in system operation?

#### Question 19: Virtual Memory
19. What is virtual memory, and how is it implemented in XV6? Discuss the advantages of using virtual memory.

#### Question 20: Boot Process
20. Outline the steps involved in the boot process of XV6. What happens from the moment the computer is powered on to when the XV6 kernel is loaded into memory?

## Answers
1) b
2) b
3) d
4) a
5) 64
6) c
7) a
8) a
9) d
10) b
11) c

12) The different states a process can be in within the XV6 operating system are:
1. Running: The process is currently being executed by the CPU.
2. Sleeping: The process is waiting for some event to occur, such as the completion of an I/O operation.
3. Runnable: The process is ready to run but is waiting for the CPU to become available.
4. Zombie: The process has completed execution, but its parent has not yet called wait() to collect its exit status.
5. Unused: The process table entry is not currently being used.

Xv6 uses a process scheduler to manage the state of each process and determine which process should be executed next. The scheduler uses a round-robin algorithm to time-share the CPU among the set of processes waiting to execute.

13) The file system structure in XV6 is organized into seven layers. The seven layers are:

1. The disk layer: This layer reads and writes blocks on a virtio hard drive.
2. The buffer cache layer: This layer caches disk blocks and synchronizes access to them, ensuring that only one kernel process at a time can modify the data stored in any particular block.
3. The logging layer: This layer allows higher layers to wrap updates to several blocks in a transaction and ensures that the blocks are updated atomically in the face of crashes.
4. The inode layer: This layer provides individual files, each of which has an inode that describes the file's metadata, such as its size, ownership, and permissions.
5. The directory layer: This layer provides a hierarchical namespace for files and directories and maps pathnames to inodes.
6. The name layer: This layer provides a way to look up inodes by name and caches recently used names to speed up future lookups.
7. The user layer: This layer provides a set of system calls that allow user programs to interact with the file system.
<centre>![image](https://github.com/anushkaa-ambuj/B21ES006_xv6-quiz/assets/92167974/dc508428-8af5-446d-8bb6-bba479d4fa91)</centre>

The file system uses on-disk data structures to represent the tree of named directories and files, to record the identities of the blocks that hold each file's content, and to record which areas of the disk are free. The file system must support crash recovery, and different processes may operate on the file system at the same time, so the file-system code must coordinate to maintain invariants. Accessing a disk is orders of magnitude slower than accessing memory, so the file system must maintain an in-memory cache of popular blocks.

14) The differences between system calls and library functions in the context of XV6 are as follows:

The system calls are the interface between user-level applications and the kernel. They provide a way for user-level applications to request services from the kernel, such as creating a new process or reading from a file. System calls are implemented in the kernel and are accessed through a software interrupt.

On the other hand, library functions are functions that are provided by libraries that are linked to user-level applications. They are not part of the kernel and are not accessed through a software interrupt. Instead, they are called like any other function in the application.

Examples of system calls in XV6 include fork(), exec(), and open(). These system calls allow user-level applications to create new processes, execute programs, and open files respectively. 
Examples of library functions in XV6 include printf() and scanf(), which are part of the C standard library and are used for input and output.

In summary, system calls provide a way for user-level applications to interact with the kernel, while library functions provide a way for user-level applications to reuse code that is provided by libraries.

15) Paging is a technique the operating system uses to manage memory. In XV6, the RISC-V hardware provides page tables that map virtual addresses used by user-level applications to physical addresses used by the hardware. The page tables allow the operating system to isolate different processes' address spaces and multiplex them onto a single physical memory. The page tables provide a level of indirection that allows the operating system to perform many tasks, such as mapping the same memory in several address spaces and guarding kernel and user stacks with an unmapped page.

The page tables in XV6 are organized into three levels: page global directory (PGD), page upper directory (PUD), and page table (PT). The PGD is the top-level page table, and it contains pointers to PUDs. The PUDs, in turn, contain pointers to PTs. The PTs contain the actual page table entries (PTEs) that map virtual addresses to physical addresses.

The benefits of using paging in memory management include:

1. Memory protection: Paging allows the operating system to protect memory from unauthorized access. Each process has its own address space, and the page tables ensure that a process can only access its own memory.

2. Virtual memory: Paging allows the operating system to provide virtual memory to user-level applications. Virtual memory allows applications to use more memory than is physically available by swapping pages of memory to disk when they are not in use.

3. Memory sharing: Paging allows the operating system to share memory between processes. By mapping the same physical memory to different virtual addresses in different processes' address spaces, the operating system can allow processes to share memory without the need for copying.

16) Three examples of shell commands are:

1. ls: This command lists the contents of a directory. When used without any arguments, it lists the contents of the current directory. For example, "ls" will list the files and directories in the current directory.
2. cd: This command changes the current working directory. For example, "cd /usr" changes the current directory to /usr.
3. cat: This command concatenates and displays the contents of files. For example, "cat file1 file2" will display the contents of file1 followed by the contents of file2.

