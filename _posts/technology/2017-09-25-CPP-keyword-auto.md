---
layout:     post
title:      关键字auto的使用
category: 	technology
tag: CPP
description: C++11推出auto，C++14进一步优化。
---

接触到auto就不自觉爱上了233，武器库又多了一样利器。

看个例子：

	#include<iostream>
	int main(void)
	{
	    auto blog = writeBlog(nowthdk.github.io);
	    return 0;
	}

Well，什么也不会发生，开个玩笑。
### 基本用法——隐藏类型#
对于容器，除角标外通常会引入迭代器：

	std::vector<int> vec(10,0);
	std::vector<int>::iterator iter = vec.begin();
	for(;iter != vec.end();++iter)
	{
        //TODO
	}

那么现在可以这么写：

	for(auto iter = vec.begin();iter != vec.end();++iter)
	{
	    //TODO
	}

还不够简洁，这样：

	for(auto member : vec)
	{
	    //TODO
	}

__这里需要说明一下__，member并非指针，而是直接对vec内元素的引用:

	for(auto member : vec)
	{
	    std::cout<< typeid(member).name() <<std::endl;//结合上文，输出结果为int.
	}

同时，对于遍历也失去了一定的便捷性，比如上面的方法不能选择在第二个元素开始操作，或者到倒数第三个元素停止操作。
还是要回到begin()和end()，引入迭代器才能实现自增自减操作。

__值得注意的一点是__，通常内置类型并不推荐使用auto，比如int、bool等，因为降低了程序的可读性。同时，尽管在编程的角度而言有争议，但是编译器允许这样写：

	int a;
	bool b;

而auto则不允许只做声明而不定义：

	auto m = a; //ok
	auto n;		//error

很容易理解，因为auto要首先根据右操作数来决定如何为变量申请内存。

### 函数返回类型#
这个特性是在C++14当中引入的：
	
	auto twoSum(int a,int b)
	{
	    return a + b;
	}
	
	int a = twoSum(1,2); //OK, auto returned an integer type
	auto b = twoSum(1,2); //OK, auto creates b as an interger from return type

那么顺理成章的，对于匿名函数和模板的使用，也可以引入auto了，只是对二者还不能用得很好，本文暂时停在这里。