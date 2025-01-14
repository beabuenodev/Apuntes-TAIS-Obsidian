* `tam_i` => número de elementos del hijo izquierdo más uno
	* Se añade a la implementación de `TreeSet_AVL.h`
	* Se debe actualizar con las rotaciones
		* Vale solo con las simples, ya que las dobles son combinaciones de simples.
#### Rotación simple derecha

![[tam_i rotaciones.png]]

$$ \begin{aligned} tami'_A &= tami_A - tami_B \\ tami'_B &= tami_B \end{aligned} $$
#### Rotación simple izquierda

El contrario al anterior

$$ \begin{aligned} tami'_A &= tami_A + tami_B \\ tami'_B &= tami_B \end{aligned} $$
