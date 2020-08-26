Peano arithmetic example demonstrating importance of recursive call placement:

##### First Way
```scheme
(define (+ x y)
    (if (= x 0)
        y
        (+ (-1+ x) (1+ y))))
```
This proc unrolls as the following steps (given `(+ 3 4)`):
```
(+ 3 4)
(+ 2 5)
(+ 1 6)
(+ 0 7)
7
```
Meaning, it's linear

##### Second Way
```scheme
(define (+ x y)
    (if  (= x 0)
        y
        (1+ (+ (-1+ x) y))))
```
This proc unrolls as the following:
```
(+ 3 4)
(1+ (+ 2 4))
(1+ (1+ (+ 1 4)))
(1+ (1+ (1+ (+ 0 4))))
(1+ (1+ (1+ 4)))
(1+ (+1 5))
(1+ 6)
7
```

Towers of Hanoi problem
```scheme
(define (move n from to spare)
    (cond ((= n 0) "DONE")
        (else
            (move (-1+ n) from spare to)
            (print-move from to)
            (move (-1+ n) spare to from ))))
```
