- [Go back](README.md)

# Representing Numbers in Binary
> Rick Wang  
> 3-21-2023

- [Representing Numbers in Binary](#representing-numbers-in-binary)
  - [Signed and Magnitude](#signed-and-magnitude)
  - [1's Complement](#1s-complement)
  - [2's Complement](#2s-complement)


In the first section we will go over different data representations and why we use 2's complement in almost if not all modern systems.

Representing numbers in binary is rather straightforward, `0001` in binary is `1` in decimal, `0101` in binary is `5` in decimal. The issue is how do we represent *negative* numbers.

When designing a number representation, we want it to have the following three important properties:
1. There should only be one way to represent each digit. binary `0101` only equals to decimal `5`, etc
2. Zero plus zero must equal to 0. 
3. Negative plus its positive counterpart must equal to 0. `-15 + 15 = 0`, `4 + -4 = 0`, etc

## Signed and Magnitude
The most naive way to represent negative numbers is something called *Signed and Magnitude*, where we simply add a 1 at the most significant bit to indicate the number is negative.

Example: 
- binary `0001` = decimal `1` 
- binary `1001` = decimal `-1`
- binary `0010 0101` = decimal `37`
- binary `1010 0101` = decimal `-37`

The issue of this is when *a negative number and its positive counterpart are added together it does not equal to 0*. Fixing this would require extra hardware which is a pita.

- Binary `0001 + 1001 = 1010 != 0` whereas in decimal `1 + -1 = 0`.
- Binary `0010 0101 + 1010 0101 = 1100 1010 != 0` whereas in decimal `37 + -37 = 0`.

## 1's Complement
The not so naive way is called *1's complement*, where for negative numbers we complement each bit of the corresponding positive number, including the sign bit.

Example: 
- binary `0001` = decimal `1` 
- binary `1110` = decimal `-1`
- binary `0010 0101` = decimal `37`
- binary `1101 1010` = decimal `-37`

This fixed the previous issue so adding a negative number and its positive counterpart results in 0, however this also have another problem where *there are two ways to represent decimal 0*.

- Binary `0001 + 1110 = 1111`, decimal `1 + -1 = 0`.
- Binary `0010 0101 + 1101 1010 = 1111 1111`, decimal `37 + -37 = 0`.

In this case, decimal 0 can be represented as `0000` or `1111`, meaning we can have a "positive zero" and "negative zero". Fixing this in hardware is again, pita.

## 2's Complement
2's complement satisfies the three requirements, without the need to use extra hardware.

Example:
- binary `0001` = decimal `1` 
- binary `1111` = decimal `-1`
- binary `0010 0101` = decimal `37`
- binary `1101 1011` = decimal `-37`

Adding together:
- Binary `0001 + 1111 = 1 0000`, decimal `1 + -1 = 0`.
- Binary `0010 0101 + 1101 1011 = 1 0000 0000`, decimal `37 + -37 = 0`.

It is important to note that the `1` in the result of "adding together" is simply discarded because of integer overflow.

- [Go back](README.md)
