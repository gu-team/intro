# 接口文档

[TOC]

## Post: /api/uploadElf/{filename}

### 说明

上传`elf`文件，后端判断是否为`elf`文件，并用`gdb`加载该文件。

`file`命令的实现。

### request

`Content-Type: multipart/form-data`

### response

|参数名称|必选|类型|描述|
|---|---|---|---|
|code|是|int|0表示失败，1表示成功|
|message|是|String|提示内容|

```json
{
    "code": 0,
    "message": "fail, it is not elf file"
}
```

## Get: /api/start

### 说明

首先，后端根据`session`和`cookie`判断该用户是否已经上传加载了文件，然后在使用`gdb`命令启动该`elf`文件。

`start`命令的实现。

### request

### response

|参数名称|必选|类型|描述|
|---|---|---|---|
|code|是|int|0表示失败，1表示成功|
|message|是|string|提示内容|

```json
{
    "code": 0,
    "message": "fail, it has not upload the elf file"
}
```

## Post: /api/break

### 说明

对已经加载和运行的文件下断点，分三种情况：

- `break <function>`，在指定的函数入口处设置断点
- `break <linenum>`，在指定的行号处设置断点。**???若没有上传源文件，还可以吗**
- `break *<address>`，在指定地址对应的代码处(指令处)设置断点

### request

`Content-Type: application/json`

|参数名称|必选|类型|描述|
|---|---|---|---|
|type|是|int|0表示函数名，1表示行号，2表示十六进制地址|
|message|是|string|`<function>` / `<linenum>` / `<address>`|

```json
{
    "type": 0,
    "message": "main"
}
```

### response

|参数名称|必选|类型|描述|
|---|---|---|---|
|code|是|int|0表示失败，1表示成功|
|message|是|string|提示内容|
|address|是|int|断点十六进制地址|
|line|是|int|断点行号|

```json
{
    "code": 0,
    "message": "...",
    "address": 0x400da0,
    "line": 37
}
```

## Get: /api/continue

### 说明

进行到下一个断点位置。

`continue`的实现。

### request

### response

|参数名称|必选|类型|描述|
|---|---|---|---|
|code|是|int|0表示失败，1表示成功|
|message|是|string|提示内容|

```json
{
    "code": 0,
    "message": "..."
}
```

## Get: /api/next

### 说明

单步执行到下一步。

`next`的实现。

### request

### response

|参数名称|必选|类型|描述|
|---|---|---|---|
|code|是|int|0表示失败，1表示成功|
|message|是|string|提示内容|

```json
{
    "code": 0,
    "message": "..."
}
```

## Get: /api/step

### 说明

单步执行下一步并进入函数。

`step`的实现。

### request

### response

|参数名称|必选|类型|描述|
|---|---|---|---|
|code|是|int|0表示失败，1表示成功|
|message|是|string|提示内容|

```json
{
    "code": 0,
    "message": "..."
}
```

## Post: /api/disassemble

### 说明

查看函数的反汇编

`disassemble`的实现。

### request

`Content-Type: application/json`

|参数名称|必选|类型|描述|
|---|---|---|---|
|funName|是|string|函数的名字，为空则默认当前函数|

```json
{
    "funName": ""
}
```

### response

|参数名称|必选|类型|描述|
|---|---|---|---|
|code|是|int|0表示失败，1表示成功|
|message|是|string|提示内容|
|assemb|是|string[]|反汇编字符串数组|

```json
{
    "code": 0,
    "message": "...",
    "assemb": [
        "0x0000000000400da0 <+0>:     push   %rbx",
        "0x0000000000400da1 <+1>:     cmp    $0x1,%edi",
        "0x0000000000400da4 <+4>:     jne    0x400db6 <main+22>",
        "0x0000000000400da6 <+6>:     mov    0x20299b(%rip),%rax        # 0x603748 <stdin@@GLIBC_2.2.5>",
        "0x0000000000400dad <+13>:    mov    %rax,0x2029b4(%rip)        # 0x603768 <infile>",
        "0x0000000000400db4 <+20>:    jmp    0x400e19 <main+121>",
        "0x0000000000400db6 <+22>:    mov    %rsi,%rbx",
        "0x0000000000400db9 <+25>:    cmp    $0x2,%edi",
        "0x0000000000400dbc <+28>:    jne    0x400df8 <main+88>",
        "0x0000000000400dbe <+30>:    mov    0x8(%rsi),%rdi",
        "0x0000000000400dc2 <+34>:    mov    $0x4022b4,%esi",
        "0x0000000000400dc7 <+39>:    callq  0x400c10 <fopen@plt>",
        "0x0000000000400dcc <+44>:    mov    %rax,0x202995(%rip)        # 0x603768 <infile>",
        ......
    ]
}
```

## Get: /api/getRip

### 说明

获取`rip`的值，即当前指令的地址。

`print $rip`的实现。

### request

### response

|参数名称|必选|类型|描述|
|---|---|---|---|
|code|是|int|0表示失败，1表示成功|
|message|是|string|提示内容|
|rip|是|int|地址值|

```json
{
    "code": 0,
    "message": "...",
    "rip": 0x400da6
}
```

## Get: /api/getRegisters

### 说明

获取寄存器的值

`info registers`的实现。

### request

### response

|参数名称|必选|类型|描述|
|---|---|---|---|
|code|是|int|0表示失败，1表示成功|
|message|是|string|提示内容|
|registers|是|object[]|对象数据，表示各寄存器|

`object`:

|参数名称|必选|类型|描述|
|---|---|---|---|
|name|是|string|寄存器名字|
|value|是|int|寄存器中的值|

```json
{
    "code": 0,
    "message": "...",
    "registers": [
        {
            "name": "rsp",
            "value": 0x7ffffffede48
        },
        .....
    ]
}
```