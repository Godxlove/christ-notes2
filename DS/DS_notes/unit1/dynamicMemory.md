Dynamic - flexible, the size of the data structure can be changed.

![[dynamicMemoryIntro.png]]

![[malloc.png]]

Return typr of malloc is void.
(malloc -> am-allok)

<br>

![[calloc.png]]
default block value is "0" (zero) - **important**

a bit of syntax difference between malloc and calloc.

---

![[malloc_vs_calloc.png]]

malloc fater than calloc cuz the former doesn't initialise blocks with zero.

---

![[free_dynamic.png]]
good practice to free the memory space

<br>

![[realloc.png]]
![[realloc_img.png]]
realloc maintains the already present value, no need to feed it more.

---

<br>

![[structure_datatype.png]]

---

### union
real life egs 
- free sized tshirt
- writing on a slate

![[union_definition.png]]

<br>

### Struct vs union

![[struct_vs_union.png]]
![[struct_vs_union2.png]]

---

![[struct_info.png]]

why you cant initialize the structure members? 
because till this point memory is not allocated, we are only defining the data type.

![[struct_info2.png]]

----

![[self_referencial_struct.png]]

![[self_referencial_struct_eg.png]]