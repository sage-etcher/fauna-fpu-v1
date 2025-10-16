<https://www.geeksforgeeks.org/digital-logic/multiplying-floating-point-numbers/>
but using ieee half-precision fp16

# division

follow multiply instructs, EXCEPT for step 3, with division you should subtract
and step 5 you should divide the 2 12bit buffers


# multiply

## step 0 inputs and expended output

    -21.92 * 110.1 = -2413.392

translate representation from base 10 to ieee fp16

     -21.92     1 10011 0101111010  ~=  -21.906
     110.1      0 10101 1011100001  ~=  110.062
    2413.392    0 11010 0010110110  ~= 2412.0

## step 1 decompose operads and add implicit 1

1-bit of mantisa overhead for each bit of exponent. additionally, resever 
another bit for implicit 1.

if exponent is 00000, treat as subnormal, do not add implicit 1

    -21.92
    -1  2^4 1.369140625
     1  19  378 1.0101111010

    110.1
    +1  2^6 1.7197265625
     0  21  737 1.1011100001

## step 2 convert exponent to 2's compliment

invert bit 4, increment 1

    10011 - 01111 = 00100
    10101 - 01111 = 00110

## step 3 add converted exponents

add exponents of the 2 numbers, store it in a temporary buffer

      4     00100
    + 6     00110
    -------------
     10     01010

## step 4 convert result back to origonal format

      01010 + 01111 = 11001

## step 5 multiply mantissas

raw binary addition of 2 16bit values

buffer 2x mantissa width +1 for implicit 1's place

                 1.0101111010	    -101 0111 1010
    *            1.1011100001	    -110 1110 0001
      -----------------------------------------------------------
    = 10.0101101011_0000111010      --10 0101 1010 1100 0011 1010

## step 6 normalize result

the mantissa should always be between 1-2, if their are extraneous bits in the 
extra bits section, left of the 1's bit (bit 10), increment exonent and right 
shift the buffer until no bits remain in the extra zone. alternatively, if 
bit 10 is 0 and the extra bits section is empty, (and the mantissa is not 0,) 
left shift until the 1's place is populated, decrementing the exponent on each 
shift

use the previously calculated exponent for calculation

    0 11001 10.0101101011_0000111010
    0 11010  1.0010110101_1000011101

## step 7 calculate the sign

the sign is easy to calculate, simply xor the input's together and out comes 
the result's sign ((a + b) % 2)

    1 xor 0 = 1

## step 8 compose result (and remove implicit 1)

remove the extra bits and implicit 1 bit, store the new sign, exponent, and the
bottom 10 bits of the mantissa as result.

    1 11010 0010110101  1110 1000 1011 0101

