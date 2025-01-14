##### Pregunta 1

![[Control-1.png]]

Tras eliminar el valor 25 el nodo con valor 26 pierde la condición de equilibrio, y hace falta una **rotación simple a la izquierda** para restablecerla.

Eso hace que la raíz también se desequilibre, y haga falta una **rotación simple a la derecha** para equilibrar el árbol.

##### Pregunta 2
![[Control-2.png]]

1.  Falso. El valor 20 está a la izquierda del 10
2.  Falso. El árbol no está equilibrado
3.  Falso. El valor 2 está a la izquierda del 1
4.  Cierto. Es un árbol de búsqueda correcto y está equilibrado.
#####  Pregunta 3
![[Control-3.png]]

En inorden se recorre primero el hijo izquierdo en inorden, después la raíz y luego el hijo derecho en inorden, por lo que, como está equilibrado el árbol AVL, se lee de menor a mayor.

##### Pregunta 4
![[Control-4.png]]

Si se inserta un valor n < 13, el nuevo nodo se coloca como hijo de 6 y hay que rotar. Si se añade un valor 13 < n < 17, el nuevo nodo se ubica como hijo derecho de 13 y no hace falta rotar. Tampoco se necesita rotación si n > 17.

**La respuesta correcta es: si y solo si n < 13** 

##### Pregunta 5
![[Control-5.png]]

Al eliminar el valor 16 es sustituido por el valor 21, lo que provoca que el node con valor 25 pierda equilibrio, y haga falta una **rotación simple a la izquierda**. Esto hace que el árbol pase a estar equilibrado.

**La respuesta correcta: Rotación simple a la izquierda.**

##### Pregunta 6
![[Control-6.png]]
El nodo con el valor 25 es el nodo a (el primero que no cumple la condición de equilibro si vamos desde el nuevo nodo insertado hasta la raíz), y para equilibrarlo hace falta una **rotación doble izquierda derecha**

**La respuesta correcta es: Rotación doble izquierda-derecha.**

##### Pregunta 7
![[Control-7.png]]

Para buscar el máximo hay que bajar por el árbol siempre hacia la derecha hasta que no se pueda más. En el caso peor habría que bajar la altura del árbol, y como el árbol es equilibrado, esta es proporcional al logaritmo del número de nodos.

##### Pregunta 8
![[Control-8.png]]

T debe ser árbol AVL y su altura solo puede ser 1 o 2 para no desequilibrar al nodo 14. Las condiciones del árbol AVL se cumplen en el resto de nodos, así que el árbol completo sí que puede ser AVL.

##### Pregunta 9
![[Control-9.png]]

Comos los valores a insertar son menor que 18, se colocarán como descendientes del nodo x. En función del orden relativo de x, 6 y 12 se dan tres situaciones posibles:
1. Si 6<x<12, cada valor acaba a un lado de _x_ y no se produce ninguna rotación.
2. 1. Si _x_ es menor que 6, se necesita una rotación simple a izquierda para reequilibrar el nodo _x_.
3. 1. Si _x_ es mayor que 12, se necesita una rotación doble izquierda-derecha para reequilibrar el nodo _x_.
En conclusión, se tiene que dar la primera de las situaciones para evitar una rotación y entonces el menor valor posible de _x_ es 7.

##### Pregunta 10
![[Control-10.png]]
Como resultado de la eliminación del nodo G, el nodo D queda desequilibrado y es necesario hacer una rotación doble izquierda-derecha para recolocar el árbol.

La respuesta correcta es: **Rotación doble izquierda-derecha**