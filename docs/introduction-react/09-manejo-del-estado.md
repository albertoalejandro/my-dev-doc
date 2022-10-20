# Manejo del estado

El estado en React nos ayuda a crear **datos mutables** o datos que pueden ser modificados.

Para manejar el estado depende del si nuestro componente es generado con una clase o si es un componente funcional.

- **Clase:** Para manejar el estado dentro de una clase podemos crearlo en el constructor de la clase, y para actualizarlo utilizamos el **setter** *setState*.

- **Función:** Si estamos en un componente funcional podemos utilizar el hook de estado, que nos regresará arreglo con un **getter** (que será el valor de nuestro estado) y un **setter** (una función para actualizar el estado).

## ¿Qué son los Hooks?

Los **Hooks** son funciones que te permiten **enganchar** el estado de React y el ciclo de vida desde componentes funcionales, entre muchas otras cosas. Nos permiten usar React sin clases.

## Estado en componentes clase

Para manejar el estado en componentes clase necesitamos crearlo como una propiedad dentro de nuestro componente clase, usamos *this.state*, y para actualizar el estado, la clase de React ya tiene un setter: *this.setState*. (Dentro de este tipo de componentes no se pueden usar los hooks).

```jsx
class Component extends React.Component {
    constructor(){
        this.state = {
            patito: '👍'
        }
    }
    
    render(){
        return (
            <button onClick={()=>this.setState("Has dado un like")}>{this.state.patito}</button>
        )
    }
}
```

## Estado en componentes funcionales

El manejo del estado en estos componentes es mucho más sencillo, utilizando el **hook de estado**.

Podemos importar este hook directamente de React o desestructurándolo de React:

```jsx
import React from 'react';

function Component() {
    const [count, setCount] = React.useState("");
}
```

```jsx
import { useState } from 'react';

function Component() {
    const [count, setCount] = useState("");
}
```

Una vez lo importamos ya podemos usarlo en nuestro componente, este hook nos regresará un array con dos elementos:

1. El valor de nuestro estado **(Getter)**.
2. La función que se ocupa de actualizar nuestro estado **(Setter)**.

También podemos pasarle un valor inicial a nuestro estado dentro de los paréntesis.
Por ejemplo, en el buscador de nuestra aplicación,

```jsx
import React from 'react';
import './TodoSearch.css';

function TodoSearch() {
  const [searchValue, setSearchValue] = React.useState('');
  
  const onSearchValueChange = (event) => {
    console.log(event.target.value);
    setSearchValue(event.target.value);
  };

  return [
    <input
      className="TodoSearch"
      placeholder="Cebolla"
      value={searchValue}
      onChange={onSearchValueChange}
    />,
    <p>{searchValue}</p>
  ];
}

export { TodoSearch };
```

## Tipos de componentes

**Stateful:** son componentes que tienen declaración de estado en su función.

**Stateless:** son componentes que no tienen ningún tipo de estado declarado en el cuerpo de la función.

## Lecturas recomendadas

- [Using the State Hook](https://reactjs.org/docs/hooks-state.html)
- [Curso de React.js: Manejo Profesional del Estado](https://platzi.com/cursos/react-estado/)