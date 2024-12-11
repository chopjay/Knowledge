变量和字符串

```
变量名：由"字母","数字"和"下划线"构成，不能以数字开头 ; 但中文可以作为变量名(不建议)

变量的值可以被替换，变量的值是多少，取决最后一次赋值操作

python使用"字符串"来表示"文本序列"
字符串的编写方式主要有三种:
	--Single quotes: 用一对单引号将文本括起来
	--Double quotes: 用一对双引号将文本括起来
	--Triple quotes: 
	==区别：没啥区别,主要确保文本两边的引号都应该成双成对

转义字符：用来表示一些不能直接显示的SASCII字符
		\\ 反斜杠		\' 单引号		 \b 退格符		
		\n 换行符		\t 水平制表符	\v 垂直制表符
		\r 回车符		\f 换页符		 \ooo ooo为八进制数		\xhh hh为十六进制数
		
字符串的加法和乘法
字符串相加称为"拼接"：'520' + '1314' output  '5201314' 
字符串相乘称为"复制"： '520' * 2  output  '520520'
```

数字类型

```
数字类型有三种："整数"、"浮点数"和"复数"
	--小数以浮点数的形式存放
	--python和C存放采用的标准相同，在需求精准领域时，可用decimal模块种的Decimal进行赋值运算
	--E记法：科学计数法，比如 5e-05 即 5乘10的负5次方
	--复数：分为实部和虚部，以浮点数形式存放，例如 1+2j  j表示虚部 
			x=1+2j   x.real获取实部数值   x.imag获取虚部数值
```

![image-20241009144942499](C:\Users\12774\AppData\Roaming\Typora\typora-user-images\image-20241009144942499.png)

```
地板除：确保两个数相除是一个整数，不是整数就向下取整(即 取比目标结果小的最大整数)
divmod：作用是 同时求出两参数地板除的结果和余数的值
复数取绝对值abs,返回的结果是复数的模
```

布尔类型

```
bool()   返回的结果是"True"或"False"
只有等值为0才会输出Flase，其他皆为True
Flase的情况
	--定义为False的对象：None和False
	--值为0的数字类型：0, 0.0, 0j, Decimal(0), Fraction(0,1)
	--空的序列和集合："", (), [], {}, set(), range(0)
```

逻辑运算符

```
and：左右两边同时为True,结果为True
or：左右两边其中一个为True,结果为True
not：操作数为True,结果为False ; 操作数为False,结果为True
如果操作数是字符串,结果将会是字符串
```

短路逻辑和运算符优先级

```
短路逻辑：从左往右,只有当第一个操作数的值无法正确 逻辑运算的结果时，才对第二个操作数进行求值
		(也就是说,从左往右,如果一个的操作数能完成逻辑运算的判断,就不会对第二个操作数求值了)
		（3 and 4 output 4              3 or 4 output 3）
		not → and → or 
```

![image-20241009152058829](C:\Users\12774\AppData\Roaming\Typora\typora-user-images\image-20241009152058829.png)从低到高



分支

```python
分支结构由if形成

⭐if-else标准写法：
if 条件表达式 :
	满足条件后执行的语句块
	····
	····
else：
	不满足条件条件后执行的语句块
	···
	···
	
⭐判断多个条件标准写法2：
if condition_1 :
	statements····
elif condition_2 :
	statements···
elif condition_3 :
	statements····
else :
	statements····
	
⭐标准写法3：
条件成立时执行的语句 if condition else 条件不成立时执行的语句
print("bingo") if age < 18 else print("sry")


比如：
if a < b:
    small = a
else:
    small = b
	相当于
small = a if a < b else b
```

循环

```python
循环语句有2种："while语句"和"for语句"

⭐标准写法1：
while condition:
	statements
    
⭐标准写法2：
for 变量 in 可迭代对象 :
    statements····
    
死循环：  (只能通过control + C强制中断程序)
while True： (或者 while 1:)
	statements
    
break：无论后续是否还有需要执行的语句，直接跳出循环体。
continue：跳出本轮循环,回到循环体的条件判断位置,开始下一轮的循环。
无论时break还是continue,只能作用于一层循环体。
```

数据类型之"列表" list

```python
列表list：一个有序且可以更改的集合。列表中的元素可以是不同类型,除数字以外,其他任何元素必须用单引号括起。
⭐
列表变量名称 = ['元素', 数字]
尽管不同列表存储的内容相同,但py还是会为每个列表开辟单独的存储位置进行存放

rhyme = [1,2,3,4,5]
通过下标索引列表中的元素
rhyme[0]（类比C语言2中的数组,可以用下标访问,从0开始）
rhyme[-1] 访问列表中最后一个元素
rhyme[-2] 访问列表中倒数第二个元素

⭐列表切片(参数表示下标,中间必须用冒号:隔开)（左开右闭原则）
rhyme[start_index : last_index]   	rhyme[1:3] → output [2,3]
rhyme[ : last_index]	rhyme[: 3] → output [1,2,3]
rhyme[start_index : ]	rhyme[3: ] → output [4,5]
rhyme[ : ] 打印怎么列表
rhyme[start_index : last_index : step]	rhyme[0 : 5 : 2] → output [1,3,5]
rhyme[ : : step]


⭐列表的储存方法(增/删/改/查)
增-------------------------------------------------------------
append()	在列表的末尾处添加一个指定的元素(只能添加一个)
rhyme.append(6)     output  [1,2,3,4,5,6]

extend()	在列表的末尾处添加一个可迭代对象(参数必须是可迭代对象)
rhyme.extend([7,8,9])	output  [1,2,3,4,5,6,7,8,9]

rhyme[len(rhyme):] = [6] 相当于 rhyme.append(6)
rhyme[len(rhyme):] = [7,8,9] 相当于 rhyme.extend([7,8,9])

insert(i_index, i_elements)	
在列表的任意下标插入一个元素(i_index指定待插入的位置; i_elements指定待插入的元素)
rhyme.insert(1,7) → output  [1,7,2,3,4,5] 在列表的下标为1处添加7

删-------------------------------------------------------------
remove(target) 删除列表中的指定元素
(列表有多个匹配的元素,仅删除第一个; target不是下标而是指定的元素,不存在会报错)
rhyme.remove(3) → output [1,2,4,5]

pop(t_index) 删除列表中 指定下标的元素
(t_index是下标,不是指定的元素)
rhyme.pop(3) → output [1,2,3,5]

clear() 列表全部清空
rhyme.chear()    结果是rhyme变为一个空列表[]

改-------------------------------------------------------------
rhyme[4] = 5	直接指定下标进行更改
rhyme[3: ] = [8,7,5]	利用切片对后续下标位置进行更改

#对列表进行排序
rhyme.sort()	从小到大(内置reverse参数，默认False,True表示从大到小)
rhyme.reverse()		将顺序翻转,即[5,8,7] → [7,8,5]

查-------------------------------------------------------------
rhyme.count(3) 	统计列表中"值为3"的元素有多少个; 这里参数是值，不是下标
rhyme.index(4)	查找某个元素的索引值,参数还是值而非下标
index(x,start,end)	x是被查元素;从start下标开始查找;在end下标位置结束查找
rhyme[rhyme.index(8)] = 2014 当不知道某个元素的索引值,但又想替换成新的元素(多个重复的元素,替换列表第一个出现的)
test = rhyme.copy() = rhyme[:]	列表拷贝,将rhyme列表拷贝到test列表(都是浅拷贝)

列表的加法和乘法-------------------------------------------------------------
s = [1,2,3]  t = [4,5,6]	
s + t = [1,2,3,4,5,6]	列表的加法相当于列表组合,并集处理
s*3 = [1,2,3,1,2,3,1,2,3]	列表的乘法相当于复制列表n次

⭐⭐嵌套列表-------------------------------------------------------------
matrix = [[1,2,3],[4,5,6],[7,8,9]]	二维列表,相当于矩阵
这里的[1,2,3]是matrix下标为0的元素,后面同理
matrix[x][b]	[x]指matrix的行,[b]指matrix的列

list = [[]]*3 → [[],[],[]]
list[0].append(3) → [[3],[3],[3]]
对于内嵌的列表,只是拷贝了对其的引用,非真正进行物理上的拷贝
A = [[t]*2]*3 → [[t,t],[t,t],[t,t]]  理解为"内乘为列数,外乘为行数"

⭐⭐访问嵌套列表（利用for循环一层一层的剥开访问多维列表）
for i in matrix:
    for each in i:
        执行语句········
        
列表复制/拷贝问题---------------------------------------------------   
x=[1,2,3]
y=x		这里的赋值并非把数据放到里面,而是将变量与数据进行挂钩,相当于引用(堪比指针)
x[1]=1
print(y)  → [1,1,3]		这里内容也会跟着改变

#对于以上的例子,可以用copy进行处理,因为copy拷贝的是列表整个对象,不仅仅是变量的引用
test = rhyme.copy() = rhyme[:]		是列表的copy方法

import copy		是copy模块的一个copy函数,注意区分
x = [[1,2,3],[4,5,6],[7,8,9]]
y = copy.copy(x)
这里是浅拷贝,只拷贝外层对象,如果有嵌套对象,那么对其是引用;一般处理一维列表

处理嵌套列表,需要深拷贝
import copy
y = copy.deepcoy(x)
深拷贝连嵌套对象也进行拷贝了,适用于处理多维列表

列表推导式-----------------------------------------------------------------

举例:对一个列表中的所有元素扩大2倍
    oho = [1,2,3,4,5]
    for i in range(len(oho)):
        oho[i] = oho[i]*2
  	但是用列表推导式的话		(效率快了接近一倍)
    oho=[i*2 for i in oho]
    
#如何构成？
[expression for target in iterable] ⭐⭐⭐ 结果一定是一个列表
执行顺序：for语句 → expression
expression：表达式
target：expression里的一个变量
iterable：可迭代的对象

x = [i for i in range(10)]
super = [[0]*3 for i in range(3)]	利用列表推导式创建二维列表
		↓
[[0,0,0],[0,0,0],[0,0,0]]

#进阶列表推导式; 加上if条件
[expression for target in iterable if judgement]⭐⭐⭐
执行顺序：for语句 → if语句 → expression
even = [i for i in range(10) if i % 2 == 0] → [0,2,4,5,8]

#列表推导式也可以嵌套
[expression for target1 in iterable1
			for target2 in iterable2
			···
			for targetN in iterableN]

x = [[1,2,3],[4,5,6],[7,8,9]]
flatten = [col for row in matrix for col in row]
	↓
[1,2,3,4,5,6,7,8,9]
上述换种写法：
fatten = []
for row in matrix:
    for col in row:
        flatten.append(col)
        
可以判断出,列表推导式也是按照顺序写嵌套的
```



数据类型之"元组" tuple

```python
元组:也是序列,和列表相似,但元组中的元素不可被改变！！！  

元组变量名称 = ('元素', 数字)
元组变量名称 = '元素', 数字

元组可以像列表一样,利用下标进行索引,可以切片,可以推导式(变成列表),可以查！！

#打包和解包
t = (123,"abc",3.14)	打包操作
x,y,z = t	→ x=123;y="abc";z=3.14  解包操作(赋值的数量必须跟右侧序列的元素数量一致)

#元组中的元素不可变,但元组中的元素是指向一个可变的列表,那么依然可以修改的
s = [1,2,3]
t = [4,5,6]
w = (s,t)
w[0,0] = 0
output:   ([0,2,3],[4,5,6])
```



数据类型之"字符串"  str

```python
⭐字符串是"不可变"的对象,只会按规则生成一个新的字符串
x = "Hey Man"

#字母大小写处理方法
x.capitalize() 将字符串的首字母变大写,其余变小写
x.casefold() 将字符串全部变成小写	（除英文字母,还可以处理其他语言的字符）
x.title()	将字符串中,每个单词的首字母变成大写
x.swapcase() 	将字符串字母的大小写反转,大写变小写,小写变大写
x.upper()	将所有字母变成大写
x.lower()	将所有字母变成小写	（只能处理英文字母）

#左中右对齐
center(width,fillchar='')	中间对齐
rjust(width,fillchar='')	右对齐
ljust(width,fillchar='')	左对齐
zfill(width)	用0去填充左侧,一般用在数据报表

width:指定整个字符串的宽度,若指定宽度 ≤ 原字符串,直接输出,无需对齐;否则用空格填充
fillchar:指定某个字符进行填充,默认是用空格
    
#字符串查找功能
count(sub[, start[, end]])		子字符串在字符串出现的次数
find(sub[, start[, end]])		子字符串在字符串出现的位置,返回值是下标
rfind(sub[, start[, end]])		从右开始判断,子字符串在字符串出现的位置,返回值是下标
index(sub[, start[, end]])		和find类似	
rindex(sub[, start[, end]])		和rindex类似

find和rfind方法查找不到时,返回的是-1值
而index和rindex方法查找不到时,是会抛出异常

sub:指定的子字符串
start和end：指定查找的起始位置和结束位置,参数为下标

#字符串替换
expandtabs([tabsize=8])	使用空格替换替换制表符,并返回新的字符串;参数一个tab=几个空格

replace(old,new,count=-1) 
将某段字符串的old部分替换为new部分;count是替换的次数，默认-1,替换全部的意思
例如 "i love you".replace("you", "meself")  →  "i love myself"

translate(table)	根据自定义规则进行替换
table是表格,用于指定转换的表格
用str.maketrans(x[,y[,z]])来获取table
例如:
table = str.maketrans("ABCDEFG","1234567")
"I love FishC".translate(table) → "I love 6ish3"

#字符串判断
startswith(prefix[,start[,end]])  用于判断参数的子字符串是否出现在字符串的起始位置,返回T/F
"his name is xxx".startswith("wo")  → True

endswith(suffix[,start[,end]]) 用于判断参数的子字符串是否出现在字符串的结束位置,返回T/F
"his name is xxx".startswith("xxx")  → True

判断字符串的所有单词是否以大写字母开头,其余均为小写
"I Love Python".istitle()  →  True

判断字符串的所有字母都是大写字母(相反,是否全部小写用islower())
"I Love Python".isupper()  →  False

判断字符串是否仅由字母构成
"I Love Python".isalpha()  →  False		空格/制表符不算字母

判断字符串是否为空白字符串
"    \n	".isspace()	→ True

判断字符串是否可以打印
"I Love Python\n".isprintable()  →  False	转移字符无法打印

判断字符串是否为合法的标识符
"i b c".isidentifier()	→	False	因为有空格

判断字符串是否为保留标识符
import keyword
keyword.iskeyword("if")	 →	 True

#截取字符串
不想看到字符串的左侧存在空白	参数默认None,当然能可以指定参数,按单个字符为单位去匹配,直到遇到不在指定字符集合中的字符为止。
"	左侧不留白".lstrip()
"www.ilovefishc.com".lstrip("wcom.")	 →	 "ilovefishc.com"	i不在指定字符集合中

不想看到字符串的右侧存在空白
"右侧不留白	".rstrip()

字符串的左右空白都不要
"	中间	".strip()

removeprefix()和removesuffix()	参数是指定的整个字符串，非单个字符
"www.ilovefishc.com".removeprefix("www.")	 →	 "ilovefishc.com"
"www.ilovefishc.com".removesuffix(".com")	 →	 "www.ilovefishc"

#拆分和拼接
将字符串以参数指定的分隔符为依据进行切割,将切割后的结果返回一个三元组(三个元素的元组)
partition(sep)	从左到右去找分隔符
rpartition(sep)	 从右到左去找分隔符
"www.ilovefishc.com".partition(".")  →  ('www', '.', 'ilovefishc.com')
"ilovefishc/com".rpartition("/")  →  ('ilovefishc', '/', 'com')

根据分隔符将字符串分割成一小块一小块
split(sep=None,maxsplit=-1)		maxsplit指定切割次数,-1默认全切
不指定参数,则将字符串变为列表中的一个元素(默认以空格为切割符进行切分)
"苟日新,日日新,又日新".split() → ['苟日新,日日新,又日新']	
"苟日新,日日新,又日新".split(',')  → ['苟日新','日日新','又日新']  按','进行分割
"苟日新,日日新,又日新".rsplit(',') → ['苟日新','日日新','又日新'] 从右往左切

将字符串按行(\n,\r,)进行分割,结果以列表的形式返回
False默认不包含换行符,True表示包含换行符
splitlines(keepends=False)
"苟日新\n日日新\n又日新".splitlines() → ['苟日新','日日新','又日新']
"苟日新\n日日新\n又日新".splitlines(True) → ['苟日新\n','日日新\n','又日新']

字符串拼接,参数是列表或元组 【join速度比加法快多了】
join(iterable)
".".join(['www','ilovefishc','com']) → 'www.ilovefishc.com'
'^'.join(('F','fish','C')) → 'F^fish^C'

s="FishC"  
s +=s 相当于 "".join('FishC',"FishC")  → 'FIshCFishC'

#格式化字符串
使用一对花括号{}来表示替换字段(即在元字符串中占一个坑位),真正的内容放在format参数中。
当然在花括号内的数字表示参数的下标位置(同一个下标可以被多次引用);也可以用关键字表示参数
format()
例如： 
year = 2010 
"studio make up {year} 年".format(year)
output:'studio make up 2010 年'
    
例如:
"1+2={}, 2²是{},3的立方是{}".format(1+2, 2*2, 3*3*3)
例如:
"{1}看到{0}就很激动！".format('我','姐姐')
output:  '姐姐看到我就很激动！'

例如:
"{name}看到{other}就很激动！".format(name='我',other'姐姐')
output:  '我看到姐姐就很激动！'

文本对齐,align有以下种; 
冒号是必须的,它的左边是参数的位置或关键字索引,右边才是格式化选项
格式[:align]
'^':居中
'<':左对齐(默认参数有)
'>':右对齐
'=':强制将填充放置在符号之后但在数字之前的位置(适用于打印'+00000120'形式的字符串)
'+':正数在前面添加正号(+),负数在前面添加负号(-)
'-':仅负数在前面添加负号(-),(默认行为)
空格:正数在前面添加一个空格,负数在前面添加负号(-)
',':在千分位除作分隔符,也可以是其他符号;如果位数不足,千位分隔符不显示
'.xf':像f或F,是限定小数点后显示x个数位;g或G是限定小数点前后一共显示x个数位;精度选项不允许在整数或字符串上应用
'b':将参数以二进制形式输出; c以Unicode字符; d以十进制; o以八进制; x和X以十六进制;None默认d;e和E以科学计数法; %后面附带一个百分号
'#b':井号表示,为输出在前面追加一个前缀
    
-----------------------------example----------------------------------
"{:^10}".format(250) → '   250    '		10表示字符宽度小于10个字符,用空格填充至10个字符
"{1:>10}{0:<10}".format(520,250)  →  '       250520       '
"{:010}".format(250)相当于"{:0=10}".format(250) → '0000000520'	用0填充,仅对数字有效
"{:010}".format(-250) → '-000000520'	用0填充,负号也算一个字符
"{:%10}".format(250) → '%%%%%%%520'	用%符号填充
"{:+} {:-}".format(520,-250) → '+520 -520'
"{:,}".format(123456789) → '123,456,789'
"{:.2f}".format(3.1415) → '3.14'	小数点后一共
"{:.2g}".format(3.1415) → '3.1'	小数点前后一共
"{:.6}".format("i love fishc") → 'i love'	字符串前6位
"{:b}".format(80) → 1010000
"{:#b}".format(80) → 0b1010000

# f-string
进一步简化字符串的操作,在字符串前面加上一个f或者F即可
比如:
    year = 2010
    F"studio set up {year} 年"	相当于 "studio set up {year} 年".format(2010)
    output: "studio set up 2010 年"
     
```



数据类型之“序列”

```python
序列:指一组有序排列的值的集合; 根据是否能被修改这一特征分为2种序列
    	--可变序列:列表
        --不可变序列:元组、字符串
            
每一个对象都有三个基本属性:
    --唯一标志:随着对象创建的同时而产生,不可被修改且值不重复(类比身份证)。可以id()查询
    --类型:
    --值:

 迭代器和迭代对象的异同点:
    	--一个迭代器肯定是一个可迭代对象
        --可迭代对象可以重复使用,但迭代器是一次性的
        --都可以通过for循环进行遍历
        --迭代器维护遍历的状态。每次调用next()函数都会移动到下一个元素。
        --如果一个对象具有iter()方法,那么它可迭代,如果还有next()方法,它就是迭代器
        
#能够作用于序列的一些运算符和函数
+:两个序列进行拼接
*:将序列进行重复(拷贝)
id():查看对象的唯一标志.
is 和 is not:检测对象的id值是否相同,从而判断对象是否是同一个.
in 和 not in:判断某个元素是否在该序列当中.
del:用于删除一个或多个指定的对象.
    
    
#列表、元组和字符串相互转换   
list()
tuple()
str()

min()	对比传入的参数,返回最小值,传入的参数是字符串,则比较ASCII码的大小
max()	对比传入的参数,返回最大值
传输的参数是空序列,则会报错; 否则使用一个default.
len()	统计序列的长度,但是有上限,2的操作系统位数次方-1
sum()	统计序列中,所有元素的总和
all()	判断可迭代对象中,是否所有元素的值都为真
any()	判断可迭代对象中,是否存在某一个元素的值为真
enumerate()		用于返回一个枚举对象,功能是将可迭代对象中的每个元素从指定'开始的序号'(默认从0开始)共同构成一个二元组的列表
zip()	将多个可迭代对象打包成一个个元组,然后返回由这些元组组成的对象。要求可迭代对象一致。
zip_longest()	这是itertools模块中的函数,比zip()高级一点的是,允许可迭代对象长度不一致,继续打包剩余的元素,直到最长的可迭代对象结束.
map(function,iterable)	根据指定的函数对可迭代对象的每一个元素进行运算,并返回运算结果。
filter(function, iterable)	过滤掉不符合条件的元素，返回一个‘符合所有条件且结果为真的元素’的迭代器。(只有符合function且计算结果为真的元素,才会被保留)


list('fishc')   →  ['f', 'i', 's', 'h', 'c']		字符串变列表
list((1,2,3,4,5))   →  [1,2,3,4,5]		元组变列表
tuple('fishc')   →  ('f', 'i', 's', 'h', 'c')		字符串变元组
tuple([1,2,3,4,5])   →  (1,2,3,4,5)		列表变元组
str([1,2,3,4,5])   →  '[1,2,3,4,5]'		列表变数组
str((1,2,3,4,5))   →  '(1,2,3,4,5)'		元组变数组
min([],default='nothing in it')		default在min和max函数的应用举例

seasons = ['Spring','Summer','Fall','Winter']
enumerate(seasons)	创建一个枚举对象
list(enumerate(seasons)) → [(0,'Spring'),(1,'Summer'),(2,'Fall'),(3,'Winter')]
list(enumerate(seasons),10) → [(10,'Spring'),(11,'Summer'),(12,'Fall'),(13,'Winter')]

x = [1,2,3]
y = [4,5,6]
z = [7,8,9]
consist = zip(x, y, z)
list(consist)  →  [(1,4,7),(2,5,8),(3,6,9)]

import itertools
consist = zip(x,y,'fishc')
output → [(1,4,'f'),(2,5,'i'),(3,6,'s'),(None,None,'h'),(None,None,'c')]

test = map(str.upper, ['hello','world'])
list(test)	→	['HELLO','WORLD']

list(filter(str.islower,'FishC')) → ['i','s','h']

-----------------迭代对象和迭代器---------------------------
iteration_list = [1,2,3,4]
for i in iteration_list:	//这里的iteration_list就是迭代对象
    print(i)
    
iterator = iter(iteration)	//iter()用于获取一个可迭代对象的迭代器,并返回该对象的迭代器.
next()函数用于获取迭代器的下一个元素,如果迭代器没有更多的元素,则抛出一个StopIteration异常.
next(iterator)	//此时打印为 1
next(iterator)	//此时打印为 2
next(iterator)	//此时打印为 3
next(iterator)	//此时打印为 4
next(iterator,'nothing')	//没有更多的元素,将异常改为打印nothing.
------------------------------------------------------------------------------------
```



数据类型之‘字典’ dict

```python
字典dict是PYTHON中唯一实现映射关系的内置类型。
字典是一种内置的数据结构,它存储键值对(key-value),表示一种映射关系。
格式 variable = {key1:value1, key2:value2,·····}
冒号前面的key是键,冒号后面的value是值
序列是通过位置(下标)的偏移来存取数据的; 而字典通过键实现写入和读取
即:序列在方括号[]内写入的是下标值;而字典在方括号[]内写入的是键值
例如： 
y = {'lvbu':'卢布','guanyu':'关羽'}
y['lvbu'] → '卢布'	通过键值输出value
y['liubei'] = ['刘备']	通过指定一个不存在于字典中的键,就可创建一个新的键值对
print(y) → {'lvbu':'卢布','guanyu':'关羽', 'liubei':'刘备'}

#字典的基本操作
---------------------------------创建字典的方法-----------------------------
a = {'lvbu':'卢布','guanyu':'关羽'}		通过{}和:的组合将映射关系套牢
b = dict(卢布='lb',关羽=‘'gy',刘备='lb2')	通过dict()函数构造字典,通过key='value'建立内容,其中键即使是字符串但也没有引号
c = dict([('卢布','lb'),('关于','gy'),('刘备','lb2')]) 将键值对以二元组为单位存放到列表中,然后生成字典.每个键值对的格式为(key,value),其中key和value都需要引号。
d = dict({'lvbu':'卢布','guanyu':'关羽'})  结合dict和a的方法
e = dict({'lvbu':'卢布','guanyu':'关羽'},zhangfei='张飞') 结合b,d的方法
h = dict(zip(['lvbu','guanyu','liubei'],["卢布","关羽","刘备"])) 利用zip函数创建
fromkeys(iterable[,values])		根据给定的可迭代对象创建一个新的字典
d = dict.fromkeys('fish',250) → {'f':250, 'i':250, 's':250, 'h':250}
----------------------------------------删除-----------------------------------
pop(key,[,default])	根据指定的键进行删除操作,返回的是被删除键对应的值
d.pop('s','nothing')	如果删除一个不存在的键,会抛出异常KeyError,这里异常改为nothing

d.popitem()	删除最后一个加入字典的键值对

del d['i']	利用del根据指定键值进行删除

d.clear()	删除字典的所有键值对,变成一个空字典
----------------------------------------修改-----------------------------------
d['f'] = 115	通过指定键对相应值进行修改; 但如果该键不存在则会添加至字典而非修改

update([other])	可以同时传入多个键值对,也可以传入另外一个字典,或者一个包含键值对的迭代对象
d.update({'i':105, 'h':104})
d.update(F=70, c=67)
----------------------------------------查-----------------------------------
d['f']	根据指定键查对应的值,	键不存在于字典会报错

get(key,[, default])	根据指定键查对应的值,找不到键可以抛出异常,异常内容可以自己修改
d.get('c', 'no_c')

setdefault(key,[, default])查找一个键是否存在于字典中,存在则返回对应的值,不在则添加到字典
d.setdefault('C','code')
----------------------------------------其他应用----------------------------------
视图对象:即字典的动态视图,意味着当字典的内容发生改变时,视图对象的内容也会相应地改变.
	items()	获取字典的键值对
	keys()	获取字典的键
	values()	获取字典的值
#For Instance
d = dict.fromkeys('fish',250) → {'f':250, 'i':250, 's':250, 'h':250}
items = d.items()	→	dict_items([('f',250),('i',250),('s',250),('h',250)])
keys = d.keys()		→	dict_keys(['f','i','s','h'])
values = d.values()		→	dict_values([250,250,250,250])
d.pop('f')	当删除指定键后,三个视图也会跟着发生改变
items	→	dict_items([('i',250),('s',250),('h',250)])
keys	→	dict_keys(['i','s','h'])
values	→	dict_values([250,250,250])
#

len()	获取字典中的键值对数量
in 和 not in 判断键是否在字典中
list(d)	→ ['i','s','h']		将字典转为列表,字典中的键按顺序变成列表中的元素
list(d.values()) → [250,250,250]	将字典中,键对应的值按顺序变成列表中的元素
e = iter(d)	将字典变成一个迭代器,迭代器中的元素就是字典中的键
list(reversed(d.values))	将字典中的value翻转然后存入列表中

#嵌套(某个键的值是另外一个字典)
d = {"吕布":{'Chinese':60, 'Math':70, 'English':80}, 
     "刘备":{'Chinese':45, 'Math':72, 'English':20}}	字典嵌套字典
d['吕布']['Math'] → 70	由外到内进行键索引,内层也是字典,用键索引

t = {"吕布":[60,70,80], "刘备":[15,45,32]}	字典嵌套列表
t['吕布'][1]  → 70	也是由外到内,不同点在于,内层是列表,用下标索引

#字典推导式
dc = {'f':70, 'i':105, 's':80, 'h':43}
b = {v:k for k,v in dc.items()}		//这里的意思是进行键和键值调换
print(b) → {'70':'f', '105':'i', '80':'s', '43':'h'}
c = {v:k for k,v in dc.items() if v > 100}	//这里加上筛选条件
print(c) → {'105':'i'}
·······类比于列表的推导式·······················
```



数据类型之‘集合’ set

```python
集合中所有元素都是独一无二且无顺序的。不可以用下标索引的方式进行集合访问
格式： {value,balue,value,·····}

{s for s in 'fishc'} → {'h','i','f','s','c'}	集合也可以使用推导式;集合没有顺序

set(iterable)	用set()函数创建集合
s = set('fishc')

in 和 not in 判断某个元素是否存在于集合中
'c' in s  →  True


set([1,1,2,3,5]) → {1,2,3,5}  利用集合进行去重操作,可迭代对象转为集合时,会自动进行去重操作

len(iterable) == len(set(iterable))	判断一个可迭代对象是否存在重复元素

t = s.copy()浅拷贝

#集合的操作,传入的参数不是集合类型,会首先转为集合类型再进行计算; 参数可以是多个 ; 结果赋值
#如果使用运算符,则符号两边必须是集合类型的数据,否则报错
s.isdisjoint(set(iterable))	判断两个集合是否没有交集;没有返回True	

s.issubset(set(iterable))	判断iterable是否存在子集s
s<=set(iterable)  检查集合s是否是集合iterable的子集
s<set(iterable)  检查集合s是否是集合iterable的真子集(是子集但不相等)

s.issuperset(set(iterable))	判断子集s是否为iterable的超集(一个集合包含另外一个集合的所有元素,并可能还包含其他元素)
s>=set(iterable)  检查集合s是否是集合iterable的超集
s>set(iterable)  检查集合s是否是集合iterable的真超集

s.union(set(iterable)) 	求并集,返回一个集合
s|{1,2,3}|set(iterable)	求并集

s.intersection(set(iterable))	求交集(两个集合共有的部分),返回一个集合
s&{1,2,3}&set(iterable)	求交集

s.difference(set(iterable))	求s - iterable的差集(存在于集合s但不存在于集合iterable的元素,所构成的集合),返回一个集合
s - {1,2,3} - set(iterable)	 求差集

s.symmetric_difference(set(iterable))	求对称差集(两个集合的并集减去它们的交集,即剔除两个集合的共同部分的并集),仅允许一个参数,返回一个集合
s ^ {1,2,3}	 求对称差集,仅允许一个参数


#细分为'可变集合'和'不可变集合'
set(iterable)  可变
frozenset(iterable)	 不可变

#仅适合于set()对象的方法,可以对集合内容进行改动的方法,iterable是可迭代对象
s=set('FishC')
t = forzenset('Hello')
##集合运算后,会更改集合里面的内容。结果保留在集合s里面,而非赋值结果
update(*others)	//others表示支持多个参数,other表示支持一个参数; 其实就是union_update
s.update([1,1], '23')  →  {1,'3','C','i','s','h','F','2'}
t.update([1,1], '23')  → 报错

s.intersection_update(*others)	求交集
s.difference_update(*others)	求差集
s.symmetric_difference_update(others)	求对称差集

s.add(item) 单纯的往集合里面添加数据,这里的参数并非是迭代参数,而是作为一个元素,插入进去
s.add("45") → {1,'3','C','i','s','h','F','2','45'}	

s.remove(item) 删除,若指定的元素不存在,会抛出异常
s.discard(item)  删除,若指定的元素不存在,会静默处理(相当于没有这条语句)
s.pop()	会随机删除集合一个元素
s.clear() 清空集合中的元素,变成空集合{}

#什么叫可哈希？
即一个值value可以通过哈希函数hash(value)得到一个值哈希值eq_value,那么这个值value就是可哈希。用于快速比较和检索字典的键和集合的元素。因为哈希值需要在对象的生命周期内保持不变。
	--大多数不可变的对象都是可哈希。例如字符串、元组、含有列表作为元素的集合
	--而可变的对象都是不可哈希的。例如列表、字典、集合
    --对于不同对象,如果它们的值相同,则哈希值相同; 比如1和1.0的哈希值相同
```



函数

```python
定义函数格式：
def function_name():
	函数体
	statement1
	statement2
    return item		(不需要返回参数可以不写)

调用函数格式：
function_name()

#函数的参数
从调用的角度,分为两类:‘形式参数’和‘实际参数’
	--形参：函数定义的时候,写参数的名字
    --实参：调用函数的时候传递进去的值,按形参定义的顺序进行传递
    
^_^位置参数:调用函数时根据参数的位置来传递参数; 位置参数的顺序必须与函数定义中的顺序相匹配,传递的数量也要相同,除非包含可接受额外参数的机制。
    
^_^关键字参数:函数调用时根据参数的名字来传递参数; 顺序可以不按函数定义参数的顺序。

⭐如果同时使用位置参数和关键字参数,则位置参数必须在关键字参数之前,否则就会报错。
默认参数:在调用函数时,如果没有传入实参,则采用默认的参数值来代替

⭐⭐
help() 一般用来查看某个函数的使用文档
help(sum) → sum(iterable,/,start=0)
在文档字符串中,使用'/'和'*'来表示参数的传递方式:
    '/'表示,符号左侧的参数必须传递位置参数不非关键字参数;符号右侧的参数随意.
	'*'表示,符号左侧的参数必须传递关键字参数非位置参数

⭐
#到底需要传入多少个参数？？？？
^_^收集参数:函数能够接收并处理一个不确定数量的参数。这些参数可以时位置参数或关键字参数;允许函数在调用时接收比定义形参时更多的参数。
        *args:用于收集额外的位置参数。当调用函数时,若实参数量多于形参数量,所有实参会存入同一元组,形参中的args相当于元组。
    	**kwargs:用于收集额外的关键字参数。当调用函数时,若实参是命名参数,且实参的名字没有在 函数定义中作为位置参数出现,那么所有实参会存入同一字典,形参中的kwargs相当于字典。
    args全称Arguments,代表函数可以接受任意数量的未命名位置参数。只能收集位置参数。
    kwargs全称Keyword Arguments,代表函数可以接受任意数量的命名关键字参数。
----For Instance-----
    def funs(*args):
        print(args)
funs(1,2,3,'a','b') → (1,2,3,'a','b')	输出是元组类型

	def func(**kwargs):
        print(kwargs)
func(a=1,b=2,c=3) → {'a':1,'b':2,'c':3}	输出是字典类型

解包参数:
	--在形参中,希望函数能够接受任意数量的位置参数或关键字参数。
    --在实参中,将序列中的元素作为位置参数传递给函数。*align_name。 将字典中的键值对作为关键字参数传递给函数。**dict_name
    
    def funt(a,b,c,d):
        print(a,b,c,d)
args = (1,2,3,4)
kwargs = {'a':1,'b':2,'c':3,'d':4}
funt(*args) = funt(**kwargs) → 1 2 3 4


#作用域
作用域:指一个变量可以被访问的范围。
    --局部作用域：一般指在函数内部定义的局部变量,只能在该函数内部被访问和修改。
    --全局作用域：在程序的任何地方定义的全局变量,都可在全局作用域内被访问和修改。
    --内置作用域：Python解释器内部使用的变量,可在程序的任何地方使用,但不建议对其修改。
    --类作用域：在类定义内部的变量和方法
---访问规则LEGB---
Local局部作用域 → Enclosed嵌套函数的外层函数作用域 → Global全局作用域 → Build-In内置作用域

global语句:在函数或其他作用域中,声明的变量为全局变量,即这些变量属于全局作用域;使用global可以访问和修改全局作用域中的变量。
    
nonlocal语句:用于嵌套函数中声明变量,这些变量属于拥有该嵌套函数的函数体,允许在嵌套函数中修改外部函数的局部变量。【如果多个嵌套函数共享同一个封闭作用域,那么在一个嵌套函数中使用nonlocal修改变量,这个修改将影响到所有可以访问该变量的其他嵌套函数。】

    
⭐闭包:能够访问"其外部函数作用域中的变量"的函数。
	def outer_func():
        a='haha'
        def inner_func():
            print(a)	//内嵌函数引用外部函数的变量
        return inner_func	//返回内嵌函数,创建闭包
    closure = outer_func()	//获取闭包函数
    closure()	//调用闭包函数
    
⭐装饰器:允许用户在不修改函数本身的情况下,给函数增加额外的功能。本质上是一个函数,它接受一个函数作为参数并返回新的函数。提供一种灵活的方式来扩展函数和方法的功能。
    --常用于日志记录、新能测试、缓存、权限校验。
    --多个装饰器可以同时用在同一个函数上,顺序是,越靠近被装饰函数的装饰器越先被执行,随后结果传到下一个装饰器进行执行。由下往上按顺序执行。
    --当然,可以在注释中,进行装饰器传递参数
    --装饰器可以没有形参,但内部函数需要一个形参来引用被装饰的函数。
    
###装饰器的基本结构和用法###⭐⭐⭐⭐
def my_decorator(func):	 //创建一个名叫my_decorator的装饰器,形参func用于接收一个函数对象
    def wrapper(*args, **kwargs):
        //被装饰函数(原始函数)调用前,所执行的代码内容,例如下面的语句
        print('Something before the function running')
        ··········
        //调用被装饰函数(原始函数)，这里的func()是核心,相当于整个被装饰函数(原始函数)
        result = func(*args, **kwargs)	或者 func(*args, **kwargs)
        //被装饰函数(原始函数)调用完成后,所执行的代码内容,例如下面的语句
        print('Something after the function runned')
        ······························
        return result //返回被装饰函数的返回值(返回原始函数的返回值)【可有可无】
    //确保装饰器能够正确地返回一个函数对象,wrapper时一个包装函数,用于增强或修改原始函数func的行为。即返回值通常时一个新的函数或可调用对象
    return wrapper	

//使用装饰器时,将装饰器放在需要装饰的函数定义之前,并用@符号
@my_decorator	//必须要有这个注释,这里相当于把passive_function作为参数放入到装饰器了
def passive_function(name):
    print(f'hello {name}')

passive_function()	//调用被装饰函数(原始函数)

###-------lambda表达式--------###
格式: lambda arg1, arg2, ····, argN : expression
    
lambda是关键字,冒号左边是传入函数的参数,冒号右边是函数实现表达式以及返回值;它是匿名函数

例如：
def squareX(x):
    return x*x
squareX(3) → 9
	相当于
squareY = lambda y:y*y
squareY(3) → 9

##--生成器--##
让函数在退出之后还能保留状态 → 闭包或全局变量	【但不安全】

在函数用yield表达式来代替return语句; 但是每次调用时,提供一个数据,即每次执行到yield语句就生成一个数据,暂停并保留状态,下次调用从yield语句的下一个语句开始执行。可以配合next()语句使用
例如:
    def counter():
    i = 0
    while i <= 5:
        yield i
        i += 1
    counter()	→	此时counter变成一个生成器generator object
    for i in counter():
        print(i)	→	0 1 2 3 4 5

生成器表达式,类似于列表推导式,但返回的时一个生成器
格式: (result_expression for element in iterable if condition)
    
##函数文档##  
    使用help()函数查看某些函数的使用说明
    
----创建函数文档----
函数文档是在函数的最顶部,使用函数时,文档不会被打印出来。可用help(exchange)进行文档查看。
def exchange(dollar, rat6.32):
    """			三个引号用于创建多行字符串
    功能:汇率转换, 美元 -> 人民币
    参数:
     - dollar 美元数量
     - rate 汇率, 默认值时6.32 (2024-10-25)
    返回值:
     - 人民币的数量
    """
    return dollar * rate
    
----类型注释----
为函数的参数和范围值添加类型注解.

1.变量注解 →  number:float = 10.2
    
2.函数注解↓    
def times(s:str, n:int) -> str:
    return s*n
上述代码中, s:str表示函数times的参数s和n预期分别是一个字符串类型和整数类型; ->str表示函数的返回值预期也是一个字符串类型;但实参可以不是预期类型,只是作者希望实参是这种类型
    
3.类变量注解↓
class Point:
    x: int
    y: int

    def __init__(self, x: int, y: int):
        self.x = x
        self.y = y
   

----内省----
内省:指在运行时检查和分析对象,如变量、函数、属性和方法的能力。通过一些特殊的属性来实现内省
1.函数的__name__属性包含了函数的名字
def my_function():
    pass
print(my_function.__name__) → my_function

2.__annotations__属性包含了函数的类型注释

3.__doc__属性包含了函数的文档字符串

4.dir()函数列出函数的所有属性和方法,包括内置的和自定义的

5.
__defaults__属性包含了位置参数的默认值
 __kwdefaults__属性包含了关键字参数的默认值

    
##高阶函数##
满足两个条件:
    --接受一个或多个函数作为参数:将函数作为参数传递给其他函数
    --返回一个函数:将函数作为结果返回
        
⭐--@wraps-----
@wraps:是一个装饰器,用于装饰其他装饰器; 由functools模块提供,主要作用是将‘被装饰函数’的元数据(函数名、注解等)复制到装饰器上,保持‘被装饰函数’的原始信息.

    举例:
        from functools import wraps	//首要导入模块
        def my_func(f):
            def wrapper(*args, **kwargs):
                ···
                result = f(*args, **kwargs)
                ···
                return result
            return wrapper
        
        @my_decorator
        def greet(name):
            """So great with you"""
            print(f'hello {name}')
            
        greet.__name__ 	→	'wrapper'	//此时打印的是装饰器的函数名
        
        -----通过在包装器上加入@wraps-----
        def my_func(f):
            @wraps(f)	//这里的f代表被装饰函数,告诉wraps函数应该从参数f复制元数据.
            def wrapper(*args, **kwargs):
                ···
                result = f(*args, **kwargs)
                ···
                return result
            return wrapper
        
        @my_decorator
        def greet(name):
            """So great with you"""
            print(f'hello {name}')
            
        greet.__name__ 	→	'greet'		//此时打印的是被装饰函数的函数名
```



异常 exception

```python
处理异常(negative)
格式:↓
try:
	检测范围
except [expression [as identifier]]:	//指定是某异常类型才执行except异常处理代码
     异常处理代码
else:	(当try语句中没有检测任何异常,则执行else语句中的内容)
		没触发异常时执行的代码       
finally:	(无论异常是否发生,都必须执行的内容)
		收尾工作执行的代码      
    
比如：
try:
	1/0
except :
    print('error')
    
-----------------------------------
raise语句,加上from构成异常链		//类型语句必须存在,不能由用户自己定义

raise ValueError('not true') from ZeroDivisionError

-----------------------------------
assert语句,只能引发AssertionError的异常,通常用于代码调试

s='fishc'
assert s == 'fishc' → True
assert s != 'fishc' → 抛出异常

-----------------------------------
利用异常实现goto

try:
    while True:
        while True:
            for i in range(10):
                if i > 3:
                    raise
                print(i)
            print('skipped')
        print('skipped')
    print('skipped')
except:
    print('come here~!')
```



类和对象

```python
面向对象是一种代码'封装'的方法,将相关的数据和实现的函数给封装在一起。
三个基本特征：封装、继承、多态

对象 = 属性(静态特征) + 方法(对象所能做的事情)

格式:
    class ClassName:		#class关键字用来声明一个类,ClassName是类的名字
        #类变量(静态变量),只能通过类方法进行修改和访问。类变量被所有实例共享。
        #可以通过类名访问类变量(ClassName.static_var)。
        static_var = 'jingtai'	
        
        #__init__是类的构造函数,创建实例时,会自动初始化类的属性。
        #self参数代表类的实例本身,通常是每个方法的第一个参数,self允许实例方法访问和修改属于该实例的属性和其他·实例方法。
        #parameter是传递给构造函数的参数,可被用来初始化类的属性;是实例属性,只能通过实例访问
        def __init__(self, parameter1, parameter2):	
            #实例变量是定义在类的实例上的变量,属于类的每个具体对象。
            #通常在__init__中定义,并通过self关键字来引用.每个实例都有自己的实例变量,它们之间互不影响。左边的parameter1是绑定到实例化对象;右边的parameter1是传递进来的参数
            self.parameter1 = parameter1  
            self.parameter2 = parameter2	
            
        def method1(self):	#实例方法,主要用来访问和修改实例变量。
            #实例方法的实现
            pass
        
        @classmethod	#装饰器,用于定义一个类方法,类方法属于类而非实例方法.类方法的第一个参数通常是cls,cls代表类本身非实例.
        def method2(cls):	#此时method2被装饰了,是类方法,通过cls参数访问和修改类变量;类方法通常用于创建需要特殊逻辑的实例;类方法无需实例可直接通过类名调用。
            #类方法的实现
            pass
        
        @staticmethod	#装饰器,用于定义一个静态方法,用于不依赖类或实例的功能,时一个辅助性功能;不接收cls或self的引用作为第一参数;可以通过类名或实例来调用
        def method3():	#此时method3被装饰了,是静态方法。
            pass
        
instance = ClassName(value1, value2)	#类的实例化,value会自动被__init__初始化

instance.method1()	#调用实例方法


##封装##
将属性和行为捆绑在一起,形成一个独立的类;隐藏了对象的内部状态和实现细节,只暴露有限的接口供外部访问。

##继承##
一种创建新类的方式,子类(新类)继承父类(被继承的类)的属性和方法。继承支持代码的重用、扩展或修改父类的行为。
⭐任何类都是object的一个子类

格式：
	class A:	//A是父类
        x=520
        def hello(self):
            print('hello,i am A')
        def test(self)
        	print('trust me')
            pass
            
    class B(A):        	//B是子类,()内是需要继承的父类,即B继承了A类
        x = 880
        def hello(self):	//#重写(覆盖)了父类A的hello方法
            print('hello,i am B')
    
    b = B()	//创建类的实例
    b.test()	//    	//调用实例的方法
    
判断一个对象是否属于某个类
isinstance(对象, 类)	→	True
isinstance(b, B)	→	True
isinstance(b, A)	→	True

判断一个类是否为某个类的子类
isinstance(子类, 父类)
issubclass(A, B)	→	False
issubclass(B, A)	→	True

##多重继承##
一个子类可以同时继承多个父类
    class D(A, B):        	//子类D同时继承父类A和B
        pass

当继承多个父类时,继承和访问顺序时按照继承的顺序,从左到右
c = C()
c.x → 520
从.hello() → 'hello,i am A'


##组合##
	class Turtle:
        def say(self):
            print('gogogo')
     
    class Cat:
        def say(self):
            print('miao~miao~miao')
            
    class Dog:
        def say(self):
            print('wang~wang~')
            
    //组合
    class Zoo:
        t = Turtle()
        c = Cat()
        d = Dog()
        def say(self):	//self的作用就是将实例对象跟类的方法进行绑定
            self.t.say()
            self.c.say()
            self.d.say()
    
    z =Zoo()
    z.say() 	output:'gogogo'	'miao~miao~miao' 'wang~wang~'
      
    
    
 ##重写##
子类提供了与父类同名的方法的实现。目的是为了改变父类方法的行为,或根据子类的具体需求提供特定的实现。

##钻石继承##
当两个子类B和C继承来自同一个父类A,然后者两个子类B和C共同衍生一个子类D。这种结构在类继承图中就像钻石。

super()函数用于调用父类(超类)的一个方法。根据MRO来确定下一个应被调用的方法。严重依赖MRO顺序.
	--调用父类的构造器:当子类的构成方法__init__()中需要调用父类的构造方法时,可以使用super()来实现。确保父类的初始化代码被正确执行。
     --方法重写:当子类重写了父类的方法时,如果子类方法中需要扩写非重写,可用super()来调用父类中的方法。

比如:
    class A:	// 爷爷辈
    def speak(self):
        print("A speaking")

class B(A):		//爸爸辈1
    def speak(self):
        print("B speaking")
        super().speak()	//扩写后继承父类A的方法

class C(A):		//爸爸辈2
    def speak(self):
        print("C speaking")
        super().speak()	//扩写后继承父类A的方法

class D(B, C):	//儿子
    def speak(self):
        print("D speaking")
        super().speak()	//扩写后继承父类B、C的方法

d = D()	//实例化
d.speak()	//调用方法

  output （根据MRO方法解系顺序:）
	↓
D speaking
B speaking
C speaking
A speaking


## Mix-in ##
通过组合来重构代码,非继承。在不改变类继承结构的情况下,为类添加额外的功能。相当于外挂,插件,脚本

## 多态 ##
允许父类的引用指向子类的对象
	--编译时多态(静态多态):方法重载,即同一个类中有多个同名方法,但参数列表不同
    --运行时多态(动态多态):方法覆盖,即子类重写父类。
        
## 私有变量 ##
仅在定义它们的类内部可访问的变量。防止外部代码直接访问和修改这些状态。

name mangling机制：在名字前面添加2个下划线__
	class C:
        def __init__(self,x,y):
            self.__x = x	//私有变量,只能通过特定接口进行访问和修改
            self.y = y		//共有变量,外部可以直接进行访问
        def set_x(self,x):
            self.__x = x
        def get_x(self):
            print(self.__x)
        c = C(250,30)
        c.__x	→ 	AttributeError	//虽然__x是变量,但是需要通过特定接口去访问
        c.get_x()	→ 	250
        或者c._c__x	→	250		//下划线+类型+变量名
        c.y 	→	30
        
_单个下横线开头的变量:受保护变量,它不应该从类的外部直接访问,但可在类及其子类内部访问
单个下横线结尾的变量_:通常表示这个变量是私有的
    
## __slots__ ##
当一个类只需固定的几个属性,且后续不再会有动态添加属性这个功能需求。可以__slots__类属性可以节省空间。
但是,当子类继承父类时,父类的__slots__属性时不会再子类中生效的。
	class C:
        __slots__ = ['x','y']	//列表的元素是'类可以使用的属性名称'
        def __init__(self,x):
            self.x = x
    c = C(250)	//这里就创建了一个属性受限制的对象c
    c.x → 250
    c.y = 520
    z.z → AttributeError,会报错,因为属性只能由x和y;不允许额外添加属性
    
## magic ##
事实上,对象是由__new__(cls[,.......])方法来创建的,在__init__()函数之前被调用

## 类方法 ##⭐⭐
通过@classmathod装饰器创建的。是一种绑定到类的方法,非类的实例。类方法的第一个参数通常是cls,提供了对类本身的引用。它们不访问或修改实例的状态,但可以访问和修改类的状态。
例如：
class Person:
    #类变量,用于记录所有实例的个数
    person_count = 0
    
    def __init__(self,name):
        self.name = name	#这里的name是实例变量
        Person.person_count +=1		#通过类名访问类变量
        
    @classmethod	#装饰器,指明这是一个类方法.
    def get_person_count(cls):	
        return cls.person_count			
        
    @classmethod
    def create_from_name(cls, name):
    	return cls(name)	#用于创建新的Person实例,参数name会传给__init__来创建新的实例
        
person1 = Person('Alice')	#直接用类名实例化,简单明了
person2 = Person.create_from_name('Bob') #用类方法实例化,允许创建实例时加入额外的逻辑处理


## 静态方法 ##⭐⭐
通过@staticmethod装饰器创建的。不能直接访问实例属性或类属性。
例如：
class Math:
    @staticmethod
    def add(x,y):
        return x+y
    
result_add = Math.add(5,3)	#通过类名调用静态方法
math_instance = Math()	#先通过实例化,再通过实例调用静态方法
re_add = math_instance.add(5,3)

## 类的装饰器 ##⭐⭐
类的装饰是一种修改类或其行为的函数;'类的装饰器'接收一个类对象作为参数,并返回一个修改过的类对象,这用于增强类的功能.

例如：

def decorator(cls):	#定义一个类的装饰器,cls表示实参的对象是类
    def oncall(*args, **kwargs):
        ##被装饰类执行前的代码部分····
        print('start instantiation！')
        instance = cls(*args, **kwargs)	#执行被装饰类,并保存实例
        ##被装饰类执行后的代码部分····
        print('end instantiation！')
        return instance	#返回创建的实例,返回给re实例
    return oncall

@decorator	#相当于 Test=decorator(Test),然后decorator返回oncall函数
class Test:		
    def __init__(self,x,y,z):
        self.x = x
        self.y = y
        self.z = z
        print('function is going now！~')
        
re = Test(1,2,3)	#实例化Test类, 相当于 oncall(1,2,3)
	↓
"start instantiation！  function is going now！  ~end instantiation！"


### __init_subclass__(cls) ###⭐
作用是加强父类对子类的管理。

例如:
class C:
    def __init_subclass__(cls):	#这是一个类方法
        print('father love you')
        cls.x = 520	#为子类设置了一个类属性x,并赋值为520
        
 class D(C):	#子类D继承父类C
    x = 250
    
result: 当在代码中定义class D(C):后,控制台会立刻打印'father love you',因为D类触发了C类中的 __init_subclass__ 方法,随后D类中类属性x会继承下来,并且x=250会覆盖父类设置的x值
```



一些函数用法

```python
在py中,有关下标的结构遵循左闭右开原则, 即起始位置包含在范围内，结束位置不包含在范围内。

⭐
range()   生成一个数字序列(参数必须时整形)
	--range(stop)	生成一个从0到stop的序列,步长默认1
    --range(start, stop)	生成一个从start到stop的序列,步长默认为1
    --range(start, stop, step)	生成一个从start到stop的序列,步长(间隔)为step
    
is运算符：同一性运算符,用于检验两个变量是否指向同一个对象的运算符
```

