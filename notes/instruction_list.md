
# planned instructions

TOS top-of-stack
NOS next-of-stack

memmory mapped stack
program keeps track of stack pointers

## data(6/12) `00000-01011`

- `00000 NOP       do nothing`
- `00001 CHS       TOS = -TOS`
- `00010 COPY      push stack, TOS`
- `00011 POP       pop stack`
- `00100 PI        push stack, pi(3.14)`
- `00101 XCHG      exchange TOS and NOS`

## maths(4/4) `01100-01111`

- `01100 ADD       NOS = TOS + NOS, pop stack`
- `01101 SUB       NOS = TOS - NOS, pop stack`
- `01110 MUL       NOS = TOS * NOS, pop stack`
- `01111 DIV       NOS = TOS / NOS, pop stack`

## derived(11/16) `10000-11111`

- `10000 SQRT      TOS = sqrt(TOS)`
- `10001 SIN       TOS = sin(TOS)`
- `10010 COS       TOS = cos(TOS)`
- `10011 TAN       TOS = tan(TOS)`
- `10100 ASIN      TOS = asin(TOS)`
- `10101 ACOS      TOS = acos(TOS)`
- `10110 ATAN      TOS = atan(TOS)`
- `10111 LOG       TOS = log_10(TOS)`
- `11000 LN        TOS = log_e(TOS)`
- `11001 EXP       TOS = exp(TOS)`
- `11010 PWR       NOS = pow(NOS, TOS), pop stack`

# opcode chart
```
   0    1    2    3    4    5    6    7    8    9    a    b    c    d    e    f
0 NOP  CHS  COPY POP  PI   XCHG                               ADD  SUB  MUL  DIV 
1 SQRT SIN  COS  TAN  ASIN ACOS ATAN LOG  LN   EXP  PWR                          
```

