- [Go back](README.md)

# Data Representation
> Stephen Hamilton  
> 3-16-2023

Computers use binary since its easier to check if a transistor is on or off,
and not somewhere in between three states.
There are ternary computers that exist, but they are not very common.

A **bit** is a single unit of computer memory.
It can store either a 0 or a 1.
8 bits is a **byte**,
4 bits is a **nybble**.
You'll often see written binary separated out into nybbles.
This is just for our human brains to more easily understand.
The computer just sees an infinite string of 1s and 0s.

This helps explain why we have different types of ints, like `int32_t`, `int8_t`, `uint64_t`, etc.
Each of these types holds a different amount of bits.
- `int8_t` is an 8-bit number, or 1 byte.
- `int16_t` is a 16-bit number, or 2 bytes.
- `int32_t` is a 32-bit number, or 4 bytes.
- `int64_t` is a 64-bit number, or 8 bytes.

## Unsigned and Signed Integers
You have likely seen int types like `uint8_t` and `int8_t`.
The difference between these two is `uint8_t` is **unsigned**,
 while `int8_t` is **signed**.
This means that an `int8_t` can store a negative number,
and a `uint8_t` cannot.

Unsigned data types can typically hold twice the amount of numbers.
The range of a `uint8_t` is 0 - 255,
while the range of an `int8_t` is -128 - 127.
In general, unsigned types have a range of 0 - `(2^n)-1`,
while signed types have a range of `-[2^(n-1)] - 2^(n-1)-1`,
where n is the number of bits.

The reason for this difference in range is how they are represented in binary.
Most commonly, computers use what's known as **2s Complement**
to represent negative numbers.

For example, in binary, 42 is 
```
0010 1010
```
However, -42 is
```
1101 0110
```

So how is 2s Complement done?
It's in two simple steps:
1. Flip the bits (0s become 1s, 1s become 0s)
2. Add 1

So to convert 42 to -42:
```
0010 1010
1. 1101 0101
2. 1101 0110
```

### Determining if a signed number is negative
You are given a binary number, `0001 0101`,
and you are told it is a signed number,
and that you must convert it to base 10.

Here is how you do that:
1. Check the leftmost bit.
   - If it's a 1, flip all the bits and add 1
   - If it's a 0, do nothing
2. Interpret the number to decimal.
3. If the leftmost bit was a 1, add a negative sign to the number.

So let's look at `0001 0101`:  
The leftmost bit is a `0`, so all we do is interpret the number.
`0001 0101` in decimal is `21`.

Now you are given `1110 1011`, told it is a signed number,
and that you must convert it to base 10.

Look at the leftmost bit, it is a 1!
Flip the bits:
```
0001 0100
```  
Add 1:  
```
0001 0101
```  
Interpret the number to decimal:  
```
21
```
Remember that the leftmost bit was a 1:
```
-21
```
Done!

- [Go back](README.md)
