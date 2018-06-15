# Sobre Go

![](/assets/appenginegopher.jpg)

> Imagen - [\[38\]](recursos.md)

"Go es un lenguaje de programación de código abierto que facilita la creación de software simple, confiable y eficiente". [\[1\]](recursos.md)

"Go es expresivo, conciso, limpio y eficiente. Sus mecanismos de concurrencia facilitan la escritura de programas que aprovechan al máximo las máquinas multinúcleo, y de red, mientras que su novedoso sistema de tipo permite la construcción de programas flexibles y modulares. Go compila rápidamente el código de máquina y tiene la comodidad de la recolección de basura y el poder de la reflexión en tiempo de ejecución. Es un lenguaje compilado, rápido, de tipado estático, que se siente como un lenguaje interpretado de tipado dinámico". [\[2\]](recursos.md)

## Orígenes

_Go_ fue creado en Google en el año 2007 por _Robert Griesemer_, _Rob Pike_, y _Ken Thomson_. _Go_ también es conocido como _Golang_.

![](/assets/gopher.png)

> Imagen - [\[39\]](recursos.md)

Su lanzamiento oficial fue en noviembre del año 2009, pero su primera versión estable - 1.0- se publicó en marzo de 2012.

## Características

_Go_ esta inspirado en la sintaxis de _C_ como otros lenguajes: _C++_, _C#_, _Java_, _PHP_, _Javascript_, etc. Por sus características suele clasificarse como un lenguaje compilado que tiene características de lenguajes interpretados.

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

Para Mark Summerfield [\[27\]](recursos.md) "_Go_ es bastante parecido a C en su espíritu, ya que es un lenguaje pequeño y eficiente con convenientes facilidades de bajo nivel, como punteros. Sin embargo, _Go_ también ofrece muchas características asociadas con lenguajes de alto o muy alto nivel, como cadenas Unicode, potentes estructuras de datos integradas, duck typing, recolección de basura y soporte de concurrencia de alto nivel que utiliza comunicaciones en lugar de datos compartidos y bloqueos. _Go_ también tiene una gran biblioteca estándar de amplio rango".

Para Shiju Varghese [\[19\]](recursos.md) "El lenguaje de programación _Go_ se puede describir simplemente en tres palabras: simple, mínimo y pragmático.
El objetivo del diseño de _Go_ es ser un lenguaje de programación simple, minimalista y expresivo que proporcione todas las características esenciales para crear sistemas de software confiables y eficientes. Cada idioma tiene su propio objetivo de diseño y una filosofía única. La simplicidad no se puede agregar más adelante en el idioma, por lo que debe ser construida con la simplicidad en mente. _Go_ está diseñado para ser simple. Al combinar la simplicidad y el pragmatismo de _Go_, puede construir sistemas de software altamente eficientes con un mayor nivel de productividad".

Para Karl Seguin [\[11\]](recursos.md) "_Go_ tiene la naturaleza de simplificar la complejidad que hemos visto incluida en los lenguajes de programación en el último par de décadas mediante el uso de varios mecanismos".



## Controversias

_Go_ como todos los lenguajes de programación presenta ciertas controversias. Sus detractores por ejemplo manifiestan que el lenguaje no tiene:
- genéricos
- excepciones
- sobrecarga de operadores
- etc [\[51\]](recursos.md)

No obstante los desarrolladores de _Go_ no son ajenos a estas críticas, y permiten que se propongan nuevas funcionalidades. Para esto se deben completar una serie de pasos que se encuentran documentados en el siguiente link: [https://github.com/golang/proposal](https://github.com/golang/proposal).

_Go_ trata de respetar su filosofía de mantener un lenguaje extremadamente simple y rápido de compilar, por lo que la incorporación de nuevas características que pudieran afectar a uno de estos dos puntos debe poder justificarse claramente, y no debe existir forma alguna de poder llevar a cabo esa tarea con las características actuales del lenguaje. Por ejemplo estas son algunas respuesta que la documentación de _Go_ por la que no existen las excepciones:

"En _Go_, el manejo de errores es importante. El diseño y las convenciones del idioma lo alientan a verificar explícitamente si ocurren errores (a diferencia de la convención en otros idiomas de arrojar excepciones y, a veces, capturarlas). En algunos casos, esto hace que código de _Go_ sea verboso, pero afortunadamente hay algunas técnicas que puede utilizar para minimizar el manejo de errores repetitivos." [\[50\]](recursos.md)

"Creemos que acoplar excepciones a una estructura de control como en el try-catch-finally, da como resultado un código intrincado. También tiende a alentar a los programadores a etiquetar demasiados errores comunes, como no abrir un archivo, como excepcionales.
_Go_ toma un enfoque diferente. Para el manejo simple de errores, los retornos multi-valor de _Go_ facilitan el reporte de un error sin sobrecargar el valor de retorno. Un tipo de error canónico, junto con otras características de _Go_, hace que el manejo de errores sea agradable, pero bastante diferente del de otros lenguajes." [\[44\]](recursos.md)

Esta filosofía para algunos controvertida es la que creo en mi opinión que hace a _Go_ tan interesante. En vez incorporar constantemente nuevas características y/o copiar otras de otros lenguajes de programación, _Go_ intenta mantener un lenguaje simple, mínimo y conciso.
