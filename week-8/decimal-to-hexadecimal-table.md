- [Go back](README.md)

# Decimal to Hexadecimal Table
> Stephen Hamilton  
> 3-16-2023

There's an easy way to figure out what a binary number is in decimal,
without having to do all of this conversion math.

A single hexadecimal digit is equal to 4 binary digits.
So let's see this table:
```
BIN  = HEX
0000 = 0
0001 = 1
0010 = 2
0011 = 3
0100 = 4
0101 = 5
0110 = 6
0111 = 7
1000 = 8
1001 = 9
1010 = A
1011 = B
1100 = C
1101 = D
1110 = E
1111 = F
```
To create the table, you start with the rightmost bit and alternate 0 and 1.
Then you go to the left and alternate 0 and 1 every two rows.
Then you go to the left and alternate 0 and 1 every four rows.
Then you do that one more time every eight rows.
Since there are 16 hexadecimal digits, you do 16 rows.
Also make sure you start with 0.

- [Go back](README.md)
