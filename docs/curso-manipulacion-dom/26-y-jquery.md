# ¿Y jQuery?

de alguien:

Resumen:

Fue popular porque no era fácil manipular el DOM.
No todos los navegadores tenían las mismas API.
Solucionaba errores e inconsistencias entre navegadores.
Hoy en día no es necesario pues los navegadores se mantienen al día con los estándares de HTML y JS.
Será útil si los usuarios de tus sitios web utilizan navegadores muy antiguos.
JQuery no murió, cambio tanto la forma de hacer frontend que se integró con la web.
Muchos de los web apis usados hoy fueron inspirados en jquery.

OTRO

jQuery fue algo muy hermoso que allá en años anteriores nos ayudó a tener una web más fácil de mantener, estandarizó a muchos navegadores, si algo no funcionaba en un navegador y en otro sí, jQuery hacía que funcionase en los dos, por eso fue tan mágico!
.
Sin embargo, los navegadores se actualizaron, y hoy en día hacer todo lo que hacía jQuery desde JavaScript nativo ya es muy fácil gracias a la implementación de ECMAScript que desde 2015 nos ha estado trayendo nuevos cambios y funcionalidades a JavaScript, le recomiento tomar el Curso de ECMAScript 6+ para enterarse de todos estos cambios.
.
De hecho, la noticia de que jQuery ya se estaba dejando de usar tuvo un gran impacto gracias a que GitHub publicó en su blog que se deshacían de jQuery:
.
Removing jQuery from GitHub.com frontend
.
¿Entonces debería seguir usando jQuery o no?
.
Es una pregunta difícil, porque la verdad depende mucho, si un proyecto ya estaba usando jQuery, no tiene caso que quites jQuery de ahí porque tendrías que rehacer tu app seguramente, y esto en muchos casos no es viable, sobre todo para empresas que ya tienen una web funcionando bajo jQuery. Sin embargo, si planeas iniciar un proyecto desde 0, lo mejor es que ya no uses jQuery, dale una oportunidad a JavaScript, Platzi tiene muchos cursos para aprender JavaScript profesionalmente, tienes toda una Escuela de JavaScript para ello.
.
El problema de la compatibilidad entre navegadores ya no es tan grande gracias a que existen transpiladores como Babel que permiten dar soporte a nuevas versiones de ECMAScript para la mayoría de los navegadores.
.
Incluso más allá, existen compiladores ya integrados que te dan la configuración de Babel + WebPack y preprocesadores de CSS como SASS o LESS ya listas y configuradas solo para ser usados, tu simplemente lo instalas, creas tus archivos y estos compiladores generan bundles con el código adaptado para diferentes navegadores, un ejemplo de ellos es Laravel Mix que es el compilador de front-end que usa Laravel para servir sus aplicaciones, y puedes usar Laravel Mix SIN tener que usar Laravel necesariamente (Laravel es un framework de PHP).
.
Incluso más allá, existen nuevos Frameworks progresivos que ya tienen todo esto integrado y permiten hacer cosas más increíbles como Vue, React, Angular o Svelte Ft. Oscar Barajas jaja.
.
Así que los invito a probar cosas nuevas porque seguro encuentran algo que les guste 👀

### Lecturas recomendadas

- [You Might Not Need jQuery](https://youmightnotneedjquery.com/)