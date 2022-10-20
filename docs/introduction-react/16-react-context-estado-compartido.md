# React Context: estado compartido

Es una forma de **tener acceso a datos** a través del árbol de componentes **sin tener que pasar props manualmente** en cada nivel, usando datos globales.

Para esto tenemos un proveedor que envolverá a todos los componentes que serán los consumidores de nuestro contexto.

Fases:

1. **Crear** el contexto de nuestra aplicación.
2. **Proveer** nuestro contexto con los datos que queremos globales.
3. **Consumir** los datos desde cualquier parte de nuestra aplicación.

## Creando el contexto de nuestra aplicación

Primero necesitamos crear nuestra carpeta *TodoContext*, aunque también en muchos proyectos crean una carpeta *context* aparte, en donde tendrán todo el contexto de su aplicación.

Es importante crear el contexto con *createContext*, ya que este nos regresará dos componentes: proveedor y consumidor.

## TodoContext/index.js

```jsx
import React from 'react';
import { useLocalStorage } from './useLocalStorage';

// Al crear el contexto también podemos pasarle un valor inicial entre los paréntesis
const TodoContext = React.createContext();

function TodoProvider(props) {
  // Nos traemos todo el estado y las funciones de nuestra aplicación que queremos globales
  const {
    item: todos,
    saveItem: saveTodos,
    loading,
    error,
  } = useLocalStorage('TODOS_V1', []);
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
  
  // Retornamos nuestro proveedor con nuestro contexto en la etiqueta value, que recibirá a toda nuestra aplicación, por eso necesitamos la prop children
  return (
    <TodoContext.Provider value={{
      loading,
      error,
      totalTodos,
      completedTodos,
      searchValue,
      setSearchValue,
      searchedTodos,
      completeTodo,
      deleteTodo,
    }}>
      {props.children}
    </TodoContext.Provider>
  );
}

// Exportamos nuestro proveedor y nuestro contexto, en el context también esta el consumer, para acceder a nuestro contexto
export { TodoContext, TodoProvider };
```
Los componentes que consumen el contexto deben estar envueltos en la etiqueta proveedora.

## App/index.js

Ahora importamos nuestro proveedor para envolver nuestra aplicación:

```jsx
import React from 'react';
import { TodoProvider } from '../TodoContext';
import { AppUI } from './AppUI';


function App() {
  return (
    <TodoProvider>
      <AppUI />
    </TodoProvider>
  );
}

export default App;
```

## Consumir el contexto desde otro componente

Una vez ya tenemos nuestro proveedor envolviendo toda nuestra aplicación, ya podemos acceder a los datos desde cualquier componente hijo y olvidarnos de pasar props componente por componente.

### AppUI.js

```jsx
import React from 'react';
// Importamos nuestro contexto
import { TodoContext } from '../TodoContext';
import { TodoCounter } from '../TodoCounter';
import { TodoSearch } from '../TodoSearch';
import { TodoList } from '../TodoList';
import { TodoItem } from '../TodoItem';
import { CreateTodoButton } from '../CreateTodoButton';

function AppUI() {
  return (
    <React.Fragment>
      <TodoCounter />
      <TodoSearch />

      {/* Podemos acceder a nuestro contexto con el consumer */}
      <TodoContext.Consumer>
        {({
          error,
          loading,
          searchedTodos,
          completeTodo,
          deleteTodo,
        }) => (
          <TodoList>
            {error && <p>Desespérate, hubo un error...</p>}
            {loading && <p>Estamos cargando, no desesperes...</p>}
            {(!loading && !searchedTodos.length) && <p>¡Crea tu primer TODO!</p>}
            
            {searchedTodos.map(todo => (
              <TodoItem
                key={todo.text}
                text={todo.text}
                completed={todo.completed}
                onComplete={() => completeTodo(todo.text)}
                onDelete={() => deleteTodo(todo.text)}
              />
            ))}
          </TodoList>
        )}
      </TodoContext.Consumer>

      <CreateTodoButton />
    </React.Fragment>
  );
}

export { AppUI };
```

Con esto evitas pasar props a todos los componentes. Puedes tener muchos componentes que consuman un solo contexto y también varios contextos.

Si el valor del contexto cambia, todos los componentes suscritos se re-renderizan y actualizarán su estado.

Todavía nos falta utilizar nuestro consumer en todos los demás componentes, pero la verdad es que esta no es la mejor forma de consumir nuestro contexto.

## Lecturas recomendadas

- [Render Props](https://reactjs.org/docs/render-props.html)
- [Context](https://reactjs.org/docs/context.html)