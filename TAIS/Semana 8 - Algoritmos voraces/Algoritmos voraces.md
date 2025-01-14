- El método voraz construye una solución a través de una secuencia de pasos, hasta que se alcanza una solución completa al problema.
- En cada paso, la elección debe ser:
	- **factible**, es decir, satisfacer las restricciones del problema
	- **óptima localmente,** es decir, la mejor opción local entre todas las disponibles en ese paso
	- **irrevocable**, es decir, no se puede cambiar en los pasos posteriores del algoritmo
- Problema del cambio de monedas:
	- Pagar de forma exacta cierta cantidad, utilizando el menor número de monedas.
	- La estrategia voraz no funciona para cualquier sistema monetario. 

## Método voraz
* Para construir la solución se dispone de un **conjunto de candidatos.** Se van formando dos conjuntos: los **candidatos seleccionados** (formarán parte de la solución), y los **rechazados** definitivamente
* Existe una **función de selección** que indica cuál es el candidato más prometedor de entre los aún no considerados.
* Existe un **test de factibilidad** que comprueba si un candidato es compatible con la solución parcial construida hasta el momento.
* Existe un **test de solución** que determina si una solución parcial forma una solución "completa".
* Se tiene que obtener una **solución óptima** según una función objetivo que asocia un valor a cada solución.
![[Pasted image 20250114164129.png]]

