### Números combinatorios
![[Combinatorios.png]]

#### Programación dinámica
- Utilización de una tabla donde se almacenan los resultados a subproblemas ya resueltos.
- La tabla tiene tantas dimensiones como argumentos tiene la recurrencia.
- El tamaño de cada dimensión coincide con los valores que puede tomar el argumento correspondiente.
- Cada subproblema se asocia a una posición de la tabla.

![[Matriz dinámica.png]]

#### Programación dinámica descendente

- Mantiene el diseño recursivo.
- La función recibe como parámetro de entrada/salida, la tabla donde se almacenan las soluciones a subproblemas ya resueltos.
- Antes de resolver de manera recursiva un subproblema, se mira en la tabla por si ya se hubiera resuelto.
- Tras resolver un subproblema recursivo, su solución se almacena en la tabla.
- Necesidad de saber si un subproblema está resuelto o no.

```cpp
int num_combi(int i, int j, Matriz<int> & C) {
	if (j == 0 || j == i) return 1;
	else if (C[i][j] != -1) return C[i][j];
	else {
		C[i][j] = num_combi(i-1, j-1, C) + num_combi(i-1, j, C);
		return C[i][j];
	}
}
```

#### Programación dinámica ascendente
- Cambiar el orden en el que se resuelve los subproblemas.
- Comenzar por resolver todos los subproblemas más pequeños que se puedan necesitar, para ir combinándolos hasta llegar a resolver el problema original.
- Los subproblemas se van resolviendo recorriéndolos de menor a mayor tamaño.
- Todos los posibles subproblemas de tamaño menor tienen que ser resueltos antes de resolver uno de tamaño mayor.

![[Pascal - 1.png]]


```cpp
int pascal(int n, int r) {
	Matriz<int> C(n+1,r+1,0);
	C[0][0] = 1;
	for (int i = 1; i <= n; ++i) {
		C[i][0] = 1;
		for (int j = 1; j <= r; ++j)
			C[i][j] = C[i-1][j-1] + C[i-1][j];
	}
	return C[n][r];
}
```


- Reducción del espacio necesario para la tabla - actualización sobre el propio vector.
![[Pascal - 2.png]]

```cpp
int pascal2(int n, int r) {
	vector<int> C(r+1,0);
	C[0] = 1;
	for (int i = 1; i <= n; ++i)
		for (int j = r; j >= 1; --j)
			C[j] = C[j-1] + C[j];
	return C[r];
}
```