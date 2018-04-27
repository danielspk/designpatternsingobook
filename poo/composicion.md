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
Se expresa a la herencia como una relación **es-un/a**.

## Composición:

La composicion es una manera de defiinir obejtos dentro de otros objetos. De esta forma un objeto puede adquirir los comportamientos y datos de los otros objetos por los que esta compuesto.

> Esto en cierta medida es más similar al concepto de herencia múltiple que al de simple.

Se expresa a la composición como una relación **tiene-un/a**.

## ¿Por qué _Go_ no tiene herencia?:

Seguramente no haya una respuesta única. No obstante en el faq de la documentación oficial de _Go_ responden a esta pregunta de la siguiente forma [\[44\]](/recursos.md):

"**¿Por qué no hay herencia?**:
La programación orientada a objetos, al menos en los lenguajes más conocidos, implica demasiada discusión sobre las relaciones entre tipos, relaciones que a menudo podrían derivarse automáticamente. _Go_ toma un enfoque diferente.
En lugar de requerir que el programador declare de antemano que dos tipos están relacionados, en _Go_ un tipo satisface automáticamente cualquier interfaz que especifique un subconjunto de sus métodos. Además de reducir la administración *(la palabra original es bookkeeping)*, este enfoque tiene ventajas reales. Los tipos pueden satisfacer muchas interfaces a la vez, sin las complejidades de la herencia múltiple tradicional. Las interfaces pueden ser muy livianas - una interfaz con uno o incluso cero métodos puede expresar un concepto útil. Las interfaces se pueden agregar tardiamente si aparece una nueva idea o para probarla - sin anotar los tipos originales. Debido a que no existen relaciones explícitas entre los tipos y las interfaces, no hay una jerarquía de tipos para administrar o discutir.
Es posible utilizar estas ideas para construir algo análogo a los type-safe de las pipes de Unix. Por ejemplo, vea cómo _fmt.Fprintf_ permite la impresión formateada de cualquier salida, no solo de un archivo, o cómo el paquete _bufio_ puede estar completamente separado de la E/S, o cómo el paquete _image_ genera archivos de imágenes comprimidas. Todas estas ideas se derivan de una única interfaz (_io.Writer_) que representa un único método (_Write_). Y esto sólo está arañando la superficie. Las interfaces en _Go_ tienen una profunda influencia sobre cómo se estructuran los programas.
Toma un tiempo acostumbrarse, pero este estilo implícito de dependencia de tipos es una de las cosas más productivas sobre _Go_."

## ¿La composición es mejor que la herencia?:

En nuestro rubro existen miles de afirmaciones poco fundadas del estilo _'esto es mejor que aquello'_.
Al incursionar en _Go_ y leer sobre porque no existe la herencia me encontraba con frases del estilo "la herencia es mala", "la herencia simple no alcanza pero la herencia múltiple es aún peor", etc. En más de una oportunidad encontré una referencia a un artículo de JavaWorld [\[45\]](/recursos.md) donde el autor cuenta la siguiente anécdota:

"Una vez asistí a una reunión del grupo de usuarios de Java, donde James Gosling (el inventor de Java) fue el orador principal. Durante la memorable sesión de preguntas y respuestas, alguien le preguntó: 'Si pudieras volver a hacer Java, ¿qué cambiarías?' 'Suprimiría las clases', respondió. Después de que la risa se calmó, explicó que el verdadero problema no eran las clases en sí, sino la herencia de implementación (la relación  extends). La herencia de interfaz (la relación implements) es preferible. Debe evitar la herencia de implementación siempre que sea posible.".

En mi opinión personal no entro en estos temas de que es mejor que otra cosa, simplemente veo que son formas diferentes de extender comportamientos y reutilizar código.

Veamos un pequeño ejemplo en _Java_ - _ya que permite ambas formas_ - con algunos pros y contras - basado del siguiente artículo [\[46\]](/recursos.md):

#### Herencia:

```java
class Fruta {
    public void pelar() {
        System.out.println("Pelando una fruta");
    }
}

class Manzana extends Fruta {
    public void pelar() {
        System.out.println("Pelando una manzana");
    }
}
```

**Pros:**
- **Reutilización de código:** todo código definido en la clase Fruta puede ser reutilizado por cualquiera de sus subclases.
- **Polimorfismo:** una variable de tipo Fruta puede contener una referencia a un objeto de tipo superclase o cualquiera de sus subclases.
- **Enlace dinámico:** en tiempo de ejecución se decidirá que método invocar en función del tipo de clase del objeto.
- **Facilidad para agregar una nueva subclase:** simplemente se debe agregar una subclase que heredé de la superclase.

**Contras:**
- **Equipaje adicional:** se heredan todos los métodos y propiedades de la superclase aunque no se deseen todos ellos.
- **Alto Acoplamiento:** La subclase y superclase están fuertemente conectadas. Un cambio en la superclase puede impactar negativamente en la subclase.
- **Débil Encapsulamiento**: si cambia la firma de un método en la superclase, hasta que la subclase no lo modifique el código no funcionará/compilará.

#### Composición:

```java
class Fruta {
    public void pelar() {
        System.out.println("Pelando una fruta");
    }
}

class Manzana {
    private Fruta fruta = new Fruta();
    
    public void pelar() {
        fruta.pelar();
    }
}
```

**Pros:**
- **Bajo Acoplamiento:** Cualquier cambio en la clase Fruta no afecta a la clase Manzana. Incluso si se agrega un método en la clase Fruta con la misma firma de uno de la clase Manzana no afecta a ésta última.
- **Reutilización de Código:** Se puede lograr de igual forma que con la herencia, aunque hay que llamar explicitamente al código que necesita ser reutilizado (**Nota:** esto último no es necesario en _Go_ **@TODO: validar!!!**).
- **Encapsulación más fuerte:** en el ejemplo, si se cambia la firma del método pelar() en la clase Fruta, no hay necesidad de cambiar nada en la clase Manzana.

**Contras:**
- **Es más dificil agregar una nueva clase:** sintácticamente requiere de más código.
- **Costo de rendimiento:** el método explicito de reenvío de llamadas tiene un costo de rendimiento en comparación con la invocación directa de la herencia.

## Ejemplo de Composición en _Go_:

```go
import
```

**Contenido en desarrollo.**

## Conclusión:

El uso de interfaces (_es-un_) y de la composición (_tiene-un_) posibilitan la reutilización de código en _Go_ y la adopción de técnicas y de patrones orientados a objetos.
