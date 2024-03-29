<div align="center"><img src="img/ray.fw.png" alt="Ray Logo" width="25%" height="25%" /></div>

<u>English</u>|[简体中文](README.zh-CN.md)

> The philosophy of Ray
>
> We are great knights.
>
> We have enough strength.
>
> With sharp swords made of easy,
>
> a strong shield made of practicality,
>
> as well as a rapid horse of efficiency,
>
> WE ARE SURE TO MAKE A BETTER WORLD!
>
> by S·c

Well, Ray is just a language aimed to be simple and efficiency.

## Hello, world!

```ray
// An instruction must end with a comma
@get console as con; // import the module 'console' and create the alias 'con'

fn main(args: string[]) // define the entry point
{
	con.out('Hello, world!'); // print 'Hello, world!'
}
```

## Module Management

To import modules, use neither `import` nor `using` but simply `get`.

```ray
@get console as {Puts}; // import the function Puts from module 'console'
@get console as con; // import the module 'console' and create the alias 'con'
```

A simple `@put` is good enough for exporting things.

```ray
@put{
 var i: int32 = 0; // export the variable 'i' for other programs
}; // ";" can be left out
```

## Variables and Constants

Before Variables are used, they must be declared using `var`. 
The type name of the variable is given in the declaration.

```ray
var i: int32; // define the variable 'i' with the type name 'int' and automatically set to the default value 0.
var j: int32 = 1; // a variable can be declared with the value set
```

Use `const` to define constants. The type name of the constant is given in the definition.

```ray
const foo: string = 'bar'; // a constant must be declared with the value set
```

Names of variables and constants are made up of letters, digits and underscores. The first character cannot be a digit. Upper-case and lower-case letters are distinct.

```ray
var aaa123: int32; // legal
var _: int32; // legal
var _1: string; // legal
var 1_: string; // illegal
var int32: int32; // illegal
```

## Functions

Functions can be defined using `function` or `fn`.

```ray
// the entry point function, implicitly specifies no return value
fn main()
{
	return; // legal
	return 0; // illegal, cannot return a value
}

// the entry point function which equals to the pervious one, explicitly specifies no return value
function main() : void
{
	return; // legal
	return 0; // illegal, cannot return a value
}

// another entry point function, needs one argument, explicitly specifies the type of the return value as 'int'
fn main(args: string[]) : int
{
	return; // illegal, must return a value
	return 0; // legal

	// automatically return the default value to the type of the return value when there is no return instruction
}

fn () { } // An anonymous function without argument, body and return value

```

## Operators

Mostly the same as the C programming language.

## Branches

Use `if` and `else` to write branches.

```ray
if ('foo' == 'bar' | n == 1) // 'or' can be done through '|' instead of '||'
{
	/* do something */
}
else if (true == false & n == 2) // 'and' is the same as 'or', 'else if' is optional
{
	/* do something else */
}
else // 'else' is optional
{
	/* do something more else */
}
```

It is illegal to write branches without braces, in order to avoid ambiguity.

```ray
if (foo) bar(); // illegal

if (a) { fn_a(); } // legal
else if (b) fn_b(); // classic ambiguous instruction, illegal
else { fn_c(); } // legal
```

Another way to write branches is using `match` instruction.

```ray
match (i)
{
	case 1 {
		/* do something when 'i' equals to 1 */

		//break; // 'break' instruction cannot be used in 'switch', illegal
	}

	2,3{ // i == 2 | i == 3
		/* do something else when 'i' equals to 2 or 3 */
	}

	//"3","4","5"{ //only available when i is a string, and the two instruction blocks will be executed in order when 'i' equals to "3"
	//	/* do something more else when 'i' equals to "3", "4” or “5” */
	//}

	else{ // other conditions
		/* do something ultra else */
	}
}
```

## Loops

Use `for` to write loops.

```ray
for (var i: int32 = 0; i < 20; i++) // loop 20 times
{
	/* do something */
}
```

`for` can also be used to write infinite loops.

```ray
for (;;) // infinite loop， or 'while(true) instead'
{
	if (foo)
	{
		break; // break the loop
	}
	else if (bar)
	{
		continue; // continue to the next round of the loop
	}
}
```

Note that there's no `while` loop.

## Comments

Single line comments start with `//`.

```ray
// this is a single line comment
```

Comment blocks start with `/*`, end with `*/`.

```ray
/* this is a comment block
   which can consist multiple lines */
```

## String Literals

Use `'` or `"` to quote string literals.

```ray
var foo: string = "this is
a string"; // a  multiple lines string literal is legal
var bar: string = '\\ -> backslash, \n -> new line'; // escaping can be used in string literals
```

## Object Oriented Programming

It is simplified a lot.The grammar was as follow.Notice that all class must be **Uppercase**！

```ray
@get console as con;//import the module console

//Any class is inherited from the type Object
class Obj{
	
    // Constructor
	public fn Obj(){
	}
	
	// Destructor is an operator overrideing function
	public fn __DEL__(){
		con.out("The object was deleted!");
	}
};

class Human{

};

//Multiple inheritance is not ok，and it's deprecated.
//class People extends Obj,Human //will cause a compile error
//{

//};

fn main(args: string[]){
	var o:Obj = new Obj();//the variable ‘o' is only a reference
}

```

## Interfaces

Abstract class to implement "multiple inheritance" which is recommended

```ray

interface Animal{//can inherit other interface(s)
	function kill():void;
};

class Cat implements Animal{
	protected var name:string;
	
	public function Cat(name:string){
		this.name = name;
	}
	//After declaring this method，Cat can be casted to Animal
	public function kill(){
	
	}
};
```

