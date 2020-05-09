# Visitor

## Propósito

Según el libro "Patrones de Diseño" [\[29\]](../../../recursos.md) el patrón _Visitor_ "representa una operación sobre los elementos de una estructura de variables. Permite definir una nueva operación sin cambiar los tipos de datos de los elementos sobre los que opera".

## Estructura

![](../../../.gitbook/assets/visitor.png)

## Participantes

* **Visitante:**
  * declara una operación visitar para cada tipo de dato de operación de ElementoConcreto de la estructura de variables. El nombre y signatura de la operación identifican al tipo de dato que envía la petición visitar al visitante. Eso permite al visitante determinar el tipo de dato concreto de elemento que está siendo visitada. A continuación el visitante puede acceder al elemento directamente a través de su interfaz particular.
* **VisitanteConcreto:**
  * implementa cada operación declarada por Visitante. Casa operación implementa un fragmento del algoritmo definido para el tipo de dato correspondiente de la colección. Visitanteconcreto proporciona el contexto para el algoritmo y guarda su estado local. Muchas veces este estado acumula resultados durante el recorrido de la estructura.
* **Elemento:**
  * define una operación aceptar que toma un visitante como argumento.
* **ElementoConcreto:**
  * implementa una operación aceptar que toma un visitante como argumento.
* **EstructuradDeObjeto:**
  * puede enumerar sus elementos.
  * puede proporcionar una interfaz de alto nivel para permitir al visitante visitar a sus elementos.
  * puede ser un [Composite](../estructurales/composite.md) o una colección, como una lista o un conjunto.

## Implementación

* No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.
* Dado que _Go_ no soporta sobrecarga de método, y a fin de facilitar el ejemplo sin hacer uso de la [reflexión](https://golang.org/pkg/reflect/), los visitantes dispondan de diferentes comportamientos para cada tipo de elemento variando los nombres de sus funciones.
* Se omite del código de ejemplo _EstructuraDeObjeto_ dado que sólo sería una colección que acepta elementos.

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

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/visitor) \| [Ejecutar código](https://play.golang.org/p/WSPGvlwREuQ)

