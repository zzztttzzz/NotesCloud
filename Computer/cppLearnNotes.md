## Compiler and Linker

* 编译器将source code编译为`.obj`文件，即一个个的translation unit。链接器将各个文件链接到一起形成可执行文件。
* `#include`宏定义仅仅是复制头文件到源文件中，`#define`宏仅仅是替换代码。
* 头文件中`#pragmma once`防止多次declare函数。

## 变量类型以及指针

* `char`占1byte，`int`通常占4bytes，取决于compiler
* 指针实质上都是integer。定义时需要说明指向的变量类型，例如`char* ptr`,`int* ptr`分别指向`char`以及`int`类型。指针的大小通常为4bytes，可以表示4GB个地址。
* `void`指针仅仅是保持了所有指针都可以赋值给它的特性，个人认为完全可以不用。因为它不能操作指向的对象，强制转换后才可以，既然提前data的type，就完全可以定义一个指向该datatype的指针了？
* `Reference`的使用较为方便，`int& ref = a`，改变`ref`即可改变`a`的值。



## Class and Struct

* `class`默认是private权限，而`struct`默认是public权限，二者在c++中的区别仅此而已。网友普遍说：如果定义数据结构用`struct`，定义对象用`class`。

* 写一个`class`时可以将private, public的函数以及变量分开写，例如：

  ```c++
  class Log
  {
  public:
  	const int LogLevelError = 0;
  	const int LogLevelWarning = 1;
  	const int LogLevelInfo = 2;
  private:
  	int m_LogLevel = LogLevelInfo;
  public:
  	void SetLevel(int level)
  	{
  		m_LogLevel = level;
  	}
  	void Info(const char* message)
  	{
  		if (m_LogLevel>=LogLevelInfo)
  			std::cout << "[Info]:  " << message << std::endl;
  	}
  	void Warn(const char* message)
  	{
  		if (m_LogLevel >= LogLevelWarning)
  			std::cout << "[Warning]:  " << message << std::endl;
  	}
  	void Error(const char* message)
  	{
  		if (m_LogLevel >= LogLevelError)
  			std::cout << "[Error]:  " << message << std::endl;
  	}
  };
  ```



## Static

* `static`keyword，意味着变量只会在当前的源码中被link，尽量避免更多的全局变量。
* 意味着，所有函数以及类内声明的变量以及函数都会被当做当前源文件中的"全局变量"。
* `::` is known as the *scope resolution operator*.  作用域符号。
  可以用来访问`class`的`static`变量，例如：`SomeClass::x=8;`
* **单例模式**：没有完全理解，以后作为一个专题。



## enum

* 可以定义新的枚举类型datatype，例如：

  ```c++
  enum ball {red, yellow=5, blue, green, black};
  ```

  枚举量默认从0开始计数，未指定的较前一个递增1。

* 括号内的变量在作用域内会被当做整型而使用。
* 全局定义的话可能存在scope内命名污染的问题，不能再有跟枚举量相同的变量名。参考：
  https://blog.csdn.net/victorydh123/article/details/73520808



## constructor and destructor

* constructor 可以简化初始化class，少写个初始化的函数。类内成员函数的名称和类名相同即可。

* destructor类名前加`~`即可。参看代码：

  ```c++
  #include <iostream>
  
  class Entity {
  public:
  	float X, Y;
  	Entity()
  	{
  		X = 0.0f;
  		Y = 0.0f;
  		std::cout << "Constructed Entity!" << std::endl;
  	}
  
  
  	~Entity() {
  		std::cout << "Destroyed Entity" << std::endl; 
  	}
  
  	void print() 
  	{
  		std::cout << X << ", " << Y << std::endl;
  	}
  };
  
  
  void function()
  {
  	Entity e;
  	e.print();
  }
  
  int main()
  {
  	function();
  	std::cin.get();
  }
  ```



## Inheritance(继承)

* 继承另一个类内的所有对象，还可以自己添加新的对象进去；而且可以作为以父类为输入的函数的输入。
* `class Child : public Parents`.



## 28 29 Virtual Functions & Interface(Pure virtual function)

* `new`关键字就是开辟一个新的堆，然后指向声明变量的首地址。

  ```c++
  new int;//开辟一个存放整数的存储空间，返回一个指向该存储空间的地址(即指针)
  new int(100);//开辟一个存放整数的空间，并指定该整数的初值为100，返回一个指向该存储空间的地址 　　
  new char[10];//开辟一个存放字符数组(包括10个元素)的空间，返回首元素的地址 　　
  new int[5][4];//开辟一个存放二维整型数组(大小为5*4)的空间，返回首元素的地址 　　
  float *p=new float (3.14159);//开辟一个存放单精度数的空间，并指定该实数的初值为//3.14159，将返回的该空间的地址赋给指针变量p 　　
  ```

* 配合`delete`使用

* 虚函数理解cherno的意思主要是说：通过基类访问派生类定义的函数，只能借助指针实现多态。

* 继承类的函数定义后最好加上`override`关键字

* 定义interface只需要指定基类函数为0，派生类内必须指定该函数才能调用

  ```c++
  class Entity
  {
  public:
  	//virtual std::string GetName() { return "Entity"; }
  	virtual std::string GetName() = 0;
  };
  ```



## 30 Visibility

* `class`的私有变量其继承也无法访问，如果想要访问的话，可以将`private`关键字改为`protected`



## 31 Arrays

* Array就是个指针，指向第一个元素的内存地址，以下代码合法。

  ```c++
  int example[5];
  int* p = example;
  ```

* 指针加法需要关注指针的类型，一般如果是`int*`，则加2相当于地址加8，因为`int`占4个byte。

* 可以使用`new`分配一个数组，这样example即堆上的某个地址。

  ```c++
  int* example = new int[5];
  ```

* `#include <array>`即可使用库函数

  ```c++
  std::array<int, 5> another;
  std::cout << another.size() << std::endl;
  ```



## 32 Strings

* 基础的string以ASCII为基础，由char衍生。string就是char的array。
* `const`关键字定义指针后，内容无法改变。

* string的结尾是NULL，即ASCII为0。

* c++跟matlab类似，`""`双引为char array，`''`为char。

* 两种方式，不用指针的话最后需要加0，表示终止。

* ```c++
  	const char* name = "zzdzzd";
    	char name2[7] = { 'z','z','d','z','z','d',0};
  ```

* `const char`不能直接相加，想拼接字符串的话使用std::string可以直接加：

  ```c++
  std::string name3 = "zzdzzd";
  	name3 = name3 + "hehehe"; // name3 += "hehehe";
  ```

* string传入函数的时候多使用`&`，可以不用copy一份。



## String Literal

* 使用`const char* name`定义string，无法使用`name[2]='t'`改变某个字符的值，因为是`const`。

* `wchar_t`, `char16_t`, `char32_t`三种长字符串

  ```c++
  	const char* name = u8"zzdzzd";
  	const wchar_t* name2 = L"zzdzzd";
  	const char16_t* name3 = u"zzdzzd";
  	const char32_t* name4 = U"zzdzzd";
  ```

* `std::string_literals`命名空间内的s后缀可以转换const char

  ```c++
  std::u32string name0 = U"zzdzzd"s + U"zzdzzd";
  ```

* `R`operator，raw string，类似于python内的用法，括号内部的string所见即所得，不会转义。



## 34 Const

* `const`keyword保证了变量初始化后不能改变。

* `const int* a`和`int* const a`完全不同，前者可以改变a的指向，后者不能改变a的指向，前者是一个指向常量的指针（常量指针），后者是一个指针常量（指针本身是常量）。

* 还可以使用`const int* const a`，值和地址都不能变……

* class内部的`const`keyword放在函数声明后，则该函数无法更改class内部的变量值。

  ```c++
  class Entity
  {
  private:
  	int m_X, m_Y;
  public:
  	int GetX() const
  	{
          //m_X = 2;  //非法
  		return m_X;
  	}
  	void SetX(int x)
  	{
  		m_X = x;
  	}
  };
  ```

* 结合返回值的类型，甚至可以这样写：

  ```c++
  class Entity
  {
  private:
  	int* m_X, m_Y;
  public:
  	const int* const GetX() const
  	{
  		return m_X;
  	}
  	void SetX(int* x)
  	{
  		m_X = x;
  	}
  };
  ```

  如果调用GetX函数返回的ptr内容和指向都无法改变。

* 使用`const Entity& e`作为函数的输入时，访问Entity类内成员函数需要保证该函数是const function。

  ```c++
  void Print(const Entity& e)
  {
  	std::cout << e.GetX() << std::endl;
  }
  ```

  当GetX函数没声明为const function时会报错，因为无法保证其不会改变初始引用的Entity实例的值。
  此处多看34Const代码。

* 如果使用了const function仍然想在函数内改变某个值，可以使用`mutable`关键字声明一个变量，不受const function的约束。



## 35Mutable

* ```c++
  class Entity
  {
  private:
  	std::string m_Name;
  	mutable int m_DebugCount = 0;
  public:
  	const std::string& GetName()  const 
  	{
  		m_DebugCount++;
  		return m_Name; 
  	}
  };
  ```

  const function内仍然想改变变量的值，使用`mutable`

* ```c++
  	int x = 8;
    	auto f = [=]() mutable
    	{
    		x++;
    		std::cout << x << std::endl;
    	};
    	f();
  ```

  后续再跟进`auto`的用法。运行结束后`x`依然等于8。

* 传递原生的变量到函数中，例如`int`,`char`类型，直接建立局部变量即可；如果传入一个自建的`class`，可以尽量使用引用，降低复制的开销。 

## 36 Member Initializer Lists

* 初始化class第一种常规写法：

  ```c++
  class Entity
  {
  private:
  	std::string m_Name;
  public:
  	Entity()
  	{
  		m_Name = "Unknown";
  	}
  	Entity(const std::string& name)
  	{
  		m_Name = name;
  	}
  
  	const std::string& GetName() const { return m_Name; }
  };
  ```

  写两个constructor，分别针对不同的初始化情况。

* 另外就是使用memory initializer lists：

  ```c++
  class Entity
  {
  private:
  	std::string m_Name;
  	
  public:
  	Entity()
  		:m_Name("Unknown")
  	{
  	}
  	Entity(const std::string& name)
  		: m_Name(name)
  	{
  	}
  
  	const std::string& GetName() const { return m_Name; }
  };
  ```

  

* 默认constructor可能对函数体内的类初始化两次，例如：

  ```c++
  class Example
  {
  public:
      Example()
      {
          std::cout << "default" << std::endl;
      }
      Example(int x)
      {
          std::cout << x << std::endl;
      }
  };
  class Entity
  {
      Example m_Example;
  public:
      Entity()
      {
          m_Example = Example(8);
      }
  };
  ```

  实例化Entity的时候会对Example初始化两次。

  ```c++
  class Entity
  {
      Example m_Example;
  public:
      Entity()
      	: m_Example(8)
      {
      }
  };
  ```

  则只会初始化一次。

* 所以初始化的时候只需要使用member initializer lists，不用原始的方式，这样可以提高性能。



## 37 Ternary Operator

* 代替if...else语句：

  ```c++
  	int s_Level = 1, s_Speed = 2;
  	if (s_Level > 5)
  		s_Speed = 10;
  	else
  		s_Speed = 5;
  
  	int s_Speed = s_Level > 5 ? 10 : 5;
  ```

* 可以更快一点，直接返回一个`s_Speed`变量而不用预定义。

* 还可以嵌套，但是感觉用处不大，可读性不强。



## 38 Heap

* scope内部的函数默认都是创建在stack上，一旦结束scope，栈就会清空。使用`new`在heap上开辟内存空间，并取出地址，即使namespace结束也可以访问变量的值。

  ```c++
  int main()
  {
  	Entity* e;
  	{
  		Entity* entity = new Entity("zzdzzd");
  		e = entity;
  		std::cout << (*entity).GetName() << std::endl;
  		
  	}
  	std::cin.get();
  	delete e;
  }
  ```

  `entity`变量被清空后，在`delete`执行前都可以通过`e`访问到该实例的成员变量。



## 39 New

* 在heap上创建一个类：

  ```c++
  Entity *e  = new Entity();
  Entity *e  = (Entity*)malloc(sizeof(Entity));
  ```

  二者唯一的区别是使用`new`会调用constructor，而下面的不会，c++中在堆中创建类时不建议使用

* new一个array后，使用`delete [] `.

* delete一个指针后，stack中的内容清空，但是指针还是指向该地址，本质上只是delete了指针指向的内容。



## 40 Implicit Conversion

* ```c++
  class Entity
  {
  private:
  	std::string m_Name;
  	int m_Age;
  public:
  	Entity(std::string name)
  		: m_Name(name), m_Age(-1) {}
  	Entity(int age)
  		: m_Name("Unknown"), m_Age(age) {}
  };
  
  ```

  以上的类定下，实例化的时候：

  ```c++
  Entity e(24);
  Entity e1("zzdzzd");
  ```

  分别定义了两个实例，然而还有另外一种定义方式：

  ```c++
  Entity e = 24;
  Entity e1 = "zzdzzd";
  ```

  这样属于隐式转换，将`int`和`const char[7]`转化为Entity。

* 当声明另外一个函数

  ```c++
  void PrintEntity(const Entity& entity)
  {
  	//Printing;
  }
  ```

  此时同样可以采用如下的调用方式：

  ```c++
  PrintEntity(24);  // implicit conversion convert int 24 to an Entity.
  PrintEntity("zzdzzd"); // Error! No definition of a constructor which convert 
  						//	const char[7] to Entity;
  ```

  第二种错误原因是没有定义从const char array到Entity的constructor。更正即可：

  ```c++
  PrintEntity(std::string("zzdzzd"));
  PrintEntity(Entity("zzdzzd"));
  ```

  尽量避免隐式转化。

* `explicit`规定了constructor只能显示传入指定类型的参数，隐式转换非法。



## 41 Operator and Operator Overloading

* 自定义的数据结构需要实现加减乘除等基本操作，可以定义operator简化代码。

  ```c++
  #include <iostream>
  #include <string>
  
  struct Vector2
  {
  	float x, y;
  	Vector2(float x, float y)
  		:x(x), y(y)
  	{}
  
  	Vector2 Add(const Vector2& other) const
  	{
  		return Vector2(x + other.x, y + other.y);
  	}
  	
  	Vector2 Multiply(const Vector2& other) const
  	{
  		return Vector2(x * other.x, y * other.y);
  	}
  };
  
  int main()
  {
  	Vector2 position(4.0f, 4.0f);
  	Vector2 speed(0.5f, 1.5f);
  	Vector2 powerup(1.1f, 1.1f);
  
  	Vector2 result = position.Add(speed.Multiply(powerup));
  
  	std::cin.get();
  }
  ```

  加上operator overload之后如下：

  ```c++
  	Vector2 operator+(const Vector2& other) const
  	{
  		return Add(other);
  	}
  ```

  就可以在主函数中使用`Vector2`类的`+`了。

  ```c++
  Vector2 reesult = position + speed;
  ```



## 42 This

* `this`关键字在类内使用，本质上是个`const *`，指向该类。
* const function内部的`this`是const pointer，普通函数内部的`this`仅仅是个pointer。



## 43 Object Lifetime

* 栈上创建的变量，脱离了scope其lifetime就结束了。

* 想要在堆上新建一个变量，脱离scope使其lifetime也结束的方法（本质上就是写一个类，唯一的成员变量是个指向目标类的指针，进入scope的时候construct该类，在destructor里面delete指针即可。）：

  ```c++
  class ScopePtr
  {
  private:
  	Entity* m_Ptr;
  public:
  	ScopePtr(Entity* ptr)
  		: m_Ptr(ptr)
  	{
  
  	}
  	~ScopePtr()
  	{
  		delete m_Ptr;
  	}
  };
  ```



## 44 Smart Ptr

* 为了解决指针内存分配的问题

* Unique Pointer：不能被指向另一个unique pointer。

  ```c++
  		std::unique_ptr<Entity> entity(new Entity());
  		std::unique_ptr<Entity> e1 = entity;  //无法指向另一个uniquepointer
  		Entity* e0 = entity;   //没有定义从unique ptr到Entity*的conversion
  ```

* shared Pointer：指向内容可以被多个ptr共享，直到最后一个lifetime结束，指向内容才会销毁。

* weak Pointer：可以被多个ptr共享，但是第一个ptr的lifetime结束后，指向内容就会销毁。

  ```c++
  int main()
  {
  	{
  		std::shared_ptr<Entity> e0;
  		{
  			std::shared_ptr<Entity> sharedEntity = std::make_shared<Entity>();
  			e0 = sharedEntity;
  		}  //本行执行后sharedEntity的lifetime结束，但是依然没有destroy Entity.
  	}  //e0的lifetime结束后Entity被destroy.
  	std::cin.get();
  }
  ```

  替换`shared_ptr`为`weak_ptr`效果不同，e0的lifetime结束后Entity就被destroy。



## 45 Copy Constructors

* 自定义一个类，新建一个实例，再建一个该实例的copy。例如：

  ```c++
  class String
  {
  private:
  	char* m_Buffer;
  	unsigned int m_Size;
  public:
  	String(const char* string)
  	{
  		m_Size = strlen(string);
  		m_Buffer = new char[m_Size+1];
  		memcpy(m_Buffer, string, m_Size);
  		m_Buffer[m_Size] = 0;
  	}
      ~String()
      {
          delete[] m_Buffer;
      }
  };
  ```

  在主函数中：

  ```c++
  String string = "zzdzzd";
  String second = string;
  ```

  此时`second`相当于是`string`的一份copy。如果不写copy constructor，默认会把`string`的两个成员变量copy给`second`，一个是`char*`，一个是`unsigned int`。并不会触发constructor，没有重新new一个内存。两个`String`类成员指针变量均指向的是同一个地址，最后destructor会报错，因为delete了同一个地址两次。

* 如果不想浅复制，想深复制的话，需要写一个copy constructor（拷贝函数）：

  ```c++
  	String(const String& other)
  		:m_Size(other.m_Size)
  	{
  		std::cout << "Copyed !" << std::endl;
  		m_Buffer = new char[m_Size + 1];
  		memcpy(m_Buffer, other.m_Buffer, m_Size + 1);
  	}
  ```

  这样便会在copy时触发copy constructor，从而重新new一块内存。

* 当把String做为一个函数的传入变量时，同样也会触发copy constructor，此时即为深拷贝。事实上传入函数完全没必要深拷贝，所以**Always using const reference as input parameter**。



## 46 Arrow operator

* `->`相当于指针解引用。
* 可以使用运算符重载，例如定义一个指针类的引用操作。



## 47 Dynamic Array

* 使用c++的库函数`std::verctor`，相当于一个container容器。

* 基本用法：`std::vector<int> varName`.
  定义一个数据结构，并重载`<<`操作符（省略代码）

  ```c++
  struct Vertex
  {
  	float x, y, z;
  };
  ```

  在主函数中：

  ```c++
  int main()
  {
  	std::vector<Vertex> vertices;
  	vertices.push_back({ 1, 2, 3 });
  	vertices.push_back({ 4,5,6 });
  
  	for (int i = 0; i < vertices.size(); i++)
  		std::cout << vertices[i] << std::endl;
  	
  	for (const Vertex& v : vertices)
  		std::cout << v << std::endl;
  	vertices.clear();
  
  	std::cin.get();
  }
  ```

* 容器的函数用法：
  清除内部所有变量`vertices.clear();`

  清除某元素`vertices.erase(veritces.begin() + 1);`

* 将vector传入函数的时候，同样使用const reference避免拷贝变量。



## 48 Optimizing Vector

* 如果直接使用`push_back`向vector内加入元素，每一次`push_back`操作都会将之前容器内所有的类都复制一次。
* 提前指定好`vertices.reserve(4)`，里面有4个元素的话，每一次`push_back`则只会触发一次当前类的复制构造函数。
* 如果使用`vertices.empalce_back(1,2,3)`，则原地触发构造函数，而不用触发复制构造函数，更快捷。



## 49 Dynamic Library

* Static libary会被build到.exe文件中，而Dynamic library则只是在运行的时候被链接。

* include时，使用`""`会首先搜索相对路径，如果没有则会从include path里面搜索。使用`<>`则是标准库函数。

* gfw3dll.lib和gfw3.dll前者是后者的指针？

  当编译通过后，.exe文件目录下如果没有gfw3.dll则会报错，复制至该目录下即可。



## 51 Making libraries(Multiple Projects)

* Solution下可以有多个Projects，当Game作为主函数体的Project，Engine作为外部依赖库的时候，需要将Project Properties中Engine的Configuration type设置为Static Library.
* include 问题，使用双引号本质上是利用路径访问，最好在Configuration Properties中设置Additional Include Directories为：`$(SolutionDir)Engine\src`，这样可以在Game主Project的源文件中直接`include “engine.h”`
* 在Game Project中需要add reference，添加外部的Engine依赖库以后，编译链接Game会同时编译链接Engine。



## 52 Deal with Multiple return



## 53 Templates in c++

* 多态的实现防止写很多重载的函数，使用`template <typename T>`，函数的入口参数可以直接写为：`Print(T someValue)`。
  * C++可以自动检测出`Print(5)`输入`int`，`Print("hehe")`输入为`const char`。
    可以指定`Print<char>(64)`，传入类型的变量。
* 可以利用`template <int N>`定义一个未知的`N`，主函数中输入`Array<N> array;`，可以任意定义类`Array`的长度，具有扩展性。
* 类似地，template可以结合使用。`template <typename T , int N>`。可以定义任意类型以及任意长度的`Array`类。



## 54 Stack and heap memory

* 使用`new`来在heap上分配一个内存空间，Stack会更快一些。
* stack上的lifetime会随着一个scope结束而结束，heap则会长很多，如果不使用智能指针需要手动delete。
* `new`调用了`malloc`，可以自动计算返回指针的大小，并且系统提供一个freelist，new的时候在freelist中寻找一块连续的block。



## 55 Macro

* 宏就是预编译过程中的代码替换。

* 使用

  ```c++
  #define LOG(x) std::cout<< x << std::endl
  ```

  可以定义一个具有函数功能的宏，尽量不要在末尾添加`;`

* 在工程设置中添加preprocessor的预定义，可以方便地使用宏：

  ```c++
  #ifdef PR_DEBUG
  #define LOG(x) std::cout << x << std::endl
  #else 
  #define LOG(x)
  ```

  可以根据环境不同选择是否输出。

* `\`可以跨越当前行，宏定义超过一行的内容



## 56 Auto

* 基本的用法，让编译器自动判断数据类型并赋值。

  ```c++
  auto a = 4;  // int
  auto b = 'c';  //char
  auto c ="zzdzzd";  //const char*
  ```

* `auto`可以一定程度省略工作量，例如定义一个函数：

  ```c++
  std::string GetName()
  {
  	return "zzdzzd";
  }
  ```

  主函数中调用：

  ```c++
  auto name = GetName();
  ```

  当改变函数的返回类型为`char*`时，主函数中的类型也会随之改变，而若不用`auto`，事实上也可以运行，因为编译器具有隐式转换，会把`char*`隐式转换为`std::string`。各有利弊。

* 复杂返回值使用`auto`，可以更优雅，其他情况尽量少使用，不知道函数干了什么。



## 57 std array

* 工作在栈上，速度很快
* `std::array<int, 5> stdarray={0,1,2,3,4};`，拥有很多库函数，个人理解可以和`std::vector`相比较。

* 内存对齐问题，计算类的size很重要。
* `iterator`可以方便地类似于指针形式地访问容器内的变量；`vector.end()`指向的是最后一个元素后面的索引。
* 