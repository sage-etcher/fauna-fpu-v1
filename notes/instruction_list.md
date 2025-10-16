
# registers

- A: fp16\_t
- B: fp16\_t

# planned instructions

## misc(2/2) `00000-00001`

- `00000 NOP       do nothing`
- `00001 HLT       halt`

## data manipulation(9/10) `00010-01011`

- `00010 INA       A = databus`
- `00011 INB       B = databus`
- `00100 OUTA      databus = A`
- `00101 OUTB      databus = B`
- `00110 ATOB      B = A`
- `00111 BTOA      A = B`
- `01000 XCHG      exchange A and B`
- `01001 CHS       A = -A`
- `01010 API       A = pi`
- `01011`

## maths(4/4) `01100-01111`

- `01100 ADD       A = A + B`
- `01101 SUB       A = A - B`
- `01110 MUL       A = A * B`
- `01111 DIV       A = A / B`

## derived(11/16) `10000-11111`

- `10000 SQRT      A = sqrt(A)`
- `10001 SIN       A = sin(A)`
- `10010 COS       A = cos(A)`
- `10011 TAN       A = tan(A)`
- `10100 ASIN      A = asin(A)`
- `10101 ACOS      A = acos(A)`
- `10110 ATAN      A = atan(A)`
- `10111 LOG       A = log_10(A)`
- `11000 LN        A = log_e(A)`
- `11001 EXP       A = exp(A)`
- `11010 PWR       A = pow(A, B)`
- `11011`
- `11100`
- `11101`
- `11110`
- `11111`

# opcode chart
```
   0    1    2    3    4    5    6    7    8    9    a    b    c    d    e    f
0 NOP  HLT  INA  INB  OUTA OUTB ATOB BTOA XCHG CHS  API       ADD  SUB  MUL  DIV
1 SQRT SIN  COS  TAN  ASIN ACOS ATAN LOG  LN   EXP  PWR
```

# pins

```
- D0..D15    16bit databus
- C0..C4     5bit command bus
- SEL       execute command
- ACK       command acknowledge

- RST       reset

- CLK       clock pulse
- PWR       +5v
- GND       ground

        +-----------+
D0  <-> | 1      15 | <-> D8
D1  <-> | 2      16 | <-> D9
D2  <-> | 3      17 | <-> D10
D3  <-> | 4      18 | <-> D11
D4  <-> | 5      19 | <-> D12
D5  <-> | 6      20 | <-> D13
D6  <-> | 7      21 | <-> D14
D7  <-> | 8      22 | <-> D15
PWR --> | 9      23 | <-- C0
GND --> | 10     24 | <-- C1
CLK --> | 11     25 | <-- C2
RST --> | 12     26 | <-- C3
SEL --> | 13     27 | <-- C4
    --- | 14     28 | --> ACK
        +-----------+
```

