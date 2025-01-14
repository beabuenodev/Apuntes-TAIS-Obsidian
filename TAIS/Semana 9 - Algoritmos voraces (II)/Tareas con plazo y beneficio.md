- Tenemos n tareas, cada una requiriendo una unidad de tiempo en ejecutarse, y con un plazo pi y un beneficio bi.
- Si la tarea se realiza no después de su plazo, se obtiene el beneficio.
- No todas las tareas tienen por qué realizarse. Solamente las que puedan hacerse antes de que venza el plazo.
- El objetivo es planificar las tareas de forma que se maximice el beneficio total obtenido.
![[Tareas.png]]

#### Estrategia voraz
- Un conjunto de tareas es **factible** si existe alguna **secuencia de ejecución admisible**, que permita realizar todas las tareas dentro de sus plazos.
- Una permutación (i1, i2, ..., ik) es admisible si $$
\forall j : 1 \leq j \leq k : p_{ij} \geq j
$$
- Las tareas se ordenan de mayor a menor beneficio, y cada tarea se selecciona si al añadirla al conjunto de tareas seleccionadas, este sigue siendo factible.

### Implementación
```cpp
struct Tarea {
	int plazo;
	int beneficio;
	int id;
};

bool operator>(Tarea a, Tarea b) {
	return a.beneficio > b.beneficio;
}

// las tareas están ordenadas de mayor a menor beneficio
int resolver(vector<Tarea> const& tareas, vector<int> & sol) {
	int N = tareas.size(); // número de tareas
	
	vector<int> libre(N + 1, 0);
	for (int i = 0; i <= N; ++i)
		libre[i] = i;
		
	vector<int> plan(N + 1); // 0 es que no está usado
	
	ConjuntosDisjuntos particion(N + 1);
	
	int beneficio = 0;

	// recorrer las tareas de mayor a menor beneficio
	for (int i = 0; i < N; ++i) {
		int c1 = particion.buscar(min(N, tareas[i].plazo));
		int m = libre[c1];
		if (m != 0) { // podemos colocar la tarea i
			plan[m] = tareas[i].id;
			beneficio += tareas[i].beneficio;
			int c2 = particion.buscar(m-1);
			particion.unir(c1, c2);
			libre[c1] = libre[c2];
		}
	}

	// compactamos la solución
	for (int i = 1; i <= N; ++i) {
		if (plan[i] > 0)
			sol.push_back(plan[i]);
	}
	
	return beneficio;
}
```
