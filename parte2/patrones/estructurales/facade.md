# Facade

## Propósito

Según el libro "Patrones de Diseño" [\[29\]](../../../recursos.md) el patrón _Facade_ "proporciona una interfaz unificada para un conjunto de interfaces de un subsistema. Define una interfaz de alto nivel que hace que el subsistema sea más fácil de usar".

## Estructura

![](../../../.gitbook/assets/facade.png)

## Participantes

* **Fachada:**
  * sabe qué tipos de datos del subsistema son los responsables ante una petición.
  * delega las peticiones de los clientes en las variables apropiadas del subsistema.
* **Tipos del subsistema:**
  * implementa la funcionalidad del subsistema.
  * realizan las labores encomendadas por la variable Fachada.
  * no conocen a la fachada; es decir, no tienen referencias a ella.

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

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/estructurales/facade) \| [Ejecutar código](https://play.golang.org/p/JM-ZC-pmaxu)

