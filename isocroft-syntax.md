## SOURCE FILE
- Source file can be empty, otherwise it must contain a valid set of (any 66536) UTF-8 codepoints.

- Support for UTF-8 identifiers is planned.


## COMMENTS
#### Single-line comments
- Single-line comments start with `#` and `//`
    ```php
    # Hello, World!
    ```
    ```java
    // Hello, World!
    ```

    The singline comment starts with `#` so the plain source can be executed natively using shebang `(#!)` or system command can be executed at the start of the source file.

#### Multiline comments
- Nested multiline comment is allowed.
    ```rust
    /*
     * Multiline comments can span multiple lines.
     * They begin with `/*`.
     * And they end with `*/`.
     */
    ```
## DATA TYPES
- Data types in ratio

* int > a sequence of symbols from the standard number set (e.g. 2489)
* long > two or more `int` type(s) put together as a sequence (e.g. 1267383994747489948947333344747)
* float >
* char > a single symbol from the standard chracter set ('$')
* str > two or more `char` type(s) put together ('$rw32')
* bool > true, false
* byte > |01011010, |10010011

## SUBJECT
- Subject consist of a subject name and value

    ```js
    const num = 2561 // implicit definition as 4 bytes of int type for 2561
    const int num = 2561 // explicit definition as 4 bytes of int type for 2561
    
    ```

    ```js
    const name = "John" // implicit definition as 4 bytes of char type for "John"
    const char<4> name = "John" // explicit definition as 4 bytes of char type for "John" (a tuple of characters)
    
    // a string in ratio is therefore a tuple of characters which are immutable
    const str name = "John"
    ```

    Here `name` is the name of the subject and `"John"` the value or object.

- The `const` keyword is used for subject which value cannot change.
    ```cpp
    const name = "John"
    name = "Doe" // Invalid!
    ```

- The `var` keyword is used for subject whose values can change.
    ```js
    var int number = 10
    number = 50 // value changed to 50
    ```

#### Shadowing
- A subject declared on the outer scope is shadowed by subject in inner scope.

    ```kotlin
    func outer() {
        var id = "JohnDoe"

        func inner() {
            var id = 1234568
            print(id) //1234568
        }
        inner()
        print(id) //"JohnDoe"
    }

    ```

- A constant subject cannot be overshadowed

    ```kotlin
    func outer() {
        const id = "JohnDoe"

        func inner() {
            var id = 1234568 //Invalid. fails
            ...
        }
        ...
    }

    ```

## IDENTIFIERS
- Identifiers must start with a character and can be followed by characters, digits or underscore.

- For now, characters can only be in the ASCII range. Support for certain UTF-8 characters is planned.

- An example of a subject identifier

    ```js
    const name = "John Lennon"
    ```
    
- An example of a list identifier. More on lists [later](#lists)

```js

    var char<5,4> names = ["Steve", "Kunle", "Chris", "Azeez"] // a list of strings with a length of 4 and each string a length of 5
```

- An example of a function identifier. More on functions [later](#functions).

    ```swift
    func get_number() -> int {
        return 20
    }
    
    func get_number(int num) -> int {
        return 20
    }
    ```

- An example of a type identifier. More on types [later](#types).

    ```swift
    type Person {
        name: str,
        age: int,
    }
    ```
    
## ARITHMETIC OPERATION
- Operations in ratio can either be arithmetic, bitwise, logical, relational or functional

####  functional opearator (binary)

* `~>` (pipe)

#### aritmetic operators (binary)

* `+` (add)
* `-` (subtract)
* `*` (multiply)
* `/` (divide)
* `%` (modulo)
* `+=` (rewrite add)
* `-=` (rewrite subtract)

#### arithmetic operators (unary)

* `++` (increment)
* `--` (decrement)

#### logical operators (binary)

* `&&` (and)
* `and` (and)
* `||` (or)
* `or` (or)

#### logical operators (unary)

* `!` (not)
* `not` (not)

#### relational operators (binary)

* `<`
* `>`
* `>=`
* `<=`
* `!=`
* `!==`

#### bitwise operators (binary)

* `>>`

```js

var item = 3

print(--item) // 2
print(++item) // 3

```

## ARRAYS ( Mutable / Immutable )
- Arrays in ratio will serve as an array of variables of unmixed or mixed types

>mutable arrays (lists) are defined using `var`
```js

var int<4> list = [1, 2, 3, 4]

list[0] = 0 // No error

print(list); // 0, 2, 3, 4

```

>immutable arrays (tuples) are defined using `const`

```js

const int<2> tuple = [1, 5]; # you can't add or remove from the tuple but you can change the content at all indexes

tuple[0] = 2 // No error

print(tuple); // 2, 5
```

- Array of a complex type in ratio

```js

var Person<3> persons = [ 
   {name: "Tochukwu Nkedilim", age: 27}, 
   {name: "Ikechi Micheal", age: 29}, 
   {name: "Azeez Adewale", age: 26} 
]
```

## SEMI COLONS
- Semi colons are used to separate multiple statements or expressions.

    ```swift
    const name = "John"; const age = 40;
    print(name, age);
    ```

- Semi colons are optional if statements/expressions are separated by newlines.

    ```cpp
    const name = "John"
    const age = 40
    print(name, age)
    ```

## TYPE ANNOTATION
- Types can be automatically inferred in Ratio.
    ```js
    var todo = "Create a new programming language :)" // `todo` is inferred as `str` (String)
    ```

    ```cpp
    func add(a, b) {
        return a + b
    }

    const sum = add(1, 1) // Usage of `add` inferred as `(int, int) -> int` here.
    ```

- Subjects can be explicitly type-annotated.

    ```js
    var int identification = 60
    ```

- Functions can also be explicitly type-annotated.

    ```swift
    func add(a int, b int) -> int {
        return a + b
    }
    ```

## CONCATENATION ( OVERLOADED OPERATOR - `++` )

- The concatenation symbol for ratio is `++`

```swift
func sort(arr) -> int {
   
}
```

>the pipe operator `~>` can also be used to sort the resulting list
```elixir

var int<8> numbers = [1,3,5,7] ++ [0,2,4,6] ~> sort

```

- The concatenation symbol can also be used to join for a list of characters (strings) in ratio

```elixir

print("Hello " ++ "World");

```

## DESTRUCTURING
- Destructuring a string.

```js

  const [...chars] = "Happy Birthday!"
```
- Destructuring a tuple.

    ```js
    const tuple = ["John", 50];
    const (name, age) = tuple
    ```

- Destructuring a list.

    ```js
    var list = [1, 2, 3, 4, 5];
    const [..., last] = list
    const [first, ... , last] = list
    ```

- Destructuring an object (or dictionary).

    ```js
    const john = { name: "Funke Aderonke", age: 45 };
    const { name, age } = john
    ```

## IF / UNLESS EXPRESSION
- Conditional branches using `if`, `unless`, `else if` and `else`.

>Checking conditions using `if`
    ```swift
    if cond1 {
        print("if")
    } else if cond2 {
        print("else if")
    } else {
        print("else ")
    }
    ```
    
>Checking conditions using `unless`
```r

unless cond3 {
  print("unless")
} else {
  print("else ")
}

```

>Checking for falsy values using `if`.

```swift
    if !complete { 
        print("incomplete")
    }
```
>Checking for falsy values using `unless`.
 
```swift
    unless !complete { 
        print("incomplete")
    }
```

- Checking for Noneness and binding value to a name.

    ```swift
    if const stock_code = get_stock_code("") {
        print(stock_code)
    }
    ```
    
## CASE EXPRESSION
- Conditional branching using `case`

```elixir

var num = 3
case num {
   1 ?? print("Hello, i am 1")
   2 ?? print("Hello, i am 2")
   3 ?? print("Hello, i am 3")
}

```

- Can also detect default cases using `else`

```elixir

var num = 5
case num {
   1 ?? print("Hello, i am 1")
   2 ?? print("Hello, i am 2")
   3 ?? print("Hello, i am 3")
} else {
   print("Hello, i am ${num}") // using a string literal
}
```

## FOR EXPRESSION { LOOP }
- A `for` loop iterates through an iterable and binds the value at each index or pocket of the iterable to a subject.

    ```py
    for i in 1:11 { # default step is 1
        print(i)
    }
    ```
- A `for` loop with step argument

```py
    for i in 1:11,2 { # step is now 2
        print(i)
    }
    ```
 - for loop can also break using a label
 ```js

    loop_1:
    for i in 1:50 {
        if i == 29 {
            break loop_1
        }
    }
```
- Destructuring of a tuple in a for loop.

 ```py
    const interesting_numbers = ["int", 13];
    for (kind, number) in interesting_numbers {
        print(kind, number)
    }
 ```
    
- Destructuring of a list in a for loop.

 ```py
    var interesting_numbers = ["int", 13];
    for [ kind, number ] in interesting_numbers {
        print(kind, number)
    }
 ```
    
- Destructuring of an object in loop.

```py
    var interesting_numbers = { kind: "int", number: 13 };
    for { kind, number } in interesting_numbers {
        print(kind, number)
    }
```

- A `for` loop can be extended with a `where` condiition.
    
 ```swift
    for i in array where i%2 == 0 {
        print(i)
    }
 ```
- A `for` loop must return a value if it an expression for subject assignment is nothing is returned the last value is returned.

 ```js
        const num = for i in 1:100 {
            if i == 59 {
                return i
            }
        }
        print(num) //59
 ```
    
- A `for` loop can copy out the contents of an array into another array variable
    
 ```py
        const int num = for i in array {
           pass
        }
        print(num) //array[array.length-1]
 ```
    
- A `for` loop can transform an array into another array variable

```js
    const str<> num = for letter in array {
        return "'" ++ letter ++ "'"
    }
```

- A `break` cannot be used in a `for` loop that is expected to return a value but can be used to break out of the iteration if not return value is expected.

 ```js
        const num = for i in 1:100 {
            if i == 59 {
                break //Invalid. Error
            }
        }
 ```

 ```js
        var result = 0
        for i in 1:100,1 {
            if i == 59 {
                break //valid
            } 
            var += i
        }
 ```
## WHILE EXPRESSION { LOOP }
- A `while` loop iterates by a condition until that condition is false

```js

while cond4 {
   print("cond4 is still true")
}

```

## DO WHILE EXPRESSION { LOOP }
- A `while` loop iterates by a condition until that condition is false

```js
  do {
     print("a do while loop...")
  } while cond6
```

## UNTIL EXPRESSION { LOOP }
- An `until` loop iterates by a condition until that condition is true

```cargo

var num = 5
until num === 0 {
   print("num is not yet zero"); --num
}

```

## TRY / CATCH EXPRESSION { ERROR HANDLING }
- A `try` / `catch` is used to deal with exceptional cases where code desn't work as expected

```js

try {
   var quotient = num / 2 // num is not defined
} catch err {
   print("an error occured: ${err.message}")
}

```

## EXPRESSION ORIENTED
- Almost everything in Ratio (save a few constructs like impl, trait, type and import) is an expression!

    ```js
    var is_appcypher_crazy = (fave_hobby == "CountingBirds")
    ```

    ```rust
    const name = (condition ? "John" -> "Peter" )
    ```
    

- The last expression of a function is always returned.
    ```swift
    func add(a, b) {
        a + b // The result of a + b will be returned to the caller.
    }

    hieght = add(2, 3)
    ```


- A semi-colon at the end of a block, prevents the block from returning its last value
    ```swift
    func set_name(p: Person, name: String) {
        p.name = name;
    }

    const name = set_name("John Smith") // Invalid! set_name returns no result.
    ```


## FUNCTIONS

- Declare a function

    ```swift
    func add(a int, b int) -> int {
        return a + b
    }
    ```

- Functions have types. For the example above, we say `add` has type `(int, int) -> int`.

- Functions are first-class objects in Ratio, so there is support for closures and higher-order functions.


- An example of a closure.

    ```swift
    func foo(obj) {
        return func bar() {
           print(obj)
        }
    }
    ```

- An example of a higher-order function

    ```swift
    func map(int arr, f: (int) -> int) -> [int] {
        var new_arr = []
        for (index, item) in enumerate(arr) {
            new_arr[index] = f(item)
        }
        return new_arr
    }

    const arr = map(
        [1, 2, 3],
        func _(i) {i * 2}
    )
    ```

- Function assigned to a subject

    ```swift
    const forwardAdd = func(numbers: ..int) -> int {
        var result = 0
        for number in numbers {
            result += number
        }
        return result
    }
    ```

- Lambdas are syntactic sugars for anonymous functions

    ```swift
    const arr = map([1, 2, 3], func(i) {i * 2}) // Anonymous function.
    const arr = map([1, 2, 3], (i) => i * 2) // Lambda.
    ```

## TYPES
#### Type definition

- You can type-annotate the fields
    ```rust
    type Person {
        name: String,
        age: Int
    }
    ```

- You may also leave out the field types, which implicitly makes it a generic type.

    ```rust
    type Person {
        name,
        age
    }
    ```

#### Type methods
- Types can have associated functions. We call them `type methods`.

    ```swift
    impl Person {
        func new(name, age) -> self {
            self { name, age }
        }
    }
    ```

    NB: `self` here refers to the enclosing type.

- Calling a type method.

    ```rust
    const john = Person::new("John", 40)
    ```

#### Instance methods
- Instances of a type can have associated functions. We call them `instance methods`.

    ```swift
    impl Person {
        func get_name(self) -> str {
            self.name
        }
    }
    ```

    NB: `self` here refers to the type instance.

- Calling an instance method.

    ```rust
    john.get_name()

    get_name(john)
    ```


#### Instantiation
- You can instantiate types.
    ```rust
    type Person {
        name: String,
        age: Int
    }
    ```

    ```rust
    const person = Person::new("John", 45)
    ```

    ```
    var Window window = {
        title: "Hello World",
        extended: true
    }
    ```

## UNIFORM FUNCTION CALL SYNTAX (UFCS)
- UFCS is a feature that blurs the line between instance methods and regular functions.

- A regular function can be called using both the dot notation call syntax or the regular function call syntax.

    ```swift
    func get_name(p: Person) -> str {
        p.name
    }

    const person = Person::new("John", 52)

    person.get_name() // dot notation syntax
    get_name(person) // regular call syntax
    ```

- Likewise instance methods can be called using both the dot notation call syntax or the regular function call syntax.

    ```swift
    impl Person {
        func get_name(self) -> str {
            self.name
        }
    }

    const person = Person::new("John", 52)

    person.get_name() // dot notation syntax
    get_name(person) //  regular call syntax
    ```

#### Why UFCS is useful

Sometimes it makes sense to have certain functions be instance methods because they associate closely to a particular type. Other times it makes sense for such functions to be regular top-level functions because they don't associate with any single type. With UFCS, you don't have to memorize which one is a function or which one is an instance method, because you can call them using the both dot notation call and regular call syntaxes.


- Take `map` function for example. It is a generic function and does not associate with any single type.

    ```swift
    func map[T, U](iter: T, fn: (U) -> U) -> T {
        var new = T::new()
        for (i, x) in enumerate(iter) {
            new[i] = fn(x)
        }
        new
    }
    ```

    Because we have UFCS support, we can chain up calls to regular function using the dot notation syntax, which can be easier to read sometimes.

    ```swift
    map(filter(map(arr, (x) => x * 2), (x) => x > 2), (x) => x * 2)
    ```

    ```swift
    arr
        .map((x) => x * 2)
        .filter((x) => x > 2)
        .map((x) => x * 2)
    ```



## TRAITS
- Ratio does not support inheritance. Instead it choses composition-based type extension.

    ```rust
    trait Callable {
        call: (...Int) -> Int
    }
    ```

    ```swift
    impl Sum extends Callable {
        func call(args: ...Int) -> Int {
            var result = 0
            for i in args {
                result += i
            }
            result
        }
    }
    ```

## UNSAFE BLOCK
- The unsafe block is necessary for scoping the usage of unsafe/unstable features like pointer arithmetic and destructive casting.

    ```rust
    const base_ptr = some_ref as *Int

    const base_ptr = unsafe {
        base_ptr.add(20)
    }
    ```


## CASTING
- Non-destructive casting uses `as` keyword and it is only supported for scalar types.

    ```rust
    const val = 1000 as f32
    ```

## ACCESS MODIFIERS
- Everything is private by default, but you can make member of a module or type public using the `public` keyword.

    ```swift
    public type Person {
        pub name,
        age
    }
    ```

    ```swift
    public func new(name, age) -> self {
        self {
            name, age
        }
    }
    ```


## IMPORT
- Ratio is a module-based language. To use things from other module, you have to import from it.

    ```py
    import module

    module.foo()
    ```

    ```py
    import path.to.some.module {foo}
    import module {foo as bar}

    foo()
    bar()
    ```

- Ratio does not allow cyclic imports/dependencies.

## GENERICS
- Declaring a generic type

    ```rust
    type Buffer:[T] {
        buffer: *T,
        capacity,
        len
    }
    ```

- Declaring a generic function

    ```swift
    impl Buffer:[T] where T < Integer {
        func new[T]() -> self {
            self {
                buffer: allocator:[T](10),
                capacity: 10,
                len: 0,
            }
        }
    }
    ```

- Calling a generic function or type.

    ```julia
    const arr = map:[int]([1, 2, 3], (i) => i³)
    ```

    ```julia
    const buf = Buffer::new:[int]()
    ```

- Sometimes the compiler can infer the type parameters of a generic type or function from its arguments so you don't have to specify it.

    ```rust
    const arr = map([1, 2, 3], (i) => i³)
    ```
    
