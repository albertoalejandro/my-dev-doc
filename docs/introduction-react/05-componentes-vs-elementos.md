
# JSX: componentes vs. elementos (y props vs. atributos)

JSX es una extensión de JavaScript creada por Facebook para usarse con React.js. Nos presenta muchas ventajas el trabajar con elementos y componentes muy similar a la sintaxis de HTML.

La función que JSX tiene es de ser un preprocesador y transformar el código a JavaScript.

💡 JSX es solamente azúcar sintáctica para el método *React.createElement(component, props, ...children)* de React.

**Nota:** dentro del código encontrarás comentarios que explicarán que es lo que se está añadiendo o algunos consejos.

## ¿Cómo crear un componente?

Existen varias formas de crear un componente en React, por convención siempre los creamos utilizando **PascalCase** (La primera letra de cada palabra en mayúscula y juntas).

### Crear un componente con clases

Este es el modo que se empleaba antes, ahora ya casi nadie la utiliza, pero es bueno saber cómo funciona, por si llegamos a trabajar con proyectos que las usen, con el método render podemos renderizar el JSX que retorna nuestra clase.

```jsx
class Componente extends React.Component {
	render() {
		return (
		    // JSX
		)
	}
}
```

Podemos agregar JSX entre los paréntesis del *return*.

### Crear un componente con funciones

Los componentes funcionales son los más utilizados hoy en día, ya que nos permiten controlar el ciclo de vida mucho más fácil con los [hooks de React](https://platzi.com/cursos/react-hooks/):

```jsx
function Component() {
    return (
        // JSX
    )
} 

// Utilizando arrow function
const Component = () => {
    return(
        // JSX
    )
}
```

## Componentes vs. Elementos

Los componentes son invisibles para HTML, pero no para React, de hecho React utiliza los componentes para renderizar, y optimizar los re-renderizados.

### Componente

Un componente es una pieza de código que describe una parte reutilizable de la interfaz, recibe propiedades y retornan elementos, dentro de los componentes podemos utilizar variables de JavaScript con ayuda de las llaves *{}*.

```jsx
const Component = () => {
    const titulo = Soy un título;
    
    return(
        <h1>{titulo}h1>
    )
}
```

### Elemento

Un elemento es lo que devuelve un componente, es una representación de un nodo en el DOM.

```jsx
<h1>Soy un título<h1>
```

## Propiedades vs. Atributos

La diferencia principal es que un atributo no se puede modificar y una propiedad si, ya que los atributos son de HTML y las propiedades son de JavaScript.

### Atributo

Los atributos los pueden tener las etiquetas de HTML.

```jsx
<h1 class="titulo">Soy un título<h1>
```

### Propiedad

Las propiedades las pueden recibir los elementos y componentes en React.

```jsx
const Component = () => {
    return(
        <h1 className="titulo">
            Soy un titulo
        <h1>
    )
}
```

Es importante notar que algunos atributos de HTML se escriben diferente como propiedades, por ejemplo; el atributo *class* de HTML no se debe utilizar como propiedad de una clase o elemento de React, ya que *class* es una palabra reservada para crear clases en JavaScript, en su lugar utilizamos *className*.

## Pasando propiedades a nuestros componentes

Algo mágico de React es que podemos pasarle propiedades a nuestros componentes.

```jsx
// Le pasamos la propiedad saludo
<"Oli" />
```

```jsx
// Recibimos las propiedades

const Componente = (props) => {
    return(
        {/* ¡Así creamos un comentario en JSX! */}
        {/* Accedemos a saludo desde las props */}
        {props.saludo} 
        {/* props.saludo = Oli */}
    )
}
```

## Propiedad children

También podemos utilizar los componentes de React como etiquetas abiertas, para pasarle contenido, elementos o incluso otros componentes, la manera de acceder a ellos es con la propiedad especial *children*.

```jsx
¡Soy un título anidado!
```

```jsx
const Componente = (props) => {
    return(
        <div className="titulo">
            {props.children}
            {/* props.children = <h1>¡Soy un título anidado!h1> */}
        div>
    )
}

```

## MIS NOTAS

Los componentes son invisibles para HTML pero son visibles para React. Lo que renderiza en HTML son los elementos.

```jsx
<App saludo="Oli" />
```
saludo es una propiedad del componente App

hay una propiedad especial: children

```jsx
<App>
-> aquí saldrá todo lo que pongamos aquí
</App>
```

props.children

## Lecturas recomendadas

- [JSX In Depth](https://reactjs.org/docs/jsx-in-depth.html)
- [Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)
- [Curso intro react](https://github.com/platzi/curso-intro-react/tree/1dbecf33188913424ec8d85784f1860ac047898c)
- [Introducción a la nueva transformación de JSX](https://es.reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html)