# Tipos de imágenes

Las imágenes representan una pieza fundamental al momento de mostrar contenido para web. Aquí conoceremos los principales tipos de imágenes web y sus formatos.

## Tipos de imágenes para web

### Lossless (sin pérdida):

- Capturan todos los datos del archivo original.
- No se pierde nada del archivo original.
- Puede comprimirse, pero podrá reconstruir su imagen al estado original.

### Lossy (con pérdida):

- Se aproximan a su imagen original.
- Podría reducir la cantidad de colores en su imagen o analizar la imagen en busca de datos innecesarios.
- Por consiguiente puede reducir su tamaño, lo que mejora el tiempo de carga de la página, pero pierde su calidad.
- Los archivos tipo *lossy* son mucho más livianos que los archivos tipo *lossless*, por lo que son ideales para usar en sitios en donde el tamaño del archivo y la velocidad de descarga son importantes.

![Tabla de diferencias](./img/table-for-different-images.webp)

## Formatos de imagen para web

- **GIF** (Graphics Interchange Format): Formato de imagen sin pérdida, no se puede comprimir
- **PNG 8** (Portable Network Graphics): Formato de imagen sin pérdida, uso de colores de 256, se utiliza para logotipos e iconos para la página. Los PNG pueden tener fondo transparente.
- **PNG 24** (Portable Network Graphics): Formato de imagen sin pérdida, utilización de colores ilimitados, alta calidad, si intentamos comprimir no ayudará demasiado por la gran cantidad de colores. Formato más pesado que GIF y PNG 8.
- **JPG / JPEG** (Photographic Experts Group): Formato de imagen con pérdida, perdemos calidad a la hora de comprimirlas, pero llegan a ser óptimas para la carga en la página web. Es para fotografías. Suelen ser imágenes grandes, la imagen pesará menos para renderizarlas rápidas.
- **SVG - Vector** (Scalable Vector Graphics): Formato de imagen muy ligero sin pérdida, con svg no perdemos calidad, ya que está compuesta por vectores. Es un formato muy ligero para iconos o logotipos hechos para escalar. Por ejemplo, para pantallas de retina. Hay un algoritmo matemático para que no pierda calidad ni se pixele.
- **WebP**: Es un formato gráfico en forma de contenedor que sustenta tanto compresión con pérdida como sin ella. ​​Fue desarrollado por Google.