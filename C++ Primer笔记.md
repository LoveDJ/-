## 二 变量和基本类型



### 1. const变量

const变量：变量的值不能被改变

```c++
const int bufSize = 512;
const int j = get_size(); //正确
```

可以用非常量对象初始化常量：

```c++
int i = 42;
const int a = i; //用非常量初始化常量
int j = a;//用常量初始化非常量
```

const变量仅在本文件中有效，在编译时，会用const变量的值替换出现的地方

在其他文件中用const变量 extern：

```c++
//extern 关键字
extern 	const int bufSize;
```



**const引用**

const引用：不能通过该引用改变对象的值。

```c++
// 对常量的引用(常量引用)
const int ci = 1024;
const int &r1 = ci;
```

允许将常量引用绑定到 <u>*非常量*</u>、<u>*字面值*</u>、<u>*表达式*</u> 上。

```c++
//非常量
int i = 42;
const int &j = i;
//字面值
const int &k = 42;
//表达式
const int &v = j * 2;
```



**指针和const**

指向常量的指针：不能通过该指针去改变变量的值。

```c++
// 指向常量
const double pi = 3.14;
const double *ptr = &pi;
// 指向非常量
double dval = 3.14;
const double *ptr = &dval;
```

const指针（常量指针）：将指针本身定为常量，即指向不能发生变化。

```c++
//指向非常量
int errNum = 0;
int *const curErr = &errNum;

const double pi = 3.14;
const double *const cpr = &pi; // 指向常量对象的常量指针
```



**顶层const**

- 顶层const：指针本身是个常量
- 底层const：所指向的对象是个const



**constexpr**

常量表达式：值不会改变且在编译过程就能得到计算结果的表达式。

constexpr：判断一个初始值是不是常量表达式，同时将该变量声明为常量。

```c++
constexpr int mf = 20;
constexpr int limit = mf + 1;
constexpr int sz = get_size();//只有当get_size()是constexpr函数时，才是正确的

//constexpr修饰指针时，会将该指针设置为常量，即常量指针（顶层const）
constexpr double *ptr = &pi; //ptr的指向不能变
```







## 三 字符串和数组



### 2. 字符串

####  (1)  定义和初始化

```c++
string s1;
// 直接初始化
string s2(s1);
string s3("dingjian");
string s4(10, 'c');
// 拷贝初始化
string s5 = s1;
string s6 = "dingjian";
string s7 = string(10, 'c');// 临时对象
```

#### (2) 操作

**读写string**

```c++
// 1. 读写一个string
string s;
cin >> s;// 会忽略空白
cout << s;

// 2. 读写多个string
string s1, s2;
cin >> s1 >> s2;
cout << s1 << s2;

// 3. 循环读
string word;
while(cin >> word)
{
    cout << word;
}

// 4. 读一行，需要保留空白
string line;
while(getline(cin, line))
{
    cout << line << endl;
}
```

**string::size_type类型**

string size()操作返回size_type类型，该类型与机器无关。

```c++
auto len = line.size();
size_type len = line.size();
```

**string比较**

依照字典顺序进行比较

**string对象相加**

确保每个相加运算符的两侧至少有一个是string对象，不能将两个字面值直接相加

```c++
// error
string s = "abc" + "def";
string s = "abc" + "def" + s1;
// correct
string s = s1 + "abc";
string s = s1 + "abc" + "def";
```

#### (3) 处理string中的字符

```c++
// 1. 改变string全部的字符-for循环
string s = "aabcs";
for(auto &c : s) // c是一个引用，对c的改变将会改变原字符串
{
    c = toupper(c);
}

// 2. 改变string中部分的字符-通过下标[]
string s = "abcd";
s[0] = toupper(s[0]);
```



### 3. VECTOR

#### (1) 定义和初始化

```c++
vector<T> v1;
vector<T> v1(v2);
vector<T> v2 = v1; //等价上式
vector<T> v3(n, val);
vector<T> v4(n);
vector<T> v5{a,b,c...};
vector<T> v6 = {a,b,c...}; //等价上式
```

#### (2) 操作

1. warning:添加元素时不能使用for循环
2. 不能用下标方式添加元素

```c++
v.push_back();
v.empty();
v.size();
v[n]; //返回引用
v == v1; // != > >= < <= 
```

### 4. 迭代器

迭代器是用来访问容器的元素，功能与下标运算符相同。

```c++
//获取迭代器
auto a = v.begin(), b = v.end();
//操作
*iter; //返回元素的引用
iter->mem; // 等价于(*iter).mem 解引用iter，获取元素的成员
//迭代器运算
++iter; --iter;
iter + n; iter - n;
iter += n; iter -= n;
== != >= <=
```

### 5.数组

#### (1) 定义和初始化

1. 数组的维度必须是已知的
2. 数组的维度必须是常量表达式
3. 数组初始化不允许拷贝和赋值，arr2 = arr这样是错误的

```c++
int arr[10];
int *arr[10]; //包含10个指针的数组
constexpr unsigned sz = 10;
string strs[sz];
//显示初始化
int a1[3] = {0, 1, 2};
int a2[] = {0, 1, 2};
int a3[5] = {0, 1, 2}; //等价于{0, 1, 2, 0, 0}
```

**字符数组的初始化：**

1. 可以使用字符串字面值初始化
2. 注意初始化时，结尾处的空字符'\0'

```c++
char a1[] = {'C', '+', '+'};
char a2[] = {'C', '+', '+', '\0'}
char a3[4] = "ding"; //error
char a4[5] = "ding"; //correct
char a5[] = "ding";
```

**复杂初始化**

引用一个数组&

指向一个数组*

```c++
//由内向外阅读
int (*arr1)[10] = &arr; //arr1是指针，指向一个10个元素的数组arr
int (&arr2)[10] = arr; //arr2是引用，引用了10个元素的数组arr
```

#### (2) 访问元素

```c++
// 1.下标
int arr[5] = {0, 1, 2, 3, 4};
cout << arr[0] << endl;
// 2.for循环
for(auto i : arr)
{
    cout << i << " ";
}
```

#### (3) 数组与指针

**数组名其实是首元素的地址**

```c++
// 利用指针迭代数组 缺点：数组的长度需要确定
int arr[5] = {0, 1, 2, 3, 4};
int *b = arr;
int *e = arr[10];
for(; b!=e; ++b)
{
    cout << *b <<endl;
}
```

**利用begin和end函数迭代数组**

```c++
int arr[5] = {0, 1, 2, 3, 4};
int *b = begin(arr);
int *e = end(arr);
for(; b!=e; ++b)
{
    cout << *b <<endl;
}
```



## 四 表达式

### 1. 成员访问运算符

- 点运算符 获取类对象的一个成员
- 箭头运算符 通过类指针直接访问

```c++
string s1 = "a string";
string *p = &s1;
//点运算符
auto n = s1.size();
n = (*p).size(); //必须加括号
//箭头运算符
n = p->size();
```

### 2. 位运算符

```c++
unsigned long quiz1 = 0;
quiz1 |= 1UL << 27; //第27个同学通过测验
quiz1 &= ~(1UL << 27);//第27个同学没有通过测验
bool status = quiz1 & (1UL << 27); //判断是否通过了测验

```

### 3. sizeof

sizeof返回一个类型所占的字节数。

- sizeof 引用：返回被引用对象所占用的大小
- sizeof 指针：指针本身的大小
- sizeof 解引用：指向对象的大小
- sizeof 数组名：整个数组占用的大小
- sizeof string/vector：固定部分的大小，不会计算对象中的元素占用了多少空间

```c++
size_t sz = sizeof(ia)/sizeof(*ia);
```

### 4. 类型转化

**隐式转化**

- 小类型转成大类型
- 无符号类型大，带符号转无符号
- 无符号类型小，无符号转带符号
- 数组转指针

```c++
int a[10];
int *p = a;
```

- 转成指针：数值0和字面值nullptr可以转成任意指针类型；非常量指针可以转成void*；所有指针都可以转成const void\*

- 转成引用：非常量引用转成常量引用
- 类类型转化：字符串字面值转string；while(cin>>s) cin转成bool类型

**显式转化**

- static_cast(类型转化)

```c++
//将大类型转成小类型
double slope = static_cast<double>(j)/i;
//找回指针类型
void* p = &d; // double类型
double *dp = static_cast<double*>(p);
```

- const_cast（将常量改为非常量）

```c++
const char *pc;
char *p = const_cast<char*>(pc);
```



## 五 语句

异常处理

```c++
while(cin>> item1 >> item2)
{
    try
    {
        
    }catch(runtime_error err)
    {
        cout << err.what() << endl;
    }
}
```





## 六 函数

函数包含4个部分：<u>*返回类型*</u>、<u>*函数名*</u>、<u>*形参*</u>、<u>*函数体*</u>

### 1. 参数传递

值传递：实参的值拷贝到形参上，形参和实参是两个独立的对象。（指针传参也是值传递）

引用传递：形参是引用类型，绑定到对应的实参上。

```c++
//引用传递
void reset(int &i)
{
    i = 0;
}
int j = 42;
reset(j);//直接传入对象，无需获取地址
```

#### (1) 形参和实参中带有const

带有const的形参的初始化和变量的初始化类似。

1. 形参有顶层const时，传常量或者非常量都是i可以的

```c++
void fcn(const int i)
```

2. 不能用底层const对象初始化非常量

```c++
int i = 42;
const int *p = &i;
int *p2 = p; //error

const int &r = i;
int &r2 = r; //error
int &r3 = 42; //error 不能直接引用字面值常量
```

3. 尽量使用常量引用

```c++
void fnc(int &s);
fnc("hello");//error 不能将字面值常量赋值给普通引用
```

#### (2) 数组作为参数

1. 传递数组实际上传递的是数组首元素的指针，传递数组参数的方法：

```c++
// 互相等价
void print(const int*);
void print(const int[]);
void print(const int[10]); //10没有意义
```

2. 数组作为参数，由于传递的是指针，不知道数组大小，所以一般需要额外的信息

	- 使用特殊标记结尾
	- 传递首尾指针
	- 传递数组大小

3. 数组引用形参

```c++
void print(int (&arr)[10]) // 括号不能省略
{
    for(auto elem : arr)
        cout << elem <<endl;
}
```

3. 传递多维数组

```c++
void print(int (*matrix)[10], int row_size)
```

#### (3) main函数的命令行选项

argc: 命令行字符串个数；

argv: 是一个数组，它的元素是指向C风格字符串的指针

```c++
int main(int argc, char *argv[])
{
    ...
}
```

eg:

```shell
prog -d -o ofile data0
argv[0] = "prog";
argv[1] = "-d";
argv[3] = "ofile";
argv[4] = "data0";
argv[5] = 0;
```



​    



## 八 IO库

- iostream 处理控制台的IO
- fstream 处理文件的IO
- stringstream 处理内存string的IO

### 文件的输入输出

读取文件：

```c++
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
using namespace std;


int main()
{
    ifstream in("1.txt");
    vector<string> v;
    string a;
    while(getline(in, a))
    {
        v.push_back(a);
    }
    for(int i=0; i<v.size();++i)
    {
        cout << v[i] <<endl;
    }
}
```

写入文件：

```c++
#include <fstream>
using namespace std;


int main()
{
   ofstream out;
   out.open("1.txt");
   out << "123" << endl;
}
```



## 十一 关联容器





### 4. 无序容器

- 无序容器操作与有序容器相同
- 无序容器有对其自身桶的操作
- 内置数据类型有默认的hash模板；自定义类型需要自定义哈希函数

```c++
size_t hasher(const Sales_data &sd)
{
    return hash<string>() (sd.isbn());
}
size_t eqOp(const Sales_data &lhs, const Sales_data &rhs)
{
    return lhs.isbn() == rhs.isbn();
}
unordered_multiset<Sales_data, decltype(hasher)*, decltype(eqOp)*> bookstore(42, hasher, eqOp);
```



## 十二 动态内存

