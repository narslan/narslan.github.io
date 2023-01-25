---
layout: default
title:  "Scheme Cookbook with SRFI-178"
---
## {{page.title}}
A bitvector is a data structure that stores bits.  
It is powerful at using bit-level parallelism to perform operations quickly.  
This power is exploited in areas where efficiency is most appreciated.  

### Constructing bit vectors.

`b` stands for the inital value of bit (seed, the left most bit).

```scheme
 (bitvector-unfold
   (lambda (_ b)
     (values b (not b))) 16 #f)
```

```sh
#bitvector(0 1 0 1 0 1 0 1 0 1 0 1 0 1 0 1)
```

You want to build a bit vector with a particular bit set.

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