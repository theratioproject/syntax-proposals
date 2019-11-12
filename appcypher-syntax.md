## SOURCE FILE
- Source file can be empty, otherwise it must contain a valid set of UTF-8 codepoints.

- Support for UTF-8 identifiers is planned.


## COMMENTS
#### Single-line comments
- Single-line comments start with `//`
    ```js
    // Hello, World!
    ```

#### Multiline comments
- Nested multiline comment is allowed.
    ```
    /*
     * Multiline comments can span multiple lines.
     * They begin with `/*`.
     * And they end with `*/`.
     */
    ```

## SUBJECTS
- Subject, in this context, refers to the identifier a value/object is bound to. We say a value/object is bound to a subject.

    ```
    let name = "Okechukwu"
    ```

    Here `name` is the subject and `"Okechukwu"` the value or object, so we say the value `"Okechukwu"` is bound to the subject `name`.

- The `let` keyword is used for subject whose values cannot change.
    ```js
    let immutable = 10
    immutable = 50 // Invalid!
    ```

- The `var` keyword is used for subject whose values can change.
    ```js
    var mutable = 10
    mutable = 50 // Subject value changed to 50
    ```

- Late binding is not supported because it makes static analysis harder and there is no real benefit to it.
    ```js
    var mutable // Invalid!
    ```

#### Shadowing
- A subject can be rebound to a different type within the same scope.
    ```js
    let phone = "08074789222" // `phone` has type `String` here
    let phone = 08074789222 // `phone` now has type `Int`
    ```

## IDENTIFIERS
- Identifiers must start with a character and can be followed by characters, digits or underscore.

- For now, characters can only be in the ASCII range. Support for certain UTF-8 characters is planned.

- Specifially, characters in the following Unicode categories `Lu`, `Ll`, `Lt`, `Lm`, `Lo`, `Nl`, `Mn`, `Mc`, `Nd`, `Pc`, `_`

- An example of a subject identifier
    ```js
    let book_title = "Ender's Game"
    ```

- An example of a function identifier. More on functions [later](#functions).
    ```swift
    func get_foo() -> String {
        return "foo"
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
    let name = "John"; let age = 40;
    print(name, age);
    ```

- Semi colons are optional if statements/expressions are separated by newlines.

    ```swift
    let name = "John"
    let age = 40
    print(name, age)
    ```

## TYPE ANNOTATION
- Types can be automatically inferred in Ratio.
    ```js
    var todo = "Create a new programming language :)" // `todo` is inferred as `String`
    ```

    ```swift
    func add(a, b) {
        return a + b
    }

    let sum = add(1, 1) // Usage of `add` inferred as `(Int, Int) -> Int` here.
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

- Ratio has support for [union types](https://en.wikipedia.org/wiki/Union_type). It allows a subject to assume multiple types.

    This is useful for having heterogenous and sophisticated type inference implementation.

    ```swift
    let identification: String|Int = "120232435" // `identification` has type `String` here
    identification = 120232435 // `identification` now has type `Int` here
    ```

    ```swift
    func print_id(id: String|Int) {
        print(id)
    }

    print(identification)
    ```


## NUMERIC LITERALS
- Ratio has 13 scalar types

    #### Signed Integers
    - Int - Pointer-sized signed integer
    - I8 - 8-bit signed integer
    - I16 - 16-bit signed integer
    - I32 - 32-bit signed integer
    - I64 - 64-bit signed integer
    - Int - Pointer-sized integer

    #### Unsigned Integers
    - UInt - Pointer-sized unsigned integer
    - U8 - 8-bit unsigned integer
    - U16 - 16-bit unsigned integer
    - U32 - 32-bit unsigned integer
    - U64 - 64-bit unsigned integer

    #### Floating point numbers
    - F32 - 32-bit IEEE 754-2019 floating point representation
    - F64 - 64-bit IEEE 754-2019 floating point representation

- Some examples of numeric literals.

    ```js
    var index = 5 // UInt literal
    var axis = -3 // Int literal
    let meters = 0.25e-5 // F64 literal
    ```

- Hex, binary and octal literals are supported as well.

    ```js
    var price = 0x6FFF00p+12 // Hex literal
    var op_code = 0b10110001 // Binary literal
    var interest = 0o56676 // Octal literal
    ```

## TUPLES
- Tuple is a special datatype with statically-known length. It allows for cool features like arguments unpacking.

    ```swift
    var fave_game = ("Uncharted 4", 2016)
    ```

    One-element tuple. Note the trailing comma.

    ```rust
    let map = (london,)
    ```

    Empty tuple.

    ```swift
    let empty_tuple = ()
    ```

- Tuple indexing. Tuple index space starts at index 0.

    ```rust
    let book = ("Harry Potter", "J.K. Rowling", 1995)
    let title = book.1 // Harry Potter
    let author = book.2 // J.K. Rowling
    let year = book.3 // 1995
    ```

- Tuple destructuring.

    ```rust
    let person = ("Sam", 50)
    let (name, age) = person
    ```

- Tuple unpacking.

    ```swift
    func add(a, b) {
        a + b
    }

    let arguments = (5, 6)
    add(...arguments)
    ```

- Tuples have limitations because they are expected to be amenable to static analysis.

    ```swift
    var tup1 = (1, 2)
    var tup2 = (5, 6)
    ```

    Directly or indirectly, a tuple can't be used to extend itself.

    ```go
    for i in range(x) {
        tup2 = (...tup2, ...tup1) // Invalid!
    }

    for i in range(x) {
        tup3 = (...tup2, 1)
        tup2 = (tup3, tup1) // Invalid!
    }
    ```

- The type of a tuple.

    Since tuples can't change in size, a tuple has a fixed type. For example the tuple `(0xFF, "Hi")` has type `(Int, String)`. `("Hello", 5.0, "Hi")` has type `(String, F64, String)`

## LISTS
- List is a dynamic container for storing and accessing items.

    ```swift
    var unordered_list = [7, 3, 8, 5, 4, 0, 9, 1, 2, 6]
    ```

    Empty list.

    ```swift
    var empty_list = []
    ```

    Using List constructor.

    ```swift
    let students = List::new()
    ```

- Type annotation for lists.

    ```swift
    var names: [String] = []
    ```

- Ratio lists can have heterogenous elements.

    ```swift
    var stuffs = [500, "Steve", 1.0] // Inferred
    var stuffs: [F64|String|Int] = [500, "Steve", 1.0] // Explicit typing
    ```

- List indexing. List index space starts at index 0.

    ```swift
    stuffs[0] // 500
    ```

- Slicing a list.

    ```swift
    contestants[2..7] // 3rd to the 7th index
    contestants[2..] // 3rd to the last index
    contestants[..7] // first to the 7th index
    contestants[..] // first to the last index
    ```

    A slice can have a step value.

    ```swift
    let odds = numbers[1..2..30] // The step value is the `2` in the middle.
    ```

## RANGE
- Range is an iterable that allows iterating through a range of values.

    ```swift
    let days = 1..31 // 1 to 30
    ```

- A range can have a step value.

    ```swift
    let evens = 2..2..20 // The step value is the `2` in the middle.
    ```


## STRINGS
- Strings are a sequence of valid UTF-8 codepoints and they are delimited by double quotes `"`.

    ```swift
    let language = "Ratio"
    ```

- String interpolation is done with a pair of curly braces
    ```js
    var story = "{language} was started in the {year}"
    ```

- String operations

    ```js
    var concatenate = "ab" + "c" // "abc"
    var multiply = "ab" * 2 // "abcabc"
    ```

## CHAR
- Char represents a valid single 32-bit UTF-32 codepoint and it is delimited by single quotes `'`.

    ```swift
    var pi_char = 'π'
    ```

## DESTRUCTURING
- Destructuring a tuple.

    ```js
    let (name, age) = ("John", 50)
    ```

- Destructuring a list.

    ```js
    let [..., last] = [1, 2, 3, 4, 5]
    ```

- Destructuring an object.

    ```rust
    let {name, age} = john
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
    if phone_number { // The block executes if `phone_number` is not falsy.
        call(phone_number)
    }
    ```

- Checking a value for Noneness and binding it to a subject.

    ```swift
    if let stock_code = get_stock_code("") {
        print(stock_code)
    }
    ```

## FOR LOOP
- A `for` loop iterates through an iterable and binds the value to a subject.
    ```py
    for i in 1..11 {
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
    for i in array where i == 5 {
        return i
    }
    ```

## WHILE LOOP
- A `while` loop loops until the header condition is not satisfied.

    ```rust
    while file.has_next() {
        print file.next()
    }
    ```

- Checking a value for Noneness and binding it to a subject.

    ```swift
    while let details = books[title] {
        print details
        if details.author != "J.K. Rowlings" {
            break
        }
        title = choose_title_randomly()
    }
    ```

## MATCH EXPRESSION
- Match is used for pattern matching.

    ```rust
    match obj {
        Person { name, age } => 0,
        (x, y) => 1,
        75 => 2,
        75 | 97 => 3,
        [..., last] => 4,
        _ => 5
    }
    ```

## EXPRESSION ORIENTED
- Almost everything in Ratio (save a few constructs like impl, trait, type and import) is an expression!
    ```js
    var is_appcypher_crazy = (fave_hobby == "CountingBirds")
    ```

    ```rust
    let name = if condition {
        "John"
    } else {
        "Peter"
    }
    ```

- In the case of a for loop, the last expression on the final iteration is returned, if there is no break.

    ```swift
    let cube = for i in 1..10 {
        i³
    }
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

    let name = set_name("John Smith") // Invalid! set_name returns no result.
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

    let arr = map(
        [1, 2, 3],
        func _(i) {i * 2}
    )
    ```

- Lambdas are syntactic sugars for anonymous functions

    ```swift
    let arr = map([1, 2, 3], func _(i) {i * 2}) // Anonymous function
    let arr = map([1, 2, 3], (i) => i * 2) // Lambda
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
        func new(name, age) -> Self {
            Self { name, age }
        }
    }
    ```

    NOTE: `Self` here refers to the enclosing type.

- Calling a type method.

    ```rust
    let john = Person::new("John", 40)
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

    NOTE: `self` here refers to the type instance.

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
    let person = Person::new("John", 45)
    ```

#### SINGLETONS
- A type without body is a singleton type in Ratio. It represents both the type value and the type name.

    ```rust
    type UniqueValue

    let value: UniqueValue = UniqueValue
    ```


## ENUMS

- Enums in Ratio are implemented with union types

    ```swift
    typealias Mammal = Human | Dog

    let jack: Mammal = Dog{ "Jack", 10 }
    ```

## OPERATORS

- Ratio has both unary and binary operators. An unary operator can either be prefix or postfix.

    ```julia
    let x = 2 + 4
    let y = x²
    let z = √x
    ```

- Ratio supports operator overloading.

    An example of a binary operator overloading.

    ```go
    func *(lhs: BigInt, rhs: BigInt) -> BigInt {
        lhs.value.add(rhs.value)
    }

    let res = BigInt::new(1000) * BigInt::new(100000000000000000000000000000000)
    ```

    An example of a postfix unary operator overloading.

    ```go
    func ²(b: BigInt) -> BigInt {
        b.pow(2)
    }

    let res = BigInt::new(25)²
    ```

    An example of prefix unary operator overloading.

    ```go
    func √(b: BigInt) -> BigInt {
        b.sqrt()
    }

    let res = √BigInt::new(5)
    ```

- A list of all arithmetic operators

    ```py
    +
    -
    /
    *
    %
    ^
    +=
    -=
    /=
    *=
    %=
    ^=
    >
    <
    >=
    <=
    !=
    not
    and
    or
    in
    not in
    >>
    <<
    |
    &
    ~
    ```


- Custom operators are not supported because they are [easily abused](https://blog.jooq.org/2014/02/10/why-everyone-hates-operator-overloading/).


## UNIFORM FUNCTION CALL SYNTAX
- UNIFORM FUNCTION CALL SYNTAX (UFCS) is a feature that blurs the line between instance methods and regular functions.

- A regular function can be called using both the dot notation call syntax or the regular function call syntax.

    ```swift
    func get_name(p: Person) -> String {
        p.name
    }

    let person = Person::new("John", 52)

    person.get_name() // Dot notation syntax
    get_name(person) // Regular function call syntax
    ```

- Likewise instance methods can be called using both the dot notation call syntax or the regular function call syntax.

    ```swift
    impl Person {
        func get_name(self) -> String {
            self.name
        }
    }

    let person = Person::new("John", 52)

    person.get_name() // Dot notation syntax
    get_name(person) //  Regular function call syntax
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
    impl Sum: Callable {
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
    let base_ptr = some_ref as *Int

    let base_ptr = unsafe {
        base_ptr.add(20)
    }
    ```


## CASTING
- Non-destructive casting uses `as` keyword and it is only supported for scalar types.

    ```rust
    let val = 1000 as f32
    ```

- For destructive casting, compiler-intrinsic `transmute` function can be used.

    ```rust
    let s = "String"
    let buf = unsafe { transmute:[String, Buffer](s) }
    ```

## ACCESS MODIFIERS
- Everything is private by default, but you can make member of a module or type public using the `pub` keyword.

    ```rs
    pub type Person {
        pub name,
        age
    }
    ```

    ```swift
    pub func new(name, age) -> Self {
        Self {
            name, age
        }
    }
    ```


## IMPORT
- Ratio is a module-based language. To use things from other modules, you have to import from them.

    ```py
    import .dir {foo}
    ```

- Ratio has a special file called `index.ratio`. It is used to expose modules in a particular folder. Modules of a folder can only be accessed if the folder has an `index.ratio` that exposes them.

    ```py
    import .dir
    ```

    If there is a folder called `dir`, this import can only be valid if there is a file path `./dir/index.ratio`

    If there is no folder called `dir`, then there has to be a file `./dir.ratio`


- Ratio has two kinds of imports.

    #### Regular relative import

    The imported module is relative to the source file defining the import. The import symbol is preceded by a dot.

    ```py
    import .dir
    ```

    `dir` here can either be `./dir.ratio` or `./dir/index.ratio`

    #### Root relative import

    The imported module is relative to the project's root folder or it is some external dependency.

    ```go
    import dir
    ```

    `dir` here can either be `src/dir.ratio` or `src/dir/index.ratio` or some external dependency named `dir` with a path `src/index.ratio`.

- Ratio supports aliasing an imported element '

    ```py
    import ext {foo}
    import .module.some {foo as bar}

    foo()
    bar()
    ```

- Ratio does not allow cyclic imports/dependencies.

## GENERICS
- Declaring a generic type

    ```rust
    type Buffer[T] {
        buffer: *T,
        capacity,
        len
    }
    ```

- Declaring a generic function

    ```swift
    impl Buffer[T] where T: Integer {
        func new[T]() -> Self {
            Self {
                buffer: allocator:[T](10),
                capacity: 10,
                len: 0,
            }
        }
    }
    ```

- Calling a generic function or type.

    ```julia
    let arr = map:[Int]([1, 2, 3], (i) => i³)
    ```

    ```julia
    let buf = Buffer::new:[Int]()
    ```

- Sometimes the compiler can infer the type parameters of a generic type or function from its arguments so you don't have to specify it.

    ```rust
    let arr = map([1, 2, 3], (i) => i³)
    ```

## STACK OR HEAP
- Because Ratio is a managed language, the compiler determines (using lifetime analysis) where an object is allocated at runtime. This can either be the stack or the heap. If the compiler can prove every reference to a local object does not escape the stack frame, it allocates it on stack, otherwise, it is allocated on the heap.

    ```swift
    func lifetime_test() {
        let p = "Peter"
        let j = "John"

        print(p) // `p` value allocated on stack
        return j // `j` value allocated on heap
    }
    ```

    ```js
    let escaped_ref = lifetime_test()
    ```

