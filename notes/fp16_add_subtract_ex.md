<https://www.cs.colostate.edu/~cs470/s25/resources/FloatingPointExample.pdf>
but using ieee half-precision fp16

# subtract

same as add except preform 2's compliment on input 2

# add 

## step 0 inputs and expended output

    3.75 + 5.125 == 8.875

translate representation from base 10 to ieee fp16

    3.75	0 10000 1110000000
    5.125	0 10001 0100100000
    8.875	0 10010 0001110000	~= 8.88 real

## step 1 decompose operads and add implicit 1

1-bit of mantisa overhead for each bit of exponent. additionally, resever 
another bit for implicit 1.

if exponent is 00000, treat as subnormal, do not add implicit 1

    3.75
    +1	2^1	1.875
     0	128	896	00000_1_1110000000

    5.125
    +1	2^2	1.28125
     0	129	288	00000_1_0100100000

## step 2 equalizing operand exponents

take the fp16 with the smaller exponent, for each difference in exponent shift
the buffer (mantissa + overhead) right

    0 10001 00000_0_1111000000
    0 10001 00000_1_0100100000

## step 3 convert operands from signed magnitude to 2's compliment

if sign bit is set, translate the buffer into 2s compliment (negate, add 1),
otherwise pass through unchanged

## step 4 add mantisas

raw binary addition of 2 16bit values

      00000_0_1111000000	0000 0011 1100 0000
    + 00000_1_0100100000	0000 0101 0010 0000
      ------------------
    = 00001_0_0011100000	0000 1001 1100 0000

## step 5 convert result from 2's complement to signed magnatude

if the result is negative (bit 15 is 1), set sign bit and convert from 2's 
compliemnt to signed magnitude (sub 1, negate).

the result is not negative

## step 6 normalize result

the mantissa should always be between 1-2, if their are extraneous bits in the 
extra bits section, left of the 1's bit (bit 10), increment exonent and right 
shift the buffer until no bits remain in the extra zone. alternatively, if 
bit 10 is 0 and the extra bits section is empty, (and the mantissa is not 0,) 
left shift until the 1's place is populated, decrementing the exponent on each 
shift

    0 10001 00001_0_0011100000 >> 1
    0 10010 00000_1_0001110000

## step 7 compose result (and remove implicit 1)

remove the extra bits and implicit 1 bit, store the new sign, exponent, and the
bottom 10 bits of the mantissa as result.

    0 10010 0001110000	0100 1000 0111 0000

