### 初始化数据
1. 变量的定义
在使用中一般不会定义两个变量在一行。
```cpp
int a, b;
```
这样会严重影响可读性，一般我们会分开。
```cpp
int a;
int b;
```
2. 初始化变量
在使用中，我们常常会尚未初始化一个变量的时候就使用该变量
```cpp
int a;
int c;
int b = a + c;
```
如果你写一个大型项目，你声明了很多变量却没有初始化，一旦程序需要调用它们，那么将引发程序的Error。  
为了避免这种低级错误，我们要随时坚持一个原则，这个原则就是一旦声明了一个变量，便立即初始化它，随便赋给它一个值，也好过引发“使用未初始化变量”的错误。

在 `C++ 17`标准下，我们通过如下语句初始化
```cpp
int a{};
printf("%d", a);
```
以上代码的意思是把{ int a }初始化为0。

### .h文件
一般.h文件都会存放一些类和结构体的定义，以及文件的索引，并且不一定需要导入到含有main函数的文件中调用，可在其他文件引入.h文件使用。

注：
- .h文件中不可以定义Class的函数，这样做会使得其他文件只有一个文件可以调用Clss。
- 正确做法应该为定义一个.h文件，再定义同名.cpp文件在cpp文件中定义Class函数。

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