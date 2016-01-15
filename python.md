# Python学习笔记

## 开发环境搭建
```
使用brew安装pyenv和pyenv-virtualenv：
brew update
brew install pyenv
brew install pyenv-virtualenv

使用pyenv安装python：
pyenv install 3.4.3
pyenv install 2.7.10
新版本的python2和3都自带pip，所以无需再单独安装了。

配置环境：
在.profile文件中添加语句，用以配置pyenv和pyenv-virtualenv:
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

设置2.7.10版本为全局默认版本：
pyenv versions
pyenv global 2.7.10

创建虚拟环境：
pyenv virtualenv 3.4.3 venv
这个创建的venv目录在~/.pyenv/versions目录下

启动虚拟环境：
pyenv activate venv

使用pip安装包：
pip install tornado

退出虚拟环境：
pyenv deactivate
```

## Python 3字符编码
Python3中的所有string都是按照Unicode编码进行存储的。[Unicode码查询](http://unicode-table.com/en/)  

起初最流行的编码方式是ASCII，但它只有一个字节的长度，共256种可能，无法容纳所有中文字符。为了解决这个问题，出现了GB2312这种编码方式。  

同样的，很多国家都会有自己的一套甚至多套编码方式，去解决ASCII编码不能满足本国语言需求的问题。这样一来就造成了混乱，如果编码和解码方式不一致的话，就会出现乱码的现象。为了解决这个问题，出现了Unicode编码，它统一了编码规范。  

有了Unicode编码后，世界上所有符号都有与之对应的Unicode编码。但是字母数字等符号只需要一个字节表示，而中文字符通常需要3到4个字节。这样一来在解码的时候就会遇到问题，举个例：  
将一个包含3个字节的二进制数据解码成Unicode码，那么我们怎么知道这3个字节是整体表示一个中文字符呢，还是说每个字节分别表示一个英文字符。  
其实，最简单粗暴的解决方案就是：所有字符都统一使用4个字节来编码。但这样一来就大大的浪费了存储空间。为了解决这个问题，出现了UTF-8编码方式。  

UTF-8其实是Unicode编码规范的一种具体实现。它规定了Unicode编码在内存中按什么格式存储，从而方便判断到底几个字节表示一个具体的字符。  
![Unicode编码怎么转换成UTF-8编码](https://github.com/bitmonk404/learn_note/blob/master/imgs/unicode.png)

```python
aa = '严'
bb = "\u4E25"
bb # '严'

cc = aa.encode('utf-8')
cc # b'\xe4\xb8\xa5'

# 1、Python3中，所有str类型的数据都按照Unicode编码进行存储。
# 2、Python3中，可以通过encode的方法对Unicode数据(即str类型的数据)进行转换，转换为UTF-8(即bytes类型)的数据。
# 3、同理，也可以通过decode对bytes类型的数据解码，还原成str类型的数据。
# 4、总结，简单的说就是：在Python3中所有str类型数据都按照Unicode编码方式进行存储；所有bytes类型数据都按照UTF-8编码方式进行存储。
```

## Python 2字符编码
在Python2中，字符串有两种格式，分别是：str、unicode。它们都继承自basestring类。

```python
# 用这种方式，无论实参是str还是unicode类型，它都能通过basestring进行判断。
def is_str(s):
    return isinstance(s, basestring)
```

#### 赋值
```python
str_test = '你好'
unicode_test = u'你好'

str_test # '\xe4\xbd\xa0\xe5\xa5\xbd'
print str_test # 你好
isinstance(str_test, str) # True

unicode_test # u'\u4f60\u597d'
print unicode_test # 你好
isinstance(unicode_test, unicode) # True
```

#### 编码和解码
```python
# str类型通过decode，解码成unicode类型。
# unicode类型通过encode，编码成str类型。
res1 = str_test.decode('utf-8')
res2 = unicode_test.encode('utf-8')

res1 # u'\u4f60\u597d'
print res1 # 你好
type(res1) # unicode

res2 # '\xe4\xbd\xa0\xe5\xa5\xbd'
print res2 # 你好
type(res2) # str
```

#### 提示
```python
# 如果元数据是：非utf-8编码的str类型，需要转换成utf-8编码的str类型。
# 可以使用unicode类型作为中间人进行转换。
test = '么么哒' # 假设它是code
res = test.decode('gb2312').encode('utf-8')

# 如果原数据是：带有\u，即unicode记法的str类型，需要转换为能够显示为中文的正常utf-8的str类型。
# 其实思路和上面一样，都是先decode为标准的unicode类型，然后再encode为utf-8类型。
test = '\u4fee\u6539'
test2 = '\\u4fee\\u6539'

res1 = test.decode('unicode_escape').encode('utf-8')
res2 = tets.decode('unicode_escape').encode('utf-8')

res1 # '\xe4\xbf\xae\xe6\x94\xb9'
res2 # '\xe4\xbf\xae\xe6\x94\xb9'
print res1 # 修改
print res2 # 修改
```

## 正则表达式
#### 常用函数match()  search()  findall()  split()  sub()
```python
import re
source = 'Young Frankenstein'

#match()
m = re.match('You', source) 
if m: 
    print(m.group()) # You

m = re.match('^You', source) 
if m:
    print(m.group()) # You

m = re.match('Frank', source)
if m:
    print(m.group()) # 什么都不会匹配到，因为match只会从一开始匹配。

# search()
m = re.search('Frank', source)
if m:
    print(m.group()) # Frank   不同于match，用search就可以匹配到。

m = re.match('.*Frank', source)
if m:
    print(m.group()) # Young Frank

# findall()
m = re.findall('n', source)
m # ['n', 'n', 'n', 'n']
print('Found', len(m), 'matches') # Found 4 matches

m = re.findall('n.', source)
m # ['ng', 'nk', 'ns']

m = re.findall('n.?', source)
m # ['ng', 'nk', 'ns', 'n']

# split()
m = re.split('n', source)
m # ['You', 'g Fra', 'ke', 'stei', '']

# sub()
m = re.sub('n', '?', source)
m # 'You?g Fra?ke?stei?'
```

#### 特殊字符
```python
'''
\d 整型  
\D 不是整型的任意字符  
\w 字符(字母、数字、下划线)  
\W 不是字符的任意字符  
\s 空白符(空格、制表符、换行符等等)  
\S 不是空白符  
\b 分隔符，在\w和\W之间。  
\B 不是分隔符
'''

import string
printable = string.printable
len(printable) # 100
printable[0:50] 
# '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMN'
printable[50:] 
# 'OPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'

re.findall('\d', printable)
# ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']

re.findall('\w', printable)
'''
['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b',
 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n',
 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z',
 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L',
 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X',
 'Y', 'Z', '_']
'''

re.findall('\s', printable)
# [' ', '\t', '\n', '\r', '\x0b', '\x0c']

x = 'abc' + '-/*' + '\u00ea' + '\u0115'
re.findall('\w', x)
# ['a', 'b', 'c', 'ê', 'ĕ']
# 注意：正则表达式的\w不是针对ASCII编码的字符设计的。而是针对Unicode编码设计的。所以'ê', 'ĕ'这两个Unicode字符也会被匹配出来。
```

#### 模式匹配符号
```python
'''
|   或  
.   任意字符，不包括\n  
^   开始符号  
$   结束符号  
?   0个或1个。  
*   0个或多个，贪婪模式。  
*?  0个或多个，非贪婪模式。  
+   1个或多个，贪婪模式。  
+?  1个或多个，非贪婪模式。  
{m} m个  
{m, n} m到n个，贪婪模式。  
{m, n}? m到n各，非贪婪模式。  
[abc]  a或b或c  
[^abc] 不是a或b或c中的任意一个。  
a(?=b)  匹配的是a，这个a后面必须跟着一个b。  
a(?!b)  匹配的是a，这个a后面不能跟着b。  
(?<=a)b 匹配的是b，这个b前面必须是a。  
(?<!a)b 匹配的是b，这个b前面不能是a。
'''

source = '''I wish I may, I wish I might
    Have a dish of fish tonight.'''

re.findall('wish', source) # ['wish', 'wish']

re.findall('wish|fish', source) # ['wish', 'wish', 'fish']

re.findall('^wish', source) # []

re.findall('^I wish', source) # ['I wish']

re.findall('fish$', source) # []

re.findall('fish tonight.$', source) 
# ['fish tonight.']
# 注意末尾的.在正则里是模式匹配符号，而不是字符串的句号。所以它在这里表示任意一个符号，那么句号当然也属于任意一个符号，所以匹配到了。

re.findall('fish tonight\.$', source)
# ['fish tonight.']
# 虽然结果和上例一样，但是这里的使用更精确，它就是要去匹配句号。

re.findall('[wf]ish', source)
# ['wish', 'wish', 'fish']

re.findall('[wsh]+', source)
# ['w', 'sh', 'w', 'sh', 'h', 'sh', 'sh', 'h']

re.findall('ght\W', source)
# ['ght\n', 'ght.']

re.findall('I (?=wish)', source)
# ['I ', 'I ']

re.findall('(?<=I) wish', source)
# [' wish', ' wish']

re.findall('\bfish', source)
# []
# 本来应该匹配到['fish']的，但为什么是空呢？
# 因为这里的\b在字符串中表示退格，而字符串的转义是优先于正则的特殊符号的。

re.findall(r'\bfish', source)
# ['fish']
# 这样就能成功匹配到了。

m = re.search(r'(. dish\b).*(\bfish)', source)
m.group() # 'a dish of fish'
m.groups() # ('a dish', 'fish')

m = re.search(r'(?P<DISH>. dish\b).*(?P<FISH>\bfish)', source)
m.group() # 'a dish of fish'
m.groups() # ('a dish', 'fish')
m.group('DISH') # 'a dish'
m.group('FISH') # 'fish'
```