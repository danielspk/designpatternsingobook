# Patrón Proxy

## Propósito

Proporciona un representante o sustituto de otra estructura estado para controlar el acceso a ésta.

## También conocido como

_Surrogate_ (Sustituto)

## Aplicabilidad

Este patrón es aplicable cada vez que hay necesidad de una referencia a una estructura con estado más versátil o sofisticada que un simple puntero. Úsese el patrón Proxy cuando:
* se requiere de un representante local de un objeto situado en otro espacio de direcciones (**proxy remoto**).
* se requiere crear estructuras con estado costosas por encargo (** proxy virtual**).
* se requiere controlar el acceso a la estructura con estado original en base a diferentes permisos (**proxy de protección**).
* se requiere de un sustituto simple, como un puntero, que permita realizar operaciones adicionales (**referencia inteligente**).

## Estructura

![](/assets/uml/proxy.png)

## Participantes

* **Proxy:**
  * mantiene una referencia que permite al proxy acceder a la estructura con estado original. El proxy puede referirse a un Sujeto en caso de que las interfaces de SujetoReal y Sujeto sean la misma.
  * proporciona una interfaz ientica a la de Sujeto, de manera que un proxy pueda ser sustituido por el sujeto real.
  * controla el acceso al sujeto real, y puede ser responsable de su creación y borrado.
  * otras responsabilidades dependen del tipo de proxy:
    * los proxies remotos son responsables de codificar una petición y sus argumentos para enviar la petición codificada al sujeto real que se encuentra en un espacio de direcciones diferente.
    * los proxies virtuales pueden guardar información adicional sobre el sujeto real, por lo que pueden retardar el acceso al mismo.
    * los proxies de protección comprueban que el llamador tenga los permisos de acceso necesarios para realizar una petición.
* **Sujeto:**
  * define una interfaz común para el SujetoReal y el Proxy, de modo que pueda usarse un Proxy en cualquier sitio en el que se espere un SujetoReal.
* **SujetoReal:**
  * define la estructura con estado real representada.

## Colaboradores

El Proxy  redirige peticiones al SujetoReal cuando sea necesario, dependiendo del tipo de proxy.

## Implementación

No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.

## Código de ejemplo

En este ejemplo queremos restringir los accesos a redes sociales en los navegadores de una escuela. Para esto realizaremos un proxy de protección.

Implementación:

```go
// Sujeto Interface
type NavegadorInterface interface {
    Direccion(string) string
}

// Sujeto Real
type Navegador struct{}

func (n *Navegador) Direccion(url string) string {
    return "Respuesta de la url " + url
}

// Proxy
type NavegadorProxy struct {
    navegador NavegadorInterface
}

func (n *NavegadorProxy) Direccion(url string) string {
    if url == "http://twitter.com" || url == "http://facebook.com" {
        return "Acceso restringido a " + url
    }

    return n.navegador.Direccion(url)
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
navegadorProxy := &NavegadorProxy{&Navegador{}}

fmt.Printf("%s\n", navegadorProxy.Direccion("http://google.com"))
fmt.Printf("%s\n", navegadorProxy.Direccion("http://twitter.com"))
fmt.Printf("%s\n", navegadorProxy.Direccion("http://facebook.com"))
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/estructurales/proxy) | [Ejecutar código](https://play.golang.org/p/7JSOE4GYByc)

## Patrones relacionados

[Adapter](/patrones/estructurales/adapter.md): un adaptador proporciona una intefaz diferente para la estructura con estado que adapta. Por el contrario, un proxy tiene la misma interfaz que su sujeto. No obstante, un proxy utilizado para protección de acceso podría rechazar una operación que el sujeto sí realiza, de modo que su interfaz puede ser realmente un subconjunto de la del sujeto.
[Decorator](/patrones/estructurales/decorator.md): si bien los decoradores pueden tener una implementación parecida a los proxies, tienen un proposito diferente. Un decorador añade una o más responsabilidades a una estructura con estado, mientras que un proxy controla el acceso a una estructura con estado.
Los proxies difieren en el grado de similitud entre su implementación y la de un decorador. Un proxy de protección podría implementarse exactamente como un decorador. Por otro lado, un proxy remoto no contendrá una referencia directa a su sujeto real sino sólo una referencia indirecta, como un "ID" de máquina y la dirección local de dicha máquina. Un proxy virtual empezará teniendo una referencia indirecta como un nombre de fichero, pero podrá al final obtener y utilizar una referencia directa.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Proxy_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
