# Memento

## Propósito

Según el libro "Patrones de Diseño" [\[29\]](../../../recursos.md) el patrón _Memento_ "representa y externaliza el estado interno de una variable sin violar la encapsulación, de forma que ésta pueda volver a dicho estado más tarde".

## También conocido como

_Token_

## Estructura

![](../../../.gitbook/assets/memento.png)

## Participantes

* **Memento:**
  * guarda el estado interno de la variable Creador. El memento puede guardar tanta información del estado interno del creador como sea necesario a discreción del creador.
  * protege frente a accesos de otras variables que no sean el creador. Los mementos tienen realmente dos interfaces. El Conserje va una interfaz _reducida_ del memento - sólo puede pasar el memento a otras variables -. El Creador, por el contrario, ve una interfaz _amplia_, que le permite acceder a todos los datos necesarios para volver a su estado anterior. Idealmente, sólo el creador que produjo el memento estaría autorizado a acceder al estado interno de éste.
* **Creador:**
  * crea un memento que contiene una instantánea de su estado interno actual.
  * usa el memento para volver a su estado anterior.
* **Conserje:**
  * es responsable de guardar en lugar seguro el memento.
  * nunca examina los contenidos del memento, ni opera sobre ellos.

## Implementación

No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.

## Código de ejemplo

En este ejemplo queremos que un editor de texto tenga la posibilidad de volver atras su estado luego de una actualización de contenido.

Implementación:

```go
// Interface
type Memento interface {
    SetContenido(string)
    GetContenido() string
}

// Memento
type EditorMemento struct {
     contenido string
}

func (em *EditorMemento) SetContenido(contenido string) {
    em.contenido = contenido
}

func (em *EditorMemento) GetContenido() string {
    return em.contenido
}

// Originador
type Editor struct {
    contenido string
}

func (e *Editor) VerContenido() string {
    return e.contenido
}

func (e *Editor) Escribir(texto string) {
    e.contenido = e.contenido + " " + texto
}

func (e *Editor) Guardar() Memento {
    editorMemento := &EditorMemento{}
    editorMemento.SetContenido(e.contenido)

    return editorMemento
}

func (e *Editor) Restaurar(memento Memento) {
    e.contenido = memento.GetContenido()
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
editor := &Editor{}
editor.Escribir("TextoA")
editor.Escribir("TextoB")
fmt.Printf("El editor contiene:%s\n", editor.VerContenido())

fmt.Println("Se guarda el estado actual")
memento := editor.Guardar()

fmt.Println("Se escribe unnuevo contenido")
editor.Escribir("TextoC")

fmt.Printf("El editor ahora contiene:%s\n", editor.VerContenido())

fmt.Println("Se restaura el contenido guardado")
editor.Restaurar(memento)

fmt.Printf("El editor nuevamente contiene:%s\n", editor.VerContenido())
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/memento) \| [Ejecutar código](https://play.golang.org/p/4o78qJhd-h2)

