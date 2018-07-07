# Patrón Command

## Propósito

Encapsula una petición en una estructura con estado, permitiendo así parametrizar a los clientes con diferentes peticiones, hacer cola o llevar registro de las peticiones, y poder deshacer las operaciones.

## También conocido como

_Action_, _Transaction_

## Motivación

**Contenido en desarrollo.**

## Aplicabilidad

Úsese el patrón Command cuando se quiera

* parametrizar estructuras con estado con una acción a realizar. En un lenguaje de prodecimiento se puede expresar la parametrización mediante una función _callback_, es decir, con una función que esté registrada en algú sitio para que sea llamada más tarde.
* especificar, poner en cola y ajecutar peticiones en diferentes instantes de tiempo. Si se puede representar el receptor de una petición en una forma independiente del espacio de direcciones, entonces se puede transferir una estructura orden con la petición a un proceso diferente y llevar a cabo la petición allí.
* permitir deshacer. Las órdenes ejecutadas se guardan en una lista que hace las veces de historial. Se pueden lograr niveles ilimitados de deshacer y repetir recorriendo dicha lista hacia atrás y hacia delante.
* permitir registrar los cambios de manera que se puedan volver a aplicar en caso de una caída del sistema.
* estructurar un sistema alrededor de operaciones de alto nivel construidas sobre operaciones básicas. Dicha estructura es común en los sistemas de información que permiten *transacciones*. El patrón Command ofrece un modo de modelar transacciones. Las órdenes tienen una interfaz común, permitiendo así invocar a todas las transacciones del mismo modo. El patrón también facilita extender el sistema con nuevas transacciones.

**Contenido en desarrollo.**
