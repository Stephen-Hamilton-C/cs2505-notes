- [Go back](README.md)

# Extending Variable Lifetime with Static
> Stephen Hamilton  
> 3-1-2023

Let's do a quick refresher on what variable lifetime is.
If you're already familiar with lifetime, you can skip to the
[Static](#static) section.

## Lifetime
Variable lifetime is how long a variable stays in memory.
For variables in stack memory, the default lifetime is the scope of the variable.
For example:
```c
void myFunction(int param)
{
    if(param == 7)
    {
        int y = param * 7;
    } // y goes out of scope and its memory is freed
} // param goes out of scope and its memory is freed
```
`param` and `y` are in stack memory, since they were not allocated with `malloc`.
This is good for most cases.
However, there may be some instances where you want a variable to last longer.
This is where `static` comes in.

## Static
`static` can go out of scope, but won't be freed when it does.
Let's look at a simple example here of how `static` works:
```c
void myFunction()
{
    static int runCount = 0;
    runCount++;
    printf("myFunction has been run %d time(s)!\n", runCount);
} // runCount goes out of scope, but its memory is not freed
```
Here, we see that runCount goes out of scope,
so it cannot be used outside of the function.
However, its memory is retained, despite being on the stack.
So, when the function runs again, it still "remembers" the value
it was when the function was last run.

This also means that when a static variable is initialized as we see above,
the initialization only happens once.

So, on the first run of `myFunction`, `runCount` hasn't been created yet,
so memory is allocated on the stack for `runCount` and it is assigned to 0.
However, on the second run, C will see that `runCount` has already been
initialized, and so it won't re-initialize the variable to 0.
So on the second run, `runCount` is 1 to start off with, and it is then
incremented to 2.

Say we call the function like this:
```c
#include <stdio.h>

int main()
{
    myFunction();
    myFunction();
    myFunction();
}
```
Here is what the output would look like:
```
myFunction has been run 1 time(s)!
myFunction has been run 2 time(s)!
myFunction has been run 3 time(s)!
```

Note that `static` variables are *not* considered to be global variables,
**which are a big no-no** and are generally bad practice.
So McPherson won't get angey if you use `static` variables :D

- [Go back](README.md)
