- Dado un grafo no dirigido G, un árbol de recubrimiento de G es un subgrafo T tal que:
	- T es un árbol: es conexo y acíclico
	- T es de recubrimiento: alcanza todos los vértices de G

![[Arbol de Recubrimiento.png]]

- Si T es un árbol de recubrimiento de un grafo G con V vértices:
	- T contiene exactamente V - 1 aristas.
	- Al eliminar cualquier arista de T deja de ser conexo.
	- Añadir cualquier arista a T crea un ciclo

- Dado un grafo valorado no dirigido G, encontrar un árbol de recubrimiento de coste mínimo (ARM)
![[ARM.png]]
##### Aplicaciones de los ARMs
- Verificación facial en tiempo real.
- Búsqueda de redes de carreteras en imágenes de satélites o aéreas.
- Reducción del almacenamiento de datos en la secuenciación de aminoácidos de una proteína.
- Modelar la localidad de interacciones entre partículas en flujos de fluidos turbulentos.
- Algoritmos de aproximación para problemas NP-difíciles (por ejemplo, TSP, árbol de Steiner).
- Diseño de redes (comunicaciones, eléctricas, hidráulicas, informáticas, viales).

##### Dos simplificaciones
- El grafo es conexo - existe un ARM
- Los valores de las aristas son todos distintos - ARM único

##### Propiedad del corte
- Un corte de un grafo es una partición de sus vértices en dos conjuntos no vacíos.
- Una arista cruza el corte si tiene un extremo en cada conjunto.
- Dado un corte cualquiera, la arista de menor peso que lo cruza pertenece al ARM

![[Cortes.png]]

##### Algoritmo de Kruskal
- Considera las aristas en orden creciente de coste, y cada arista se selecciona si no crea ciclos.

```cpp
template <typename Valor>
class ARM_Kruskal {
private:
	std::vector<Arista<Valor>> _ARM;
	Valor coste;
public:
	
	Valor costeARM() const {
		return coste;
	}
	
	std::vector<Arista<Valor>> const& ARM() const {
		return _ARM;
	}

	ARM_Kruskal(GrafoValorado<Valor> const& g) : coste(0) {
		PriorityQueue<Arista<Valor>> pq(g.aristas());
		ConjuntosDisjuntos cjtos(g.V());
		while (!pq.empty()) {
			auto a = pq.top(); pq.pop();
			int v = a.uno(), w = a.otro(v);
			if (!cjtos.unidos(v,w)) {
				cjtos.unir(v, w);
				_ARM.push_back(a); coste += a.valor();
				if (_ARM.size() == g.V() - 1) break;
			}
		}
	}
};

```

- Calcula el ARM en un tiempo en $O(A\log A)$ y con un espacio adicional en $O(A)$

![[Coste.png]]