---
layout: default
title:  "Scheme Cookbook with SRFI-178"
---
From [Exceptions](https://practical-scheme.net/gauche/man/gauche-refe/Exceptions.html)
> Exception is the situation, and condition is a runtime object that describes it.



```scheme
(call-with-current-continuation
 (lambda (k)
  (with-exception-handler (lambda (x) (k '(hello)))
                          (lambda () (car '()))))
                          ))
 ```

 ```scheme
 (handle-exceptions exn
		   (begin
		     (display "Went wrong")
		     (newline))
 (car '()))
 ```