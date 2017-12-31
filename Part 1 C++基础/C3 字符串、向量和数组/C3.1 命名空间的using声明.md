# C3.1 命名空间的using声明
目前为止，我们用到的库函数基本上都属于命名空间`std`，而程序也显式地将这一点标示了出来。例如，`std::cin`表示从标准输入中读取内容。此处使用作用域操作符（`::`）的含义是：编译器应从操作符左侧名字所示的作用域中寻找右侧那个名字。因此，`std::cin`的意思就是要使用命名空间`std`中的名字`cin`。

上面的方法显得比较烦琐，然而幸运的是，通过更简单的途径也能使用到命名空间中的成员。本节我们学习其中一种最安全的方法，也就是使用**using 声明（using declaration）**。

有了`using`声明就无须专门的前缀（形如命名空间`::`）也能使用所需的名字了。  
`using`声明具有如下的形式：
```cpp
using namespace::name;
```

一旦声明了上述语句，就可以直接访问命名空间中的名字了：
```cpp
#include <iostream>
using std::cin;

int main()
{
    int i;
    cin >> i;
    cout << i;        //错误：没有对应的using声明，必须使用完整的名字
    std::cout << i;
    return 0;
}
```

**明个名字都需要独立的using声明**  
按照规定，每个`using`声明引入命名空间中的一个成员。例如，可以把要用到的标准库中的名字都以`using`声明的形式表示出来
```cpp
#include <iostream>
using std::cin;
using std::cout;
using std::endl;

int main()
{
    cout << "Enter two number: " << endl;

    int v1,v2;
    cin >> v1 >> v2;
    cout << "The sum of " << v1 << "and " << v2
         << " is " << v1 + v2 << endl;
    return 0;
}
```

**头文件不应包含using声明**  
位于头文件的代码一般来说不应该使用`using`声明。  
这是因为头文件的内容会拷贝到所有引用它的文件中去，如果头文件里有某个`using`声明，那么每个使用了该头文件的文件就都会有这个声明。对于某些程序来说，由于不经意间包含了一些名字，反而可能产生始料未及的名字冲突。