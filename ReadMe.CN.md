<img src="img/ray.fw.png" alt="Ray的Logo" width="33%" height="33%" />

[English](ReadMe.md)|<u>简体中文</u>

# Ray语言设计总览

### 设计哲学

>​				The philosophy of Ray
>
>​		We are great knights.
>
>​		We have enough strength.
>
>​		With  sharp  swords made of easy,
>
>​		 a strong shield made of practicality,
>
>​		as well as a rapid horse of efficiency,
>
>​		WE ARE SURE TO MAKE A BETTER WORLD!
>
>​						By Andrew ·Sc  (S·c)

是的,Ray是一门以简单高效为目的的语言，仅此而已. 



## 以下语法内容,<>为必选，[]为可选



### 模块系统

##### 导入

​	没有`import` ,没有`using` ,仅仅是`get`.

``` ray
get console//也可以使用 get console as con; 给模块起别名
```

##### 导出

​	为了简单，一个`put`足够了。

```ray
put int i:int =0
```

### 变量和常量系统

```ray
var i:int
const s:string = "Hello"//常量必须初始化
```

语法是 `<var|const> 名称:<类型> [= value]`

### 函数

```ray
fn main(argc:int,args:string[]){//->void 可以 省略,并且 function 也可。
	
}
```

语法是

```
<fn|function> 名称([参数])[->类型]{

}
```

示例程序

```ray
get console as con;
function fib(n:int)->int{
	if (n == 1 | n == 2)// "或" 仅仅是 | 而不是 ||
	{
		return 1;
	}
	else
	{
		return fun(n - 1) + fun(n - 2);
	}
}

fn main(argc:int,args:string[]){
	con.out(fib(25));
}
```

### 注释

```ray
//单行注释
/*
注释
多行
*/
```

### 字符串

```ray
var a:string = '单行字符串\t 转义字符例如\\n \r\n';
var b:string = 
"
原始字符串 ,
escape character is useless
";
```

