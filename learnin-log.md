# Learnin' Log
Notes, comments, and log for working. Hold yourself accountable and take notes on things that are interesting or confusing!

# Part 1 - Functional
## Section 1
2024-01-12
Watched the intro video and made this dang repo. This first section might not include a lot of new information but it'll be important to watch it and work through things anyway to be sure you fill any knowledge gaps. 

Remember, you don't know what you don't know!

## Section 2
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