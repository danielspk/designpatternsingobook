# Patrón Facade

## Propósito

Proporciona una interfaz unificada para un conjunto de interfaces de un subsistema. Define una interfaz de alto nivel que hace que el subsistema sea más fácil de usar.

## Aplicabilidad

Úsese el patrón Facade cuando:
* se quiere proporcionar una interfaz simple para un subsistema complejo. Los subsistemas suelen volverse más complicados a medida que van evolucionando. La mayoría de los patrones, cuando se aplican, dan como resultados más tipos de datos y más pequeños. Esto hace que el subsistema sea más reutilizable y fácil de personalizar, pero eso también lo hace más dificil de usar para aquellos clientes que no necesitan personalizarlo. Una fachada puede proporcionar, por omisión, una vista simple del subsistema que resulta adecuada para la mayoría de clientes. Sólo aquellos clientes que necesitan más personalización necesitarán ir más allá de la fachada.
* haya muchas dependencias entre los clientes y los tipos de datos que implementan una abstracción. Se introduce una fachada para desacoplar el subsistema de sus clientes y de otros subsistemas, promoviendo así la independencia entre subsistemas y la portabilidad.
* se requiere dividir en capas los subsistemas. Se usa una fachada para definir un punto de entrada en cada nivel del subsistema. Si éstos son dependientes, se pueden simplificar las dependencias entre ellos haciendo que se comuniquen entre sí únicamente a través de sus fachadas.

## Estructura

![](/assets/uml/facade.png)

## Participantes

* **Fachada:**
  * sabe qué tipos de datos del subsistema son los responsables ante una petición.
  * delega las peticiones de los clientes en las variables apropiadas del subsistema.
* **Tipos del subsistema:**
  * implementa la funcionalidad del subsistema.
  * realizan las labores encomendadas por la variable Fachada.
  * no conocen a la fachada; es decir, no tienen referencias a ella.

## Colaboradores

* Los clientes se comunican con el subsistema enviando peticiones a la variable Fachada, la cual las reenvía a las variables apropiadas del subsistema. Aunque son las variables del subsistema las que realizan el trabajo real, la fachada puede tener que hacer algo de trabajo para pasar de su interfaz a las del subsistema.
* Los clientes que usan la fachada no tienen que acceder directamente a las variables del subsistema.

## Implementación

No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.

## Código de ejemplo

En este ejemplo queremos que un sistema de agencia de viajes pueda interactuar con otros subsistemas: buscador de hoteles y buscador de pasajes aéreos.

Implementación:

```go
// Subsistema
type BuscadorHotel struct{}

func (bh *BuscadorHotel) BuscarHabitacion(entrada string, salida string) []string {
    return []string{
        "Hotel A con Habitación Classic - Entrada " + entrada + ", Salida " + salida + " - $500.00",
        "Hotel B con Habitación Deluxe - Entrada " + entrada + ", Salida " + salida + " - $750.00",
    }
}

// Subsistema
type BuscadorAvion struct{}

func (ba *BuscadorAvion) BuscarPasaje(salida string, regreso string) []string {
    return []string{
        "Aerolinea A - Clase Turista - Salida " + salida + ", Regreso " + regreso + " - $2400.00",
        "Aerolinea A - Clase Ejecutiva - Salida " + salida + ", Regreso " + regreso + " - $3200.00",
        "Aerolinea B - Clase Ejecutiva - Salida " + salida + ", Regreso " + regreso + " - $3800.00",
    }
}

// Fachada
type AgenciaViaje struct{}

func (av *AgenciaViaje) BuscarPaquete(desde string, hasta string) string {
    buscadorHoteles := &BuscadorHotel{}
    buscadorAvion := &BuscadorAvion{}

    resultadosHabitaciones := buscadorHoteles.BuscarHabitacion(desde, hasta)
    resultadosPasajes := buscadorAvion.BuscarPasaje(desde, hasta)

    respuesta := "Hoteles disponibles:\n"

    for _, habitacion := range resultadosHabitaciones {
        respuesta = respuesta + " - " + habitacion + "\n"
    }

    respuesta = respuesta + "\nAerolineas disponibles:\n"

    for _, pajase := range resultadosPasajes {
        respuesta = respuesta + " - " + pajase + "\n"
    }

    return respuesta
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
agencia := &AgenciaViaje{}

fmt.Printf("%s\n", agencia.BuscarPaquete("2018-12-01", "2018-12-08"))
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/estructurales/facade) | [Ejecutar código](https://play.golang.org/p/JM-ZC-pmaxu)

## Patrones relacionados

El patròn [Abstract Factory](/patrones/creacionales/abstractfactory.md) puede usarse para proporcionar una interfaz para crear el subsistema de variables de forma independiente a otros subsistemas. Las fábricas abstractas también pueden ser una alternativa a las fachadas para ocultar tipos de datos específicos de la plataforma.
El patrón [Mediator](/patrones/comportamiento/mediator.md) es parecido al Facade en el sentido de que abstrae funcionalidad a partir de unos tipos de datos existentes. Sin embargo, el propósito del Mediator es abstraer cualquier comunicación entre variables similares, a menudo centralizando la funcionalidad que no pertenece a ninguno de ellas. Los colegas del mediador sólo se preocupan de comunicarse con él y no entre ellos directamente. Por el contrario, una fachada simplemente abstrae una interfaz para las variabless del subsistema, hacíendolas más fácil de usar; no define nueva funcionalidad, y los tipos de datos del subsistema no saben de su existencia.
Normalmente sólo necesita una variable Fachada. Por tanto, éstas suelen implementarse como [Singlotons](/patrones/creacionales/singleton.md).

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Facade_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
