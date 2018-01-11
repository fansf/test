# C4.10 逗号运算符
**逗号运算符（comma operator）** 含有两个运算对象，按照从左向右的顺序依次求值。  
和逻辑与、逻辑或以及条件运算符一样，逗号运算符也规定了运算对象求值的顺序。

对于逗号运算符来说，首先对左侧的表达式求值，然后将求值结果丢弃掉。逗号运算符真正的结果是右侧表达式的值。如果右侧运算对象是左值，那么最终的求值结果也是左值。

逗号运算符经常被用在`for`循环中：
```cpp
vector<int>::size_type cnt = ivec.size();

for (vector<int>::size_type ix = 0;ix != ivec.size();++ix,--cnt)
    ivec[ix] = cnt;
```

