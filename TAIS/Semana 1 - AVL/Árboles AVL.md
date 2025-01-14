
### Árboles AVL
* Son árboles de búsqueda binaria con una condición de equilibrio: **todos los nodos del árbol cumplen que la diferencia de alturas de sus dos hijos es como mucho 1**
![[AVL_arboles.png]]
* **Altura - $O(\log n)$** siendo n el número de nodos
* **Mínimo número de nodos - $S(h) = S(h-1) + S(h-2) + 1$** con  $S(0) = 0$ y $S(1) = 1$
* Cuando se producen adiciones o eliminaciones de nodos, el árbol se debe equilibrar con **rotaciones**.
##### Rotaciones
![[Rotaciones.png]]