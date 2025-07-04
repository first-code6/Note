#### 变量申明

使用：变量类型 + 变量名 = 默认值
```cpp
#include <iostream>
using namespace std;

int main() {
	int a = 10;

	cout << "Hello Another!" << a;
}
```

#### 定义函数

使用：返回值类型 + 函数名 (形参)
描述：注意，和js的函数定义不同，C++的函数定义非常注意前后顺序，如果想函数在main函数后定义，那么需要在开头先定义函数，否则不需要。
```cpp
#include <iostream>
using namespace std;

int max(int num1, int num2);

int main() {
	int a = 0;
	int b = 0;

	cout << "请输入第一个数字：";
	cin >> a;
	cout << "请输入第二个数字：";
	cin >> b;
	cout << "最大的数字是" << max(a, b) << endl;
}

int max(int num1, int num2) {
	int result;

	if (num1 > num2) {
		result = num1;
	}
	else {
		result = num2;
	}

	return result;
};
```

#### 跨文件使用函数

在普通使用中，一般肯定不会在同一个文件中定义所有的函数，所以一般会在不同的cpp文件中写入不同需求的函数，只需在main文件中定义该函数并在其他文件写入函数即可
1. 最基本的写法
>another.cpp
```cpp
// another.cpp
#include <iostream>
using namespace std;

void max() {
	int result;
	int a = 0;
	int b = 0;

	cout << "请输入第一个数字：";
	cin >> a;
	cout << "请输入第二个数字：";
	cin >> b;

	if (a > b) {
		result = a;
	}
	else {
		result = b;
	}

	cout << "最大的数字是" << max(a, b) << endl;

};

```
>main.cpp
```cpp
#include<iostream>
using namespace std;
void max()

int main() {
	max();
}
```
2. 标准写法
在试用中如果文件过多，许多地方都需要使用的时候，上面的方法会异常复杂，所以一般标准使用是新建一个.h头文件然后将需要使用的函数在该处定义

>another.cpp

**如上**

>another.h
```cpp
void max();
```
>main.cpp
```cpp
#include "another.h"

int main() {
	max();
}
```

#### 数组
##### 声明数组

和声明变量类似
`type arrayName [ arraySize ];`
这叫做一维数组。**arraySize** 必须是一个大于零的整数常量，**type** 可以是任意有效的 C++ 数据类型。
```cpp
void arryTest() {
	// 五个单位的int类型的数组(并且默认值全部复制为0)
	int firstIntArry[5]{};
	// 5个单位的double类型的数组
	double firstDoubleArry[] = {1.0, 53.1, 12.0, 12.4, 11.7};

	// 给int数组赋值
	for (int i = 0; i < 5; i++) {
		firstIntArry[i] = i + 1;
	}

	for (int i = 0; i < 5; i++) {
		cout << "第" << i + 1 << "个数据为   " << "整数：" << firstIntArry[i];
		cout << "   小数：" << firstDoubleArry[i] << endl;
	}
}
```

##### 多维数组

相对于一维数组，还有二维，三维数组等
```cpp
void arryTest1() {
	// 初始化二维数组
	int firstIntArry[5][5]{};
	double firstDoubleArry[5][5] = {
		{1.1, 1.2, 1.3, 1.4, 1.5},
		{2.1, 2.2, 2.3, 2.4, 2.5},
		{3.1, 3.2, 3.3, 3.4, 3.5},
		{4.1, 4.2, 4.3, 4.4, 4.5},
		{5.1, 5.2, 5.3, 5.4, 5.5},
	};

	for (int i = 0; i < 5; i++) {
		cout << "二维数组第"<<  i << "行数据： || ";
		for (int z = 0; z < 5; z++) {
			cout << firstIntArry[i][z] << "  " << firstDoubleArry[i][z] << " || ";
		}
		// 换行
		cout << endl;
	}
}
```

#### 指针

指针，C++的重点。

通过指针，可以简化一些 C++ 编程任务的执行，还有一些任务，如动态内存分配，没有指针是无法执行的。

##### 指针的基本使用
1. & 获取变量的内存地址
2. \* 指针，也可以说，获取变量内存地址中的数据
```cpp
void pointerTest(){
	int num = 10;				// 定义int变量
	int* numPointer{};			// 定义int指针

	numPointer = &num;			// 将int变量的地址赋值给指针

	//打印指针和指针的数据
	cout << "num:" << num << " || munaddress:" << numPointer << " || addressData:" << *numPointer;

}
```

#### 结构体

[C++ 结构体(struct)](https://www.runoob.com/cplusplus/cpp-struct.html)
##### 结构体基础

结构体类似对象

首先先定义结构体，然后将结构体像数据类型一样使用，在插入字符串数据时需使用\<cstring\>库中的strcpy_s函数
```cpp
void stractTest() {
	//定义结构体
	struct books
	{
		char tktle[50];
		char authot[20];
		int book_id;
	};
	
	books myBook{};
	books hisBook{};

	strcpy_s(myBook.tktle, "肖生客的救赎");
	strcpy_s(myBook.authot, "未知");
	myBook.book_id = 1;

	cout << "第一本书的名字：" << myBook.tktle << endl;
	cout << "第一本书的作者：" << myBook.authot << endl;
	cout << "第一本书的id：" << myBook.book_id << endl << endl;

	cout << "第二本书的名字：" << hisBook.tktle << endl;
	cout << "第二本书的作者：" << hisBook.authot << endl;
	cout << "第二本书的id：" << hisBook.book_id << endl;

}
```

##### 指向结构的指针

您可以定义指向结构的指针，方式与定义指向其他类型变量的指针相似，如下所示：
```cpp 
struct Books *struct_pointer;
```

调用数据时候就不应使用 `.` 了，转而使用 `->` 调用函数。
```cpp
#include <iostream>
#include <string>
 
using namespace std;
 
// 声明一个结构体类型 Books 
struct Books
{
    string title;
    string author;
    string subject;
    int book_id;
 
    // 构造函数
    Books(string t, string a, string s, int id)
        : title(t), author(a), subject(s), book_id(id) {}
};
 
// 打印书籍信息的函数，接受一个指向 Books 结构体的指针
void printBookInfo(const Books* book) {
    cout << "书籍标题: " << book->title << endl;
    cout << "书籍作者: " << book->author << endl;
    cout << "书籍类目: " << book->subject << endl;
    cout << "书籍 ID: " << book->book_id << endl;
}
 
int main()
{
    // 创建两本书的对象
    Books Book1("C++ 教程", "Runoob", "编程语言", 12345);
    Books Book2("CSS 教程", "Runoob", "前端技术", 12346);
 
    // 使用指针指向这两本书的对象
    Books* ptrBook1 = &Book1;
    Books* ptrBook2 = &Book2;
 
    // 输出书籍信息，传递指针
    printBookInfo(ptrBook1);
    printBookInfo(ptrBook2);
 
    return 0;
}
```

#### 类
类是 C++ 的核心特性，通常被称为用户定义的类型。

类用于指定对象的形式，是一种用户自定义的数据类型，它是一种封装了数据和函数的组合。类中的数据称为成员变量，函数称为成员函数。类可以被看作是一种模板，可以用来创建具有相同属性和行为的多个对象。

定义一个类需要使用关键字 class，然后指定类的名称，并类的主体是包含在一对花括号中，主体包含类的成员变量和成员函数。

定义一个类，本质上是定义一个数据类型的蓝图，它定义了类的对象包括了什么，以及可以在这个对象上执行哪些操作。

```cpp
// 定义类
class Box
{
   public:
      double length;   // 盒子的长度
      double breadth;  // 盒子的宽度
      double height;   // 盒子的高度
};

// 使用类
Box Box1;          // 声明 Box1，类型为 Box
Box Box2;          // 声明 Box2，类型为 Box

// 使用变量
Box1.length
```

##### **实例**

>boxClass.h

```cpp
#include <iostream>
using namespace std;

class Box2D
{

protected:
	float longNum;
	float width;

public:

	void setData(float longNumD, float widthD);
	void printArear();
	Box2D();
	~Box2D();

};


class Box3D : public Box2D
{

protected:
	float height;

public:
	Box3D();
	~Box3D();
	void setHData(float heightData);
	float printV();

};
```

>BoxClass.cpp

```cpp
#include "BoxClass.h"

/*-------------------Box2D-------------------*/

Box2D::Box2D()
{
	longNum = 10;
	width = 10;
	cout << "盒子长度和宽度已经设置为10。" << endl;
}

Box2D::~Box2D()
{
	cout << "清除2D盒子。" << endl;
}

void Box2D::setData(float longNumD, float widthD) {
	longNum = longNumD;
	width = widthD;
}

void Box2D::printArear() {
	cout << "面积为：" << longNum * width << endl;
}

/*------------------Box3D------------------*/

Box3D::Box3D()
{
	height = 1;
	cout << "创建Box3D。默认高度为1" << endl;
}

Box3D::~Box3D()
{
	cout << "删除Box3D。" << endl;
}

void Box3D::setHData(float heightData)
{
	height = heightData;
}

float Box3D::printV()
{
	return longNum * width * height;
}
```

##### 类的访问修饰符（访问权限）
1. public:公有成员
**公有成员**在程序中类的外部是可访问的。您可以不使用任何成员函数来设置和获取公有变量的值，如下所示：
2. private:私有成员
**私有成员**变量或函数在类的外部是不可访问的，甚至是不可查看的。只有类和友元函数可以访问私有成员。
默认情况下，类的所有成员都是私有的。例如在下面的类中，**width** 是一个私有成员，这意味着，如果您没有使用任何访问修饰符，类的成员将被假定为私有成员：
```cpp
class Box
{
   double width;
   public:
      double length;
      void setWidth( double wid );
      double getWidth( void );
};
```
3. protected:受保护成员
**受保成员**变量或函数与私有成员十分相似，但有一点不同，protected（受保护）成员在派生类（即子类）中是可访问的。
```cpp
#include <iostream>
using namespace std;
 
class Box
{
   protected:
      double width;
};
 
class SmallBox:Box // SmallBox 是派生类
{
   public:
      void setSmallWidth( double wid );
      double getSmallWidth( void );
};
 
// 子类的成员函数
double SmallBox::getSmallWidth(void)
{
    return width ;
}
 
void SmallBox::setSmallWidth( double wid )
{
    width = wid;
}
 
// 程序的主函数
int main( )
{
   SmallBox box;
 
   // 使用成员函数设置宽度
   box.setSmallWidth(5.0);
   cout << "Width of box : "<< box.getSmallWidth() << endl;
 
   return 0;
}
```

##### 继承

有public, protected, private三种继承方式，它们相应地改变了基类成员的访问属性。

- **public 继承**：基类 public 成员，protected 成员，private 成员的访问属性在派生类中分别变成：public, protected, private
- **protected 继承**：基类 public 成员，protected 成员，private 成员的访问属性在派生类中分别变成：protected, protected, private
- **private 继承**：基类 public 成员，protected 成员，private 成员的访问属性在派生类中分别变成：private, private, private

但无论哪种继承方式，下面两点都没有改变：
-  private 成员只能被本类成员（类内）和友元访问，不能被派生类访问；
-  protected 成员可以被派生类访问。

>public继承
```cpp
#include<iostream>
#include<assert.h>
using namespace std;
 
class A{
public:
  int a;
  A(){
    a1 = 1;
    a2 = 2;
    a3 = 3;
    a = 4;
  }
  void fun(){
    cout << a << endl;    //正确
    cout << a1 << endl;   //正确
    cout << a2 << endl;   //正确
    cout << a3 << endl;   //正确
  }
public:
  int a1;
protected:
  int a2;
private:
  int a3;
};
class B : public A{
public:
  int a;
  B(int i){
    A();
    a = i;
  }
  void fun(){
    cout << a << endl;       //正确，public成员
    cout << a1 << endl;       //正确，基类的public成员，在派生类中仍是public成员。
    cout << a2 << endl;       //正确，基类的protected成员，在派生类中仍是protected可以被派生类访问。
    cout << a3 << endl;       //错误，基类的private成员不能被派生类访问。
  }
};
int main(){
  B b(10);
  cout << b.a << endl;
  cout << b.a1 << endl;   //正确
  cout << b.a2 << endl;   //错误，类外不能访问protected成员
  cout << b.a3 << endl;   //错误，类外不能访问private成员
  system("pause");
  return 0;
}
```
>protected继承
```cpp
#include<iostream>
#include<assert.h>
using namespace std;
class A{
public:
  int a;
  A(){
    a1 = 1;
    a2 = 2;
    a3 = 3;
    a = 4;
  }
  void fun(){
    cout << a << endl;    //正确
    cout << a1 << endl;   //正确
    cout << a2 << endl;   //正确
    cout << a3 << endl;   //正确
  }
public:
  int a1;
protected:
  int a2;
private:
  int a3;
};
class B : protected A{
public:
  int a;
  B(int i){
    A();
    a = i;
  }
  void fun(){
    cout << a << endl;       //正确，public成员。
    cout << a1 << endl;       //正确，基类的public成员，在派生类中变成了protected，可以被派生类访问。
    cout << a2 << endl;       //正确，基类的protected成员，在派生类中还是protected，可以被派生类访问。
    cout << a3 << endl;       //错误，基类的private成员不能被派生类访问。
  }
};
int main(){
  B b(10);
  cout << b.a << endl;       //正确。public成员
  cout << b.a1 << endl;      //错误，protected成员不能在类外访问。
  cout << b.a2 << endl;      //错误，protected成员不能在类外访问。
  cout << b.a3 << endl;      //错误，private成员不能在类外访问。
  system("pause");
  return 0;
}
```
>private继承
```cpp
#include<iostream>
#include<assert.h>
using namespace std;
class A{
public:
  int a;
  A(){
    a1 = 1;
    a2 = 2;
    a3 = 3;
    a = 4;
  }
  void fun(){
    cout << a << endl;    //正确
    cout << a1 << endl;   //正确
    cout << a2 << endl;   //正确
    cout << a3 << endl;   //正确
  }
public:
  int a1;
protected:
  int a2;
private:
  int a3;
};
class B : private A{
public:
  int a;
  B(int i){
    A();
    a = i;
  }
  void fun(){
    cout << a << endl;       //正确，public成员。
    cout << a1 << endl;       //正确，基类public成员,在派生类中变成了private,可以被派生类访问。
    cout << a2 << endl;       //正确，基类的protected成员，在派生类中变成了private,可以被派生类访问。
    cout << a3 << endl;       //错误，基类的private成员不能被派生类访问。
  }
};
int main(){
  B b(10);
  cout << b.a << endl;       //正确。public成员
  cout << b.a1 << endl;      //错误，private成员不能在类外访问。
  cout << b.a2 << endl;      //错误, private成员不能在类外访问。
  cout << b.a3 << endl;      //错误，private成员不能在类外访问。
  system("pause");
  return 0;
}
```

##### 构造函数&解析函数
###### **构造函数**

类的**构造函数**是类的一种特殊的成员函数，它会在每次创建类的新对象时执行。
构造函数的名称与类的名称是完全相同的，并且不会返回任何类型，也不会返回 void。构造函数可用于为某些成员变量设置初始值。

 ###### **解析函数**
 
类的**析构函数**是类的一种特殊的成员函数，它会在每次删除所创建的对象时执行。
析构函数的名称与类的名称是完全相同的，只是在前面加了个波浪号（~）作为前缀，它不会返回任何值，也不能带有任何参数。析构函数有助于在跳出程序（比如关闭文件、释放内存等）前释放资源。

###### 示例
```cpp
#include <iostream>
 
using namespace std;
 
class Line
{
   public:
      void setLength( double len );
      double getLength( void );
      Line();   // 这是构造函数声明
      ~Line();  // 这是析构函数声明
 
   private:
      double length;
};
 
// 成员函数定义，包括构造函数
Line::Line(void)
{
    cout << "Object is being created" << endl;
}
Line::~Line(void)
{
    cout << "Object is being deleted" << endl;
}
 
void Line::setLength( double len )
{
    length = len;
}
 
double Line::getLength( void )
{
    return length;
}
// 程序的主函数
int main( )
{
   Line line;
 
   // 设置长度
   line.setLength(6.0); 
   cout << "Length of line : " << line.getLength() <<endl;
 
   return 0;
}
```

##### 复制构造函数

##### 友元函数

##### 内联函数

##### this指针

在 C++ 中，**this** 指针是一个特殊的指针，它指向当前对象的实例。

在 C++ 中，每一个对象都能通过 **this** 指针来访问自己的地址。

**this**是一个隐藏的指针，可以在类的成员函数中使用，它可以用来指向调用对象。

当一个对象的成员函数被调用时，编译器会隐式地传递该对象的地址作为 this 指针。

友元函数没有 **this** 指针，因为友元不是类的成员，只有成员函数才有 **this** 指针。
```cpp
#include <iostream>
 
class MyClass {
private:
    int value;
 
public:
    void setValue(int value) {
        this->value = value;
    }
 
    void printValue() {
        std::cout << "Value: " << this->value << std::endl;
    }
};
 
int main() {
    MyClass obj;
    obj.setValue(42);
    obj.printValue();
 
    return 0;
}
```

