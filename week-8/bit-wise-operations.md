- [Go back](README.md)

# Bit Wise Operations

> Rick Wang  
> 3-21-2023

- [Bit Wise Operations](#bit-wise-operations)
  - [Bitwise operators](#bitwise-operators)
  - [Bit Masks](#bit-masks)
    - [Manipulating bit values](#manipulating-bit-values)
    - [Obtaining bit values](#obtaining-bit-values)
  - [Printing Bits One by One](#printing-bits-one-by-one)

## Bitwise operators
see the other notes about bit wise operations.

- `m & n` = m logic_and n
- `m | n` = m logic_or n
- `m~` = m not
- `m << 1` = have m right shift 1 bit, pad the least significant bit(s) with 0s.
- `m >> 1` = have m left shift 1 bit, pad the most significant bit(s) with 0s.

There is also a slightly more complex shift operation called circular shift, where instead of padding with 0s we "rotate" the bits from the other end of the target integer.

## Bit Masks
A "bit mask" is a way for us to manipulate or obtain one or more bits in a byte.

For example, suppose we have a 8-bit value representing 8 separate bits of data, and we need to perform the following operations without affecting any of the other irrelevant bits:

### Manipulating bit values
```
"Force both bit 4 and bit 5 to 1"
bit value:  1010 1100
bit mask:   0011 0000   Perform bitwise OR
                        The mask is initially all 0s, with 1s in the bit 
                        position(s) to be forced to 1
--------------------------------------------------------------------------------
result      1011 1100   bit 4 and 5 are changed to 1

"Force both bit 2 and bit 3 to 0"
bit value:  0111 1001
bit mask:   1111 0011   Perform bitwise AND
                        The mask is initially all 1s, with 0s in the bit 
                        position(s) to be forced to 0.
--------------------------------------------------------------------------------
result      0111 0001   Bit 2 and 3 are changed to 0

"Bonus: flip bit 0 and bit 1 to its opposite value (toggling)"
bit value:  1011 0010
bit mask:   0000 0011   Perform bitwise XOR
                        The mask is initially all 0s, with 1s in the bit 
                        position(s) to be toggled
--------------------------------------------------------------------------------
result      1011 0001   Bit 0 and 1 are toggled
```

### Obtaining bit values
```
"Obtain the value of bit 0"
bit value:  1011 0011
bit mask:   0000 0001   Perform bitwise AND
                        The mask is initially all 0s, with 1s in the bit
                        position(s) to be obtained
----------------------------------------------------
result      0000 0001   isolate the value of bit 0

"Obtain the value of bit 7"
bit value:  0100 1010
bit mask:   1000 0000   Perform bitwise AND
                        The mask is initially all 0s, with 1s in the bit
                        position(s) to be obtained
----------------------------------------------------
result      0000 0000   Isolate the value of bit 7
```

## Printing Bits One by One
There are two major ways to prints bits one by one. Here we will go through the way where we shift the value bits one by one.

Approach: Obtain the most significant (left-most) bit, print that bit value out, shift the entire variable to the left by 1 bit, repeat.

Pseudo code:
1. loop, until we have gone through every bit in the given integer
   - use a mask to obtain the value in the most significant bit (left-most bit)
   - print out the value obtained from the previous step
   - shift the integer to the left by 1 bit

```c
int8_t num = 10;    // 0000 1010
for (size_t i = 0; i < sizeof(int8_t) * 8; i++) {
    bool leftMostBit = num & 0x80; // 0x80 = 1000 0000 (binary)
    printf("%d", leftMostBit);
    num = num << 1;
    if(i == 3) printf(" ");
}
```

Prof McPherson's method is slightly different from what we have above, instead of shifting the variable `num`, he shifts the mask towards the right bit by bit to check whether the bit at that position is either 0 or 1.

Pseudo code:
1. loop until we have gone through every bit in the given integer
    - use a mask to obtain the bit value at position "bitPos"
      - if the bit value at that position is 0, print '0'
      - print '1' otherwise
    - shift the mask to the right by 1 bit

```c
uint8_t num = 27;       // 0001 1011
uint8_t mask = 0x80;    // 1000 0000
for (int bitPos = 8; bitPos > 0; bitPos--) {
   printf("%c", (num & mask) == 0 ? '0' : '1');
   if(bitPos == 5) printf(" ");
   mask = mask >> 1; // Move 1 to next bit down
}
```

- [Go back](README.md)