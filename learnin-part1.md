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
https://www.udemy.com/course/python-3-deep-dive-part-1/learn/lecture/7065350#questions