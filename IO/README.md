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
