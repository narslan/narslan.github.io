---
layout: default
title:  "Scheme Cookbook with SRFI-178"
---
## {{page.title}}
A bitvector is a data structure that stores bits.  
It is powerful at using bit-level parallelism to perform operations quickly.  

### Constructing bit vectors.

`b` stands for the current state of bit .
`seed` is the left most bit.
`_` is the current index

### bitvector of a flipping sequence
```scheme
 (bitvector-unfold
   (lambda (_ b)
     (values b (not b))) 16 #f)
```

```sh
#bitvector(0 1 0 1 0 1 0 1 0 1 0 1 0 1 0 1)
```

### bitvector of particular bit set.

```scheme
(define (set-bitvector-at id)
  (bitvector-unfold (lambda (_ b)
		     (values (if (equal? _ id) (not b) b) b))
		     16
                     #f))
(define x (set-bitvector-at 3))
```

```sh
#bitvector(0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0)
```

### bitvector of a random number

```scheme
(define (generate-random-bits )
	(bitvector-unfold (lambda (_) (pseudo-random-integer 2)) 64))
(bitvector->integer ( generate-random-bits))
```
