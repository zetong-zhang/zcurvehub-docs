# Appendix
Here is the appendix information.

## Correspondence Between Bases and Chars

| Char | Base       | Char | Base       | Char | Base    | Char | Base    |
|:----:|:----------:|:----:|:----------:|:----:|:-------:|:----:|:-------:|
|  A   | A          |  B   | C, G, T    |  C   | C       |  D   | A, G, T |
|  E   | *null*     |  F   | *null*     |  G   | G       |  H   | A, C, T |
|  I   | A, G, C, T |  J   | *null*     |  K   | G, T    |  L   | *null*  |
|  M   | A, C       |  N   | A, G, C, T |  O   | *null*  |  P   | *null*  |
|  Q   | *null*     |  R   | A, G       |  S   | G, C    |  T   | T       |
|  U   | T          |  V   | A, G, C    |  W   | A, T    |  X   | *null*  |
|  Y   | C, T       |  Z   | A          |

Remarks:
1.  *null* means the program will just skip the character when read strings;
2.  Degenerate symbols will be handled using rule of frequency, for example:
    'M' will be regarded as 50% A + 50% C and vectorized as $[0.5, 0, 0.5, 0]$;
3.  'I' means hypoxanthine and may be paired with any type of bases;   
    'Z' means diaminopurine and can only be paired with 'A'. (Zhou Y, et al. Science, 
    2021, 372(6541): 512-516.)

## ZCurvePy Source Code

ZCurvePy is a free open source software follows the MIT license, so you can view the source code or change in my code repository: https://github.com/zetong-zhang/zcurvepy/