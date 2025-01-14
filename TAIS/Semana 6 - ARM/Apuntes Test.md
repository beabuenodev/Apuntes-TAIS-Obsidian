#### Añadir una arista - valores que harían pertenecer a esa arista si o si
- Si el peso es menor que las aristas en esos vértices será parte del ARM
- Si el peso esta entre los valores, no se puede garantizar si será parte del ARM.
- Si es mayor que las otras aristas, no se elegirá
##### Operaciones de unión
- N - 1 - operaciones de unión se pueden realizar a lo sumo que modifiquen al estructura.
##### Algoritmo de Kruskal
1. Ordenamos las aristas por costo de menor a mayor.
2. Seleccionamos la arista de menor costo que no forme un ciclo, añadiéndola al ARM.
3. Repetimos hasta que el ARM tenga V - 1 aristas.