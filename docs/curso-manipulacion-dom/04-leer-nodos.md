# Leer nodos

Vamos a trabajar con esta página:
https://getbootstrap.com/docs/4.5/examples/checkout/

Básicamente tenemos 4 formas de leer nodos con JS:

- parent.getElementById(‘id’) => nos permite obtener un elemento a través de su id.

- parent.getElementsByClassName(‘class’) => obtiene un array con todos los elementos hijos que tengan esa clase, ojo “getElementByClassName” no existe, es decir no podremos obtener solo 1 elemento con esa clase.

- parent.getElementsByTagName(‘div’) => con este método obtenemos una lista o “array list” con todos los elementos que tengan esa etiqueta, ejemplo todos los divs. Al igual que con el método anterior no hay posibilidad de usarlo en singular, siempre tendremos que usar getElements

- parent.querySelector() => nos permite buscar de 3 formas, con id, clase o tagName. A diferencia de los 2 anteriores este nos devuelve 1 solo elemento, el primero que contenga el valor que se le paso. Id => (’#id’), class => (’.class’), tagName (‘div’)

- parent.querySelectorAll() => este método retorna una array list con todos los elementos que tengan ese selector (id, class o tagName)
Casi siempre el elemento “padre o parent” es document. ya que estamos haciendo referencia a todo el DOM, todo el documento y esto en ciertos casos nos permite evitar errores.
    ejemplo = const button = document.querySelector(’#button)

```
> document.getElementById('firstName');

> document.getElementsByTagName('input');

> document.getElementsByClassName('form-control');

únicamente pasamos el nombre sin el . como cuando definimos una clase en CSS

- Exiten dos selectores más utilizados hoy en día:

> document.querySelector('selector')
Me trae el primer match

> document.querySelector('#address')
<input type=​"text" class=​"form-control" id=​"address" placeholder=​"1234 Main St" required>​

> document.querySelector('input')
<input type=​"text" class=​"form-control" placeholder=​"Promo code">​

> document.querySelector('.form-control')
<input type=​"text" class=​"form-control" placeholder=​"Promo code">​

> document.querySelector('div[class="invalid-feedback"]')
<div class=​"invalid-feedback">​ Valid first name is required. ​</div>​





> document.querySelectorAll('selector')
Me trae todos los elementos que hacen match


> document.querySelectorAll('input')

> document.querySelectorAll('.mb-3')
```