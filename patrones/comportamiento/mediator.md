# Patrón Mediator

## Propósito

Define una estructura con estado que encapsula cómo interactúan una serie de estructuras con estado. Promueve un bajo acoplamiento al evitar que las estructuras con estado se refieran unas a otras explícitamente, y permite variar la interacción entre ellas de forma independiente.

## Aplicabilidad

Úsese el patrón Mediator cuando:
* un conjunto de estructuras con estado se comunican de forma bien definida, pero compleja. Las interdependencias resultantes no están estructuradas y son difíciles de comprender.
* es difícil reutilizar una estructura con estado, ya que ésta se refiere a otras muchas estructuras con estado, con las que se comunica.
* un comportamiento que ésta distribuido entre varias estructuras debería poder ser adaptado sin necesidad de una gran cantidad de sub estructuras.

## Estructura

![](/assets/uml/mediator.png)

## Participantes

* **Mediador:**
  * define una interfaz para comunicarse con sus estructuras con estado Colega.
* **MediadorConcreto:**
  * implementa el comportamiento cooperativo coordinando estructuras con estado Colega.
  * conoce a sus Colegas.
* **Colega:**
  * cada estructura Colega conoce a su estructura con estado Mediador.
  * cada Colega se comunica con su mediador cada vez que, de no existir éste, se hubiera comunicado con otro Colega.

## Colaboradores

Los Colegas envían y reciben peticiones a través de un Mediador. El mediador implementa el comportamiento cooperativo encaminando estas peticiones a los Colegas apropiados.

## Implementación

- No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.
- El _Mediador_ y _Colega_ se definen como interfaces por simplificación.

## Código de ejemplo

En este ejemplo queremos montar una sala de chat en donde los usuarios puedan comunicarse entre sí. La sala de chat actua como mediador entre los usuarios.

Implementación:

```go
// Interface Mediador
type Mediador interface {
    MostrarMensaje(Usuario, string)
}

// Mediador Concreto
type ChatRoom struct{}

func (cr *ChatRoom) MostrarMensaje(usuario Usuario, mensaje string) {
    fmt.Printf("El mensaje de %s es: %s\n", usuario.GetNombre(), mensaje)
}

// Interface Colega
type Usuario interface {
    EnviarMensaje(string)
    GetNombre() string
}

// Colega Concreto
type UsuarioChat struct {
    nombre   string
    mediador Mediador
}

func (u *UsuarioChat) GetNombre() string {
    return u.nombre
}

func (u *UsuarioChat) EnviarMensaje(mensaje string) {
    u.mediador.MostrarMensaje(u, mensaje)
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
mediador := &ChatRoom{}

usuarioA := &UsuarioChat{"Daniel", mediador}
usuarioB := &UsuarioChat{"Pedro", mediador}

usuarioA.EnviarMensaje("Hola como estas?")
usuarioB.EnviarMensaje("Muy bien y vos?")
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/mediator) | [Ejecutar código](https://play.golang.org/p/PWO1HBJYjPx)

## Patrones relacionados

El patrón [Facade](/patrones/estructurales/facade.md) difiere del Mediator en que abstrae un subsistema de estructuras con estado para proporcionar una interfaz más conveniente. Su protocolo es unidireccional; es decir, las estructuras con estado Facade hacen peticiones a las sub estructuras del subsistema pero no a la inversa. Por el contrario, el patrón Mediator permite un comportamiento cooperativo que no es proporcionado por las estructuras con estado Colegas y el protocolo es multidireccional.
Los Colegas pueden comunicarse con el mediador usando el patrón [Observer](/patrones/comportamiento/observer.md).

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Mediator_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
