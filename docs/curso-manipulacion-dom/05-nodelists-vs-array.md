# NodeLists vs Array

La diferencia entre NodeList y Array, es que el NodeList carece de métodos que si están disponibles en los Arrays, pero podemos pasar esto fácilmente usando el operador de propagación.

// De esta forma pasamos todos los elementos en el NodeList a un arreglo al cual si podremos usar los métodos filter, map, reduce entre otros. 
const nodeList = document.querySelectorAll("selector css");
const elementList = [...nodeList];

Recomendación importante cada vez que obtengamos un NodeList pásemelo a Array ya que los motores de javascript como el motor V8 de google están mas optimizados para Arrays que para NodeList.

```
> const nodeList = document.querySelectorAll('div')

> nodeList.length

> nodeList.forEach


lo demás métodos como .map, .some, .filter, .reduce   no existen


pero para transformar un NodeList a Array:

const nodeListAsArray = [...nodeList]
```

Otros:

La diferencia entre NodeList y Array, es que el NodeList carece de métodos que si están disponibles en los Arrays, pero podemos pasar esto fácilmente usando el operador de propagación.

```javascript
// De esta forma pasamos todos los elementos en el NodeList a un arreglo al cual si podremos usar los métodos filter, map, reduce entre otros. 
const nodeList = document.querySelectorAll("selector css");
const elementList = [...nodeList];
```

*Recomendación importante cada vez que obtengamos un NodeList pásemelo a Array ya que los motores de javascript como el motor V8 de google están mas optimizados para Arrays que para NodeList.*

Otro

En clases anteriores les dije que devolvía un array y entre paréntesis le ponía que realmente era un NodeList, esto fue para que se hicieran una idea de qué era lo que devolvía, NodeList, aunque no es un array, se comporta muy similar, y es muy importante comprender la diferencia porque luego los empezamos a manejar como arrays y nos preguntamos por qué no funciona.

Una de las formas de convertirlos a array es la vista en la clase:

```
const nodeListArray = [...nodeList]
```

Sin embargo, a mi me gusta más está forma y es más legible:
```
const nodeListArray = Array.from(nodeList)
```

De esas formas podemos obtener un arreglo a partir de un NodeList (o cualquier objeto iterable) 👀

