* TAD Grafos
	* crear un grafo vacío `Grafo(int V)`
	* añadir una arista, `void ponArista(int v, int w)`
	* consultar los adyacentes a un vértice, `Adys ady(int v) const`
	* consultar el numero de vértice, `int V() const`
	* consultar el numero de aristas, `int A() const`

* Se usan listas de adyacentes en la practica.
![[Representacion grafos.png]]

$\text{Máximo de aristas} = \frac{n(n-1)}{2}$

* Un árbol libre es un tipo de grafo que tiene las siguientes propiedades:
	* Es conexo
	* No tiene ciclos
	* n nodos, n - 1 aristas
