* Son colas en las cuales se atiende según la prioridad de los elementos y no según el orden de llegada.
* Cada elemento tiene una prioridad que determina quién va a ser el primero en ser atendido.
* El primero en ser atendido puede ser el elemento con menor valor o el elemento con mayor valor según se trate de colas de **prioridad de mínimos o de máximos**

#### TAD colas prioridad
```cpp
Cola vacia
void push(T const& e)
T const& top() cosnt
void pop()
bool empty() const
int size() const
```

* Se puede usar la librería de STL `priority_queue` que la implementa de máximos
* Para que la cola sea de mínimos - `priority_queue<int, vector<int>, greater<int>> cola_min;`

#### Costes de las implementaciones de colas de prioridad

![[Costes Cola.png]]

#### Ejercicio tipo de colas de prioridad

Con un struct o TAD sin operador, se crea la cola con ese operador sobrecargado para que realice la prioridad correctamente.