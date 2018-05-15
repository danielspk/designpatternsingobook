**Contenido en desarrollo - En esta sección se detallará que motivo la realización de esta publicación. Qué criterios se utilizaron. Cómo resulto la experiencia. Cúal fue el plan de trabajo, etc.**

# Acerca de esta publicación

## Motivación

Esta publicación fue motivada como trabajo final de mi Posgrado de Especialización en Ingeniería del Software que curse durante el año 2017 en la [UCA](http://www.uca.edu.ar) *(Pontificia Universidad Católica Argentina)*.

Aproximadamente durante los últimos 10 años vengo desarrollando software principalmente orientado a objetos. En uno de mis últimos proyectos debimos analizar un cambio en el lenguaje de programación que utilizábamos ya que uno de los principales atributos de calidad que debía cumplir el nuevo software era la eficiencia; por esto era fundamental que el software fuera lo más rápido posible. Si bien es un análisis muy pobre el analizar que tan rápido es un software sólo mirando con que lenguaje de programación se desarrollo, esta era una oportunidad que como equipo teníamos para explorar nuevos lenguajes. Luego de varias pruebas y discusiones quedaron dos candidatos finales: [Go](https://golang.org/) y [Rust](https://www.rust-lang.org/en-US/).
La paradoja de esta historia es que al final el proyecto se realizo en [Node.js](https://nodejs.org/en/). Las razones escapan a esta publicación, sin embargo una de ellas tuvo un fuerte impacto es esa decisión: "como transferir el conocimiento orientado a objetos que posee el grupo de desarrolladores a estos lenguajes que no son puramente orientados a objetos, o no de igual manera como lo conocen los desarrolladores de Java, C#, PHP, etc".
Anteriormente decia que la elección de Node.js fue una paradoja porque quien alguna vez ha desarrollado en Javascript sabra las limitaciones que posee su orientación a objetos y de las grandes discuciones que hay en la comunidad sobre si Javascript es realmente un lenguaje orientado a objetos u orientado a prototipos.
Esta es la razón principal de esta publicación, la de poder ayudar a un futuro equipo de tecnología a que puedan visualizar como es la Programación Orientada a Objetos en Go partiendo de los ya clásicos Patrones de Diseño GoF.

### El trabajo

El trabajo presentado se denomina:

> "Una perspectiva a la Programación Orientada a Objetos en Go en base a los Patrones de Diseño GoF"*

El mismo se presenta como:

> "El objetivo principal del presente trabajo será mostrar cómo pueden aplicarse los Patrones de Diseño GoF en un lenguaje de programación que no es completamente orientado a objetos. Para esto se utilizará como referencia el lenguaje de programación Go. Su propósito principal será servir de material de referencia para desarrolladores Go que deseen aplicar los patrones de Diseño GoF.
Se analizará la viabilidad, los ajustes, y las adaptaciones necesarias para implementar los Patrones de Diseño en base a las características del lenguaje de programación Go. Para esto, previamente se abordarán y explicarán los atributos orientados a objetos que posee el lenguaje de programación Go.
Adicionalmente el trabajo se publicará como ebook online mediante la realización de una página web, junto a ejemplos autoejecutables y un repositorio público con todo el código fuente, ejemplos y diagramas desarrollados."

### Porqué Go

Al momento de tomar la decisión sobre cuál de los dos lenguajes antes mencionados ([Go](https://golang.org/), [Rust](https://www.rust-lang.org/en-US/)) iba a basar mi trabajo, decidí hacer una pequeño análisis sobre la popularidad de ambos lenguajes en los últimos años.
Para esto tome como referencia el índice de popularidad de los lenguajes de programación [\[43\]](recursos.md) de la Empresa [Tiobe](https://www.tiobe.com).

Tiobe es una empresa especializada en la evaluación y el seguimiento de la calidad del software que publica mensualmente un índice [\[43\]](recursos.md) de popularidad de lenguajes de programación. Este índice es conformado en base a la cantidad de resultados que arrojan varios motores de búsqueda. Los resultados deben cumplir ciertos requerimientos para calificar para el índice, por ejemplo el lenguaje de programación debe tener su propia entrada en Wikipedia, ser completo (poder simular una máquina de Turing) y tener al menor 5.000 visitas en búsquedas aplicadas desde Google. La empresa también utiliza filtros para evitar falsos positivos y otras reglas para valorar la calificación del resultado.

> El proceso de como Tiobe confecciona el índice se encuentra bien detallado en el siguiente link: [https://www.tiobe.com/tiobe-index/programming-languages-definition/](https://www.tiobe.com/tiobe-index/programming-languages-definition/)

Basándome en el índice antes mencionado realice una comparación de ambos lenguajes y _Go_ en su historia como actualmente, tiene mayor popularidad respecto de _Rust_.

Como se puede apreciar en la siguiente gráfica _(Mayo/2018)_ _Go_ obtuve su mejor ubicación dentro del ranking en Julio de 2017 al ubicarse entre los primeros 10 lenguajes de programación. Desde mediados de 2016 a mediados de 2017 tuvo su mayor pico de popularidad, con un marcado descenso actualmente.

![](/assets/stats/rankinggo.png)

Actualmente _(Mayo/2018)_ _Go_ se ubica en la 14ª posición:

![](/assets/stats/indextiobe201805.png)

Por el contrario _Rust_ se ubica actualmente _(Mayo/2018)_ en la 91ª posición en una clara caida dentro del ranking. Si bien por su posición actual sus estadísticas ya no se publican dentro del índice Tiobe, al momento de su evaluación estaba dento del ranking de los 20ª a 50ª.

> Las estadísticas registradas de Tiobe corresponden a Mayo del 2018. Consulte el Índice Tiobe [\[43\]](recursos.md) para tener datos más actualizados.

Existen otros sitios especializados en medir la popularidad de los lenguajes de programación como [http://pypl.github.io/PYPL.html](http://pypl.github.io/PYPL.html), y [http://redmonk.com/sogrady/category/programming-languages/](http://redmonk.com/sogrady/category/programming-languages/), pero Tiobe es a mi entender el que más criterios de evaluación y filtros detalla para su ranking.

En conclusión, el historial de popularidad de _Go_ respecto de _Rust_ fue lo que definió su selección para la publicación de este trabajo en ese lenguaje de programación.

### El camino recorrido

**Contenido en desarrollo.**

### Las decisiones

**Contenido en desarrollo.**

### Las herramientas utilizadas

Para esta publicación se priorizó la utilización de herramientas que cumplieran alguna de las siguientes premisas:
- que fueran gratuitas y de libre acceso
- que fueran open source

Las herramientas utilizadas fueron:
- **GitBook**: plataforma para la publicación online de este trabajo. - [https://www.gitbook.com/](https://www.gitbook.com/)
- **Github**: plataforma para la publicación del código fuentes de esta publicación. - [https://github.com/](https://github.com/)
- **Git**: software para el control de versiones del código fuente de esta publicación. - [https://git-scm.com/](https://git-scm.com/)
- **Markdown**: lenguaje de marcado para la redacción de esta publicación. - [https://daringfireball.net/projects/markdown/](https://daringfireball.net/projects/markdown/)
- **Go Playground**: plataforma para la publicación y ejecución de códigos de ejemplo de _Go_. - [https://play.golang.org/](https://play.golang.org/)
- **Violet UML Editor**: software para la generación de diagramas UML. - [http://alexdp.free.fr/violetumleditor](http://alexdp.free.fr/violetumleditor)

La motivación de la elección de estas y no otras herramientas fue la siguiente:
- Para la generación de la publicación se analizaron otras alternativas a _GitBook_ como: **a)** hacer una web puramente en HTML/CSS, **b)** hacer una web con algún CMS como _Joomla_ o _WordPress_, y **c)** utilizar un generador de ebook como _Pandoc_ o similares. Sin embargo la elección fue _GitBook_ ya que integra varias características como la auto publicación online, la redacción en markdown, la exportación a otros formatos (ePub, PDF, Mobi), y un entorno de colaboración con terceros mediante la publicación de comentarios y notas.
- Para la publicación de códigos fuentes se analizaron otras plataformas a _Github_ como: **a)** _GitLab_, o **b)** _Bitbucket_. Sin embargo la elección fue _Github_ ya que, de las tres, en mi experiencia es la que más proyectos open source aloja. Siendo mi deseo que esta publicación pueda ser el punto de partida para otros fork y discusiones en la comunidad de _Go_.
- Para el control de versiones de analizo también _SVN_. Sin embargo la elección fue _Git_ ya que a diferencia de _SVN_ no requiere de un repositorio central facilitando el trabajo de la redacción de la publicación en diferentes equipos y lugares.
- Para el lenguaje de redacción de la publicación se analizaron otras alternativas a _Markdown_ como: **a)** _HTML_, **b)** _OpenDocument_, y **c)** _reStructuredText_. Sin embargo la elección fue _Markdown_ ya que resulta ser un lenguaje mucho más simple de aprender que los anteriores y existe una gran cantidad de herramientas para convertir el mismo en otros formatos. Este punto es muy importante para facilitar una posterior colaboración y ampliación de la publicación mediante la comunidad interesada en _Go_.
- Para la generación de diagramas UML se analizaron otras alternativas a _Violet UML_ como: **a)** _StarUML_, **b)** _Diagram Designer_, y **c)** _ModelioSoft_. Sin embargo la elección fue _Violet UML_ ya que se encuentra disponible para varios Sistemas Operativos y es muy simple de aprender dado que no tiene demasiadas opciones y tipos de diagramas disponibles.
- Para la ejecución online de código de ejemplo en _Go_ no analice otras alternativas ya que _Go Playgroung_ es la herramienta oficial de _Go_ y se encuentra muy popularizada en su comunidad.

### Los porqué / foco

**Contenido en desarrollo.**

## Agradecimientos

**Contenido en desarrollo.**
