# Pointers
- https://beginnersbook.com/2014/01/c-pointers/
- https://beginnersbook.com/2014/01/c-pointer-to-pointer/
- https://beginnersbook.com/2014/01/c-function-call-by-reference-example/ (compare to the intuitive https://beginnersbook.com/2014/01/c-function-call-by-value-example/)

## Takeaways
- `*` means "Get value at address" operator (dereferencing operator) when used in front of data
- `*` is also used to mean "pointer to this type" when used in front of a type.
- `&` means "address of" operator (referencing operator) when used in front of data

## Notes
Unfortunately (in my opinion), * and & have different meanings when used in front of a type as when used in front of data.
You might think that * can only be used in front of a variale-name. See my lesson on "Arrays" for a counterexample. That's why I say "data" instead of "variable name."

## Assessment
- See "Can you guess the output of following C program?" from https://beginnersbook.com/2014/01/c-pointers/
- Guess the output of the "Example of double Pointer" from https://beginnersbook.com/2014/01/c-pointer-to-pointer/
- Explain to a rubber duck what this prints:

```C
int j = 4;
printf("%d\n", *&*&*&*&j);
````

- Write `swap` for two ints without looking.

# Structs
- https://www.cprogramming.com/tutorial/c/lesson7.html
- https://beginnersbook.com/2014/01/c-structures-examples/

## Takeaways
- They're C's version of classes.

## Notes
- Having to say `struct` in `struct struct_name variable_name` is a pain. It only exists for historical reasons. Most modern C code is 'typedef'ed so that you don't need to say it. Unfortunately you have to know it for interacting with old code, such as the POSIX standard library. Do this instead:

```C
typedef struct /* no name here */ {
  /* members go here */
} struct_name;
struct_name var_name;
````

- Something you have to memorize rote: the last two lines are the same.

```C
struct struct_name *instance_name;
(*instance_name).member_variable; // this operation is so common, it got a shortcut
instance_name->member_variable; // that's just a shortcut.
```

# Arrays
- https://www.programiz.com/c-programming/c-pointers-arrays
- https://en.wikibooks.org/wiki/C_Programming/Arrays_and_strings

## Notes
- When you declare a new array, first think if your array is static (stack-initialized fixed-size) or dynamic (heap-initialized undetermined-size). This will tell you which declaration to use:

```C
#define size 4
Type fixed_size_array[size /* the thing in here must be compile-time constant, so either a literal number or a #define */
                          ];

Type* underermined_size_array = malloc(n /* n could depend on user input */
                                         * sizeof(Type));

// both of these methods end up with a Type*
// even though the first one doesn't look like it
```

## Takeaways
- Pointer arithmetic is a thing
- An array is just a pointer to the first element in a contiguous block of memory

## Assessment
- C-strings should be completely intuitive now: https://www.learn-c.org/en/Strings
- Fun fact: in C `array[2]` works just as well as `2[array]`. Explain why using pointer arithmetic.
