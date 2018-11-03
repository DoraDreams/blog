title: 'c|c++中使用const void *'
date: 2016-03-20 19:42:05
categories: c/c++
---

关于在c语言中使用const关键字的说明

## 指针
在指针中使用const，比如const void *p，就意味着p is a pointer to const xx.也就是说p指向的位置的值不可改变（这里面有层含义是说通过使用*（type *）的时候不可改变，但是使用原来的引用还是可以更改的，同时你也可以更改指针的指向。同时使用const void *p的指针，使用int *p1 = p时不能隐式转换，需要使用cast。

当时用int * const a时说明a是个const不可改变，其实这也很好理解，只要按照c语言的优先顺序即可理解。

我们一般使用const void *p比较多，特别是在用c写自己的数据结构时。笔者再用c写数据结构时，就发现许多的实现方法中都有const void *的写法。

## 变量
在变量前面加上const，就是类似于int * const a。


##总结：
其实对于这个不用那么纠结，这一般使用的都是const void *。转换的时候需要显示转换。这点要注意。