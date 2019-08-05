# Patrón Interpreter

## Propósito

Dado un lenguaje, define una representación de su gramática junto con un intérprete que usa dicha representación para interpretar sentencias del lenguaje.

## Aplicabilidad

Úsese el patrón Interpreter cuando hay un lenguaje que interpretar y se pueden representar las sentencias del lenguaje como árboles de sintácticos abstractos. El patrón Interpreter funciona mejor cuando la gramática es simple. Para gramáticas complejas, la jerarquía de tipos de datos de la gramática se vuelve grande e inmanejable. Herramientas como los generadores de analizadores sintácticos constituyen una alternativa mejor en estos casos. Éstas pueden interpretar expresiones sin necesidad de construir árboles sintácticos abstractos, lo que puede ahorrar espacio y, posiblemente, tiempo.
La eficiencia no es una preocupación crítica. Los intérpretes más eficientes normalmente no se implementan interpretando árboles de análisis sintáctico directamente, sino que primero los traducen en algún otro formato. Por ejemplo, las expresiones regulares suelen transformarse en máquinas de estados. Pero incluso en ese caso, el _traductor_ puede implementarse con el patrón Interpreter, de modo que éste sigue siendo aplicable.

## Estructura

![](/assets/uml/interpreter.png)

## Participantes

* **ExpresionAbstracta:**
  * declara una operación abstracta _interpretar_ que es común a todos los nodos del árbol de sintaxis abstracto.
* **ExpresionTerminal:**
  * implementa una operación _interpretar_ asociada con los símbolos terminales de la gramática.
  * se necesita una variable de este tipo de dato para cada símbolo terminal de la sentencia.
* **ExpresionNoTerminal:**
  * por cada regla de la gramática debe haber uno de estos tipos de datos.
  * mantiene variables de tipo ExpresionAbstracta para cada uno de los símbolos de cada regla.
* **Contexto:**
  * contiene información que es global al intérprete.
* **Cliente:**
  * construye (o recibe) un árbol sintáctico abstracto que representa una determinada sentencia del lenguaje definido por la gramática. Este aŕbol sintáctico abstracto está formado por variables del tipo de dato ExpresionNoTerminal y ExpresionTerminal.
  * invoca a la operación _interpretar_.

## Colaboradores

* El cliente construye (o recibe) la sentencia como un árbol sintáctico abstracto formado por variables de ExpresionTerminal y ExpresionNoTerminal. A continuación el cliente inicializa el contexto e invoca a la operación _interpretar_.
* Cada nodo ExpresionNoTerminal define _interpretar_ en términos de _interpretar_ de cada subexpresión. La operación _interpretar_ de cada ExpresionTerminal define el caso base de recursión.
* Las operaciones _interpretar_ de cada nodo usan el contexto para almacenar y acceder al estado del intérprete.

## Implementación

- No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.
- La _ExpresionAbstracta_ se define como una interfaz por simplificación.

## Código de ejemplo

En este ejemplo queremos que interpretar distintas expresiones lógicas: AND y OR en base a palabras definidas en un contexto.

Implementación:

```go
// Contexto
type Contexto struct {
    Palabra string
}

// Interface
type ExpresionAbstracta interface {
    Interpretar(Contexto) bool
}

// Expresion Terminal
type ExpresionTerminal struct {
    Palabra string
}

func (et *ExpresionTerminal) Interpretar(contexto Contexto) bool {
    return contexto.Palabra == et.Palabra
}

// Expresion No Terminal
type ExpresionOR struct {
    expresionA ExpresionAbstracta
    expresionB ExpresionAbstracta
}

func (eo *ExpresionOR) Interpretar(contexto Contexto) bool {
    return eo.expresionA.Interpretar(contexto) || eo.expresionB.Interpretar(contexto)
}

// Expresion No Terminal
type ExpresionAND struct {
    expresionA ExpresionAbstracta
    expresionB ExpresionAbstracta
}

func (ea *ExpresionAND) Interpretar(contexto Contexto) bool {
    return ea.expresionA.Interpretar(contexto) && ea.expresionB.Interpretar(contexto)
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
expresionA := &ExpresionTerminal{"Perro"}
expresionB := &ExpresionTerminal{"Gato"}
expresionC := &ExpresionTerminal{"Perro"}

contextoOR := Contexto{"Perro"}
expresionOR := &ExpresionOR{expresionA, expresionB}
fmt.Printf("La expresion OR contiene la palabra perro: %v\n", expresionOR.Interpretar(contextoOR))

contextoAND := Contexto{"Perro"}
expresionAND := &ExpresionAND{expresionA, expresionC}
fmt.Printf("La expresion AND contiene dos palabras perro: %v\n", expresionAND.Interpretar(contextoAND))
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/interpreter) | [Ejecutar código](https://play.golang.org/p/zmXhDClx5k7)

## Patrones relacionados

[Composite](/patrones/estructurales/composite.md): el árbol sintáctico abstracto es una variable del patrón Composite.
El patrón [Flyweight](/patrones/comportamiento/flyweight.md) muestra cómo compartir terminales dentro del árbol sintáctico abstracto.
[Iterator](/patrones/comportamiento/iterator.md): el intérprete puede usar un Iterator para recorrer la estructura.
Puede usarse el patrón [Visitor](/patrones/comportamiento/visitor.md) para mantener el comportamiento de cada nodo del árbol sintáctico abstracto de una clase.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Interpreter_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
