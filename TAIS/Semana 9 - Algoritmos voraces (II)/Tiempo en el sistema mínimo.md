- Tenemos n tareas, cada una de las cuales requiere un tiempo de ejecución ti.
- Queremos minimizar el tiempo medio de estancia de una tarea en el sistema.

## Procedimiento
- Ti es el tiempo en el sistema de la tarea i, que es la suma de su tiempo de ejecución ti, más los tiempos de ejecución de las tareas que se ejecutan antes que ella.
- El problema consiste en minimizar el tiempo medio en el sistema, pero como n está fijo, esto es equivalente a minimizar el tiempo total.
- $$
T = \sum_{i=1}^{n} T_i
$$
- La planificación óptima consiste en atender a las tareas por **orden creciente de tiempo de ejecución.**