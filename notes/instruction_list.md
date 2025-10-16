
# planned instructions

TOS top-of-stack
NOS next-of-stack

memmory mapped stack
program keeps track of stack pointers

## maths(4)

- `01000 ADD       TOS = TOS + NOS, pop stack`
- `01001 SUB       TOS = TOS - NOS, pop stack`
- `01010 MUL       TOS = TOS * NOS, pop stack`
- `01011 DIV       TOS = TOS / NOS, pop stack`

## derived(11)

- `10000 SQRT      TOS = sqrt(TOS)`
- `10001 SIN       TOS = sin(TOS)`
- `10010 COS       TOS = cos(TOS)`
- `10011 TAN       TOS = tan(TOS)`
- `10100 ASIN      TOS = asin(TOS)`
- `10101 ACOS      TOS = acos(TOS)`
- `10110 ATAN      TOS = atan(TOS)`
- `10111 LOG       TOS = log\_10(TOS)`
- `11000 LN        TOS = log\_e(TOS)`
- `11001 EXP       TOS = exp(TOS)`
- `11010 PWR       NOS = pow(NOS, TOS), pop stack`

## data(6)

- `00000 NOP       do nothing`
- `00001 CHS       TOS = -TOS`
- `00010 COPY      push stack, TOS`
- `00011 POP       pop stack`
- `00100 PUPI      push stack, pi(3.14)`
- `00101 XCHG      exchange TOS and NOS`


