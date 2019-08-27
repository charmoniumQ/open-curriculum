# Pointers

Learning pointers is possibly the biggest difference between C and higher-level languages. They are really important in every non-trivial program. Take time on this one, and the rest of the lessons will be easier.

## Resources
- [Beginners Book: C Pointers](https://beginnersbook.com/2014/01/c-pointers/)
- [Beginners Book: C Pointer to Pointer](https://beginnersbook.com/2014/01/c-pointer-to-pointer/). If you truly understand pointers from the first link, this link does not introduce any new information. It's useful exercise to try and understand.
- [Beginners Book: C function call-by-reference example](https://beginnersbook.com/2014/01/c-function-call-by-reference-example/) (compare to the intuitive [Beginners Book: C function call-by-value example](https://beginnersbook.com/2014/01/c-function-call-by-value-example/)). Also not really any new information, but uses old information. Call-by-reference is incredibly important. It shows up everywhere, even in other languages.

## Takeaways
- `*` means "Get value at address" operator (dereferencing operator) when used in front of data
- `*` is also used to mean "pointer to this type" when used in front of a type.
- `&` means "address of" operator (referencing operator) when used in front of data

## Notes
Unfortunately (in my opinion), * and & have different meanings when used in front of a type as when used in front of data.
You might think that * can only be used in front of a variale-name. See my lesson on "Arrays" for a counterexample. That's why I say "data" instead of "variable name."

## Assessment
- See "Can you guess the output of following C program?" from [Beginners Book: C Pointers](https://beginnersbook.com/2014/01/c-pointers/)
- Guess the output of the "Example of double Pointer" from [Beginners Book: C Pointer to Pointer](https://beginnersbook.com/2014/01/c-pointer-to-pointer/)
- Explain to a rubber duck what this prints:

```C
int j = 4;
printf("%d\n", *&*&*&*&j);
````

- Write `swap` for two ints without looking.
- This is actually a hard question. We can talk about it next time. Guess answers and then write a program that verifies your guesses.

```Python
# this is Python code

int_var = 4
foo(int_var)
# passed by value or reference?

list_var = [4]
foo(list_var)
# passed by value or reference?

class MyClass:
    pass

object_var = MyClass()
foo(object_var)
# passed by value or reference?
```

# Structs

They're C's version of classes. Yeah, it stands for 'structure' in case you are like me and didn't realize this until years later. Also `cout` is prononuced "C out."

## Resources
- [Beginners Book: C Structure Exmaples](https://beginnersbook.com/2014/01/c-structures-examples/)

## Notes
- Having to say `struct` in `struct struct_name variable_name` is a pain. It only exists for historical reasons. Most modern C code is `typedef`ed so that you don't need to say it. Unfortunately you have to know it for interacting with old code, such as the POSIX standard library. Do this instead:

```C
typedef struct /* no name here */ {
  /* members go here */
} struct_name;
struct_name var_name;
````

- Something you have to memorize: the last two lines in the following program are the same.

```C
struct struct_name *instance_name;
(*instance_name).member_variable; // this operation is so common, it got a shortcut
instance_name->member_variable; // that's just a shortcut.
```

## Takeaways
- Now you see why having pointers to structs is so common. It's because people want to pass them by reference most of the time. Hence the so-called 'arrow' operator.

# Arrays

## Resources

- [Programiz: C Pointers & Arrays](https://www.programiz.com/c-programming/c-pointers-arrays)
- [Arrays and strings](https://en.wikibooks.org/wiki/C_Programming/Arrays_and_strings)

## Notes
- When you declare a new array, first think if your array is static (stack-initialized fixed-size) or dynamic (heap-initialized undetermined-size). This will tell you which declaration to use:

```C
#define size 4
Type array[size /* the thing in here must be compile-time constant, so either a literal number or a #define */
                ];

Type* array = malloc(n /* n could depend on user input */
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

# POSIX I/O (you don't have to read this for next time, but you can)

## Primer
You give the OS a path (encoded as a string), it gives you back an int called a _file descriptor_. That function is called `open`. Everything else you want to do with the file, you identify the file by the file descriptor.

Get used to wading through "man pages" (like [`man open`](https://linux.die.net/man/3/open)). Most of the space is devoted to arcane details that are not relevant to your use case. After a while, you'll know exactly where to look to find what you need. The text-headers are actually well-structured :o

Remember how statically allocated arrays are fixed-size? Because of that, *almost every* function in POSIX IO takes an argument "how big is the array."

## Resources
- [A professor's summary of POSIX I/O functions](https://www.classes.cs.uchicago.edu/archive/2017/winter/51081-1/LabFAQ/lab2/fileio.html)

## Assessment
- [This example code](http://www.techytalk.info/linux-system-programming-open-file-read-file-and-write-file/) should make sense.
  - Note on this assessment: `argc` is the number of command-line arguments (see line 25) and `argv` is an array of command-line arguments (see lines 31 and 38).

- Write a functoin called `read_all` that allocates and returns an array containing *the whole file* not just the first N bytes (like `read`). Start by `read`ing a fixed-number of bytes into a buffer. If there is more file left, resize the buffer to be bigger (use `realloc`), and repeat. Keep going until `read` hits the end.
  - Note on this assessment: see [`realloc`](http://www.cplusplus.com/reference/cstdlib/realloc/)
