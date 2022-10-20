# Etiqueta img

El elemento HTML ```<img>``` incrusta una imagen dentro de un documento. A continuación, veremos cómo funciona.

La etiqueta ```<img>``` va siempre dentro del contenedor ```<body>```, pues es un elemento visible.

## Funcionamiento de la etiqueta alt:

```html
<img src=“ubicación de la imagen” alt=“descripción de la imagen”>
```

Con esta misma estructura, podemos utilizar el siguiente ejemplo de un estudiante cansado:

```html
<img src=“https://www.ipp.edu.pe/blog/wp-content/uploads/2020/05/shutterstock_1489158410.jpg” alt=“estudiante cansado”>
```

Al añadir el código que acabamos de crear a un documento, la imagen que se mostrará en el navegador es la siguiente:

![](./img/shutterstock_1489158410.jpeg)

## Atributos de la etiqueta img

La etiqueta img cuenta con dos atributos, el atributo "src" y el segundo atributo es "alt". Ambos son importantes.

El atributo de "src" es el recurso de imagen (con la ruta) para mostrar en dónde se encuentra la imagen que vamos a incrustar. Las imágenes se pueden obtener de alguna carpeta o una URL que obtengamos de internet.

- En caso de que el nombre de tu imagen lleve algún espacio, deberás sustituir ese espacio con un guion o guion medio. Caso contrario, el navegador no podrá reconocer la ubicación.

*alt* sirve para agregar una descripción a nuestra imagen. Esto es útil por cuestiones de SEO y también para accesibilidad (por ejemplo para personas con visión reducida).

- ```<img/>```, a diferencia de la gran mayoría de las demás etiquetas de HMTL, no necesita una etiqueta de cierre.
