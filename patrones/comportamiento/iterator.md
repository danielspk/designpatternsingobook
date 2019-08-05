# Patrón Iterator

## Propósito

Proporciona un modo de acceder secuencialmente a los elementos de una variable agregada sin exponer su representación interna.

## También conocido como

_Cursor_

## Aplicabilidad

Úsese el patrón Iterator

* para acceder al contenido de una variable agregada sin exponer su representación interna.
* para permitir varios recorridos sobre variables agregadas.
* para proporcionar una interfaz uniforme para recorrer diferentes estructuras agregadas (es decir, para permitir la iteración polimórfica).

## Estructura

![](/assets/uml/iterator.png)

## Participantes

* **Iterador:**
  * define una interfaz para recorrer los elementos y acceder a ellos.
* **IteradorConcreto:**
  * implementa la interfaz Iterador.
  * mantiene la posición actual en el recorrido del agregado.
* **Agregado:**
  * define una interfaz para crear una variable Iterador.
* **AgregadoConcreto:**
  * implementa la interfaz de creación de Iterador para devolver una variable del IteradorConcreto apropiado.

## Colaboradores

Un IteradorConcreto sabe cúal es la variable actual del agregado y puede calcular la variable siguiente en el recorrido.

## Implementación

- No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.
- El _Iterador_ y _Agregado_ se definen como interfaces por simplificación.

## Código de ejemplo

En este ejemplo queremos recorrer las distintas estaciones de radio preseteadas de un estéreo de audio.

Implementación:

```go
// Iterador Interface
type Iterador interface {
    Valor() string
    Siguiente()
    Anterior()
}

// Agregado Interface
type Agregado interface {
    CrearIterador() Iterador
}

// Agregado Concreto
type Radio struct {
    Estaciones []string
}

func (r *Radio) CrearIterador() Iterador {
    return &RadioIterador{radio: r}
}

func (r *Radio) Registrar(estacion string) {
    r.Estaciones = append(r.Estaciones, estacion)
}

// Iterador Concreto
type RadioIterador struct {
    radio  *Radio
    indice int
}

func (ri *RadioIterador) Valor() string {
    return ri.radio.Estaciones[ri.indice]
}

func (ri *RadioIterador) Siguiente() {
    ri.indice++
}

func (ri *RadioIterador) Anterior() {
    ri.indice--
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
radio := &Radio{}
radio.Registrar("FM100")
radio.Registrar("FM200")
radio.Registrar("FM300")

iterador := radio.CrearIterador()

fmt.Printf("Escuhando la radio %s\n", iterador.Valor())

iterador.Siguiente()
fmt.Printf("Escuhando la radio %s\n", iterador.Valor())

iterador.Siguiente()
fmt.Printf("Escuhando la radio %s\n", iterador.Valor())

iterador.Anterior()
fmt.Printf("Escuhando nuevamente la radio %s\n", iterador.Valor())
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/iterator) | [Ejecutar código](https://play.golang.org/p/qpY_F7wrd6u)

## Patrones relacionados

[Composite](/patrones/estructurales/composite.md): los iteradores suelen aplicarse a estructuras recursivas como los Composite.
[Factory Method](/patrones/creacionales/factorymethod.md): los iteradores polimórficos se basan en funciones de fabricación para crear variables de los subtipos de datos apropiados de Iterator.
El patrón [Memento](/patrones/comportamiento/memento.md) suele usarse conjuntamente con el patrón Iterator. Un iterador puede usar un memento para representar el estado de una iteración. El iterador almacena el memento internamente.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Iterator_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
