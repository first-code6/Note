#### strcpy_s()函数
原型声明：char \*strcpy(char\* dest, const char \*src);

头文件：#include <string.h> 和 \#include <stdio.h>

功能：把从src地址开始且含有NULL结束符的字符串复制到以dest开始的地址空间

和strcpy的区别：strcpy函数，就象gets函数一样，它没有方法来保证有效的缓冲区尺寸，所以它只能假定缓冲足够大来容纳要拷贝的字符串。在程序运行时，这将导致不可预料的行为。用strcpy_s就可以避免这些不可预料的行为。这个函数用两个参数、三个参数都可以，只要可以保证缓冲区大小。

三个参数时：
errno_t strcpy_s( char \*strDestination, size_t numberOfElements, const char \*strSource );
两个参数时：
errno_t strcpy_s( char (&strDestination)\[size\], const char \*strSource );

当写入的变量为指针的时候需要三个参数
```cpp

void Test(void)
{
	char *str1=NULL;
	str1=new char[20];
	char str[7];
	//三个参数
	strcpy_s(str1,20,"hello world");
	//两个参数但如果：char *str=new char[7];会出错：提示不支持两个参数
	strcpy_s(str,"hello");
	cout<<"strlen(str1)"<<strlen(str1)<<"strlen(str)"<<strlen(str)<<endl;
	printf(str1);printf("\n");
	cout<<str<<endl;
}
```