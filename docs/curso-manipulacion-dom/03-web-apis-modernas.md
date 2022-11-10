# Web APIs modernas

DOM + JavaScript = Web API

Una Web API: Nos permite conectar el dom con JavaScript

¿Qué rayos son las API?

Puede parecernos un concepto muy abstracto o confuso al principio, ya que como dice el profesor ‘’lo utilizamos sin discreción para referirnos a todo’’. Pero, en pocas palabras, una API es todo lo que sirva para comunicar fácilmente un pedazo de software con otro.

APIs de terceros
Twitter, por ejemplo, nos proporciona una manera sencilla de mostrar tweets de algún usuario a través de su API. Tan solo tenemos que hacer una petición GET al siguiente Endpoint:

GET https://api.twitter.com/2/users/:id/tweets

APIs de servicios
Si quisieramos mostrar mapas de Google Maps, tambien podriamos hacerlo a través de su API.

Por ejemplo, para mostrar la ubicación de Sydney, New South Wales, Australia, lo haríamos de la siguiente manera:

```javascript
function initMap() {
  map = new google.maps.Map(document.getElementById("map"), {
    center: { lat: -34.397, lng: 150.644 },
    zoom: 8,
  });
}
```

## Conclusión

Si prestamos atención, nos damos cuenta de que son una manera sencilla de acceder a información o funcionalidades de otro pedazo de código. Es por eso que se les llama ‘’intermediarios’’ o ‘’puentes’’.

Si tienes algún otro ejemplo de APIs coméntalo o si dije alguna imprecisión corrígeme con confianza. Estamos para ayudarnos compañeros,** nunca paren de aprender.**


OTRO

Web APIs modernas
<h4>Ideas/conceptos claves</h4>
API ⇒ Es un puente 🌉

<h4>Recursos</h4>
MDN Web Docs

Can I use… Support tables for HTML5, CSS3, etc

<h4>Apuntes</h4>
DOM + JS = Web API
Una web API nos permite conectar el JS con el DOM para poder manejarlo (leer y modificar)
Actualmente existen más de 70 web APIs, Dom es solo una de ellas

- ya existen diferentes propósitos
    Animaciones
    Drag & Drop
    Transmisión de video con web RTC
    Manejo de videojuegos como ser con WebGL
    Incluso pagos sin necesidad de otro servicio

- Debemos hacernos dos preguntas al momento de usar las APIs
    ¿Como lo uso?
        MDN contiene bastante información acerca de las webs APIs

**¿Puedo usarlo?**
No todas las webs API’s estarán soportadas por todos los navegadores entonces podemos usar caniuse
Chrome tiene bastante compatibilidad con nuevas APIs

**RESUMEN**: Para manejar el DOM mediante JS se debe tomar en cuenta que estaremos usando una web API, cada vez que usemos una de ellas debemos tomar en cuenta dos preguntas de cómo usarlo y si se puede implementar en todos los navegadores o usuarios que deseemos llegar


OTRO

Resumen de la Clase 👌👌
Web Apis Modernas

Una WEB API nos permite conectar el DOM con Javascript para que nosotros podamos (leerlo y modificarlo), actualmente existen mas de 70 web APIS y el DOM solo es una de ellas

Pero existen algunas de ella para hacer:

    Animaciones
    Drag & Drog
    Manejar de Archivos
    Trasmisión de video con web RTC
    Manejo de videojuegos como ser con OpenGL
    Incluso para manejo de pagos, sin necesidad de contar con librerías o servicios externos.

Recursos que debemos tener en cuenta al momento de usar APIS

¿Como lo uso? → developer mozilla org

Podremos encontrar bastante información sobre Frontend cuando la necesitamos

¿Puedo usarlo? → caniuse

También tenemos que tener en cuenta que la API que vayamos a usar este soportada por los navegadores, entonces caniuse podrá ayudarnos a saber sobre la compatibilidad que hay.

Chrome tiene compatibilidad con la mayoría de APIS y también de las mas recientes.