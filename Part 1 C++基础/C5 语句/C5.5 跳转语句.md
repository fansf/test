# C5.5 跳转语句
跳转语句中断当前的执行过程。C++ 语言提供了4种跳转语句：
- `break`
- `continue`
- `goto`
- `return`

本章介绍前三种

## break语句
**break语句（break statement）** 负责终止离它最近的`while`、`do while`、`for`或`switch`语句，并从这些语句之后的第一条语句开始继续执行。

`break`语句只能出现在迭代语句或者`switch`语句内部（包括嵌套在此类循环里的语句或块的内部）。`break`语句的作用范围仅限于最近的循环或者`switch`。

## continue语句
**continue语句（continue statement）** 终止最近的循环中的当前迭代并立即开始下一次迭代。`continue`语句只能出现在`for`、`while`和`do while`循环的内部，或者嵌套在此类循环里的语句或块的内部。和`break`语句类似的是，出现在嵌套循环中的`continue`语句也仅仅作用于离它最近的循环。和`break`语句不同的是，只有当`switch`语句嵌套在迭代语句内部时，才能在`switch`里使用`continue`。

`continue`语句中断当前的迭代，但是仍然继续执行循环。对于`while`或者`do while`语句来说，继续判断条件的值；对于传统的`for`循环来说，继续执行`for`语句头的*express*；而对于范围*for*语句来说，则是用序列中的下一个元素初始化循环控制变量。

## goto语句
**goto语句（goto statement）** 的作用是从goto语句无条件跳转代词同一函数内的另一条语句。

`goto`语句的语法形式是：
```cpp
goto label;
```

其中，*label*是用于标识一条语句的标识符。**带标签语句（labeled statement）** 是一种特殊的语句，在它之前有一个标识符及一个冒号：
```cpp
end: return;
```

标签标识符独立于变量或其他标识符的名字，因此，标签标识符可以和程序中其他实体的标识符使用同一个名字而不会相互干扰。`goto`语句和控制权转向的那条带标签的语句必须位于同一个函数之内。

和`switch`语句类似，`goto`语句也不能将程序的控制权从变量的作用于之外转移到作用域之内：
```cpp
//...
goto end;
int ix = 10;

end:
    //错误：此处的代码需要使用ix，但是goto语句绕过了它的声明
    ix = 42;
```

向后跳过一个已经执行的定义是合法的。跳回到变量定义之前意味着系统将销毁该变量，然后重新创建它：
```cpp
begin:
    int sz = get_size();
    if (sz <= 0)
        goto begin;
    }
```

在上面的代码中，`goto`语句执行后将销毁`sz`。因为跳转到`begin`的动作跨过了`sz`的定义语句，所以`sz`将重新定义并初始化。