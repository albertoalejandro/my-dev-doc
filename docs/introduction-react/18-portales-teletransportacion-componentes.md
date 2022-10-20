# Portales: teletransportación de componentes

Los portales nos permiten teletransportar componentes a otro nodo de HTML, y seguir comunicándose con otros componentes como si estuviera en el mismo nodo.

Se emplean en ocasiones donde los estilos CSS restringen los elementos. Por ejemplo, problemas de apilamiento *z-index* y desbordamiento *overflow*.

¿Para qué podemos usarlos?

- Modales
- Tooltips
- Menús flotantes
- Widgets

```jsx
// Es el mismo import para las versiones mayores o iguales a ReactV18
import ReactDOM from "react-dom";

ReactDOM.createPortal(componente, contenedor)
```

## Creando nuestro modal

Lo primero que necesitamos es crear otro *div* dentro del *body* en nuestro HTML.

```html
<div id="modal"></div>
```

Una vez tenemos nuestro ```div``` exclusivo para nuestro modal ya podemos trabajar con React:

### Modal/index.js

Crearemos un componente Modal:

```jsx
import React from 'react';
// Necesitamos ReactDOM para renderizar nuestro modal en el DOM
import ReactDOM from 'react-dom';
import './Modal.css';

function Modal({ children }) {
  // ReactDom tiene este método para crear portales
  return ReactDOM.createPortal(
    <div className="ModalBackground">
      {children}
    </div>,
    document.getElementById('modal')
  );
}

export { Modal };
```

### Modal.css

También agreguemos un poco de CSS para que se vea como un modal.

```css
.ModalBackground {
  background: rgba(32,35,41,.8);
  position: fixed;
  top: -10px;
  left: -10px;
  right: -10px;
  bottom: -10px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
}
```

### AppUI.js

Lo interesante es que podemos pasarle otros componentes y hasta tener acceso al contexto de nuestra aplicación al importar nuestro modal dentro de la aplicación.

```jsx
import React from 'react';
import { TodoContext } from '../TodoContext';
import { TodoCounter } from '../TodoCounter';
import { TodoSearch } from '../TodoSearch';
import { TodoList } from '../TodoList';
import { TodoItem } from '../TodoItem';
import { CreateTodoButton } from '../CreateTodoButton';
import { Modal } from '../Modal';

function AppUI() {
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

      <Modal>
        <p>{searchedTodos[0]?.text}</p>
      </Modal>

      <CreateTodoButton />
    </React.Fragment>
  );
}

export { AppUI };
```

Si hacemos esto, ya tendremos nuestro modal en nuestra aplicación, pero hay un pequeño detalle, el modal aparece sobre toda nuestra aplicación, necesitamos crear un estado para decirle si estará abierto o cerrado, y también para poder cerrarlo cuando sea necesario.

Dentro de nuestro contexto crearemos un estado extra que será para nuestro modal:

### TodoContext/index.js

```jsx
const [openModal, setOpenModal] = React.useState(false);
...
// Y lo exportamos
    return (
        <TodoContext.Provider value={{
          ....
          openModal
          setOpenModal,
        }}>
          {props.children}
        </TodoContext.Provider>
  );
}
```

### Cambios en AppUI.js

¡Ahora podemos abrir y cerrar nuestro modal desde cualquier parte de nuestra aplicación!
Por ejemplo, en nuestro componente *CreateTodoButton*, primero necesitamos crear la lógica para mostrar el Modal solo cuando *openModal*, sea *true* en nuestro componente.

```jsx
import React from 'react';
import { TodoContext } from '../TodoContext';
import { TodoCounter } from '../TodoCounter';
import { TodoSearch } from '../TodoSearch';
import { TodoList } from '../TodoList';
import { TodoItem } from '../TodoItem';
import { CreateTodoButton } from '../CreateTodoButton';
import { Modal } from '../Modal';

function AppUI() {
  const {
    error,
    loading,
    searchedTodos,
    completeTodo,
    deleteTodo,
    openModal,
    setOpenModal,
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

      {!!openModal && (
        <Modal>
          <p>{searchedTodos[0]?.text}</p>
        </Modal>
      )}

      <CreateTodoButton
        setOpenModal={setOpenModal}
      />
    </React.Fragment>
  );
}

export { AppUI };
```

Y ahora que pasamos nuestro contexto por props, ya podemos cambiar este estado para abrir nuestro modal.

```jsx
import React from 'react';
import './CreateTodoButton.css';

function CreateTodoButton(props) {
  const onClickButton = () => {
    props.setOpenModal(true);
  };
  
  return (
    <button
      className="CreateTodoButton"
      onClick={onClickButton}
    >
      +
    </button>
  );
}

export { CreateTodoButton };
```

Pero, antes de avanzar, todavía hay un pequeño problema, no podemos cerrar nuestro modal, esto queda como reto para ti, deja correr tu creatividad.

Puedes crear un botón de cerrar nuestro modal, o que al hacer clic en el background del modal se cierre, también puedes hacer un toggle para el botón de crear TODO, o hasta añadir un botón de cancelar en el modal para cerrarlo. ¡Esperamos ver tu resultado en los comentarios!

## Lecturas recomendadas

- [Portals](https://reactjs.org/docs/portals.html)

