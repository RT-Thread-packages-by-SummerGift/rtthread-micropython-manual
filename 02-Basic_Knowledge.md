# RT-Thread MicroPython 基础知识

## 1. 运行 python 文件

在 MicroPython 上运行 python 文件有以下要求：

- 系统内使用了 rt-thread 的文件系统。
- 开启 `msh` 功能。

符合以上两点，就可以使用 `msh` 命令行中的 `python` 命令加上 `*.py` 文件名来执行一个 python 文件了。

## 2. 术语表

### baremetal

  A system without a (full-fledged) OS, for example an [MCU](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-mcu)-based system. When running on a baremetal system, MicroPython effectively becomes its user-facing OS with a command interpreter (REPL).

### board

  A PCB board. Oftentimes, the term is used to denote a particular model of an [MCU](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-mcu) system. Sometimes, it is used to actually refer to [MicroPython port](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-micropython-port) to a particular board (and then may also refer to “boardless” ports like [Unix port](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-micropython-unix-port)).

### callee-owned tuple

  A tuple returned by some builtin function/method, containing data which is valid for a limited time, usually until next call to the same function (or a group of related functions). After next call, data in the tuple may be changed. This leads to the following restriction on the usage of callee-owned tuples - references to them cannot be stored. The only valid operation is extracting values from them (including making a copy). Callee-owned tuples is a MicroPython-specific construct (not available in the general Python language), introduced for memory allocation optimization. The idea is that callee-owned tuple is allocated once and stored on the callee side. Subsequent calls don’t require allocation, allowing to return multiple values when allocation is not possible (e.g. in interrupt context) or not desirable (because allocation inherently leads to memory fragmentation). Note that callee-owned tuples are effectively mutable tuples, making an exception to Python’s rule that tuples are immutable. (It may be interesting why tuples were used for such a purpose then, instead of mutable lists - the reason for that is that lists are mutable from user application side too, so a user could do things to a callee-owned list which the callee doesn’t expect and could lead to problems; a tuple is protected from this.)

### CPython

  CPython is the reference implementation of Python programming language, and the most well-known one, which most of the people run. It is however one of many implementations (among which Jython, IronPython, PyPy, and many more, including MicroPython). As there is no formal specification of the Python language, only CPython documentation, it is not always easy to draw a line between Python the language and CPython its particular implementation. This however leaves more freedom for other implementations. For example, MicroPython does a lot of things differently than CPython, while still aspiring to be a Python language implementation.

### GPIO

  General-purpose input/output. The simplest means to control electrical signals. With GPIO, user can configure hardware signal pin to be either input or output, and set or get its digital signal value (logical “0” or “1”). MicroPython abstracts GPIO access using [`machine.Pin`](http://docs.micropython.org/en/latest/pyboard/library/machine.Pin.html#machine.Pin) and [`machine.Signal`](http://docs.micropython.org/en/latest/pyboard/library/machine.Signal.html#machine.Signal) classes.

### GPIO port

  A group of [GPIO](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-gpio) pins, usually based on hardware properties of these pins (e.g. controllable by the same register).

### interned string

  A string referenced by its (unique) identity rather than its address. Interned strings are thus can be quickly compared just by their identifiers, instead of comparing by content. The drawbacks of interned strings are that interning operation takes time (proportional to the number of existing interned strings, i.e. becoming slower and slower over time) and that the space used for interned strings is not reclaimable. String interning is done automatically by MicroPython compiler and runtimer when it’s either required by the implementation (e.g. function keyword arguments are represented by interned string id’s) or deemed beneficial (e.g. for short enough strings, which have a chance to be repeated, and thus interning them would save memory on copies). Most of string and I/O operations don’t produce interned strings due to drawbacks described above.

### MCU

  Microcontroller. Microcontrollers usually have much less resources than a full-fledged computing system, but smaller, cheaper and require much less power. MicroPython is designed to be small and optimized enough to run on an average modern microcontroller.

### micropython-lib

  MicroPython is (usually) distributed as a single executable/binary file with just few builtin modules. There is no extensive standard library comparable with [CPython](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-cpython). Instead, there is a related, but separate project [micropython-lib](https://github.com/micropython/micropython-lib) which provides implementations for many modules from CPython’s standard library. However, large subset of these modules require POSIX-like environment (Linux, FreeBSD, MacOS, etc.; Windows may be partially supported), and thus would work or make sense only with [`MicroPython Unix port`](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-micropython-unix-port). Some subset of modules is however usable for [`baremetal`](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-baremetal) ports too.Unlike monolithic [CPython](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-cpython) stdlib, micropython-lib modules are intended to be installed individually - either using manual copying or using [upip](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-upip).

### MicroPython port

  MicroPython supports different [boards](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-board), RTOSes, and OSes, and can be relatively easily adapted to new systems. MicroPython with support for a particular system is called a “port” to that system. Different ports may have widely different functionality. This documentation is intended to be a reference of the generic APIs available across different ports (“MicroPython core”). Note that some ports may still omit some APIs described here (e.g. due to resource constraints). Any such differences, and port-specific extensions beyond MicroPython core functionality, would be described in the separate port-specific documentation.

### MicroPython Unix port

  Unix port is one of the major [MicroPython ports](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-micropython-port). It is intended to run on POSIX-compatible operating systems, like Linux, MacOS, FreeBSD, Solaris, etc. It also serves as the basis of Windows port. The importance of Unix port lies in the fact that while there are many different [boards](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-board), so two random users unlikely have the same board, almost all modern OSes have some level of POSIX compatibility, so Unix port serves as a kind of “common ground” to which any user can have access. So, Unix port is used for initial prototyping, different kinds of testing, development of machine-independent features, etc. All users of MicroPython, even those which are interested only in running MicroPython on [MCU](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-mcu) systems, are recommended to be familiar with Unix (or Windows) port, as it is important productivity helper and a part of normal MicroPython workflow.

### port

  Either [MicroPython port](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-micropython-port) or [GPIO port](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-gpio-port). If not clear from context, it’s recommended to use full specification like one of the above.

### stream

  Also known as a “file-like object”. An object which provides sequential read-write access to the underlying data. A stream object implements a corresponding interface, which consists of methods like `read()`, `write()`, `readinto()`, `seek()`, `flush()`, `close()`, etc. A stream is an important concept in MicroPython, many I/O objects implement the stream interface, and thus can be used consistently and interchangeably in different contexts. For more information on streams in MicroPython, see [`uio`](http://docs.micropython.org/en/latest/pyboard/library/uio.html#module-uio) module.

### upip

  (Literally, “micro pip”). A package manage for MicroPython, inspired by [CPython](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-cpython)’s pip, but much smaller and with reduced functionality. upip runs both on [Unix port](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-micropython-unix-port) and on [baremetal](http://docs.micropython.org/en/latest/pyboard/reference/glossary.html#term-baremetal) ports (those which offer filesystem and networking support).