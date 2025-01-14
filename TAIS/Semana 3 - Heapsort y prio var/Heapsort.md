* Utiliza una cola de prioridad en vez de un montículo directamente.
```cpp
template <typename T>
void heapsort_abstracto(std::vector<T> & v) {
	PriorityQueue<T> colap;
	for (auto const& e : v)
		colap.push(e);
	for (int i = 0; i < v.size(); ++i) {
		v[i] = colap.top();
		colap.pop();
	}
}
```

* El coste en tiempo esta en $\circleddash(N \log N)$, y en espacio adicional en $\circleddash(N)$ 


* Podemos ahorrarnos el espacio adicional si utilizamos el mismo vector para representar el montículo auxiliar.
* Primero el vector se convierte en un monticulo.
* Después se va extrayendo sucesivamente el elemento mas prioritario para colocarlo al final del vector, en la parte ya no necesaria para almacenar el montículo, cada vez mas pequeño

##### Implementación
```cpp
template <typename T, typename Comparador = std::less<T>>
void heapsort(std::vector<T> & v, Comparador cmp = Comparador()) {
	// monticulizar
	for (int i = (v.size() - 1) / 2; i >= 0; --i)
		hundir_max(v, v.size(), i, cmp);
	// ordenar
	for (int i = v.size() - 1; i > 0; --i) {
		std::swap(v[i], v[0]);
		hundir_max(v, i, 0, cmp);
}
}

template <typename T, typename Comparador>
void hundir_max(std::vector<T> & v, int N, int j, Comparador cmp) {
	// montículo en v en posiciones de 0 a N-1
	T elem = v[j];
	int hueco = j;
	int hijo = 2*hueco + 1; // hijo izquierdo, si existe
	while (hijo < N) {
	// cambiar al hijo derecho si existe y va antes que el izquierdo
		if (hijo + 1 < N && cmp(v[hijo], v[hijo + 1]))
			++hijo;
	// flotar el hijo mayor si va antes que el elemento hundiéndose
		if (cmp(elem, v[hijo])) {
			v[hueco] = v[hijo];
			hueco = hijo; hijo = 2*hueco + 1;
		} else break;
	}
	v[hueco] = elem;
}
```
