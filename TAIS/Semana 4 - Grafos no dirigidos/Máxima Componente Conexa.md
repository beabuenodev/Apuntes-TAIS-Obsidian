- Recorremos todas las componentes recordando cual es el tamaño mayor.
- Num vertices = num aristas + 1
- Num vertices = num aristas + k - bosque con k arboles

##### Implementación
```cpp
class MaximaCompConexa {
public:
	MaximaCompConexa(Grafo const& g) : visit(g.V(), false), maxim(0) {
		for (int v = 0; v < g.V(); ++v) {
			if (!visit[v]) { // se recorre una nueva componente conexa
				int tam = dfs(g, v);
				maxim = max(maxim, tam);
			}
		}
	}
	// tamaño máximo de una componente conexa
	int maximo() const {
		return maxim;
	}
private:
	vector<bool> visit;
	int maxim; // tamaño de la componente mayor
	
	int dfs(Grafo const& g, int v) {
		visit[v] = true;
		int tam = 1;
		for (int w : g.ady(v)) {
			if (!visit[w])
				tam += dfs(g, w);
		}
		return tam;
	}
};

void resuelveCaso() { // O(N + M)
	int N, M;
	cin >> N >> M;
	Grafo amigos(N);
	int v,w;
	for (int i = 0; i < M; ++i) {
		cin >> v >> w;
	amigos.ponArista(v-1, w-1);
	}
	MaximaCompConexa mcc(amigos);
	cout << mcc.maximo() << '\n';
}
```