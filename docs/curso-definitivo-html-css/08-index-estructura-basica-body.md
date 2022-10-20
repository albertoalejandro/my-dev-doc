# Index y su estructura básica: body

*body* es la etiqueta que identifica la parte visible de nuestro sitio web. Dentro del body, se añadirán las etiquetas para marcar los elementos visuales del sitio web, como logotipo, menús de navegación, contenido principal, entre otrs. [Es muy importante usar HTML semántico](https://platzi.com/clases/1802-accesibilidad-web/26072-que-es-el-html-semantico-y-por-que-es-importante/) y no llenar todo de ```<div>``` para que nuestro sitio sea mejor interpretado por el navegador y, por lo tanto, más accesible.

## Etiquetas del cuerpo del documento (body):

- **article**: diferencia partes del contenido que pueden vivir por sí mismas.
- **nav**: para hacer menús de navegación.
- **aside**: contenido menos relevante, como publicidad, etc.
- **section**: sirve para diferenciar las secciones principales del contenido.
- **header**: cabecera del documento.
- **footer**: pie de página del documento.
- **h1 - h6**: títulos de nuestro sitio web.
- **table**: tablas de contenidos, similar a la estructura de las hojas de calculo.
- **ul y ol**: listas de items.
- **div**: cualquier división para organizar el contenido.
- **h1 a h6**: son etiquetas para indicar títulos con un estilo que destaca del resto.
- **article**: es la parte de nuestro contenido que puede vivir por sí mismo. Pueden haber tantos artícle como proyectos o eventos tenga nuestro portafolio.
- **p**: define el texto de un párrafo.
- **small**: aplica una apariencia de texto reducido en tamaño.
- **strong**: aplica al texto un formato de negritas.
- **a**: corresponde a un ancla o enlace a una url interna o externa del documento.
- **img**: con esta etiqueta podemos enlazar imágenes en el documento.
- **figure**: le da un contexto semántico a las imágenes.

## Ejemplo de un body con etiquetas semánticas HTML.

```html
<body>

    <header> <!--Sección superior de nuestro website--> 

      <nav></nav> <!--Sección de navegación de nuestro website, siempre dentro del header-->

    </header>

    <main> <!--Main es el contenido central de nuestro website, "la parte del medio"-->

      <section> 
        <!--Nuestro website puede estar divido por secciones, por ejemplo platzi tiene 3: El navegador de cursos y rutas, el feed y nuestras rutas de aprendizaje-->

        <article>
          <!--Contenido independiente de la página. Es reutilizable-->
        </article>

      </section>

      <ul> <!--Lista desordenada: Sin numerar-->

        <li><!--Item List. Elementos de la lista--></li>

      </ul>

      <ol></ol> <!--Lista ordenada: Numerada-->
      
    </main>

    <footer> <!--Sección final de nuestro website-->

    </footer>

    <p>Soy un texto</p> <!--Párrafo, texto-->

    <h1>Soy un titulo</h1> 
    <!--Títulos, muestran el texto más grande y con negrilla. Existen desde el h1 al h6-->

    <a href="#">Soy un link</a>
    <!--Enlaces/links que nos permitirán movernos entre páginas.-->

  </body>
```

## MIS NOTAS

- **Etiquetas contenedoras**: van a llevar más etiquetas adentro y nos ayudarán a generar la estructura de nuestra página. Por ejemplo:
 header, ..., div.

- **Etiquetas de contenidos**: son las etiquetas que llevarán texto, imágenes, vídeos, ... o cualquier cosa que se va a reenderizar en el proyecto.

*Nota: Tenemos que utilizar HTML semántico, las etiquetas tienen que ir dónde tienen que ponerse. No es buena práctica llenar todo de ```<div>```.*
