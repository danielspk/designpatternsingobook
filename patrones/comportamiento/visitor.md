# Patrón Visitor

## Propósito

Representa una operación sobre los elementos de una organización de estructuras con estado. Permite definir una nueva operación sin cambiar las estructuras de los elementos sobre los que opera.

## Aplicabilidad

Úsese el patrón Visitor cuando

* una organización de estructuras con estado contiene muchas clases de estructuras con estado con diferentes interfaces, y queremos realizar operaciones sobre esos elementos que dependen de su estructura concreta.
* se necesitan realizar muchas operaciones distintas y no relacionadas sobre estructuras con estado de una organización de estructuras con estado, y queremos evitar "contaminar" sus estructuras con dichas operaciones. El patrón Visitor permite mantener juntas operaciones relacionadas definiéndolas en una estructura. Cuando la organización de estructuras con estado es compartida por varias aplicaciones, el patrón Visitor permite poner operaciones sólo en aquellas aplicaciones que las necesiten.
* las estructuras que definen la organización de estructuras con estado rara vez cambian, pero muchas veces queremos definir nuevas operaciones sobre la organización. Cambiar las estructuras de la organización de estructuras con estado requiere redefinir la interfaz para todos los visitantes, lo que es potencialmente costoso. Si las estructuras de la organización cambian con frecuencia, probablemente sea mejor definir las operaciones en las propias estructuras.

##### Nota:
> "Estructura de Objeto" es sinónimo de "organización de estructuras con estado" para ésta publicación.

## Estructura

![](/assets/uml/visitor.png)

## Participantes

* **Visitante:**
  * declara una operación visitar para cada estructura de operación de ElementoConcreto de la organización de estructuras con estado. El nombre y signatura de la operación identifican a la estructura que envía la petición visitar al visitante. Eso permite al visitante determinar la estructura concreta de elemento que está siendo visitada. A continuación el visitante puede acceder al elemento directamente a través de su interfaz particular.
* **VisitanteConcreto:**
  * implementa cada operación declarada por Visitante. Casa operación implementa un fragmento del algoritmo definido para la estructura correspondiente de la colección. Visitanteconcreto proporciona el contexto para el algoritmo y guarda su estado local. Muchas veces este estado acumula resultados durante el recorrido de la organización de estructuras.
* **Elemento:**
  * define una operación aceptar que toma un visitante como argumento.
* **ElementoConcreto:**
  * implementa una operación aceptar que toma un visitante como argumento.
* **EstructuradDeObjeto _(OrganizaciónDeEstructura)_:**
  * puede enumerar sus elementos.
  * puede proporcionar una interfaz de alto nivel para permitir al visitante visitar a sus elementos.
  * puede ser un [Composite](/patrones/estructurales/composite.md) o una colección, como una lista o un conjunto.

## Colaboradores

* Un cliente que usa el patrón Visitor debe crear una estructura VisitanteConcreto y a continuación recorrer la organización de estructuras, visitando cada estructura con el visitante.
* Cada vez que se visita a un elemento, éste llama a la operación del Visitante que se corresponde con su estructura. El elemento pasa a sí mismo como argumento de la operación para permitir al visitante acceder a su estado, en caso de que sea necesario.

## Implementación

- No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.
- Dado que _Go_ no soporta sobrecarga de método, y a fin de facilitar el ejemplo sin hacer uso de la [reflexión](https://golang.org/pkg/reflect/), los visitantes dispondan de diferentes comportamientos para cada tipo de elemento variando los nombres de sus funciones.
- Se omite del código de ejemplo _EstructuraDeObjeto_ dado que sólo sería una colección que acepta elementos.

## Código de ejemplo

En este ejemplo queremos recrear un juego de rol en donde algunos personajes tengan superpoderes y otros armas de batalla.

Implementación:

```go
// Visitante
type Visitante interface {
    VisitarSuperpoder(*ElementoSuperpoder)
    VisitarArma(*ElementoArma)
}

// Visitante Concreto
type VisitanteNivel1 struct{}

func (v *VisitanteNivel1) VisitarSuperpoder(elementoSuperpoder *ElementoSuperpoder) {
    elementoSuperpoder.Poder = "Rayo superpoderoso"
}

func (v *VisitanteNivel1) VisitarArma(elementoArma *ElementoArma) {
    elementoArma.Arma = "Espada de dos manos"
}

// Visitante Concreto
type VisitanteNivel0 struct{}

func (v *VisitanteNivel0) VisitarSuperpoder(elementoSuperpoder *ElementoSuperpoder) {
    elementoSuperpoder.Poder = "Rayo simple"
}

func (v *VisitanteNivel0) VisitarArma(elementoArma *ElementoArma) {
    elementoArma.Arma = "Espada de una mano"
}

// Elemento
type Elemento interface {
    Aceptar(Visitante)
}

// Elemento Concreto
type ElementoSuperpoder struct {
    Poder string
}

func (e *ElementoSuperpoder) Aceptar(visitante Visitante) {
    visitante.VisitarSuperpoder(e)
}

// Elemento Concreto
type ElementoArma struct {
    Arma string
}

func (e *ElementoArma) Aceptar(visitante Visitante) {
    visitante.VisitarArma(e)
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
// desde visitar
elementoArma0 := &ElementoArma{}
elementoSuperpoder0 := &ElementoSuperpoder{}

visitanteNivel0 := &VisitanteNivel0{}
visitanteNivel0.VisitarArma(elementoArma0)
visitanteNivel0.VisitarSuperpoder(elementoSuperpoder0)

fmt.Printf("El visitante Nivel 0 tiene la siguiente arma de batalla: %s\n", elementoArma0.Arma)
fmt.Printf("El visitante Nivel 0 tiene el siguiente superpoder: %s\n", elementoSuperpoder0.Poder)

elementoArma1 := &ElementoArma{}
elementoSuperpoder1 := &ElementoSuperpoder{}

visitanteNivel1 := &VisitanteNivel1{}
visitanteNivel1.VisitarArma(elementoArma1)    visitanteNivel1.VisitarSuperpoder(elementoSuperpoder1)

fmt.Printf("El visitante Nivel 1 tiene la siguiente arma de batalla: %s\n", elementoArma1.Arma)
fmt.Printf("El visitante Nivel 1 tiene el siguiente superpoder: %s\n", elementoSuperpoder1.Poder)

// desde aceptar
visitanteNivel0 = &VisitanteNivel0{}
elementoArma0 = &ElementoArma{}
elementoArma0.Aceptar(visitanteNivel0)

fmt.Printf("El elemento Arma aceptada por un visitante Nivel 0 es: %s\n", elementoArma0.Arma)
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/visitor) | [Ejecutar código](https://play.golang.org/p/WSPGvlwREuQ)

## Patrones relacionados

[Composite](/patrones/estructurales/composite.md): los visitantes pueden usarse para aplicar una operación sobre una organización de estructuras definida por el patrón composite.
[Interpreter](/patrones/comportamiento/interpreter.md): se puede aplicar el patrón visitor para llevar a cabo la implementación.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Visitor_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
