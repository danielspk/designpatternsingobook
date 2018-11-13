# Patrón Flyweight

## Propósito

Usa comportamiento para permitir un gran número de estructuras con estado de grano fino de forma eficiente.

## Aplicabilidad

Úsese el patrón Flyweight cuando se cumpla _todo_ lo siguiente:
* una aplicación utiliza un gran número de estructuras con estado.
* los costos de almacenamiento son elevados debido a la gran cantidad de estructuras con estado.
* la mayor parte del estado de la estructura con estado puede hacerse extrínseco.
* muchos grupos de estructuras con estado pueden reemplazarse por relaticamente pocas estructuras con estado compartidas, una vez que se ha eliminado el estado extrínseco.
* la aplicación no depende de la identidad de una estructura con estado. Puesto que las estructuras con estado flyweight pueden ser compartidas, las comprobaciones de identidad devolverán verdadero para estructuras con estado conceptualmente distintas.

## Estructura

![](/assets/uml/flyweight.png)

## Participantes

* **Flyweight:**
  * declara una interfaz a travéz de la cual los flyweight concretos pueden recibir un estado extrínseco y actuar sobre él.
* **FlyweightConcreto:**
  * implementa la interfaz Flyweight y permite almacenar el estado intrínseco, en caso de que lo haya. Una estructura con estado FlyweightConcreto debe poder ser compartida, por lo que cualquier estado que almacene debe ser intrínseco, esto es, debe ser independiente del contexto de la estructura con estado FlyweightConcreto.
* **FlyweightConcretoNoCompartido:**
  * no todas las sub estructuras de Flyweight necesitan ser compartidas. La interfaz Flyweight permite el comportamiento, no fuerza a él. Las estructuras con estado FlyweightConcretoNoCompartido suelen tener estructuras con estado FlyweightConcreto como hijos en algún nivel de la jerarquía de estructuras con estado.
* **FabricaFlyweight:**
  * crea y controla estructuras con estado flyweight.
  * garantiza  que los flyweight se compartan de manera adecuada. Cuando un cliente solicita un flyweight, la estructura con estado FabricaFlyweight proporciona una instancia concreta o crea una nueva, en caso de que no exista ninguna.
* **Cliente:**
  * mantiene una referencia a los flyweight.
  * culcula o guarda el estado extrínseco de los flyweight.

## Colaboradores

* El estado que un flyweight necesita para funcionar debe ser caracterizado como intrínseco o extrínseco. El estado intrínseco se guarda en la estructura con estado FlyweightConcreto, mientras que el estado extrínseco lo guardan o lo calculan las estructuras con estado Cliente. Los clientes pasan este estado al flyweight cuando invocan sus operaciones.
* Los clientes no deberían crear instancias FlyweightConcreto directamente, sino que deben obtener las estructuras con estado FlyweightConcreto sólo a partir de FabricaFlyweight para garantizar que se puedan compartir adecuadamente.

## Implementación

No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.

## Código de ejemplo

En este ejemplo queremos que nuestro sistema sea capaz de dibujar controles en la pantalla haciendo un uso eficiente de los recursos ya que existen controles (los botones) que pueden ser reutilizados.

Implementación:

```go
// Flyweight Interface
type Control interface {
    Dibujar(x string, y string) string
    GetReferencia() string
}

// Flyweight Concreto
type Boton struct {
    referencia string
}

func (b *Boton) Dibujar(x string, y string) string {
    return "Dibujando Botón #" + b.referencia + " en ejes " + x + ", " + y
}

func (b *Boton) GetReferencia() string {
    return b.referencia
}

// Flyweight Concreto No Compartido
type CampoPassword struct{}

func (cp *CampoPassword) Dibujar(x string, y string) string {
    return "Dibujando Campo de Password en ejes " + x + ", " + y
}

func (cp *CampoPassword) GetReferencia() string {
    return ""
}

// Fabrica Flyweight
type PantallaFabrica struct {
    controles []Control
}

func (pb *PantallaFabrica) ObtenerControl(tipo string, referencia string, x string, y string) string {
    for _, control := range pb.controles {
        if control.GetReferencia() == referencia {
            return control.Dibujar(x, y) + " || <control recuperado>"
        }
    }

    if tipo == "BOTON" {
        control := &Boton{referencia}

        pb.controles = append(pb.controles, control)

        return control.Dibujar(x, y)
    }

    if tipo == "PASSWORD" {
        control := &CampoPassword{}

        return control.Dibujar(x, y)
    }

    return ""
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
pantalla := &PantallaFabrica{}

fmt.Printf("%s\n", pantalla.ObtenerControl("BOTON", "BTN1", "100", "300"))
fmt.Printf("%s\n", pantalla.ObtenerControl("BOTON", "BTN2", "200", "300"))
fmt.Printf("%s\n", pantalla.ObtenerControl("BOTON", "BTN3", "300", "300"))
fmt.Printf("%s\n", pantalla.ObtenerControl("PASSWORD", "PWD1", "500", "300"))
fmt.Printf("%s\n", pantalla.ObtenerControl("BOTON", "BTN1", "400", "300"))
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/estructurales/flyweight) | [Ejecutar código](https://play.golang.org/p/o1TA4FcaAmD)

## Patrones relacionados

El patrón flyweight suele combinarse con el patrón [Composite](/patrones/estructurales/composite.md) para implementar una jerarquía lógica en términos de un grafo dirigido acíclico con nodos hojas compartidos.
Suele ser mejor implementar las estructuras con estado [State](/patrones/comportamiento/state.md) y [Strategy](/patrones/comportamiento/strategy.md) como flyweight.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Flyweight_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
