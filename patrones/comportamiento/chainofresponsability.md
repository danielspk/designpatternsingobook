# Patrón Chain of Responsability

## Propósito

Evita acoplar el emisor de una petición a su receptor, dando a más de una estructura con estado la posibilidad de responder a la petición. Encadena las estructuras con estado receptoras y pasa la petición a través de la cadena hasta que es procesada por alguna estructura con estado.

## Motivación

Queremos desacoplar a los emisores de los receptores dándole a varias esructuras con estado la posibilidad de tratar un petición. El esquema propuesto es el siguiente:

**Contenido en desarrollo.**

## Aplicabilidad

El patrón Chain of Responsability se debe usar cuando:

* hay más de una estructura con estado que pueden manejar una petición, y el manejador no se conoce _a priori_, sino que debería determinarse automáticamente.
* se quiere enviar una petición a una estructura con estado entre varias sin especificar explícitamente la receptora.
* el conjunto de estructuras con estado que pueden tratar una petición debería ser especificado dinámicamente.

## Estructura

**Contenido en desarrollo.**

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

**Contenido en desarrollo. a) analizar otras alternativas, b) implicancias con concurrencia.**

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

Este patrón se suele aplicar conjuntamente con el patrón [Composite](/patrones/estructurales/composite.md). En él, los padres de los componentes pueden actuar como sucesores.
