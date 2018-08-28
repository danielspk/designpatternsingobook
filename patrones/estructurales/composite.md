# Patrón Composite

## Propósito

Compone estructuras con estado en jerarquías de árbol para representar jerarquías de parte-todo. Permite que los clientes traten de manera uniforme a las estructuras con estado individuales y a las compuestas.

## Aplicabilidad

Úsese el patrón Composite cuando:
* quiera representar jerarquías de estructuras con estado parte-todo.
* quiera que los clientes sean capaces de obviar las diferencias entre composiciones de estructuras con estados y las estructuras con estado individuales. Los clientes tratarán a todas las estructuras con estado de la jerarquía compuesta de manera uniforme.

## Estructura

![](/assets/uml/composite.png)

## Participantes

* **Componente:**
  * declara la interfaz de las estructuras con estado de la composición.
  * implementa el comportamiento predeterminado de la interfaz que es común a todas las estructuras.
  * declara una interfaz para acceder a sus componentes hijos y gestionarlos.
  * _(opcional)_ define una interfaz para acceder al padre de un componente en la jerarquía recursiva y, si es necesario, la implementa.
* **Hoja:**
  * representa estructuras con estado hoja en la composición. Una hoja no tiene hijos.
  * define el comportamiento de las estructuras con estado primitivas de la composición.
* **Compuesto:**
  * define el comportamiento de los componentes que tienen hijos.
  * almacena componentes hijos.
  * implementa las operaciones de la interfaz Componente relacionadas con los hijos.
* **Cliente:**
  * manipula estructuras con estado en la composición a través de la interfaz Componente.

## Colaboradores

Los Clientes usan la interfaz de la estructura Componente para interactuar con las estructuras con estado de la jerarquía compuesta. Si el recipiente es una Hoja, la petición se trata correctamente. Si es un Compuesto, normalmente redirige las peticiones a sus componentes hijos, posiblemente realizando operaciones adicionales antes o después.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

Muchas veces se usa el enlace al componente padre para implementar el patrón [Chain of Responsability](/patrones/comportamiento/chainofresponsability.md).
El patrón [Decorator](/patrones/estructurales/decorator.md) suele usarse junto con el Composite. Cuando se usan juntos decoradores y compuestos, normalmente ambos tendrán una estructura común. Por tanto, los decoradores tendrán que admitir la interfaz Componente con operaciones de añadir, eliminar y obtenerHijo.
El patrón [Flyweight](/patrones/estructurales/flyweight.md) permite compartir componentes, si bien en ese caso éstos ya no pueden referirse a sus padres.
Se puede usar el patrón [Iterator](/patrones/comportamiento/iterator.md) para recorrer las estructuras definidas por el patrón Composite.
El patrón [Visitor](/patrones/comportamiento/visitor.md) localiza operaciones y comportamiento que de otro modo estaría distribuido en estructuras Compuesto y Hoja.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Composite_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
