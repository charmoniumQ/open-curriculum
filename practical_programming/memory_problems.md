<title>Memory Problems in C</title>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.css" integrity="sha384-rHyoN1iRsVXV4nD0JutlnGaslCJuC7uwjduW9SVrLvRYooPp2bWYgmgJQIXwl/Sp" crossorigin="anonymous">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
<div class="container">

# Memory Problems in C

Estimated time: 40 minutes. Let me know if I'm wrong.

Language: C

Objective: to introduce you to the tools for debugging memory
errors. Knowing your tools makes you a 10x more productive programmer.

> As a novice performing automotive repair, I can struggle for hours
> trying to fit my rudimentary tools (hammer, duct tape, wrench,
> etc.) to the task at hand. When I fail miserably and tow my jalopy
> to a real mechanic, he invariably fishes around in a huge tool
> chest until pulling out the perfect gizmo which makes the job seem
> effortless.

_from the `nmap` manual page_

---

1. The following program crashes at line D, however removing any of
these seemingly unrelated lines, A, B, or C cause the program to
succeed. Why is this? Experiment and write down your guess.

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    char * file;
    size_t line; // A
    char * type; // B
    size_t size;
} entry_t;

int main() {
    entry_t* entry = malloc(sizeof(entry));

    entry->size = 10; // C
    entry->file = "file";
    printf("%s %d\n", entry->file, entry->size); // D

    free(entry);

    return 0;
}
```


Since this crash is undefined behavior, it is possible that on your
compiler and OS, something different happens. I tested this in GCC
with Linux, and I believe this behavior should be generalizable to
other 64-bit environments, but it might not be. Let me know if this
doesn't work. The rest of the exercise will still work.

2. Install valgrind.


    gcc -g program.c -o program.exe
    valgrind ./program.exe

If valgraind is not an option (e.g. if you have Windows), compile the program with address sanitization (ASAN):

    gcc -fsanitize=address -g program.c -o program.exe
    ./program.exe

This compiles in address bounds checking to your Now try executing
`program.exe`. Was your guess correct?

Valgrind output:

<div class="spoiler">

I ran the program with no modifications. This is what catches my eye:

    ==16725== Invalid write of size 8
    ==16725==    at 0x10916F: main (memory_problems.c:15)
    ==16725==  Address 0x4a3d058 is 16 bytes after a block of size 8 alloc'd
    ==16725==    by 0x109166: main (memory_problems.c:13)

On line C, it looks like `entry->size` points to an address that isn't
writable (hence invalid write). So `entry` does not point to a valid
`entry_t`. I don't yet know why. Take another look at its
construction, which is the other line that Valgrind flagged.

</div>

ASAN output:

<div class="spoiler">

I ran the program with line A removed. The relevant output is here:

    SUMMARY: AddressSanitizer: heap-buffer-overflow ./memory_problems.c:15 in main

This must mean that `entry` was not properly constructed. It does not point to 24 bytes (24 is the size of the struct) of empty data.

</div>

4. These tools lead us to the actual error. Was your guess correct?

<div class="spoiler">

`malloc(sizeof(entry))` should be `malloc(sizeof(entry_t))`.

</div>

5. Explain why this line of code matters.

<div class="spoiler">

In the incorrect version, C won't allocate enough memory for an `entry_t`.

`sizeof(entry)` (i.e. `sizeof(entry_t*)`) is 8 (as are all pointers),
but `sizeof(entry_t)` is 24. This means that the first field, `file`
points to 8 bytes of empty memory. This explains all of the observed
behavior:

- accessing `size` causes a crash because `size` exists at `entry +
  20` which is invalid if `entry` points to a block of 8 free bytes.

- removing either member variable A or B shifts the struct up by 4 or
  8 bytes respectively. The program for whatever reason has some empty
  data after `entry`, so `entry->file` (`entry + 12` or `entry + 16`)
  accesses that memory. This is not valid because we are writing
  someone elses memory, but it does not crash.

This is a silly typo. In C, it never makes sense to write `Type*
object = malloc(sizeof(object));` In an ideal programming language,
the programmer would not have to repeat the type that they are
mallocing.

</div>

6. Can this same kind of bug happen in C++ (with `new`)?

<div class="spoiler">

No.

We would write 

    entry_t* entry = new ____;

The blank has to be filled in with a type-name, not a variable
name. Furthermore, `new T` evaluates to a `T*` so it can only be
assigned to variables of type `T*`. The problem is that the return
type of `malloc` is `void*` which allows for no typechecking at
all.

That's one reason some poeple prefer C++ to C.

</div>

# Further reading

Note that Valgrind's memcheck is the canonical tool for checking
memory, whereas ASAN is more recently made, and its design has some
inherent limitations. Valgrind actually runs your program in a virtual
machine where every memory access is logged. ASAN inserts
runtime-checks, which is less powerful.

- [Common Valgrind use-cases](https://stackoverflow.com/a/44989219/1078199)
- [Common Valgrind use-cases (different author)](https://linoxide.com/tools/valgrind-memcheck/)
- [Common ASAN use-cases](https://en.wikipedia.org/wiki/AddressSanitizer#Examples)

<style type="text/css">
.spoiler:not(:hover) > * {
    opacity: 0;
}
.spoiler > * {
    transition: opacity .5s ease-in;
}
.spoiler {
    background-color: tan;
}
</style>

</div>
