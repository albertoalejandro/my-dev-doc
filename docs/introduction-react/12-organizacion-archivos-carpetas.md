# Organización de archivos y carpetas

La organización de un proyecto es algo muy importante, nos ayuda a tener un mejor control y orden sobre nuestra aplicación.

## ¿Cuál es la mejor estructura?

**No existe una mejor estructura** de carpetas, existen varias estructuras, y la más utilizada es la **agrupación por tipo de archivo**, puedes usar la que más te guste, la que mejor se adapte a tu proyecto, o ¡incluso crear una propia!

## Agrupación por tipo de archivo

En esta estructura solo agrupamos los **archivos similares**, es la más recomendada para proyectos grandes, también sirve para tener una excelente organización en proyectos pequeños, por ejemplo:

```
└── src/
    ├── assets/
    │   ├── img/
    │       └── foto.jpg
    │   ├── fonts/
    │       └──ubuntu.woff2
    ├── components/
    │   ├── CreateTodoButton/
    │       ├── index.js
    │       └── CreateTodoButton.css
    │   ├── TodoCounter/
    │   ├── TodoItem/
    │   ├── TodoList/
    │   ├── TodoSearch/
    ├── context/
    │   ├── TodoContext.js
    ├── hooks/
    │   ├── useLocalStorage.js
    ├── utils/
    │   ├── fetch.js
```
## Creando la estructura de nuestro proyecto

Puedes usar la estructura que más te guste, en nuestra aplicación, ya que son muy pocos componentes, solamente crearemos una carpeta por cada componente.

Una vez tengamos esto listo, ahora podemos importarlo dentro de nuestro archivo *App.js*, pero si queremos seguir las reglas de stateful y stateless, no tiene mucho sentido, por eso vamos a abstraer la UI de nuestro archivo *App.js* en otro componente que llamaremos *AppUI.js*:

### App/index.js

```jsx
import React from 'react';
import { AppUI } from './AppUI';

const defaultTodos = [
  { text: 'Cortar cebolla', completed: true },
  { text: 'Tomar el cursso de intro a React', completed: false },
  { text: 'Llorar con la llorona', completed: true },
  { text: 'LALALALAA', completed: false },
];

function App() {
  const [todos, setTodos] = React.useState(defaultTodos);
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

### App/AppUI.js

```jsx
import React from 'react';
import { TodoCounter } from '../TodoCounter';
import { TodoSearch } from '../TodoSearch';
import { TodoList } from '../TodoList';
import { TodoItem } from '../TodoItem';
import { CreateTodoButton } from '../CreateTodoButton';

function AppUI({
  totalTodos,
  completedTodos,
  searchValue,
  setSearchValue,
  searchedTodos,
  completeTodo,
  deleteTodo,
}) {
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

## MIS NOTAS

Stateful y Statless components:

- Los componentes stateful son los componentes que guardan y manejan estados. Por lo que hemos aprendido hasta ahora sería los que usan alguna variable que usa React.useState
- Mientras los componentes stateless son los componentes que solo presentan información. Es decir son los componentes que reciben props o simplemente muestran algun contenido

[Fuente](https://programmingwithmosh.com/javascript/stateful-stateless-components-react/)