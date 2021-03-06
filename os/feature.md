# 操作系统的基本特征
操作系统具有并发、共享、虚拟和异步这四个基本特征，其中，并发特征是操作系统最重要的特征，其他特征都是以并发特征为前提的。

## 并发性
与并发相似的概念是并行。并发和并行既有相似又有区别。并行性是指两个或多个事件在同一时刻发生，事件程序运行相互独立。并发性是指在一段时间内,用户的角度看有多个程序在同时运行，但其实本质上是多个程序在分时的交替执行。

程序并发执行的方式：
- 进程：为使多个程序能并发执行，系统必须分别为每个程序建立进程(Process)。简单说来，进程是指在系统中能独立运行并作为资源分配的基本单位
- 线程：通常一个进程中可以拥有多个线程，在引入线程的OS中，通常把线程作为独立运行和调度的基本单位。

## 共享性
所谓共享性，是指系统中的资源可供内存中多个并发执行的进程（线程）共同使用。也叫资源共享。

实现资源共享的方式：

1. 互斥共享：当 A 进程访问完成并释放该资源后，才允许 B 进程来对该资源进行访问。而把在一段时间内只运行一个进程访问的资源称为临界资源或独占资源。
2. 同时访问：还有一类资源，它允许在一段时间内由多个进程同时对它们进行访问。

## 虚拟技术
操作系统中的所谓的虚拟指的是通过某种技术把一个物理实体变为若干个逻辑上的对应物。在操作系统中利用两种技术实现了虚拟技术，即时分复用技术和空分复用技术。

- 时分复用技术：在虚拟处理机技术中，利用多道程序设计技术，为每道程序建立一个进程，让多道程序并发地执行，以此来分时使用一台处理机。还可以通过虚拟设备技术，将一台物理机 I/O 设备虚拟为多台逻辑上的 I/O 设备，并允许每个用户占用一台逻辑上的 I/O 设备。
- 空分复用技术：虚拟磁盘技术，将一台硬盘虚拟称多台虚拟磁盘。虚拟存储器技术, 利用存储器的空闲空间来存放其他的程序，以提高内存的利用率。

## 异步性
内存中的每个进程在何时能获得处理机运行，何时又因提出某种资源请求而暂停，以及进程以怎样的速度向前推进，没到程序需要多长时间来完成等，这些都是不可预知的。进程是以人们不可预知的速度向前推进，此即进程的异步性。

# 操作系统的主要功能

操作系统的主要任务，是为多道程序的运行提供良好的运行环境，以保证多道程序能有条不紊地高效的运行，并能最大程度地提高系统中各种资源的利用率和方便用户的使用。
操作系统应该具备这样几方面的功能：处理机管理、存储器管理、设备管理和文件管理。

## 处理机管理功能

在传统的多道程序系统中，处理机的分配和运行的基本单位是进程。因而对处理机管理可以归结为进程的管理。在引入线程的 OS 中，也包含对线程的管理。

处理机主要管理的功能是: 
- 创建和撤销进程（线程）
- 对进程（线程）的运行进行协调
- 实现进程（线程）间的信息交换
- 按照一定的算法把处理机分配给进程（线程）

1. 进程控制：主要功能是为作业创建进程，撤销以结束的进程，以及控制进程在运行过程中的状态转换。在引入线程的 OS 中，还应该具备为一个进程创建若干个线程和撤销（终止）以完成任务的线程的功能。
2. 进程同步：进程是以异步方式运行的。为了使多个进程有条不紊的运行，必须设置进程同步机制，进程同步的主要任务就是为多个进程（线程）的运行进行协调。
进程协调的方式有：进程互斥方式和进程同步方式。而进程互斥的机制实现方式有：锁机制，信号量机制
3. 进程间通信：进程间通信主要任务是实现在相互合作的进程间的信息交换。通常采用消息队列的方式来实现进程间通信。
4. 调度：需要执行的每个作业都需要经过调度才能执行。调度包括：作业调度和进程调度。作业调度就是按照一定的算法，选择出若干个作业，为他们分配运行所需要的资源。进程调度是指按照一定的算法选出一个进程，把处理机分配给他们。并为它设置运行现场，使进程投入运行。

## 存储器管理功能
存储器管理的主要任务是为多道程序的运行提供良好的环境，方便用户使用存储器，提高用户的存储器的利用率以及能从逻辑上扩充内存。存储器具有的功能如下：

### 1. 内存分配  
- 为每道程序分配内存空间，使它们各得其所
- 提高存储器的利用率，以减少不可用的内存空间
- 允许正在允许的程序申请附件的内存

分配内存的两种方式：

- 静态分配：每个作业的内存空间是在装入作业的时候确定的，作业运行期间，不允许再申请新的内存空间，也不允许作业在内存中“移动”
- 动态分配：每个作业所要求的基本的内存空间是在装入时确定的，但允许作业在运行时申请新的附加的内存。也允许作业在内存中“移动”

内存分配具有的结构和功能：

1. 内存分配数据结构。用于记录内存空间的使用情况，作为内存分配的依据。
2. 内存分配功能。系统安装一定的内存分配算法为用户程序分配内存空间。
3. 内存回收功能。系统对于用户不在需要的内存，通过用户的释放请求去完成系统的回收功能。

### 2. 内存保护
内存保护的主要任务是确保每道用户程序都只在自己的内存空间运行，彼此互不干扰；系统必须设置内存保护机制，一种比较简单的内存保护机制是设置两个界限寄存器，分别用于存放程序的上届和下届。系统必须对
每条指令所要访问的地址进行检查，如果发生越界，便发出越界中断的请求，以停止该程序的执行。一般情况下，越界检查都由硬件来实现，发生越界后的处理，还须与软件的配合来完成。

### 3. 地址映射
一个应用程序经过编译之后，通常会形成若干个目标程序;这些目标程序再经过链接便形成了可装入程序。这些程序的地址都是从“0”开始的，程序中的其他地址都是相对于起始地址计算的。由这些地址所形成的地址范围称为“地址空间”，其中的地址称为“逻辑地址”或“相对地址”。此外，由内存中的一系列单元所限定的地址范围称为“内存空间”，其中的地址称为“物理地址”。
在多道程序的环境下，每道程序不可能都是从 “0” 地址开始装入（内存），这就导致地址空间内的逻辑地址和内存空间中的物理地址不一致。为了使得程序能正常运行，
存储器管理必须提供地址映射的功能，以将地址空间中的逻辑地址转换为内存空间中与之对应的物理地址。该功能在硬件的支持下完成。

### 4. 内存扩充
这里的扩充不是去扩大物理内存的容量，而是借助于虚拟存储技术，从逻辑上去扩充内存容量，使用户所感觉到的内存的容量比实际的内存容量大的多，以便程序能并发的运行。

## 设备管理功能
设备管理功能用来管理计算机系统中所有的外围设备，设备管理的主要任务是：

- 完成用户进程提出的 I/O 请求
- 为用户进程分配其所需的 I/O 设备
- 提高 CPU 和 I/O 设备的利用率
- 提高 I/O 速度
- 方便用户使用 I/O 设备

## 文件管理功能
文件管理的主要任务是对用户文件和系统文件进行管理，以便方便用户使用，并保证文件的安全性。文件管理应具备对文件存储的管理，目录管理，文件的读写管理，以及文件的共享与保护等功能。
