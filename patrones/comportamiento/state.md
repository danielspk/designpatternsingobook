# Patrón State

## Propósito

Permite que una variable modifique su comportamiento cada vez que cambie su estado interno. Parecerá que cambia el tipo de dato de la variable.

## También conocido como

_Objects for states_ (Estados como Objetos)

## Aplicabilidad

Úsese el patrón State en cualquiera de los siguientes dos casos:
* El comportamiento de una variable depende de su estado, y debe cambiar en tiempo de ejecución dependiendo de ese estado.
* Las operaciones tienen largas sentencias condicionales con múltiples ramas que dependen del estado de la variable. Ese estado se suele representar por una o más constantes enumeradas. Muchas veces son varias las operaciones que contienen esta misma organización condicional. el patrón state pone cada rama de la condición en un tipo de dato aparte. Esto nos permite tratar al estado de la variable como una variable de pleno derecho que puede variar independientemente de otras variables.

## Estructura

![](/assets/uml/state.png)

## Participantes

* **Contexto:**
  * define la interfaz de interés para los clientes.
  * mantiene una variable de un subtipo de dato de EstadoConcreto que define el estado actual.
* **Estado:**
  * define una interfaz para encapsular el comportamiento asociado con un determinado estado del Contexto.
* **Subtipos de Datos de EstadoConcreto:**
  * cada subtipo de dato implementa un comportamiento asociado con un estado del Contexto.

## Colaboradores

* Contexto delega las peticiones que dependen del estado en la variable EstadoConcreto actual.
* Un contexto puede pasarse a sí mismo como parámetro para que la variable Estado maneje la petición. Esto permite a la variable Estado acceder al contexto si fuera necesario.
* Contexto es la interfaz principal para los clientes. Los clientes pueden configurar un contexto con variables Estado. Una vez que está configurado el contexto, sus clientes ya no tienen que tratar con las variables Estado directamente.
* Cualquiera de los subtipos de datos de Contexto o de EstadoConcreto pueden decidir qué estado sigue a otro y  bajo qué circunstancias.

## Implementación

- No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.
- El _Estado_ se define como interface por simplificación.

## Código de ejemplo

En este ejemplo queremos escribir texto en base al estado de una botonera de estilos, pudiendo ser estos estados "negrita" o "cursiva".

Implementación:

```go
// Interface Estado
type Estado interface {
    Escribir(string) string
}

// Estado Concreto
type EstadoNegrita struct{}

func (en *EstadoNegrita) Escribir(texto string) string {
    return "*" + texto + "*"
}

// Estado Concreto
type EstadoCursiva struct{}

func (ec *EstadoCursiva) Escribir(texto string) string {
    return "_" + texto + "_"
}

// Contexto
type EditorMarkdown struct {
    estado Estado
}

func (em *EditorMarkdown) SetEstado(estado Estado) {
    em.estado = estado
}

func (em *EditorMarkdown) Redactar(texto string) string {
    if em.estado == nil {
        return texto
    }

    return em.estado.Escribir(texto)
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
editor := &EditorMarkdown{}
fmt.Printf("Texto redactado sin estado: %s\n", editor.Redactar("Lorem ipsum"))

editor.SetEstado(&EstadoNegrita{})
fmt.Printf("Texto redactado en negrita: %s\n", editor.Redactar("Lorem ipsum"))

editor.SetEstado(&EstadoCursiva{})
fmt.Printf("Texto redactado en cursiva: %s\n", editor.Redactar("Lorem ipsum"))
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/state) | [Ejecutar código](https://play.golang.org/p/KsYfTyLBDVI)

## Patrones relacionados

El patrón [Flyweight](/patrones/estructurales/flyweight.md) explica cuándo y cómo compartir variables Estado.
Las variables Estado muchas veces son [Singleton](/patrones/creacionales/singleton.md).

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _State_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
