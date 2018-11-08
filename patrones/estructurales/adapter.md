# Patrón Adapter

## Propósito

Convierte la interfaz de una estructura en otra interfaz que es la que esperan los clientes. Permite que cooperen estructuras que de otra forma no podrían por tener interfaces incompatibles.

## También conocido como

_Wrapper_ (Envoltorio)

## Aplicabilidad

Úsese el patrón Adaptor cuando:
* se quiere usar una estructura existente y su interfaz no concuerda con la que necesita.
* se quiere crear una estructura reutilizable que coopere con estructuras no relacionadas o que no han sido previstas, es decir, estructuras que no tienen por qué tener interfaces compatibles.

## Estructura

![](/assets/uml/adapter.png)

## Participantes

* **Objetivo:**
  * define la interfaz específica del dominio que usa el Cliente.
* **Cliente:**
  * colabora con estructuras con estado que se ajustan a la interfaz Objetivo.
* **Adaptable:**
  * define una interfaz existente que necesita ser adaptada.
* **Adaptador:**
  * adapta la interfaz de Adaptable a la interfaz Objetivo.

## Colaboradores

Los clientes llaman a operaciones de una instancia de Adaptador. A su vez, el adaptador llama a operaciones de Adaptable, que son las que satisfacen la petición.

## Implementación

No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.

## Código de ejemplo

En este ejemplo queremos que un juego de RPG se pueda adaptar a un nuevo tipo de personaje (_Magos_) que no comparte las mismas características que los guerreros originales (_Elfos_).
Para esto es necesario realizar un adaptador para que un _Mago_ pueda atacar como un _Elfo_.

Implementación:

```go
// Objetivo
type Gerrero interface {
    UsarArma() string
}

type Elfo struct{}

func (e *Elfo) UsarArma() string {
    return "atacando con arco y flecha"
}

// Adaptable
type GerreroMagico interface {
    UsarMagia() string
}

type Mago struct{}

func (m *Mago) UsarMagia() string {
    return "atacando con magia"
}

// Adaptador
type MagoAdaptador struct {
    gerrero GerreroMagico
}

func (ma *MagoAdaptador) UsarArma() string {
    return ma.gerrero.UsarMagia()
}

// Cliente
type Jugador struct {
    guerrero Gerrero
}

func (j *Jugador) Atacar() string {
    return j.guerrero.UsarArma()
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
jugadorA := &Jugador{&Elfo{}}
fmt.Printf("Jugador A: %s\n", jugadorA.Atacar())

jugadorB := &Jugador{&MagoAdaptador{&Mago{}}}
fmt.Printf("Jugador B: %s\n", jugadorB.Atacar())odos los desarrolladores de la Gerencia es de $%d\n", gerenciaIT.ObtenerSalario())
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/estructurales/adapter) | [Ejecutar código](https://play.golang.org/p/60tlY8la04W)

## Patrones relacionados

El patrón [Bridge](/patrones/estructurales/bridge.md) tiene una estructura similar a un Adapter, pero con un proposito diferente: está pensado para separar una interfaz de su implementación, de manera que ambos puedan cambiar facilmente y de forma independiente uno del otro, mientras que un adapter está pensado para cambiar la interfaz de una estructura con estado existente.
El patrón [Decorator](/patrones/estructurales/decorator.md) decora otra estructura con estado sin cambiar su interfaz. Un decorador es por tanto más transparente a la aplicación que un adaptador. Como resultado, el patrpon Decorator permite la composición recursiva, lo que no es posible con adaptadores puros.
El patrón [Proxy](/patrones/estructurales/proxy.md) define un representante o sustituto de otra estructura con estado sin cambiar su interfaz.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Adapter_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
