# Patrón Composite

## Propósito

Compone estructuras con estado en jerarquías de árbol para representar jerarquías de parte-todo. Permite que los clientes traten de manera uniforme a las estructuras con estado individuales y a las compuestas.

## Aplicabilidad

Úsese el patrón Composite cuando:
* quiera representar jerarquías de estructuras con estado parte-todo.
* quiera que los clientes sean capaces de obviar las diferencias entre composiciones de estructuras con estados y las estructuras con estado individuales. Los clientes tratarán a todas las estructuras con estado de la jerarquía compuesta de manera uniforme.

## Estructura

![](/assets/uml/composite.png)

## Participantes

* **Componente:**
  * declara la interfaz de las estructuras con estado de la composición.
  * implementa el comportamiento predeterminado de la interfaz que es común a todas las estructuras.
  * declara una interfaz para acceder a sus componentes hijos y gestionarlos.
  * _(opcional)_ define una interfaz para acceder al padre de un componente en la jerarquía recursiva y, si es necesario, la implementa.
* **Hoja:**
  * representa estructuras con estado hoja en la composición. Una hoja no tiene hijos.
  * define el comportamiento de las estructuras con estado primitivas de la composición.
* **Compuesto:**
  * define el comportamiento de los componentes que tienen hijos.
  * almacena componentes hijos.
  * implementa las operaciones de la interfaz Componente relacionadas con los hijos.
* **Cliente:**
  * manipula estructuras con estado en la composición a través de la interfaz Componente.

## Colaboradores

Los Clientes usan la interfaz de la estructura Componente para interactuar con las estructuras con estado de la jerarquía compuesta. Si el recipiente es una Hoja, la petición se trata correctamente. Si es un Compuesto, normalmente redirige las peticiones a sus componentes hijos, posiblemente realizando operaciones adicionales antes o después.

## Implementación

No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.

## Código de ejemplo

En este ejemplo queremos  acceder a los salarios de los empleados de una gerencia tanto de forma individual como grupal. De esta forma la compañia podría analizar el impacto de futuros bonos de productividad tanto para una gerencia completa o para alguno de sus empleados.

Implementación:

```go
// Componente Interface
type Empleado interface {
    ObtenerSalario() int
}

// Hoja
type DesarrolladorSenior struct{}

func (ds *DesarrolladorSenior) ObtenerSalario() int {
    return 1000
}

// Hoja
type DesarrolladorJunior struct{}

func (dj *DesarrolladorJunior) ObtenerSalario() int {
    return 750
}

// Compuesto
type GerenciaIT struct {
    empleados []Empleado
}

func (g *GerenciaIT) AgregarEmpleado(empleado Empleado) {
    g.empleados = append(g.empleados, empleado)
}

func (g *GerenciaIT) ObtenerSalario() int {
    sumaSalarios := 0

    for _, empleado := range g.empleados {
        sumaSalarios = sumaSalarios + empleado.ObtenerSalario()
    }

    return sumaSalarios
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
empleadoA := &DesarrolladorJunior{}
empleadoB := &DesarrolladorJunior{}
empleadoC := &DesarrolladorSenior{}

gerenciaIT := &GerenciaIT{}
gerenciaIT.AgregarEmpleado(empleadoA)
gerenciaIT.AgregarEmpleado(empleadoB)
gerenciaIT.AgregarEmpleado(empleadoC)

fmt.Printf("El salario individual del desarrollador A es de $%d\n", empleadoA.ObtenerSalario())
fmt.Printf("El salario individual del desarrollador B es de $%d\n", empleadoB.ObtenerSalario())
fmt.Printf("El salario individual del desarrollador C es de $%d\n", empleadoC.ObtenerSalario())
fmt.Printf("Los salarios de todos los desarrolladores de la Gerencia es de $%d\n", gerenciaIT.ObtenerSalario())
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/estructurales/composite) | [Ejecutar código](https://play.golang.org/p/BR_zwXpOD0O)

## Patrones relacionados

Muchas veces se usa el enlace al componente padre para implementar el patrón [Chain of Responsability](/patrones/comportamiento/chainofresponsability.md).
El patrón [Decorator](/patrones/estructurales/decorator.md) suele usarse junto con el Composite. Cuando se usan juntos decoradores y compuestos, normalmente ambos tendrán una estructura común. Por tanto, los decoradores tendrán que admitir la interfaz Componente con operaciones de añadir, eliminar y obtenerHijo.
El patrón [Flyweight](/patrones/estructurales/flyweight.md) permite compartir componentes, si bien en ese caso éstos ya no pueden referirse a sus padres.
Se puede usar el patrón [Iterator](/patrones/comportamiento/iterator.md) para recorrer las estructuras definidas por el patrón Composite.
El patrón [Visitor](/patrones/comportamiento/visitor.md) localiza operaciones y comportamiento que de otro modo estaría distribuido en estructuras Compuesto y Hoja.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Composite_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
