c++ reference 和pointer区别？
都是通过操作变量的地址，pointer可以不初始化，但是reference 必须初始化，而且初始化好不能改变。
new 与malloc的区别？
new除了申请内存，还会调用构造函数。
析构函数一般声明成virtual，为什么？
利用virtual函数的多态性，delete基类指针来达到析构子类的目的。
const char* p 与char * const p的区别？
从右往左读。
区分全局变量和局部变量，编译器或者链接器在处理全局和局部变量的时候做了什么操作？
函数内部的非static变量都是局部变量，函数体外部或者static变量全局变量，全局变量编译器需要在data section预留空间，而局部变量生成指令时候只是esp 预留空间，在运行时候stack上才分配。
STL vector::capacity() 和size()区别？vector实现是连续内存？以及内存不够时候怎么增加，可以把int *p = vector[i], 其中p值缓存下来以后使用吗？
不能缓存，应为vector空间不够时候，会reallocate,内存失效。
STL map怎么实现的，如果要把一个对象放到map里，要实现什么接口？
map是内存是红黑树，放到map的对象必须实现“<”的接口。
构造函数可以调用virtual member function吗?为什么?
构造函数不能调用virtual 函数,因为这个时候virtual function table还没初始化好.
构造函数实现时，有函数体和初始化列表 区别，为什么？
构造函数首先调用初始化列表，然后构造函数主体，初始化列表第一为了性能，另外就是有些reference 成员只能在初始化列表里初始化，否则编译错误。
类的成员函数int foo:f() const, 为什么被声明成const函数？
不会更改对象的状态，所有可以应用在const foo对象上。
类的成员变量加修饰符mutible目的是什么？
该变量可以被const函数修改。
多线程中,变量前加volatile目的？
该值可能被外部修改，比如其他线程和设备驱动，防止编译器优化。
c++ name mangling的目的是什么？
区分重载函数。
extern “C” c++ C++函数为什么？
防止c++ name mangling.
为什么有虚拟继承？
防止diamond problem, 基类的多个copy存在子类。
虚拟继承时候，构造函数的调用顺序？
i++, ++i的区别？
一个没有声明任何成员变量的类(EmptyClass)的对象，sizeof(EmptyClass) 是多少？
深入了解c++对象模型系列
类对象大小受三个因素影响?
virtual base和virtual function带来的vptr影响
空基类优化处理,EBC（Empty Base Class）占用一个字节，其他含有数据成员的从EBC派生的派生类，只会算自己数据成员的大小，不受EBC一字节的影响
alignment 字节对齐
vtable的内容？
virtual class offset（有虚基类才有)
topoffset
typeinfo
继承基类所声明的虚函数实例，或者是覆盖（override）基类的虚函数
新的虚函数（或者是纯虚函数占位）
执行期虚函数调用步骤
通过vptr找到vtbl
通过thunk技术以及topoffset调整this指针（因为成员函数里面可能调用了成员变量）
通过virtual class offset找到虚基类共享部分的成员
执行vtbl中对应slot的函数
函数性能:Inline Member > (Nonmember Friend, Static Member, Nonstatic Member) > Virtual Member > Virtual Member(多重继承) > Virtual Member(虚拟继承)
B虚拟继承A, C虚拟继承A, D继承A和C, D的内存布局，虚函数表等内容？
