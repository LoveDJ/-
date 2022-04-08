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

#### (2) string操作

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

