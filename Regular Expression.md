
# Python 正则表达式

## [官方文档](https://docs.python.org/3/library/re.html#module-re)

* 准备文本：zen of python


```python
import this
import re

text = '''
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
'''
```

## 模糊匹配

1. `.` 表示任意一个除了"\t与\n"的字符

eg:

- 所有以i字母开头，长度为2的字符串


```python
r = re.findall('i.',text)
print(*r)  #星号解包
```

    im if is ic it is im ic it im is is ic is is il it ia ia ic it it il ic it il ig it io io it io ir is is ig im io is in it id im io is in it id in id
    

2. `[a,b,c]` 匹配\[  \]内的任意一个字符

    - `[0 -9]` 表示数字

    - `[a-z]` 表示字母

eg：

- 所有的is，if，和it 包括大写


```python
r = re.findall('i[s,f,t]',text,re.I)
print(*r)
```

    if is it is it is is is is it it it it it it is is If is it If is it
    

3. `*` 匹配任意多个字符

eg：

- 包含任意多个is的字符串： (is)*


```python
r = re.findall('(is)*',text)
print(*r)
```

                                                 is                             is                               is                               is                                is                             is                                                                                                                                                                                                                                                                                                                                                                                                           is                                    is                                                       is                                                          is                                                                                                           
    

4. `+` 匹配一个以上的字符

eg：

- 包含至少一个is的字符串：（is）+


```python
r = re.findall('(is)+',text)
print(*r)
```

    is is is is is is is is is is
    

## 精确匹配

1. 直接 `'匹配内容'` 即可

eg:

- 匹配 'perfect'


```python
r = re.findall('perfect',text)
print(*r)
```

    
    

## 常用 RE 规则

| 模式 | 描述 |
| ---- | ---- |
| `\d` | [0-9] |
| `\D` | [^-9] |
| `\w` | [a-zA-Z0-9_] |
| `\W` | [^a-zA-Z0-9_] |
| `\s` | [\t\n\r\f] |
| `\S` | [^\t\n\r\f] |
| `^` | 以字串开头 |
| `$` | 以字串结尾 |
| `.` | 任意一个除了"\t与\n"的字符 |
| `[...]` | 匹配[ ]内的任意一个字符 |
| `[^...]` | 匹配不在[ ]内的任意一个字符 |
| `*` | 匹配任意多个前面表达式 |
| `+` | 匹配至少一个前面表达式 |
| `?` | 匹配0或1个前面表达式，也可以用来表示非贪婪方式 |
| `{n}` | 精确匹配 n 个前面表达式 |
| `{n, m}` | 匹配 n 到 m 次由前面的正则表达式定义的片段，贪婪方式 |
| `a | b` | 匹配 a 或 b |
| `( )` | 匹配括号内的表达式，也表示一个组 |

## RE库常用函数

| 库里常用函数 | 描述 |
| ---- | ---- |
| `re.match(pattern, string, flags=0)` | 尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，match()就返回none |
| `re.search(pattern, string, flags=0)` | 扫描整个字符串并返回第一个成功的匹配 |
| `re.sub(pattern, repl, string, count=0)` | 用于替换字符串中的匹配项，repl : 替换的字符串，也可为一个函数 |
| `re.compile(pattern[, flags])` | 用于编译正则表达式，生成一个正则表达式（ Pattern ）对象，供 match() 和 search() 这两个函数使用 |
| `findall(string[, pos[, endpos]])` | 在字符串中找到正则表达式所匹配的所有子串，并返回一个列表，如果没有找到匹配的，则返回空列表 |
| `re.split(pattern, string[, maxsplit=0, flags=0])` |  能够匹配的子串将字符串分割后返回列表 |

## flags 修饰符

| 修饰符 flags | 描述 |
| ---- | ---- |
| `re.I` | 使匹配对大小写不敏感 |
| `re.L` | 做本地化识别（locale-aware）匹配 |
| `re.M` | 多行匹配，影响 ^ 和 $ |
| `re.S` | 使 `.` 匹配包括换行在内的所有字符 |
| `re.U` | 根据Unicode字符集解析字符。这个标志影响 \w, \W, \b, \B. |
| `re.X` | 该标志通过给予你更灵活的格式以便你将正则表达式写得更易于理解。 |

- 最后这几个用的不多，日后用到详细钻研后再补充
