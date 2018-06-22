# Patrones Creacionales

![](/assets/doc.png)

> Imagen - [\[38\]](/recursos.md)

"Los patrones de diseño de creación abstraen el proceso de creación de instancias. Ayudan a hacer un sistema independiente de cómo se crean, se componen y se representan sus objetos. Un patrón de creación de clases usa la herencia para cambiar la clase de la instancia a crear, mientras que un patrón de creación de objetos delega la creación de la instancia en otro objeto." [\[29\]](/recursos.md)

Esta definición de Gamma es un desafio de representar en _Go_ ya que como hemos visto no existen ni las *clases*, ni los *objetos* y ni la *herencia*. Sin embargo veremos como todo encaja en su lugar en cada patrón y cómo pueden implementarse en _Go_.

### Concurrencia

_Go_ es un lenguaje que permite la programación concurrente y los patrones de diseño creacionales asumen que se trabaja sobre un único hilo de ejecución. De ser requerido se analizará que implicancias tiene la concurrencia en dicho patrón.

## Contenido

* [Singleton](singleton.md)
* [Builder](builder.md)
* [Factory Method](factorymethod.md)
* [Abstract Factory](abstractfactory.md)
* [Prototype](prototype.md)
