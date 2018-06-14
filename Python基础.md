# Python基础

## 数据类型和变量

### 数据类型

+ 整数

  + 0x开头表示十六进制，比如0xff00,表示范围无限大

+ 浮点数，表示范围无限大

+ 字符串：

  + 用`''`或`""`括起来的任意文本

  + `\`转义

  + `\n`换行

  + 为了简化，Python允许用`'''...'''`格式来表示多行内容

    ```python
    print('''line1
    ...line2
    ...line3''')
    //输出
    line1
    line2
    line3
    ```

    ​

+ 布尔值：只有两种值`True`，`False`,首字母大写

+ 空值：一个特殊的值，用`None`表示

### 变量

​	Python是一种动态语言，变量本身类型不固定，在定义变量时不需要指定变量类型

### 常量

​	本没有常量，只不过人们约定不去改它，一般声明全用大写字母。

```python
PI=3.1415
/**PI是可以改的，只不过人们约定全部大写的不去改*/
```

### 精确的除法

	#### 一般除法

`/`得到的永远是浮点数

#### 整除除法

`//`得到是整数部分

```python
>>> 10//3
3
```

#### 取余

```python
>>> 10%3
1
```

## 字符串和编码

### ASCLL

美国人发明，只有127个字符，不注意表示全球多种语言

### Unicode

世界大同，英文需要一个字符就够了，但是为了一致，在前面补`00000000`，所以每个字符都是两个字节，这样有点浪费

### UTF8

将Unicode编码转为可变长编码`UTF-8`，常用英文字母只需要一个字节，汉字通常需要3个字节，只有很生僻的字符才会被编码成4-6个字节。如果传输的文本包含大量的英文字符，用utf-8就很能节省空间。

这样有一个好处，Ascll码的软件可以在utf-8编码下继续工作

### Python中字符串

在Python 3中，字符串是以Unicode编码的，所以Python的字符串支持多语言。

+ 对于单个字符的编码，Python提供了`ord()`函数来获取字符的整数表示,`chr()`把对应的编码转为对应的字符

```python
>>> ord('A')
65
>>> chr(66)
'B'
```

+ `str`和`bytes`

```python
# str通过调用encode()方法，可以编码为指定的bytes
>>> 'ABC'.encode('ascii')
b'ABC'
>>> '中文'.encode('ascii')
# 报错，因为中文在ASCII中没有编码
# bytes通过调用decode()转化为str
>>>b'ABC'.decode('ascii')
'ABC'
# 如果bytes中包含一小部分无效的字节，可以传入`errors=ignore`忽略错误字节
>>>b'ABC'.decode('utf-8',errors='ignore')
```

+ `len()`

计算字符串`str`的字符数，如果换成`bytes`,`len()`函数就会计算字节数

```python
>>>len('aBC')
3
>>>len('中文'.encode('utf-8'))
6
```

+ python代码中的编码

```python
#!/usr/bin/env python3    //告诉linux/os
# -*- coding: utf-8 -*-   //告诉Python解释器，按照utf_8编码读取源码
```

### 字符串格式化输出

类似于c语言，通过`%`来实现,通过`%.2f`来指定浮点数的位数(四舍五入)

| 占位符 | 替换内容     |
| ------ | ------------ |
| %d     | 整数         |
| %f     | 浮点数       |
| %s     | 字符串       |
| %x     | 十六进制整数 |

```python
>>>'Hello, %s' % 'world'
'hello, world'
>>> 'Hi,%s,you hava $%d.' % ('weberlee',10000)
'Hi,weberlee,you hava $10000'
>>>print('%.2f' % 3.12232)
3.12
```

## 使用list和tuple

### list

```python
>>> classmates=['a','b','c']
>>> classmates
['a','b','c']
>>> len(classmates)
3
>>> classmates[0]
'a'
>>> classmates[-1]
# 得到最后一个，[-2]得到倒数第二个
# 插入元素到指定位置，比如索引号为1的位置
>>> classmates.insert(1,'Jack')
>>> classmates
['a','jack','b','c']
# 删除list末尾元素 pop()
>>> classmates.pop()  返回被删除元素
'c'
>>> classmates
['a','jack','b']
# 删除指定位置的元素 pop(i) 、、索引位置
>>> classmates.pop(1)
['a','b']
```

`list`中元素可以不同类型，也可以list嵌套

### tuple



另一种有序列表叫元组：`tuple`。它和list十分类似，但是`tuple`一旦初始化就不能修改。不能修改其中数据的地址。要是元组中有list，可以修改list内容，只要其地址指向不变

```python
>>>t=('a','b','c')
>>> t
('a','b','c')
# 只定义一个元素时，要用到,
>>> t=(1,)
>>> t
(1,)

>>> t=([1,2,3],'c')
>>> t[0][1]
2
>>> t[0]='a'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

## 条件判断

```python
s=input('bmi:')
bmi=int(s)
if bmi<18.5:
    print('过轻')
elif bmi<25:
    print('正常')
elif bmi<28:
    print('过重')
elif bmi<32:
    print('肥胖')
else:
    print('严重肥胖')
```

## 循环

### `for item in list`

​	Python提供了一个for in 循环。Python提供了一个`range()`函数，可以生成一个整数序列，再通过`list()`函数将其转换为list,这样就可以用于for in循环。

```python
sum=0
for item in list(range(101)):
    sum=sum+item
print(sum)
```

### while循环

```python
sum=0
n=99
while n>0:
    sum=sum+n
    n=n-2
print(sum)
```

### break&&continue

+ break用于跳出循环
+ continue用于跳过本次循环

## dict和set

### dict

类似于其他语言的map，使用键值对(key-value)存储，查找速度极快

```python
d={'a':100,'b':11,'c':34}  
d['a']//100
```

`一个key只能对应一个value`，所以当多次存入一个key的时候，后面的值会被前面值冲掉

为了避免key不存在的情况，有两种方法避免

+ in方法判断

```python
>>> 'd' in d
False
```

+ 通过`get()`方法，如果key不存在，返回None,或者自己指定的value

```python
>>>d.get('d')
#返回空
```

`删除`元素，一个key，用`pop(key)`方法，对应的value也会被删除,返回删除value

```python
>>> d.pop('c')
34
```

### dict和list比较

#### dict

+ 查找和插入速度快，不会随着key的增加而变慢
+ 占用大量内存，浪费多
+ 空间换时间

#### list

+ 查找和插入的时间随着元素的增加而增加
+ 占用内存小，浪费少
+ 时间换空间

### set

类似于dict，但是只能存储key，不存储value。但是key不能重复，所以set中没有重复元素。

```python
>>> d=set([1,2,3,4,5,6,5,6,5])
>>> d
{1, 2, 3, 4, 5, 6}
```

添加元素`add(key)`重复会没用

```python
>>> d.add(9)
>>> d
{1, 2, 3, 4, 5, 6, 9}
```

删除元素`remove(key)`

```python
>>> d.remove(1)
>>> d
{2, 3, 4, 5, 6, 9}
>>> d.remove(8)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 8
### 删除不存在的key报错
```

set可以看成数学上的无序无重复元素的集合，所以两个set可以进行交集，并集等操作

```python
>>> s1=set([1,2,3])
>>> s2=set([2,3,4])
>>> s1&s2    并集
{2, 3}
>>> s1|s2    交集
{1, 2, 3, 4}
>>> s1^s2    补集
{1, 4}
```

