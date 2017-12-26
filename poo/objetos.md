# Objetos en Go

A diferencia de otros lenguajes orientados a objetos como _C++_, _Java_, _C\#_, _Python_ y _PHP_, entre otros, en _Go_ no hay clases, ni objetos, ni excepciones, ni herencia.

Rápidamente se podría inferir en que _Go_ no es un lenguaje orientado a objetos. ¿Cómo puede existir un lenguaje orientado a objetos que no disponga de clases?. La pregunta que realmente debemos hacernos es: _**¿Qué es la programación orientada a objetos?**_.

Los desarrolladores tenemos una tendencia natural a comprar las cosas. Entonces porque actualmente _Java_ es el rey indiscutido de la programación orientado a objetos, y éste lenguaje tiene entre otras características clases y herencia; si _Go_ no las tiene entonces no puede ser un lenguaje orientado a objetos.

_¿Alguien alguna vez escucho decir que _Javascript_ es un lenguaje orientado a objetos?_. Existe una gran discución sobre si lo es o no - a fin de cuentas en _Javascript_ tampoco hay clases ni herencia de la forma clásica como la que las hay en _Java_. _Javascript_ suele ser considerado un lenguaje orientado a objetos. _¿Porqué?_. Porque permite implementar ciertas características de la programación orientada a objetos.

> En ES6 se incorporan las clases en Javascript aunque con un soporte muy limitado en comparación con otros lenguajes orientados a objetos clásicos.

Al analizar a _Go_, debemos comparar que características de la programación orientada a objetos se pueden implementar y no simplemente hacer una comparación de un lenguaje respecto del otro.

## Cómo es la POO en Go:

### Objetos:

En _Go_ no existen clases ni objetos. Existen estructuras que son tipos de datos definidos por el usuario que pueden incorporar comportamientos. En una analogía con una clase, las propiedades pudieran ser los tipos de datos de la estructura, y los métodos las funciones asociadas a la estructura.

Ejemplo:

```go
type Persona struct {
    Nombre   string
    Apellido string
    Edad     int
}

func (p *Persona) Saludar() {
   fmt.Printf("Nombre: %s, Apellido: %s, Edad: %d\n", p.Nombre, p.Apellido, p.Edad)
}
```

[Ejecutar código](https://play.golang.org/p/3uoR7qRs9eV)

### Herencia:

En _Go_ tampoco existe la herencia. Se pueden componer estructuras con otras estructuras - _más información en el siguiente apartado - [link](composicion.md)_

Ejemplo:

```go

```

**Contenido en desarrollo.**

## Qué dicen otros autores:

Según Gigi Sayfan [\[4\]](recursos.md) "Go es una extraña mezcla de ideas antiguas y nuevas.", y "Muchas personas ni siquiera están seguras de si Go es un lenguaje orientado a objetos", sin embargo para el "Go es un lenguaje de programación orientado a objetos de buena fe. Permite el modelado basado en objetos y promueve las mejores prácticas de usar interfaces en lugar de tipos concretos de jerarquías. Go tiene algunas elecciones sintácticas inusuales, pero el trabajo general con tipos, métodos e interfaces parece simple, ligero y natural. La incrustración no es muy pura, pero aparentemente estaba en juego el pragmatismo, y se proporcionó una incrustración en lugar de sólo la composición por nombre".

**Contenido en desarrollo.**

## Mi conclusión:

Ya que existen otros lenguajes que permiten programar orientado a objetos sin ser realmente orientados a objetos puedo decir que **"**_**Go**_** es un lenguaje no orientado a objetos, que permite que permite la programación orientado a objetos - **_**aunque no de la forma tradicional**_**"**.

