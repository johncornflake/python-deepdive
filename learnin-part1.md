# Learnin' Log
Notes, comments, and log for working. Hold yourself accountable and take notes on things that are interesting or confusing!

# Part 1 - Functional
## Section 1
2024-01-12
Watched the intro video and made this dang repo. This first section might not include a lot of new information but it'll be important to watch it and work through things anyway to be sure you fill any knowledge gaps. 

Remember, you don't know what you don't know!

## Section 2 - A Quick Refresher
2024-01-12
### The Python Type Hyerarchy
Overview of types, no new info that won't be covered later. Though I didn't know fractions were a thing, I thought it was all floats/decimals!

### Multi-line statements and strings
Pretty boring chapter, but it's interesting he's using leading commas. 
Are there any common conventions to have leading commas?

### Variable Names
pretty obvious stuff. can't be reserved words, starts with underscore or letter, etc.

Conventions are good for review. Starting with an underscore indicates it's "private" because things can't actually have private objects.
Dunderscore prefix `__my_var` is used to "mangle" class attributes used in inheritance chains. (more detail later)
dunderscore wrapped used for system-defined names with a special meaning. don't invent them!

For example, when you run `x < y`, python is _actually_ running `x.__lt__(y)`. Neat!

#### Other conventions
- Packages should be short, all lowercase, preferably with no underscores.
- Modules short, all lowercase, but can have underscores.
- Classes use upper camelcase. ThisClass
- Functions should be snake_case
- Variables should be snake_case
- Constands should be uppercase snake_case.
- 
**TODO: Read PEP8 style guide!** https://www.python.org/dev/peps/pep-0008

### Conditionals
Nothing I didn't already know.

### Functions
Annotations are somethign I haven't used but am aware of. Used to documentation but doesn't enforce it.
`def func(a: int, b: int)`
The idea of polymorphism where something like `*` can be used with different types.
Cleared up a bit on lambdas and what they do. I get they're basically functions, but I think I get why they're more useful now (passing a function as an arg to an iterator, or something)

### While Loop
Know all of this, but I didn't know `str.isprintable()`!
else is availabe in a `while` loops!
If it ran to the end without hitting a break statement, else will execute something. Neat!

### Break, Continue, and the Try Statement
Nothing new, but good reminder of `finally`!

### The For Loop
Best to think of them not as iterating over a list or something like that, but it's iterating over _an iterable_.
Not new, but helps align how I think about what's happening under the hood differently.
It's also a neat idea to have an else in a for loop. Typically I would write an if statement after, but often the else would be simpler.

I've never used `enumerate`, but it's significantly easier! Much like looping through key/value pairs in a dict.

### Classes
"magic methods"
You can override internal functionality like `str()` to return something
`__repr__` will change how the object is represented, so when you run `print(class_obj_name)` it will return that method's representation and not something like `<__main__.Rectangle object at 0x10158cee0>`
using `__eq__` will override how python measures equality of two objects, so two classes with the same instantiation can be more easily equated.
`isinstance`!
implementing `__lt__` or `__gt__` will technically both be implemented. If < is not found, it just flips it and it results in >.
getter and setter
These are conventions to get an attribute and set an attribute. This is to make attributes implicitly private, and add rules around how they can be defined. For example, in a rectangle the width can't be <= 0, so you can raise an error when this happens.
Many folks who come from something like java will implement them right out of the gate in order to prevent future cases where you want to restrict it to not break other people's code that have relied on that functionality.
In Python unless you have an explicit reason to do so, don't bother. You can use a property decorator
```
    def __init__(self):
     self._width = width
    
    @property
    def width(self):
        return self._width

    @width.setter
    def width(self, width)
        self._width = width
```
These are cool!

## Section 3 - Variables and Memory
### Variables are Memory References
Already something I was aware of, but a nice reminder.

### Reference Counting
Cool to see this. More things I knew, but I never have to think about it and it's neat to be reminded of.

### Garbage Collection
Circular references (two slots in memory point to one another). That's a memory leak! How can that even happen?
You can interact with the garbage collector using the `gc` module. 
You're allowed to turn it off, but the only reason you would is for performance, and you have to be absolutely sure you don't have memory leaks.

### Dynamic vs Static Typing
Nothing new - just declaring variable types vs not having to do that.

### Variable Reassignment
When you change the value of a variable, it creates a new value at a different memory address and references that instead.

### Object Mutability
An object whose internal state _can_ be changed is mutable. If it cannot, it's immutable.

immutable examples:
- Numbers
- strings
- tuples
- frozen sets
- user defined classes can be defined as immutable
Mutable
- lists
- sets
- dictionaries
- user-defined classes can be defined as mutable

A tuple is mutable, but the elements it contains may _not_ be immutable.
For example:
```
a = [1,2]
b = [1,2]
t = (a,b)
"""t is ([1,2], [1,2])""
a.append(3)
"""t is now ([1,2,3], [1,2])"""
```
Something to consider is that the method you use to change something will either update it's internal state or create a new reference.
a.append(3) is not the same as a = a + [3]

### Function Arguments and Mutability
Pretty much all stuff I know - a function is able to modify a mutable variable that's passed to it.

### Shared References and Mutability
Again all things I was aware of.

### Variable Equality
`is` is assessing if two vars have the same _memory address_.

### Everything is an Object 
I think at some point I knew this, but thinking of operators and built in types as objects is interesting.
In general I don't think of things like functions as objects even though they are. I haven't encountered a stuation where I need to think of a func as an object to pass to something else, but thinking of some simple lamba functions being passed into iterators it makes sense.

### Python Optimizations: Interning
Interning is reusing objects on demand

Emmet’s continuing to be a bit of a nut, but he’s doing better every day. He’s still very immature and incredibly prone to distraction. Been playing really increasingly intense games of tug which help fulfill him more and he’s improving at fetch but tends to prefer posession games.

### Python Optimization: String Interning
if something _looks_ like an identifier (short, all underscore or alphabetical) then it will be interned automatically because python by default will intern things that appear to be namespaces.
You can force things to intern with sys.intern(). You don't often need to do this, but for things like natural language processors you want words to be interned for quicker comparisons!

### Python Optimizations: Peephole
Constant expressions are stored expression results. If you have something like 24*60 all over your code, it will remember it for you.
Membership tests

## Section 4 - Numeric Types
### Integers
Integers in most languages are 32 bit, but python is variable bit. If it needs more space, python will give it to it. 
If you go beyond your architecture bit (64-bit) it will take more than one operation to do basic arithmetic with these numbers because they go beyond what can be stored.

### Integers: Operations
+,-,*,** will all return an integer, but division _always_ returns a float, even if the number is an integer. 
`//` is floor division, which is the **largest decimel <= the number you are looking at**. This is important to know for negative numbers. floor(-3.2) is -4, _not_ -3. 
floats have a limited precision, so `math.floor(-3.0000000000000001)` is actually -3, not -4. The 1 ends up getting dropped.

### Integers: Constructors and Bases
Creating an int from a float _truncates_ the number. 10.9 becomes 10, 122.999 becomes 122, etc.
The second (optional) argument is the base, so you can indicate 2, 16, whatever base you want, and python will interpret it accordingly. Note: t he int will always be displayed in base 10.
The required base is between 2 and 36. Obviously the default base is 10.
1-10 and A-Z are the allowed characters, which is why the base limit is 36 (26 letters + 10 numbers)
There are internal functions to convert reverse (base 10 to a different base).
`bin()` is used to represet numbers in base 2.
`oct()` is base 8.
`hex()` is base 16.
You can use the base prefix (`0b`, `0o`, `0x`) to have a number in a specific type. 
```
a = 0b1010 # notice this is _not_ a string!
print(int(a))
```
This results in 10.

`n = (n // b) * b + (n % b)

n is the number in base 10 and b is the base

`divmod(n, b)` will return a tuple containing the `//` and `%` operations (in that order) (if you forget, think DIV and then MOD)

### Rational Numbers
Any number with a finite number of digits before and after the decimal point is rational.
pi is not a rational number
`from fraction` is the library to use to work with fractions. Fractions will automatically be reduced (6/4 becomes 3/2). negative numbers are always done on the numerator.
You can give Fraction an irrational number and it will give an approximate fraction because all numbers, irrational or not, are still represented as floats with limited precision.
Some floats are not perfectly represented and may have odd conversions into fractions. For example, float 0.3 will not give 3/10 as expected, but a very large num/denom.
Fraction's max_denominator will approximate the denominator to the max.

### Floats - Internal Representation
In CPython (most python) floats are in IEEE double-precision binary float, or binary64.
Numbers like .1 are approximations, because in binary .1 cannot be represented (similar to .3 which is actualy .3333... to infinity) and the numbers are _approximates_.
To prove this, (0.1+0.1+0.1 == 0.3) returns False! Check with format(n, '25f') to display more

### Floats: Equality Testing
One way to compare is to use an epsilon. For example, with an epsilon of .0001: `abs(a-b) > eps`. This is fine for many numbers, but as numbers scale up it gets less reliable.
Another way is relative tolerance, which fails as numbers get closer to 0. With a tolerance of .1% (or .0001), This formula is `tolerance = rel_tol * max(a,b)`

https://peps.python.org/pep-0485/

Math has it built in! `math.isclose

### Floats: Coercing to Integers
Obviously, converting a float will result in data loss because any decimal point is not an integer. 
Pick your poison:
* Truncate: return the interger portion of the number. In other words, drop everything after the decimal point. 10.9999 -> 10, 99.00001 -> 99. `math.trunc()`
  * when giving int() a float, it does truncation. So, int(float_var) will truncate it.
* Floor: the largest integer less than or equal to the number. `math.floor()`
  * With positive numbers, this is the same as trunc, but negative goes the opposite direction. floor of 10.4 is 10, floor of -10.4 is -11.
  * Floor division is floor(a / b), which is obviously why they call it floor division.
* Ceiling is the opposite of floor. The smallest integer greater than or equal to the number. `math.ceil()` ceil(10.4) is 11, -10.4 is -10.
* Rounding, but that's a whole other topic...

### Floats: Rounding
Rounds to multiples of power of 10, so the arg can be positive _or_ negative!
Ties will cause issues. When this happens, it does a "round up," but the better way to say it is it rounds _away from zero._
But, 1.25 rounds to 1.2, and -1.25 rounds to -1.2, which is the opposite. 
This is IEEE 254 standard, "Banker's Rounding." rounds to the nearest value with ties rounded to the nearest value with an even significant digit.
They do this to get rid of bias, so with billions of transactions doing rounding, it tends to balance out because it's not always away from zero.
You can always round away from zero by adding .5 to positive integers and -.5 to negative integers.
`sign(x) * int(abs(x)+0.5)` or `int(x + 0.5 * sign(x))`

### Decimals
PEP 327 for implementation details
`import decimal`
Decimals have a context that controls certain aspects, like precision and rounding.
Precision is the number of decimal places, and rounding is the rounding algorithm it will use (remember that from floats?)
You can set a global context or a local (temporary) context.

### Decimals: Constructors and Contexts
You can use a variety of types (including tuples!) to construct a Decimal object.
Technically you can use a float, but you shouldn't (remember, 0.1 isn't precisely 0.1!)

Working with tuples. 1.23 
This is 123 * 10^-2. You need the sign, digits, and exponent. To make a decimal with a tuple, you pass (sign(0 for +, 1 for -), (digits), exponent).
You'dd make this with Decimal(0, (1,2,3), -2)

Context precision does not affect the _constructor_, only when you're actually doing math. For example, adding two decimals will result in the context's precision.

### Decimals: Math Operations
div and mod (and divmod) still satisfy **the equation** n = d * (n // d) + (n % d)
for integers, // performs _truncated_ floor division. this is fine for positive, but not for negative.
Decimal(10) // Decimal(3) = 3
Decimal(-10) // Decimal(3) = -3 instead of -4

Some `math` operations are not implemented in the Decimal class (like trig functions)
`math` functions will cast the Decimal to a float, do the calculation, then return it, so you lose the whole precision mechanism. No benefit to using the math module to do operations on Decimals, really.
But, Decimal has things like sqrt() built in to get the precise square roots.