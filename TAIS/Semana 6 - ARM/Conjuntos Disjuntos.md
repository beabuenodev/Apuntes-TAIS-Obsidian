- Representan una relación de equivalencia.
- TAD de conjuntos disjuntos:
	- crear una partición unitaria, `ConjuntosDisjuntos(int N)`
	- unir dos conjuntos, `void unir(int a, int b)`
	- buscar un elemento, `int buscar(int a) const`
	- consultar si dos elementos pertenecen al mismo conjunto, `bool unidos(int a, int b) const`
	- consultar el cardinal de un conjunto, `int cardinal(int a) const`
	- consultar el numero de conjuntos, `int num_cjtos() const`

##### Costes
![[TAIS/Semana 6 - ARM/Imagenes/Costes.png]]

##### Implementación
```cpp
class ConjuntosDisjuntos {
protected:
	int ncjtos; // número de conjuntos disjuntos
	mutable std::vector<int> p; // enlace al padre
	std::vector<int> tam; // tamaño de los árboles

public:
	// partición unitaria de N elementos
	ConjuntosDisjuntos(int N) : ncjtos(N), p(N), tam(N,1) {
		for (int i = 0; i < N; ++i)
			p[i] = i;
	}

	void unir(int a, int b) {
		int i = buscar(a);
		int j = buscar(b);
		if (i == j) return;
		if (tam[i] >= tam[j]) { // i es la raíz del árbol más grande
			tam[i] += tam[j]; p[j] = i;
		} else {
			tam[j] += tam[i]; p[i] = j;
		}
		--ncjtos;
	}

	int buscar(int a) const {
		if (p.at(a) == a) // es una raíz
			return a;
		else
			return p[a] = buscar(p[a]);
	}

	bool unidos(int a, int b) const {
		return buscar(a) == buscar(b);
	}
	
	int cardinal(int a) const {
		return tam[buscar(a)];
	}
	
	int num_cjtos() const {
		return ncjtos;
	}

};
```
