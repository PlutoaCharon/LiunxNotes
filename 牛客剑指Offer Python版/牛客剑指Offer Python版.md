[toc]

# 牛客网剑指Offer Python版



## 字符串

### [1.  替换空格](https://www.nowcoder.com/practice/4060ac7e3e404ad1a894ef3e17650423?tpId=13&tqId=11155&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

```txt
请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。
```

1. 循环替换

```python
# -*- coding:utf-8 -*-
class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        ans = ''
        for i in s:
            if i == ' ':
                ans += '%20'
            else:
                ans += i
                
        return ans
```

2. 直接替换

   ```python
   # -*- coding:utf-8 -*-
   class Solution:
       # s 源字符串
       def replaceSpace(self, s):
           # write code here
           return s.replace(" ","%20")
   ```

   

3. 正则表达式

```python
import re
class Solution:
    def replaceSpace(self, s):
        # write code here
        s=re.sub(r" ","%20",s)
        return s
```

### 2. [正则表达式匹配](https://www.nowcoder.com/practice/45327ae22b7b413ea21df13ee7d6429c?tpId=13&tqId=11205&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

1. float函数加try模块

```python
import re
# -*- coding:utf-8 -*-
class Solution:
    # s字符串
    def isNumeric(self, s):
        # write code here
        try :
            p = float(s)
            return True
        except:
            return False
```

2. re正则表达式

Python正则表达式 `()?`表示捕获型分组， `group(0)` 表示匹配的第一个分组`[\+-]?[0-9]*(\.[0-9]*)?` 或者`[\+-]?[0-9]*([eE][\+-]?[0-9]+)?`

```python
# -*- coding:utf-8 -*-
import re
class Solution:
    # s字符串
    def isNumeric(self, s):
        # write code here
        a=re.match(r"[\+-]?[0-9]*(\.[0-9]*)?([eE][\+-]?[0-9]+)?",s)
        if a.group(0)==s:
            return True
        else:
            return False
```

