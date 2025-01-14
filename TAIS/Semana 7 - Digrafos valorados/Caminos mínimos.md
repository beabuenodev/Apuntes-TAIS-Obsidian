- Encontrar el camino mínimo de s a t.
- ![[Digrafos Valorados.png]]

##### Algoritmo de Dijkstra
1. Inicializa:
    - dist[u] = infinito para todos los nodos u, excepto dist[source] = 0
    - Un conjunto vacío de nodos visitados
2. Mientras haya nodos no visitados:
    - Selecciona el nodo u no visitado con la distancia más pequeña dist[u]
    - Marca u como visitado
    - Para cada vecino v de u:
        - Si v no ha sido visitado:
            - Si dist[u] + peso(u, v) < dist[v], entonces actualiza dist[v]
3. El algoritmo termina cuando todos los nodos han sido visitados o se ha encontrado el camino más corto a todos los nodos.

- El camino mas corto desde source hasta un vértice v se construye con los vértices últimos.
- La cola de prioridad es los vértices no visitados con una prioridad basada en la distancia mínima desde el origen en ese momento
##### Costes
- Calcula caminos mínimos desde el origen al resto de vértices en un tiempo en O(A log V) y en espacio adicional en O(V)

![[TAIS/Semana 7 - Digrafos valorados/Imagenes/Costes.png]]
##### Implementación

```cpp
template <typename Valor>
using Camino = std::deque<Valor>;

template <typename Valor>
class Dijkstra {
public:
	Dijkstra(DigrafoValorado<Valor> const& g, int orig) : origen(orig),
				dist(g.V(), INF), ulti(g.V()), pq(g.V()) {
		dist[origen] = 0;
		pq.push(origen, 0);
		while (!pq.empty()) {
			int v = pq.top().elem; pq.pop();
			for (auto a : g.ady(v))
			relajar(a);
		}
	}

	bool hayCamino(int v) const { return dist[v] != INF; }
	
	Valor distancia(int v) const { return dist[v]; }
	
	Camino<Valor> camino(int v) const {
		Camino<Valor> cam;
		// recuperamos el camino retrocediendo
		AristaDirigida<Valor> a;
		for (a = ulti[v]; a.desde() != origen; a = ulti[a.desde()])
			cam.push_front(a);
		cam.push_front(a);
		return cam;
	}

private:
	const Valor INF = std::numeric_limits<Valor>::max();
	int origen;
	std::vector<Valor> dist;
	std::vector<AristaDirigida<Valor>> ulti;
	IndexPQ<Valor> pq;

	void relajar(AristaDirigida<Valor> a) {
		int v = a.desde(), w = a.hasta();
		if (dist[w] > dist[v] + a.valor()) {
			dist[w] = dist[v] + a.valor(); ulti[w] = a;
			pq.update(w, dist[w]);
		}
	}
};
```

