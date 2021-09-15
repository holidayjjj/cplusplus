## C++基本数据类型
#### 变量名
字母字符、数字和下划线，区分大小写，名称第一个字符不能是数字  
以两个下划线开头或以下划线和大写字母开头的名称被保留给实现（编译器及其使用起源）  
以一个下划线开头的名称将保留给实现，用作全局标识符  
#### 整形（*char属于整形*）、浮点型
bool、char、signed char、unsigned char、short、unsigned short、int、unsigned int、long、unsigned long、wchar_t  
short至少为16位，int至少和short一样长，long至少32位，且至少和int一样长，确切长度取决于实现。  
```cpp
#include <iostream>
{
  using namespace std;
  char ch = 'M';
  int i = ch;
  cout<<"The ASCII code for "<<ch<<" is "<<i<<endl;
  ch = ch + 1;
  i = ch;
  cout<<"The ASCII code for "<<ch<<" is "<<i<<endl;
  return 0;
}
```
```cpp
char ch;
cin>>ch;
```
如果输入5，上述代码将读取字符“5”，并将其对应字符编码（ASCII为53）存储在变量ch中。  
```cpp
int n;
cin>>n;
```
如果输入5，上述代码将读取字符“5”，将其转换为相应的数字值5，存储在变量n中。  
#### 转义字符
#### 符号常量--预处理器方式
#### 初始化
```cpp
int owls = 100;
int wrens(432);
int hamburgers = {24};
int emus{7};
int rocs{};  //初始化为0
```
#### 运算符优先级和结合性
#### 类型转换
#### auto声明
编译器根据初始值类型判断变量的类型
```cpp
auto n = 100;
auto x = 1.5;
auto y = 1.3e12L;
auto z = 0.0;  //double
auto w = 0;   //int

std::vector<double> scores;
std::vector<double>::iterator pv = scores.begin();    //C++98
auto pv = scores.begin();    //C++11
```
## 复合类型
#### 数组
```cpp
typeName arrayName[arraySize];
int cards[4] = {3, 6, 8, 10};   //okay
int hand[4]                     //okay
hand[4] = {5, 6, 7, 90};        //not allowed
hand = cards;                   //not allowed
double earnings[4] {1.2e4, 1.6e4, 1.1e4, 1.7e4};    //okay with C++11
unsigned int counts[10] = {};       //all elements set to 0
long plifs[] = {25, 92, 3.0};       //not allowed
char slifs[4] {'h', 'i', 1122011, '\0'};      //not allowed
```
只有在定义数组时才能初始化，如果只对数组的一部分进行初始化，则编译器把其他元素设置为0；  
可不在大括号内包含任何东西，将把所有元素都设置为0；  
列表初始化禁止缩窄转换。  
#### 字符串
```
