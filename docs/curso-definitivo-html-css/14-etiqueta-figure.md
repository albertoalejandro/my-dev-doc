# Etiqueta figure

*Figure* es una etiqueta que permite almacenar una imagen en su interior. Es una mejor práctica comparada con usar solamente un contenedor *div*. Como complemento al contenedor *figure*, se utiliza la etiqueta *figcaption*, que permite darle una pequeña descripción a la imagen, como el autor, fuente o algo por el estilo, que se mostrará usualmente abajo de la imagen.

*Figcaption* se diferencia del atributo *Alt* porque esta última muestra su descripción en texto en el navegador solamente al pasar el mouse por encima de la imagen (de ahí su utilidad para personas con discapacidad visual).

Es importante considerar que la etiqueta *figure* no es únicamente para imágenes: [El elemento HTML](https://platzi.com/clases/1802-accesibilidad-web/26072-que-es-el-html-semantico-y-por-que-es-importante/)

representa contenido independiente, a menudo con un título. Por lo general, se trata de una imagen, una ilustración, un diagrama, un fragmento de código, o un esquema al que se hace referencia en el texto principal, pero que se puede mover a otra página o a un apéndice sin que afecte al flujo principal.

*figure* es una etiqueta contenedora.

## Ejemplo de etiqueta Figure:

```html
<figure>
    <img
        src="./pics/tinified/small.jpg"
        alt="Es una imagen de un perrito"
    />
    <figcaption>Es una imagen de un perrito</figcaption>  
</figure>
```