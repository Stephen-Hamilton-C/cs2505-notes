- [Go back](README.md)

# Structs
Stephen Hamilton
3-16-2023

Structs in C are *struct*ured data.
They're a simple way to organize a bunch of data.
Arrays are indexed by a number, structs are indexed by name.
Here is how you declare a struct type:
```c
struct Book
{
    char* title;
    char* author;
    int pubYear;
};
```
Yes, the semicolon does indeed go after the closing curly brace (`}`).
C is strange with semicolons.

Remember that `char*` are typically strings.
So this is a `Book` struct type that has three fields -
a string `title`, a string `author`, and an int `pubYear`.
To make a variable that uses this type, we do this:
```c
struct Book dune;
```
Note that none of the fields have been initialized,
so currently the `dune` variable has a bunch of garbage data inside.
Let's fix that:
```c
dune.title = calloc(5, sizeof(char));
strcpy(dune.title, "Dune");
dune.author = calloc(14, sizeof(char));
strcpy(dune.author, "Frank Herbert");
dune.pubYear = 1965;
```
Now, the `dune` variable is properly initialized.

Another way we can initialize a struct is when we declare the variable.
So instead of what we did above, we can do this:
```c
struct Book dune = {
    .title = calloc(5, sizeof(char)),
    .author = calloc(14, sizeof(char)),
    .pubYear = 1965
};
strcpy(dune.title, "Dune");
strcpy(dune.author, "Frank Herbert");
```

Looking at this, you may be reminded of Java's classes.
However, the big difference between a `struct` and a Java `class`,
is that `structs` can't have methods, and every field is public.

We can access each member of the `Book` struct using dot notation:
```c
printf("Book title: %s, written by %s, published in %d", dune.title, dune.author, dune.pubYear);
```
Output:
```
Book title: Dune, written by Frank Herbert, published in 1965
```

## Passing Structs as Pointers
You can pass a struct into a function as a pointer, like so:
```c
void printName(struct Book* book)
{

};
```
You can pass structs in normally, but that will copy all the data inside the struct.
So if you want to modify the data in the struct, you must pass it as a pointer.
However, to access the fields in the struct, you must dereference it *first*.
Unfortunately, the dot operator comes before the dereference operator,
so we must use parenthesis like this:
```c
void printName(struct Book* book)
{
    printf("Book name: %s", (*book).name);
}Y | OR
0 0 | 0
0 1  | 1
1  0 | 1
1  1  | 1
Arrow syntax is equivalent to the above:
```c
void printName(struct Book* book)
{
    printf("Book name: %s", book->name);
}
```
Professor McPherson loves this concept, because `book` is a pointer,
> "and there's an arrow sticking out of it!"

## Struct Initializers
In C, its good practice to have an initializer function for your structs.
These are similar to Java's constructors.
Here's an initializer function for the `Book` struct:
```c
void initializeBook(struct Book* book, char title[], char author[], int year)
{
    // We first need to reserve memory for the strings in the Book type.
    // Remember to add 1 to the size to account for the null terminator!
    book->title = calloc(strlen(title)+1, sizeof(char));
    book->author = calloc(strlen(author)+1, sizeof(char));

    // Now we can assign the strings to the Book using strcpy.
    strcpy(book->title, title);
    strcpy(book->author, author);

    book->year = year;
}
```

## Freeing Struct Memory
Remember, when you're done with the book,
you need to free the memory used for the strings:
```c
struct Book dune;
initializeBook(&dune, "Dune", "Frank Herbert", 1965);
printf("Title: %s, Author: %s, Year: %d\n", dune.title, dune.author, dune.year);
free(dune.title);
free(dune.author);
```

- [Go back](README.md)
