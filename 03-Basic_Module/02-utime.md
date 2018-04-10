# **utime** – 时间相关函数
`utime` 模块提供获取当前时间和日期、测量时间间隔和延迟的功能。

更多内容可参考 [`time`](http://docs.micropython.org/en/latest/pyboard/library/utime.html#module-utime)  。

`函数`

- utime.sleep(seconds)  
  休眠指定的时间（秒），Seconds 可以是浮点数。注意有些版本的 MicroPython不支持浮点数，为了兼容可以使用 sleep_ms() 和 ``sleep_us()``函数。

- utime.sleep_ms(ms)  
  延时指定毫秒，参数不能小于0。

- utime.sleep_us(us)  
  延时指定微秒，参数不能小于0。

- utime.ticks_ms()  
  返回不断递增的毫秒计数器，在某些值后会重新计数(未指定)。计数值本身无特定意义，只适合用在``ticks_diff()``。

注：执行标准数学运算（+，-）或关系运算符（<，>，>，> =）直接在这些值上会导致无效结果。执行数学运算然后传递结果作为论据来`ticks_diff()` 或 ` ticks_add() ` 也将导致后一个函数的无效结果。

- utime.ticks_us()  
  和上面 ticks_ms() 类似，只是返回微秒。

- utime.ticks_cpu()  
  与 ticks_ms() 和 ticks_us() 类似，具有更高精度 (使用 CPU 时钟)。

- 可用性：并非每个端口都实现此功能。

`example`:

```
>>> import time
>>> 
>>> time.sleep(1)           # sleep for 1 second
>>> time.sleep_ms(500)      # sleep for 500 milliseconds
>>> time.sleep_us(10)       # sleep for 10 microseconds
>>> start = time.ticks_ms() # get value of millisecond counter
>>> delta = time.ticks_diff(time.ticks_ms(), start) # compute time difference
```

----------