# Index y su estructura básica: head

El archivo *index.html* va a ser la página inicial que el servidor va a buscar como página de inicio cuando va a iniciar un proyecto. Si no existe, habría que decirle al servidor cuál debe ser la página de inicio.

```<!DOCTYPE html>``` : le dice al navegador que es HTML5.

```<html lang="">```: indicamos al navegador con este atributo en qué lenguaje viene el contenido.

```<head>``` : esta etiqueta no lo verá el usuario. Irá todo lo que es importante para que el navegador cargue el proyecto, dependencias, librerías externas, CSS, fuentes ...

```<body>``` : esta etiqueta lo verá el usuario. Irán las cosas interactivas de nuestro proyecto: texto, imágenes, vídeos ...

```<meta charset="UTF-8">``` : para que el navegador pueda entender caracteres especiales.

```<meta name="description" content="">``` : servirá para la parte de SEO. Dará más información al usuario cuando busque algo. Indicará de qué es la página.

```<meta name="robots">``` : autorizamos a los robots de los buscadores para colocar nuestra página para cuando se hagan búsquedas (buscador de google y otros).

```<meta name="viewport" content="width=device-width, inictial-scale=1.0">``` : para hacer responsive el proyecto, para que se escale el texto y las imágenes.

```<link rel="stylesheet" href="./css/style.css">``` : anexamos los estilos.