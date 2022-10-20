# Contando y buscando TODOs

El **levantamiento de estado** es una técnica de React que pone el estado en una localización donde se pueda pasar como props a los componentes.

Lo ideal es poner el estado en el lugar más cercano a todos los componentes que quieren compartir esa información, así todos nuestros componentes tendrán el mismo estado y cuando este cambie sólo re-renderizará lo necesario.

Esto es justamente lo que haremos ahora para hacer funcionar nuestro contador y nuestro buscador, pero debemos tener mucho **cuidado al manejar re-renderizados**, porque estos pueden causar una mala experiencia de usuario o incluso romper nuestra aplicación.

## Contando TODOs

Dentro de nuestro componente *App.js* primero necesitamos crear el estado de nuestros TODOs, para apartir de ahí poder saber cuántos TODOs existen y cuántos están completados.

```jsx
import React from 'react';
import { TodoCounter } from './TodoCounter';
import { TodoSearch } from './TodoSearch';
import { TodoList } from './TodoList';
import { TodoItem } from './TodoItem';
import { CreateTodoButton } from './CreateTodoButton';
// import './App.css';

const defaultTodos = [
  { text: 'Cortar cebolla', completed: true },
  { text: 'Tomar el cursso de intro a React', completed: false },
  { text: 'Llorar con la llorona', completed: true },
  { text: 'LALALALAA', completed: false },
];

function App() {
  // Estado inicial de nuestros TODOs
  const [todos, setTodos] = React.useState(defaultTodos);
  // Cantidad de TODOs completados
  const completedTodos = todos.filter(todo => !!todo.completed).length;
  // Cantidad total de TODOs
  const totalTodos = todos.length;
  
  return (
    <React.Fragment>
      {/* Pasamos el estado a nuestro componente */}
      <TodoCounter
        total={totalTodos}
        completed={completedTodos}
      />
      <TodoSearch />
      <TodoList>
        {searchedTodos.map(todo => (
          <TodoItem
            key={todo.text}
            text={todo.text}
            completed={todo.completed}
          />
        ))}
      </TodoList>

      <CreateTodoButton />
    </React.Fragment>
  );
}

export default App;
```

Una vez teniendo estos datos, ya podemos recibir las props en nuestro contador.

```jsx
import React from 'react';
import './TodoCounter.css';

// Desestructuramos los props que pasamos al componente
function TodoCounter({ total, completed }) {
  return (
    <h2 className="TodoCounter">Has completado {completed} de {total} TODOs</h2>
  );
}

export { TodoCounter };
```

## Buscando TODOs

Para esto haremos algo parecido a lo que hicimos para contar nuestros TODOs, para tener acceso al valor de la búsqueda desde nuestro componente *App.js* y ahí filtrar nuestros TODOs.

Primero crearemos nuestro estado de búsqueda en *App.js*, y utilizaremos el método *filter* de JavaScript para filtrar los TODOs que coincidan con nuestra búsqueda, y también haremos uso de *toLowerCase()*, para poder filtrar sin importar si las letras son mayúsculas o minúsculas.

```jsx
import React from 'react';
import { TodoCounter } from './TodoCounter';
import { TodoSearch } from './TodoSearch';
import { TodoList } from './TodoList';
import { TodoItem } from './TodoItem';
import { CreateTodoButton } from './CreateTodoButton';
// import './App.css';

const defaultTodos = [
  { text: 'Cortar cebolla', completed: true },
  { text: 'Tomar el cursso de intro a React', completed: false },
  { text: 'Llorar con la llorona', completed: true },
  { text: 'LALALALAA', completed: false },
];

function App() {
  const [todos, setTodos] = React.useState(defaultTodos);
  // El estado de nuestra búsqueda
  const [searchValue, setSearchValue] = React.useState('');

  const completedTodos = todos.filter(todo => !!todo.completed).length;
  const totalTodos = todos.length;
  // Creamos una nueva variable en donde guardaremos las coincidencias con la búsqueda
  let searchedTodos = [];

  // Lógica para filtrar
  if (!searchValue.length >= 1) {
    searchedTodos = todos;
  } else {
    searchedTodos = todos.filter(todo => {
      const todoText = todo.text.toLowerCase();
      const searchText = searchValue.toLowerCase();
      return todoText.includes(searchText);
    });
  }
  
  return (
    <React.Fragment>
      <TodoCounter
        total={totalTodos}
        completed={completedTodos}
      />
      <TodoSearch
        searchValue={searchValue}
        setSearchValue={setSearchValue}
      />

      <TodoList>
        {/* Regresamos solamente los TODOs buscados */}
        {searchedTodos.map(todo => (
          <TodoItem
            key={todo.text}
            text={todo.text}
            completed={todo.completed}
          />
        ))}
      </TodoList>

      <CreateTodoButton />
    </React.Fragment>
  );
}

export default App;
```