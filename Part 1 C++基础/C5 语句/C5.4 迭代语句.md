# C5.4 迭代语句
迭代语句通常称为循环，它重复执行操作直到满足某个条件才停下来。`while`和`for`语句在执行循环体之前检查条件，`do while`语句先执行循环体，然后才检查条件。

## while语句
只要条件为真，**while语句（while statement）** 就重复地执行循环体，它的语法形式是：
```cpp
while (condition)
    statement
```

在`while`结构中，只要*condition*的求值结果为真就一直执行*statement*（常常是一个块）。*condition*不能为空，如果*condition*第一次求值就得到`false`，*statement*一次都不执行。

`while`的条件部分可以是一个表达式或者是一个带初始化的变量声明。通常来说，应该有条件本身或者循环体设法改变表达式的值，否则循环可能无法终止。

### 使用while循环
当不确定到底要迭代多少次时，使用`while`循环比较合适，比如读取输入的内容就是如此。还有一种情况也应该使用`while`循环，就是我们想在循环结束后访问循环控制变量。例如：
```cpp
vector<int> v;
int i;
while (cin >> i)
    v.push_back(i);

auto beg = v.begin();
while (beg != v.end() && *beg >= 0)
    ++beg;
if (beg == v.end())
    //此时我们知道v中所有元素都大于等于0
```

第一个循环从标准输入中读取数据，我们一开始不清楚循环要执行多少次，当`cin`读取到无效数据、遇到其他一些输入错误或是达到文件末尾时循环条件失效。第二个循环重复执行直到到遇到一个负值为止，循环终止后，`beg`或者等于`v.end()`，或者指向`v`中一个小于`0`的元素。可以再`while`循环外继续使用`beg`的状态以进行其他处理。

## 传统的for语句
**for 语句** 的语法形式是：
```cpp
for (init-statement;condition;expression)
    statement
```

关键字`for`及括号里的部分称作`for`语句头。

*init-statement*必须是以下三种形式中的一种：
- 声明语句
- 表达式语句
- 空语句

因为这些语句都以分号作为结束，所以`for`语句的语法形式也可以看作：
```cpp
for (initializer;condition;expression)
    statement
```

一般情况下，`init-statement`负责初始化一个值，这个值将随着循环的进行而改变。*condition*作为循环控制的条件，只要*condition*为真，就执行一次*statement*。如果*condition*第一次的求值结果就是`false`，则*statement*一次也不会执行。*expression*负责修改*init-statement*初始化的变量，这个变量正好就是*condition*检查的对象，修改发生在每次循环迭代之后。*statement*可以是一条单独的语句也可以是一条复合语句。

### for语句头中的多重定义
和其他声明一样，*init-statement*也可以定义多个对象。但是*init-statement*只能有一条声明语句，因此，所有变量的基础类型必须相同。

### 省略for语句头的某些部分
`for`语句头能省略掉*init-statement*、*condition*和*expression*中的任何一个（或者全部）。

如果无须初始化，则我们可以使用一条空语句作为*init-statement*。

省略*condition*的效果等价于在条件部分写了一个`true`。

如果省略`for`语句头中的*express*，但是在这样的循环中就要条件部分或者循环体必须改变迭代变量的值

## 范围for语句
C++11 新标准引入了一种更为简单的`for`语句，这种语句可以遍历容器或其他序列的所有元素。**范围for语句（range for statement）** 的语法形式是：
```cpp
for (declaration : expression)
    statement
```

*expression*表示的必须是一个序列，比如用花括号括起来的初始值列表、数组或者`vector`或`string`等类型的对象，这些类型的共同特点是拥有能返回迭代器的`begin`和`end`成员。

*declaration*定义一个变量，序列中的每一个元素都得转换成该变量的类型。确保类型相容最简单的办法就是使用`auto`类型说明符，这个关键字可以令编译器帮助我们指定合适的类型。如果需要对序列中的元素执行写操作，循环变量必须声明成引用类型。

每次迭代都会重新定义循环控制的变量，并将其初始化成序列中的下一个值，之后才会执行*statement*。像往常一样，*statement*可以是一条单独的语句也可以是一个块。所有元素都处理完毕后循环终止。

学习了范围`for`语句的原理后，我们也就不难理解为什么要强调不通过范围`for`语句中增加`vector`对象（或者其他容器）的元素了。在范围`for`语句中，预存了`end()`的值。一旦在序列中添加（删除）元素，`end`函数的值就可能变得无效了。

## do while 语句
**do while语句（do while statement）** 和 **while** 语句非常相似，唯一的区别是，**do while**语句先执行循环体后检查条件。不管条件的值如何，我们都至少执行一次循环。**do while** 语句的语法形式如下所示：
```cpp
do
    statement
while (condition);
```

在`do`语句中，求*condition*的值之前首先执行一次*statement*，*condition*不能为空。如果*condition*的值为假，循环终止；否则，重复循环过程。*condition*使用的变量必须定义在循环体之外。
