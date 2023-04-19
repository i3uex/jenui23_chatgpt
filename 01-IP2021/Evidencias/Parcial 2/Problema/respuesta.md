You:
Una productora musical está desarrollando una aplicación para reproducir canciones de su catálogo en el móvil. Te han contratado para que desarrolles la gestión de las canciones que escucha una persona.

Ya se ha definido un TAD Cancion que contiene la información de cada canción: un identificador (entero), cantante (string), duración (real) y veces que se ha escuchado (int).

Las cabeceras de las operaciones del TAD Cancion son:

// Inicia la información de la canción. Inicialmente el número de veces que se ha escuchado la canción es 1.
void nueva (int id, string cantante, float duracion, Cancion &c);
// Incrementa el número de veces que se ha escuchado la canción c
void incrementar (Cancion &c);
// devuelve el identificador de la canción c
int obtenerIdentificador (Cancion c);
// devuelve el nombre de la persona o grupo que canta la canción c
string obtenerCantante (Cancion c);
// devuelve la duración de la canción c
float obtenerDuracion (Cancion c);
// devuelve el número de veces que se ha escuchado la canción c
int obtenerVeces (Cancion c);

El número máximo de canciones que va a poder gestionar la aplicación es 5000.

La especificación de las operaciones del TAD Reproductor que debes implementar son las siguientes:

TAD
  Reproductor es iniciar, escuchar, total, masEscuchada, borrar
Operaciones
  iniciar
          salida: Reproductor
          efecto: Inicia la estructura sin información
  escuchar (r: Reproductor, identificador: int, cantante: string, duracion: float)
          modifica: r
          efecto: Actualiza la información del reproductor con la canción que se está escuchando. Si ya existe una canción con el mismo identificador, incrementa el número de veces que se ha escuchado. Si no, inserta la información de esa nueva canción. Si se ha alcanzado el máximo de capacidad, esta operación no hace nada.
  total (r: Reproductor, cantante: string)
          salida: int, float
          efecto: Devuelve el número de canciones y la duración total de todas las canciones del cantante que se indica.
  masEscuchada (r: Reproductor)
          salida: int, string
          efecto: Devuelve identificador y cantante de la canción que más veces se ha escuchado. Podemos suponer que hay, como mínimo, una canción. Si hay varias canciones que se han escuchado las mismas veces, devuelve una cualquiera.
  borrar (r: Reproductor, n: int)
          modifica: r
          salida: int, float
          efecto: Borra la información de todas las canciones que se han escuchado menos de n veces. Además, la operación devolverá el número de canciones borradas y su duración total.

Otra persona ya ha definido la estructura de datos para el Reproductor y ha implementado la operación iniciar.

const int MAX = 5000;
typedef Cancion TVector[MAX];
struct Reproductor {
  TVector vector;
  int ocupadas;
};

void iniciar (Reproductor &r) {
  r.ocupadas = 0;
}

1. a) Implementar de forma eficiente la operación escuchar del TAD Reproductor.

ChatGPT:
La operación `escuchar` debería implementarse de la siguiente manera:

```c
void escuchar(Reproductor &r, int identificador, string cantante, float duracion) {
  if (r.ocupadas == MAX) return; // si el vector está lleno, no hacer nada

  // buscar la canción con el identificador especificado
  int posicion = -1;
  for (int i = 0; i < r.ocupadas; i++) {
    if (obtenerIdentificador(r.vector[i]) == identificador) {
      posicion = i;
      break;
    }
  }

  // si la canción ya existe, incrementar el número de veces que se ha escuchado
  if (posicion != -1) {
    incrementar(r.vector[posicion]);
    return;
  }

  // si la canción no existe, agregarla al vector de canciones
  nueva(identificador, cantante, duracion, r.vector[r.ocupadas]);
  r.ocupadas++;
}
```

Esta implementación busca la canción con el identificador especificado en el vector de canciones. Si la canción ya existe, se incrementa el número de veces que se ha escuchado. Si no existe, se agrega la canción al vector de canciones y se incrementa el contador de canciones ocupadas.

You:
1. b) Implementar de forma eficiente la operación total del TAD Reproductor.

ChatGPT:
La operación `total` debería implementarse de la siguiente manera:

```c
void total(Reproductor &r, string cantante, int &numCanciones, float &duracionTotal) {
  numCanciones = 0;
  duracionTotal = 0;

  for (int i = 0; i < r.ocupadas; i++) {
    if (obtenerCantante(r.vector[i]) == cantante) {
      numCanciones++;
      duracionTotal += obtenerDuracion(r.vector[i]);
    }
  }
}
```

Esta implementación recorre todas las canciones del vector de canciones y, para aquellas que tienen el mismo cantante que el especificado, se cuentan y se suma su duración a la duración total. Al finalizar el recorrido, `numCanciones` y `duracionTotal` contienen el número de canciones y la duración total de las canciones del cantante especificado.

You:
1. c) Implementar de forma eficiente la operación masEscuchada del TAD Reproductor.

ChatGPT:
La operación `masEscuchada` debería implementarse de la siguiente manera:

```c
void masEscuchada(Reproductor &r, int &identificador, string &cantante) {
  identificador = -1;
  cantante = "";
  int veces = 0;

  // buscar la canción más escuchada
  for (int i = 0; i < r.ocupadas; i++) {
    if (obtenerVeces(r.vector[i]) > veces) {
      identificador = obtenerIdentificador(r.vector[i]);
      cantante = obtenerCantante(r.vector[i]);
      veces = obtenerVeces(r.vector[i]);
    }
  }
}
```

Esta implementación recorre todas las canciones del vector de canciones y busca aquella que tenga el mayor número de veces que se ha escuchado. Al finalizar el recorrido, `identificador` y `cantante` contienen el identificador y el cantante de la canción más escuchada.

You:
1. d) Implementar de forma eficiente la operación borrar del TAD Reproductor.

ChatGPT:
La operación `borrar` debería implementarse de la siguiente manera:

```c
void borrar(Reproductor &r, int n, int &numCancionesBorradas, float &duracionTotalBorrada) {
  numCancionesBorradas = 0;
  duracionTotalBorrada = 0;

  // recorrer el vector de canciones y borrar aquellas que se han escuchado menos de n veces
  for (int i = 0; i < r.ocupadas; i++) {
    if (obtenerVeces(r.vector[i]) < n) {
      numCancionesBorradas++;
      duracionTotalBorrada += obtenerDuracion(r.vector[i]);
      r.vector[i] = r.vector[r.ocupadas - 1];
      r.ocupadas--;
      i--;
    }
  }
}
```

Esta implementación recorre todas las canciones del vector de canciones y, para aquellas que se han escuchado menos de `n` veces, se eliminan del vector de canciones y se cuentan y se suma su duración a la duración total borrada. Al finalizar el recorrido, `numCancionesBorradas` y `duracionTotalBorrada` contienen el número de canciones borradas y su duración total.

You:
2. Queremos implementar una operación tiempo que devuelva la duración total de todas las canciones que contiene el reproductor. Esta operación debe tener coste constante. Indicar claramente los cambios que deben hacerse en la estructura y en las operaciones del TAD para conseguirlo.

ChatGPT:
Para poder implementar una operación `tiempo` que tenga coste constante, se pueden realizar los siguientes cambios en la estructura y en las operaciones del TAD:

`En la estructura Reproductor, agregar un nuevo campo duracionTotal que contenga la duración total de todas las canciones que contiene el reproductor.``En la operación escuchar, actualizar el campo duracionTotal con la duración de la canción que se está escuchando. Si la canción ya existe, solo se actualiza el número de veces que se ha escuchado, sin afectar el campo duracionTotal.``En la operación borrar, actualizar el campo duracionTotal con la duración total borrada.`

Con estos cambios, se puede implementar una operación `tiempo` que tenga coste constante:

```javascript
float tiempo(Reproductor &r) {
  return r.duracionTotal;
}
```

Esta operación simplemente devuelve el valor del campo `duracionTotal` de la estructura `Reproductor`. Al estar este valor actualizado en las operaciones que modifican el reproductor, se puede obtener la duración total de todas las canciones en tiempo constante.
