# S.O.L.I.D

SOLID es un acrónimo introducido por Robert C. Martin en su libro "Agile Software Development, Principles, Patterns and Practices" [\[48\]](../../recursos.md) y hace referencia a los siguientes cinco principios:

* **S**: _\(SRP - Single responsibility principle\)_ Principio de responsabilidad única.
* **O**: _\(OCP - Open closed principle\)_ Principio abierto cerrado.
* **L**: _\(LSP - Liskov substitution principle\)_ Principio de substitución de Liskov.
* **I**: _\(ISP - Interface segregation principle\)_ Principio de segregación de la interfaz.
* **D**: _\(DIP - Dependency inversion principle\)_ Principio de inversión de la dependencia.

El objetivo de aplicar estos principios es obtener sistemas orientados a objetos con código de mayor calidad, facilidad de mantenimiento y mejores oportunidades de reuso de código.

### Principio de responsabilidad única

> Una clase debe tener una, y sólo una, razón para cambiar, lo que significa que una clase debe tener un solo trabajo.

La primera observación respecto de este principio es que en _Go_ no existen clases. Sin embargo, como vimos mediante la incorporación de comportamientos a tipos de datos, podemos llegar a un concepto equivalente.

Este principio hace foco en que un objeto debe tener únicamente una responsabilidad encapsulada por la clase. Cuando se hace referencia a una responsabilidad es para referirse a una razón para cambiar.  
Mantener una clase que tiene múltiples objetivos o responsabilidades es mucho más complejo que una clase enfocada en una única responsabilidad.

El siguiente ejemplo no cumple con este principio porque otorga a una estructura dos responsabilidades bien diferenciadas: _guardar en un archivo local_ y _guardar en una base de datos_.

```go
package main

type Documento struct {
    Nombre  string
}

func (d *Documento) GuardarEnArchivo() {
   // ...
}

func (d *Documento) GuardarEnBaseDatos() {
   // ...
}
```

[Ejecutar código](https://play.golang.org/p/1d5JvLzQTEH)

Un _Documento_ debería saber cómo acceder al sistema de archivos local y a la vez como conectarse y operar contra una base de datos. Implementar ambas acciones en una misma estructura genera un alto acoplamiento.

Creando estructuras con responsabilidades bien definidas se puede mejorar el código de la siguiente manera:

```go
package model

type Documento struct {
    Nombre  string
}
```

```go
package store

import "model"

type GuardadorDocumento interface {
    Guardar(d model.Documento)
}

type GuardadorDocumentoArchivo struct {
    Path  string
}

func (gda GuardadorDocumentoArchivo) Guardar(d model.Documento) {
   // ...
}

type GuardadorDocumentoBaseDatos struct {
    StringConnection  string
}

func (gdbd GuardadorDocumentoBaseDatos) Guardar(d model.Documento) {
   // ...
}
```

[Ejecutar código](https://play.golang.org/p/nxRPMtLbWP2)

**¿Qué pasa en** _**Go**_**:** Gracias a la organización en paquetes que permite _Go_ es posible crear estructuras, tipos, funciones y métodos empaquetados con propósitos claros y bien definidos.

### Principio abierto cerrado

> Los objetos o entidades deberían estar abiertos para la extensión, pero cerrados para su modificación.

Este principio propone que una entidad esté cerrada, lista para ser usada y estable en su calidad e interfaces, y al mismo tiempo abierta, es decir, que permita extender su comportamiento \(pero sin modificar su código fuente\).

Imaginemos que se requiere cambiar el comportamiento de la siguiente estructura únicamente en uno de sus métodos:

```go
type Animal struct {
    Nombre  string
}

func (a Animal) Caminar() {
    // ...
}

func (a Animal) Saltar() {
    // ...
}
```

[Ejecutar código](https://play.golang.org/p/FP80Iem9qqV)

Podemos hacerlo de la siguiente forma:

```go
type AnimalModificado struct {
    Animal
}

func (am AnimalModificado) Caminar() {
    // ...
}
```

[Ejecutar código](https://play.golang.org/p/Sf1WkRugRN3)

**¿Qué pasa en** _**Go**_**:** Gracias a la composición que permite _Go_ es posible componer tipos simples en más complejos manteniendo la interfaz del tipo original.

### Principio de substitución de Liskov

> Cada clase que herede de otra debe poder utilizarse como su clase padre sin necesidad de conocer las diferencias que pudieran existir entre ellas.

Este principio propone que el contrato de una clase base debe ser honrado por sus clases derivadas para que instancias de las clases derivadas puedan reemplazar a instancias de la clase base.

Veamos el siguiente código:

```go
type RespuestaJSON struct {}

func (r RespuestaJSON) Imprimir() {
    // ...
}

type RespuestaHTML struct {}

func (r RespuestaHTML) Imprimir() {
    // ...
}

type Emision struct {}

func (e Emision) EmitirJSON(r RespuestaJSON) {
    // ...
}

func (e Emision) EmitirHTML(r RespuestaHTML) {
    // ...
}
```

[Ejecutar código](https://play.golang.org/p/4jwdJ0NUjOe)

La estructura _Emision_ debe implementar dos comportamientos, ya que debe poder gestionar impresiones en HTML y JSON. Si a futuro se requiriera de otro tipo de impresión - _xml por ejemplo_ - se debería modificar su código fuente.

La siguiente modificación permite intercambiar cualquier tipo de respuesta para su impresión:

```go
type Respuesta interface {
    Imprimir()
}

type RespuestaJSON struct {}

func (r RespuestaJSON) Imprimir() {
    // ...
}

type RespuestaHTML struct {}

func (r RespuestaHTML) Imprimir() {
    // ...
}

type Emision struct {}

func (e Emision) Emitir(r Respuesta) {
    // ...
}
```

[Ejecutar código](https://play.golang.org/p/ZJ0iEXpWgt4)

**¿Qué pasa en** _**Go**_**:** Al definir firmas de métodos a través de interfaces, y no mediante tipos concretos, es posible utilizar cualquier tipo que respete implícitamente la interfaz.

### Principio de segregación de la interfaz

> Nunca se debe obligar a un cliente a implementar una interfaz que no utilice, o no se debe forzar a los clientes a depender de métodos que no usan.

Este principio hace foco en como deben definirse las interfaces. Las mismas deben ser pequeñas y específicas.  
Grandes y complejas interfaces obligan al cliente a implementar métodos que no necesita.

Veamos la siguiente interface:

```go
type Boton interface {
    OnClick()
    OnDobleClick()
}

type BotonLogin struct {}

func (b BotonLogin) OnClick() {
    // ...
}

func (b BotonLogin) OnDobleClick() {
    // vacio
}
```

[Ejecutar código](https://play.golang.org/p/FHu4-lVUJ2D)

Como puede verse la interface _Boton_ obliga a implementar ambos comportamientos en sus clientes cuando es muy factible que no todos ellos deban implementar ambas opciones.

Una solución podría ser la siguiente:

```go
type OnClickListener interface {
    OnClick()
}

type OnDobleClickListener interface {
    OnDobleClick()
}

type BotonLogin struct {}

func (b BotonLogin) OnClick() {
    // ...
}

type BotonIcono struct {}

func (b BotonIcono) OnDobleClick() {
    // ...
}
```

[Ejecutar código](https://play.golang.org/p/umwCkd0_eKQ)

**¿Qué pasa en** _**Go**_**:** En _Go_ puede aplicarse este concepto aislando el comportamiento requerido utilizando interfaces más pequeñas.

### Principio de inversión de la dependencia

> Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deberían depender de abstracciones.  
> Las abstracciones no deben depender de los detalles. Los detalles deben depender de las abstracciones.

Este principio esta basado en reducir las dependencias entre los módulos del código para atacar el alto acoplamiento.

Veamos la siguiente ejemplo:

```go
type B struct {}

func (b B) Saludar() {
    // ...
}

type A struct {
    B
}
```

[Ejecutar código](https://play.golang.org/p/ANqhCiBv3Zr)

Como puede verse el tipo A depende del tipo B por lo que si el tipo B es modificado afectará al tipo A.

Una solución podría ser la siguiente:

```go
type Saludador interface {
    Saludar()
}

type B struct {}

func (b B) Saludar() {
    // ...
}

type A struct {
    Saludador
}
```

[Ejecutar código](https://play.golang.org/p/pHDUY3VCNTI)

**¿Qué pasa en** _**Go**_**:** Componer tipos mediante interfaces, y no mediante tipos concretos, permite evitar una fuerte dependencia entre tipos.

## Conclusión

Si bien el libro de Robert C. Martin [\[48\]](../../recursos.md) tiene más de una década y media y hace referencia a lenguajes propiamente orientados a objetos, vimos como también pueden aplicarse esos principios en _Go_.

Como se vio en el apartado anterior, el poder de la composición y de las interfaces implícitas le permiten a _Go_ implementar buenas prácticas y conceptos propios de la programación orientada a objetos.



> **Atención**: Esta publicación se encuentra abandonada. Puede acceder a la versión vigente en [https://leanpub.com/designpatternsingo](https://leanpub.com/designpatternsingo)

