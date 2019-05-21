# Arithmetic 




## Fractional part

```q
q)x:0 1 -2 3.4 -5.6 -6.1
q)x mod 1
0 0 0 0.4 0.4 0.9
```


## Integer and fractional parts of positive x

```q
q)x:12.3 23.4 5.33 8.999
q){f,'x-f:floor x}x
12 0.3
23 0.4
5  0.33
8  0.999
```


## Magnitude of fractional part

```q
q)x:6.13 -6.13
q)abs[x]
6.13 6.13
q)a-floor a:abs x
0.13 0.13
```


## Fractional part with sign

```q
q)signum[x]*abs[x]mod 1
0.2 0.3 -0.2 -0.8 0 0 -0
```


## Leading digit of numeric code abbb

```q
q)ld:{floor x%1000}
q)x:1319 8629 6581 6988 790 9045
q)ld x
1 8 6 6 0 9
```


## Last part of abbb

```q
q)x:1234 5678 9012 345 6789
q)x mod 1000
234 678 12 345 789
```




## Sum a vector

```q
q)x:1 2 3 4 5
q)sum x
15
```


## Sum columns of matrix

```q
q)x:1+3 4#til 12
q)x
1 2  3  4
5 6  7  8
9 10 11 12
q)sum x
15 18 21 24
```


## Sum rows of matrix

```q
q)x:1+3 4#til 12
q)x
1 2  3  4
5 6  7  8
9 10 11 12
q)sum each x
10 26 42
```


## Sum items of x given by y

```q
q)show x:log 1+til 5
0 0.6931472 1.098612 1.386294 1.609438
q)y:1 4 1 4 1
q)show a:value group y
0 2 4
1 3
q)sum each x[a]
2.70805 2.079442
q)sum x[0 2 4]
2.70805
q)sum x[1 3]
2.079442
q)sum each x value group y
2.70805 2.079442
```


## Add x to each row of y

```q
q)x:1+til 4
q)show y:3 4#2+til 12
2  3  4  5
6  7  8  9
10 11 12 13
q)x+/:y
3  5  7  9
7  9  11 13
11 13 15 17
```


## Add x to each column of y

```q
q)x:1+til 2
q)show y:2 5#3+til 10
3 4 5  6  7
8 9 10 11 12
q)x+'y
4  5  6  7  8
10 11 12 13 14
```


## Sum reciprocal series

```q
q)x:10 9 10 7 8
q)y:80 63 70 63 64
q)sum y%x
39f
```


## Sum over subsets of x specified by y

```q
q)show x:`float$1+3 4#til 12
1 2  3  4
5 6  7  8
9 10 11 12
q)show y:`float$4 3#1 0
1 0 1
0 1 0
1 0 1
0 1 0
q)x mmu y
4  6  4
12 14 12
20 22 20
```

==FIXME: how does y specify subsets of x?==


## Sum squares of x

```q
q)x:1 2 3 4 5
q)sum x*x
55
```

==DROP: trivial==


## Alternating sum

```q
q)x:1+til 10
q)x
1 2 3 4 5 6 7 8 9 10
q)a:((count x)#1 -1)
q)b:x*a
q)sum b
-5
q)sum x*(count x)#1 -1
-5
```


## Alternating sum series

```q
q)x:1+til 10
q)x
1 2 3 4 5 6 7 8 9 10
q)a:((count x)#1 -1)
q)a
1 -1 1 -1 1 -1 1 -1 1 -1
q)b:x*a
q)b
1 -2 3 -4 5 -6 7 -8 9 -10
q)sums b
1 -1 2 -2 3 -3 4 -4 5 -5
q)as:{sums x*(count x)#1 -1}
q)as[x]
1 -1 2 -2 3 -3 4 -4 5 -5
```


## Increase absolute value without sign change

```q
q)x:0 -1 2 -3 4 -5
q)y:10
q)x+y*(x=0)+signum x
10 -11 12 -13 14 -15
q)x+y*@[signum x;where x=0;:;1]
10 -11 12 -13 14 -15
```


## First difference

```q
q)show x:sums 1 2 3 4 5
1 3 6 10 15
q)deltas x
1 2 3 4 5
```


## Pairwise difference

```q
q)x:9 3 5 2 0
q)deltas x
9 -6 2 -3 -2
q)1_ deltas x
-6 2 -3 -2
q)1_ neg deltas x
6 -2 3 2
```


## Primes to n

```q
q)n:10
q)show x:1+til n
1 2 3 4 5 6 7 8 9 10
q)x mod/:x:1+til n
0 0 0 0 0 0 0 0 0 0
1 0 1 0 1 0 1 0 1 0
1 2 0 1 2 0 1 2 0 1
1 2 3 0 1 2 3 0 1 2
1 2 3 4 0 1 2 3 4 0
1 2 3 4 5 0 1 2 3 4
1 2 3 4 5 6 0 1 2 3
1 2 3 4 5 6 7 0 1 2
1 2 3 4 5 6 7 8 0 1
1 2 3 4 5 6 7 8 9 0
q)sum 0=x mod/:x:1+til n
1 2 2 3 2 4 2 4 3 4
q)2=sum 0=x mod/:x:1+til n
0110101000b
q)0b,2=sum 0=x mod/:x:1+til n
00110101000b
q)where 0b,2=sum 0=x mod/:x:1+til n
2 3 5 7
q)pn:{[n]where 0b,2=sum 0=x mod/:x:1+til n}
q)pn 30
2 3 5 7 11 13 17 19 23 29
q)/Classic:
q)p:{x[where not (x in distinct raze x*/:\:x:2_ key x)]}
q)p 10
2 3 5 7
q)p 30
2 3 5 7 11 13 17 19 23 29
```


## First 10 figurate numbers of order x

```q
q)fg:{x+\/10#1}
q)fg 0
1 1 1 1 1 1 1 1 1 1
q)fg 1
1 2 3 4 5 6 7 8 9 10
q)fg 2
1 3 6 10 15 21 28 36 45 55
q)fg 3
1 4 10 20 35 56 84 120 165 220
q)fg 4
1 5 15 35 70 126 210 330 495 715
```


## Maximum table

```q
q)x:til 10
q)x&\:x
0 0 0 0 0 0 0 0 0 0
0 1 1 1 1 1 1 1 1 1
0 1 2 2 2 2 2 2 2 2
0 1 2 3 3 3 3 3 3 3
0 1 2 3 4 4 4 4 4 4
0 1 2 3 4 5 5 5 5 5
0 1 2 3 4 5 6 6 6 6
0 1 2 3 4 5 6 7 7 7
0 1 2 3 4 5 6 7 8 8
0 1 2 3 4 5 6 7 8 9
```


## Product

```q
q)x:1 2 3 4 5
q)prd x
120
```


## Multiplication table of order x

```q
q)mt:{{x*\:x}1+til x}
q)mt 5
1 2  3  4  5
2 4  6  8  10
3 6  9  12 15
4 8  12 16 20
5 10 15 20 25
```


## Square x retaining sign

```q
q)x:0 -1 2 -3 4
q)x*abs x
0 -1 4 -9 16
```


## Alternating product

```q
q)x:1 2 3 4 5
q)a:(count x)#1 -1
q)a
1 -1 1 -1 1
q)prd xexp[x;a]
1.875
q)xexp[x;a]
1 0.5 3 0.25 5
```


## Direct matrix product

```q
q)x:1+3 2#til 6
q)y:1+2 4#til 8
q)flip each x*\:\:y
1 2 3 4     2 4 6 8     5  6  7  8  10 12 14 16
3 6 9  12   4 8 12 16   15 18 21 24 20 24 28 32
5 10 15 20  6 12 18 24  25 30 35 40 30 36 42 48
q)dp:{flip each x*\:\:y}
```


## Matrix product

```q
q)show x:`float$(1 2 3;4 5 6)
1 2 3
4 5 6
q)show y:`float$(1 2;3 4;5 6)
1 2
3 4
5 6
q)x mmu y
22 28
49 64
```

==DROP: keyword not idiom==


## Dot product of vectors

```q
q)x:1 2 3 4 5
q)y:10 20 30 40 50
q)sum x*y
550
```



## Product over subsets of x specified by y

```q
q)show x:1+3 4#til 12
1 2  3  4
5 6  7  8
9 10 11 12
q)show y:4 3#1 0
1 0 1
0 1 0
1 0 1
0 1 0
q)x('[prd;xexp])\:y
3  8   3
35 48  35
99 120 99
```


## Divisors

```q
q)dv:{where 0=x mod/:key 1+x}
q)x:363
q)dv x
1 3 11 33 121 363
q)x:365
q)dv x
1 5 73 365
q)dv 367
1 367
q)dv each 1 2 3 4 5 6 7 8 9 10
,1
1 2
1 3
1 2 4
1 5
1 2 3 6
1 7
1 2 4 8
1 3 9
1 2 5 10
```


## Greatest common divisor

```q
q)x:6 9 12
q)1+til min x
1 2 3 4 5 6
q)x mod/:1+til min x
0 0 0
0 1 0
0 0 0
2 1 0
1 4 2
0 3 0
q)0=x mod/:1+til min x
111b
101b
111b
001b
000b
101b
q)min each 0=x mod/:1+til min x
101000b
q)where min each 0=x mod/:1+til min x
0 2
q)1+last where min each 0=x mod/:1+til min x
3
```


## Pairwise ratios

```q
q)ratios x
2 5 5 2f
q)1_ratios x
5 5 2f
```

