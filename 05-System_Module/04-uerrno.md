# **uerrno** – 系统错误码模块

!!! abstract "简介"
    `uerrno` 模块提供了标准的 errno 系统符号，每个符号都有对应的整数值。

## 示例

```
try:
    uos.mkdir("my_dir")
except OSError as exc:
    if exc.args[0] == uerrno.EEXIST:
        print("Directory already exists")
uerrno.errorcode
Dictionary mapping numeric error codes to strings with symbolic error code (see above):

>>> print(uerrno.errorcode[uerrno.EEXIST])
EEXIST
```
更多内容可参考 [errno](https://docs.python.org/3/library/errno.html?highlight=errno#module-errno) 。

----------