--- 
layout: default
title: "Continuations and control of flow" 
---

### Dynamic wind  

Following information has been retrieved from mzscheme manual.=> [Dynamic wind](https://www.informatik.uni-kiel.de/~scheme/doc/mzscheme/node87.htm)

> ```scheme 
(dynamic-wind pre-thunk value-thunk post-thunk) 
``` 

applies its three thunk arguments in order.


The value of a `dynamic-wind` expression is the value returned by `value-thunk`.  
The `pre-thunk` procedure is invoked before calling `value-thunk` and  
`post-thunk` is invoked after `value-thunk` returns.     

 The special properties of `dynamic-wind` are manifest when control jumps into  
 or out of the value-thunk application (either due to an exception or a  
 continuation invocation):  every time control jumps into the `value-thunk`  
 application, `pre-thunk` is invoked, and every time control jumps out of  
 `value-thunk`, `post-thunk` is invoked. (No special handling is performed for  
 jumps into or out of the pre-thunk and post-thunk applications.)  

 When `dynamic-wind` calls `pre-thunk` for normal evaluation of `value-thunk`,  
the continuation of the `pre-thunk` application calls `value-thunk` (with  
`dynamic-wind`'s special jump handling) and then `post-thunk`. Similarly, the  
continuation of the `post-thunk` application returns the value of the preceding  
`value-thunk` application to the continuation of the entire `dynamic-wind`  
application.

When pre-thunk is called due to a continuation jump, the continuation of pre-thunk

 1. calls more deeply nested pre-thunks, then
 2. jumps to the destination continuation, then
 3. continues with the context of the dynamic-wind call.

Normally, the third part of this continuation is never reached,  
due to the jump in the second part. However, the third part is   
relevant because it enables jumps to escape continuations that  
are contained in the context of the `dynamic-wind` call.   
Similarly, when `post-thunk` is called due to a continuation jump,    
the continuation of `post-thunk` calls less deeply nested post-thunks,  
them jumps to the destination continuation, then continues from the `dynamic-wind`
application.

```
(dynamic-wind
	(lambda () (display 'z))
	(lambda () (display 'e))
	(lambda () (display 'n)))
```
```sh
$> zen
```
