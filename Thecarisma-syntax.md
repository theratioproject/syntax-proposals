## SOURCE FILE
- Source file can be empty, otherwise it must contain a valid set of UTF-8 codepoints.

- Support for UTF-8 identifiers is planned.


## COMMENTS
#### Single-line comments
- Single-line comments start with `#` and `//`
    ```python
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

## SUBJECT
- Subject consist of a subject name and value

    ```cpp
    const name = "John"
    ```

    Here `name` is the name of the subject and `"John"` the value or object.

- The `const` keyword is used for subject which value cannot change.
    ```cpp
    const name = "John"
    name = "Doe" // Invalid!
    ```

- The `var` keyword is used for subject whose values can change.
    ```js
    var number = 10
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

- An example of a function identifier. More on functions [later](#functions).

    ```swift
    func get_number() -> Int {
        return 20
    }
    ```

- An example of a type identifier. More on types [later](#types).

    ```swift
    type Person {
        name: String,
        age: Int,
    }
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
    var todo = "Create a new programming language :)" // `todo` is inferred as `String`
    ```

    ```cpp
    func add(a, b) {
        return a + b
    }

    const sum = add(1, 1) // Usage of `add` inferred as `(Int, Int) -> Int` here.
    ```

- Subjects can be explicitly type-annotated.

    ```js
    var identification: Int = 60
    ```

- Functions can also be explicitly type-annotated.

    ```swift
    func add(a: Int, b: Int) -> Int {
        return a + b
    }
    ```


## DESTRUCTURING
- Destructuring a tuple.

    ```js
    const (name, age) = ("John", 50)
    ```

- Destructuring a list.

    ```js
    const [..., last] = [1, 2, 3, 4, 5]
    ```

- Destructuring an object.

    ```js
    const {name, age} = john
    ```

## IF EXPRESSION
- Conditional branches using `if`, `else if` and `else`.

    ```swift
    if cond1 {
        print("if")
    } else if cond2 {
        print("else if")
    } else {
        print("else ")
    }
    ```

- Checking for falsy values.

    ```swift
    if !complete { 
        print("incomplete")
    }
    ```

- Checking for Noneness and binding value to a name.

    ```swift
    if const stock_code = get_stock_code("") {
        print(stock_code)
    }
    ```

## FOR LOOP
- A `for` loop iterates through an iterable and binds the value to a subject.

    ```py
    for i in 1:11 {
        print(i)
    }
    ```

- Destructuring in loop.

    ```py
    for (kind, number) in interesting_numbers {
        print(kind, number)
    }
    ```

- A `for` loop can be extended with a `where` condiition.
    ```swift
    for i in array where i%2 == 0 {
        print(i)
    }
    ```

- for loop must return a value if it an expression for subject assignment is nothing is returned the last value is returned.

    ```js
        const num = for i in 1:100 {
            if i == 59 {
                return i
            }
        }
        print(num) //59
    ```

    ```js
        const num = for i in array {
            
        }
        print(num) //array[array.length-1]
    ```

- break cannot be used in a for loop that is expected to return a value but can be used to break out of the iteration if not return value is expected.

    ```js
        const num = for i in 1:100 {
            if i == 59 {
                break //Invalid. Error
            }
        }
    ```

    ```js
        var result = 0
        for i in 1:100 {
            if i == 59 {
                break //valid
            } 
            var += i
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
    func add(a: Int, b: Int) -> Int {
        return a + b
    }
    ```

- Functions have types. For the example above, we say `add` has type `(Int, Int) -> Int`.

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
    func map(arr: [Int], f: (Int) -> Int) -> [Int] {
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
    const forwardAdd = func(numbers: ..Int) -> Int {
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
        func get_name(self) -> String {
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
    window = Window {
        title: "Hello World",
        extended: true
    }
    ```

## UNIFORM FUNCTION CALL SYNTAX (UFCS)
- UFCS is a feature that blurs the line between instance methods and regular functions.

- A regular function can be called using both the dot notation call syntax or the regular function call syntax.

    ```swift
    func get_name(p: Person) -> String {
        p.name
    }

    const person = Person::new("John", 52)

    person.get_name() // dot notation syntax
    get_name(person) // regular call syntax
    ```

- Likewise instance methods can be called using both the dot notation call syntax or the regular function call syntax.

    ```swift
    impl Person {
        func get_name(self) -> String {
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
    const arr = map:[Int]([1, 2, 3], (i) => i³)
    ```

    ```julia
    const buf = Buffer::new:[Int]()
    ```

- Sometimes the compiler can infer the type parameters of a generic type or function from its arguments so you don't have to specify it.

    ```rust
    const arr = map([1, 2, 3], (i) => i³)
    ```
    
