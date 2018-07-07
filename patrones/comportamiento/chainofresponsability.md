# Patrón Chain of Responsability

## Propósito

Evita acoplar el emisor de una petición a su receptor, dando a más de una estructura con estado la posibilidad de responder a la petición. Encadena las estructuras con estado receptoras y pasa la petición a través de la cadena hasta que es procesada por alguna estructura con estado.

## Motivación

Queremos desacoplar a los emisores de mensajes de los distintos receptores disponibles. Delegango así, a dichos receptores la posibilidad de procesar o no los mensajes recepcionados. El esquema propuesto es el siguiente:

![](/assets/uml/ejemplos/chainofresponsability.png)

## Aplicabilidad

El patrón Chain of Responsability se debe usar cuando:

* hay más de una estructura con estado que pueden manejar una petición, y el manejador no se conoce _a priori_, sino que debería determinarse automáticamente.
* se quiere enviar una petición a una estructura con estado entre varias sin especificar explícitamente la receptora.
* el conjunto de estructuras con estado que pueden tratar una petición debería ser especificado dinámicamente.

## Estructura

![](/assets/uml/chainofresponsability.png)

## Participantes

* **Manejador:**
  * define una interfaz para tratar las peticiones.
  * _(opcional)_ implementa el enlace al sucesor.
* **ManejadorConcreto:**
  * trata las peticiones de las que es responsable.
  * puede acceder a su sucesor.
  * si el ManejadorConcreto puede manejar la petición, lo hace; en caso contrario la reenvía a su sucesor.
* **Cliente:**
  * inicializa la petición a una estructura con estado ManejadorConcreto de la cadena.

## Colaboradores

Cuando un cliente envía una petición, ésta se propaga a través de la cadena hasta que una estructura con estado ManejadorConcreto se hace responsable de procesarla.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

En este ejemplo se definen dos receptores distintos de mensajes. Uno para mensajes de alta prioridad y otro para mensajes de baja prioridad. El mensaje enviado por el cliente es transmitido a través de la cadena de receptores y cada receptor trata o no el mensaje de acuerdo a su prioridad.

```go
// Interface
type Receptor interface {
    ProcesarMensaje(int, string) string
}

// Receptor de Alta Prioridad
type ReceptorAltaPrioridad struct{
    siguiente Receptor
}

func (rap ReceptorAltaPrioridad) ProcesarMensaje(prioridad int, mensaje string) string {
    if prioridad >= 5 {
       return "Procesando mensaje de alta prioridad: " + mensaje
    }
    
    if rap.siguiente != nil {
       return rap.siguiente.ProcesarMensaje(prioridad, mensaje)
    }
    
    return ""
}

// Receptor de Baja Prioridad
type ReceptorBajaPrioridad struct{
    siguiente Receptor
}

func (rbp ReceptorBajaPrioridad) ProcesarMensaje(prioridad int, mensaje string) string {
    if prioridad < 5 {
       return "Procesando mensaje de baja prioridad: " + mensaje
    }
    
    if rbp.siguiente != nil {
       return rbp.siguiente.ProcesarMensaje(prioridad, mensaje)
    }
    
    return ""
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
manejadores := ReceptorBajaPrioridad {
    siguiente: ReceptorAltaPrioridad {},
}

fmt.Println(manejadores.ProcesarMensaje(4, "Mensaje 1"))

fmt.Println(manejadores.ProcesarMensaje(5, "Mensaje 2"))

fmt.Println(manejadores.ProcesarMensaje(10, "Mensaje 3"))
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/chainofresponsability) | [Ejecutar código](https://play.golang.org/p/TnwdRltyBds)

## Patrones relacionados

Este patrón se suele aplicar conjuntamente con el patrón [Composite](/patrones/estructurales/composite.md). En él, los padres de los componentes pueden actuar como sucesores.
