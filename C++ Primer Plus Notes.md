# C++ Primer Plus

### 第三章 处理数据

##### 3.1 整型

​	（按宽度从小到大）

+ 有符号：char、short、int、long、long long

+ 无符号：使用unsigned关键字

+ 整型类型占用的内存根据不同系统进行变化。通常int为自然长度，short用于需要节省内存的状况。

+ char：八位，保存一位字符

##### 3.2 字面值与进制：

- 十进制：1-9开头
- 八进制：0开头，第二位为1-7
- 十六进制：0x开头
- 不论表示为什么进制，计算都为二进制。
- 在cout中可使用oct（8）、hex（16）、dec（10）关键字控制输出的形式1

##### 3.3 浮点数

+ 组成：基准值+缩放因子

+ 表示：15.26 或者 3.45E6（3.45*10^6）

+ 类型：float（6有效位），double，long double

##### 3.4 C++的类型转换

+ 初始化和赋值：值将被转换为接受变量的类型

+ 使用{}进行转换（列表初始化）：

     ```c++
     char c1 {12345}
     //{}中的变量必须是常量（const）
     ```

     

+ 表达式中转换：在计算表达式中，位数小于int的整型将被转换为int进行计算（自然类型）；较小类型将被转为较大类型进行计算；

     浮点数提升：long double > double > float  ，否则进行整型提升； 

+ 传递参数时的转换

+ 强制类型转换：

     ```C++
     (typeName) value
     typeName(value)
     static_cast<typeName> (value)
     ```
     
     

##### 3.5 auto声明（c++11）

   不指定变量的类型，编译器将设置为与初始值相同

   ```c++
   auto n = 111
   ```



### 第四章 符合类型

##### 4.1 数组

```c++
//typeName arrayName[arraysize]
short months[12] //0-11
```

arraysize必须是const或常数值，在编译时必须是已知的

**初始化**：

```c++
int cards[4] = {3, 6, 8, 10};
int cards[4] = {2, 5}; //剩余将为0
int cards[4] = {0}; //全置为0
double earnings[4]{1.2, 1.3, 1.5, 0.8};	//C++11
```

##### 4.2 字符串

+ string为以**'\0'**结尾的字符数组。

```c++
char bird[] = "Mr. creeps";
//'s'->83;
//"s"->s和'\0'
```

+ sizeof VS strlen:

  sizeof : 数组长度，包括\0

  strlen：只计算可看见的字符，不计算\0

+ 字符串的输入

  + cin通过空格、换行、制表符来确定字符串的结束位置

  + cin.getline()

    ```c++
    cin.getline(name, 20);
    ```

    

  + cin.get()

+ 字符串操作

  ```C++
  strcpy(s1, s2);	//copy s2 to s1
  strcat(s1, s2);	//append s2 to s1
  ```

  未初始化的字符数组内容未定，strlen从第一个符号开始计算到空字符，长度随机；而未初始化的string长度为0
  
+ 其他

  + 原始字符：无需使用反斜杠，是啥就是啥；界定符也可自行定义

    ```c++
    R"(Jim "king" Tutt uses "\n" instead of endl.)";
    R"+(ab)+";
    ```

    

  + C++11新类型

    ```C++
    wchar_t a[] = L"abcd";
    char16_t b[] = u"abcd";
    char32_t c[] = U"abcd";
    ```

    

##### 4.3 结构Struct

```C++
struct structName{
	type1 valueName1;
	type2 valueName2;
	//……
};	//结构名可省略，后置变量名，将创建一个不可复用的结构与一个结构变量

structName abc = {
    value1;
    value2;
    //……
};

//c++11
structName edf {value1, value2 };	//大括号内为空则初值为0

cout << abc.valueName1;	//通过类似类的方式访问属性

//可以创建结构数组
structName abcd=[10] = {
    {……},
    {……}
}

//创建结构时对位数进行限制
struct structName{
	type1 valueName1 :bitNum;
	type2 valueName2 :bitNum;
	//……
};
```



##### 4.4 共用体 union

创建方式与结构相同，共用体能够存储不同的数据类型，但同时只能存储其中的一种。因此共用体在不同时间可能类型不同。

共用体长度为其最大成员的长度。通常用于节省内存。



##### 4.5 枚举 enum

```c++
enum spectrum {red, orange, yellow};
//red, orange, yellow将作为符号常量，对应整数值0~2
spectrum band;
band = red;	//正确语句
band = 20; 	//错误
band = spectrum(2);	//当数字有效时有效，强制类型转换

enum bits {one = 1, two = 2, four = 4, eight = 8};	//指定值，只可以为整数 
```

枚举类型只定义了赋值运算。但在与int类型的混合运算中，将被转换为int进行运算。



##### 4.6 指针 pointer

**指针**：存储值的地址

**作用**：在运行阶段，分配未命名的内存进行存储

**&运算符**：可获得变量的**地址**

***运算符**：可获得地址存储的**值**

```C++
int jumbo =23;
int * pe = &jumbo;
//jumbo与*pe都为23值
//&jumbo与pe都为变量地址
```

1. 不同类型的字节数不同，在系统内部内存地址格式也不同，因此声明指针时必须指定指针指向的数据类型

   ```C++
   int* p_a;
   //p_a为“指向一个int的地址，int*”， *p_a为int
   ```

2. 可在声明语句中**初始化指针**

   ```c++
   int a = 5;
   int* b = &a;
   ```

3.  运算符new

   ```c++
   int* a = new int;
   //new运算符根据数据的类型来确定需要分配多少字节的空间
   //地址只指出了对象存储地址的开始，没有指出大小、类型
   ```

   可使用delete将new分配的内存空间归还内存池 ，delete与new需要配套使用，不然将会发生内存泄漏

   delete将释放内存，但不会删除指针

4. 使用new动态创建数组

   + 静态联编：在编译时为数组分配内存
   + 动态联编：在程序运行时确定数组长度

   创建/删除动态数组：

   ```C++
   int * psome = new int[10];
   
   delete [] psome;
   ```

   指针变量加一，增加的量等于指向类型的字节数；

   **C++常将数组名解释为地址**（在sizeof、取地址情况中，不将数组名解释为地址 ）

   ```C++
   //两种获得数组地址的方式
   double wages[3] = {0.1, 0.2, 0.3};
   double *pw1 = wages;
   double *pw2 = &wages[0];
   ```

   将字符串赋值给数组：

   ```c++
   //1.初始化数组时使用赋值
   char food[20] = "carrots";
   //2.其他情况使用strcpy
   strcpy(food, "flan");
   //3.字符串过长时使用strncpy,第三个参数为限制长度
   strncpy(food, "…………", 19);
   food[19] = '\0'
   ```

5. 使用new创建动态结构

   ```c++
   structName *pt = new structName;
   ```

   访问成员：创建动态结构时，指针不能使用**句点成员运算符号（.）**，需要使用**间接成员运算符号（->）**
   
   ```C++
   //访问成员的方法
   pt->a;
   (*pt).a;
   ```
   
   使用new可根据输入分配内存，节约空间
   
6. C++处理内存前瞻

   C++分配内存的3种方法：自动存储、静态存储、动态存储（或自由存储空间或堆）

   C++11新的存储类型：线程存储

   + 自动存储

     函数内部定义的变量称为自动变量，它在函数被调用时自动产生，函数结束时自动释放。**局部变量**

     自动变量通常存储在**栈**中

   + 静态存储

     整个程序执行期间都存在，定义方法：

     1. 在函数外定义
     2. 使用**static关键字**

   + 动态存储

     new和delete运算符提供的存储方法。它们管理一个内存池（**自由存储空间/堆**）

   **内存泄漏**：通过new分配的自由存储空间，若未通过delete释放，指向该空间的指针又由于生命周期被释放，则将导致内存泄漏。

   被泄漏的内存在程序整个周期都不可复用。

##### 4.7 数组的替代品 vector和array

1. vector 长度可变

   ```c++
   vector<typeName> vt(n_elem);
   ```

2. array 长度固定 C++11

   ```c++
   array<typeName, n_elem> arr;
   ```

3. 数组、vector、array比较

   + array与数组存储在栈中，vector存储在自由存储空间中
   + array对象可以直接赋值给另一个array对象，而数组需要逐个元素赋值
   
     

### 第五章 循环和关系表达式

##### 5.1 for循环

```C++
for(init_stat; condition; update_stat){
	//执行语句
}
//顺序：init_stat -> condition -(true)> 执行语句 -> update_state
```

##### 5.2 表达式和运算符

+ C++表达式是值、值与运算符的组合，每个C++表达式都有值
+ 赋值表达式的值为=左边变量的值
+ ++与--中，后缀优先级>前缀优先级。在用户定义的递增、递减中，前缀格式效率更高
+ 逗号表达式的值为最右部分的值

##### 5.3 字符串比较

+ C风格：由于字符数组名本质上为指针，使用==对数组名进行比较实际上为比较地址，不可靠。因此常用**strcmp(a, b)**函数对两个字符数组进行比较。返回值为**0**时，为a、b相同；小于0代表按字母顺序a排在b前
+ string比较：string可以使用==、!=进行比较

##### 5.4 while循环

略

##### 5.5 基于范围的for循环（C++11）

```c++
double prices[5] = {4.99, 10.99, 6.87, 7.99, 8.49};
for (double x : prices){
	//stat
}
```

##### 5.6 循环和文本输入

1. 使用原始cin输入，设置哨兵字符

   该方法将省略输入的空格

   ```C++
   char ch;
   int cnt = 0;
   cin >> ch;
   while (ch != '#'){
       cout << ch;
       ++cnt;
       cin >> ch;
   }
   ```

2. 使用cin.get(char)，该方法可以保存空格

3. 文本操作步骤：

   1. 包含头文件fstream
   2. 创建ofstream对象
   3. 使用.open将ofstream和文件关联
   4. 像使用cout一样使用ofstream对象

### 第七章 C++函数

##### 7.1 函数的特性

+ C++按值传递参数，函数将使用新的变量接收参数传递的值

##### 7.2 函数和数组

```C++
int func(int arr[], int n);
int func(int *arr, int n);
```

```
//数组与指针恒等式
arr[i] == *(arr + i);
&arr[i] == arr + i;
```

##### 7.3 指针与const

将const应用于指针的两种情况：

1. 指针指向一个**常数对象**：

   ```c++
   int age = 18;
   const in * pt = &age;
   ```

   上述定义表示仅对于指针**pt**来说，指向的是一个常数，指针pt无法用于修改值，但使用原本变量名age可以。

   **正确方式：**将const变量的地址赋给指向const的指针

   ```C++
   const float g_earth = 9.80;
   const float *pe = &g_earth;
   ```

2. 指针本身为**常数**：

   ```C++
   int * const pt = &age;
   ```

   此时指针只能指向age，允许使用指针修改指向的值，但无法使指针指向其他位置

##### 7.4 函数指针

函数**也有地址** 

1. 定义函数指针

   ```C++
   typeName (*pt)(paraList);
   //与需要指向的函数的原型相同
   ```

2. 函数指针使用

   ```c++
   //与函数相似
   (*pt)(paraList)
   ```

3. 可使用auto自动匹配类型（C++11)

##### 7.5 内联函数

+ **普通函数**：在函数调用后跳到指定内存地址执行
+ **内联函数**：将代码复制到原地（更快，代价是内存消耗更多）
+ 创建方法：在函数的声明与定义前加关键字**inline**
+ 编译器并不一定会接收内联定义，函数过大或函数存在递归时可能将不会定义成内联函数（内联函数不能递归）

##### 7.6 引用变量

使用**&符号**表示引用

```C++
int & rodents = rats;
```

