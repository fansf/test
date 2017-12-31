# 为什么char有三种类型
仅仅从字符的表现形式来说，只有两种：带符号的 和 无符号的。也就是`signed char` 和 `unsigned char`。

`char`类型会表现为以上两种形式，但并不是固定的，具体是哪种类型由编译器决定。

可以用下面的代码测试你的编译器：
```cpp
char test = -1;
printf("test = %d\n",test);
```

如果输出`-1`，则当前编译器将`char`处理成`signed char`  
如果输出`255`，则当前编译器将`char`处理成`unsigned char`

如果你想知道为什么是这个结果，请搜索 ”计算机中的数表示“