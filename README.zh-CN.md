<div align="center"><img src="img/ray.fw.png" alt="Ray Logo" width="25%" height="25%" /></div>

[English](README.md)|<u>简体中文</u>

> Ray 设计哲学
>
> 我们是那伟大的骑士
>
> 拥有无穷无尽的力量
>
> 挥舞简单铸就的利剑
>
> 举起实用性构成的盾
>
> 骑着效率至上的战马
>
> 誓要将世界变得更好
>
> -- S·c
>
> （NKID00 翻译）

是的，Ray 是一门以简单高效为目标的语言，仅此而已

## Hello, world!

```ray
// 语句必须以分号结尾
@get console as con; // 导入 console 模块并起别名 con

fn main(args: string[]) // 定义入口点
{
	con.out('Hello, world!'); // 输出 Hello, world!
}
```

## 模块

导入时没有 `import`，没有 `using`，仅仅是 `@get`

```ray
@get console { Puts }; // 导入 console 模块里的puts函数
@get console as con; // 导入 console 模块并起别名 con
```

一个简单的 `@put` 就足够导出了

```ray
@put {
	var i: int32 = 0; // 导出变量 i 供其他程序使用
};// ";" 可以省略
```

## 变量和常量

变量在使用前需要用 `var` 来声明。声明中包含类型名。

```ray
var i: int32; // 定义 int 类型变量 i，将会自动赋值为默认值
var j: int32 = 1; // 变量可以在定义时赋值
```

使用 `const` 来定义常量。定义中包含类型名。

```ray
const foo: string = 'bar'; // 常量必须在定义时赋值
```

变量和常量的名称只能由字母、数字和下划线组成。第一个字符不能是数字。区分大小写字母。

```ray
var aaa123: int32; // 合法
var _: int32; // 合法
var _1: string; // 合法
var 1_: string; // 非法
var int32: int32; // 非法
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
function main() : void
{
	return; // 合法
	return 0; // 非法，不能返回值
}

// 另一种入口点函数写法，传入命令行参数，显式指定返回值类型
fn main(args: string[]) : int
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

也可以使用 `match`来构造分支

```ray
match (i)
{
	case 1 {
		/* 当 i 等于 1 时做点什么 */

		//break; // break 语句不能用于 switch 中，非法
	}

	case 2,3 { // i == 2 | i == 3
		/* 当 i 等于 2 或 3 时做点什么别的 */
	}

	//"3","4","5"{ // 仅当i是字符串时可用
	//	/* 当 i 等于 3、4 或 5 时做点什么更加别的 */
	//}

	else{ // 其他情况
		/* 做点什么非常别的 */
	}
}
```

## 循环

用 `for` 来构造循环

```ray
for (var i: int32 = 0; i < 20; i++) // 循环20次
{
	/* 做点什么 */
}
```

`for` 也可以用来构造无限循环（死循环）

```ray
for(;;) // 无限循环 或者 while(true)
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

## 注释

单行注释以 `//` 开头

```ray
// 这是一行单行注释
```

注释块以 `/*` 开头，以 `*/` 结尾

```ray
/* 这是一个注释块
   其中可换行 */
```

## 字符串

用 `'`或`“` 表示一个字符串字面值

```ray
var foo: string = "这是一个
字符串"; // 字符串字面值,多行字符串也是合法的
var bar: string = '\\ : 反斜杠，\n : 换行符'; // 字符串中可以转义
```

## 面向对象编程

极大的简化了.语法如下,注意，类名必须**大写**！.

```ray
@get console as con;//导入模块 console

//任何类一律继承自类型Object
class Obj{
	
    // 构造函数
	public fn Obj(){
	
	}
	
	// 析构函数
	public fn __DEL__(){
		con.out("The object was deleted!");
	}
};

class Human{

};

//class People extends Obj,Human //编译错误：多继承被弃用
//{

//};


fn main(args: string[]){
	var o:Obj = new Obj();//这个变量仅仅是引用
}

```

## 接口

抽象类，推荐的"多继承"实现方法

```ray
interface Animal{
	function kill():void;
};

class Cat implements Animal{
	protected var name:string;
	
	public function Cat(name:string){
		this.name = name;
	}
	//定义了这个方法以后，Cat可以被强制转化到Animal
	public function kill(){
	
	}
};
```

## 泛型

使用 `object`类型实现非const变量的运行时类型识别.

```ray
fn add(a:object,b:object): object{
	if(typeof(a) != typeof(b)){
		return null;
	}
	if(typeof(a).isNum){
		return uint64(a) + uint64(b);
	}
	else{
		return null;
	}
}
fn main(){
	const obj:int32 = int32(add(1,2)); // null 会导致错误，可以被异常机制捕获
	return;
}
```

Type 对象支持包括

| 方法\属性                            | 作用                                 |
| ------------------------------------ | ------------------------------------ |
| isNum:bool                           | 是否是数值类型/数组                  |
| isString:bool                        | 是否是字符串类型/数组                |
| isObject:bool                        | 是否是由类构造的对象/数组            |
| typeName:string                      | 类型的名称（字符串）                 |
| isArray:bool                         | 是否是数组                           |
| isNull:bool                          | 是否是空                             |
| isBaseOf(type:string):bool           | 是否是type的基类                     |
| isChildOf(type:string):bool          | 是否是type的子类                     |
| isImpled(interface:string):bool      | 是否实现了interface这个接口          |
| has(member:string):bool              | 是否拥有member这个成员（不包括函数） |
| get(member:string):object            | 取得member这个属性                   |
| set(member:string,value:object):bool | 设置member这个属性                   |

