# Custom Hook para Local Storage

Algo super interesante de React es que podemos crear **hooks personalizados** para ejecutar procesos para manejar información sin que afecte a otros componentes, lo que haremos será abstraer nuestra lógica de localStorage para manejarla dentro de nuestro propio **hook**.

### Reglas para crear un custom hook:

1. Nuestro hook personalizado debe empezar por **use**, por ejemplo: *usePatito, useTodos o useUnicornio*.
2. **No anidar hooks** en loops u otros bloques.
3. Llamar dentro de componentes de React o hooks propios, nunca dentro de funciones normales.

## Creando nuestro Custom Hook

El objetivo de un custom hook es **reutilizar código**, entonces este hook debería poder funcionar para guardar cualquier tipo de dato en el localStorage.

Primero necesitamos analizar que **parámetros** necesita tener nuestro custom hook:

1. Un nombre para el item en nuestro localStorage.
2. Un estado inicial.

También tenemos que regresar algunos datos para que nuestro hook sea funcional:

1. Los datos actuales de nuestro ítem en el localStorage.
2. Una función para actualizar los datos de este ítem.

¡Ahora que sabemos qué tenemos que hacer, podemos empezar a crear nuestro custom hook!

```jsx
// Recibimos como parámetros el nombre y el estado inicial de nuestro item.
function useLocalStorage(itemName, initialValue) {
  // Guardamos nuestro item en una constante
  const localStorageItem = localStorage.getItem(itemName);
  let parsedItem;
  
  // Utilizamos la lógica que teníamos, pero ahora con las variables y parámentros nuevos
  if (!localStorageItem) {
    localStorage.setItem(itemName, JSON.stringify(initialValue));
    parsedItem = initialValue;
  } else {
    parsedItem = JSON.parse(localStorageItem);
  }
  
  // ¡Podemos utilizar otros hooks!
  const [item, setItem] = React.useState(parsedItem);

  // Actualizamos la función para guardar nuestro item con las nuevas variables y parámetros
  const saveItem = (newItem) => {
    const stringifiedItem = JSON.stringify(newItem);
    localStorage.setItem(itemName, stringifiedItem);
    setItem(newItem);
  };

  // Regresamos los datos que necesitamos
  return [
    item,
    saveItem,
  ];
}
```

Ahora que hemos creado nuestro custom hook podemos usarlo las veces que queramos.
¡Vamos a añadirlo a la lógica de nuestra aplicación!

```jsx
import React from 'react';
import { AppUI } from './AppUI';

// const defaultTodos = [
//   { text: 'Cortar cebolla', completed: true },
//   { text: 'Tomar el cursso de intro a React', completed: false },
//   { text: 'Llorar con la llorona', completed: true },
//   { text: 'LALALALAA', completed: false },
// ];

function useLocalStorage(itemName, initialValue) {
  const localStorageItem = localStorage.getItem(itemName);
  let parsedItem;
  
  if (!localStorageItem) {
    localStorage.setItem(itemName, JSON.stringify(initialValue));
    parsedItem = initialValue;
  } else {
    parsedItem = JSON.parse(localStorageItem);
  }

  const [item, setItem] = React.useState(parsedItem);

  const saveItem = (newItem) => {
    const stringifiedItem = JSON.stringify(newItem);
    localStorage.setItem(itemName, stringifiedItem);
    setItem(newItem);
  };

  return [
    item,
    saveItem,
  ];
}

function App() {
  // Desestructuramos los datos que retornamos de nuestro custom hook, y le pasamos los argumentos que necesitamos (nombre y estado inicial)
  const [todos, saveTodos] = useLocalStorage('TODOS_V1', []);
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
    saveTodos(newTodos);
  };

  const deleteTodo = (text) => {
    const todoIndex = todos.findIndex(todo => todo.text === text);
    const newTodos = [...todos];
    newTodos.splice(todoIndex, 1);
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
    />,
  );
}

export default App;
```

Ahora nuestro código está mucho mejor organizado, si queremos tener aún más control de nuestro proyecto, incluso podemos crear una carpeta para hooks, y luego poder importarlos a cualquier parte de nuestro proyecto.

¡Te retamos a que lo hagas!

## Lecturas recomendadas

- [Rules of Hooks](https://reactjs.org/docs/hooks-rules.html)
- [Building Your Own Hooks](https://reactjs.org/docs/hooks-custom.html)