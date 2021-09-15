## string
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
