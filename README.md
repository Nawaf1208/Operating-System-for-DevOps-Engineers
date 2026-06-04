# Operating-System-for-DevOps-Engineers

![](OS.png)

## Self Assessment

<details>
<summary><b><i>1.What is an operating system?</i></b></summary>

$\color{green}{\text{Answer}}$

- It is responsible for making it easy to run programs (even allowing you to seemingly run many at the same time), allowing programs to share memory, enabling programs to interact with devices, and other fun stuff like that.

</details>

## Process

<details>
<summary><b><i>2.Can you explain what is a process?</i></b></summary>

$\color{green}{\text{Answer}}$

- A process is a running program. A program is one or more instructions and the program (or process) is executed by the operating system.

</details>

<details>
<summary><b><i>3.If you had to design an API for processes in an operating system, what would this API look like?</i></b></summary>

$\color{green}{\text{Answer}}$

- It would support the following:
  - Create -> allow to create new processes
  - Delete -> allow to remove/destroy processes
  - State -> allow to check the state of the process, whether it's running, stopped, waiting, etc.
  - Stop -> allow to stop a running proce

</details>

<details>
<summary><b><i>4.How a process is created?</i></b></summary>

$\color{green}{\text{Answer}}$

- The OS is reading program's code and any additional relevant data

- Program's code is loaded into the memory or more specifically, into the address space of the process.

- Memory is allocated for program's stack (aka run-time stack). The stack also initialized by the OS with data like argv, argc and parameters to main()

- Memory is allocated for program's heap which is required for dynamically allocated data like the data structures linked lists and hash tables

- I/O initialization tasks are performed, like in Unix/Linux based systems, where each process has 3 file descriptors (input, output and error)

- OS is running the program, starting from main()

</details>

<details>
<summary><b><i>5.True or False? The loading of the program into the memory is done eagerly (all at once)</i></b></summary>

$\color{green}{\text{Answer}}$

- False. It was true in the past but today's operating systems perform lazy loading, which means only the relevant pieces required for the process to run are loaded first.

</details>

<details>
<summary><b><i>6.What are different states of a process?</i></b></summary>

$\color{green}{\text{Answer}}$

- Running - it's executing instructions
- Ready - it's ready to run, but for different reasons it's on hold
- Blocked - it's waiting for some operation to complete, for example I/O disk request

</details>

<details>
<summary><b><i>7.What are some reasons for a process to become blocked?</i></b></summary>

$\color{green}{\text{Answer}}$

- I/O operations (e.g. Reading from a disk)
- Waiting for a packet from a network

</details>

<details>
<summary><b><i>8.What is Inter Process Communication (IPC)?</i></b></summary>

$\color{green}{\text{Answer}}$

- Inter-process communication (IPC) refers to the mechanisms provided by an operating system that allow processes to manage shared data.

</details>

<details>
<summary><b><i>9.What is "time sharing"?</i></b></summary>

$\color{green}{\text{Answer}}$

- Even when using a system with one physical CPU, it's possible to allow multiple users to work on it and run programs. This is possible with time sharing, where computing resources are shared in a way it seems to the user, the system has multiple CPUs, but in fact it's simply one CPU shared by applying multiprogramming and multi-tasking.

</details>

<details>
<summary><b><i>10.What is "space sharing"?</i></b></summary>

$\color{green}{\text{Answer}}$

- Somewhat the opposite of time sharing. While in time sharing a resource is used for a while by one entity and then the same resource can be used by another resource, in space sharing the space is shared by multiple entities but in a way where it's not being transferred between them.

- It's used by one entity, until this entity decides to get rid of it. Take for example storage. In storage, a file is yours, until you decide to delete it.

</details>

<details>
<summary><b><i>11.What component determines which process runs at a given moment in time?</i></b></summary>

$\color{green}{\text{Answer}}$

- CPU schedule

</details>

## Memory

<details>
<summary><b><i>12.What is "virtual memory" and what purpose does serve?</i></b></summary>

$\color{green}{\text{Answer}}$

- Virtual memory combines your computer's RAM with temporary space on your hard disk. When RAM runs low, virtual memory helps to move data from RAM to a space called a paging file. Moving data to paging file can free up the RAM, so your computer can complete its work. In general, the more RAM your computer has, the faster the programs run.

</details>

<details>
<summary><b><i>13.What is demand paging?</i></b></summary>

$\color{green}{\text{Answer}}$

- Demand paging is a memory management technique where pages are loaded into physical memory only when accessed by a process. It optimizes memory usage by loading pages on demand, reducing startup latency and space overhead. However, it introduces some latency when accessing pages for the first time. Overall, it’s a cost-effective approach for managing memory resources in operating systems.

</details>

<details>
<summary><b><i>14.What is copy-on-write?</i></b></summary>

$\color{green}{\text{Answer}}$

- Copy-on-write (COW) is a resource management concept, with the goal to reduce unnecessary copying of information. It is a concept, which is implemented for instance within the POSIX fork syscall, which creates a duplicate process of the calling process.

- The idea:
- 1.If resources are shared between 2 or more entities (for example shared memory segments between 2 processes), the resources don't need to be copied for every entity, but rather every entity has a READ operation access permission on the shared resource. (the shared segments are marked as read-only) (Think of every entity having a pointer to the location of the shared resource, which can be dereferenced to read its value)

- 2.If one entity would perform a WRITE operation on a shared resource, a problem would arise, since the resource also would be permanently changed for ALL other entities sharing it. (Think of a process modifying some variables on the stack, or allocatingy some data dynamically on the heap, these changes to the shared resource would also apply for ALL other processes, this is definitely an undesirable behaviour)

- 3.As a solution only, if a WRITE operation is about to be performed on a shared resource, this resource gets COPIED first and then the changes are applied.

</details>

<details>
<summary><b><i>15.What is a kernel, and what does it do?</i></b></summary>

$\color{green}{\text{Answer}}$

- The kernel is part of the operating system and is responsible for tasks like:
  - Allocating memory
  - Schedule processes
  - Control CPU

</details>

<details>
<summary><b><i>16.True or False? Some pieces of the code in the kernel are loaded into protected areas of the memory so applications can't overwrite them.</i></b></summary>

$\color{green}{\text{Answer}}$

- True

</details>

<details>
<summary><b><i>17.What is POSIX?</i></b></summary>

$\color{green}{\text{Answer}}$

- POSIX (Portable Operating System Interface) is a set of standards that define the interface between a Unix-like operating system and application programs.

</details>

<details>
<summary><b><i>18.Explain what is Semaphore and what its role in operating systems.</i></b></summary>

$\color{green}{\text{Answer}}$

- A semaphore is a synchronization primitive used in operating systems and concurrent programming to control access to shared resources. It's a variable or abstract data type that acts as a counter or a signaling mechanism for managing access to resources by multiple processes or threads.

</details>

<details>
<summary><b><i>19.What is cache? What is buffer?</i></b></summary>

$\color{green}{\text{Answer}}$

- Cache: Cache is usually used when processes are reading and writing to the disk to make the process faster, by making similar data used by different programs easily accessible. Buffer: Reserved place in RAM, which is used to hold data for temporary purposes.

</details>
