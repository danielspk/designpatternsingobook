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

**Contenido en desarrollo.**

## Colaboradores

**Contenido en desarrollo.**

## Implementación

**Contenido en desarrollo. a) analizar otras alternativas, b) implicancias con concurrencia.**

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

Este patrón se suele aplicar conjuntamente con el patrón [Composite](/patrones/estructurales/composite.md). En él, los padres de los componentes pueden actuar como sucesores.
