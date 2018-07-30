# Patrón Interpreter

## Propósito

Dado un lenguaje, define una representación de su gramática junto con un intérprete que usa dicha representación para interpretar sentencias del lenguaje.

## Aplicabilidad

Úsese el patrón Interpreter cuando hay un lenguaje que interpretar y se pueden representar las sentencias del lenguaje como árboles de sintácticos abstractos. El patrón Interpreter funciona mejor cuando la gramática es simple. Para gramáticas complejas, la jerarquía de estructuras de la gramática se vuelve grande e inmanejable. Herramientas como los generadores de analizadores sintácticos constituyen una alternativa mejor en estos casos. Éstas pueden interpretar expresiones sin necesidad de construir árboles sintácticos abstractos, lo que puede ahorrar espacio y, posiblemente, tiempo.
La eficiencia no es una preocupación crítica. Los intérpretes más eficientes normalmente no se implementan interpretando árboles de análisis sintáctico directamente, sino que primero los traducen en algún otro formato. Por ejemplo, las expresiones regulares suelen transformarse en máquinas de estados. Pero incluso en ese caso, el _traductor_ puede implementarse con el patrón Interpreter, de modo que éste sigue siendo aplicable.

## Estructura

![](/assets/uml/interpreter.png)

## Participantes

**Contenido en desarrollo.**

## Colaboradores

**Contenido en desarrollo.**

## Implementación

**Contenido en desarrollo.**

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

**Contenido en desarrollo.**

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Interpreter_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
