1. Declare functions in a header file using ifndef macros to prevent multiple includes:

```c
/* example.h file */
#ifndef EXAMPLE_H
#define EXAMPLE_H

void example(void);

#endif
```

Do this for each file. In this example `another-example.c`, `third-example.c`.

2. Create implementation / definition of that function:

```c
/* example.c file */
void example(void);
{
    /* do something */
}
```

3. Compile to object file: `clang -c example.c another-example.c third-example.c`. You can also do `clang -c *.c`.

To create archive (static library): `llvm-ar r outputname.a example.c another-example.c third-example.c`

To create shared object (dynamic library): `ld.lld --shared -o outputname.so example.c another-example.c third-example.c`

Use either with your main:

Archive: `clang main.c outputname.a`

---

Shared object: `clang main.c outputname.so`

On Linux also set correct LD_LIBRARY_PATH with `export LD_LIBRARY_PATH=/path/to/outputname.so`