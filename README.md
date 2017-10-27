Mana Programming Language
===
### Norice: WIP
# I. Mana Programming Language

## I.1. Keywords
Like any language, Mana has reserved keywords, which are:
`let`, `mut`, `in`, `class`, `interface`, `local`, `for`, `foreach`, `while`, `repeat`, `if`, `else`, `as`, `is`, `match` 

## I.2. Primitive Data Types
Mana comes with 12 built-in basic data types, which are:

|Name|Explication|Range|
|:---:|:---|:---|
|`u8`|8-bit wide unsigned integer|0 to 255|
|`i8`|8-bit wide signed integer|-128 to 127|
|`u16`|8-bit wide unsigned integer|0 to 65,535|
|`i16`|16-bit wide signed integer|-32768 to 32767|
|`u32`|32-bit wide unsigned integer|0 to 4,294,967,295|
|`i32`|32-bit wide signed integer|–2,147,483,648 to 2,147,483,647|
|`u64`|64-bit wide unsigned integer|0 to 18,446,744,073,709,551,615|
|`i64`|64-bit wide signed integer|–9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|
|`f32`|32-bit wide floating point number|3.4E +/- 38 (7 digits)|
|`f64`|64-bit wide floating point number|1.7E +/- 308 (15 digits)|
|`char`|A single UTF-8 Character|`?`|
|`bool`|Boolean value (8-bit sized) |`true` or `false`|


## I.3. Operators

|Precedence| Operator|Description|Associativity|Overloadable|
|:---:|:---:|:---:|:---:|:---:|
|1|`++`|postfix incerement| LTR|**Y**|
|1|`--`|postfix decerement| LTR|**Y**|
|1|`()`|function call| LTR|**Y**|
|1|`[]`|array/tuple subscripting| LTR|**Y**|
|1|`.`|class member/method access| LTR|**N**|
|1|`::`|module variable/function/type access| LTR|**N**|
|2|`++`|prefix increment| RTL|**Y**|
|2|`--`|prefix decrement| RTL|**Y**|
|2|`+`|**unary** plus| RTL|**Y**|
|2|`-`|**unary** minus| RTL|**Y**|
|2|`!`|logical not| RTL|**Y**|
|2|`~`|bitwise not| RTL|**Y**|
|2|`sizeof`|size-of | RTL|**N**|
|2|`as`|type polymorphism| RTL|**N**|
|3|`*`| multiplication| LTR|**Y**|
|3|`/`| division | LTR|**Y**|
|3|`%`| remainder| LTR|**Y**|
|4|`+`| addition| LTR|**Y**|
|4|`-`| substraction| LTR|**Y**|
|5|`>>`| bitwise right shift| LTR|**Y**|
|5|`<<`| bitwise left shift| LTR|**Y**|
|6|`<`| greater | LTR|**Y**|
|6|`<=`| greater or equal| LTR|**Y**|
|6|`>`| less| LTR|**Y**|
|6|`>=`| less or equal| LTR|**Y**|
|7|`==`| equality test| LTR|**Y**|
|7|`!=`| unequality test| LTR|**Y**|
|8|`&`| bitwise AND| LTR|**Y**|
|9|`^`| bitwise XOR| LTR|**Y**|
|10|`|`|bitwise OR| LTR|**Y**|
|11|`&&`| logical AND| LTR|**Y**|
|12|`||`| local OR| LTR|**Y**|
|13|`=`| Assignment | RTL|**Y**|
|13|`+=`| Assignment by sum | RTL|**Y**|
|13|`-=`| Assignment by difference | RTL|**Y**|
|13|`*=`| Assignment by product| RTL|**Y**|
|13|`/=`| Assignment by quotient| RTL|**Y**|
|13|`%=`| Assignment by remainder| RTL|**Y**|
|13|`<<=`| Assignment by bitwise left shift| RTL|**Y**|
|13|`>>=`| Assignment by bitwise right shift| RTL|**Y**|
|13|`&=`| Assignment by bitwise AND| RTL|**Y**|
|13|`^=`| Assignment by bitwise XOR| RTL|**Y**|
|13|`|=`| Assignment by bitwise OR| RTL|**Y**|

## I.4. Literal Values

### I.4.a. Integers

|Regex|Semantic|Example|
|:---:|:---:|:---:|
|`0[b|B][0-1]+`|Base 2 (Bin) numeric|`0b1001`|
|`0[0-7]+`|Base 8 (Oct) numeric|`05647`|
|`[1-9][0-9]*`|Base 10 (Dec) numeric|`5464987`|
|`0[x|X][0-9a-fA-F]+`|Base 16 (Hex) numeric|`0xffeEA325845`|

### I.4.b. Floats/Doubles
Floating literal can only decimals. The regex used to validate floating points is the following: `[+|-]?(?:[0-9]*)(?:.[0-9]+)(?:[e|E]-[0-9]+)?f?`
The final `f` character is optional, and it indicates that the literal is of type float (f32) and not double (f64; by default)

### I.4.c. Boolean
Boolean literal are either `true` or `false`.

### I.4.d. Strings
Mana strings are by default UTF-8.
There are two types of strings in Mana:

- Formattable Strings
- Normal Strings

The only difference is that a formattable String can have expressions injected inside it. This type of strings starts with double quotes.

Examples:
```ml
let w = "world"
let str1 = 'hello, '+w
let str2 = `hello ${w}`
```

### I.4.e. Character
Single characters are represented as a UTF-8 character. The `char` data type does not necessary have a size of 8 bits (Like in C).

Example:
```ml
let c1: char = '竜'
```

## I.5. Import Statement
Import statements serve to add additional dependencies to the current file

```ebnf
<Import> ::= import '(' <Import List> ')'

<Import List> ::= <Import Element> <Import List>
                | <Import Element>

<Import Element> ::= <Import Simple>
                   | <Import All>
                   | <Import From>

<Import Simple> ::= Identifier '.' <Import Simple>
                  | Identifier

<Import All> ::= Identifier '.' <Import All>
               | Identifier '.' '*'

<Import From> ::= Identifier '.' <Import From>
                | Identifier '{' <Import Simple From> '}'

<Import Simple From> ::= <Import Simple> ',' <Import Simple From>
                       | <Import Simple>

```

## I.6. Variable Declaration
A variable is declared using the `let` keywords. By default, variables in Mana are **immutables**. Inorder to define a mutable variable, one would need to use the `mut` modifier to declare a variable as **mutable**. In case of a class or a module, a variable can be considered local if it is desired to be used only inside its parent  container. In such cases, the `local` modifier can be used. Note that local is allowed only to define local class members and local package variables.

Syntax:

```bnf
<LVar Decl> ::= 'let'               <Decl Vars> '=' <Expr List>
              | 'let'               <Decl Vars> 
              | 'let' 'mut'         <Decl Vars> '=' <Expr List>
              | 'let' 'mut'         <Decl Vars>
              | 'let' 'local'       <Decl Vars> '=' <Expr List>
              | 'let' 'local'       <Decl Vars> 
              | 'let' 'mut' 'local' <Decl Vars> '=' <Expr List>
              | 'let' 'mut' 'local' <Decl Vars> 
              | 'let' 'local' 'mut' <Decl Vars> '=' <Expr List>
              | 'let' 'local' 'mut' <Decl Vars> 

<Decl Element> ::= Identifier
                 | Identifier ':' <Type>

<Decl List> ::= <Decl Element> ',' <Decl List>
              | <Decl Element>             

<Decl Vars> ::= '(' <Decl List> ')'
              | <Id List> ':' <Type>
              | <Id List>
```

Mana does not support null references, there is **No**`null` or `undefined` values. A variable is either explicitly or implicitly assigned to a value. (see [I.2. Null Pattern](#))

Examples:
```ml
let x: u32 = 255;
let mut y = x
let z: u32

// declaring and initializing multiple variables
let local a, b: char = 'a', 'z'

// declaring and unpacking from tuple
let mut (c, d) = ('c', 'y')
// or
let mut (e: char, f: i32) = ('c', -1)
```

## I.6 Function Declaration

Mana distinguishes between normal functions, lambda expressions and class methods. They can all be used in the same way, but they are compiled differently.

A function is declared only within a module.

Syntax:

```bnf
<Fn Decl> ::= <Modifiers> 'fn' '(' <Params> ')' '->' <Type> '{' <Statements> '}'
            | <Modifiers> 'fn' '(' <Params> ')'             '{' <Statements> '}'
            | <Modifiers> 'fn' '('          ')' '->' <Type> '{' <Statements> '}'
            | <Modifiers> 'fn' '('          ')'             '{' <Statements> '}'
            | <Modifiers> 'fn' '(' <Params> ')' '->' <Type> '=' <Expression>
            | <Modifiers> 'fn' '(' <Params> ')'             '=' <Expression>
            | <Modifiers> 'fn' '('          ')' '->' <Type> '=' <Expression>
            | <Modifiers> 'fn' '('          ')'             '=' <Expression>
			
<Modifiers> ::= 'local'
              | 'sync'
              | 'local' 'sync'
              | 'sync' 'local'
```

The `sync` modifier specifies that the function is not thread-safe and need to be locked when ran in a parrallel environment.

The `local` modifier specifies that the function is visible only inside its current scope.

A normal function must have a body. If it does not, an error would occure. The only expection to this are **native functions** (see [#1.10. Native Functions](#)).

Example:

```ml
fn printMe(me: String) { stdio::print("hello, world!") }
fn runMe(f: fn(String), me: String) { f(me) }

runMe(printMe, "Welcome to Mana Programming Language")
```


In mana, parameter names are very important, in fact the signature of the function is defined as the function name the number of its parameters and parameters' names, **not their order**.

Example:

```ml
fn openFile(url: String, mode: String) -> File {..}
let f: File = openFile({mode: 'w', url: './file.csv'})
```

Functions can also be generic:

```ml
fn print(t: T?[]) {
	foreach e: T in t {
		stdio::print(e)
	}
}
```


## TODO:
- Unlimited function arguments
- Native functions


## I.7. Expressions
Mana comes with a rich set of expressions, which gives you more flexibility on how to design and structure your code.

### I.7.a. `let` .. `in` ..
This expression allow you to declare a variable, initialize it and use it inside an expression. Of course it is entirely an expression.

Example:
```ml
let x = 1 + let y: u8 = 120 in y*2 + y*5

fn abs(x: s8) -> u8 = let negative = x < 0 in
	match sign {
		true: -x
		false: x
	}
```

the `let` .. `in` expression defines a variable/function that is visible only inside the scope of that expression.

### I.7.b. Lambda Expression
Lambda expressions are simply functions used as expressions. The function is defined right where it needs to be used. 

```bnf
<Lambda Expression> ::= 'fn' '(' <Params> ')' '->' <Type> '{' <Statements> '}'
                      | 'fn' '('          ')' '->' <Type> '{' <Statements> '}'
                      | 'fn' '(' <Params> ')' '->' <Type> '=' <Expression>
                      | 'fn' '('          ')' '->' <Type> '=' <Expression>
                      | 'fn' '(' <Params> ')'             '=' <Expression>
                      | 'fn' '('          ')'             '=' <Expression>
```

Example:

```ml
let str = ['hello', 'worlderful', 'world']
let len = map(str, fn(x: String) = x.length())
```

### I.7.c. Match Expression
`match` can be used both as expression or statement. Pattern matching elements must be of the same type, in other words, you cannot match a variable for a value and then match it for a parent type.

Syntax:
```bnf
<Match Expr> ::= 'match' <Expr> '{' <Match Cases> '}'
<Match Cases> ::= <Expr> ':'<Expr> <Match Cases>
                | <Expr> ':' <Expr>
                | 'else' ':' <Expr>
```

Example

```ml
fn fib(x: u64) -> u64 = match x {
	0: 1
	1: 1
	else: fib(n-1) + fib(n-2)
}
```

### II.7.d.

## I.8. Data Types
Tuples are a set of data types grouped together into a single unit.

```ml

```

## I.10. Classes

### I.10.a. Generic Class

A generic class is a definition of a class bound to one or many types that are specified later on. The main advantage is that it reduces code by being more generic.

```ml

```

## I.11.Interfaces

## I.12. Algebraic Data Types

## I.13. Annotations
Annotations are compile time options. They add metadata about classes 

```ml
/*
 * UTF-8 String
 */
 
@Immutable
class String {
	local data: byte[]
	
	fn String(){}
	fn String(String copy){}
}



@Synchronized
fn get

```


## II. Mana Standard Library
### II.1. String
### II.2. Integer
### II.3. Float
### II.4. Integer
### II.5. Containers
### II.6. Concurrency
### II.7. File System
### II.8. System


## III. Mana Programming Patterns

## IV. Mana Native Interface
