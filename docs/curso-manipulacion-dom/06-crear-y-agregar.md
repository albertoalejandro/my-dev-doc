# Crear y agregar

Al decir “crear nodos” nos referimos a crear elementos dentro de nuestro DOM. Para ello podemos hacer uso de:

- createElement: Para crear una etiqueta HTML:

```
// Solo se ha creado, aún no se agrega al DOM
const etiquetaH1 = document.createElement("h1")
```

- createTextNode: Para crear un texto:
```
// Solo se ha creado, aún no se agrega al DOM
const texto = document.createTextNode("¡Hola, Mundo!")
```

Como solo creamos, necesitamos formas de agregarlos al DOM, para ello, JavaScript nos provee de estas formas:

- parentElement.appendChild(): Agrega un hijo al final algún elemento
```
// Obtengo el elemento padre
const parentElement = document.querySelector("selector")
// Creo el nodo a insertar
const h3 = document.createElement("h3")
// Creo el texto del nodo
const texto = document.createTextNode("Hola!")
// Inserto el texto al nodo
h3.appendChild(h3)
// Inserto el nodo al padre
parentElement.appendChild(h3)
```

- parentElement.append(): Es la evolución de appendChild, podemos agregar más de un nodo, puedes agregar texto y… no es soportado por Internet Explorer ¬¬!

Un polyfill es una adaptación del código para dar soporte a navegadores que no lo soportan, aquí está el polyfill de append:
https://developer.mozilla.org/es/docs/Web/API/ParentNode/append#polyfill

```
// Obtengo el elemento padre
const parentElement = document.querySelector("selector")
// Agrego al elemento padre
parentElement.append("agrego un texto", document.createElement("div"))
```

- parentElement.insertBefore(): Inserta nodos antes del elemento que le pasemos como referencia, este nodo de referencia **tiene que ser un hijo DIRECTO del padre**

```
// Obtengo el elemento padre
const parentElement = document.querySelector("selector")
// Creo un elemento
const titulo = document.createElement("h1")
// Obtengo la referencia del elemento del que quiero insertar antes:
const referencia = document.querySelector("selector")
// ¡Lo insertamos!
parentElement.insertBefore(titulo, referencia)
```

- parentElement.insertAdjacentElement(): Inserta nodos según las opciones que le pasemos:

1.beforebegin: Lo inserta antes del nodo
2.afterbegin: Lo inserta despues del nodo
3.beforeend: Lo inserta antes de donde finaliza el nodo
4.afterend: Lo inserta después de donde finaliza el nodo

```
// Obtengo el elemento padre
const parentElement = document.querySelector("selector")
// Creo un elemento
const nodo = document.createElement("span")
parentElement.insertAdjacentElement("beforebegin", nodo)
```

COPIAR DE OTRO chico: Fernando

MIO

```
APPENDCHILD

> const container = document.querySelector('div.py-5.text-center')
> container
<div class=​"py-5 text-center">​…​</div>​

>const h3 = document.createElement('h3')
> container.appendChild(h3)
<h3>​</h3>​
> const texto = document.createTextNode('holita')
> h3.appendChild(texto)
"holita"


APPEND

> container.append('hola 2', document.createElement('div'))



Insert Before:

> const titulo = document.createElement('h1')

> const referencia = document.querySelector('h2')

> referencia
<h2>​Checkout form​</h2>​

> container.insertBefore(titulo, referencia)
<h1>​</h1>​


Importante: El nodo de referencia tiene que ser hijo directo del nodo base.


InsertAdjacentElement

> const referencia = document.querySelector('h2')

> const nodo = document.createElement('span')


Tenemos 4 opciones:

> referencia.insertAdjacentElement('beforebegin', nodo)
<span>​</span>​


> referencia.insertAdjacentElement('afterbegin', nodo)
<span>​</span>​


> referencia.insertAdjacentElement('beforeend', nodo)
<span>​</span>​


> referencia.insertAdjacentElement('afterend', nodo)
<span>​</span>​

```

### Lecturas recomendadas

- [ParentNode.append() - Referencia de la API Web | MDN](https://developer.mozilla.org/es/docs/Web/API/ParentNode/append)