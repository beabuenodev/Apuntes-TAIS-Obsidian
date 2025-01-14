* Grafo con aristas dirigidas
* TAD de los grafos dirigidos:
	* crear un grafo vacío, `Digrafo(int V)`
	* añadir una arista, `void ponArista(int v, int w)`
	* consultar los adyacentes a un vértice, `Adys ady(int v) const`
	* consultar el numero de vértices, `int V() const`
	* consultar el numero de aristas, `int A() const`
	* calcular el grafo inverso, `Digrafo inverso() const`

- Se elige representación de lista de adyacentes
![[Representacion.png]]


##### Implementación 

```cpp
//
//  Digrafo.h
//
//  Implementación de grafos dirigidos
//
//  Facultad de Informática
//  Universidad Complutense de Madrid
//
//  Copyright (c) 2020  Alberto Verdejo
//

#ifndef DIGRAFO_H_
#define DIGRAFO_H_

#include <iostream>
#include <stdexcept>
#include <vector>

using Adys = std::vector<int>;  // lista de adyacentes a un vértice

class Digrafo {

   int _V;   // número de vértices
   int _A;   // número de aristas
   std::vector<Adys> _ady;   // vector de listas de adyacentes

public:

   /**
    * Crea un grafo dirigido con V vértices.
    */
   Digrafo(int V) : _V(V), _A(0), _ady(_V) {}

   /**
    * Crea un grafo dirigido a partir de los datos en el flujo de entrada (si puede).
    * primer es el índice del primer vértice del grafo en el entrada.
    */
   Digrafo(std::istream & flujo, int primer = 0) : _A(0) {
      flujo >> _V;
      if (!flujo) return;
      _ady.resize(_V);
      int E, v, w;
      flujo >> E;
      while (E--) {
         flujo >> v >> w;
         ponArista(v - primer, w - primer);
      }
   }

   /**
    * Devuelve el número de vértices del grafo.
    */
   int V() const { return _V; }

   /**
    * Devuelve el número de aristas del grafo.
    */
   int A() const { return _A; }

   /**
    * Añade la arista dirigida v-w al grafo.
    * @throws domain_error si algún vértice no existe
    */
   void ponArista(int v, int w) {
      if (v < 0 || v >= _V || w < 0 || w >= _V)
         throw std::domain_error("Vertice inexistente");
      ++_A;
      _ady[v].push_back(w);
   }


   /**
    * Comprueba si hay arista de u a v.
    */
   bool hayArista(int u, int v) const {
      for (int w : _ady[u])
         if (w == v) return true;
      return false;
   }


   /**
    * Devuelve la lista de adyacencia de v.
    * @throws domain_error si v no existe
    */
   Adys const& ady(int v) const {
      if (v < 0 || v >= _V)
         throw std::domain_error("Vertice inexistente");
      return _ady[v];
   }


   /**
    * Devuelve el grafo dirigido inverso.
    */
   Digrafo inverso() const {
      Digrafo inv(_V);
      for (int v = 0; v < _V; ++v) {
         for (int w : _ady[v]) {
            inv.ponArista(w, v);
         }
      }
      return inv;
   }


   /**
    * Muestra el grafo en el stream de salida o (para depurar)
    */
   void print(std::ostream& o = std::cout) const {
      o << _V << " vértices, " << _A << " aristas\n";
      for (int v = 0; v < _V; ++v) {
         o << v << ": ";
         for (int w : _ady[v]) {
            o << w << " ";
         }
         o << "\n";
      }
   }

};

/**
 * Para mostrar grafos por la salida estándar.
 */
inline std::ostream & operator<<(std::ostream & o, Digrafo const& g) {
   g.print(o);
   return o;
}


#endif /* DIGRAFO_H_ */

```

##### Recorrido en profundidad

```cpp
class DFSDirigido {
public:
	DFSDirigido(Digrafo const& g, int s) : visit(g.V(), false) {
		dfs(g, s);
	}
	
	bool alcanzable(int v) const {
		return visit[v];
	}
	
private:
	std::vector<bool> visit; // visit[v] = ¿hay camino dirigido de s a v?
	void dfs(Digrafo const& g, int v) {
		visit[v] = true;
		for (int w : g.ady(v))
			if (!visit[w]) dfs(g, w);
	}
};
```

###### Alcanzabilidad
- Detectar código muerto, bucles infinitos.
- Recolector basura
- Web crawler

##### Recorrido en anchura
```cpp
class BFSDirigido {
public:
	BFSDirigido(Digrafo const& g, int s) : visit(g.V(), false),
		ant(g.V()), dist(g.V()), s(s) {
		bfs(g);
	}
	
	bool hayCamino(int v) const {
		return visit[v];
	}
	
	int distancia(int v) const {
	return dist[v];
	}

	Camino camino(int v) const {
		if (!hayCamino(v)) throw std::domain_error("No existe camino");
		Camino cam;
		for (int x = v; x != s; x = ant[x])
			cam.push_front(x);
		cam.push_front(s);
		return cam;
	}
private:
	std::vector<bool> visit; // visit[v] = ¿hay camino de s a v?
	std::vector<int> ant; // ant[v] = último vértice antes de llegar a v
	std::vector<int> dist; // dist[v] = aristas en el camino s->v más corto
	int s;

	void bfs(Digrafo const& g) {
		std::queue<int> q;
		dist[s] = 0; visit[s] = true;
		q.push(s);
		while (!q.empty()) {
			int v = q.front(); q.pop();
			for (int w : g.ady(v)) {
				if (!visit[w]) {
					ant[w] = v; dist[w] = dist[v] + 1; visit[w] = true;
					q.push(w);
				}
			}
		}
	}
};
```