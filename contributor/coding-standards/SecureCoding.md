# 一、范围

CANN开源社区开发者。

# 二、C++安全编码规范

C++安全编码规范涉及到内存与指针安全、数值运算安全、输入与数据验证、资源管理、文件与IO安全、并发与数据一致性、接口与兼容性、隐私保护等。

[C++安全编码规范门禁扫描支持情况](#41-c安全编码规范门禁扫描支持情况)

### 2.1新增文件时在文件头必须添加COPYRIGHT和LICENSE声明

举例：
c++文件COPYRIGHT和LICENSE声明：

```
/*
 * Copyright (c) 2025 Huawei Technologies Co., Ltd.
 * This file is a part of the CANN Open Software.
 * Licensed under CANN Open Software License Agreement Version 1.0 (the "License").
 * Please refer to the License for details. You may not use this file except in compliance with the License.
 * THIS SOFTWARE IS PROVIDED ON AN "AS IS" BASIS, WITHOUT WARRANTIES OF ANY KIND, EITHER EXPRESS OR IMPLIED,
 * INCLUDING BUT NOT LIMITED TO NON-INFRINGEMENT, MERCHANTABILITY, OR FITNESS FOR A PARTICULAR PURPOSE.
 * See LICENSE in the root of the software repository for the full text of the License.
 */
```

### 2.2 确保有符号整数运算不溢出

**【描述】**
有符号整数溢出是未定义的行为。出于安全考虑，对外部数据中的有符号整数值在如下场景中使用时，需要确保运算不会导致溢出：

- 指针运算的整数操作数(指针偏移值)
- 数组索引
- 变长数组的长度(及长度运算表达式)
- 内存拷贝的长度
- 内存分配函数的参数
- 循环判断条件

在精度低于int的整数类型上进行运算时，需要考虑整数提升。程序员还需要掌握整数转换规则，包括隐式转换规则，以便设计安全的算术运算。

1)加法

**【错误代码示例】**(加法)

如下代码示例中，参与加法运算的整数是外部数据，在使用前未做校验，可能出现整数溢出。

```
int num_a = ... // 来自外部数据
int num_b = ... // 来自外部数据
int sum = num_a + num_b;
...
```

**【正确代码示例】**(加法)

```
int num_a = ... // 来自外部数据
int num_b = ... // 来自外部数据
int sum = 0;
if (((num_a > 0) && (num_b > (INT_MAX - num_a))) ||
	((num_a < 0) && (num_b < (INT_MIN - num_a)))) {
 	... // 错误处理
}
sum = num_a + num_b;
...
```

2)减法

**【错误代码示例】**(减法)

如下代码示例中，参与减法运算的整数是外部数据，在使用前未做校验，可能出现整数溢出，进而造成后续的内存复制操作出现缓冲区溢出。

```
unsigned char  *content = ... // 指向报文头的指针
size_t content_size = ... // 缓冲区的总长度
int total_len = ... // 报文总长度
int skip_len = ... // 从消息中解析出来的需要忽略的数据长度
// 用total_len - skip_len 计算剩余数据长度，可能出现整数溢出
(void)memmove(content, content + skip_len, total_len - skip_len);
...
```

**【正确代码示例】**(减法)

如下代码示例中，重构为使用size_t类型的变量表示数据长度，并校验外部数据长度是否在合法范围内。

```
unsigned char *content = ... //指向报文头的指针
size_t content_size = ... // 缓冲区的总长度
size_t total_len = ... // 报文总长度
size_t skip_len = ... // 从消息中解析出来的需要忽略的数据长度
if (skip_len >= total_len || total_len > content_size) {
	... // 错误处理
}

(void)memmove(content, content + skip_len, total_len - skip_len);
...
```

3)乘法

**【错误代码示例】**(乘法)

如下代码示例中，内核代码对来自用户态的数值范围做了校验，但是由于opt是int类型，而校验条件中错误的使用了ULONG_MAX进行限制，导致整数溢出。

```
int opt = ... // 来自用户态
if ((opt < 0) || (opt > (ULONG_MAX / (60 * HZ)))) { // 错误的使用了ULONG_MAX做上限校验
	return -EINVAL;
}

... = opt * 60 * HZ; // 可能出现整数溢出
...
```

**【正确代码示例】**(乘法)

一种改进方案是将opt的类型修改为unsigned long类型，这种方案适用于修改了变量类型更符合业务逻辑的场景。

```
unsigned long opt = ... // 将类型重构为 unsigned long 类型。
if (opt > (ULONG_MAX / (60 * HZ))) {
	return -EINVAL;
}
... = opt * 60 * HZ;
...
```

另一种改进方案是将数值上限修改为INT_MAX。

```
int opt = ... // 来自用户态
if ((opt < 0) || (opt > (INT_MAX / (60 * HZ)))) { // 修改使用INT_MAX作为上限值
	return -EINVAL;
}
... = opt * 60 * HZ;
```

4)除法

**【错误代码示例】**(除法)

如下代码示例中，做除法运算前只检查了是否出现被零除的问题，缺少对数值范围的校验，可能出现整数溢出。

```
int num_a =  ... // 来自外部数据
int num_b =  ... // 来自外部数据
int result = 0;

if (num_b == 0) {
	... // 对除数为0的错误处理
}

result = num_a / num_b; // 可能出现整数溢出
...
```

**【正确代码示例】**(除法)

如下代码示例中，按照最大允许值进行校验，防止整数溢出，在编程时可根据具体业务场景做更严格的值域校验。

```
int num_a = ... // 来自外部数据

int num_b = ... // 来自外部数据

int result = 0;

// 检查除数为0及除法溢出错误

if ((num_b == 0) || ((num_a == INT_MIN) && (num_b == -1))) {

 ... // 错误处理

}

result = num_a / num_b;
...
```

5)求余数

**【错误代码示例】**(求余数)

```
int num_a = ... // 来自外部数据
int num_b = ... // 来自外部数据
int result = 0;
if (num_b == 0) {
	... // 对除数为0的错误处理
}

result = num_a % num_b; // 可能出现整数溢出
...
}
```

**【正确代码示例】**(求余数)

如下代码示例中，按照最大允许值进行校验，防止整数溢出。在编程时可根据具体业务场景做更严格的值域校验。

```
int num_a =  ... // 来自外部数据
int num_b =  ... // 来自外部数据
int result = 0;

// 检查除数为0及除法溢出错误
if ((num_b == 0)  || ((num_a == INT_MIN) && (num_b == -1))) {
	... // 错误处理
}

result = num_a % num_b;
...
}
```

6)一元减

当操作数等于有符号整数类型的最小值时，在二进制补码一元求反期间会发生溢出。

**【错误代码示例】**(一元减)

如下代码示例中，计算前未校验数值范围，可能出现整数溢出。

```
int num_a = ... // 来自外部数据
int result = -num_a; // 可能出现整数溢出
...
```

**【正确代码示例】**(一元减)

如下代码示例中，按照最大允许值进行校验，防止整数溢出。在编程时可根据具体业务场景做更严格的值域校验。

```
int num_a =  ... // 来自外部数据
int result = 0;

if (num_a == LNT_MIN) {
	... // 错误处理
}

result = -num_a;
...
```

### 2.3 确保无符号整数运算不回绕

**【描述】**

涉及无符号操作数的计算永远不会溢出，因为超出无符号整数类型表示范围的计算结果会按照（结果类型可表示的最大值 + 1）的数值取模。

这种行为更多时候被非正式地称为无符号整数回绕。

在精度低于int的整数类型上进行运算时，需要考虑整数提升。程序员还需要掌握整数转换规则，包括隐式转换规则，以便设计安全的算术运算。

出于安全考虑，对外部数据中的无符号整数值在如下场景中使用时，需要确保运算不会导致回绕：

- 指针运算的整数操作数(指针偏移值)
- 数组索引
- 变长数组的长度(及长度运算表达式)
- 内存拷贝的长度
- 内存分配函数的参数
- 循环判断条件

1)加法

**【错误代码示例】**(加法)

如下代码示例中，校验下一个子报文的长度加上已处理报文的长度是否超过了整体报文的最大长度，在校验条件中的加法运算可能会出现整数回绕，造成绕过该校验的问题。

```
size_t total_len =  ... // 报文的总长度
size_t read_len = 0 // 记录已经处理报文的长度
...
size_t pkt_len = parse_pkt_len(); // 从网络报文中解析出来的下一个子报文的长度
if (read_len + pkt_len > total_len) { // 可能出现整数回绕
	... // 错误处理
}

...
read_len += pkt_len;
...
```

**【正确代码示例】**(加法)

由于read_len变量记录的是已经处理报文的长度，必然会小于total_len，因此将代码中的加法运算修改为减法运算，导致条件绕过。

```
size_t total_len = ... // 报文的总长度
size_t read_len = 0; // 记录已经处理报文的长度
...

size_t pkt_len = parse_pkt_len(); // 来自网络报文
if (pkt_len > total_len - read_len) {
	... // 错误处理
}

...
read_len += pkt_len;
...
```

2)减法

**【错误代码示例】**(减法)

如下代码示例中，校验len合法范围的运算可能会出现整数回绕，导致条件绕过。

```
size_t len = ... // 来自用户态输入
if (SCTP_SIZE_MAX - len < sizeof(SctpAuthBytes)) { // 减法操作可能出现整数回绕
	... // 错误处理
}

... = kmalloc(sizeof(SctpAuthBytes) + len, gfp); // 可能出现整数回绕
...
```

**【正确代码示例】**(减法)

如下代码示例中，调整减法运算的位置（需要确保编译期间减法表达式的值不翻转），避免整数回绕问题。

```
size_t len = ... // 来自用户态输入
if (len > SCTP_SIZE_MAX - sizeof(SctpAuthBytes)) { // 确保编译期间减法表达式的值不翻转
	... // 错误处理
}

... = kmalloc(sizeof(SctpAuthBytes) + len, gfp);
...
```

3)乘法

**【错误代码示例】**（乘法）

如下代码示例中，使用外部数据计算申请内存长度时未校验，可能出现整数回绕。

```
size_t width =  ... // 来自外部数据
size_t hight =  ... // 来自外部数据
unsigned char  *buf = (unsigned char  *)malloc(width  * hight);
```

无符号整数回绕可能导致分配的内存不足。

**【正确代码示例】**（乘法）

如下代码是一种解决方案，校验参与乘法运算的整数数值范围，确保不会出现整数回绕。

```
size_t width =  ... // 来自外部数据
size_t hight =  ... // 来自外部数据
if (width == 0 || hight == 0) {
	... // 错误处理
}

if (width  > SIZE_MAX / hight) {
	... // 错误处理
}

unsigned char  *buf = (unsigned char  *)malloc(width  * hight);
```

**【例外】**
为正确执行程序，必要时无符号整数可能表现出模态（回绕）。建议将变量声明明确注释为支持模数行为，并且对该整数的每个操作也应明确注释为支持模数行为。

**【相关软件CWE编号】** CWE-190

### 2.4 确保除法和余数运算不会导致除以零的错误(被零除)

**【描述】**

整数的除法和取余运算的第二个操作数值为0会导致程序产生未定义的行为，因此使用时要确保整数的除法和余数运算不会导致除零错误(被零除，下同)。

1)除法

**【错误代码示例】**(除法)

有符号整数类型的除法运算如果限制不当，会导致溢出。

如下示例对有符号整数进行的除法运算做了防止溢出限制，确保不会导致溢出，但不能防止有符号操作数num_a和num_b之间的除法过程中出现除零错误：

```
int num_a =  ... // 来自外部数据
int num_b =  ... // 来自外部数据
int result = 0;

if ((num_a == INT_MIN) && (num_b == -1)) {
	... // 错误处理
}

result = num_a / num_b; // 可能出现除零错误
...
```

**【正确代码示例】**(除法)

如下代码示例中，添加num_b是否为0的校验，防止除零错误。

```
int num_a =  ... // 来自外部数据
int num_b =  ... // 来自外部数据
int result = 0;

if ((num_b == 0)  | | ((num_a == INT_MIN) && (num_b == -1))) {
	... // 错误处理
}

result = num_a / num_b;
...
```

2)取余

**【错误代码示例】**(求余数)

如下代码，同除法的错误代码示例一样，可能出现除零错误，因为许多平台以相同的指令实现求余数和除法运算。

```
int num_a =  ... // 来自外部数据
int num_b =  ... // 来自外部数据
int result = 0;

if ((num_a == INT_MIN) && (num_b == -1)) {
	... // 错误处理
}

result = num_a % num_b; // 可能出现除零错误
...
```

**【正确代码示例】**(求余数)

如下代码示例中，添加num_b是否为0的校验，防止除零错误。

```
int num_a =  ... // 来自外部数据
int num_b =  ... // 来自外部数据
int result = 0;

if ((num_b == 0)  | | ((num_a == INT_MIN) && (num_b == -1))) {
	... // 错误处理
}

result = num_a % num_b;
...
```

### 2.5 禁止使用未初始化的变量

【描述】
这里的变量，指的是局部动态变量，并且还包括内存堆上申请的内存块。 因为他们的初始值都是不可预料的，所以禁止未经有效初始化就直接读取其值。

```
void foo( ...)
{
	int data;
	bar(data); // 错误：未初始化就使用
	...
}
```

如果有不同分支，要确保所有分支都得到初始化后才能使用：

```
#define CUSTOMIZED_SIZE 100
void foo( ...)
{
	int data;
	if (condition > 0) {
		data = CUSTOMIZED_SIZE;
	}

	bar(data); // 错误：部分分支该值未初始化
	...
}
```

### 2.6 指向资源句柄或描述符的变量，在资源释放后立即赋予新值

**【描述】**
指向资源句柄或描述符的变量包括指针、文件描述符、socket描述符以及其它指向资源的变量。
以指针为例，当指针成功申请了一段内存之后，在这段内存释放以后，如果其指针未立即设置为NULL，也未分配一个新的对象，那这个指针就是一个悬空指针。
如果再对悬空指针操作，可能会发生重复释放或访问已释放内存的问题，造成安全漏洞。
消减该漏洞的有效方法是将释放后的指针立即设置为一个确定的新值，例如设置为NULL。对于全局性的资源句柄或描述符，在资源释放后，应该马上设置新值，以避免使用其已释放的无效值；对于只在单个函数内使用的资源句柄或描述符，应确保资源释放后其无效值不被再次使用。

**【错误代码示例】**
如下代码示例中，根据消息类型处理消息，处理完后释放掉body或head指向的内存，但是释放后未将指针设置为NULL。如果还有其他函数再次处理该消息结构体时，可能出现重复释放内存或访问已释放内存的问题。

```
int foo(void)
{
	SomeStruct *msg = NULL;
	... // 初始化msg->type，分配 msg->body 的内存空间
	if (msg->type == MESSAGE_A) {
		...
		free(msg->body);
	}

	...
EXIT:
	...
	free(msg->body);
	return ret;
}
```

**【正确代码示例】**
如下代码示例中，立即对释放后的指针设置为NULL，避免重复放指针。

```
int foo(void)
{
	SomeStruct  *msg = NULL;
	... // 初始化msg->type，分配 msg->body 的内存空间

	if (msg->type == MESSAGE_A) {
		...
		free(msg->body);
		msg->body = NULL;
	}

	...
EXIT:
	...
	free(msg->body);
	return ret;
}
```

当free()函数的入参为NULL时，函数不执行任何操作。

**【错误代码示例】**
如下代码示例中文件描述符关闭后未赋新值。

```
SOCKET s = INVALID_SOCKET;
int fd = -1;
...
closesocket(s);
...
close(fd);
...
```

**【正确代码示例】**
如下代码示例中，在资源释放后，对应的变量应该立即赋予新值。

```
SOCKET s = INVALID_SOCKET;
int fd = -1;
...
closesocket(s);
s = INVALID_SOCKET;
...
close(fd);
fd = -1;
...
```

### 2.7 外部数据作为数组索引时必须确保在数组大小范围内

**【描述】**
外部数据作为数组索引对内存进行访问时，必须对数据的大小进行严格的校验，确保数组索引在有效范围内，否则会导致严重的错误。
当一个指针指向数组元素时，可以指向数组最后一个元素的下一个元素的位置，但是不能读写该位置的内存。

**【错误代码示例】**
如下代码示例中, set_dev_id()函数存在差一错误，当 index 等于 DEV_NUM 时，恰好越界写一个元素；
同样get_dev()函数也存在差一错误，虽然函数执行过程中没有问题，但是当解引用这个函数返回的指针时，行为是未定义的。

```
#define DEV_NUM 10
#define MAX_NAME_LEN 128
typedef struct {
	int id;
	char name[MAX_NAME_LEN];
} Dev;

static Dev devs[DEV_NUM];
int set_dev_id(size_t index, int id)
{
	if (index > DEV_NUM) { // 错误：差一错误。
 		... // 错误处理
	}

	devs[index].id = id;
	return 0;
}

static Dev *get_dev(size_t index)
{
	if (index > DEV_NUM) { // 错误：差一错误。
 		... // 错误处理
	}

	return devs + index;
}
```

**【正确代码示例】**
如下代码示例中，修改校验索引的条件，避免差一错误。

```
#define DEV_NUM 10
#define MAX_NAME_LEN 128
typedef struct {
	int id;
	char name[MAX_NAME_LEN];
} Dev;

static Dev devs[DEV_NUM];

int set_dev_Id (size_t index, int id)
{
	if (index >= DEV_NUM) {
		... // 错误处理
	}

	devs[index].id = id;
	return 0;
}

static Dev *get_dev(size_t index)
{
	if (index >= DEV_NUM) {
 		... // 错误处理
	}

	return devs + index;
}
```

**【相关软件CWE编号】** CWE-119，CWE-123，CWE-125

### 2.8 禁止通过对指针变量进行sizeof操作来获取数组大小

**【描述】**
将指针当做数组进行sizeof操作时，会导致实际的执行结果与预期不符。例如：变量定义 char *p = array，其中array的定义为char array[LEN]，表达式sizeof(p) 得到的结果与 sizeof(char *)相同，并非array的长度。

**【错误代码示例】**
如下代码示例中，buffer和path分别是指针和数组，程序员想对这2个内存进行清0操作，但由于程序员的疏忽，将内存大小误写成了sizeof(buffer)，与预期不符。

```
char path[MAX_PATH];
char *buffer = (char *)malloc(SIZE);
...
(void)memset(path, 0, sizeof(path));
// sizeof与预期不符，其结果为指针本身的大小而不是缓冲区大小
(void)memset(buffer, 0, sizeof(buffer));
```

**【正确代码示例】**
如下代码示例中，将sizeof(buffer)修改为申请的缓冲区大小：

```
char path[MAX_PATH];
char *buffer = (char *)malloc(SIZE);
...
(void)memset(path, 0, sizeof(path));
(void)memset(buffer, 0, SIZE); // 使用申请的缓冲区大小
```

### 2.9 指针操作，使用前必须要判空

**【描述】**解引用空指针会导致程序产生未定义行为，通常会造成程序异常终止。

* 指针变量在使用前，一定要做好初始化的赋值，严禁对空指针进行访问；
* 对于指针所代表的地址空间的任何操作，一定要保证空间的有效性；
* 指针指向的内存释放后，操作系统并不会自动将指针置为NULL，需要调用者将指针显式置为NULL，防止“野指针”
* 内部函数传参时，在上级调用函数能确保传参不会为NULL的情况下，可以不对入参进行非NULL检查。
  **【错误代码示例】**

```
// result 未做除空指针判断
auto result = executor->AllocTensor(self->GetDataType(), op::Format::FORMAT_ND, op::Format::FORMAT_ND);
INFER_SHAPE(BinaryCrossEntropy, OP_INPUT(self, target, weight), OP_OUTPUT(result), OP_ATTR(reduction));
```

**【正确代码示例】**

```
// 业务中较多场景会需要申请指针，可以在申请加校验，保证业务场景不会触发空指针的解引用
auto result = executor->AllocTensor(self->GetDataType(), op::Format::FORMAT_ND, op::Format::FORMAT_ND);
CHECK_RET(reluOut != nullptr, nullptr);
INFER_SHAPE(BinaryCrossEntropy, OP_INPUT(self, target, weight), OP_OUTPUT(result), OP_ATTR(reduction));
```

**【错误代码示例】**

```
// 未对context.GetOptionalInputDesc(ATTEN_MASK_INPUT_INDEX)进行非空判断，导致coredump
uint32_t attenMaskTypeSize = NUM_BYTES_BOOL; // default DT_BOOL
auto attenMaskInput = context.GetOptionalInputTensor(ATTEN_MASK_INPUT_INDEX);
if (attenMaskInput != nullptr) {
   auto attenMaskDataType = context.GetOptionalInputDesc(ATTEN_MASK_INPUT_INDEX)->GetDataType();
   ......
}
```

**【正确代码示例】**

```
uint32_t attenMaskTypeSize = NUM_BYTES_BOOL; // default DT_BOOL
auto attenMaskInput = context.GetOptionalInputTensor(ATTEN_MASK_INPUT_INDEX);
if (attenMaskInput != nullptr) {
    OP_TILING_CHECK(context.GetOptionalInputDesc(ATTEN_MASK_INPUT_INDEX) == nullptr,
                VECTOR_INNER_ERR_REPORT_TILIING(context.GetNodeName(), "Desc of tensor atten_mask is nullptr"),
                return ge::GRAPH_FAILED);  // 校验空指针，报错退出

    auto attenMaskDataType = context.GetOptionalInputDesc(ATTEN_MASK_INPUT_INDEX)->GetDataType();
    ......}
```

### 2.10 确保字符串存储有足够的空间容纳字符数据和null结束符

**【描述】**
将数据复制到不足以容纳数据的缓冲区，会导致缓冲区溢出。缓冲区溢出经常发生在字符串操作中。为了避免这种错误，截断拷贝的数据以限制字符串的字节长度是一种防御方法，但是最好的措施是确保目标缓冲区的大小足以容纳复制数据和null结束符。当字符串存储在堆空间时， 确保分配内存时已分配了足够的空间。

部分字符串处理函数由于设计时安全考虑不足，或者存在一些隐含的目的缓冲区长度要求，容易被误用，导致缓冲区写溢出。此类典型函数包括不在C标准库函数中的itoa()，realpath()函数。

**【错误代码示例】**(itoa)
有些函数如itoa(), realpath()需要在对传入的缓冲区指针位置进行写入操作，但函数并没有提供缓冲区长度。因此，在调用这些函数前，必须提供足够的缓冲区。
如下代码示例中，试图将数字转为字符串，但是目标存储空间的预留长度不足：

```
int num = ...
char str[8];
itoa(num, str, 10); // 10进制整数的最大存储长度是12个字节
```

**【正确代码示例】**
如下代码示例中，在对外部数据进行解析并将内容保存到name中，考虑了name的大小：

```
int num = ...
char str[13];
itoa(num, str, 10); // 10进制整数的最大存储长度是12个字节
```

【错误代码示例】**(realpath)**

如下代码示例中，试图将路径标准化，但是目标存储空间的长度不足：

```
#define MAX_PATH_LEN 100
char resolved_path[MAX_PATH_LEN];
/ *
- realpath函数的存储缓冲区长度是由PATH_MAX常量定义，
- 或是由_PC_PATH_MAX系统值配置的，通常都大于100字节
*/

char  *res = realpath(path, resolved_path);
...
```

**【正确代码示例】**

可以将realpath的第二个参数传入NULL, 以让系统自动分配合适的内存。

```
char *resolved_path = NULL;
resolved_path = realpath(path, NULL);
if (resolved_path == NULL) {
	... // 处理错误
}

...
if (resolved_path != NULL) {
	free(resolved_path);
	resolved_path = NULL;
}
...
```

**【相关软件CWE编号】** CWE-170，CWE-464

### 2.11 资源申请后必须判断是否成功

**【描述】**
内存、对象、stream、notify等资源申请分配一旦失败，那么后续的操作会存在未定义的行为风险。比如malloc申请失败返回了空指针，对空指针的解引用是一种未定义行为，需要进行异常捕获或返回值校验。

**【错误代码示例】**
如下代码示例中，调用malloc分配内存之后，没有判断是否成功，直接引用了p。如果malloc失败，它将返回一个空指针并传递给p。当如下代码在内存拷贝中解引用了该空指针p时，程序会出现未定义行为。

```
struct tm *make_tm(int year, int mon, int day, int hour, int min, int sec)
{
	struct tm *tmb = (struct tm*)malloc(sizeof(*tmb));
	tmb->year = year;
	...

	return tmb;
}
```

**【正确代码示例】**
如下代码示例中，在malloc分配内存之后，立即判断其是否成功，消除了上述的风险。

```
struct tm  *make_tm(int year, int mon, int day, int hour, int min, int sec)
{
	struct tm  *tmb = (struct tm *)malloc(sizeof(*tmb));
	if (tmb == NULL) {
		... // 错误处理
	}

	tmb->year = year;
	...
	return tmb;
}
```

### 2.12 外部输入作为内存操作相关函数的复制长度时，需要校验其合法性

**【描述】**
将数据复制到容量不足以容纳该数据的内存中会导致缓冲区溢出。为了防止此类错误，必须根据目标容量的大小限制被复制的数据大小，或者必须确保目标容量足够大以容纳要复制的数据。

**【错误代码示例】**
外部输入的数据不一定会直接作为内存复制长度使用，还可能会间接参与内存复制操作。
如下代码示例中，inputTable->count来自外部报文，虽然没有直接作为内存复制长度使用，而是作为for循环体的上限使用，间接参与了内存复制操作。由于没有校验其大小，可造成缓冲区溢出：

```
typedef struct {
	size_t count;
	int val[MAX_num_bERS];
} ValueTable;

ValueTable *value_table_dup(const ValueTable *input_table)
{
	ValueTable *output_table = ... // 分配内存
	...
	for (size_t i = 0; i  < input_table->count; i++) {
		output_table->val[i] = input_table->val[i];
	}
 	...
}
```

**【正确代码示例】**
如下代码示例中，对input_table->count做了校验。

```
typedef struct {
size_t count;
int val[MAX_num_bERS];
}ValueTable;

ValueTable *value_table_dup(const ValueTable *input_table)
{
	ValueTable *output_table = ... // 分配内存
	...

	/ *
	- 根据应用场景，对来自外部报文的循环长度input_table->count
	- 与output_table->val数组大小做校验，避免造成缓冲区溢出
	*/
	if (input_table->count  > sizeof(output_table->val) / sizeof(output_table->val[0]){
		return NULL;
	}

	for (size_t i = 0; i  < input_table->count; i++) {
		output_table->val[i] = input_table->val[i];
	}

	...
}
```

### 2.13 创建文件时必须显式指定合适的文件访问权限

**【描述】**
创建文件时，如果不显式指定合适访问权限，可能会让未经授权的用户访问该文件，造成信息泄露，文件数据被篡改，文件中被注入恶意代码等风险。

虽然文件的访问权限也依赖于文件系统，但是当前许多文件创建函数（例如POSIX open函数）都具有设置（或影响）文件访问权限的功能，所以当使用这些函数创建文件时，必须显式指定合适的文件访问权限，以防止意外访问。

**【错误代码示例】**
使用POSIX open()函数创建文件但未显示指定该文件的访问权限，可能会导致文件创建时具有过高的访问权限，这可能会导致漏洞。

```
void foo(void)
{
	int fd = -1;
	char *file_name = NULL;
	... // 初始化 file_name
	fd = open(file_name, O_CREAT | O_WRONLY); // 没有显式指定访问权限
	if (fd == -1) {
		... // 错误处理
	}
	...
}
```

**【正确代码示例】**
应该在open的第三个参数中显式指定新创建文件的访问权限。可以根据文件实际的应用情况设置何种访问权限。

```
void foo(void)
{
	int fd = -1;
	char *file_name = NULL;
	... // 初始化 file_name 和指定其访问权限
	// 此处根据文件实际需要，显式指定其访问权限
	int fd = open(file_name, O_CREAT | O_WRONLY, S_IRUSR | S_IWUSR);
	if (fd == -1) {
		... // 错误处理
	}
	...
}
```

### 2.14 必须对文件路径进行规范化后再使用

**【描述】**
当文件路径来自外部数据时，必须对其做合法性校验，如果不校验，可能造成系统文件的被任意访问。但是禁止直接对其进行校验，正确做法是在校验之前必须对其进行路径规范化处理，因为：
同一个文件可以通过多种形式的路径来描述和引用，例如既可以是绝对路径，也可以是相对路径；而且路径名、目录名和文件名可能包含使校验变得困难和不准确的字符（如："."、".."）。此外，文件还可以是符号链接，这进一步模糊了文件的实际位置或标识，增加了校验的难度和校验准确性。所以必须先将文件路径规范化，从而更容易校验其路径、目录或文件名，增加校验准确性，如使用realpath函数。

一个简单的案例说明如下：

当文件路径来自外部数据时，需要先将文件路径规范化，如果没有作规范化处理，攻击者就有机会通过恶意构造文件路径进行文件的越权访问。

例如，攻击者可以构造"../../../etc/passwd"的方式进行任意文件访问。

**【错误代码示例】**
在此错误的示例中，argv[1]包含一个源于受污染源的文件名，并且该文件名已打开以进行写入。在使用此文件名操作之前，应该对其进行验证，以确保它引用的是预期的有效文件。
不幸的是，argv[1]引用的文件名可能包含特殊字符，例如目录字符，这使验证变得困难，甚至不可能。而且，argv[1]中可能包含可以指向任意文件路径的符号链接，即使该文件名通过了验证，也会导致该文件名是无效的。
这种场景下，对文件名的直接验证即使被执行也是得不到预期的结果，对fopen()的调用可能会导致访问一个意外的文件。

```
...
if (!verify_file(input_file_name) { // 没有对input_file_name做规范化，直接做校验
	... // 错误处理
}

if (fopen(input_file_name, "w") == NULL) {
	... // 错误处理
}
...
```

**【正确代码示例】**
规范化文件名是具有一定难度的，因为这需要了解底层文件系统。
POSIX realpath()函数可以帮助将路径名转换为规范形式。

对上面的错误代码示例，我们采用如下解决方案：

```
char *real_path_res = NULL;
...
// 在校验之前，先对input_file_name做规范化处理
real_path_res = realpath(input_file_name, NULL);
if (real_path_res == NULL) {
	... // 规范化的错误处理
}

// 规范化以后对路径进行校验
if (!verify_file(real_path_res) {
	... // 校验的错误处理
}

// 使用
if (fopen(real_path_res, "w") == NULL) {
	... // 实际操作的错误处理
}

...
free(real_path_res);
real_path_res = NULL;
...
```

**【正确代码示例】**
根据我们的实际场景，我们还可以采用的第二套解决方案，说明如下：

如果PATH_MAX被定义为中的一个常量，那么使用非空的resolved_path调用realpath()也是安全的。
在本例中realpath()函数期望resolved_path引用一个字符数组，该字符数组足够大，可以容纳规范化的路径。
如果定义了PATH_MAX，则分配一个大小为PATH_MAX的缓冲区来保存realpath()的结果。正确代码示例如下：

```
char *real_path_res = NULL;
char *canonical_file_name = NULL;
size_t path_size = 0;
...
path_size = (size_t)PATH_MAX;
if (verify_path_size(path_size) == TRUE) {
	canonical_file_name = (char *)malloc(path_size);
	if (canonical_file_name == NULL) {
		... // 错误处理
	}

	real_path_res = realpath(inputFilename, canonical_file_name);
}

if (real_path_res == NULL) {
	... // 错误处理
}

if (verify_file(real_path_res) == FALSE) {
	... // 错误处理
}

if (fopen(real_path_res, "w") == NULL ) {
	... // 错误处理
}

...
free(canonical_file_name);
canonical_file_name = NULL;
...
```

**【错误代码示例】**
下面的代码场景是从外部获取到文件名称，拼接成文件路径后，直接对文件内容进行读取，导致攻击者可以读取到任意文件的内容：

```
char *file_name = get_msg_from_remote();
...
sprintf(untrust_path, "/tmp/%s", file_name);
char *text = read_file_content(untrust_path);
```

**【正确代码示例】**
正确的做法是，对路径进行规范化后，再判断路径是否是本程序所认为的合法的路径：

```
char *file_name = get_msg_from_remote();
...
sprintf(untrust_path, "/tmp/%s", file_name);
char path[PATH_MAX] = {0};
if (realpath(untrust_path, path) == NULL) {
	... // 处理错误
}

if (!is_valid_path(path)) { // 检查文件的位置是否正确
	... // 处理错误
}

char *text = read_file_content(path);
```

**【例外】**

运行于控制台的命令行程序，通过控制台手工输入文件路径，可以作为本条款例外。

```
int main(int argc, char **argv)
{
	int fd = -1;
	if (argc == 2) {
		fd = open(argv[1], O_RDONLY);
		...
	}

	...
}
```

### 2.15 外部输入数据（如函数入参/通信消息/寄存器数据等）需要做合法性校验

**【描述】**

* 1、外部输入数据需要做合法性校验且确保校验范围正确
* 2、边界接口需要对传入的地址做合法性校验避免任意地址读写
* 3、需要对入参进行合法性校验避免数组越界
* 4、需要对地址偏移校验避免任意地址读写
* 5、外部传入指针需要判空后使用（模块内调用确认不会传入空指针下不需要判空）
* 6、外部入参参与循环、递归条件的运算，必须严格校验边界和终止条件
* 7、文件路径来自外部数据时，必须对其做合法性校验

### 2.16 资源泄露（内存、句柄、锁等）

**【描述】**

* 1、资源申请和释放必须匹配，包括：内存类的malloc/free/alloc_page/free_page, 锁lock/unlock、文件open/close，文件引用fget/fput，symbol_get/symbol_put，内存mm_get/mm_put，尤其关注异常分支和异常场景。
* 2、释放结构体/类/数组/各类数据容器指针前，必须先释放成员指针
* 3、对外接口处理涉及资源申请但未释放，引起资源泄露，导致拒绝服务
* 4、C++捕获异常时确保恢复程序的一致性; 建议使用RAII模式，确保资源在异常发生时自动释放

### 2.17 访问临界资源需要进行保护

**【描述】**临界资源的保护是多线程编程中的关键问题，不合理的访问会导致数据不一致、内存踩踏、程序崩溃、死锁等问题，需要使用互斥锁进行保护或使用线程安全函数。以下场景需要尤其注意：

* 1、多线程共享的全局变量
* 2、线程与中断都会访问的数据结构
* 3、C语言非线程安全的函数在多线程环境下调用
* 4、用户态线程与信号处理函数都会访问的变量/数据结构

### 2.18 对外结构体接口新增字段时必须在结构体最后添加

* 【描述】：为了最大程度上在ABI层面的兼容，对外结构体接口添加新字段时必须在结构体最后添加。

### 2.19 外部接口或数据结构变更必须考虑兼容性

**【描述】**外部接口、接口参数、返回值、数据结构、消息字段等变更会引起版本兼容性问题，或者是客户界面变更，导致客户应用程序执行出错，非必要不建议变更，在必须变更时，须与相关干系人确认清楚。

# 三、python安全编码规范
python安全编码规范涉及到数值运算安全、输入与数据验证、文件与系统操作安全、加密与通信安全、特定格式处理安全、隐私保护等。

[python安全编码规范门禁扫描支持情况](#42-python安全编码规范门禁扫描支持情况)


### 3.1 文件头注释应该包含COPYRIGHT和LICENSE声明

**【描述】**在每个源文件的开头添加COPYRIGHT和LICENSE声明，确保代码的合法性和可追溯性。这有助于保护代码的知识产权，并明确使用条款。

举例：

```
#
# Copyright (c) 2025 Huawei Technologies Co., Ltd.
# This file is a part of the CANN Open Software.
# Licensed under CANN Open Software License Agreement Version 1.0 (the "License").
# Please refer to the License for details. You may not use this file except in compliance with the License.
# THIS SOFTWARE IS PROVIDED ON AN "AS IS" BASIS, WITHOUT WARRANTIES OF ANY KIND, EITHER EXPRESS OR IMPLIED,
# INCLUDING BUT NOT LIMITED TO NON-INFRINGEMENT, MERCHANTABILITY, OR FITNESS FOR A PARTICULAR PURPOSE.
# See LICENSE in the root of the software repository for the full text of the License.
#
```
### 3.2 对除法运算和模运算中的除数为0的情况做相应保护

**【描述】**在进行除法运算或取模运算时，应先检查除数是否为0，以防止程序因除零错误而崩溃。可以通过条件语句或异常处理来实现。

### 3.3 禁止通过异常泄露敏感数据

**【描述】**在捕获和处理异常时，不应将敏感数据（如密码、密钥等）包含在异常消息中，以防止这些信息被意外泄露。

### 3.4 产品代码不要包含任何调试入口点

**【描述】**发布的产品代码中不应包含用于调试的入口点或特殊功能，以确保代码的安全性和稳定性。调试代码应在开发环境中单独管理。

### 3.5 正式发布的代码及注释内容要合法合规，不要有个人隐私信息

**【描述】**正式发布的代码和注释内容要合法合规；不应包含开发者的个人隐私信息（如身份证号码、手机号码等），以保护个人隐私。

### 3.6 代码中包含禁止包含用户界面不可见、或是资料未公开的公网地址

**【描述】**代码中不应硬编码公网地址，以防止因地址变更导致的问题或因公网地址引起的质疑。对于公开的公网地址应该存储在配置文件或数据库中。
**【例外】**对于标准协议中必须指定公网地址的场景例外。

### 3.7 在多用户系统中创建文件时应根据需要指定合适的权限

**【描述】**在多用户系统中创建文件时，应根据实际需求设置合适的文件权限，以确保文件的安全性和访问控制。

### 3.8 使用外部数据构造的文件路径前必须进行校验，校验前必须对文件路径进行规范化处理

**【描述】**在使用外部数据生成文件路径之前，应对路径进行规范化处理（如去除多余的路径分隔符），并进行校验，以防止路径遍历攻击。

### 3.9 禁止使用tempfile.mktemp创建临时文件

**【描述】**`tempfile.mktemp` 函数存在安全风险，因为它不会创建文件，只返回一个路径，可能导致竞态条件。应使用 `tempfile.TemporaryFile` 或 `tempfile.NamedTemporaryFile` 来创建临时文件。

### 3.10 临时文件使用完毕应及时删除

**【描述】**临时文件在使用完毕后应立即删除，以释放系统资源并防止数据泄露。

### 3.11 解压文件必须进行安全检查

**【描述】**在解压文件之前，应对压缩文件进行安全检查，确保其中不包含恶意文件或路径遍历攻击。

### 3.12 禁止使用pickle.load、_pickle.load和shelve模块加载外部数据

**【描述】**`pickle` 和 `shelve` 模块存在安全风险，因为它们可以执行任意代码。应使用更安全的序列化方法，如 `json`。

### 3.13 禁止序列化未加密的敏感数据

**【描述】**在序列化敏感数据时，应使用加密算法进行加密，以防止数据在传输过程中被窃取。

### 3.14 禁止使用yaml模块的load函数

**【描述】**`yaml.load` 函数存在安全风险，因为它可以执行任意代码。应使用 `yaml.safe_load` 来替代。

### 3.15 禁止使用jsonpickle模块的encode/decode或dumps/loads函数

**【描述】**`jsonpickle` 模块存在安全风险，因为它可以执行任意代码。应使用更安全的序列化方法，如 `json`。

### 3.16 禁止使用eval和exec函数执行不可信代码

**【描述】**`eval` 和 `exec` 函数可以执行任意代码，存在严重的安全风险。应避免使用这些函数处理不可信的数据。

### 3.17 禁止使用OS命令解析器或“危险函数”调用系统命令

**【描述】**应避免使用 `os.system`、`os.popen` 等函数直接调用系统命令，因为它们存在注入攻击的风险。应使用 `subprocess` 模块的更安全方法。

### 3.18 避免在命令解析器中使用通配符

**【描述】**在命令解析器中使用通配符（如 `*`）可能会导致意外的行为和安全问题。应尽量避免使用通配符，明确指定文件名或路径。

### 3.19 禁止使用subprocess模块中的shell=True选项

**【描述】**`subprocess` 模块的 `shell=True` 选项会通过系统 shell 执行命令，存在注入攻击的风险。应使用 `shell=False` 并传递命令列表。

### 3.20 不受信任的外部数据禁止使用.format()进行格式化

**【描述】**在使用 `str.format` 方法时，应避免使用不受信任的外部数据，以防止格式字符串注入攻击。可以使用 `f-string` 或 `str.format_map` 方法。

### 3.21 禁止直接使用外部数据来拼接XML

**【描述】**直接使用外部数据拼接 XML 可能会导致 XML 注入攻击。应使用 XML 库提供的安全方法来构建 XML 文档。

### 3.22 禁止在处理XML数据时解析不可信的实体

**【描述】**在处理 XML 数据时，应禁用外部实体解析，以防止 XXE（XML External Entity）攻击。

### 3.23 禁止直接使用外部数据记录日志

**【描述】**直接使用外部数据记录日志可能泄露敏感信息。应对外部数据进行过滤和清理后再记录日志。

### 3.24 禁止在生产版本的业务代码中使用assert

**【描述】**`assert` 语句在生产环境中会被忽略，不应依赖于 `assert` 进行错误处理。应使用条件语句和异常处理来确保代码的健壮性。

### 3.25 将敏感对象发送出信任区域前进行签名并加密

**【描述】**在将敏感对象发送到非信任区域（如网络传输）之前，应对其进行数字签名和加密，以确保数据的完整性和保密性。

### 3.26 安全场景下必须使用密码学意义上的安全随机数

**【描述】**在涉及安全性的场景中（如生成密钥、令牌等），应使用密码学安全的随机数生成器，以防止被预测和攻击。

### 3.27 必须使用ssl.SSLSocket代替socket.Socket来进行安全数据交互

**【描述】**在进行网络通信时，应使用 `ssl.SSLSocket` 而不是普通的 `socket.Socket`，以确保数据传输的安全性。

### 3.28 禁止在用户界面、日志中暴露不必要信息

**【描述】**在用户界面和日志中不应暴露不必要的信息，特别是敏感信息，以防止信息泄露和滥用。

# 四 附录

## 4.1 C++安全编码规范门禁扫描支持情况

| 规则 | 支持情况 |
| :--- | :---: |
| [2.1 新增文件时在文件头必须添加copyright和license声明](#21新增文件时在文件头必须添加copyright和license声明) | 支持 |
| [2.2 确保有符号整数运算不溢出](#22-确保有符号整数运算不溢出) | 不支持 |
| [2.3 确保无符号整数运算不回绕](#23-确保无符号整数运算不回绕) | 不支持 |
| [2.4 确保除法和余数运算不会导致除以零的错误被零除](#24-确保除法和余数运算不会导致除以零的错误被零除) | 支持 |
| [2.5 禁止使用未初始化的变量](#25-禁止使用未初始化的变量) | 不支持 |
| [2.6 指向资源句柄或描述符的变量在资源释放后立即赋予新值](#26-指向资源句柄或描述符的变量在资源释放后立即赋予新值) | 支持 |
| [2.7 外部数据作为数组索引时必须确保在数组大小范围内](#27-外部数据作为数组索引时必须确保在数组大小范围内) | 不支持 |
| [2.8 禁止通过对指针变量进行sizeof操作来获取数组大小](#28-禁止通过对指针变量进行sizeof操作来获取数组大小) | 支持 |
| [2.9 指针操作使用前必须要判空](#29-指针操作使用前必须要判空) | 不支持 |
| [2.10 确保字符串存储有足够的空间容纳字符数据和null结束符](#210-确保字符串存储有足够的空间容纳字符数据和null结束符) | 支持 |
| [2.11 资源申请后必须判断是否成功](#211-资源申请后必须判断是否成功) | 不支持 |
| [2.12 外部输入作为内存操作相关函数的复制长度时需要校验其合法性](#212-外部输入作为内存操作相关函数的复制长度时需要校验其合法性) | 不支持 |
| [2.13 创建文件时必须显式指定合适的文件访问权限](#213-创建文件时必须显式指定合适的文件访问权限) | 不支持 |
| [2.14 必须对文件路径进行规范化后再使用](#214-必须对文件路径进行规范化后再使用) | 不支持 |
| [2.15 外部输入数据如函数入参通信消息寄存器数据等需要做合法性校验](#215-外部输入数据如函数入参通信消息寄存器数据等需要做合法性校验) | 不支持 |
| [2.16 资源泄露内存句柄锁等](#216-资源泄露内存句柄锁等) | 不支持 |
| [2.17 访问临界资源需要进行保护](#217-访问临界资源需要进行保护) | 不支持 |
| [2.18 对外结构体接口新增字段时必须在结构体最后添加](#218-对外结构体接口新增字段时必须在结构体最后添加) | 不支持 |
| [2.19 外部接口或数据结构变更必须考虑兼容性](#219-外部接口或数据结构变更必须考虑兼容性) | 不支持 |

## 4.2 Python安全编码规范门禁扫描支持情况
| 规则 | 支持情况 |
| :--- | :---: |
|[3.1 文件头注释应该包含COPYRIGHT和LICENSE声明](#31-文件头注释应该包含copyright和license声明)|支持|
|[3.2 对除法运算和模运算中的除数为0的情况做相应保护](#32-对除法运算和模运算中的除数为0的情况做相应保护)|支持|
|[3.3 禁止通过异常泄露敏感数据](#33-禁止通过异常泄露敏感数据)|支持|
|[3.4 产品代码不要包含任何调试入口点](#34-产品代码不要包含任何调试入口点)|支持|
|[3.5 正式发布的代码及注释内容要合法合规，不要有个人隐私信息](#35-正式发布的代码及注释内容要合法合规不要有个人隐私信息)|支持|
|[3.6 代码中包含禁止包含用户界面不可见、或是资料未公开的公网地址](#36-代码中包含禁止包含用户界面不可见或是资料未公开的公网地址)|不支持|
|[3.7 在多用户系统中创建文件时应根据需要指定合适的权限](#37-在多用户系统中创建文件时应根据需要指定合适的权限)|支持|
|[3.8 使用外部数据构造的文件路径前必须进行校验，校验前必须对文件路径进行规范化处理](#38-使用外部数据构造的文件路径前必须进行校验校验前必须对文件路径进行规范化处理)|不支持|
|[3.9 禁止使用tempfile.mktemp创建临时文件](#39-禁止使用tempfilemktemp创建临时文件)|支持|
|[3.10 临时文件使用完毕应及时删除](#310-临时文件使用完毕应及时删除)|支持|
|[3.11 解压文件必须进行安全检查](#311-解压文件必须进行安全检查)|不支持|
|[3.12 禁止使用pickle.load、_pickle.load和shelve模块加载外部数据](#312-禁止使用pickleload_pickleload和shelve模块加载外部数据)|不支持|
|[3.13 禁止序列化未加密的敏感数据](#313-禁止序列化未加密的敏感数据)|支持|
|[3.14 禁止使用yaml模块的load函数](#314-禁止使用yaml模块的load函数)|支持|
|[3.15 禁止使用jsonpickle模块的encode/decode或dumps/loads函数](#315-禁止使用jsonpickle模块的encodedecode或dumpsloads函数)|支持|
|[3.16 禁止使用eval和exec函数执行不可信代码](#316-禁止使用eval和exec函数执行不可信代码)|不支持|
|[3.17 禁止使用OS命令解析器或“危险函数”调用系统命令](#317-禁止使用os命令解析器或危险函数调用系统命令)|不支持|
|[3.18 避免在命令解析器中使用通配符](#318-避免在命令解析器中使用通配符)|支持|
|[3.19 禁止使用subprocess模块中的shell=True选项](#319-禁止使用subprocess模块中的shelltrue选项)|支持|
|[3.20 不受信任的外部数据禁止使用.format()进行格式化](#320-不受信任的外部数据禁止使用format进行格式化)|不支持|
|[3.21 禁止直接使用外部数据来拼接XML](#321-禁止直接使用外部数据来拼接xml)|支持|
|[3.22 禁止在处理XML数据时解析不可信的实体](#322-禁止在处理xml数据时解析不可信的实体)|支持|
|[3.23 禁止直接使用外部数据记录日志](#323-禁止直接使用外部数据记录日志)|支持|
|[3.24 禁止在生产版本的业务代码中使用assert](#324-禁止在生产版本的业务代码中使用assert)|支持|
|[3.25 将敏感对象发送出信任区域前进行签名并加密](#325-将敏感对象发送出信任区域前进行签名并加密)|支持|
|[3.26 安全场景下必须使用密码学意义上的安全随机数](#326-安全场景下必须使用密码学意义上的安全随机数)|支持|
|[3.27 必须使用ssl.SSLSocket代替socket.Socket来进行安全数据交互](#327-必须使用sslsslsocket代替socketsocket来进行安全数据交互)|支持|
|[3.28 禁止在用户界面、日志中暴露不必要信息](#328-禁止在用户界面日志中暴露不必要信息)|支持|