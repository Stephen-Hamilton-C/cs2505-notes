- [Go back](README.md)

# String Length
Stephen Hamilton
3-16-2023

You can get the length of a string using the `strlen` function in the `string.h` library.
Note that this function will only work for strings that have the null terminator at the end.
All strings should have a null terminator, so this should not be an issue.
```c
char hello[] = "Hello, world!";
int helloLen = strlen(hello);
printf("Length of \"%s\": %d\n", hello, helloLen);
```
Output:
```
Length of "Hello, world!": 13
```
`Hello, world!` has 13 characters, so `strlen` returned 13.
Note that `strlen` does not take the null terminator into account.

This works the same for dynamically allocated strings:
```c
char* goodbye = calloc(64, sizeof(char));
strcpy(goodbye, "Goodbye, world!");
int goodbyeLen = strlen(goodbye);
printf("Length of \"%s\": %d\n", goodbye, goodbyeLen);
```
Output:
```
Length of "Goodbye, world!": 15
```
Even though we allocated 64 bytes of memory for `goodbye`,
`strlen` correctly reported that `Goodbye, world!` is 15 characters.

- [Go back](README.md)