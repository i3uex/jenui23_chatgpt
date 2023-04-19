You:
Dado el grafo no dirigido formado por los nodos {A,B,C,D,E,F,G} y las aristas {(A,B),(B,A),(A,C),(C,A),(A,D), (D,A),(B,C),(C,B),(B,E),(E,B),(C,D),(D,C), (C,E), (E,C), (C,F), (F,C), (D,F), (F,D), (E,F), (F,E), (F,G), (G,F)}. 
Este grafo representa el espacio de búsqueda de un problema. 

El estado inicial de la búsqueda corresponde al nodo A. 
Los valores de la función heurística h que estima el camino que falta hasta la solución desde cada nodo toma los siguientes valores {h(A)=6,h(B)=7,h(C)=4,h(D)=3,h(E)=2,h(F)=8,h(G)=0}

Representa gráficamente, cada una de las situaciones por las que va pasando el árbol de búsqueda para el algoritmo de primero mejor. Debe dibujar un árbol cada vez que expanda un nodo. 

ChatGPT:
El algoritmo de primero mejor se basa en expandir siempre el nodo que tenga el valor de la función heurística h más bajo. Por lo tanto, en este caso, el árbol de búsqueda se desarrollaría de la siguiente manera:

`El primer nodo expandido será el nodo E, ya que tiene el valor de h más bajo (2). El árbol de búsqueda tendría la siguiente forma:`

```css
       A
      /
     E
```

`El siguiente nodo expandido sería el nodo D, ya que tiene el siguiente valor de h más bajo (3). El árbol de búsqueda se vería así:`

```css
       A
      /
     E
      \
       D
```

`Luego, se expandiría el nodo C, ya que tiene el siguiente valor de h más bajo (4). El árbol de búsqueda se vería así:`

```css
       A
      /
     E
    / \
   C   D
```

`A continuación, se expandiría el nodo B, ya que tiene el siguiente valor de h más bajo (7). El árbol de búsqueda se vería así:`

```css
       A
      /
     E
    / \
   C   D
        \
         B
```

`Finalmente, se expandiría el nodo F, ya que tiene el siguiente valor de h más bajo (8). El árbol de búsqueda se vería así:`

```css
       A
      /
     E
    / \
   C   D
        \
         B
          \
           F
```

En este punto, el algoritmo de primero mejor habría expandido todos los nodos del grafo, y encontrado la solución en el nodo G, que tiene un valor de h igual a 0.