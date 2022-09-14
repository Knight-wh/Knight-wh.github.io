# 代码笔记

## 类的常量成员赋值

C++规定：对象的成员变量初始化动作发生在进入构造函数本体之前。

```cpp
class PP
{
    PP(int& p);
    ~PP() {};
private:
    int ppp;
    const int x;
};

PP::PP(int& p):
    x(p)
{
    ppp = p;
}
```

程序优化：在上面例子中，`x`在初始化列表中被初始化，而`ppp`在构造函数本体中被赋值。前者采用拷贝构造一步到位，而后者先调用默认构造函数初始化，再调用赋值操作符，增大了开销。对于内置类型，如`int`,初始化与赋值差别不大。

**应尽可能在成员变量初始化列表中完成初始化**

[类成员变量的赋值与初始化](https://blog.csdn.net/qq575787460/article/details/7873224)

## 类的成员函数后加const

加const表明这个函数不会对这个类对象的数据成员（准确地说是非静态数据成员）作任何改变、
在设计类的时候，一个原则就是对于不改变数据成员的成员函数都要在后面加 const，而对于改变数据成员的成员函数不能加 const。所以 const 关键字对成员函数的行为作了更加明确的限定：有 const 修饰的成员函数（指 const 放在函数参数表的后面，而不是在函数前面或者参数表内），只能读取数据成员，不能改变数据成员；没有 const 修饰的成员函数，对数据成员则是可读可写的。

[void display() const中的const是什么意思？](https://blog.csdn.net/bugaosuonia/article/details/19999403)

## 智能指针shared_ptr

[【C++11】 之 std::unique_ptr 详解](https://blog.csdn.net/lemonxiaoxiao/article/details/108603916)

```cpp
std::shared_ptr<int> p = std::make_shared<int>(10);
std::unique_ptr<int> u = std::make_unique<int>(10);
```

使用`std::move()`在容器中存放智能指针可以提高效率

## 容器vector::swap()

交换两个容器的内容，可以用来收缩内存空间。

[C++ vector容器的swap方法（容器互换）](https://blog.csdn.net/qq_41929943/article/details/103190891)

## 引用和指针的区别

对象指的是一块能存储数据并具有某种类型的内存空间。

- 指针本身就是一个对象，允许对指针进行赋值和拷贝，而在指针的生命周期内它可以先后指向几个不同的对象。
- 指针无须在定义时赋初值。和其他内置类型一样，在块作用域内定义的指针如果没有被初始化，也将拥有一个不确定的值。

- 引用本身不是一个对象，只是绑定在对象上。引用即别名。一旦定义引用，就无法令其再绑定到另外的对象。
- 引用必须初始化。
- 对引用的所有**操作**都是在**与之绑定的对象上**进行的。

```cpp
int* x, y;
//x是指向int的指针，y是int
```
在C++中加入引用的主要目的是为了给函数传参。在C语言中，将变量名作为实参，那么将变量的值传递给形参。这种传递是单向的，在调用函数时，形参和实参不是用一个存储单元。执行函数期间形参值发生变化并不传递回实参。
而引用（即别名）与他所引用的对象共用同一块内存空间，在函数中直接改变引用的值，原变量的值也会随之改变。

```cpp
void change(int x)
{
    x++;
}
void change2(int& x)
{
    x++;
}
void main()
{
    int x = 3;
    change(x);//x的值不发生变化
    change2(x);//x的值加一
}
```

### 常引用

在引用之前加上const对引用进行限制，使得引用在函数中不能进行改变，但原变量的值可以改变

```cpp
int a = 3;
const int &b = a;
b = 1; //改变常引用b的值，错误
a = 4; // change a, correct
```

**常引用通常作为函数形参，这样能保证形参在函数内不被改变。可以减少开销**

[c++中常引用const int &a的介绍](https://blog.csdn.net/donnieliu/article/details/123316214)

---

c++11：允许将变量声明为constexpr类型以便由编译器来验证变量的值是否是一个常量表达式。声明为constexpr的变量一定是一个常量，而且必须使用常量表达式初始化。

## 一些小记录

```cpp
double j = 0;
int i = static_cast<size_t>(j);
```
`static_cast<>()` C++中的强制类型转换