## 对象和类
类是一种将抽象转换为用户定义类型的C++工具，它将数据表示和操作数据的方法组合成一个整洁的包。  
C++程序员将接口（类定义）放在头文件中，并将实现类方法的代码放在源代码文件中。  
关键词class定义一个类。  
使用类对象的程序可以直接访问公有部分，但只能通过公有成员函数或友元函数来访问对象的私有成员，公有成员函数是程序和对象的私有成员之间的桥梁。  
private是类对象的默认访问控制。  

## 标准输入输出  
### cin>> 的用法  
cin 可以连续从键盘读取想要的数据，以空格、tab 或换行作为分隔符，实例如下：  
```cpp
#include <iostream>
using namespace std;
int main() {
	char a;
	int b;
	float c;
	string 
	cin>>a>>b>>c;
	cout<<a<<" "<<b<<" "<<c<<" "<<endl;
	return 0;
}
```
**当 cin>> 从缓冲区中读取数据时，若缓冲区中第一个字符是空格、tab或换行这些分隔符时，cin>> 会将其忽略并清除，继续读取下一个字符，若缓冲区为空，则继续等待。但是如果读取成功，字符后面的分隔符是残留在缓冲区的，cin>> 不做处理。**
### cin.get() 的用法
读取一个字符，可以使用 cin.get() 或者 cin.get(var)，示例代码如下：
```cpp
#include <iostream>
using namespace std;
int main() {
	char a;
	char b;
	a=cin.get();
	cin.get(b);
	cout << a << b <<endl;
	return 0;
}
```
**cin.get() 从输入缓冲区读取单个字符时不忽略分隔符，直接将其读取，输入被缓冲。**
### cin.get() 读取一行
```cpp
istream& get(char* s, streamsize n)
istream& get(char* s, size_t n, streamsize  delim)
```
**二者的区别是前者默认以换行符结束，后者可指定行结束符，n 表示目标空间的大小。**
示例代码如下：
```cpp
#include <iostream>
using namespace std;
int main() {
	char a;
	char array[20]={NULL}; 
	cin.get(array,20);
	cin.get(a);
	cout<<array<<" "<<(int)a<<endl;
	return 0;
}
```
### cin.getline() 读取一行
从标准输入设备键盘读取一串字符串，并以指定的结束符结束。
```cpp
istream& getline(char* s, streamsize count); //默认以换行符结束
istream& getline(char* s, streamsize count, char delim);
```
示例：
```cpp
#include <iostream>
using namespace std;
int main() {
	char array[20]={NULL};
	cin.getline(array,20); //或者指定结束符，使用下面一行
	//cin.getline(array,20,'\n');
	cout<<array<<endl;
	return 0;
}
```
**cin.getline() 与 cin.get() 的区别是，cin.getline() 不会将行结束符（如换行符）残留在输入缓冲区中。cin.get(str,size); 读取一行时，只能将字符串读入 C 风格的字符串中，即 char\*，但是 cin.getline() 函数可以将字符串读入C++ 风格的字符串 string中。鉴于 cin.getline() 较 cin.get() 的这两种优点，建议使用 cin.getline() 读取行。**
### cin 清空输入缓冲区
从上文中可以看出，上一次的输入操作很有可能是输入缓冲区中残留数据，影响下一次输入。那么如何解决这个问题呢？自然而然，我们想到了在进行输入时，对输入缓冲区进行清空和状态条件的复位。条件状态的复位使用 clear()，清空输入缓冲区应该使用 cin.ignore()。  
函数原型：
```cpp
istream &ignore(streamsize num=1, int delim=EOF);
```
函数作用：跳过输入流中 n 个字符，或在遇到指定的终止字符时提前结束（此时跳过包括终止字符在内的若干字符）。
示例如下：
```cpp
#include <iostream>
using namespace std;
int main() {
	char str1[20] = {NULL}, str2[20] = {NULL};
    cin.getline(str1,5);
    cin.clear();  // 清除错误标志
	cin.ignore(numeric_limits<std::streamsize>::max(),'\n'); // 清除缓冲区的当前行
	cin.getline(str2,20);
	cout << "str1:" << str1 << endl;
	cout << "str2:" << str2 << endl;
	return 0;
}
```
其中，numeric_limits<std::streamsize>::max()是<limits>头文件定义的流使用的最大值，也可以用一个足够大的整数代替它。如果想清空输入缓冲区的所有内容，去掉换行符即可：
 ```cpp
  cin.ignore(numeric_limits< std::streamsize>::max());
  ```
  *https://blog.csdn.net/K346K346/article/details/48213811*

## string对象
### 概述
string是C++标准库的一个重要的部分，主要用于字符串处理。可以使用输入输出流方式直接进行string操作，也可以通过文件等手段进行string操作。同时，C++的算法库对string类也有着很好的支持，并且string类还和c语言的字符串之间有着良好的接口。  
### string转换为char*
```cpp
#include <string>
#include <iostream>
#include <stdio.h>
using namespace std;
int main()
{
    string strOutput = "Hello World";
    cout << "[cout] strOutput is: " << strOutput << endl;
    // string 转换为 char*
    const char* pszOutput = strOutput.c_str();
    printf("[printf] strOutput is: %s\n", pszOutput);
    return 0;
}
 ```
**cout 可直接输出 string 类的对象的内容；**  
**使用 c_str() 方法转换 string 类型到 char\* 类型时，需要为char\*添加 const 关键字；**  
**printf() 函数不能直接打印 string 类的对象的内容，可以通过将 string 转换为 char\* 类型，再使用 printf() 函数打印。**  
### 计算string长度、string字符串比较
```cpp
#include <string>
#include <iostream>
#define HELLOSTR "Hello World"
using namespace std;
int main()
{
    string strOutput = "Hello World";
    int nLen = strOutput.length();
    cout << "the length of strOutput is: " << nLen << endl;
    if (0 == strOutput.compare(HELLOSTR))
    {
        cout << "strOutput equal with macro HELLOSTR" << endl;
    }
    return 0;
}
```
**string类型可直接使用 length() 方法计算字符串长度，该方法计算结果为字符串的实际长度，如本例中"Hello World"字符串的长度为11；**   
**string类型可使用 compare(const string& str) 方法进行字符串比较。**  
### string对象判空
可使用 empty() 方法对string类型的对象进行判空，如下：  
```cpp
    if (str2.empty())
    {
        cout << "str2 is empty." << endl;
    }
```
### char*、char[]转换为string
将 char*、char[] 转换为 string 类型时，直接进行赋值操作，将 char*、char[] 的变量赋值给 string 对象即可。  
**这里所说的“赋值”操作，实际上是将 char\*、char[] 定义的字符串的首地址赋值给 string 对象了。**
```cpp
#include <string>
#include <iostream>
using namespace std;
int main()
{
    const char* pszName = "liitdar";
    char pszCamp[] = "alliance";
    string strName;
    string strCamp;
    strName = pszName;
    strCamp = pszCamp;
    cout << "strName is: " << strName << endl;
    cout << "strCamp is: " << strCamp << endl;
    return 0;
}
```
### string类的find方法
使用string类的find方法，在字符串中检索自字符串是否存在。  
**https://blog.csdn.net/liitdar/article/details/80498634**
