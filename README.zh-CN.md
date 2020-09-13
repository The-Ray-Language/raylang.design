<div align="center"><img src="img/ray.fw.png" alt="Ray Logo" width="25%" height="25%" /></div>

[English](README.md)|<u>简体中文</u>

>​ Ray 设计哲学
>
> 我们是那伟大的骑士
>
>​ 拥有无穷无尽的力量
>
>​ 挥舞简单铸成的利剑
>
> 举起实用性制作的盾
>
>​ 骑着效率至上的马匹
>
>​ 誓要将世界变得更好
>
>​ -- 安德鲁 · Sc（S·c）
>
> （NKID00 翻译）

是的，Ray 是一门以简单高效为目标的语言，仅此而已

## Hello, world!

```ray
// 语句必须以分号结尾
get console as con; // 导入 console 模块并起别名 con

fn main(args: string[]) // 定义入口点
{
	con.out('Hello, world!'); // 输出 Hello, world!
}
```

## 模块

导入时没有 `import`，没有 `using`，仅仅是 `get`

```ray
get console; // 导入 console 模块
get console as con; // 导入 console 模块并起别名 con
```

​一个简单的 `put` 就足够导出了

```ray
put var i: int = 0; // 导出变量 i 供其他程序使用
```

## 变量和常量

变量在使用前需要用 `var` 来声明。声明中包含类型名。

```ray
var i: int; // 定义 int 类型变量 i，将会自动赋值为默认值
var j: int = 1; // 变量可以在定义时赋值
```

使用 `const` 来定义常量。定义中包含类型名。

```ray
const foo: string = 'bar'; // 常量必须在定义时赋值
```

变量和常量的名称只能由字母、数字和下划线组成。第一个字符不能是数字。区分大小写字母。

```ray
var aaa123: int; // 合法
var _: int; // 合法
var _1: string; // 合法
var 1_: string; // 非法
var int: int; // 非法
```

## 函数

用 `function` 或 `fn` 来定义函数

```ray
// 入口点函数，隐式指定无返回值
fn main()
{
	return; // 合法
	return 0; // 非法，不能返回值
}

// 与上面的写法等价的入口点函数写法，显式指定无返回值
function main() -> void
{
	return; // 合法
	return 0; // 非法，不能返回值
}

// 另一种入口点函数写法，传入命令行参数，显式指定返回值类型
fn main(args: string[]) -> int
{
	return; // 非法，必须返回一个值
	return 0; // 合法

	// 如果未出现返回语句，将会自动返回定义为返回值类型的变量自动初始化后的值
}

fn () { } // 无参数、无函数体、无返回值的匿名函数

```

## 运算符

与 C 语言大致相同

## 分支

用 `if` 和 `else` 来构造分支

```ray
if ('foo' == 'bar' | n == 1) // '或' 仅仅是 | 而不是 ||
{
	/* 做点什么 */
}
else if (true == false & n == 2) // '且' 也一样，else if 是可选的
{
	/* 做点什么别的 */
}
else // else 是可选的
{
	/* 做点什么更加别的 */
}
```

不使用大括号是非法的，避免造成歧义

```ray
if (foo) bar(); // 非法

if (a) { fn_a(); } // 合法
else if (b) fn_b(); // 经典的歧义语句，非法
else { fn_c(); } // 合法
```

也可以使用 `switch` 来构造分支

```ray
switch (i)
{
	1 ->
	{
		/* 当 i 等于 1 时做点什么 */

		break; // break 语句不能用于 switch 中，非法
	}

	2,3 -> // i == 2 | i == 3
	{
		/* 当 i 等于 2 或 3 时做点什么别的 */
	}

	3,4,5 -> // i 等于 3 时会依次执行两个语句块
	{
		/* 当 i 等于 3、4 或 5 时做点什么更加别的 */
	}

	-> // 其他情况
	{
		/* 做点什么非常别的 */
	}
}
```

### 循环

用 `for` 来构造循环

```ray
for (var i: int = 0; i < 20; i++) // 循环20次
{
	/* 做点什么 */
}
```

`for` 也可以用来构造无限循环（死循环）

```ray
for(;;) // 无限循环
{
	if (foo)
	{
		break; // 跳出循环
	}
	else if (bar)
	{
		continue; // 继续下一次循环
	}
}
```

注意没有 `while` 循环

### 注释

单行注释以 `//` 开头

```ray
// 这是一行单行注释
```

注释块以 `/*` 开头，以 `*/` 结尾

```ray
/* 这是一个注释块
   其中可换行 */
```

### 字符串

用 `'` 表示一个字符串字面值

```ray
var foo: string = '这是一个字符串'; // 字符串字面值
var bar: string = '\\ -> 反斜杠，\n -> 换行符'; // 字符串中可以转义
```

用 `"` 表示一个原始字符串字面值

```ray
var raw: string = "原始字符串字面值
其中可换行
\n -> 无效，仅仅是字面值";
```
