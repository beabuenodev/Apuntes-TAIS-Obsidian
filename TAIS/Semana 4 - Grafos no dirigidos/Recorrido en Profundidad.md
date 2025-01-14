* El recorrido en profundidad imita la resolución de un laberinto.
* Para recorrer un grafo utilizamos un algoritmo recursivo que va visitando vértices.
* Visitar un vértice v consiste en:
	* Marcarlo como visitado
	* Hacer algo con el
	* Visitar recursivamente todos los vértices adyacentes a v aun no visitados

##### Hacer Test
- **Identifica los nodos y sus conexiones**: Representa mentalmente un grafo con sus nodos y aristas. Asegúrate de asociar prioridades a las aristas o a los nodos.
- **Inicializa una cola de prioridad vacía**: Esta cola almacenará los nodos pendientes de visitar, priorizando según un criterio (por ejemplo, peso de aristas o prioridad del nodo).
- **Marca un nodo inicial y agrégalo a la cola**.
- **Sigue estas reglas para cada iteración**:
    - Saca el nodo.
    - Si no ha sido visitado, márcalo como visitado.
    - Agrega sus vecinos no visitados a la cola.
- **Repite hasta que la cola esté vacía**.

##### Implementación caminos desde un origen
```cpp
class CaminosDFS {
private:
	std::vector<bool> visit; // visit[v] = ¿hay camino de s a v?
	std::vector<int> ant; // ant[v] = último vértice antes de llegar a v
	int s; // vértice origen
	void dfs(Grafo const& G, int v) {
		visit[v] = true;
		for (int w : G.ady(v)) {
			if (!visit[w]) {
				ant[w] = v;
				dfs(G, w);
			}
		}
	}

public:
	CaminosDFS(Grafo const& g, int s) : visit(g.V(), false),
		ant(g.V()), s(s) {
		dfs(g, s);
	}
	// ¿hay camino del origen a v?
	bool hayCamino(int v) const {
		return visit[v];
	}

	using Camino = std::deque<int>; // para representar caminos
	// devuelve un camino desde el origen a v (debe existir)
	Camino camino(int v) const {
		if (!hayCamino(v))
			throw std::domain_error("No existe camino");
		Camino cam;
		// recuperamos el camino retrocediendo
		for (int x = v; x != s; x = ant[x])
			cam.push_front(x);
		cam.push_front(s);
		return cam;
	}
}
```

##### Coste
$O(V+A)$