# Aplicando Lazy loading

Los atributos data-cualquiercosa sirven para definir atributos personalizados dentro de HTML, es decir, puedes inventarte atributos, yo los he usado desde siempre porque son muy útiles para pasar datos entre HTML y JavaScript, su sintaxis consta en que SIEMPRE deben iniciar con data- y después de eso puedes poner cualquier cosa: data-este-es-un-atributo-data-personalizado, y se pueden usar de esta manera:

````
<div id="myDiv" data-atributo="hola" data-un-atributo="el-valor-del-atributo">Hola 😄</div>
````

e esta forma podemos tener atributos personalizados en HTML:
.
Atributos personalizados en HTML5, más datos con un simple “data-…”https://www.genbeta.com/desarrollo/atributos-personalizados-en-html5-mas-datos-con-un-simple-data
.
La forma de acceder a estos elementos desde JavaScript es mediante la propiedad dataset, esta propiedad contiene la lista de todos los atributos personalizados que le pusiste a tu elemento:

````
const atributo = myDiv.dataset.atributo; // hola
````

Para los atributos que tienen más de un guion, JavaScript es inteligente y los convierte a camel case 🐫:

````
const unAtributo = myDiv.dataset.unAtributo; // el-valor-del-atributo
````


