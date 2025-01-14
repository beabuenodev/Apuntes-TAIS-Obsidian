- Conjunto finito M = {m1, m2, ..., mn} de tipos de monedas, donde cada mi es un número natural.
- Existe una cantidad ilimitada de monedas de cada valor.
- Se quiere pagar una cantidad C > 0 utilizando el menor número posible de monedas.
- La alternativa dinámica se usa para sistema de monedas no canónicos.
- Podemos fijar un orden en el que vamos considerando los tipos de monedas, sin que afecte al resultado final.
![[Problema del cambio.png]]
![[monedas(i, j).png]]
- Principio de optimalidad de Bellman: para conseguir una solución óptima basta con considerar subsoluciones óptimas.
- Se cumple en un problema si una solución óptima a una instancia del problema siempre contiene soluciones óptimas a todas sus subinstancias.
### Definición recursiva
- Casos recursivos:
![[Monedas - recursión.png]]
- Casos básicos:
![[Casos básicos.png]]
- Llamada inicial: monedas(n, C)

```cpp
EntInf devolver_cambio(vector<int> const& M, int C) {
	int n = M.size();
	Matriz<EntInf> monedas(n+1, C+1, Infinito);
	monedas[0][0] = 0;
	for (int i = 1; i <= n; ++i) {
		monedas[i][0] = 0;
		for (int j = 1; j <= C; ++j)
			if (M[i-1] > j)
				monedas[i][j] = monedas[i-1][j];
			else
				monedas[i][j] = min(monedas[i-1][j], monedas[i][j - M[i-1]] + 1);
	}
	return monedas[n][C];
}
```
![[Tablas monedas.png]]

#### Reconstrucción de la solución óptima
![[reconstrucción moendas.png]]
- Sabemos que si monedas(i, j) = min(monedas(i - 1, j), monedas(i, j - mi) + 1) es porque podemos no coger monedas de tipo i para pagar la cantidad j.
- Mientras que si monedas(i, j) != monedas(i - 1, j) debemos coger al menos una monea de tipo i para pagar j.

```cpp
	vector<int> devolver_cambio(vector<int> const& M, int C) {
	
... // rellenar la matriz monedas como antes

	vector<int> sol;
	if (monedas[n][C] != Infinito) {
		int i = n, j = C;
		while (j > 0) { // no se ha pagado todo
			if (M[i-1] <= j && monedas[i][j] != monedas[i-1][j]) {
				// tomamos una moneda de tipo i
				sol.push_back(M[i-1]); j = j - M[i-1];
			} else // no tomamos más monedas de tipo i
			--i;
		}
	}
	return sol;
}
```
 
```cpp
vector<int> devolver_cambio(vector<int> const& M, int C) {
	int n = M.size();
	vector<EntInf> monedas(C+1, Infinito);
	monedas[0] = 0;
	// calcular la matriz sobre el propio vector
	for (int i = 1; i <= n; ++i) {
		for (int j = M[i-1]; j <= C; ++j) {
			monedas[j] = min(monedas[j], monedas[j - M[i-1]] + 1);
		}
	}

	vector<int> sol;
	if (monedas[C] != Infinito) {
		int i = n, j = C;
		while (j > 0) { // no se ha pagado todo
			if (M[i-1] <= j && monedas[j] == monedas[j - M[i-1]] + 1) {
				// tomamos una moneda de tipo i
				sol.push_back(M[i-1]);
				j = j - M[i-1];
			} else // no tomamos más monedas de tipo i
				--i;
		}
	}
	return sol;
}
```