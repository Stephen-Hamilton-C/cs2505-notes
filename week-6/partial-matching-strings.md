- [Go back](README.md)

# Partial Matching Strings
> Stephen Hamilton  
> 3-1-2023

The `string.h` library has a particularly useful function known as `strstr`.
This function can do partial matching, which was a requirement for Project 1.

Partial matching means looking for a string within a string, basically.
So, for example, if I did a partial match for `pound` in `compound`,
the match would be true.

Here is how you would check for this partial match in code:
```c
#include <string.h>

int main()
{
    char fullWord[] = "compound";
    char partial[] = "pound";
    if(strstr(fullWord, partial) != NULL)
    {
        printf("It's a partial match!\n");
    }
}
```
The reason we are checking that `strstr` is not returning `NULL` is because
if it does find a match, it returns a pointer to the `char` that the match
starts at.
Otherwise, if there was no match, it will return a `NULL` pointer.
Since we only care about if there was a match or not, simply checking
that a valid pointer was returned is enough.

- [Go back](README.md)
