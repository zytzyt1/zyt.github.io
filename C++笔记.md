@[TOC](C++)

# 字符串简单处理

## strcmp	字符串比较函数

```c++
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

/*
 * int strcmp(const char *str1, const char *str2);
 * 安全版: int strncmp(const char *str1, const char *str2, size_t num); 
 * strcmp是字符串比较函数
 * 1.str1 == str2 则返回值为0
 * 2.str1 > str2 则返回值为1
 * 3.str1 < str2 则返回值为-1 
 * 
*/
int main(){
	char str2[] = "比较123";
	char* str1 = (char*)malloc(strlen(str2) + 1);
	str1 = "比较456";
	int a = strcmp(str1,str2);
	printf("%d",a);
    
    system("pause");
    return 0;
} 
```

## strcpy	字符串拷贝函数

```c++
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

/*
 * char* strcpy(char* restrict dst, const char* restrict src);
 * 安全版: char* strncpy(char* dst, const char* src, size_t num);
 * strcpy是字符串复制函数 将src的字符串拷贝到dst 
 * restrict表明src和dst不重叠(C99)
 * 返回值是dst 
*/

int main(){
	char* src = "1234";
	char* dst = (char*)malloc(strlen(src) + 1);
	strcpy(dst,src);
	printf("%s",dst);
    
    system("pause");
    return 0;
} 
```

## strcat		字符串拼接函数

```c++
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

/*
 * char* strcat(char* restrict str1, char* restrict str2);
 * 安全版: char* strncat(char* restrict str1, char* restrict str2, size_t num); 
 * 将str2 拼接到 str1 后面,接成一个长字符串
 * 返回str1
 * str1必须有足够的空间 
*/
int main(){
	char *str2 = "1234";
	char *str1 = (char*)malloc(strlen(str2) + 5);
	str1 = "567";
	strcat(str1,str2);
	printf("%s",str1);
    
    system("pause");
    return 0;
}
```

## strchr/strrchr	字符串中查找字符

```c++
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

/*
 * char* strchr(const char* str, int c); 从左至右查找 
 * char* strrchr(const char* str, int c); 从右至左查找 
 * 从字符串str中查找字符c 返回第一个c的地址 
 * 未查找到则返回NULL
*/

int main(){
	char* str = "1234556789";
	char*p = strchr(str,'1');
	if (p != NULL) 
		printf("%d",p - str);//p - str 是该字符出现的下标 
    
    system("pause");
    return 0;
} 
```

## strstr		字符串中查找字符串

```c++
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

/*
 * char* strstr(const char* str1, const char* str2); 
 * 从字符串str1中查找字符串str2 返回第一次查找到的地址 
 * 未查找到则返回NULL
*/

int main(){
	char* str1 = "abc01234567";
	char* str2 = "01";
	char* p = strstr(str1,str2);
	printf("%s",p);
    
    system("pause");
    return 0;
 }
```

# 输入输出

## 标准输入输出

```c++
scanf的格式:
%[flag]type

flag	含义		flag	含义
 *		跳过		 l	  long,double
数字	 最大字符数	 ll	   long long
hh		char	  L    long double
h		short
——————————————————————————————————————————————
printf的格式:
%[flag][width][.prec][hil]type

flag	含义
 -	 	左对齐
 + 		在前面放+或-
(space) 正数留空
0 		0填充

width或prec	含义
 number		最小字符数
 *			下一个参数是字符数
 .number	小数点后的位数
 .*			下一个参数是小数点后的位数	

hil		含义
 hh		单个字节
 h		short
 l		long
 ll		long long
 L		long double
```



## 多种输入方式

```c++
#include <iostream>

/*
* 1.单个字母输入: 1.scanf("%c",&s);
*                 2.s = getchar();
* 2.遇到空格和换行符停止输入: 1.scanf("%s",&str);
*                             2.cin << str; //string变量也能使用 
* 3.输入一整行: 1.gets(str); 
*               2.cin.getline(str,number); (number - 1)个字符之后的不会读取 
*               3.cin.get(str,number).get(); 和3.2用法类似 后面的.get()是为了读取(number - 1)之后的一个字符 
* 4.输入指定数量字符的字符串: scanf("%7s",&str); 7代表最多允许读入的字符的数，这个数应该比数组的大小小1 
*/

using namespace std;

int main(){
	char s;
	char str[10];
	short j = 20;
	//cin >> s; 
	//scanf("%c",&s);     						  //1.1
	//s = getchar();      						  //1.2
	//scanf("%s",str);    						  //2.1 
	//cin >> str;   							  //2.2
	//gets(str);          						  //3.1
	//cin.getline(str,5);                         //3.2
	//cout << (char)cin.get(str,5).get() << endl; //3.3
	//scanf("%4s",str); 						  //4.0
	//cout << s;
	cout << str;
	system("pause");
}
```

## 保留小数位或有效数字输出

```c++
头文件
#include <iomanip>
示例
double a = 123.4567;
cout << std::fixed << std::setprecision(2) << a << endl; //保留两位小数的形式输出
cout << std::setprecision(5) << a << endl; //保留五位有效数字输出
```

# 类和对象的三大特点

## new在堆区开辟内存

```c++
语法:	new 数据类型;
	返回值是该数据类型的指针
例子:	int* p = new int(10);

释放堆区的数据:
	1.int* p = new int(10); //单个数据
	  delete p;
	2.int* arr = new int[10]; //数组
	  delete[] arr;
```



## 封装(无笔记)

## 继承

### 继承语法

```c++
继承语法:	class 子类(派生类) : 继承方式 父类(基类)
例子:	class son : public father
```

### 继承方式的区别

![image-20220304222901659](C:\Users\ZYT\AppData\Roaming\Typora\typora-user-images\image-20220304222901659.png)

### 注意点

#### 1.子类继承父类所有成员属性

```c
#include <iostream>
#include <string>
using namespace std;

class Base{
	public:
		int a;
	protected:
		int b;
	private:
		int c;
};

class Son : public Base
{
	public:
		int d;
};

int main(){
	Son son;
	//输出为16 代表子类继承了父类所有成员
	//访问权限不够的成员被隐藏 
	cout << sizeof(son) << endl;
    
	system("pause");
	return 0;
}
```

#### 2.子类访问父类同名成员属性

```c++
子类访问父类中同名成员属性需要加作用域
```

```c++
#include <iostream>
#include <string>
using namespace std;

class Base{
	public:
		int m_a;
	public:
		Base(){
			m_a = 100;
		}
};

class Son : public Base
{
	public:
		int m_a;
	public:
		Son(){
			m_a = 200;
		}
};
void test01(){
	Son son;
	cout << "Son调用自己的成员" << son.m_a << endl; 
	cout << "Son调用Base的同名成员" << son.Base::m_a << endl;
} 
int main(){
	test01();
	
	system("pause");
	return 0;
}
```

#### 3.子类访问父类同名成员函数

```c++
//如果子类中出现和父类同名的成员函数，子类的同名成员函数会隐藏掉父类中所有同名成员函数
//如果想访问到父类中被隐藏的同名成员函数，需要加作用域
```

```c++
#include <iostream>
#include <string>
using namespace std;

class Base{
	public:
		void func(){
			cout << "Base中的无参成员函数func" << endl;
		}
		void func(int a){
			cout << "Base中的有参成员函数func" << endl;
		}
};

class Son : public Base
{
	public:
		void func(){
			cout << "子类中的无参成员函数func" << endl;
		}
};
void test01(){
	Son son;
	son.func();
	//son.func(3);//报错 
	son.Base::func();
	son.Base::func(3);
} 
int main(){
	test01();
	
	system("pause");
	return 0;
}
```

#### 4.继承中的同名静态成员属性

```c++
#include <iostream>
#include <string>
using namespace std;

//类中的静态变量必须: 类中定义，类外初始化 
class Base{
	public:
		static int m_num;
};
int Base::m_num = 200;
class Son : public Base
{
	public:
		static int m_num;
};

int Son::m_num = 100;

void test01(){
	//1.通过对象访问
	Son son;
	cout << "通过对象访问" << endl;
	cout << "Son中的m_num = " << son.m_num << endl;
	cout << "Base中的m_num = " << son.Base::m_num << endl;
	//1.通过类名访问
	cout << "通过类名访问" << endl;
	cout << "Son中的m_num = " << Son::m_num << endl;
	//第一个::代表通过类名访问 第二个::代表访问父类作用域下 
	cout << "Base中的m_num = " << Son::Base::m_num << endl;
} 
int main(){
	test01();
	
	system("pause");
	return 0;
}
```

#### 5.继承中的同名静态成员函数

```c++
#include <iostream>
#include <string>
using namespace std;

class Base{
	public:
		static void func(){
			cout << "Base中的func" << endl; 
		}
};

class Son : public Base
{
	public:
		static void func(){
			cout << "Son中的func" << endl;
		}
};

void test01(){
	//1.通过对象访问
	Son son;
	son.func();
	son.Base::func();
	//1.通过类名访问
	Son::func();
	Son::Base::func();
} 
int main(){
	test01();
	
	system("pause");
	return 0;
}
```

### 多继承

```c++
C++中允许一个类同时继承多个类
语法:
	class 子类 : 继承方式 父类1 , 继承方式 父类2...
实际开发中不推荐使用多继承 容易造成二义性
```



## 多态

### 多态的基本概念

```c++
多态分为两类:
	1.静态多态: 函数重载 和 运算符重载，服用函数名
	2.动态多态: 派生类 和 虚函数实现运行时多态
静态多态和动态多态的区别:
	1.静态多态的函数地址早绑定(编译阶段确定函数地址)
	2.动态多态的函数地址完绑定(运行阶段确定函数地址)
动态多态满足条件:
	1.有继承关系
	2.子类重写父类的虚函数
动态多态使用条件:
	父类的指针或引用执行子类对象
```

```c++
#include <iostream>
#include <string>
using namespace std;

//动物类 
class Animal{
	public:
		//virtual 虚函数标志 
		//作用: 函数地址晚绑定 
		//不加的话会导致多态子类始终执行父类的speak函数 
		virtual void speak(){
			cout << "动物在说话" << endl; 
		}
};
//猫类 
class Cat : public Animal 
{
	public:
		void speak(){
			cout << "猫在说话" << endl;
		}
};
//狗类 
class Dog : public Animal 
{
	public:
		void speak(){
			cout << "狗在说话" << endl;
		}
};
//执行说话函数 
void doSpeak(Animal& animal){
	animal.speak();
}

void test01(){
	Animal* cat = new Cat;
	cat->speak();
    delete cat;
	Dog dog;
	doSpeak(dog); 
} 
int main(){
	test01();
	
	system("pause");
	return 0;
}
```

### 运算符重载

#### 重载加号+

```c++
#include <iostream>
#include <string> 

using namespace std;

/*
* 重载加号+ :
* 	1.成员函数重载加号
*	2.全局函数重载加号 
*/

class Person{
	public:
		int m_x;
		int m_y;
	public:
		//1.成员函数重载加号 + 
		Person operator+(Person &p){
			Person temp;
			temp.m_x = this->m_x  + p.m_x;
			temp.m_y = this->m_y + p.m_y;
			return temp;
		}
};

//2.全局函数重载加号
//Person operator+(Person &p1,Person &p2){
//	Person temp;
//	temp.m_x = p1.m_x + p2.m_x;
//	temp.m_y = p1.m_y + p2.m_y;
//	return temp;
//}

void test01(){
	Person p1,p2;
	p1.m_x = 12;
	p1.m_y = 13;
	p2.m_x = 21;
	p2.m_y = 31;
	Person p3 = p1 + p2;
	cout << p3.m_x << "  " << p3.m_y << endl;
}

int main(){
	test01();
}
```

#### 重载左移运算符<<

```c++
#include <iostream>
#include <string>

using namespace std;

/*
* 全局函数重载左移运算符
* 注意事项: 不能用成员函数重载，否则会位置不同class << cout 
*/

class Person{
	public:
		int m_x;
		int m_y;
	public:
		Person(){
			m_x = 12;
			m_y = 23;
		}
};

//全局函数重载左移运算符
ostream& operator<<(ostream &cout, Person &p){
	cout << p.m_x << "  " << p.m_y;
	return cout;//返回值是为了多次输出 
}

void test01(){
	Person p1;
	cout << p1 << "Hello" << endl;
}
int main(){
	test01();
	system("pause");
	return 0;
}
```

#### 重载递增运算符++

```c++
#include <iostream>
#include <string>
using namespace std;

/*
* 递增符号++重载 
* 	前置递增和后置递增 
*/

class Person{
	public:
		int m_num;
	public:
		Person(){
			m_num = 0;
		}
	public:
		//1.重载前置++ 
		//返回引用是为了一直只对该数据进行递增操作 
		Person& operator++(){
			m_num++;
			return *this; 
		}
		
		//2.重载后置++
		//int代表占位参数，可以区分前置和后置参数 
		Person& operator++(int){
			Person temp = *this;
			m_num++;
			return temp;
		} 
}; 

void test01(){
	Person p1,p2;
	cout << ++p1.m_num << endl;
	cout << ++p1.m_num << endl;
	cout << p2++.m_num << endl;
	cout << p2++.m_num << endl;
	cout << p2++.m_num;
	
}

int main(){
	test01();
}
```

#### 重载赋值运算符=

```c++
#include <iostream>
#include <string>
using namespace std;

/*
* 赋值运算符=重载 
*/
class Person{
	public:
		int* m_age;
	public:
		Person(int age){
			//将年龄数据开辟到堆区 
			m_age = new int(age); 
		}
	
	public:
		Person& operator=(Person &p){
			if(m_age != NULL){
				delete m_age;
				m_age = NULL;
			}
			m_age = new int(*p.m_age);
			return *this;
		}
		//析构函数释放堆区内存 
		~Person(){
			if(m_age != NULL){
				delete m_age;
				m_age = NULL;
			}
		}
}; 

void test01(){
	Person p1(1);
	Person p2(2);
	Person p3(3);
	p1 = p2 = p3;
	cout << *p1.m_age << endl;
	cout << *p2.m_age << endl;
	cout << *p3.m_age << endl;
}

int main(){
	test01();
	system("pause");
	return 0;
}
```

### 纯虚函数和抽象类

```c++
在多态中，通常虚函数的实现是毫无意义的，主要都是调用子类重写的内容
因此可以将虚函数改为纯虚函数
语法: virtual 返回值类型 函数名 (参数列表) = 0；

当类中有了纯虚函数，这个类也成为抽象类
特点:
	无法实例化对象
    子类必须重写抽象类中的纯虚函数，否则也属于抽象类
```

### 虚析构和纯虚析构

```c++
#include <iostream>
#include <string>
using namespace std;

//动物类 
class Animal{
	public:
		virtual void speak() = 0; 
	public:
		string* m_Name;
	public:
		//虚析构函数 
		//解决父类指针释放子类对象时不干净的问题 
		virtual ~Animal(){
			if (m_Name != NULL){
				delete m_Name;
				m_Name = NULL;
			}
		}
};
//猫类 
class Cat : public Animal 
{
	public:
		string *m_Name;
	public:
		Cat(string name){
			m_Name = new string(name);
		}
	public:
		void speak(){
			cout << *m_Name << "猫在说话" << endl;
		}
};

void test01(){
	Animal* cat = new Cat("汤姆");
	cat->speak();
} 
int main(){
	test01();
	
	system("pause");
	return 0;
}
```

# 文件操作

```c++
/*
* 两种文件类型:
*	1.文本文件：文件以文本的ASCLL码形式存储在计算机中
*	2.二进制文件：文件以文本的二进制形式存储在计算机中 
*/ 

/*
* 操作文件的三大类:
*	1. ofstream 写操作
*	2. ifstream 读操作
* 	3. fstream 读写操作
*/

/*
* 文件打开方式:
* ios::in		为读文件而打开文件
* ios::out		为写文件而打开文件
* iOS::ate		初始位置: 文件尾
* ios::app		追加方式写文件
* ios::trunc	如果文件存在, 先删除再创建
* ios::binary	二进制方式 
* 文件打开方式可以通过 | 操作符配合使用
* 例如:用二进制方式写文件 ios::binary | ios::out
*/
```

## 写文件

```c++
/*
* 写入文件的步骤
* 1.包含头文件：#include<fstream>
* 2.创建流对象：ofstream ofs;
* 3.打开文件：ofs.open("文件路径",打开方式);
* 4.写入内容:：ofs << "写入的数据";
* 5.关闭文件：ofs.close();
*/
```

```c++
#include <iostream>
#include <string>
#include <fstream>
using namespace std;

int main(){
    //1.包含头文件 fstream 
	//2.创建流对象
	ofstream ofs;
	//3.指定打开方式
	ofs.open("test.txt",ios::out);
	//4.写入内容
	//endl 也能在文件内换行 
	ofs << "尝试在文件内写入内容01" << endl; 
	ofs << "尝试在文件内写入内容02" << endl; 
	//5.关闭文件
	ofs.close();
	
	return 0;
}
```

## 读文件

```c++
/*
* 读取文件的步骤
* 1.包含头文件：#include<fstream>
* 2.创建流对象：ifstream ifs;
* 3.打开文件：ifs.open("文件路径",打开方式);
* 4.读取内容: 四种方式读取文件
* 5.关闭文件：ifs.close();
*/
```

```c++
/*
* 读数据的四种方式:
* 1.字符数组循环读取:
*		char buf[1024] = { 0 };
*		while( ifs >> buf ){
*			cout << buf << endl;
*		}
* 
* 2.ifs.getline(数组名,读取长度)函数逐行读取
*		char buf[1024] = {0};
*		while(ifs.getline(buf,sizeof(buf))) {
*			cout << buf << endl;
*		}
*
*3.getline(流对象,数组名)函数逐行读取
*		string buf;
*		while(getline(ifs,buf)) {
*			cout << buf << endl;
*		}
*
*4.ifs.get()函数逐个字符读取
*		char c;
*		while((c = ifs.get()) != EOF) {
*			cout << c;
*		}
*/
```

```c++
#include <iostream>
#include <string>
#include <fstream>
using namespace std;

int main(){
    //1.包含头文件 fstream 
	//2.创建流对象
	ifstream ifs;
	//3.指定打开方式
	ifs.open("test.txt",ios::in);
	if (!ifs.is_open()){
		cout << "文件打开失败" << endl;
		return 0;
	}
	//4.读取内容
	char buf[1024] = { 0 };
	while( ifs >> buf ){
		cout << buf << endl;
	}
	//5.关闭文件
	ifs.close();
	
	return 0;
}
```

## 二进制写入文件

```c++
/*
* 二进制方式写入文件主要利用流对象调用成员函数write
* ostream& write(const char* buffer, int len);
* 参数解释:字符指针buffer指向内存中一段存储空间。len是读写的 * 字节数
*/
```

```c++
#include <iostream>
#include <string>
#include <fstream>
using namespace std;

class Person{
	public:
		char m_Name[64];//姓名 
		int m_m_Age;//年龄 
};

int main(){
	//2.创建流对象
	ofstream ofs;
	//通过构造函数直接指定打开方式 省去第三步 
	//ofstream ofs("person.txt",ios::out | ios::binary); 
	//3.指定打开方式
	ofs.open("person.txt",ios::out | ios::binary);
	//4.写入内容
	Person p ={"张三",18};
	ofs.write((const char*)&p,sizeof(Person));
	//5.关闭文件
	ofs.close();
	
	return 0;
}
```

## 二进制读取文件

```c++
/*
* 二进制方式读取文件主要利用流对象调用成员函数read
* istream& read(char* buffer, int len);
* 参数解释:字符指针buffer指向内存中一段存储空间。len是读写的* * 字节数
*/
```

```c++
#include <iostream>
#include <string>
#include <fstream>
using namespace std;

class Person{
	public:
		char m_Name[64];//姓名 
		int m_m_Age;//年龄 
};

int main(){
	//2.创建流对象
	ifstream ifs;
	//3.指定打开方式
	ifs.open("person.txt",ios::in | ios::binary);
	if(!ifs.is_open()){
		cout << "文件打开失败" << endl;
		return 0;
	}
	//4.写入内容
	Person p;
	ifs.read((char*)&p,sizeof(Person));
	cout << p.m_Name << "  " << p.m_m_Age;
	//5.关闭文件
	ifs.close();
	
	return 0;
}
```

# 类模板

```c++
1.template <class T> // 最常用的：一个class 参数。
2.template <class T = char> // 有一个默认值。
3.template <int n> // 将调用时<>中的值作为模板参数，只支持整数类型和枚举类型
4.template <class T, class U> // 两个class 参数。
5.template <class T, int N> // 一个class 和一个整数。
6.template <int Tfunc (int)> // 参数为一个函数。
```

```c++
/***********第一种用法************/
template <class T>
T use01(T t){
    return t * 2;
}
//限制了只能是vector类型的参数
T use012(vecotr<T> const &v){
    for(int i = 0; i < v.size(); i++){
        cout << v[i] << endl;
    }
}

int main(){
    use01(2);
    use01<int>(2);
    use01<double>(2)
    vecotr<int> v1 = {1,2,3};
    use012(v1);
    vecotr<float> v2 = {1.1, 2.2, 3.3};
    use012(v2);
}

/***********第二种用法************/
//因为没有参数，T判断不了类型，所以要指定一个默认类型，或者调用的时候手动指定
template <class T = int>
T use02(){
    return 2;
}

int main(){
    use01();
}

/***********第三种用法************/

template <int N>
void use03(string str){
    for(int i = 0; i < N; i++){
        cout << str << endl;
    }
}

int main(){
    use03<4>("one");
}

/***********第四种用法************/
template <class T, class U>
void use04(T t, U u){
    cout << t << endl;
    cout << u << endl;
}
```





# STL库

## vector

```c++
容器：vector
算法：for_each
迭代器：vector<T>::iterator
vecotr添加元素时，不是在原空间之后接续新空间，而是另外配置一块较大空间，然后将原内容拷贝过来
```

### vector存放内置数据类型

```c++
#include <iostream>
#include <string>
#include <algorithm>
#include <vector>
using namespace std;

//第三种输出方式的函数 
void MyPrint(int val){
	cout << val << endl;
}

void test01(){
		vector<int> v;
	//向容器中放数据 
	for(int i = 0; i < 10; i++){
		v.push_back(i);
	}
	//每个容器都有自己的迭代器，迭代器是用来遍历容器中的元素
	//v.begin()返回迭代器，这个迭代器指向容器中的第一个数据
	//v.end()返回迭代器，这个迭代器指向容器中的最后一个数据
	//vector<int>::iterator 拿到vector<int>这种容器的迭代器
	
	//遍历容器中的数据
	//方式一 
	vector<int>::iterator vbg = v.begin();
	for( ; vbg!=v.end(); vbg++){
		cout << *vbg << endl;
	}
	//方式二 
	for(vector<int>::iterator it = v.begin(); it != v.end(); it++){
		cout << *it << endl;
	}
	//方式三
	//使用STL提供提供标准遍历算法 头文件 algorithm
	for_each(v.begin(), v.end(), MyPrint);
    //方式四
    //使用auto遍历
    for(auto ite = v.begin(); ite != v.end(); ite++){
		cout << *ite << endl;
	}
}

int main(){
	test01();
}
```

### vector存放自定义数据类型

```c++
#include <iostream>
#include <string>
#include <algorithm>
#include <vector>
using namespace std;

//自定义的数据类型 
class Person{
	public:
		string mName;
		int mAge;
	public:
		Person( string name, int age){
			mName = name;
			mAge = age;
		}
};
void test01(){
	vector<Person> v;
	Person p[6] = {
		{"aaa",1},
		{"bbb",2},
		{"ccc",3},
		{"ddd",4},
		{"eee",5},
		{"fff",6}
	};
	for(int i = 0; i < 6; i++){
		v.push_back(p[i]);
	}
	for(auto it = v.begin(); it != v.end(); it++){
		cout << it->mName << "  " << it->mAge << endl;
	}
}

int main(){
	test01();
}
```

### 容器嵌套容器

```c++
#include <iostream>
#include <string>
#include <algorithm>
#include <vector>
using namespace std;

void test01(){
	//vector里面嵌套vector 类似于二维数组 
	vector<vector<int>> vs;
	vector<int> v[5];
	for(int i = 0; i < 5; i++){
		for(int j = i; j < i + 5; j++){
			v[i].push_back(j);
		}
		vs.push_back(v[i]);
	}
	for(auto it = vs.begin(); it != vs.end(); it++){
		//*it -----容器vector<int> 
		for(auto jt = (*it).begin(); jt != (*it).end(); jt++){
			cout << *jt << ' ';
		}
		cout << endl;
	}
}

int main(){
	test01();
}
```

### vector构造函数

```c++
函数原型：
	vector<T> v;
	vector(v.begin(), v.end());	//将v[begin(),end()]区间中的元素拷贝给本身
	vector(n, elem);			//将n个elem拷贝给本身
	vector(const vector &vec);	//拷贝vec给本身
```

```c++
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

void printVector(const vector<int> v){
	for(auto i = v.begin(); i != v.end(); i++){
		cout << *i << endl;
	}
}

int main(){
	vector<int> v1; //无参构造
	
	for(int i = 0; i < 10; i++){
		v1.push_back(i);
	}
	printVector(v1);
	
	vector<int> v2(v1.begin(),v1.end());
	printVector(v2);
	
	vector<int> v3(10,100);
	printVector(v3);
	
	vector<int> v4(v3);
	printVector(v4);
}
```

### vector赋值操作

```c++
函数原型：
    vector& operator=(const vector &vec);
	assign(beg, end);	//将[beg,end)区间中的数据拷贝赋值给本身
	assign(n, elem);	//将n个elem拷贝赋值给本身
```

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

void printVector(const vector<int> v){
	for(auto i = v.begin(); i != v.end(); i++){
		cout << *i << endl;
	}
}

int main(){
	vector<int> v1; //无参构造
	
	for(int i = 0; i < 10; i++){
		v1.push_back(i);
	}
	printVector(v1);
	
	vector<int> v2;
	v2 = v1;
	printVector(v2);
	
	vector<int> v3;
	v3.assign(v1.begin(), v1.end());
	printVector(v3);
	
	vector<int> v4;
	v4.assign(10,100);
	printVector(v4);
}
```

### vector容量和大小

```c++
函数原型：
    empty();				//判断容器是否为空
	capacity();				//容器的容量
	size();					//返回容器中元素的个数
	resize(int num);		//重新指定容器的长度为num 若容器变长,则填充默认值0
							//					  若容器变短,则超出的元素被删除
	resize(int num,elem);	//重新指定容器的长度为num 若容器变长,则填充默认值elem
							//					  若容器变短,则超出的元素被删除
```

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

void printVector(const vector<int> v){
	for(auto i = v.begin(); i != v.end(); i++){
		cout << *i << endl;
	}
}

int main(){
	vector<int> v1; //无参构造
	
	for(int i = 0; i < 10; i++){
		v1.push_back(i);
	}
	printVector(v1);
	
	if(v1.empty()){
		cout << "v1为空" << endl;
	} else {
		cout << "v1不为空" << endl;
		cout << "v1的容量为: " << v1.capacity() << endl;
		cout << "v1的大小为: " << v1.size() << endl;
	}
	
	//resize() 重新指定容器大小
	v1.resize(15,10);
	printVector(v1);
	
	v1.resize(5);
	printVector(v1); 
	
}
```

### vector插入和删除

```c++
函数原型：
    push_back();									//从尾部插入元素
	pop_back();										//从尾部删除元素
	insert(const_iterator pos, ele);				//迭代器指向的位置pos插入元素lel
	insert(const_iterator pos, int count, ele);		//迭代器指向的位置pos插入count个元素ele
	erase(const_iterator pos);						//删除迭代器指向的元素
	erase(const_iterator start, const_iterator end);//删除迭代器[start,end)之间的元素
	clear();										//删除容器中的所有元素
```

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

void printVector(const vector<int> v){
	for(auto i = v.begin(); i != v.end(); i++){
		cout << *i << ' ';
	}
	cout << endl;
}

int main(){
	vector<int> v1; //无参构造
	
	for(int i = 0; i < 10; i++){
		v1.push_back(i);
	}
	printVector(v1);
	
	//删除尾部第一个元素
	v1.pop_back();
	printVector(v1); 
	
	//插入
	v1.insert(v1.begin(),100);
	printVector(v1);
	v1.insert(v1.begin(),3,100); 
	printVector(v1);
	
	//删除
	v1.erase(v1.begin());
	printVector(v1);
	v1.erase(v1.begin(), v1.begin() + 3);
	printVector(v1);
	
	//清空 
	v1.clear();
	printVector(v1);
}
```

### vector数据存取

```c++
函数原型：
    at(int idx);	//返回索引idx所指的数据
	operator[];		//返回索引idx所指的数据
	front();		//返回容器中第一个数据
	back();			//返回容器中最后一个数据
```

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int main(){
	vector<int> v1; //无参构造
	
	for(int i = 0; i < 10; i++){
		v1.push_back(i);
	}
	
	for(int i = 0; i < v1.size(); i++){
		cout << v1[i] << ' ';
		cout << v1.at(i) << ' ';
	}
	cout << endl;
	
	cout << "返回v1的第一个元素" << v1.front() << endl;
	cout << "返回v1的最后一个元素" << v1.back() << endl;
}
```

### vector互换容器

```c++
功能：
    将两个容器内的元素互换
原型：
    swap(vec);	//将vec和本身的元素互换
实际用途：
    收缩内存
```

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

void printVector(const vector<int> v){
	for(auto i = v.begin(); i != v.end(); i++){
		cout << *i << ' ';
	}
	cout << endl;
}

//实际用途:收缩内存
void test01(){
	vector<int> v;
	for(int i = 0; i < 10000; i++){
		v.push_back(i);
	}
	cout << "v的容量为：" << v.capacity() << endl;
	cout << "v的大小为：" << v.size() << endl;
	
	//巧用swap收缩内存
	vector<int>(v).swap(v);
	cout << "v的容量为：" << v.capacity() << endl;
	cout << "v的大小为：" << v.size() << endl;
} 

int main(){
	vector<int> v1; //无参构造
	vector<int> v2; 
	
	for(int i = 0; i < 10; i++){
		v1.push_back(i);
		v2.push_back(i + 10); 
	}
	printVector(v1);
	printVector(v2);
	
	v1.swap(v2);
	printVector(v1);
	printVector(v2);
	
	test01();
}
```

### vector预留空间

```c++
功能：
    减少vector在动态扩展容量时的扩展次数
函数原型：
    reserve(int len);	//容器预留len个元素长度,预留位置不初始化,元素不可访问
```

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

void test01(vector<int> &v){
	//动态空间扩展次数 
	int num = 0;
	int *p = NULL;
	
	for(int i = 0; i < 100000; i++){
		v.push_back(i);
		if(p != &v[0]){
			num++;
			p = &v[0];
		}
	}
	cout << num << endl;
}

int main(){
	vector<int> v;
	test01(v);
	v.clear();
	v.reserve(10000);
	test01(v);
} 
```

vector排序和deque排序类似

## string

```c++
本质:
	string是C++风格的字符串，而string本质是一个类
string和char*的区别:
	char*是一个指针
    string是一个类，类内部封装了char*，管理这个字符串，是一个char*型的容器
特点:
	string类内部封装了很多成员方法
    例如：查找find，拷贝copy，删除delete，替换replace，插入insert
    string管理char*所分配的内存，不用担心复制越界和取值越界等，由类内部进行负责
```



### string构造函数

```c++
构造函数原型:
	string();					//创建一个空的字符串
	string(const char* s);		//使用字符串s初始化
	string(const string& str);	//使用一个string对象初始化另一个string对象
	string(int n, char c);		//使用n个字符c初始化
```

```c++
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main(){
	string s1; //默认构造
	
	const char* str = "hello world";
	string s2(str);
	
	string s3(s2);
	
	string s4(10,'a');
	
	cout << s2 << endl;
	cout << s3 << endl;
	cout << s4 << endl;
}
```

### 字符串赋值

```c++
赋值的函数原型
    1.string& operator=(const char* s);		//char*类型字符串 赋值给当前字符串
	2.string& operator=(const string &s);	//把字符串s赋值给当前字符串
	3.string& operator=(char c);			//把字符c赋值给当前字符串
	4.string& assign(const char* s);		//把字符串s赋值给当前字符串
	5.string& assign(const char* s, int n);	//把字符串s的前n个字符赋值给当前字符串
	6.string& assign(const string &s);		//把字符串s赋值给当前字符串
	7.string& assign(int n, char c);		//把b个字符c赋值给当前字符串
```

```c++
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main(){
	string str1;				
	str1 = "Hello World";			//1
	string str2;
	str2 = str1;					//2
	string str3;
	str3 = 'a';						//3
	string str4;
	str4.assign("Hello World");		//4
	string str5;
	str5.assign("Hello World",5);		//5
	string str6;
	str6.assign(str5);				//6
	string str7;
	str7.assign(10,'a');			//7
	
	cout << str1 << endl;
	cout << str2 << endl;
	cout << str3 << endl;
	cout << str4 << endl;
	cout << str5 << endl;
	cout << str6 << endl;
	cout << str7 << endl;
	
}
```

### 字符串拼接

```c++
拼接的函数原型
    1.string& operator+=(const char* s);	//char*类型字符串 拼接到当前字符串末尾
	2.string& operator+=(const string &s);	//把字符串s拼接到当前字符串末尾
	3.string& operator+=(char c);			//把字符c拼接到当前字符串末尾
	4.string& append(const char* s);		//把字符串s拼接到当前字符串末尾
	5.string& append(const char* s, int n);	//把字符串s的前n个字符拼接到当前字符串末尾
	6.string& append(const string &s);		//把字符串s拼接到当前字符串末尾
	7.string& append(const string &s, int pos. int n);//把字符串s从pos开始的n个字符拼接到当前字														符串末尾
```

```c++
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main(){
	string str1 = "Hello";				
	str1 += " World";				//1
	string str2 = "Hello";
	str2 += str1;					//2
	string str3 = "Hell";
	str3 += 'o';					//3
	string str4 = "Hello";
	str4.append(" World");			//4
	string str5 = "Hello ";
	str5.append("Hello World",5);	//5
	string str6 = "Hello ";
	str6.append(str5);				//6
	string str7 = "Hello";
	str7.append(str6,5,6);			//7
	
	cout << str1 << endl;
	cout << str2 << endl;
	cout << str3 << endl;
	cout << str4 << endl;
	cout << str5 << endl;
	cout << str6 << endl;
	cout << str7 << endl;
	
}
```

### 字符串查找和替换

```c++
查找:
	int find(const string& str, int pos = 0) const; //从pos开始查找str第一次出现的位置
	int find(const char* s, int pos = 0) const; 	//从pos开始查找s第一次出现的位置
	int find(const char c, int pos = 0) const; 		//从pos开始查找c第一次出现的位置
	int rfind(const string& str, int pos = 0) const;//从pos开始查找str最后一次出现的位置
	int rfind(const char* s, int pos = 0) const; 	//从pos开始查找s最后一次出现的位置
	int rfind(const char c, int pos = 0) const; 	//从pos开始查找c最后一次出现的位置
	查找不到返回-1
替换:
	string& replace(int pos, int n, const string& str); //替换从pos开始的n个字符为str
	string& replace(int pos, int n, char* s); 			//替换从pos开始的n个字符为s
```

```c++
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main(){
	string str1 = "Hello Hello";
	//从左往右查找字串的位置 返回查找到的下标 查找不到返回-1
	int pos = str1.find("llo");
	cout << "pos = " << pos << endl;
	//从右往左查找字串的位置 返回查找到的下标 查找不到返回-1
	pos = str1.rfind("llo");
	cout << "pos = " << pos << endl;
	//替换最后一个llo为*** 
	str1.replace(pos,3,"***");
	cout << str1 << endl;
	
}
```

### 字符串比较

```c++
功能：
    字符串间比较
    若不相等，则从第一位开始往后比较
比较方式：
    按字符的ASCLL码进行对比
    = 返回0
    > 返回1
    < 返回-1
函数原型：
    int compare(const string &s) const; //与字符串s比较
	int compare(const char* s)const; 	//与字符串s比较
```

```c++
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main(){
	string str1 = "Hello";
	string str2 = "Helloe";
	cout << str1.compare(str2);
	
}
```

### 字符串存取

```c++
char& operator[](int n);	//通过[]方式取字符
char& at(int n);			//通过at方式获取字符
```

```c++
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main(){
	string str = "Hello";
	//读取字符串中的字符 
	for(int i = 0; i < str.size(); i++){
		cout << str[i] << endl;
		cout << str.at(i) << endl;
	}
	//修改字符串中的字符
	 str[0] = '*';
	 str.at(1) = '*';
	 
	 cout << str << endl; 
}
```

### 字符串插入和删除

```c++
功能：
    对string字符串进行插入和删除操作
函数原型：
    string& insert(int pos, const char* s);		//从pos处插入s
	string& insert(int pos, const string& s);	//从pos处插入str
	string& insert(int pos, int n, char c);		//从pos处插入n个字符c
	string& erase(int pos, int n = npos);		//从pos开始删除n个字符
```

```c++
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main(){
	string str1 = "Heo Wd&&**&*";
	string str2 = "orl";
	//插入"ll" 
	str1.insert(2,"ll");
	cout << str1 << endl;
	//插入"orl" 
	str1.insert(7,str2);
	cout << str1 << endl;
	//删除末尾六个字符
	str1.erase(11,6);
	cout << str1 << endl; 
}
```

### 字符串获取子串

```c++
功能：
    从字符串中获取想要的子串
函数原型：
    string substr(int pos = 0, int n = npos) const; //返回pos开始的n个字符组成的字符串
```

```c++
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main(){
	string email = "zhangsan@qq.com";
	//获取@前面的字符
	int pos = email.find('@');
	string str = email.substr(0,pos);
	cout << str << endl;
}
```

## deque

```c++
功能：
    双端数组：可以对头端进行插入操作
deque和vector区别：
    vector对头部的插入效率低，数据量越大，效率越低
    deque相对而言，对头部的插入删除速度比vector快
    vector访问元素时的速度会比deque快
```

### 构造函数和vector类似

### 赋值操作和vector类似

### 大小和vector类似但没有容量

### 插入和删除

```c++
插入比vector多了：
    push_front();			//在容器头部插入一个数据
	pop_front();			//删除容器第一个元素
	insert(pos,beg,end);	//在pos位置插入[beg,end)区间的数据,无返回值
```

### 数据存取和vector类似

### deque排序

```c++
#include <iostream>
#include <string>
#include <deque>
#include <algorithm>

using namespace std;

void printDeque(const deque<int>& d){
	for(auto i = d.begin(); i != d.end(); i++){
		cout << *i << ' '; 
	}
	cout << endl;
}

int main(){
	deque<int> d;
	for (int i = 10; i < 50; i += 10){
		d.push_back(i);
		d.push_front(i);
	}
	cout << "排序前：" << endl;
	printDeque(d);
	
	//sort排序 默认升序
	sort(d.begin(),d.end());
	cout << "排序后：" << endl;
	printDeque(d);
}
```

## stack

```c++
构造函数：
	stack<T> stk;
	stack(const stack &stk);			//拷贝构造函数
赋值函数：
    stack& operator=(const stack &stk);	//重载等号操作符
数据存取：
    push();		//向栈顶添加元素
	pop();		//从栈顶移除第一个元素
	top();		//返回栈顶元素
大小操作：
    empty();	//判断堆栈是否为空
	size();		//返回栈的大小
```

```c++
#include <iostream>
#include <string>
#include <stack>
#include <algorithm>

using namespace std;

int main(){
	//创建栈容器
	stack<int> s1;
	
	//向栈中添加元素
	for(int i = 0; i < 5; i++){
		s1.push(i);
	}
	
	//拷贝构造函数
	stack<int> s2(s1);
	
	//重载等号符号
	stack<int> s3;
	s3 = s1;
	
	while(!s1.empty()){
		//输出栈顶元素
		cout << "s1栈顶元素为：" << s1.top() << endl;
		s1.pop(); 
		
		cout << "s2栈顶元素为：" << s2.top() << endl;
		s2.pop();
		
		cout << "s3栈顶元素为：" << s3.top() << endl;
		s3.pop();
	}
	
	cout << "s1栈的大小为：" << s1.size() << endl; 
	cout << "s2栈的大小为：" << s2.size() << endl;
	cout << "s3栈的大小为：" << s3.size() << endl;
}
```

## queue

  ```c++
  队列不提供迭代器，更不支持随机访问
  构造函数：
      queue<T> que;
  	queue(const queue &que);			//拷贝构造函数
  赋值操作：
      queue& operator=(const queue &que);	//重载等号操作符
  数据存取：
      push();		//往队尾添加元素
  	pop();		//从队头移除第一个元素
  	back();		//返回最后一个元素
  	front();	//返回第一个元素
  大小操作：
      empty();	//判断队列是否为空
  	size();		//返回队列的大小
  ```

```c++
#include <iostream>
#include <string>
#include <queue>
#include <algorithm>
using namespace std;

class Person{
	public:
		string mName; 
		int mAge;
	public:
		Person(string name, int age){
			mName = name;
			mAge = age;
		}
};

using namespace std;

int main(){
	queue<Person> q;
	
	Person p1("孙悟空",600);
	Person p2("猪八戒",700);
	Person p3("沙悟净",500);
	
	//往队列中添加元素
	 q.push(p1);
	 q.push(p2);
	 q.push(p3);
	 
	 while(!q.empty()){
	 	//输出对头元素
		cout << "队头元素--姓名：" << q.front().mName
			 << " 年龄：" << q.front().mAge << endl;
		cout << "队尾元素--姓名：" << q.back().mName
			 << " 年龄：" << q.back().mAge << endl;
		cout << endl;
		q.pop();
	 } 
}
```

## list

```c++
链表由一系列结点组成
结点：一个是存储数据的数据域，另一个是存储下一个结点地址的指针域
STL中的链表是一个双向循环链表，既存储上个结点地址，也存储下一个结点地址
list优点：
    采用动态内存分配，不会造成内存浪费和溢出
    链表执行插入和删除操作十分方便，修改指针即可，不需要移动大量元素
list缺点：
    链表灵活，但是空间(指针域)和时间(遍历)额外耗费大
```

### list构造函数

```c++
函数原型：
	list<T> lst;            //list采用采用模板类实现,对象的默认构造形式
	list(beg,end);          //构造函数将[beg, end)区间中的元素拷贝给本身	
	list(n,elem);           //构造函数将n个elem拷贝给本身。
	list(const list &lst)   //拷贝构造函数。
```

```c++
#include <iostream>
#include <string>
#include <list>
#include <algorithm>
using namespace std;

void printList(const list<int>& l){
	for(auto it = l.begin(); it != l.end(); it++){
		cout << *it << ' ';
	}
	cout << endl;
}

using namespace std;

int main(){
	list<int>l1;
	l1.push_back(10);
	l1.push_back(20);
	l1.push_back(30);
	l1.push_back(40);

	printList(l1);
	
	//不能直接l1.begin() + 3 
	auto it = l1.begin();
	for(int i = 0; i < 3; i++)
		it++;
	list<int> l2(l1.begin(), it);
	printList(l2);

	list<int>l3(l1);
	printList(l3);
	
	list<int>l4(10,100);
	printList(l4);
}
```

### list赋值和交换

```c++
函数原型：
    list& operator=(const list &lst);   //重载等号操作符
	assign(beg, end);            		//将[beg, end)区间中的数据拷贝
	assign(n, elem);             		//将n个elem拷贝赋值给本身
	swap(lst);                       	//将lst与本身的元素互换
```

```c++
#include <iostream>
#include <string>
#include <list>
#include <algorithm>
using namespace std;

void printList(const list<int>& l){
	for(auto it = l.begin(); it != l.end(); it++){
		cout << *it << ' ';
	}
	cout << endl;
}

using namespace std;

int main(){
	list<int>l1;
	l1.push_back(10);
	l1.push_back(20);
	l1.push_back(30);
	l1.push_back(40);

	printList(l1);
	
	list<int> l2;
	l2 = l1;
	printList(l2);
	
	list<int> l3;
	l3.assign(l1.begin(), l1.end());
	printList(l3);
	
	list<int> l4;
	l4.assign(10,100);
	printList(l4);
	
	//交换l1和l4
	cout << "交换前：" << endl;
	printList(l1);
	printList(l4);
	
	cout << "交换后：" << endl; 
	l1.swap(l4);
	printList(l1);
	printList(l4);
}
```

### list大小操作

```c++
没有容量 只有大小
函数原型：
	size();				//返回容器中元素个数
	empty();			//判断容器是否为空
	resize(int num);		//重新指定容器的长度为num 若容器变长,则填充默认值0
							//					  若容器变短,则超出的元素被删除
	resize(int num,elem);	//重新指定容器的长度为num 若容器变长,则填充默认值elem
							//					  若容器变短,则超出的元素被删除
```

### list 插入和删除

```c++
函数原型：
    push_back();									//从尾部插入元素
	pop_back();										//从尾部删除元素
    push_front();									//在容器头部插入一个数据
	pop_front();									//删除容器第一个元素
	insert(const_iterator pos, ele);				//迭代器指向的位置pos插入元素lel
	insert(const_iterator pos, int n, ele);			//迭代器指向的位置pos插入count个元素ele
	insert(pos,beg,end);							//在pos位置插入[beg,end)区间的数据,无返回值
	erase(const_iterator pos);						//删除迭代器指向的元素
	erase(const_iterator start, const_iterator end);//删除迭代器[start,end)之间的元素
	remove(elem);									//删除容器中所有和elem值匹配的数据
	clear();
```

```c++
#include <iostream>
#include <string>
#include <list>
#include <algorithm>
using namespace std;

void printList(const list<int>& l){
	for(auto it = l.begin(); it != l.end(); it++){
		cout << *it << ' ';
	}
	cout << endl;
}

using namespace std;

int main(){
	list<int>l1;
	for(int i = 0; i < 10; i++){
		l1.push_back(i);
		l1.push_front(i);
	}

	printList(l1);
	
	//删除值为2的元素
	l1.remove(2);
	printList(l1); 
	 
}
```

### list 数据存取

```c++
功能描述：
    对list容器中数据进行存取
函数原型：
    front();	//返回第一个元素
	back();		//返回最后一个元素
```

```c++
#include <iostream>
#include <string>
#include <list>
#include <algorithm>
using namespace std;

void printList(const list<int>& l){
	for(auto it = l.begin(); it != l.end(); it++){
		cout << *it << ' ';
	}
	cout << endl;
}

using namespace std;

int main(){
	list<int>l1;
	for(int i = 0; i < 10; i++){
		l1.push_back(i);
	}

	printList(l1);
	
	cout << "第一个元素为：" << l1.front() << endl;
	cout << "最后一个元素为：" << l1.back() << endl;
	 
}
```

### list反转和排序

```c++
功能描述：
    将容器中的元素反转，以及将容器中的数据进行排序
函数原型：
    reverse();		//反转链表
	sort();			//链表排序
```

```c++
#include <iostream>
#include <string>
#include <list>
#include <algorithm>
using namespace std;

void printList(const list<int>& l){
	for(auto it = l.begin(); it != l.end(); it++){
		cout << *it << ' ';
	}
	cout << endl;
}

//降序排列 
bool myCompare(int val1 , int val2)
{
	return val1 > val2;
}

int main(){
	list<int>l1;
	for(int i = 0; i < 10; i++){
		l1.push_back(i);
		l1.push_back(10 - i);
	}
	printList(l1);
	
	//默认升序排列
	l1.sort();
	printList(l1);
	
	//按照规则降序排列
	l1.sort(myCompare);
	printList(l1);
}
```

### list排序案例

```c++
案例描述：将Person自定义数据类型进行排序，Person中属性有姓名、年龄、身高

排序规则：按照年龄进行升序，如果年龄相同按照身高进行降序
```

```c++
#include <iostream>
#include <string>
#include <list>
#include <algorithm>
using namespace std;

class Person{
	public:
		string mName;
		int mAge;
		int mHeigh;
	public:
		Person(string name, int age, int heigh){
			mName = name;
			mAge = age;
			mHeigh = heigh;
		}
};

//排列规则 
bool myCompare(Person &p1, Person &p2)
{
	if(p1.mAge == p2.mAge){
		return p1.mHeigh > p2.mHeigh;
	}
	else{
		return p1.mAge < p2.mAge;
	}
}

int main(){
	list<Person> L;

	Person p1("刘备", 35 , 175);
	Person p2("曹操", 45 , 180);
	Person p3("孙权", 40 , 170);
	Person p4("赵云", 25 , 190);
	Person p5("张飞", 35 , 160);
	Person p6("关羽", 35 , 200);
	
	L.push_back(p1);
	L.push_back(p2);
	L.push_back(p3);
	L.push_back(p4);
	L.push_back(p5);
	L.push_back(p6);
	
	L.sort(myCompare);
	for(auto it = L.begin(); it != L.end(); it++){
		cout << "姓名：" << it->mName << " 年龄：" 
		<< it->mAge << " 身高：" << it->mHeigh << endl;
	}
}
```

## set

```c++
简介：
	所有元素都会在插入时自动被排序
本质：
    set/multiset属于关联式容器，底层结构是用二叉树实现
set和multiset区别：
    set不允许容器中有重复元素
    multiset允许容器中有重复元素
```

### set构造和赋值

```c++
功能：
    创建set容器以及赋值
构造：
    set<T> st;						//默认构造函数
	set(const set &st);				//拷贝构造函数
赋值：
    set& operator=(const set &st);	//重载等号操作符
```

```c++
#include <iostream>
#include <string>
#include <set>
#include <algorithm>
using namespace std;

void printSet(set<int> & s)
{
	for (set<int>::iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}

int main(){
	set<int> s1;

	s1.insert(10);
	s1.insert(30);
	s1.insert(20);
	s1.insert(40);
	printSet(s1);
	
	set<int> s2(s1);
	printSet(s2);
	
	set<int> s3;
	s3 = s2;
	printSet(s3);
}
```

### set大小和交换

```c++
功能：
    size();		//判断容器中元素是否为空
	empty();	//判断容器是否为空
	swap();		//交换两个集合容器
```

```c++
#include <iostream>
#include <string>
#include <set>
#include <algorithm>
using namespace std;

void printSet(set<int> & s)
{
	for (set<int>::iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}

int main(){
	set<int> s1;

	s1.insert(10);
	s1.insert(30);
	s1.insert(20);
	s1.insert(40);
	printSet(s1);
	
	if (s1.empty())
	{
		cout << "s1为空" << endl;
	}
	else
	{
		cout << "s1不为空" << endl;
		cout << "s1的大小为： " << s1.size() << endl;
	}
	
	//交换集合
	set<int> s2;

	s2.insert(50);
	s2.insert(60);
	s2.insert(70);
	s2.insert(80);
	
	cout << "s1交换前：" << endl;
	printSet(s1);
	cout << "s2交换前：" << endl;
	printSet(s2);
	
	s1.swap(s2);
	
	cout << "s1交换后：" << endl;
	printSet(s1);	
	cout << "s2交换后：" << endl;
	printSet(s2);
}
```

### set插入和删除

```c++
功能：
	set容器进行插入数据和删除数据
函数原型：
    insert();			//在容器中插入元素
	clear();			//清除所有元素
	erase(pos);			//删除pos迭代器所指的元素，返回下一个元素的迭代器
	erase(beg,end);		//删除区间[beg,end)的所有元素，返回下一个元素的迭代器
	erase(elem);		//删除容器中值为elem的元素
```

```c++
#include <iostream>
#include <string>
#include <set>
#include <algorithm>
using namespace std;

void printSet(set<int> & s)
{
	for (set<int>::iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}

int main(){
	set<int> s1;
	//插入
	s1.insert(10);
	s1.insert(30);
	s1.insert(20);
	s1.insert(40);
	printSet(s1);

	//删除
	s1.erase(s1.begin());
	printSet(s1);

	s1.erase(30);
	printSet(s1);

	//清空
	//s1.erase(s1.begin(), s1.end());
	s1.clear();
	printSet(s1);
}
```

### set查找和统计

```c++
功能：
    对set容器进行查找数据以及统计数据
函数原型：
    find(key);		//查找key是否存在，若存在则返回该键的迭代器，若不存在则返回set.end()
	count(key);		//统计key的元素个数
```

```c++
#include <iostream>
#include <string>
#include <set>
#include <algorithm>
using namespace std;

void printSet(set<int> & s)
{
	for (set<int>::iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}

int main(){
	set<int> s1;
	//插入
	s1.insert(10);
	s1.insert(30);
	s1.insert(20);
	s1.insert(40);
	printSet(s1);

	//查找
	auto pos = s1.find(30);
	if(pos != s1.end()) {
		cout << "找到了元素：" << *pos << endl;
	} else {
		cout << "未找到元素" << endl;
	}
	
	//统计
	int num = s1.count(30);
	cout << "num：" << num << endl;
}
```

### set和multiset区别

```c++
区别：
    set不可以插入重复数据，而multiset可以
    set插入数据的同时会返回插入结果，表示插入是否成功
    multiset不会检测数据，因此可以插入重复数据
```

```c++
 #include <iostream>
#include <string>
#include <set>
#include <algorithm>
using namespace std;

void test01(){
	set<int> s;
    //s.insert()返回的是插入位置的迭代器和是否插入成功两个数据
	pair<set<int>::iterator, bool>  ret = s.insert(10);
	if (ret.second) {
		cout << "第一次插入成功!" << endl;
	}
	else {
		cout << "第一次插入失败!" << endl;
	}

	ret = s.insert(10);
	if (ret.second) {
		cout << "第二次插入成功!" << endl;
	}
	else {
		cout << "第二次插入失败!" << endl;
	}
}

void test02(){
	multiset<int> ms;
	ms.insert(10);
	ms.insert(10);

	for (multiset<int>::iterator it = ms.begin(); it != ms.end(); it++) {
		cout << *it << " ";
	}
	cout << endl;
}

int main(){
	test01();
	test02();
}
```

### set容器排序

示例一：set存放内置数据类型

```c++
#include <iostream>
#include <string>
#include <set>
#include <algorithm>
using namespace std;

class MyCompare{
	 public:
	 	bool operator()(int v1, int v2){
	 		return v1 > v2;
		 }
};

void printSet(auto st){
	for(auto it = st.begin(); it != st.end(); it++){
		cout << *it << ' ';
	}
	cout << endl;
}

int main(){
	set<int> st1;
	st1.insert(10);
	st1.insert(30);
	st1.insert(20);
	st1.insert(15);
	
	//默认是升序 
	printSet(st1);
	
	//按自己写的规则降序 
	set<int,MyCompare> st2;
	st2.insert(10);
	st2.insert(30);
	st2.insert(20);
	st2.insert(15);
	printSet(st2);
}
```

示例二：set存放自定义数据类型

```c++
#include <iostream>
#include <string>
#include <set>
#include <algorithm>
using namespace std;

class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}

	string m_Name;
	int m_Age;

};
class comparePerson
{
public:
	bool operator()(const Person& p1, const Person &p2)
	{
		//按照年龄进行排序  降序
		return p1.m_Age > p2.m_Age;
	}
};

int main(){
	set<Person, comparePerson> s;

	Person p1("刘备", 23);
	Person p2("关羽", 27);
	Person p3("张飞", 25);
	Person p4("赵云", 21);

	s.insert(p1);
	s.insert(p2);
	s.insert(p3);
	s.insert(p4);

	for (auto it = s.begin(); it != s.end(); it++)
	{
		cout << "姓名： " << it->m_Name << " 年龄： " << it->m_Age << endl;
	}
}
```



## pair对组创建

```c++
功能：
    成对出现的数据，利用对组可以返回两个数据
两种创建方式：
    pair<type, type> p(value1, value2);
	pair<type, type> p = make_pair(value1, value2);
```

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main(){
	pair<string, int> p("Tom", 20);
	cout << "姓名： " <<  p.first << " 年龄： " << p.second << endl;

	pair<string, int> p2 = make_pair("Jerry", 10);
	cout << "姓名： " << p2.first << " 年龄： " << p2.second << endl;
}
```

## map/multimap

```c++
简介：
    map中所有元素都是pair
    pair中第一个元素为key(键值),起到索引作用,第二个元素为value(实值)
    所有元素都会根据元素的键值自动排序
本质：
    map/multimap属于关联式容器，底层结构是用二叉树实现
优点：
    可以根据key值快速找到value值
区别：
    map不允许容器中有重复key值元素
    multimap允许容器中有重复key值元素
```

### map构造和赋值

```c++
构造函数原型：
	map<T1, T2> mp;
	map<const map &mp>;				//拷贝构造函数
赋值：
    map& operator=(const map &mp);	//重载等号操作符
```

```c++
#include <iostream>
#include <string>
#include <map>
#include <algorithm>
using namespace std;

void printMap(auto mp){
	for(auto it = mp.begin(); it != mp.end(); it++){
		cout << "key = " << it -> first << " value = " << it -> second << endl;
	}
}

int main(){
	map<int, int> mp1;
	mp1.insert(pair<int, int>(1,10));
	mp1.insert(pair<int, int>(2,20));
	mp1.insert(pair<int, int>(3,30));
	printMap(mp1);
	
	map<int, int> mp2(mp1);
	printMap(mp2);
	
	map<int, int> mp3;
	mp3 = mp2;
	printMap(mp3);
}
```

### map大小和交换

```c++
功能：
    统计map容器大小以及交换容器
函数原型：
    size();		//返回容器中元素个数
	empty();	//判断容器是否为空
	swap();		//交换两个集合容器
```

```c++
#include <iostream>
#include <string>
#include <map>
#include <algorithm>
using namespace std;

void printMap(auto mp){
	for(auto it = mp.begin(); it != mp.end(); it++){
		cout << "key = " << it -> first << " value = " << it -> second << endl;
	}
}

int main(){
	map<int, int> mp1;
	mp1.insert(pair<int, int>(1,10));
	mp1.insert(pair<int, int>(2,20));
	mp1.insert(pair<int, int>(3,30));
	printMap(mp1);
	
	if(!mp1.empty()){
		cout << "容器不为空" << endl;
		cout << "容器大小为："  << mp1.size() << endl;
	} else {
		cout << "容器为空" << endl;
	}
	
	map<int, int> mp2;
	mp2.insert(pair<int, int>(4,40));
	mp2[5] = 50;
	mp2[6] = 60;
	
	mp1.swap(mp2);
	cout << "交换后mp1:" << endl;
	printMap(mp1);
	cout << "交换后mp2:" << endl;
	printMap(mp2);
}
```

### map插入和删除

```c++
函数原型：
    insert();			//在容器中插入元素
	clear();			//清除所有元素
	erase(pos);			//删除pos迭代器指向的元素，返回下一个元素的迭代器
	erase(beg, end);	//删除区间[beg,end)的所有元素,返回下一个元素的迭代器
	erase(key);			//删除容器中键为key的容器
```

```c++
#include <iostream>
#include <string>
#include <map>
#include <algorithm>
using namespace std;

void printMap(auto mp){
	for(auto it = mp.begin(); it != mp.end(); it++){
		cout << "key = " << it -> first << " value = " << it -> second << endl;
	}
}

int main(){
	map<int, int> mp;
	
	//第一种插入方式
	mp.insert(pair<int, int>(1,10));
	//第二种插入方式
	mp.insert(make_pair(2,20));
	//第三种插入方式
	mp.insert(map<int, int>::value_type(3,30));
	//第四种插入方式
	mp[4] = 40;
	printMap(mp);
	
	//删除
	mp.erase(mp.begin());
	printMap(mp);
	
	mp.erase(4);
	printMap(mp);
	
	//清空
	mp.erase(mp.begin(), mp.end());
	mp.clear();
	printMap(mp);
}
```

### map查找和统计

```c++
函数原型：
    find(key);		//查找键key是否存在，若存在返回该建的迭代器，否则返回end()
	count(key);		//统计键key的个数
```

```c++
#include <iostream>
#include <string>
#include <map>
#include <algorithm>
using namespace std;

void printMap(auto mp){
	for(auto it = mp.begin(); it != mp.end(); it++){
		cout << "key = " << it -> first << " value = " << it -> second << endl;
	}
}

int main(){
	map<int, int> mp;
	mp.insert(pair<int, int>(1,10));
	mp.insert(pair<int, int>(2,20));
	mp.insert(pair<int, int>(3,30));
	printMap(mp);
	
	//查找 
	auto pos = mp.find(20);
	if(pos != mp.end()){
		cout << "找到了元素 key = " << pos->first << " value = " << pos->second << endl;
	} else{
		cout << "未找到该元素" << endl; 
	}
	
	//统计
	int num = mp.count(3);
	cout << num << endl;
}
```

### map容器排序

```c++
利用仿函数,可以改变排序规则
对于自定义数据类型，map必须要指定排序规则，同set容器
```

```c++
#include <iostream>
#include <string>
#include <map>
#include <algorithm>
using namespace std;

class MyCompare{
	public:
		bool operator()(int v1, int v2){
			return v1 > v2;
		}
};

int main(){
	map<int, int, MyCompare> mp;
	mp.insert(pair<int, int>(1,10));
	mp.insert(pair<int, int>(2,20));
	mp.insert(pair<int, int>(3,30));
	
	for(auto it = mp.begin(); it != mp.end(); it++){
		cout << "key = " << it -> first 
		<< " value = " << it -> second << endl;
	}
	
}
```

## STL-----函数对象

### 函数对象

```c++
概念：
    重载函数调用操作符的类，其对象常称为函数对象
    函数对象使用重载的()时，行为类似函数调用，也叫仿函数
本质：
    函数对象(仿函数)是一个类，不是一个函数
特点：
    函数对象在使用时，可以像普通函数那样调用，可以有参数，可以有返回值
    函数对象超出普通函数的概念，函数对象可以有自己的状态
    函数对象可以作为参数传递
```

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

////1.函数对象在使用时，可以像普通函数那样调用, 可以有参数，可以有返回值
class MyAdd{
	public:
		int operator()(int v1, int v2){
			return v1 + v2;
		}
};

//2.函数对象可以有自己的状态
class MyPrint{
	public:
		int count;
	public:
		MyPrint(){
			count = 0;
		}
		void operator()(string test){
			cout << test << endl;
			count++;
		}
};

//3.函数对象可以作为参数传递
void doPrint(MyPrint& mp, string test){
	mp(test);
}

int main(){
	MyAdd ma;
	cout << ma(1,3) << endl;
	cout << ma(10,20) << endl;
	
	MyPrint mp;
	mp("hello");
	mp("hello");
	mp("hello");
	cout << "MyPrint调用次数为：" << mp.count << endl;
	
	doPrint(mp,"world");
}
```

### 谓词

```c++
概念：
    返回bool类型的仿函数成为谓词
    如果operator接受一个参数，那么叫做一元谓词
    如果operator接受两个参数，那么叫做二元谓词
```

#### 一元谓词

```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

//一元谓词
class GreatFive{
	public:
		bool operator()(int v){
			return v > 5;
		}
}; 

void test01(){
	vector<int> v;
	for(int i = 3; i < 12; i++){
		v.push_back(i);
	}
	auto it = find_if(v.begin(), v.end(), GreatFive());
	if(it == v.end()){
		cout << "未查找到大于5的数" << endl;
	} else {
		cout << "找到：" << *it << endl; 
	}
}

int main(){
	test01();
}
```

#### 二元谓词

```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

//二元谓词
class MyCompare{
	public:
		bool operator()(int v1, int v2){
			return v1 > v2;
		}
}; 

void test01(){
	vector<int> v;
	v.push_back(30);
	v.push_back(20);
	v.push_back(10);
	v.push_back(20);
	
	cout << "默认排序" << endl;
	sort(v.begin(), v.end());
	for(auto it = v.begin(); it != v.end(); it++){
		cout << *it << ' ';
	}
	cout << endl;
	
	cout << "按照自定义规则降序排序" << endl;
	sort(v.begin(), v.end(), MyCompare());
	for(auto it = v.begin(); it != v.end(); it++){
		cout << *it << ' ';
	}
}

int main(){
	test01();
}
```

### 内建函数对象

```c++
概念：
    STL内建了一些函数对象
分类：
    算术仿函数
    关系仿函数
    逻辑仿函数
用法：
    这些仿函数所产生的对象，用法和一般函数完全相同
    使用内建函数对象，需要引入头文件#include<functional>
```

#### 算术仿函数

```c++
函数原型：
    template<class T> T plus<T>         //加法仿函数
	template<class T> T minus<T>        //减法仿函数
	template<class T> T multiplies<T>   //乘法仿函数
	template<class T> T divides<T>      //除法仿函数
	template<class T> T modulus<T>      //取模仿函数
	template<class T> T negate<T>       //取反仿函数
```

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional> 
using namespace std;

void test01(){
	//取反仿函数 
	negate<int> n;
	cout << n(50) << endl;
	
	//加法仿函数
	plus<int> p;
	cout << p(10,20) << endl; 
}

int main(){
	test01();
}
```

#### 关系仿函数

```c++
函数原型：
    template<class T> bool equal_to<T>               //等于
	template<class T> bool not_equal_to<T>           //不等于
	template<class T> bool greater<T>                //大于
	template<class T> bool greater_equal<T>          //大于等于
	template<class T> bool less<T>                   //小于
	template<class T> bool less_equal<T>             //小于等于
```

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional> 
using namespace std;

void test01(){
	vector<int> v;

	v.push_back(10);
	v.push_back(30);
	v.push_back(50);
	v.push_back(40);
	v.push_back(20);

	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
		cout << *it << " ";
	}
	cout << endl;
	
	//大于仿函数 
	sort(v.begin(), v.end(), greater<int>());
	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
		cout << *it << " ";
	}
}

int main(){
	test01();
}
```

#### 逻辑仿函数

```c++
函数原型：
    template<class T> bool logical_and<T>            //逻辑与
	template<class T> bool logical_or<T>             //逻辑或
	template<class T> bool logical_not<T>            //逻辑非
```

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional> 
using namespace std;

void PrintVector(auto v){
	for(auto it = v.begin(); it != v.end(); it++ ){
		cout << *it << ' '; 
	}
	cout << endl;
}

void test01(){
	vector<bool> v;
	v.push_back(1);
	v.push_back(0);
	v.push_back(1);
	v.push_back(0);
	
	PrintVector(v);
	
	//逻辑非  将v容器搬运到v2中，并执行逻辑非运算
	vector<bool> v1;
	v1.resize(v.size());
	transform(v.begin(), v.end(), v1.begin(), logical_not<bool>());
	PrintVector(v1);
}

int main(){
	test01();
}
```



# 其他

### 宏定义

```
1. 宏的格式 :#define <名字> <值>
   例子:#define PI 3.1415
2. 注意事项:结尾没有分号 
	 名字必须是一个单词 值可以是各种东西
	 完全的文本替换
	 如果一个宏的值中有其他的宏的名字 也会被替换
	 如果一个宏的值超过一行 最后一行之前的行末需要加 \
3. 带参数的宏:#define sum(x) ((x) + (x)) //带参数的宏 参数和整个值都要加括号
```

### 位运算

```c++
#include <stdio.h>
/*
* 1.& 按位与
* 2.| 按位或 
* 3.^ 按位异或 
*/ 
int main(){
	unsigned char c = 0xaa; //1010 1010
	printf("c = %d\n",c);
	printf("~c = %hhx\n",~c);//0101 0101
	printf("-c = %hhx\n",-c);//0101 0110
} 

```

### 防止头文件重复

```c++
C语言中
标准头文件结构: __MAX_H__ 是头文件名字
#ifndef __MAX_H__
#define __MAX_H__
/*
*
*
*/
#endif
作用: 防止重复定义

C++中
#pragma once 
作用: 防止重复定义
```



### goto语句

```c++
#include <iostream>

using namespace std;

int main(){
	cout << 1 << endl;
	cout << 2 << endl;
	goto flag;
	cout << 3 << endl;
	cout << 4 << endl;
	flag:
	cout << 5 << endl;
} 
```

### 传递二维数组给函数

```c++
#include <iostream>

using namespace std;

//形参用(*p)[]接受二维数组 
void check(int (*p)[3]){
	for(int i = 0; i < 3; i++)
		for (int j = 0; j < 3; j++)
			cout << p[i][j] << ' ';
}

int main(){
	int a[3][3] = {{1,2,3},{4,5,6},{7,8,9}};
	check(a);
}
```

### 清屏和按键继续

```c++
#include <iostream>

using namespace std;

int main(){
	int i = 1;
	while(i++){
		cout << i << endl;
		system("pause"); //请按任意键继续
		system("cls"); //清屏操作 
	}
	return 0;
}
```

### 随机数

```c++
#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main(){
	//添加随机数种子 作用: ；利用当前系统时间生成随机数 防止每次随机数一样 
	srand((unsigned int)time(NULL));
	
	//系统生成(1 ~ 100)的随机数
	int num = rand() % 100 + 1; 
	
	cout << num << endl;
}
```

## 引用

```c++
#include <iostream>
using namespace std;

/*
* 语法: 数据类型& 别名 = 原名
* 注意事项:	 不能返回局部变量的引用
*			定义时必须初始化
*			如果函数的返回值是引用 这个函数调用可以作为左值 
*/

int& test01(){
	int a = 20;
	return a;
} 

int& test02(){
	static int a = 20;
	return a;
}
int main(){
	//int& ref = test01(); 不能返回局部变量的引用 
	int& ref = test02();
	cout << ref << endl;
	test02() = 1000;
	cout << ref << endl;
	system("pause");
	return 0;
}
```

## 友元函数

### 全局函数作为友元

```c++
#include <iostream>
#include <string>

using namespace std; 

/*
* 全局函数作为友元 
*/
class Building{
	friend void goodFriend(Building* build); //全局函数作为友元
	public:
		string m_SittingRoom; //客厅 
	private:
		string m_BedRoom; //卧室 
	public:
		Building(){
			this->m_SittingRoom = "客厅";
			this->m_BedRoom = "卧室";
		} 
};

//全局函数作为友元 
void goodFriend(Building* build){
	cout << "好朋友访问" << build->m_SittingRoom << endl;
	cout << "好朋友访问" << build->m_BedRoom << endl;
}

void test01(){
	Building build;
	goodFriend(&build);
}

int main(){
	test01();
}
```

### 类作为友元

```c++
#include <iostream>
#include <string>

using namespace std;

/*
* 类作为友元 
*/ 
class Building; //声明Building类 
class goodFriend{
	public:
		goodFriend(); //成员函数在类外进行定义
		void visit(); 
	private:
		Building* build; //私有化 
};

class Building{
	friend class goodFriend; //类作为友元
	public:
		string m_SittingRoom; //客厅 
	private:
		string m_BedRoom; //卧室 
	public:
		Building();//成员函数在类外定义 
};

Building::Building(): m_SittingRoom("客厅") , m_BedRoom("卧室")
{
 } 

goodFriend::goodFriend(){
	//创建Building对象
	build = new Building; 
} 

void goodFriend::visit(){
	cout << "好朋友访问" << build->m_SittingRoom << endl;
	cout << "好朋友访问" << build->m_BedRoom << endl;
}

void test01(){
	goodFriend gf;
	gf.visit();
}

int main(){
	test01();
}
```

### 类的成员函数作为友元

```c++
#include <iostream>
#include <string>

using namespace std;

/*
* 类的成员函数作为友元 
*/ 
class Building; //声明Building类 
class goodFriend{
	public:
		goodFriend(); //成员函数在类外进行定义
		void visit01(); //普通成员函数 
		void visit02(); //友元成员函数 
	private:
		Building* build; //私有化 
};

class Building{
	friend void goodFriend::visit02(); //类的某一个成员函数作为友元
	public:
		string m_SittingRoom; //客厅 
	private:
		string m_BedRoom; //卧室 
	public:
		Building();//成员函数在类外定义 
};

Building::Building(): m_SittingRoom("客厅") , m_BedRoom("卧室")
{
 } 

goodFriend::goodFriend(){
	//创建Building对象
	build = new Building; 
} 

void goodFriend::visit01(){
	cout << "好朋友a访问" << build->m_SittingRoom << endl;
	//cout << "好朋友a访问" << build->m_BedRoom << endl;
}

void goodFriend::visit02(){
	cout << "好朋友b访问" << build->m_SittingRoom << endl;
	cout << "好朋友b访问" << build->m_BedRoom << endl;
}

void test01(){
	goodFriend gf;
	gf.visit01();
	gf.visit02();
}

int main(){
	test01();
}
```

## 多文件操作

main.cpp

```c++
#include <iostream>
#include "point.h"

using namespace std;

int main(int argc, char** argv) {
	point p1;
	p1.set_x(10);
	p1.set_y(20);
	cout << p1.get_x() << endl;
	cout << p1.get_y() << endl;
	return 0;
}
```

point.h

```c++
class point{
	private:
		int m_x;
		int m_y;
	
	public:
		void set_x(int m_x);
		int get_x();
		void set_y(int m_y);
		int get_y();
};
```

point.cpp

```c++
#include <iostream>
#include "point.h"

using namespace std;

void point::set_x(int x){
	m_x = x;
}

int point::get_x(){
	return m_x;
}

void point::set_y(int y){
	m_y = y;
}

int point::get_y(){
	return m_y;
}
```

