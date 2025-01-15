- Hay n objetos, cada uno con un peso (entero) pi > 0 y un valor (real) vi > 0
- La mochila soporta un peso total (entero) máximo M > 0
- Y el problema consiste en maximizar
- ![[sum 1.png]]
- con la restricción
- ![[sum - 2.png]]
- donde xi indica si hemos cogido (1) o no (0) el objeto i.
- En las soluciones no importa el orden en el que los objetos son introducidos en la mochila.
- Las soluciones dependen de los objetos que tengamos disponibles para introducir en la mochila y del peso que soporte esta.
- Definimos la siguiente función:
- mochila (i, j) = máximo valor que podemos poner en una mochila de peso máximo j considerando los objetos del 1 al i.
- Se cumple el principio de optimalidad de Bellman.
- ![[mochila - 1.png]]
- ![[mochila - 2.png]]
- ![[mochila - 3.png]]
- ![[mochila -  3.png]]
```cpp
struct Object { int peso; double valor; }

double mochila_rec(vector<Objeto> const& obj, int i, int j, Matriz<double> & mochila) {
	if (mochila[i][j] != -1)
		return mochila[i][j];
	if (i == 0 || j == 0) mochila[i][j] = 0;
	else if (obj[i - 1].peso > j)
		mochila[i][j] = mochila_rec(obj, i - 1, j, mochila);
	else
		mochila[i][j] = max(mochila_rec(obj, i - 1, j, mochila), 
		mochila_rec(obj, i - 1, j - obj[i - 1].peso, mochila) + obj[i - 1].valor);

	return mochila[i][j];
}

double mochila(vector<Objeto> const& objetos, int M, vector<bool> & sol) {
	int n = objetos.size();
	Matriz<double> mochila(n + 1, M + 1, -1);
	double valor = mochila_rec(objetos, n, M, mochila);

	//cálculo de los objetos
	int i = n, j = M;
	sol = vector<bool>(n, false);
	while (i > 0 && j > 0) {
		if (mochila[i][j] != mochila[i-1][j]) {
			sol[i - 1] = true;
			j = j - objetos[i - 1].peso;
		}
		i--;
	}
	return valor;
}
```