- [Go back](README.md)

# Numeric Bases
> Stephen Hamilton  
> 3-16-2023

There are many different bases of numbers.
We are used to base 10, decimal numbers.
A single base 10 digit can go from 0 - 9.
That's 10 values total, because we include the 0.

Computers use base 2, binary.
A single binary digit is either 0 or 1.
That's 2 values total.

There is also base 16, hexadecimal.
A single hexadecimal (hex) digit is 0 - F.
0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F.
Note that the digits A - F are not case sensitive.
That's 16 values total.

A less commonly used base is base 8, octal.
A single octal digit is 0 - 7.
That's 8 values total.

The number of values a digit can be is known as the **radix**.
So for example, the radix of a decimal (base 10) number is 10.
The number of possible values for a single digit is `radix - 1`

## Splitting Up Numbers
Think back to elementary school.
We can split a number up using powers of 10.
For example, the number 1,234 is equivalent to
`1*1,000 + 2*100 + 3*10 + 4*1`

We can also write this as
`1*10^3 + 2*10^2 + 3*10^1 + 4*10^0`

We can also do this with other bases.
For example, 1,234 in binary is
`0100 1101 0010`
Splitting this number up, we get:
`0*2^11 + 1*2^10 + 0*2^9 + 0*2^8 + 1*2^7 + 1*2^6 + 0*2^5 + 1*2^4 + 0*2^3 + 0*2^2 + 1*2^1 + 0*2^0`

When you punch that whole equation into a calculator,
you get the number in base 10: 1,234.
So converting a number to base 10 is simply splitting it up like this,
using the radix as the number to raise the power of.

Here's a bunch of numbers in different bases:
```
1111 1111 (base 2)
100 110 (base 3)
3333 (base 4)
2010 (base 5)
37 (base 8)
FF (base 16)
```
If you do the math to convert all of these to base 10,
you'll get 255 every time,
as they are all the same number in different bases.

## Converting Binary to Decimal
Professor McPherson has a simple way to convert to decimal:
1. Repeatedly divide the number by 2
2. Stop when you get a dividend of 0
3. Read the remainders backwards

For example, convert 73,901 to binary:
```
73,901 / 2 = 36,950, 1
36,950 / 2 = 18,475, 0
18,475 / 2 = 9,273, 1
9,273 / 2 = 4,618, 1
4,618 / 2 = 2,309, 0
2,309 / 2 = 1,154, 1
1,154 / 2 = 577, 0
577 / 2 = 288, 1
288 / 2 = 144, 0
144 / 2 = 72, 0
72 / 2 = 36, 0
36 / 2 = 18, 0
18 / 2 = 9, 0
9 / 2 = 4, 1
4 / 2 = 2, 0
2 / 2 = 1, 0
1 / 2 = 0, 1
```
We got 0, stop dividing and read remainders backwards (bottom-to-top):
```
1 0010 0000 1010 1101
```

Theoretically, this method should work for other bases.
However, instead of dividing by 2, divide by whatever the radix is.
I haven't tested this myself, so don't quote me on it

- [Go back](README.md)