### Árboles binarios completos

* Un árbol binario de altura h es completo cuando todos sus nodos internos tienen dos hijos no vacíos, y todas sus hojas están en el nivel h.
![[Arbol Binario Completo.png]]
### Árboles binarios semicompletos

* Un árbol binario de altura h es semicompleto si o bien es completo o bien tiene vacantes una serie de posiciones consecutivas del nivel h empezando por la derecha.
![[Arbol binario semicompleto.png]]

### Propiedades

* Un árbol binario completo de altura $h \geq 1$ tiene $2^{i - 1}$ nodos en el nivel $i$, para todo $i$ entre 1 y h.
* Un árbol binario completo de altura $h \geq 1$ tiene $2^{h - 1}$ hojas.
* Un árbol binario completo de altura $h \geq 0$ tiene $2^{h} - 1$ nodos.
* La altura de un árbol binario semicompleto formado por n nodos es $\log n + 1$ 

### Montículos binarios

* Un montículo binario de mínimos es un árbol binario semicompleto donde el elemento en la raíz es menor (o igual) que todos los elementos en el hijo izquierdo y en el derecho, y ambos hijos son a su vez montículos de mínimos.

![[Implementacion monticulo binario.png]]

