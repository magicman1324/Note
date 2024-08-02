

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

# Benchmarking

```c++
#include<iostream>
#include<memory>
#include<chrono>

class Timer
{
public:
	Timer() {
		m_StartTimePoint = std::chrono::high_resolution_clock::now();
	}

	~Timer() {
		Stop();
	}

	void Stop(){
		auto endTimePoint = std::chrono::high_resolution_clock::now();
		auto start = std::chrono::time_point_cast<std::chrono::microseconds>(m_StartTimePoint).time_since_epoch().count();
		auto end = std::chrono::time_point_cast<std::chrono::microseconds>(endTimePoint).time_since_epoch().count();
		
		auto duration = end - start;
		double ms = duration * 0.001;

		std::cout << duration << "us(" << ms << ")ms\n";
	}
private:
	std::chrono::time_point<std::chrono::high_resolution_clock>m_StartTimePoint;
};

int main() {
		int value = 0;
		{
			Timer timer;
			for (int i = 0; i < 1000000; i++)
				value += 2;
		}
		std::cout << value << std::endl;

	__debugbreak();
}
```

```c++
#include<iostream>
#include<memory>
#include<chrono>
#include<array>
class Timer
{
public:
	Timer() {
		m_StartTimePoint = std::chrono::high_resolution_clock::now();
	}

	~Timer() {
		Stop();
	}

	void Stop(){
		auto endTimePoint = std::chrono::high_resolution_clock::now();
		auto start = std::chrono::time_point_cast<std::chrono::microseconds>(m_StartTimePoint).time_since_epoch().count();
		auto end = std::chrono::time_point_cast<std::chrono::microseconds>(endTimePoint).time_since_epoch().count();
		
		auto duration = end - start;
		double ms = duration * 0.001;

		std::cout << duration << "us(" << ms << ")ms\n";
	}
private:
	std::chrono::time_point<std::chrono::high_resolution_clock>m_StartTimePoint;
};

int main() {
	struct Vector2 {
		float x, y;
	};
	std::cout << "make shared\n";
	{
		std::array<std::shared_ptr<Vector2>, 10000>sharedPtrs;
		Timer timer;
		for (int i = 0; i< sharedPtrs.size(); i++) {
			sharedPtrs[i] = std::make_shared<Vector2>();
		}
	}
	std::cout << "new shared\n";
	{
		std::array<std::shared_ptr<Vector2>, 10000>sharedPtrs;
		Timer timer;
		for (int i = 0; i < sharedPtrs.size(); i++) {
			sharedPtrs[i] = std::shared_ptr<Vector2>(new Vector2());
		}
	}
	std::cout << "make unique\n";
	{
		std::array<std::unique_ptr<Vector2>, 10000>sharedPtrs;
		Timer timer;
		for (int i = 0; i < sharedPtrs.size(); i++) {
			sharedPtrs[i] = std::make_unique<Vector2>();
		}
	}
}
```

# 结构化绑定

```c++
#include<iostream>
#include<tuple>
#include<string>

struct Person {
	std::string Name;
	int age;
};

std::tuple<std::string, int> CreatePerson() {
	return { "wang",21 };
}


//无结构化绑定需使用get tie函数
int main() {
    //get
	auto person = CreatePerson();
	std::string& name = std::get<0>(person);
	int age= std::get<1>(person);
	//tie
	std::string name;
	int age;
	std::tie(name, age) = CreatePerson();
}
```

```c++
#include<iostream>
#include<tuple>
#include<string>

//c++17 提供结构化绑定 只需一行
std::tuple<std::string, int> CreatePerson() {
	return { "wang",21 };
}



int main() {
	auto [name, age] = CreatePerson();
	std::cout << name << std::endl;
}
```

# struct和class区别

1，可见性

struct 不添加权限修饰符 默认为pubic

class   不添加权限修饰符 默认为private

2.struct 更多是关于变量，而class 关于功能

3.继承的时候用class

# optional

```c++
#include<iostream>
#include<fstream>
#include<optional>

std::optional < std::string>ReadFileAsString(const std::string& filepath) {
	std::ifstream stream(filepath);
	if (stream) {
		std::string result;
		//read File
		stream.close();
		return result;
	}
	return {};
}



int main() {
	std::optional < std::string>data = ReadFileAsString("data.txt");
	
	std::string value = data.value_or("Not present");
	std::cout << value << std::endl;
	if (data) {
		std::cout << "read the file successfully\n";
	}
	else {
		std::cout << "could not read the file \n";
	}
	std::cin.get(); 
}
```

# variant

有点类似于加强版的union，里面可以存放复合数据类型，且操作元素更为方便。
可以用于表示多种类型的混合体，但同一时间只能用于代表一种类型的实例。  

大小为 最大类型的大小+ 元数据大小

```c++
#include<iostream>
#include<variant>
#include<optional>
#include <string>

union ss {
	std::string name;
	double age;
};

int main() {
	std::variant<std::string, int>data;
	data = "wang";
	std::cout << std::get<std::string>(data) << "\n";

	data = 2.0;
	
	std::cout << std::get<int>(data) << "\n";
	std::cout << "string:" << sizeof(std::string) << "\n";
	std::cout << "int:" << sizeof(int) << "\n";
	std::cout << "data:"<<sizeof(data) << "\n";
	std::cout << "ss:" << sizeof(ss) << "\n";
	std::cin.get();
}
```

# Singleton

```c++
#include<iostream>

class Random {
public:
	Random(const Random&) = delete;

	static Random& Get() {
		static Random instance;
		return instance;
	}

	static float Float()
	{
		return Get().IFloat();
	}
private:
	float IFloat() { return m_RandomGenerator; }
	Random (){}
	float m_RandomGenerator=0.55f;
};

int main() {
	float number = Random::Float();
	std::cout << number << std::endl;

}
```

# small string optimization

如果string 大小>=16bytes  将会调用new malloc 堆分配

<16  不会堆分配

```c++
#include<iostream>

void* operator new(size_t size) {
	std::cout << "allocating " << size << "bytes\n";
	return malloc(size);
}

int main() {
	std::string name = "china lfaif sjds";
	std::cin.get();
}
```

# track memory allocation

```c++
#include<iostream>
#include<memory>

struct AllocationMetrics
{
	uint32_t TotalAllocated = 0;
	uint32_t TotalFreed = 0;
	uint32_t CurrentUsage() { return TotalAllocated - TotalFreed; }
};

static AllocationMetrics s_AllocationMetrics;

void* operator new(size_t size) {
	s_AllocationMetrics.TotalAllocated += size;
	return malloc(size);
}

void operator delete(void* memory,size_t size) {
	s_AllocationMetrics.TotalFreed += size;
	free(memory);
}


struct Object {
	int x, y, z;
};

static void PrintMemoryUsage() {
	std::cout << "memory usage:" << s_AllocationMetrics.CurrentUsage() << "bytes\n";
}

int main() {
	PrintMemoryUsage();
	std::string name = "china";
	PrintMemoryUsage();
	{	
		std::unique_ptr<Object>obj = std::make_unique<Object>(); 
		PrintMemoryUsage();
	}
	PrintMemoryUsage();
}
```

# lvalue rvalue

```c++
#include<iostream>

void PrintName(const std::string& name) { //左值引用
	std::cout <<"[lvalue]:" << name << std::endl;
}

void PrintName(const std::string&& name) {//右值引用
	std::cout << "[rvalue]:" << name << std::endl;
}

int main() {
	std::string firstname = "wang";
	std::string lastname = "hongbo";
	
	std::string fullname = firstname + lastname;

	PrintName(fullname);
	PrintName(firstname + lastname);
}


```

# 移动语义

```c++
#include<iostream>

class String {
public:
	String() = default;
	String(const char* string) {
		printf("Created\n");
		m_Size = strlen(string);
		m_Data = new char[m_Size];
		memcpy(m_Data, string, m_Size);
	}

	String(const String& other) {
		printf("Copied\n");
		m_Size = other.m_Size;
		m_Data = new char[m_Size];
		memcpy(m_Data, other.m_Data, m_Size);
	}

	String(String&& other) noexcept {
		printf("Moved\n");
		m_Size = other.m_Size;
		m_Data = other.m_Data;
		
		other.m_Size = 0;
		other.m_Data = nullptr;
	}

	~String() {
		printf("Destoryed\n");
		delete m_Data;
	}

	void Print() {
		for (uint32_t i = 0; i < m_Size; i++) {
			printf("%c", m_Data[i]); 
		}
	}
private:
	char* m_Data;
	uint32_t m_Size;
};

class Entity {
public:
	Entity(const String& name) 
	: m_Name(name)
	{

	}

	Entity(String&& name)
		: m_Name((String&&)name) // 转换
	{

	}

	void PrintName() {
		m_Name.Print();
	}
private:
	String m_Name;
};

int main() {
	Entity entity("wang");
	entity.PrintName();

	std::cin.get();
}
```

```c++
#include<iostream>

class String {
public:
	String() = default;
	String(const char* string) {
		printf("Created\n");
		m_Size = strlen(string);
		m_Data = new char[m_Size];
		memcpy(m_Data, string, m_Size);
	}

	String(const String& other) {
		printf("Copied\n");
		m_Size = other.m_Size;
		m_Data = new char[m_Size];
		memcpy(m_Data, other.m_Data, m_Size);
	}

	String(String&& other) noexcept {
		printf("Moved\n");
		m_Size = other.m_Size;
		m_Data = other.m_Data;
		
		other.m_Size = 0;
		other.m_Data = nullptr;
	}

	String& operator=(String&& other) noexcept {

		printf("Moved\n");
		if (this != &other) {
			delete[]m_Data;
			m_Size = other.m_Size;
			m_Data = other.m_Data;

			other.m_Size = 0;
			other.m_Data = nullptr;
		}return *this;

	}

	~String() {
		printf("Destoryed\n");
		delete m_Data;
	}

	void Print() {
		for (uint32_t i = 0; i < m_Size; i++) {
			printf("%c", m_Data[i]); 
		}
		printf("\n");
	}
private:
	char* m_Data;
	uint32_t m_Size;
};

class Entity {
public:
	Entity(const String& name) 
	: m_Name(name)
	{

	}

	Entity(String&& name)
		: m_Name((String&&)name)
	{

	}

	void PrintName() {
		m_Name.Print();
	}
private:
	String m_Name;
};

int main() {
	/*Entity entity("wang");
	entity.PrintName();*/

	String apple = "Apple";
	String dest;
	std::cout << "apple: ";
	apple.Print();
	std::cout << "dest: ";
	dest.Print();

	dest = std::move(apple);
	std::cout << "apple: "; 
	apple.Print();  
	std::cout << "dest: ";
	dest.Print();
 
	

	std::cin.get();
}
```

