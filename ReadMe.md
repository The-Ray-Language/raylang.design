<img src="img/ray.fw.png" alt="Ray Logo" style="width:33%;height:33%" />

<u>English</u>|[简体中文](ReadMe.CN.md)

# The Ray Language Design Overview

### Design Philosophy

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

Well,ray is just a language aimed at  simple and efficiency. 



## In below grammar contents,"<>" represents "must" and "[]" represents "optional"

### Module System

##### import

​	No `import` ,no `using`,just a simple `get`

```ray
get console// also use  get console as con; to rename a module
```

##### export

​	To be easy ,just a `put` is enough

``` ray
put var i:int = 0
```



### Variable and constant System

```ray
var i:int
const s:string = "Hello"//constant must initalize
```

The grammar is `<var|const> name:<Type> [= value]`

### Functions

```ray
fn main(argc:int,args:string[]){//->void can leave out,and function is acceptable
	
}
```

The grammar is

```
<fn|function> name([Parameters])[->Type]{

}
```

example program

```ray
get console as con;
fn fib(n:int)->int{
	if (n == 1 | n == 2)//"OR" is just | instead of ||
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

### Comments

```ray
// Comments single line
/*
comments
multi line
*/
```

### String

```ray
var a:string = 'single line string\t  escape character such as \\n \r\n';
var b:string = 
"
raw string ,
escape character is useless
";
```

