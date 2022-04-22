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

