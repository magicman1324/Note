# printf

```c
#include<stdio.h>

int main() {
	int number = 100;
	
	printf("Decimal: %d\n", number);

	printf("Octal: %o\n", number);

	printf("Hexadecimal(lowercase): %#x\n", number);

	printf("Hexadecimal(highercase): %#X\n", number);
}
```

```c
#include<stdio.h>

int main() {
	int number = 100;
	
	printf("left-aligned: %10d\n", number);

	printf("show plus :%+d\n", number);

	printf("leading zero:%010d\n", number);
}
```

# scanf

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main() {
	int number=0;
	scanf("%d", &number);
	printf("%d\n", number);
	
}
```

```c
#include<stdio.h>

int main() {
	printf("please put a number\n");

	int  number1, number2, number3;
	scanf_s("%d %d %d", &number1, &number2, &number3);

	printf("your number is %d+%d+%d=%d", number1, number2, number3, number1 + number2 + number3);
}
```

# short

```c
#include<stdio.h>

int main() {

	short myShort = 500;
	
	unsigned short screenWidth = 800;
	unsigned short screenHeight = 600;

	unsigned short currentX = 499;
	unsigned short currentY = 300;

	printf("myShort=%hd\n", myShort);
	
	printf("screenSize=%hu X %hu\n", screenWidth, screenHeight);
	
	printf("Current Position=(%hu,%hu)\n", currentX, currentY);
}
```

```c
#include<stdio.h>

int main() {
	unsigned short color;

	color = 0b1111100000000000;

	printf("red: 0x%x\n", color);
	printf("red: 0x%X\n", color);
}
```

在C语言中，`0b` 是二进制字面量的前缀，表示后续数字是以二进制形式表示的数值。这种语法从 **C99标准** 开始被引入，允许开发者直接在代码中书写二进制数，使数值的位模式更直观。

在用户提供的代码中：

```c
unsigned short color = 0b1111100000000000;
```

- **`0b` 的作用**：明确告诉编译器这是一个二进制数，后续的 `1111100000000000` 是二进制位组合。这种写法比十六进制或十进制更直观地展示了数据的位分布（例如，可能表示颜色分量或标志位）。
- **兼容性**：需确保编译器支持 C99 或更高标准。旧版本编译器可能不支持此语法，需改用十六进制或位运算实现相同效果。
- **输出结果**：代码中 `printf` 使用 `%x` 和 `%X` 将二进制数以十六进制输出，因为 C 语言没有二进制格式的占位符。例如，`0b1111100000000000`（二进制）等于 `0xF800`（十六进制）。

# size_t

sizeof(xxx) 这是 size_t类型

```c
#include<stdio.h>

int main() {
	printf("sizeof short is  %zu byte(s)\n", sizeof(short));
	
	printf("sizeof unsigned size is %zu byte(s)\n", sizeof(unsigned short));

	printf("sizeof int is %zu bytes(s)\n", sizeof(int));

	printf("sizeof unsigned int is %zu bytes(s)\n", sizeof(unsigned int));

	printf("sizeof long is %zu byte(s)\n", sizeof(long));

	printf("sizeof unsigned long is %zu bytes(s)\n", sizeof(unsigned long));

	printf("sizeof long long is %zu bytes(s)\n", sizeof(long long));

	printf("sizeof unsigned long long is %zu bytes(s)\n", sizeof(unsigned long long));
}
```

```c
#include<stdio.h>

int main() {

	long number = 123;
	unsigned long number_2 = 456;
	long long number_3 = 789;
	unsigned long long number_4 = 1122;

	printf("%ld\n", number);
	printf("%lu\n", number_2);
	printf("%lld\n", number_3);
	printf("%llu\n", number_4);
}
```

# 企业级整型规范示例

```c
#include<stdio.h>
#include<stdint.h>

int main() {
	int8_t myInt8 = 127;
	uint8_t myUint8 = 255;

	int16_t myInt16 = 32767;
	uint16_t myUint16 = 65535;

	int32_t myInt32 = 2147483647;
	uint32_t myUint32 = 4294967295U;
	
	int64_t myInt64 = 9223372036854775807LL;
	uint64_t myUint64 = 18446744073709551615ULL;

	printf("size of int8_t=%zu\n", sizeof(myInt8));
	printf("size of uint8_t=%zu\n", sizeof(myUint8));

	printf("size of int16_t=%zu\n", sizeof(myInt16));
	printf("size of uint16_t=%zu\n", sizeof(myUint16));

	printf("size of int32_t=%zu\n", sizeof(myInt32));
	printf("size of uint32_t=%zu\n", sizeof(myUint32));

	printf("size of int64_t=%zu\n", sizeof(myInt64));
	printf("size of uint64_t=%zu\n", sizeof(myUint64));
}
```

# 隐式转换和显式转换

```c
#include<stdio.h>
#include<stdint.h>

int main() {

	//type conversation 类型转换
	//强制转换都必须 显式
	// 
	//无符号到有符号的转换
	uint16_t num1 = 11111;
	int16_t num2 = (int16_t)num1;
	printf("num1=%u\n", num1);
	printf("num2=%d\n", num2);

	//大范围到小范围
	int32_t num3 = 1234;
	int16_t num4 = (int16_t)num3;
	printf("num3=%d\n", num3);
	printf("num4=%d\n", num4);

	//小范围到大范围(扩展负数)
	int32_t num5 = 232133;
	int64_t num6 = (int64_t)num5;
	printf("num5=%d\n", num5);
	printf("num6=%d\n", num6);

	
}
```

# inttypes.h

[^inttypes.h]: 固定宽度整型类型格式化宏输出



```c
#include<stdio.h>
#include<stdint.h>
#include<inttypes.h>

int main() {

	int8_t myInt8 = INT8_MAX;
	uint16_t myUInt16 = UINT16_MAX;
	uint32_t myUInt32 = UINT32_MAX;
	uint64_t myUInt64 = UINT64_MAX;

	printf("myInt8=%"PRId8"\n", myInt8);
	printf("myUInt16=%"PRIu16"\n", myUInt16);
	printf("myUInt32=%"PRIu32"\n", myUInt32);
	printf("myUInt64=%"PRIu64"\n", myUInt64);
}
```

# int_leastN_t

```c
#include<stdio.h>
#include<stdint.h>
#include<inttypes.h>

int main() {

	//int_leastN_t number;
	//至少有N位，可能更多，适用于需要保证最小存储容量的可移植代码。
	//int_fastN_t 特效 8bit 16bit
	//至少有N位，但是选择速度最快的类型，适用于需要性能敏感的代码

	//标准整数类型  固定宽度整数类型
	int_least32_t playerScore = 6000;

	//初始化像素块
	int_least32_t pixelValue = 1000;

	return 0;
}
```

# IEEE754 指数偏移存储浮点数

0 ----------------------------------127--------------------------------------255

向127的左偏移 指数上的幂位负                 幂为正

 

```c
#include<stdio.h>

int main() {

	float num = 12.34f;

	//%f
	printf("using %%f: %f\n", num);

	//%e %E 科学计数法
	printf("using %%e: %e\n", num);
	printf("using %%E: %E\n", num);
	
	//%a %A 16进制浮点数 p计数法
	printf("using %%a: %a\n", num);
	printf("using %%A: %A\n", num);
}
```

# overflow,underflow

```c
#include<stdio.h>
#include<float.h>
int main() {
	float max_float = FLT_MAX;
	
	float overflow = max_float * 1000.0f;

	printf("max_float:%e\n", max_float);
	printf("overfloat:%e\n", overflow);

	float min_float = FLT_MIN;

	float underflow = min_float / 1000.0f;
	printf("min_float:%e\n", min_float);
	printf("underflow:%e\n", underflow);


}
```

# 银行家舍入

银行家舍入是一种“中点舍入”策略，当数值的小数部分正好等于0.5时，会将该值舍入到最接近的偶数

```c
#include<stdio.h>

int main() {

	float num1 = 3.15f;
	float num2 = 3.25f;

	printf("1->num1=%.1f\n", num1);
	printf("2->num2=%.1f\n", num2);

}

```

# float double 有效精度对比

```c
#include<stdio.h>
#include<float.h>

int main() {

	float float_num = 1.0 / 3.0;
	double double_num = 1.0 / 3.0;

	printf("float precision:%.20f\n", float_num);
	printf("double precision:%.20lf\n", double_num);

	printf("float max precision:%d\n", FLT_DIG);
	printf("double max precision:%d\n", DBL_DIG);
}
```

![](F:\Study\notes\C\C_photos\float，double有效精度对比.png)

实际分别为 7 16 根据IEEE754标准

