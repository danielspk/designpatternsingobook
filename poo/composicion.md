# Herencia vs Composición en Go

Como se indicó previamente en _Go_ no existe el concepto de herencia típico de lenguajes orientados a objetos como _Java_, _C++_ y _Smalltalk_ entre otros.

En _Go_ existe otro concepto complementario que es la **composición**.

Tal como menciona Steve Francia [\[6\]](/recursos.md) "Existen varios enfoques diferentes para definir relaciones entre objetos. Si bien difieren bastante entre sí, todos comparten un propósito común como mecanismo para la reutilización de código":

- Herencia
- Herencia múltiple
- Polimorfismo
- Composición de objetos

## Herencia:

Es el mecanismo por el que un objeto se basa en otro y justamente por esto hereda los comportamientos y los datos de el. No todos los lenguajes de programación implementan la herencia de la misma mandera. Algunos sólo permiten heredar de un único objeto, esto se denomina _herencia simple_; mientras otros permiten heredar de varios objetos y a esto se lo denomina _herencia múltiple_.
Asimismo los comportamientos y datos heredados pueden estar limitados al acceso con el que el objeto padre los definió, esto se denomina _visibilidad_.

## Composición:

La composicion es una manera de defiinir obejtos dentro de otros objetos. De esta forma un objeto puede adquirir los comportamientos y datos de los otros objetos por los que esta compuesto.

> Esto en cierta medida es más similar al concepto de herencia múltiple que al de simple.

## ¿Por qué _Go_ no tiene herencia?

Seguramente no haya una respuesta única. No obstante en el faq de la documentación oficial de _Go_ responden a esta pregunta de la siguiente forma [\[44\]](/recursos.md):

"**¿Por qué no hay herencia de tipo?**:

"

**Contenido en desarrollo.**
