# useContext

El **hook de contexto** nos ayuda a acceder a datos globales de nuestro contexto, desde cualquier componente hijo, sin tener que pasar estos datos por props componente por componente.

Tiene la misma funcionalidad que el consumer de nuestro contexto, pero **useContext** también tiene una manera más sencilla de utilizar y una sintaxis mucho más clara.

## Context.Consumer a useContext

```jsx
import React from 'react';
// También es importante importar nuestro contexto
import { TodoContext } from '../TodoContext';
import { TodoCounter } from '../TodoCounter';
import { TodoSearch } from '../TodoSearch';
import { TodoList } from '../TodoList';
import { TodoItem } from '../TodoItem';
import { CreateTodoButton } from '../CreateTodoButton';

function AppUI() {
  // Desesctructuramos los valores de nuestro contexto
  const {
    error,
    loading,
    searchedTodos,
    completeTodo,
    deleteTodo,
  } = React.useContext(TodoContext);
  
  return (
    <React.Fragment>
      <TodoCounter />
      <TodoSearch />

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


      <CreateTodoButton />
    </React.Fragment>
  );
}

export { AppUI };
```

Ahora solo nos queda utilizar este hook para acceder a nuestro contexto desde los componentes faltantes.

### TodoCounter.js

```jsx
import React from 'react';
import { TodoContext } from '../TodoContext';
import './TodoCounter.css';

function TodoCounter() {
  const { totalTodos, completedTodos } = React.useContext(TodoContext);
  
  return (
    <h2 className="TodoCounter">Has completado {completedTodos} de {totalTodos} TODOs</h2>
  );
}

export { TodoCounter };
```

### TodoSearch.js

```jsx
import React from 'react';
import { TodoContext } from '../TodoContext';
import './TodoSearch.css';

function TodoSearch() {
  const { searchValue, setSearchValue } = React.useContext(TodoContext);
  
  const onSearchValueChange = (event) => {
    console.log(event.target.value);
    setSearchValue(event.target.value);
  };

  return (
    <input
      className="TodoSearch"
      placeholder="Cebolla"
      value={searchValue}
      onChange={onSearchValueChange}
    />
  );
}

export { TodoSearch };
```

## ¿Cuándo se recomienda emplear React Context?

- Estado global
- Tema
- Configuración de la app
- Autenticación de usuario
- Configuración de usuario
- Lenguaje preferido
- Colección de servicios

## Lecturas recomendadas

- [useContext](https://reactjs.org/docs/hooks-reference.html#usecontext)
