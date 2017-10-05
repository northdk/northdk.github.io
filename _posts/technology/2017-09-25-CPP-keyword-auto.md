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
	int main(void){
		auto blog = writeBlog(nowthdk.github.io);
	}

Well，什么也不会发生，开个玩笑。
### 基本用法——隐藏类型#
对于容器，除角标外通常会引入迭代器：

	vector<Typename> vec;
	vector<Typename>::iterator iter = vec.begin();
	for(;iter != vec.end();++iter){}

那么现在可以这么写：

	auto iter = vec.begin();

还不够简洁，这样：

	for(auto member : vec){}

*需要注意的一点是*，通常内置类型并不推荐使用auto，比如int、bool等，因为降低了程序的可读性。同时，尽管在编程的角度而言有争议，但是编译器允许这样写：

	int a;
	bool b;

而auto则不允许只做声明而不定义：

	auto m = a; //ok
	auto n;		//error

很容易理解，因为auto要首先根据右操作数来决定如何为变量申请内存。