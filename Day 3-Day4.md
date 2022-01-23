# Day 3 -Day4

## Python基础语法



+ 数据类型(上面是不可变数据，下面是可变数据)

  + 数字(整型，浮点型，布尔型，复数)

  + 字符串(元组的一种，用于索引、切片、乘法-多次输出、成员资格检查、长度len()、最大值、最小值)

  + 元组((),元素不可修改)

    +++

    

  + 列表([],增删改，)

  + 集合

    > - set 是一个无序不重复元素的序列
    > - 使用大括号 { } 或者 set() 函数创建集合
    > - 用 set() 创建一个空集合
    > - 使用 set 可以去重

  + 字典

> - 字典的每个元素是键值对，无序的对象集合
> - 字典是可变容器模型，且可存储任意类型对象
> - 字典可以通过键来引用，键必须是唯一的且键名必须是不可改变的（即键名必须为Number、String、元组三种类型的某一种），但值则不必
> - 字典是使用 { } 大括号包含键值对
> - 创建空字典使用 { }



+ 循环语句

  1.循环控制语句

  + break语句

       （ 在语句块执行过程中终止循环，并且跳出整个循环）

    + continue语句

      ​    在语句块执行过程中终止当前循环，跳出该次循环，执行下一次循环。

      + pass语句

        ​    pass是空语句，是为了保持程序结构的完整性。



2.for循环语句

> for循环使用的语法:
> for 变量 in 序列:
>     循环要执行的动作

例如range：

```python
range(stop): 0 - stop-1
range(start,stop): start - stop-1
range(start,stop,step): start - stop-1 step(步长)
```

```python
for item in range(5):
    print(item)
print('\n')
 
for num in range(10,15):
    print(num)
print('\n')
 
for a in range(20,30,2):
    print(a)
```



3.while循环

> while 条件():
>     条件满足时，做的事情1
>     条件满足时，做的事情2

```python
i = 0
result = 0
 
while i <= 100:
    result += i
    i += 1
print('1+2+3+...+100的和为:%d' %result)
```



如果while的条件恒为真时，那就是一个死循环:

```python
while True:
    print('Hello world！')
```



4.while嵌套

例如打印九九乘法表：

```python
row = 1
while row <= 9:
    col = 1
    while col <= row:
        print('%d * %d = %d\t' %(row,col,col * row),end='')
        col += 1
    print('')
    row += 1
```



+ 函数

  ```python
  def 函数名([参数，参数……]):
      代码
      return
  
      #使用def开始函数定义，紧接着是函数名，括号内部为函数的参数，内部为函数的具体功能实现代码，return结束函数
  ```

  (被定义的参数是形参，被调用的参数是实参)

1.参数

> 以下是调用函数时可使用的正式参数类型：
>
> - 必备参数(须以正确的顺序传入函数。调用时的数量必须和声明时的一样)
> - 关键字参数(函数调用使用关键字参数来确定传入的参数值,使用关键字参数允许函数调用时参数的顺序与声明时不一致)
> - 默认参数(调用函数时，默认参数的值如果没有传入，则被认为是默认值)
> - 不定长参数(有时可能需要一个函数能处理比当初声明时更多的参数, 这些参数叫做不定长参数，声明时不会命名。)

不定长参数基本语法：

```python
def functionname([formal_args,] *args, **kwargs):
   """函数_文档字符串"""
   function_suite
   return [expression]

```

> 注意：
> 加了星号（*）的变量args会存放所有未命名的变量参数，args为元组
> 而加**的变量kwargs会存放命名参数，即形如key=value的参数， kwargs为字典.



2.匿名函数(lambda)

> - lambda只是一个表达式，函数体比def简单很多。
> - lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
> - lambda函数拥有自己的命名空间，且不能访问自有参数列表之外或全局命名空间里的参数。
> - 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率.

```python
lambda [arg1 [,arg2,.....argn]]:expression
```



3.return语句(退出函数，选择性地向调用方返回一个表达式。不带参数值的return语句返回None。)

```python
# 可写函数说明
def sum( arg1, arg2 ):
   # 返回2个参数的和."
   total = arg1 + arg2
   print "函数内 : ", total
   return total
 
# 调用sum函数
total = sum( 10, 20 )
```



4.全局变量和局部变量

> 定义在函数内部的变量拥有一个局部作用域，定义在函数外的拥有全局作用域。
>
> 局部变量只能在其被声明的函数内部访问，而全局变量可以在整个程序范围内访问。调用函数时，所有在函数内声明的变量名称都将被加入到作用域中。

```python
total = 0 # 这是一个全局变量
# 可写函数说明
def sum( arg1, arg2 ):
   #返回2个参数的和."
   total = arg1 + arg2 # total在这里是局部变量.
   print "函数内是局部变量 : ", total
   return total
 
#调用sum函数
sum( 10, 20 )
print "函数外是全局变量 : ", total
```

```python
函数内是局部变量 :  30
函数外是全局变量 :  0
```





+ 模块

  > Python 模块(Module)，是一个 Python 文件，以 .py 结尾，包含了 Python 对象定义和Python语句。
  >
  > 模块让你能够有逻辑地组织你的 Python 代码段。
  >
  > 把相关的代码分配到一个模块里能让你的代码更好用，更易懂。
  >
  > 模块能定义函数，类和变量，模块里也能包含可执行的代码。

1.导入模块可以利用import，as这两个关键字来实现。

> 常见的 **import** 导入语句可以分为两种：单独的 import 语句用来导入模块名；
>
> 带有from 的 import 语句用来导入模块中的变量名，同时可以使用 `*` 号导入模块中的所有变量.
>
> 在以上两种语句中，我们都可以使用 **as** 语句为导入的模块或变量指定别名。当语句包含多个子句（以逗号分隔）时，为每个子句分别执行模块导入的三个步骤，就像子句已被分隔为单独的 import 语句一样。

2.import形式

import 语句将模块导入文件中：

```python
import module_name
```

> 一旦导入完成，一个模块的属性（函数和变量）可以通过熟悉的 （. ）句点属性标识法访问。
>
> module.function()
>
> module.variable

3.from - import 形式

使用 from-import 语句可以将模块的属性导入到当前作用域，并绑定到指定的变量名.

```python
from module import name1[, name2[,... nameN]]
```

> 和 reload 调用同时使用时，from 语句有比较严重的问题，因为导入的变量名可能引用之前导入的对象。
>
> 简单模块一般倾向于使用 import，而不是 from。多数的 from 语句是用于明确列举出想要的变量，而且限制在每个文件中只用一次 from * 形式。当你必须使用两个不同模块内定义的相同的变量名时，才真的必须使用 import，这种情况下不能用 from（当然你可以在 from 语句中使用 as 语句来个规避变量名冲突的问题）。

4.from - import * 形式

从一个模块导入许多变量名时，import 行会越来越长，直到自动换行，而且我们需要使用反斜杠字符 ``让一条语句横跨多行 。

```python
from module import name1, name2, name3, name4, ame5, name6, name7
```

5.扩展的导入语句（as）

> 使用扩展的 **as** 子句，你就可以在导入的同时指定局部绑定名称。
>
> 这个扩展功能很常用，替代变量名较长的变量提供简短一些的同义词，而且当已在脚本中使用一个变量名使得执行普通 import 语句会被覆盖时，使用 as，就可避免变量名冲突。

```python
import modulename as name相当于：
import modulenamename = modulenamedel modulenamefrom modulename 

import attrname as name相当于：
from modulename import attrnamename = attrnamedel attrname

```





## 数学



1.

+ 线性方程组(齐次，非齐次)，

+ 矩阵运算(二三四阶)，

+ 求逆(AB=E),

+ 秩(把某一行全部化成0，剩下的行数的数值即为秩)，

+ 协方差(衡量两个变量的总体误差),

+ 特征值(设A 是n阶方阵，如果存在数m和非零n维列向量 x，使得Ax=mx 成立，则称m 是矩阵A的一个特征值（characteristic value)或本征值（eigenvalue)。)

+ 特征向量(线性变换的特征向量是指在变换下方向不变，或者简单地乘以一个缩放因子的非零向量。

  特征向量对应的特征值是它所乘的那个缩放因子。)

2.常见距离

+ 欧氏距离(在n维空间中两个点的真实距离)![欧氏距离公式](https://img-blog.csdnimg.cn/2020070323443076.png)

+ 闵氏距离(一组距离)

  ![img](https://img-blog.csdnimg.cn/img_convert/9f535fb75ad4b4a50cad779f9bd01f27.png)

+ 余弦值相似性

  > 其他距离直接测量两个高维空间上的点的距离，如果距离为0则两个点“相同”；
  >
  > 余弦的结果为在[0，1]之中，如果为 1，只能确定两者完全相关、完全相似.



![在这里插入图片描述](https://img-blog.csdnimg.cn/20200703235330209.png)

3.中心化

+ Min-Max标准化

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200114123120129.png)

+ Box-Cox转换

  (引入一个参数，通过数据本身估计该参数进而确定应采取的数据变换形式，Box-Cox变换可以明显地改善数据的正态性、对称性和方差相等性，)



4.统计知识

+ t检验

  > 用于小样本（ 样本容量 小于30）的两个平均值差异程度的检验方法。
  >
  > 它是用T分布理论来推断差异发生的概率，从而判定两个平均数的差异是否显著。

+ f检验

  > 在零假设之下，统计值服从F-分布的检验.
  >
  > 通常用来在不知道两个总体的均值，但知道其中某个方差的情况下，假设另一方差（F检验），即是否具有统计意义。
  >
  > 在两样本t检验中要用到F检验。
  >
  > 从两研究总体中随机抽取样本，要对这两个样本进行比较的时候，首先要判断两总体方差是否相同，即方差齐性。若两总体方差相等，则直接用t检验。



![F=\frac{s_1^2/{\sigma_1}^2}{s_2^2/{\sigma_2}^2} \rightarrow F(n_1-1,n_2-1)](https://math.jianshu.com/math?formula=F%3D%5Cfrac%7Bs_1%5E2%2F%7B%5Csigma_1%7D%5E2%7D%7Bs_2%5E2%2F%7B%5Csigma_2%7D%5E2%7D%20%5Crightarrow%20F(n_1-1%2Cn_2-1))

+ 正态检验

> 利用观测数据判断总体是否服从正态分布的检验称为正态性检验，它是统计判决中重要的一种特殊的拟合优度假设检验.

设![img](https://bkimg.cdn.bcebos.com/formula/4634a17efc552e6de3d4912ac077e26d.svg)。表示来自总体的样本，![img](https://bkimg.cdn.bcebos.com/formula/1158fdb8066eda341952378f7236a8a0.svg)表示 i 阶样本中心矩。正态分布的偏度和峰度均为 0，其中偏度和峰度的定义分别为:

![img](https://bkimg.cdn.bcebos.com/formula/a531d7cf3ad81ba81763ce548175b9b7.svg)



该检验就是根据这个特点来检验分布正态性的。



+ 卡方检验

  > 卡方检验就是统计样本的实际观测值与理论推断值之间的偏离程度，实际观测值与理论推断值之间的偏离程度就决定卡方值的大小，如果卡方值越大，二者偏差程度越大；反之，二者偏差越小；若两个值完全相等时，卡方值就为0，表明理论值完全符合。
  >
  > 注意：卡方检验针对分类变量。

卡方检验的计算公式为：

![img](https://imgconvert.csdnimg.cn/aHR0cDovL2ltYWdlcy5jbml0YmxvZy5jb20vYmxvZy81MDI5MzAvMjAxMzEwLzE0MjAyMzQ2LWI1NzQyY2FjYjY0YzRmNGQ4ZDA3YWQ2MzgxNzllNDcxLmpwZw?x-oss-process=image/format,png)

其中，A为实际值，T为理论值。

x*2用于衡量实际值与理论值的差异程度（也就是卡方检验的核心思想），包含了以下两个信息：

a. 实际值与理论值偏差的绝对大小（由于平方的存在，差异是被放大的）
b. 差异程度与理论值的相对大小



+ 最小二乘法(误差估计、不确定度、系统辨识及预测、预报等数据处理)

![一次函数的最小二乘法](https://img-blog.csdnimg.cn/c1f2d62d76604e588f4a238ef88bdd77.bmp?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAUG9sYXJpc19U,size_20,color_FFFFFF,t_70,g_se,x_16)



![高次函数的最小二乘法](https://img-blog.csdnimg.cn/9c063bb680c045d2bcd26eea3ae2f0bb.bmp?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAUG9sYXJpc19U,size_20,color_FFFFFF,t_70,g_se,x_16)





## 机器学习

#### KNN算法

+ 简单阐述

  > 1.计算测试数据与训练数据之间的距离
  >
  > 2.按照距离的从小到大的关系进行排序
  >
  > 3.选取距离最小的k个点
  >
  > 4.统计前k个点所在类别的出现频率
  >
  > 5.返回前k个点中 出现频率最高的类别作为测试数据的预测分类。

! [公式1](https://img-blog.csdnimg.cn/20201116151845761.png)

+ 算法流程

> 将每个样本视作一个点
> 1. 载入数据集，对数据进行必要的预处理
>
> 2. 设置参数K，K最好选择奇数，因为后续进行归类的策略是少数服从多数，设置K为奇数的话总会有结果。
>
> 3. 计算待预测点与已知点之间的关系，这里的关系可以有多种方式来体现，常用如下：
>   ①欧式距离（应用较广，其他及其算法也有广泛应用），其计算方法：
> ! [公式2](https://img-blog.csdn.net/20180907235325606?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzA4NDkyOA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
>
> ②余弦值
>   ③相关度
>   ④曼哈顿距离
>   ⑤…
>   
>   4. 之前确定了参数K，计算了待预测点与已知点之间的距离衡量，将计算的结果进行从小到大排序，取前K个点
>      5. 将待预测点归类为多数的那一个类别，这便是对于未知点的类别预测结果

(离未知点越近的，权重大，对结果贡献度大，反之离未知点远的，权重小，对结果的贡献度小.)