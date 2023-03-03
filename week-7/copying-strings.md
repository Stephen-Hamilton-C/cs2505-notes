# Copying Strings
In C, you can't assign an array to an array.
```c
char array1[] = "Hello!";
char array2[7];
array2 = array1; // Error: Assignment to expression with array type
```

However, you can assign an array to a pointer:
```c
char array1[] = "Hello!";
char* array2;
array2 = array1;
```
However, this won't copy the string to `array2`.
It will instead make the `array2` pointer point to the beginning of `array1`.
So, if we modify `array1` or `array2`, the changes will be reflected in both:
```c
array2[0] = 'd';
array2[0] = 'o';
array2[0] = 'g';
array2[0] = '\0'; // Can't forget the null terminator!

printf("array1: %s\n", array1);
printf("array2: %s\n", array2);
```
This will print out:
```
array1: dog
array2: dog
```

This isn't what we want. We want to make a *copy* of the string,
so that the changes aren't reflected in the original variable.
Luckily, the `string.h` library has us covered.
There is a built-in `strcpy` function that takes in two arguments:
first is the destination, the second is the source.
So, if we do this:
```c
char array1[] = "Hello!";
char array2[7];
strcpy(array2, array1);
printf("array1: %s\n", array1);
printf("array2: %s\n", array2);

array1[0] = 'd';
array1[1] = 'o';
array1[2] = 'g';
array1[3] = '\0';
printf("array1: %s\n", array1);
printf("array2: %s\n", array2);
```
It will output:
```
array1: Hello!
array2: Hello!
array1: dog
array2: Hello!
```
