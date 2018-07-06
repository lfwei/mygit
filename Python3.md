## Python3

### 基础

####  数据类型：
* 整数：__int__
  * 1、100、-8080
  * 十六进制：十六进制用`0x`前缀和0-9，a-f表示，例如：`0xff00`，`0xa5b4c3d2`
* 浮点数：__float__
  * 数学写法：1.23、3.14、-9.01
  * 科学计数法：$1.23x10^9$就是1.23e9
* 字符串：__str__
  * \:转移字符
  * __\n__:换行
  * __\t__:制表符
    ```
      >>> print('/\t/')
      \    \
    ```
  * __r' '__:`''`内部的字符串默认不转义
    ```
      >>> print(r'\n\\\')
      \n\\\
    ```
  * __'''…'''__:多行
    ```
      >>> print('''a1
      ... a2
      ... a3''')
      a1
      a2
      a3
    ```
    ```
      >>> print(r'''a1,\nb
      ... a2
      ... a3''')
      a1,\nb
      a2
      a3
    ```
* 布尔值：__True/False__
  * 布尔运算：
    ```
      >>> 3 > 2
      True
      >>> 3 > 5
      False
    ```
  * __and/or/not__运算
    ```
      >>> True and False
      False
      >>> 5 > 3 or 1 > 3
      True
      >>> not 1 > 2
      True
    ```
  * 布尔值经常用在条件判断中，比如：
    ```
      if age >= 18:
          print('You are an adult')
      else:
          print('You are an teenager')
    ```
* 空值：__None__
  * `None`不能理解为`0`，因为`0`是有意义的，而`None`是一个特殊的空值
* 变量：变量名必须是`大小写英文`、`数字`和`_`的组合，且不能用数字开头
  * `=`是赋值语句，可以把任意数据类型赋值给变量，同一个变量可以反复赋值，而且可以是不同类型的变量
  * 变量在计算机内存中的表示(变量最终指向的是一个具体数据对象，不是指向另一个变量):
    ```
      >>> a = 'ABC'
      # python解释器做了两件事
        1. 在内存中创建一个'ABC'的字符串
        2. 在内存中创建一个名为`a`的变量，并把它指向'ABC'
    ```
* 常量：__通常用全部大写的变量名表示常量__
* 除法：
  * `/`:结果得到一个浮点数
  * `//`:取整，得到一个整数
  * `%`:取余，得到一个整数

#### 字符串编码
* 编码方式
  * ASCII编码：1个字节
  * Unicode编码：2个字节
  * UTF-8编码：1-6个字节（汉字3个字节）
* __在计算机内存中，统一使用Unicode编码，打需要保存到硬盘或者需要传输时转换成UTF-8编码__
* python3中，字符串是以Unicode编码
* __Python源代码是一个文本文件，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为UTF-8编码__
* __Python解释器读取源代码时，为了让它按UTF-8编码读取，我们通常在文件开头写上这两行：__
  ```
    #! /usr/bin/env python3
    # -*- coding:utf-8 -*-
  ```
####  __格式化字符串__
* 占位符：
  * `%d`:整数
  * `%f`:浮点数
  * `%s`:字符串
  * `%x`:十六进制整数
    ```
      >>> print('%5d;\n%05' % (3,8))
          3;                                   # 补空格，达到5位
      00008                                    # 补0，达到5位
    ```
    ```
      >>> print('%.3f' % 3.14159)
      3.141                                    # 取小数点后3位
    ```

#### list(有序列表，元素可以修改)
* 读取元素：
  ```
    >>> a = [3,4,5,'www','Bob']
    >>> a[0]
    3                                          # 第一个元素
    >>> a[-1]   
    'Bob'                                      # 最后一个元素
    >>> len(a)
    5                                          # a列表中总共有多少个元素 
  ```
* 追加元素：`append()/insert()`
  ```
    >>> a.append('M')                         # 追加元素'M'到末尾
    >>> a.insert(1,'QQ')                      # 追加元素'QQ'到索引号为1的位置
  ```
* 删除元素：`pop()`
  ```
    >>> a.pop()                               # 删除末尾元素
    >>> a.pop(1)                              # 删除索引号为1的元素
    >>> del a[1]                              # 删除索引号为1的元素
  ```
* 替换元素：
  ```
    >>> a[1] = '999'                          # 用'999'替换索引号为1的元素
  ```
* 二维数组
  ```
    >>> s = ['a','b',[3,4,'NB'],555,888]     # s可以看成是一个二维数组
    >>> s[2][1]
    4
    >>> len(s)
    5
  ```
#### tuple(元组，元素不可修改)
  ```
    >>> t = ()                              # 定义一个空的tuple
    >>> t
    ()
  ```
  ```
    >>> L = (3,)                           # 定义一个只有一个元素的tuple
    >>> L
    (3,)
  ```
* tuple __每个元素指向不变__
  ```
    >>> t = ('a', 'b', ['A', 'B'])
    >>> t[2][0] = 'X'
    >>> t[2][1] = 'Y'
    >>> t
    ('a', 'b', ['X', 'Y'])
  ```
  * 定义的时候tuple包含的3个元素：

    ![001](C:\Users\wlf\Desktop\20180112\001.png)

  * 当我们把list的元素`'A'`和`'B'`修改为`'X'`和`'Y'`后，tuple变为：

    ![002](C:\Users\wlf\Desktop\20180112\002.png)

  * 表面上看，tuple的元素确实变了，但其实变的不是tuple的元素，而是list的元素。__tuple一开始指向的list并没有改成别的list，所以，tuple所谓的“不变”是说，tuple的每个元素，指向永远不变__。即指向`'a'`，就不能改成指向`'b'`，指向一个list，就不能改成指向其他对象，但指向的这个list本身是可变的！

  * max/min():返回元组中最大最小值

#### if条件判断
* 根据Python的缩进规则，如果`if`语句判断是`True`，就把缩进的语句执行了
* `if`语句执行有个特点，它是从上往下判断，如果在某个判断上是`True`，把该判断对应的语句执行后，就忽略掉剩下的`elif`和`else`
  ```
    #! /usr/bin/env python3
    # _*_ coding:utf-8 _*_

    h = float(input('please your height(M):'))
    t = float(input('please your weight(Kg):'))
    bmi = t/(h*h)
    # 也可这样写：bmi = t/pow(h,2);bmi = t/(h**2)
    if bmi > 32 :
        print('BMI:%.1f;\nSevere obesity !' % bmi)
    elif bmi > 28 :
        print('BMI:%.1f;\nObesity !' % bmi)
    elif bmi > 25 :
        print('BMI:%.1f;\nOverweight !' % bmi)
    elif bmi > 18.5 :
        print('BMI:%.1f;\nNormalweight !' % bmi)
    else :
        print('BMI:%.1f;\nUnderweight !' % bmi)
  ```

  #### for...in...循环
* __for...in.../ range() /continue__
  ```
      a = input('a = ')
      b = input('b = ')
      m = int(a)
      n = int(b)
      sum = 0
      for t in range(m,n+1):
          if t % 2 == 0:
              continue
          print(t)
          sum = sum + t
      print(sum)
  ```

#### while 循环
* continue
  ```
    n = 0
    while n < 100:
        n = n + 1
        if n % 2 == 0:    # 如果n是偶数，执行continue语句
            continue      # continue语句会直接继续下一轮循环，后边的语句不会执行
        print(n)
  ```
* break
  ```
    n = 1
    while n <= 100
        if n > 10:              # 当n = 11时，条件满足，执行break语句        
            break               # break语句会结束当前循环 
        print(n)
        n = n + 1
    print('end')
  ```

