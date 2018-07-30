# Patrón Interpreter

## Propósito

Dado un lenguaje, define una representación de su gramática junto con un intérprete que usa dicha representación para interpretar sentencias del lenguaje.

## Aplicabilidad

Úsese el patrón Interpreter cuando hay un lenguaje que interpretar y se pueden representar las sentencias del lenguaje como árboles de sintácticos abstractos. El patrón Interpreter funciona mejor cuando la gramática es simple. Para gramáticas complejas, la jerarquía de estructuras de la gramática se vuelve grande e inmanejable. Herramientas como los generadores de analizadores sintácticos constituyen una alternativa mejor en estos casos. Éstas pueden interpretar expresiones sin necesidad de construir árboles sintácticos abstractos, lo que puede ahorrar espacio y, posiblemente, tiempo.
La eficiencia no es una preocupación crítica. Los intérpretes más eficientes normalmente no se implementan interpretando árboles de análisis sintáctico directamente, sino que primero los traducen en algún otro formato. Por ejemplo, las expresiones regulares suelen transformarse en máquinas de estados. Pero incluso en ese caso, el _traductor_ puede implementarse con el patrón Interpreter, de modo que éste sigue siendo aplicable.

## Estructura

![](/assets/uml/interpreter.png)

## Participantes

* **ExpresionAbstracta:**
  * declara una operación abstracta _interpretar_ que es común a todos los nodos del árbol de sintaxis abstracto.
* **ExpresionTerminal:**
  * implementa una operación _interpretar_ asociada con los símbolos terminales de la gramática.
  * se necesita una instancia de esta estructura para cada símbolo terminal de la sentencia.
* **ExpresionNoTerminal:**
  * por cada regla de la gramática debe haber una de estas estructuras.
  * mantiene variables de instancia de tipo ExpresionAbstracta para cada uno de los símbolos de cada regla.
* **Contexto:**
  * contiene información que es global al intérprete.
* **Cliente:**
  * construye (o recibe) un árbol sintáctico abstracto que representa una determinada sentencia del lenguaje definido por la gramática. Este aŕbol sintáctico abstracto está formado por instancias de las estructuras ExpresionNoTerminal y ExpresionTerminal.
  * invoca a la operación _interpretar_.

## Colaboradores

* El cliente construye (o recibe) la sentencia como un árbol sintáctico abstracto formado por instancias de ExpresionTerminal y ExpresionNoTerminal. A continuación el cliente inicializa el contexto e invoca a la operación _interpretar_.
* Cada nodo ExpresionNoTerminal define _interpretar_ en términos de _interpretar_ de cada subexpresión. La operación _interpretar_ de cada ExpresionTerminal define el caso base de recursión.
* Las operaciones _interpretar_ de cada nodo usan el contexto para almacenar y acceder al estado del intérprete.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

[Composite](/patrones/estructurales/composite.md): el árbol sintáctico abstracto es una instancia del patrón Composite.
El patrón [Flyweight](/patrones/comportamiento/flyweight.md) muestra cómo compartir terminales dentro del árbol sintáctico abstracto.
[Iterator](/patrones/comportamiento/iterator.md): el intérprete puede usar un Iterator para recorrer la estructura.
Puede usarse el patrón [Visitor](/patrones/comportamiento/visitor.md) para mantener el comportamiento de cada nodo del árbol sintáctico abstracto de una clase.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Interpreter_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
