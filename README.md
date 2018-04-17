# RT-Thread Micropython 开发手册介绍

----------

!!! abstract "摘要"
     本手册介绍了 RT-Thread MicroPython 的基础知识、常用模块，以及开发新模块的流程。带领读者了解 MicroPython ，并学会使用 MicroPython 进行开发。
     
## 1.1 主要特性

- MicroPython 是 Python 3 编程语言的一种精简而高效的实现，它包含 Python 标准库的一个子集，并被优化为在微控制器和受限环境中运行。

- RT-Thread MicroPython 可以运行在任何搭载了 RT-Thread 操作系统并且有一定资源的嵌入式平台上。

- MicroPython 可以运行在有一定资源的开发板上，给你一个低层次的 Python 操作系统，可以用来控制各种电子系统。

- MicroPython 富有各种高级特性，比如交互式提示、任意精度整数、闭包函数、列表解析、生成器、异常处理等等。

- MicroPython 的目标是尽可能与普通 Python 兼容，使开发者能够轻松地将代码从桌面端转移到微控制器或嵌入式系统。程序可移植性很强，因为不需要考虑底层驱动，所以程序移植变得轻松和容易。

## 1.2 MicroPython 的优势

- Python 是一款容易上手的脚本语言，同时具有强大的功能，语法优雅简单。使用 MicroPython 编程可以降低嵌入式的开发门槛，让更多的人体验嵌入式的乐趣。
- 通过 MicroPython 实现硬件底层的访问和控制，不需要了解底层寄存器、数据手册、厂家的库函数等，即可轻松控制硬件。
- 外设与常用功能都有相应的模块，降低开发难度，使开发和移植变得容易和快速。

## 1.3 MicroPython 的应用领域

- MicroPython 在嵌入式系统上完整实现了 Python3 的核心功能，可以在产品开发的各个阶段给发开发者带来便利。
- 通过  MicroPython  提供的库和函数，开发者可以快速控制 LED、液晶、舵机、多种传感器、SD、UART、I2C 等，实现各种功能，而不用再去研究底层模块的使用方法。这样不但降低了开发难度，而且减少了重复开发工作，可以加快开发速度，提高开发效率。以前需要较高水平的嵌入式工程师花费数天甚至数周才能完成的功能，现在普通的嵌入式开发者用几个小时就能实现类似的功能，而且要更加轻松和简单。
- 随着半导体技术的不断发展，芯片的功能、内部的存储器容量和资源不断增加，成本不断降低，可以使用 MicroPython 来进行开发设计的应用领域越来越多。

### 1.3.1 产品原型设计

- 使用 MicroPython  对于产品原型设计、软件移植非常有好处，让开发过程变得轻松，充满乐趣。和传统开发方法相比，使用 MicroPython 开发产品原型的速度更快，程序也更容易实现模块化，更方便进行维护。程序不用反复编译、下载、仿真，有很多的库可以参考使用。
- 网络功能是 MicroPython  的长处，在进行一些联网功能开发时可以利用已有的众多网络模块，这些功能如果使用C/C++ 来完成，会耗费几倍的时间。

### 1.3.2 教育

- MicroPython  使用简单、方便，性能好，非常适合于编程入门。在校学生或者业余爱好者都可以通过 MicroPython 快速的开发一些好玩的项目，在开发的过程中学习编程思想，提高自己的动手能力。

### 1.3.3 创客 DIY

- MicroPython 无需复杂的设置，不需要安装特别的软件和额外的硬件，使用任何文本编辑器就可以进行编程。大部分硬件功能，使用一个命令就能驱动，不用了解硬件底层就能快速开发。这些特性使得 MicroPython 非常适合创客使用来开发一些有创意的项目。

# 2. MicroPython 开发资源

- [MicroPython 官方网站](https://micropython.org/)
- [在线文档](http://docs.micropython.org/en/latest/pyboard/)
- [MicroPython 在线演示](https://micropython.org/unicorn)
- [MicroPython 源码](https://github.com/micropython/micropython)
- [MicroPython 官方论坛](http://forum.micropython.org/)
- [MicroPython 中文社区](http://www.micropython.org.cn/)
- [RT-Thread MicroPython 论坛](https://www.rt-thread.org/qa/forum.php)

