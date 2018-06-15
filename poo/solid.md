# Principios S.O.L.I.D. en Go

SOLID es un acrónimo introducido por Robert C. Martin en su libro "Agile Software Development, Principles, Patterns and Practices" [\[48\]](/recursos.md) y hace referencia a los siguientes cinco principios:

- **S**: *(SRP - Single responsibility principle)* Principio de responsabilidad única.
- **O**: *(OCP - Open closed principle)* Principio de abierto cerrado.
- **L**: *(LSP - Liskov substitution principle)* Principio de substitución de Liskov.
- **I**: *(ISP - Interface segregation principle)* Principio de segregación de la interfaz.
- **D**: *(DIP - Dependency inversion principle)* Principio de inversión de la dependencia.

El objetivo de aplicar estos principios es objtener sistemas orientados a objetos con código de mayor calidad, facilidad es su mantenimiento y un buen rehuso de código.

### Principio de responsabilidad única

> Una clase debe tener una, y sólo una, razón para cambiar, lo que significa que una clase debe tener un solo trabajo.

**Contenido en desarrollo.**

Gracias a la organización en paquetes que permite _Go_ es posible crear estructuras, tipos, funciones y métodos empaquetados con propositos claros y bien definidos.

### Principio de abierto cerrado

> Los objetos o entidades deberían estar abiertos para la extensión, pero cerrados para su modificación.

**Contenido en desarrollo.**

Gracias a la composición que permite _Go_ es posible componer tipos simples en más complejos.

### Principio de substitución de Liskov

> Los subtipos deben poder ser sustituidos por su tipo base.

**Contenido en desarrollo.**

Gracias al modo de intefaces que permite _Go_ es factible expresar las dependencias entre paquetes a traves de interfaces y no tipos concretos.

### Principio de segregación de la interfaz

> Nunca se debe obligar a un cliente a implementar una interfaz que no utilice, o no se debe forzar a los clientes a depender de métodos que no usan.

**Contenido en desarrollo.**

En _Go_ puede aplicarse este concepto asilando el comportamiento requerido para que una función haga su trabajo.

### Principio de inversión de la dependencia

> Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deberían depender de abstracciones.
Las abstracciones no deben depender de los detalles. Los detalles deben depender de las abstracciones. 

**Contenido en desarrollo.**

La forma en la que compila _Go_ valida que este principio se cumpla. Caso contrario el programa no podría compilar.

## Conclusión

Si bien el libro de Robert C. Martin [\[48\]](/recursos.md) tiene más de una decada y media y hace referencia a lenguajes propiamente orientados a objetos, vimos como también pueden aplicarse esos principios en _Go_.

Como se vio en el apartado anterior, el poder de la composición y de las interfaces implícitas le permiten a _Go_ implementar prácticas y conceptos propios de la programación orientada a objetos.
