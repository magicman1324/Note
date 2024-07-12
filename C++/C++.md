

# 重载运算符

```c++
#include<iostream>
#include<string>
struct Vector2 {
	float x, y;

	Vector2(float x, float y)
		:x(x), y(y) {}

	Vector2 Add(const Vector2& other)const {
		return Vector2(x + other.x, y + other.y);
	}
	Vector2 operator+(const Vector2&other) const {
		return Add(other);
	}

	Vector2 Multiply(const Vector2& other)const {
		return Vector2(x * other.x, y * other.y);
	}

	Vector2 operator*(const Vector2& other) const {
		return Multiply(other);
	}

	bool operator==(const Vector2 & other)const {
		return x == other.x && y == other.y;
	}

	bool operator!=(const Vector2& other)const {
		return !(*this == other);
	}
};

std::ostream& operator<<(std::ostream& stream, const Vector2& other) {
	stream << other.x << "," << other.y;
	return stream;
}

int main() {
	Vector2 position(4.0f, 5.0f);

	Vector2 speed(0.5f, 1.5f);

	Vector2 powerup(1.1f, 1.1f);

	Vector2 result1 = position.Add(speed.Multiply(powerup));
	Vector2 result2 = position+speed*powerup;
	bool result3 = (result1 == result2);
	std::cout << result2 << std::endl;
	std::cout << result3 << std::endl;
	std::cin.get();
}
```

# 智能指针

```c++
#include<iostream>
#include<string>
#include<memory>
//unique 指针
class Entity {
public:
	Entity() {
		std::cout << "created" << std::endl;
	}
	~Entity() {
		std::cout << "destroy" << std::endl;
	}
	void Print(){}

};

int main() {
	{
		std::unique_ptr<Entity>entity = std::make_unique<Entity>();


		entity->Print();
	}

	std::cin.get();

}
```

```c++
#include<iostream>
#include<string>
#include<memory>
//share 指针
class Entity {
public:
	Entity() {
		std::cout << "created" << std::endl;
	}
	~Entity() {
		std::cout << "destroy" << std::endl;
	}
	void Print(){}

};

int main() {
	{	
		std::shared_ptr<Entity>e0;
		{
			std::shared_ptr<Entity>sharedentity = std::make_shared<Entity>();
			e0 = sharedentity;
		}
	}
	std::cin.get();

}
```

sharedptr  引入 引用计数 计数器为0时 才销毁 共享堆中的内存

weakptr 解决sharedptr  循环引用的问题

# 浅拷贝和深拷贝



1  在未定义显示拷贝构造函数的情况下，系统会调用默认的拷贝函数——即浅拷贝，它能够完成成员的一一复制。当数据成员中没有指针时，浅拷贝是可行的；但当数据成员中有指针时，如果采用简单的浅拷贝，则两类中的两个指针将指向同一个地址，当对象快结束时，会调用两次析构函数，而导致指针悬挂现象，所以，此时，必须采用深拷贝。

2 深拷贝与浅拷贝的区别就在于深拷贝会在堆内存中另外申请空间来储存数据，从而也就解决了指针悬挂的问题。简而言之，当数据成员中有指针时，必须要用深拷贝。

```c++
#include<iostream>
#include<string>
class String {
private:
	char* m_Buffer;
	unsigned int m_Size;
public:
	String(const char* string) {
		m_Size = strlen(string);
		m_Buffer = new char[m_Size + 1];
		memcpy(m_Buffer, string, m_Size);
		m_Buffer[m_Size] = 0;
	}

	String(const String& other) 
		:m_Size(other.m_Size)
	{
		std::cout << "copy string" << std::endl;
		m_Buffer = new char[m_Size + 1];
		memcpy(m_Buffer, other.m_Buffer, m_Size+1 );
	}

	~String() {
		delete[]m_Buffer;
	}

	char& operator[](unsigned int index) {
		return m_Buffer[index];
	}
	friend std::ostream& operator<<(std::ostream& stream, const String& string);
};

std::ostream& operator<<(std::ostream& stream, const String&string) {
	stream << string.m_Buffer;
	return stream;
}

void PrintString(const String& string) {
	std::cout << string << std::endl;
}

int main() {
	String string = "Wang";
	String second = string;
	
	second[2] = 'q';

	PrintString(string);
	PrintString(second);

	std::cin.get();
}
```

# ->的使用

```c++
#include<iostream>
#include<string>

class Entity {
public:
	int x;
public:
	void Print() const { std::cout << "Hello" << std::endl; }
};

class ScopedPtr {
private:
	Entity* m_Obj;
public:
		ScopedPtr(Entity* entity)
			:m_Obj(entity){}
		~ScopedPtr() {
			delete m_Obj; 
		}
		Entity* operator->() {
			return m_Obj;
		}
		const Entity* operator->() const  {
			return m_Obj;
		}
};

int main() {
	const ScopedPtr entity = new Entity();
	entity->Print();

	std::cin.get();
}
```

## 求变量的地址偏移

```c++
#include<iostream>
#include<string>

struct Vector3 {
	float x, y, z;
};

int main() {
	int offset = (int)&((Vector3*)nullptr)->x;
	std::cout << offset << std::endl;
	
}
```

# vector优化

事先确认 数组大小

使用emplace_back 而不是 push_back

- push_back 的过程

构造一个临时对象

调用移动构造函数把临时对象的副本拷贝到容器末尾增加的元素中

调用析构释放临时对象

- emplace_back 的过程

调用构造函数在容器末尾增加一个元素

```c++
#include<iostream>
#include<string>
#include <vector>

struct Vertex {
	float x, y, z;
	Vertex(float x, float y, float z)
		:x(x), y(y), z(z) {
	}

	Vertex(const Vertex& vertex)
		:x(vertex.x), y(vertex.y), z(vertex.z) {
		std::cout << "Copied" << std::endl;
	}
};

int main() {
	std::vector<Vertex> vertices;
	vertices.reserve(3);
	vertices.emplace_back(1,2,3 );
	vertices.emplace_back(4, 5, 6);
	vertices.emplace_back(7, 8, 9);

	std::cin.get();

}
```

# static

```c++
#include<iostream>
#include<string>
#include <vector>

class Singleton {
public:
	static Singleton& Get() {
		static Singleton instance;
		return instance;
	}

	void Hello(){
		std::cout << "hello" << std::endl;
	}
};

int main() {
	Singleton::Get().Hello();
	
}
```

# template

```c++
#include<iostream>
#include<string>

template<typename T>

void print(T value) {
	std::cout << value << std::endl;
}

int main() {
	print(3);
	print(4.4f);
	print("he");
	std::cin.get();
}

```

# stack 和 heap 内存分配

 每个程序/进程都有自己的stack和heap

每个线程在创建时都创建自己的stack 而 heap在所有线程之间共享

stack 类似一个Cpu指令   分配相邻的内存空间   移动栈顶指针  实现分配  	

heap    用new关键词-》调用malloc-》遍历访问 空闲列表  

# Macros

# auto

# Function Pointer

```c++
#include<iostream>

void HelloWorld(int a) {
	std::cout << "Hello World Value:" << a << std::endl;
}

int main() { 
	typedef void(*HelloWorldFunction)(int a);
	HelloWorldFunction function = HelloWorld;
	function(5);
	function(7);
	function(4);
	function(2);
	std::cin.get();
}
```

```c++
#include<iostream>
#include <vector>

void PrintValue(int value) {
	std::cout << "Value:" << value << std::endl;
}

void ForEach(const std::vector<int>& values,void(*func)(int )) {
	for (int value : values)
		func(value);
}

int main() { 
	std::vector<int>values = { 1,5,4,2,3 };
	ForEach(values, PrintValue);
	
	std::cin.get();
}
```

```c++
#include<iostream>
#include <vector>



void ForEach(const std::vector<int>& values,void(*func)(int )) {
	for (int value : values)
		func(value);
}

int main() { 
	std::vector<int>values = { 1,5,4,2,3 };
	ForEach(values, [](int value) {std::cout << "Value: " << value << std::endl; });
	
	std::cin.get();
}
```

# Lambda

```c++
#include<iostream>
#include <vector>
#include<functional>


void ForEach(const std::vector<int>& values,const std::function<void(int)> &func) {
	for (int value : values)
		func(value);
}

int main() { 
	std::vector<int>values = { 1,5,4,2,3 };
	auto it = std::find_if(values.begin(), values.end(), [](int value) {return value > 3; });
	std::cout << *it << std::endl;


	int a = 5;
	auto lambda = [=](int value) {std::cout << "Value: " << a << std::endl; };
	ForEach(values, lambda);
	
	std::cin.get();
}
```

# namespace

```c++
#include<iostream>
#include <string>
namespace apple {
	void print(const char* text) {
		std::cout << text << std::endl;
	}

	void print_again() {}
	}



namespace orange {
	void print(const char* text) {
		std::cout << text << std::endl;
	}
}

int main() {
	using apple::print;//仅print使用apple命名空间
	print("hello");
	apple::print_again();//print_again 仍需标明
	std::cin.get();
}
```

# thread

```c++
#include<iostream>
#include<thread>

static bool is_Finished = false;

void DoWork() {
	using namespace std::literals::chrono_literals;
	std::cout << "started  id=" << std::this_thread::get_id << std::endl;
	while (!is_Finished) {
		std::cout << "Working..\n";
		std::this_thread::sleep_for(1s);
	}
}

int main() {
	std::thread worker(DoWork);

	std::cin.get();
	is_Finished = true;
	worker.join();
	std::cout << "finished.\n"; 
	std::cin.get();

}
```

# timing

```c++
#include<iostream>
#include<thread>

struct Timer {
	std::chrono::time_point<std::chrono::steady_clock>start, end;
	std::chrono::duration<float> duration;

	Timer() {
		start = std::chrono::high_resolution_clock::now();
	}

	~Timer() {
		end = std::chrono::high_resolution_clock::now();
		duration = end - start;

		float ms = duration.count() * 1000.0f;
		std::cout << "Time took " << ms << "ms" << std::endl;
	}
};

void Function() {
	Timer timer;
	for (int i = 0; i < 100; i++) {
		std::cout << "hello\n" ;
	}
}
int main() {
	Function();
	
	std::cin.get();
}
```

# type punning  类型双关

```c++
![virtual destructor](F:\Study\notes\C++\virtual destructor.png)#include<iostream>

struct Entity
{
	int x, y;
};

int main() {
	Entity e = { 5,8 };
	int* position = (int*)&e;
	int y = *(int*)((char*)&e + 4);

	std::cout << y << std::endl;

	std::cout << position[0] << "," << position[1] << std::endl;

	std::cin.get();
}
```

# virtual destructor

destructor 无virtual

![](F:\Study\notes\C++\virtual destructor.png)

无法正常调用 析构函数 ，造成内存泄漏



```c++
#include<iostream>

class Base {
public:
	Base() {m_Array = new int[5]; std::cout << "Base Constructor\n"; }
	virtual ~Base() { delete[]m_Array; std::cout << "Base Destructor\n"; }
private:
	int* m_Array;
};

class Derived :public Base
{
public:
	Derived() { std::cout << "Derived Constructor\n"; }
	~Derived() { std::cout << "Derived Destructor\n"; }
};


int main() {
	Base* base = new Base();
	delete base;
	std::cout << "-------------------------------------\n";
	Derived* derived = new Derived();
	delete derived;
	std::cout << "-------------------------------------\n";
	Base* ploy = new Derived();
	delete ploy;

	std::cin.get();
}
```

# Conditional and Action breakpoints

