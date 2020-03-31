# Patrón Command

## Propósito

Encapsula una petición en una variable, permitiendo así parametrizar a los clientes con diferentes peticiones, hacer cola o llevar registro de las peticiones, y poder deshacer las operaciones.

## También conocido como

_Action_, _Transaction_

## Estructura

![](/assets/uml/command.png)

## Participantes

* **Orden:**
  * declara una interfaz para ejecutar una operación.
* **Orden Concreta:**
  * define un enlace entre una variable Receptor y una acción.
  * implementa Ejecutar invocando la correspondiente operación u operaciones del Receptor.
* **Cliente:**
  * crea una variable OrdenConcreta y establece su receptor.
* **Invocador:**
  * le pide a la orden que ejecute la petición.
* **Receptor:**
  * sabe cómo llevar a cabo las operaciones asociadas a una petición. Cualquier clase puede actuar como Receptor.

## Implementación

No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.

## Código de ejemplo

En este ejemplo queremos poder prender y apagar un televisor mediante la invocación de comandos mediante un control remoto.

Implementación:

```go
// Interface Comando (Orden)
type Comando interface {
    Ejecutar() string
}

// Comando Prender (OrdenConcreta)
type ComandoPrender struct {
    receptor Receptor
}

func (cp ComandoPrender) Ejecutar() string {
    return cp.receptor.Prender()
}

// Comando Apagar (OrdenConcreta)
type ComandoApagar struct {
    receptor Receptor
}

func (ca ComandoApagar) Ejecutar() string {
    return ca.receptor.Apagar()
}

// Invocador
type Invocador struct {
    comandos []Comando
}

func (i *Invocador) GuardarComando(comando Comando) {
    i.comandos = append(i.comandos, comando)
}

func (i *Invocador) EliminarUltimoComando() {
    if len(i.comandos) != 0 {
        i.comandos = i.comandos[:len(i.comandos)-1]
    }
}

func (i *Invocador) Limpiar() {
    i.comandos = []Comando{}
}

func (i *Invocador) Ejecutar() string {
    var resultados string

    for _, comando := range i.comandos {
        resultados += comando.Ejecutar() + "\n"
    }

    return resultados
}

// Receptor
type Receptor struct{}

func (r Receptor) Prender() string {
    return "- Prender Televisor"
}

func (r Receptor) Apagar() string {
    return "- Apagar Televisor"
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
invocador := Invocador{comandos: []Comando{}}
receptor := Receptor{}

// se establecen dos comandos concretos y se los elimina
// el invocador queda sin comandos que ejecutar
invocador.GuardarComando(ComandoPrender{receptor: receptor})
invocador.GuardarComando(ComandoApagar{receptor: receptor})
invocador.Limpiar()

// se establecen dos comandos concretos iguales y se elimina el último
// el invocador queda con un único comando para ejecutar
invocador.GuardarComando(ComandoPrender{receptor: receptor})
invocador.GuardarComando(ComandoPrender{receptor: receptor})
invocador.EliminarUltimoComando()

// se establece un comando concreto más
invocador.GuardarComando(ComandoApagar{receptor: receptor})

// el invocador ejecuta los dos comandos
fmt.Printf("Comandos ejecutados:\n%v\n", invocador.Ejecutar())
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/command) \| [Ejecutar código](https://play.golang.org/p/BRtWoVLF5nB)
