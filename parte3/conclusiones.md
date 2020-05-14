# Conclusiones

_Go_ es un lenguaje que en muchos aspectos parece "_retrasar_" o da la sensación de "_antiguo_". Esta visión puede ser correcta si se lo compara por ejemplo con la forma en la que programaríamos en _Java_. Esto es justamente lo que se debe evitar: "_la comparación_". _Go_ nace con una filosofía bien clara que todo desarrollador de _Go_ debería conocer.

Dicho esto, tal como se pudo demostrar, es factible implementar los 23 Patrones de Diseño GoF en _Go_ sin grandes modificaciones de las estructuras originales.

Su aplicación no es una simple traducción literal de un lenguaje a otro - _como he visto muchas veces_ - sino que el uso de estos patrones realmente pueden aportar coherencia y valor al software desarrollado en _Go_.

Hemos visto que _Go_ no es realmente un lenguaje orientado a objetos, sin embargo también se pudo demostrar que sus características permiten programar aplicando prácticas y patrones propios de la programación orientada a objetos.

Dicho esto, creo que es muy importante destacar que cada lenguaje de programación nace con un propósito definido, y que si bien las experiencias previas que tenemos como desarrolladores de software nos pueden facilitar el aprendizaje de nuevos lenguajes de programación, es vital comprender cuales son las recomendaciones, usos, estilos y características propias del lenguaje que estamos aprendiendo para no cometer el error común de querer hacer las cosas de igual manera como las haríamos en otros lenguajes.

Considero que _Go_ es un excelente lenguaje para realizar trabajos concurrentes. Este tipo de programación hace que tengamos que repensar como podemos reutilizar soluciones ante problemas conocidos. Por tal motivo, y haciendo alusión a lo antes comentado, considero que un desarrollador de _Go_ debería invertir más tiempo en aprender como aplicar _patrones de concurrencia_ que _patrones de diseño_.

Estoy seguro de que todo lo visto en esta publicación es de valor para el desarrollador de _Go_, pero me gustaría cerrar esta conclusión con la siguiente recomendación:

> No deberían programar en _Go_ como lo hacen en _Java_, _PHP_, _C\#_, etc. Deberían potenciar las características propias del lenguaje en sus desarrollos; esto es comprender a fondo, por ejemplo, como funcionan las _interfaces_, la _composición_ y la _concurrencia_; y sobre esta base reutilizar conceptos o usos de patrones de diseño cuando realmente se justifiquen.

