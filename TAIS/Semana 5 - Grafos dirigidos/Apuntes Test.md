#### Componentes fuertemente conexas
- Subgrafo máxima donde existe un camino dirigido entre cualquier par de vértices en ambos sentidos.
- **Máximo numero de CFC con n vértices**
	- Si no hay arcos, cada vértice es su propia CFC. Numero de componentes: 3.
	- Si hay solo arcos que no permiten ciclos o caminos en ambas direcciones, el numero de CFC se reduce.
	- Si todos los vértices están conectados bidireccionalmente o formando ciclos, entonces hay solo 1 CFC.

##### Traspuesto
El _traspuesto_ (o _inverso_) de un grafo G=(V,A) es otro grafo GT=(V,AT) donde AT={(v,u)|(u,v)∈A}.
¿Qué complejidad tendría un algoritmo para calcular el grafo traspuesto de un grafo dirigido representado mediante _listas de adyacentes_ si el grafo tiene V vértices y A aristas?
- El coste es O(V + A)

##### Complementario
El _complementario_ de un grafo G=(V,A) es otro grafo GC=(V,AC) donde AC={(u,v)|(u,v)∉A,u≠v}.
¿Qué complejidad tendría un algoritmo para calcular el grafo complementario de un grafo dirigido representado mediante _matriz de adyacencia_ si el grafo tiene V vértices y A aristas?
- $O(V^2)$ 