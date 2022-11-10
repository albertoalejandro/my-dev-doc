# Usando la API de internacionalización del browser

PONER MAS BONITO EL CSS usando los archivos del profesor: https://github.com/jonalvarezz/platzi-dom/tree/main/workshop-fetch



Tailwind es un framework de CSS: https://tailwindcss.com/docs/installation

Por ejemplo:

https://tailwindcss.com/docs/font-size


1. Aunque JavaScript nos provee de todas estas formas de controlar estilos, por buenas prácticas y por tener código limpio, es más recomendable usar clases y alternar entre clases que estén escritas en CSS, esto para no mezclar JavaScript y CSS
2. Además de la propiedad className, hay una más interesante llamada classList, esta nos permite añadir y eliminar elementos de forma dinámica fácilmente (útil para cuando queires eliminar o añadir una sola clase de manera dinámica, si usaras className tendrías que volver a escribirlas todas):

// Primero puedes usar clases iniciales (aunque para código limpio lo mejor es definirlas directamente en el HTML)
imagen.className = "h-16 w-16 md:h-24"

// Y ahora podemos usar classList para añadir/borrar dinámicamente
imagen.classList.add("md:w-24") // Añade una clase
imagen.classList.remove("h-16") // Elimina una clase


El profesor hizo un corte repentino y añadió más código sin dejarlo en la sección de archivos y enlaces (muy mal), aquí les dejo el enlace a mi repositorio que sí contiene todo el código con las clases y los estilos incluidos que uso el profesor:
[Adición del API de internacionalización](https://github.com/RetaxMaster/curso-manipulacion-dom/tree/5a883a469dd4c367c5568558cac4d94dac78d08c)


Lecturas recomendadas:
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl

---------

1. Aunque JavaScript nos provee de todas estas formas de controlar estilos, por buenas prácticas y por tener código limpio, es más recomendable usar clases y alternar entre clases que estén escritas en CSS, esto para no mezclar JavaScript y CSS
2. Además de la propiedad className, hay una más interesante llamada classList, esta nos permite añadir y eliminar elementos de forma dinámica fácilmente (útil para cuando queires eliminar o añadir una sola clase de manera dinámica, si usaras className tendrías que volver a escribirlas todas):

```
// Primero puedes usar clases iniciales (aunque para código limpio lo mejor es definirlas directamente en el HTML)
imagen.className = "h-16 w-16 md:h-24"

// Y ahora podemos usar classList para añadir/borrar dinámicamente
imagen.classList.add("md:w-24") // Añade una clase
imagen.classList.remove("h-16") // Elimina una clase
```

1. El profesor hizo un corte repentino y añadió más código sin dejarlo en la sección de archivos y enlaces (muy mal), aquí les dejo el enlace a mi repositorio que sí contiene todo el código con las clases y los estilos incluidos que uso el profesor:
Adición del API de internacionalización: https://github.com/RetaxMaster/curso-manipulacion-dom/tree/5a883a469dd4c367c5568558cac4d94dac78d08c

### 

- [Intl - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)