---
layout: default
title:  "Bitvector Arithmetic - Unfold!"
---
## {{page.title}}
<code>
 (bitvector-unfold (lambda (_ b) (values b (not b))) 64 #f)
</code>

