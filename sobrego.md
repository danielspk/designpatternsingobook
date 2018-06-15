# Sobre Go

![](/assets/appenginegopher.jpg)

> Imagen - [\[38\]](recursos.md)

"Go es un lenguaje de programación de código abierto que facilita la creación de software simple, confiable y eficiente". [\[1\]](recursos.md)

"Go es expresivo, conciso, limpio y eficiente. Sus mecanismos de concurrencia facilitan la escritura de programas que aprovechan al máximo las máquinas multinúcleo, y de red, mientras que su novedoso sistema de tipo permite la construcción de programas flexibles y modulares. Go compila rápidamente el código de máquina y tiene la comodidad de la recolección de basura y el poder de la reflexión en tiempo de ejecución. Es un lenguaje compilado, rápido, de tipado estático, que se siente como un lenguaje interpretado de tipado dinámico". [\[2\]](recursos.md)

## Origenes

_Go_ fue creado en Google en el año 2007 por _Robert Griesemer_, _Rob Pike_, y _Ken Thomson_.

![](/assets/gopher.png)

> Imagen - [\[39\]](recursos.md)

Su lanzamiento oficial fue en noviembre del año 2009, pero su primera versión estable se publicó en marzo de 2012.

## Características

_Go_ esta inspirado en la sintaxis de _C_ como otros lenguajes: _C++_, _C#_, _Java_, _PHP_, _Javascript_, etc. Por sus características suele clasificarse como un lenguaje compilado que tiene carcaterísticas de lenguajes interpretados.

![](/assets/contreras/govsother.png)

> Imagen - [\[16\]](recursos.md)

Según palabras de uno de sus creadores, _Rob Pike_: "Go es un intento de combinar la seguridad y el rendimiento de un lenguaje de tipado estático con la expresividad y la comodidad de un lenguaje interpretado de tipo dinámico." [\[16\]](recursos.md)

_Go_ se caracteriza por ser un lenguaje:

* Compilado
* Tipado estático
* Diseño minimalista
* Facilidad de aprendizaje
* Uso de punteros - _sin aritmética_
* Concurrente
* Rápido
* Recolección de basura
* Permite la programación orientada a objetos - _pero ¿es orientado a objetos?_

### Ejemplo

```go
package main

import "fmt"

func main() {
    fmt.Println("www.designpatternsingo.com")
}
```

[Ejecutar código](https://play.golang.org/p/vhgR-fZxZv6)

### Según otros autores

Para Mark Summerfield [\[27\]](recursos.md) "Go es bastante parecido a C en su espíritu, ya que es un lenguaje pequeño y eficiente con convenientes facilidades de bajo nivel, como punteros. Sin embargo, Go también ofrece muchas características asociadas con lenguajes de alto o muy alto nivel, como cadenas Unicode, potentes estructuras de datos integradas, duck typing, recolección de basura y soporte de concurrencia de alto nivel que utiliza comunicaciones en lugar de datos compartidos y bloqueos. Go también tiene una gran biblioteca estándar de amplio rango".

**Contenido en desarrollo.**

## Controversias

_Go_ como todos los lenguajes de programación presenta ciertas controversias. Sus detractores por ejemplo manifiestan que el lenguaje no tiene:
- genericos
- excepciones
-

No obstante los desarrolladores de _Go_ no son ajenos a estas críticas, y permiten que se propongan nuevas funcionalidades. Para esto se deben completar una serie de pasos que se encuentran documentados en el siguiente link: [https://github.com/golang/proposal](https://github.com/golang/proposal).

_Go_ trata de respetar su filosofía de mantener un lenguage extremadamente simple y rápido de compilar, por lo que la incorporación de nuevas características que pudieran afectar a uno de estos dos puntos debe poder justificarse claramente, y no debe existir forma alguna de poder llevar a cabo esa tarea con las características actuales del lenguage. Por ejemplo en el blog oficial de _Go_ explican de esta manera porque no existen las excepciones en el lenguage:

"En _Go_, el manejo de errores es importante. El diseño y las convenciones del idioma lo alientan a verificar explícitamente si ocurren errores (a diferencia de la convención en otros idiomas de arrojar excepciones y, a veces, capturarlas). En algunos casos, esto hace que código de _Go_ sea verboso, pero afortunadamente hay algunas técnicas que puede utilizar para minimizar el manejo de errores repetitivos."

Esta filosofía controvertida es la que creo en mi opinión que hace al lenguage tan interesante. En vez incorporar constantemente nuevas características y/o copiar otras de otros lenguajes de programación, _Go_ intenta mantener un lenguage simple, mínimo y conciso.
