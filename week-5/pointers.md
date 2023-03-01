- [Go back](README.md)

# Pointers
A pointer is a variable that stores a **memory address**.
The data at the memory address is the **target** of the pointer.
To access the target, you must dereference the pointer using an asterisk `*`,
like this: `*myPointer`.

To declare a pointer, you create a variable like normal, except you add a `*`
in between the type and the name of the variable, separated by at least one space.
So, each of these declarations are valid:
```c
int* a;
int * b;
int *c;
```

You can convert normal variables to pointers by using the address-of operator: `&`.
Here is an example:
```c
int myVariable = 0;
int* myPointer = &myVariable;
```
In this case, `myPointer` points to the memory that stores `myVariable`.
So, if `myVariable` is changed, you would see the change when dereferencing `myPointer`.
Likewise, if you change the data at `myPointer`'s target, you'll see that change in
`myVariable'. 

That's a lot of words, so let's see it in code:
```c
int myVariable = 1;
int* myPointer = &myVariable;
printf("%d\t%d", myVariable, *myPointer);

myVariable = 5;
printf("%d\t%d", myVariable, *myPointer);

*myPointer = 7;
printf("%d\t%d", myVariable, *myPointer);
```
Output:
```
1        1
5        5
7        7
```

- [Go back](README.md)
