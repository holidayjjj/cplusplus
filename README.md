## 对象和类
类是一种将抽象转换为用户定义类型的C++工具，它将数据表示和操作数据的方法组合成一个整洁的包。  
C++程序员将接口（类定义）放在头文件中，并将实现类方法的代码放在源代码文件中。  
关键词class定义一个类。  
使用类对象的程序可以直接访问公有部分，但只能通过公有成员函数或友元函数来访问对象的私有成员，公有成员函数是程序和对象的私有成员之间的桥梁。  
private是类对象的默认访问控制。  


## 各种库
#### cctype
isalnum()  如果参数是字母数字，即字母或者数字，函数返回true  
isalpha()  如果参数是字母，函数返回true  
iscntrl()  如果参数是控制字符，函数返回true  
isdigit()  如果参数是数字（0－9），函数返回true  
isgraph()  如果参数是除空格之外的打印字符，函数返回true  
islower()  如果参数是小写字母，函数返回true  
isprint()  如果参数是打印字符（包括空格），函数返回true  
ispunct()  如果参数是标点符号，函数返回true  
isspace()  如果参数是标准空白字符，如空格、换行符、水平或垂直制表符，函数返回true  
isupper()  如果参数是大写字母，函数返回true  
isxdigit() 如果参数是十六进制数字，即0－9、a－f、A－F，函数返回true  
tolower()  如果参数是大写字符，返回其小写，否则返回该参数  
toupper()  如果参数是小写字符，返回其大写，否则返回该参数  
*cctype头文件中的常用函数功能主要分为以下两类：*  
* 功能一：字符测试  
* 功能二：字符映射  
#### cstring
