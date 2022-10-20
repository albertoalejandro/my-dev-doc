# Persistencia de datos con Local Storage

Las aplicaciones web tienen tanto front-end como back-end, en **front-end** se encarga de la parte visual e interactuar con los usuarios, así como de conectarse con el **back-end**, en donde se maneja la autenticación, el almacenamiento de datos en bases de datos, esta es una manera muy utilizada para la persistencia de datos.

También es posible la persistencia de datos sin necesidad del back-end, utilizando la **API de almacenamiento web**, el **localStorage**, que nos permite almacenar datos localmente en el navegador, que persistirán incluso si el usuario recarga la página o cierra el navegador.

Además, existe otra forma de almacenar datos, aunque no es persistente, se llama **sessionStorage**, se utiliza exactamente igual que **localStorage**, la diferencia es que los datos en localStorage son persistentes.

## Local Storage

Nos permite guardar datos persistentes en el navegador del usuario, que podremos acceder, modificar y hasta eliminar, para esto **localStorage** tiene varios métodos.

- Guardar datos: setItem(nombre, dato)
- Acceder a datos: getItem(nombre)
- Borrar un dato: removeItem(nombre)
- Eliminar todos los datos: clear(nombre)

Es muy importante saber que **localStorage** solamente puede guardar texto, no objetos, arreglos, números, solo strings para esto podemos utilizar unos métodos de JSON:

- Convertir a texto: JSON.stringify()
- Convertir a JavaScript: JSON.parse()

## Local Storage en ToDo App

Para crear la lógica de nuestro almacenamiento local, antes de acceder a nuestro ítem, debemos tener en cuenta que nuestro usuario puede ser nuevo y no tener ningún TODO creado, en este caso necesitaríamos crear un arreglo vacío, si el usuario ya tiene TODOs creados, deberíamos obtener sus TODOs del **localStorage**.

```jsx
import React from 'react';
import { AppUI } from './AppUI';

function App() {
    // Traemos nuestros TODOs almacenados
  const localStorageTodos = localStorage.getItem('TODOS_V1');
  let parsedTodos;

  if (!localStorageTodos) {
    // Si el usuario es nuevo no existe un item en localStorage, por lo tanto guardamos uno con un array vacío
    localStorage.setItem('TODOS_V1', JSON.stringify([]));
    parsedTodos = [];
  } else {
    // Si existen TODOs en el localStorage los regresamos como nuestros todos
    parsedTodos = JSON.parse(localStorageTodos);
  }

  // Guardamos nuestros TODOs del localStorage en nuestro estado
  const [todos, setTodos] = React.useState(parsedTodos);
  const [searchValue, setSearchValue] = React.useState('');

  const completedTodos = todos.filter(todo => !!todo.completed).length;
  const totalTodos = todos.length;

  let searchedTodos = [];

  if (!searchValue.length >= 1) {
    searchedTodos = todos;
  } else {
    searchedTodos = todos.filter(todo => {
      const todoText = todo.text.toLowerCase();
      const searchText = searchValue.toLowerCase();
      return todoText.includes(searchText);
    });
  }

  const completeTodo = (text) => {
    const todoIndex = todos.findIndex(todo => todo.text === text);
    const newTodos = [...todos];
    newTodos[todoIndex].completed = true;
    setTodos(newTodos);
  };

  const deleteTodo = (text) => {
    const todoIndex = todos.findIndex(todo => todo.text === text);
    const newTodos = [...todos];
    newTodos.splice(todoIndex, 1);
    setTodos(newTodos);
  };
  
  return (
    <AppUI
      totalTodos={totalTodos}
      completedTodos={completedTodos}
      searchValue={searchValue}
      setSearchValue={setSearchValue}
      searchedTodos={searchedTodos}
      completeTodo={completeTodo}
      deleteTodo={deleteTodo}
    />
  );
}

export default App;
```
Todavía no creamos la lógica para agregar nuevos TODOs, pero si probamos añadiendo TODOs de prueba en nuestro localStorage, ya debería funcionar todo bien, o al menos a simple vista. Cuando interactuamos con nuestra aplicación, completando o eliminando TODOs todavía no se ve reflejado en nuestro localStorage.

Para lograr esto, crearemos una función puente, entre nuestra función que actualiza nuestro estado para actualizar nuestro localStorage.

```jsx
import React from 'react';
import { AppUI } from './AppUI';

function App() {
  const localStorageTodos = localStorage.getItem('TODOS_V1');
  let parsedTodos;

  if (!localStorageTodos) {
    localStorage.setItem('TODOS_V1', JSON.stringify([]));
    parsedTodos = [];
  } else {
    parsedTodos = JSON.parse(localStorageTodos);
  }

  const [todos, setTodos] = React.useState(parsedTodos);
  const [searchValue, setSearchValue] = React.useState('');

  const completedTodos = todos.filter(todo => !!todo.completed).length;
  const totalTodos = todos.length;

  let searchedTodos = [];

  if (!searchValue.length >= 1) {
    searchedTodos = todos;
  } else {
    searchedTodos = todos.filter(todo => {
      const todoText = todo.text.toLowerCase();
      const searchText = searchValue.toLowerCase();
      return todoText.includes(searchText);
    });
  }
  
  // Creamos la función en la que actualizaremos nuestro localStorage
  const saveTodos = (newTodos) => {
    // Convertimos a string nuestros TODOs
    const stringifiedTodos = JSON.stringify(newTodos);
    // Los guardamos en el localStorage
    localStorage.setItem('TODOS_V1', stringifiedTodos);
    // Actualizamos nuestro estado
    setTodos(newTodos);
  };

  const completeTodo = (text) => {
    const todoIndex = todos.findIndex(todo => todo.text === text);
    const newTodos = [...todos];
    newTodos[todoIndex].completed = true;
    // Cada que el usuario interactúe con nuestra aplicación se guardarán los TODOs con nuestra nueva función
    saveTodos(newTodos);
  };

  const deleteTodo = (text) => {
    const todoIndex = todos.findIndex(todo => todo.text === text);
    const newTodos = [...todos];
    newTodos.splice(todoIndex, 1);
    // Cada que el usuario interactúe con nuestra aplicación se guardarán los TODOs con nuestra nueva función
    saveTodos(newTodos);
  };
  
  return (
    <AppUI
      totalTodos={totalTodos}
      completedTodos={completedTodos}
      searchValue={searchValue}
      setSearchValue={setSearchValue}
      searchedTodos={searchedTodos}
      completeTodo={completeTodo}
      deleteTodo={deleteTodo}
    />
  );
}

export default App;
```

No fue tan complicado, ¿Verdad?

Pero ahora tenemos demasiado código en nuestro archivo *App.js* eso no es bueno, debemos de intentar separar la lógica para que sea más fácil de leer y esté mejor organizado.

## MIS NOTAS

localStorage sólo puede guardar texto.

```
JSON.stringify() -> nos permite transformar en texto cualquier objeto que tengamos en JavaScript

const ejemplo = JSON.stringify([{text: 'todos', completed: false}])

JSON.parse(ejemplo)
```

```
localStorage.setItem('ejemplotodos', ejemplo)

localStorage.getItem('ejemplotodos')

JSON.parse(localStorage.getItem('ejemplotodos'))
```