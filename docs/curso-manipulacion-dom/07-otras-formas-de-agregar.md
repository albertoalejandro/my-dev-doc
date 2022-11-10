# Otras formas de agregar

Existen otras formas de agregar nodos:

- node.outerHTML: Sirve para leer HTML para leer HTML
- node.innerHTML: Sirve para escribir HTML


PEEEEEEERO, tienen un problema de seguridad 👀☝️

hack: Cuando en el inspector de elementos seleccionas un elemento y en la consola escribes $0, este te devolverá el elemento tal como si lo hubieses seleccionado con document.querySelector().

Aquí les dejo el playground que usó el profesor para hacer las pruebas:
https://codepen.io/jonalvarezz/pen/OJXeNab?editors=0110

El problema con estas formas de inserciones es que permiten la inserción XSS, es decir, código maligno, y cualquier usuario programador malicioso podría meter scripts molestos, imagina que cada que un usuario llegue a tu página le salga un alert… ¡Sería catastrófico! Siempre sanitiza (remover caracteres especiales) los inputs de tus usuarios



Atajo: Si seleccionamos un nodo de la pestaña "Elements" y luego en consola escribimos "$0" el navegador nos dará ese elemento seleccionado nos seleccionará el nodo.

OTRO:

Otras formas de agregar
<h4>Ideas/conceptos claves</h4>
Los ataques XSS son un tipo de inyección en la cual un atacante logra ejecutar código en los navegadores de los usuarios que acceden a un sitio web legítimo

<h4>Apuntes</h4>
- Existen otras formas de leer y agregar nodos que son muchas convenientes usando cadenas de texto
    - node.outerHTML (leer)
        - Nos dejar leer el HTML como una cadena del nodo seleccionado
    - node.innerHTML (escribir)
        - Nos deja modificar el contenido del nodo

- La desventaja es que convierte el texto en HTML pudiendo crear inyecciones de XSS
    - Debido a que convierte todo el texto en HTML, habiendo la posibilidad de que se pueda inyectar códigos de terceros

- Si es que fuera muy necesario usar estos métodos y el usuario necesitara ingresar los datos, se debe hacer si o si un proceso de sanitize (Limpieza)

**RESUMEN**: Existe otras formas de leer y escribir el HTML, pero tienen un riesgo de ataques XSS, no es mala siempre y cuando se tenga un cuidado con las posibilidades del usuario

MIO

```
> $0.outerHTML
< '<h2>Checkout form</h2>'


> $0.innerHTML
< 'Checkout form'

> $0.innerHTML = "Algo nuevo"
< 'Algo nuevo'




>$0
<div class=​"py-5 text-center">​…​</div>​
>$0.outerHTML
'<div class="py-5 text-center">\n    <img class="d-block mx-auto mb-4" src="/docs/4.5/assets/brand/bootstrap-solid.svg" alt="" width="72" height="72">\n    <h2>Algo nuevo</h2>\n    <p class="lead">Below is an example form built entirely with Bootstrap’s form controls. Each required form group has a validation state that can be triggered by attempting to submit the form without completing it.</p>\n  </div>'
>const nuevoHTML = $0.outerHTML.replace('Algo nuevo', 'Algo viejo')
undefined
>nuevoHTML
'<div class="py-5 text-center">\n    <img class="d-block mx-auto mb-4" src="/docs/4.5/assets/brand/bootstrap-solid.svg" alt="" width="72" height="72">\n    <h2>Algo viejo</h2>\n    <p class="lead">Below is an example form built entirely with Bootstrap’s form controls. Each required form group has a validation state that can be triggered by attempting to submit the form without completing it.</p>\n  </div>'
>$0.innerHTML = nuevoHTML
'<div class="py-5 text-center">\n    <img class="d-block mx-auto mb-4" src="/docs/4.5/assets/brand/bootstrap-solid.svg" alt="" width="72" height="72">\n    <h2>Algo viejo</h2>\n    <p class="lead">Below is an example form built entirely with Bootstrap’s form controls. Each required form group has a validation state that can be triggered by attempting to submit the form without completing it.</p>\n  </div>'


consejo pasarle un proceso de sanitize
```


### Lecturas recomendadas

- [Attention Required! | Cloudflare](https://codepen.io/jonalvarezz/pen/OJXeNab)