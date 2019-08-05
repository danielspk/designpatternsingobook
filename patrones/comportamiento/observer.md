# Patrón Observer

## Propósito

Define una dependencia de uno-a-muchos entre variables, de forma que cuando una variable cambie de estado se notifique y se actualicen automáticamente todas las variables que dependan de ellá.

## También conocido como

_Dependents_ (Dependientes), _Publish-subscribe_ (Publicar-Suscribir)

## Aplicabilidad

Úsese el patrón Onserver en cualquiera de las siguientes situaciones:
* Cuando una abstracción tiene dos aspectos y uno depende del otro. Encapsular estos aspectos en variables separadas permite modificarlas y reutilizarlos de forma independiente.
* cuando un cambio en una variable requiere cambiar otras, y no sabemos cuántas variables necesitan cambiarse.
* cuando una variable debería ser capaz de notificar a otras sin hacer suposiciones sobre quiénes son dichas variables. En otras palabras, cuando no queremos que estas variables estén fuertemente acopladas.

## Estructura

![](/assets/uml/observer.png)

## Participantes

* **Sujeto:**
  * conoce a sus observadores. Un sujeto puede ser observado por cualquier número de variables Observador.
  * proporciona una interfaz para asignar y quitar variables Observador.
* **Observador:**
  * define una interfaz para actualizar las variables que deben ser notificadas ante cambios en un sujeto.
* **SujetoConcreto:**
  * almacena el estado de interés para las variables ObservadorConcreto.
  * envía una notificación a sus observadores cuando cambia su estado.
* **ObservadorConcreto:**
  * mantiene una referencia a una variable SujetoConcreto.
  * guarda un estado que debería ser consistente con el del sujeto.
  * implementa la interfaz de actualización del Observador para mantener su estado consistente.

## Colaboradores

* SujetoConcreto notifica a sus observadores cada vez que se produce un cambio que pudiera hacer que el estado de éstos fuera inconsistente con el suyo.
* Después de ser informado de un cambio en el sujeto concreto, una variable ObservadorConcreto puede pedirle al sujeto más información. ObservadorConcreto usa esta información para sincronizar su estado con el del sujeto.

## Implementación

- No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.
- El _Sujeto_ y _Observador_ se definen como interfaces por simplificación.

## Código de ejemplo

En este ejemplo queremos que postulantes a empleos sean notificados cuando se creen ofertas laborales.

Implementación:

```go
// Interface Sujeto
type Sujeto interface {
    Adquirir(Observador)
    notificar()
}

// Sujeto Concreto
type AgenciaEmpleo struct {
    observadores []Observador
}

func (ae *AgenciaEmpleo) Adquirir(observador Observador) {
    ae.observadores = append(ae.observadores, observador)
}

func (ae *AgenciaEmpleo) notificar(oferta string) {
    for _, observador := range ae.observadores {
        observador.Actualizar(oferta)
    }
}

func (ae *AgenciaEmpleo) IngresarOfertaLaboral(oferta string) {
    ae.notificar(oferta)
}

// Interface Observador
type Observador interface {
    Actualizar(string)
}

// Observador Concreto
type ObservadorEmpleo struct {
    nombre string
}

func (o *ObservadorEmpleo) Actualizar(oferta string) {
    fmt.Printf("Hola %s, existe la siguiente oferta de empleo: %s\n", o.nombre, oferta)
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
observadorA := &ObservadorEmpleo{"Juan"}
observadorB := &ObservadorEmpleo{"Maria"}

agencia := &AgenciaEmpleo{}
agencia.Adquirir(observadorA)
agencia.Adquirir(observadorB)

agencia.IngresarOfertaLaboral("Programador JAVA Senior")
fmt.Printf("\n")
agencia.IngresarOfertaLaboral("Programador C# Junior")
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/observer) | [Ejecutar código](https://play.golang.org/p/7CAEfYjM1lr)

## Patrones relacionados

[Mediator](/patrones/comportamiento/mediator.md): encapsulando semánticas de actualización complejas, se puede implementar un gestor de cambios que actue como mediador entre sujetos y observadores.
[Singleton](/patrones/creacionales/singleton.md): este gestor de cambios puede usar el patrón Singleton para que sea único y globalmente accesible.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Observer_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
