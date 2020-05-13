# Herencia / Composición

Como se indicó previamente en _Go_ no existe el concepto de herencia de implementación típico de lenguajes orientados a objetos como _Java_, _C++_ y _Smalltalk_ entre otros.

En _Go_ existe otro concepto complementario que es la **composición**.

Tal como menciona Steve Francia [\[6\]](../../recursos.md) "Existen varios enfoques diferentes para definir relaciones entre objetos. Si bien difieren bastante entre sí, todos comparten un propósito común como mecanismo para la reutilización de código":

* Herencia
* Herencia múltiple
* Polimorfismo
* Composición de objetos

## Herencia

La herencia se puede puede expresar de dos maneras: _herencia de clases_ y _herencia de interfaces_. "La herencia de clases define la implementación de un objeto en términos de la implementación de otro objeto. En resumen, es un mecanismo para compartir código y representación. Por el contrario, la herencia de interfaces _\(o subtipado\)_ describe cuándo se puede usar un objeto en el lugar de otro." [\[29\]](../../recursos.md)  
No todos los lenguajes de programación implementan la herencia de la misma manera. En algunos lenguajes la herencia de clases y la de interfaces existen como un mismo mecanismo \(_Eiffel_ por ejemplo\), mientras que en otros están separados \(_Java_ por ejemplo\). Algunos sólo permiten heredar de un único objeto, esto se denomina _herencia simple_; mientras otros permiten heredar de varios objetos y a esto se lo denomina _herencia múltiple_.  
Asimismo los comportamientos y datos heredados pueden estar limitados al acceso con el que el objeto padre los definió, esto se denomina _visibilidad_.

Se expresa a la herencia como una relación **es-un/a**.

## Composición

La composicion es una manera de definir objetos dentro de otros objetos. De esta forma un objeto puede adquirir los comportamientos y datos de los otros objetos por los que esta compuesto.

> Esto en cierta medida es más similar al concepto de herencia múltiple que al de simple.

Se expresa a la composición como una relación **tiene-un/a**.

## ¿Por qué _Go_ no tiene herencia?

Seguramente no haya una respuesta única. No obstante en el _faq_ de la documentación oficial de _Go_ responden a esta pregunta de la siguiente forma [\[44\]](../../recursos.md):

"**¿Por qué no hay herencia?**:  
La programación orientada a objetos, al menos en los lenguajes más conocidos, implica demasiada discusión sobre las relaciones entre tipos, relaciones que a menudo podrían derivarse automáticamente. _Go_ toma un enfoque diferente.  
En lugar de requerir que el programador declare de antemano que dos tipos están relacionados, en _Go_ un tipo satisface automáticamente cualquier interfaz que especifique un subconjunto de sus métodos. Además de reducir la administración _\(la palabra original es bookkeeping\)_, este enfoque tiene ventajas reales. Los tipos pueden satisfacer muchas interfaces a la vez, sin las complejidades de la herencia múltiple tradicional. Las interfaces pueden ser muy livianas - una interfaz con uno o incluso cero métodos puede expresar un concepto útil. Las interfaces se pueden agregar tardiamente si aparece una nueva idea o para probarla - sin anotar los tipos originales. Debido a que no existen relaciones explícitas entre los tipos y las interfaces, no hay una jerarquía de tipos para administrar o discutir.  
Es posible utilizar estas ideas para construir algo análogo a los type-safe de las pipes de Unix. Por ejemplo, vea cómo _fmt.Fprintf_ permite la impresión formateada de cualquier salida, no solo de un archivo, o cómo el paquete _bufio_ puede estar completamente separado de la E/S, o cómo el paquete _image_ genera archivos de imágenes comprimidas. Todas estas ideas se derivan de una única interfaz \(_io.Writer_\) que representa un único método \(_Write_\). Y esto sólo está arañando la superficie. Las interfaces en _Go_ tienen una profunda influencia sobre cómo se estructuran los programas.  
Toma un tiempo acostumbrarse, pero este estilo implícito de dependencia de tipos es una de las cosas más productivas sobre _Go_."

## ¿La composición es mejor que la herencia?

En la comunidad de práctica de desarrollo de software existen miles de afirmaciones poco fundadas del estilo _'esto es mejor que aquello'_.  
Al incursionar en _Go_ y leer sobre por qué no existe la herencia me encontraba con frases del estilo "la herencia es mala", "la herencia simple no alcanza pero la herencia múltiple es aún peor", etc. En más de una oportunidad encontré una referencia a un artículo de JavaWorld [\[45\]](../../recursos.md) donde el autor cuenta la siguiente anécdota:

"Una vez asistí a una reunión del grupo de usuarios de Java, donde James Gosling \(el inventor de Java\) fue el orador principal. Durante la memorable sesión de preguntas y respuestas, alguien le preguntó: 'Si pudieras volver a hacer Java, ¿qué cambiarías?' 'Suprimiría las clases', respondió. Después de que la risa se calmó, explicó que el verdadero problema no eran las clases en sí, sino la herencia de implementación \(la relación extends\). La herencia de interfaz \(la relación implements\) es preferible. Debe evitar la herencia de implementación siempre que sea posible.".

Veamos un pequeño ejemplo en _Java_ - _ya que permite ambas formas_ - con algunos pros y contras - basado en el siguiente artículo [\[46\]](../../recursos.md):

### Herencia

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

* **Reutilización de código:** todo código definido en la clase _Fruta_ puede ser reutilizado por cualquiera de sus subclases.
* **Polimorfismo:** una variable de tipo Fruta puede contener una referencia a un objeto de tipo superclase o cualquiera de sus subclases.
* **Enlace dinámico:** en tiempo de ejecución se decidirá que método invocar en función del tipo de clase del objeto.
* **Facilidad para agregar una nueva subclase:** simplemente se debe agregar una subclase que heredé de la superclase.

**Contras:**

* **Equipaje adicional:** se heredan todos los métodos y propiedades de la superclase aunque no se deseen todos ellos.
* **Alto Acoplamiento:** La subclase y superclase están fuertemente conectadas. Un cambio en la superclase puede impactar negativamente en la subclase.
* **Débil Encapsulamiento**: si cambia la firma de un método en la superclase, hasta que la subclase no lo modifique el código no funcionará/compilará.

### Composición

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

* **Bajo Acoplamiento:** Cualquier cambio en la clase _Fruta_ no afecta a la clase _Manzana_. Incluso si se agrega un método en la clase _Fruta_ con la misma firma de uno de la clase Manzana no afecta a ésta última.
* **Reutilización de Código:** Se puede lograr de igual forma que con la herencia, aunque hay que llamar explícitamente al código que necesita ser reutilizado \(**Nota:** esto último no es necesario en _Go_\).
* **Encapsulamiento más fuerte:** en el ejemplo, si se cambia la firma del método _pelar\(\)_ en la clase _Fruta_, no hay necesidad de cambiar nada en la clase _Manzana_.

**Contras:**

* **Es más difícil agregar una nueva clase:** sintácticamente requiere de más código.
* **Costo de rendimiento:** el método explícito de reenvío de llamadas tiene un costo de rendimiento en comparación con la invocación directa de la herencia.

## Ejemplo de Composición en _Go_

Como veremos la composición en _Go_ se logra embebiendo tipos de datos unos dentro de otros:

```go
type Usuario struct {
    nombre   string
    apellido string
}

func (u Usuario) getDatosPersonales() string {
    return fmt.Sprintf("%s, %s", u.nombre, u.apellido);
}

type Administrador struct {
    *Usuario
    sector string
}

func (a Administrador) getDatosCompletos() string {
    return fmt.Sprintf("%s - %s", a.getDatosPersonales(), a.sector);
}

func main() {
    var administrador = Administrador{&Usuario{"Jose", "Luis"}, "Computos"};

    fmt.Println(administrador.getDatosPersonales());
    fmt.Println(administrador.getDatosCompletos());
}
```

[Ejecutar código](https://play.golang.org/p/7W89468lRhC)

## Composición e interfaces en _Go_

```go
type Primate interface {
    Alimentar(string)
}

type Antropoide struct {}

func (t Antropoide) Alimentar(fruta string) {
   fmt.Printf("Comiendo %s", fruta)
}

type Gorila struct {
    Antropoide    
}

func DarDeComer(primate Primate) {
    primate.Alimentar("banana")
}

kong := Gorila{}
DarDeComer(kong)
```

[Ejecutar código](https://play.golang.org/p/tZhaQwcvez9)

Como se puede observar la función _DarDeComer\(\)_ espera una variable de tipo _Primate_ pero se le pasa una de tipo _Gorila_. Como el tipo _Gorila_ se compone de un _Antropoide_ que implementa el método _Alimentar\(\)_ implícitamente también es un _Primate_.

## ¿Cómo afecta esto a la implementación de los Patrones de Diseño GoF?

Como se detallará más adelante, en la implementación de cada patrón de diseño, la falta de herencia será suplida de dos formas diferentes y/o complementarias:

* la composición cuando exista un comportamiento que deba ser compartido entre tipos de datos
* mediante interfaces cuando se deba asegurar que una estructura es parte de una relación **es-un** y/o requiera implementar ciertos comportamientos.

Estrictamente hablando de programación orientada a objetos, la mayor dificultad encontrada es cuando una _clase abstracta_ implementa un _método concreto_ con comportamiento que llama a _métodos abstractos_ también definidos en dicha _clase abstracta_ que luego serán implementados en las _clases hijas_.  
Para emular este comportamiento la estrategia utilizada en esta publicación será pasar como un argumento del _método concreto_ de la _clase abstracta_ una referencia de una _interface_ que exponga cúales serán los _métodos abstractos_ que serán implementados por las _clases hijas_ que implementen esa _interface_.

Veamos un ejemplo para entender la estrategia:

#### Problema a resolver - código _Java_

```java
abstract class ClaseAbstracta {
    public void metodoConcreto() {
        this.metodoAbstracto();
    }

    abstract public void metodoAbstracto();
}

class ClaseHija extends ClaseAbstracta {
    @Override
    public void metodoAbstracto() {
        System.out.println("Soy metodo abstracto");
    }
}
```

#### Estrategia implementada en _Go_

```go
type InterfaceMetodosAbstractos interface {
    MetodoAbstracto()
}

type ClaseAbstracta struct{}

func (ca *ClaseAbstracta) MetodoConcreto(self *InterfaceMetodosAbstractos) {
    self.MetodoAbstracto()
}

type ClaseHija struct {
    *ClaseAbstracta
}

func (ch *ClaseHija) MetodoAbstracto() {
    fmt.Println("Soy metodo abstracto")
}

claseHija := &ClaseHija{&ClaseAbstracta{}}
claseHija.MetodoConcreto(&claseHija)
```

[Ejecutar código](https://play.golang.org/p/NnEeU5Z4XWI)

> Puede verse el uso de esta estrategia en el patrón [Template Method](../../parte2/patrones/comportamiento/templatemethod.md).

## Conclusión

_Go_ permite la _composición_ y la _herencia de interfaz_. El uso de interfaces \(_es-un_\) y de la composición \(_tiene-un_\) posibilitan la reutilización de código en _Go_ y la adopción de técnicas y de patrones orientados a objetos.

