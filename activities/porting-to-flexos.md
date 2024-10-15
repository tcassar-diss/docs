# Porting an application to FlexOS

## Creating Gates
- FlexOS provides a tool to automatically insert gates. e.g.
```c
main() {
    printf("hello, world\n");
}
```

will be replaced with

```c
main() {
    flexos_gate(libc, printf, "hello, world\n");
}
```

There is useful advice about making sure that all gates are present in the flexos README.
Porting
