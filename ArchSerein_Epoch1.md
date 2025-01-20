# CFC Studio 共学 Epoch1 指引
---
# [ArchSerein]

> 通过共学计划完成 cs162 的剩余实验和学习 cmu18447

## 笔记证明

> 下面的日期请保证至少两个字符占位
>
>   * 正确：12.06
>   * 错误：12.6
>
> 若当天没有学习内容，请直接跳过该日期的记录，不要在日期下记录：“请假” 等内容

### 12.06

举例示范：

今日学习时间：XXXX
学习内容小结：XXXX
Homework 部分（如果有安排需要填写证明完成）
Question and Ideas（有什么疑问/或者想法，可以记在这里，也可以分享到群里讨论交流）

<!-- Content_START --> 
### 01.06

> 今日学习时间：

> 3h

> 今日学习任务：

> reading -> Multiprocessor Benchmarks and Performance Models

> 学习内容小结：

> in this subsection, the main discussion is about evaluating processor performance through benchmarking. But due to such traditional restrictions to benchmark is chiefly limited to the architecture and compiler, better data structuers and algorithms maybe give a misleading result. Then, ucbidentified 13 design patterns that they will be part of applications of the future. Next, the main discussion of The Roofline Model, how to use it to find performance bottlenecks and how to optimize the processor. How to reduce computational bottlenecks: mix floating-point operation, improve inst-level parallelism and apply SIMD; How to reduce memory bottlenecks: software prefetching and memory affinity.

> Question and Ideas（有什么疑问/或者想法，可以记在这里，也可以分享到群里讨论交流）

> a description of The Roofline Models is at the link [the roofline models wiki](https://en.wikipedia.org/wiki/Roofline_model)

### 01.07

> 今日学习时间：

> 3h

> 今日学习任务：

> Completing the file system buffer cache

> 学习内容小结：

> The original pintos implementation of the file system, when it performs read/write operations, that will directly access the file system's underlying block device. Now, I need to add a buffer cache for the file system.

> the buffer cache structure I designed is:
```
struct buf {
  int cnt;
  bool dirty;
  struct block *dev;
  block_sector_t blockno;
  struct list_elem elem;
  uint8_t data[BLOCK_SECTOR_SIZE];
};
/**
* cnt: number of references to the current buffer 
* dirty: when data is only written to the buffer and not synchronized to disk, dirty is true, otherwise false
* dev: maybe always fs_device, but like fsutil.c use other device, maybe they don't need the buffer cache
* blockno: sector number, the position of read/write
* elem: list element, Data Structures for Bidirectional Chained Tables
* data: the data aera of buffer
**/
```
> when pintos need to read/write, it will use bread/bwrite, not block_read/block_write. block_read/block_write will be used in the bread/bwrite, when caching missing. If there are no free cache blocks, the LRU algorithm will be used to replace the one that meets the requirement. You need to make sure that ditry is set before replacing it, and if it is true you need to write it back to disk and replace it.

### 01.08

> 今日学习时间：

> 4.5h

> 今日学习任务：

> Synchronize the modified contents of the buffer to disk in the idle thread, add cwd records to the pcb, and add directory support to the filesystem (partial implementation).

> 学习内容小结：

> The cwd in pcb records the inode, but in userproc only inode structure declaration and can not access to the actual data in the inode, at first thought of how to make userproc only contain inode header file on struct inode definition but has not been successful, later in rtfsc when found in the file system Then I found out in rtfsc that there is a layer of abstraction in the file system and it provides a way to get the inode (you need to add a helper function yourself).

> As far as directory support is concerned, it is currently just an update of the lookup function originally provided by pintos.

> Regarding the synchronization of data in the buffer to disk, the manual says that this is achieved by non-busy-wait sleep, but I don't have much of an idea, so I just synchronize when the current resource is free, i.e., when the idle thread is running.

> Finally, I used the originally unused area of the inode_disk to implement the file extension support

> However, I felt that the design idea was not perfect and needed a lot of modification.

### 01.09

> 今日学习时长

> 6h

> 今日学习任务

> Added support for all directory-related system calls and filesystems, though there are still issues

> 学习内容小结

> Even if you have a simple idea before implementation, but when you implement it according to your own thinking, because you don't have enough rtfsc, it will lead to some processes are not well implemented or even have conflicts, then you have to re-conceptualize and change your thinking, but the source code of pintos is still relatively complex, then I am stuck in a loop, I hope to finish it soon!

> commit log: [01.09](https://github.com/crazyofcode/cs162/commit/cc3a71d28370b9c9da209a12575c7765d0349482)

### 01.10

> 今日学习时长

> 5h

> 今日学习任务

> Continuing with yesterday's mission.

> 学习内容小结

> Fixed the logic in the syscall parameter check, updated the logic in mkdir, open, write to create directories properly, and the userprog test points passed except for oom (which is supposed to be caused by files opened by cwd).

> commit log: [01.10](https://github.com/crazyofcode/cs162/commit/592aa7e4e475cc4efd3208a72dd8179b1551705c)

### 01.12

> 今日学习时长

> 4.5h

> 今日学习任务

> 缝缝补补, 跟着测试点的错误信息, 修改实现的问题

> 学习内容小节

> 主要是文件/目录的新建和删除相关操作实现的补充, 比如不能删除 pcb->cwd 的父目录和不能删除 "/" 目录等, 现在关于这两个部分的测试点还有 rm-tree 没有通过

> commit log: [01.12](https://github.com/crazyofcode/cs162/commit/4bde035a38e5dcddd2faed3fc4d6a567af5bc508)

### 01.13

> 今日学习时长

> 6h

> 今日学习任务

> 修复关于文件系统中 dir 相关实现的 bug

> 学习内容小结

> readdir 系统调用的实现错误, pos 指针没有被正确的记录, 修改了在第一个 proj 中对于打开文件的 entry 的定义, 增加了对目录的支持, 相应的系统调用函数如: open 等也作了相应的修改, 修改了 dir lookup 函数的 bug, 修复了 inode 被打开但是没有被正确的关闭的问题，最后是文件扩容的问题(只是实现了部分, 即是说扩容量必须小于 BLOCK_SECTOR_SIZE), 但是 dir-vine 测试点还没有通过。

> commit log: [01.13](https://github.com/crazyofcode/cs162/commit/72421901cba7848d660457f330f7f4c405ee1969)

### 01.14

> 今日学习时长

> 5h

> 今日学习任务

> 完善文件的扩展, 使用 120 个直接索引和 6 个间接索引, 能够支持更大的文件

> 学习内容小结

> 将 pintos 提供的 free-map 的功能函数进行封装，以满足我设计的双重索引的需要，主要修改了释放和分配 sector 块的逻辑，不过由于需要判断是所以直接索引还是简介索引以及间接索引的内容在哪一块磁盘空间导致逻辑变得更为复杂，写得有些乱，然后发现我的持久性测试都没有通过但是我在 shundown 和 idle-thread 里都有 bflush 的使用，还没找到问题

> commit log: [01.14](https://github.com/crazyofcode/cs162/commit/ac3e1f81c82ffa5c5b886b5b2262cc0fd0767d63)

### 01.15

> 今日学习时长

> 2h

> 今日学习任务

> 文件系统的持久化

> 学习内容小结

> 持久化的测试调试不了一点, 只能看到错误信息是 "存在名字为空的文件"，但是看不到其他的信息, 对于它打包的 tar 文件也是很难查看, 呃呃呃放弃了。后面开始看 18447 的 slides 了，cs162 就到这了吧。

### 01.16

> 今日学习时长

> 4h

> 今日学习任务

> out-of-order's lecture, Memory Technology and Organization's slide and P&H 5.1-5.2

> 学习内容小结

> OoO 主要介绍的是指令的调度和寄存器的重命名。第一种方案是每个 unit 会有一个 reservation table 记录使用的数据的来源, 每一个条目有一个别名, 会将这个别名记录到 registers alias table 中作为寄存器的别名并将寄存器的 valid 位置为 0表示这个寄存器的值在后续的 cycle 中由 producer 写入, 所有和这个寄存器有关的 consumer 都会被 stall。在 producer 完成该条指令后会通过总线进行广播，会更新每个 unit 和 registers alias table 中和这个寄存器相关的条目，如果该条目更新后，需要的源数据都准备好后就会有调度器决定是否进入后续的流水线。关于每个 unit 中的数据什么时候 retire，我还不是很清楚。由于通过总线广播生产的数据时会在很多个 table 中复制，为了减少这种消耗，后来简化成了类似指针的结构，分为前端的寄存器和与 arch 状态相关的物理寄存器，前端的寄存器在 renaming 后会有一个 index 指向实际使用的物理寄存器，以这种方式减少数据的复制。对于 commit 的指令不会立刻 retire，而是保存在 rob 中，保证顺序发射，乱许执行，顺序提交，用以实现精确异常。后面还补充了关于内存类似的步骤，不过由于内存的地址空间是非常大的，难以使用 renaming。

### 01.17

> 今日学习时长

> 5h

> 今日学习任务

> 实现 xip 取指方式，程序可以跳转到 flash 空间执行

> 学习内容小结

> 要在硬件层次实现 flash_read() 的功能, 也就是要按照一定的顺序在硬件上访问SPI master的寄存器. 需要用状态机实现 flash_read() 的功能! 与上文从flash中加载程序并执行的方式不同, 这种从flash颗粒中取指的方式并不需要在执行程序之前将程序读入到内存(对应上文的SRAM)中, 因此也称"就地执行"(XIP, eXecute In Place)方式。ysyxSOC 把 spi master 的地址空间和 flash 的地址空间都映射到了 apb 端口, 即是说在实现 xip 取指令的同时需要区分访问的是 spi 还是 flash。

> 讲义给出了如何实现的简单描述: 

1. 检查APB请求的目标地址, 若目标地址落在SPI master的地址空间, 则正常访问并回复
2. 若目标地址落在flash存储空间, 则进入XIP模式. 在XIP模式中, SPI master的输入信号由相应状态机决定
3. 状态机依次往SPI master的设备寄存器中写入相应的值, 写入的值与flash_read()基本一致
4. 状态机轮询SPI master的完成标志, 等待SPI master完成数据传输
5. 状态机从SPI master的RX寄存器中读出flash返回的数据, 处理后通过APB返回, 并退出XIP模式

> 因此我根据 flash_read 的软件实现设置了7个状态分别用来表示 xip空闲, 写 CMD, 写 DIV，写CTRL，选择 slave，循环读取 CTRL 中的完成标志位，读取 RX 寄存器中的值，禁用 slave(感觉不是必须)

> 读取出的数据是字节倒序的需要 invert_endian

### 01.19

> 今日学习时长

> 6h

> 今日学习任务

> 在上次实现 xip 后将程序加载到 flash 执行

> 学习内容小结

> 在上次的 xip 实现中，in_xip 状态的更新有错误不应该根据 xip_state 处于 IDLE 状态简单的判断 xip 已经完成了一轮状态的转移，后来发现在 xip 取指令时 penable 是一直处于高电平的，于是就通过 penable 信号判断 xip 是否执行结束。后续需要将 reset_addr 和 linker script 的和 mrom 相关的切换到 flash。然后在改写 linker script 时出现了一个问题: file offset too huge，想了挺久没有想到为什么会导致这个问题的原因，就恢复到 mrom 时的然后简单的替换和修改地址空间。发现之前遗漏了 sdata 和 srodata 这两个段的数据，导致一些程序在运行的好似后会读取到错误的数据。最后为 ysyxsoc 添加了 timer 的 AM, 在运行 coremark 等程序时会用到，增加了对 timer 寄存器访问的 skip difftest 的逻辑.

### 01.20

> 今日学习时长

> 3h

> 今日学习任务

> readings: memory hierarchy and cache(direct-mapped)

> 学习内容小结

> memory hierarchy 介绍了 SRAM, DRAM, EEPROM, FLASH and DISK 的相关概念，然后用了一个生活中的例子类比介绍了内存模型所利用的局部性原理。cache 是 18447 的 slide 中讨论的不过由于没有视频讲解，只看 slide 理解还是有些困难的。只看了关于 cache 的一些基本概念和如何尝试构建一个 direct-mapped cache. 还有一个离谱的是由于 npc 接入 soc 后仿真的效率显著的下降了导致我以为是指令执行失败，我开了 difftest 发现确实会有对比失败的指令执行，但是我检查了 axi 和 xip 应该是没有大问题的，毕竟 cpu-tests 是都可以跑过的。我试着去看了看 nemu 的 src，发现 nemu 的 memory 我是开了 random data 的导致 npc 取到的是 0，nemu 取到的是随机数据。现在我关闭了内存的随机化，但是跑了挺久(我一开始以为和 nemu 的速度慢不了多少)还是没有运行结束，我就在 coremark 里加了 debug info 才发现是运行得太慢了。

<!-- Content_END -->
