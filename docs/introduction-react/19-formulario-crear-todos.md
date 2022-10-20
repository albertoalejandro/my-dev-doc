# Formulario para crear TODOs

Algo muy importante al crear formularios es tener en cuenta que React funciona un poco diferente al HTML, ya que en HTML conservan naturalmente algún estado interno.

En React nosotros podemos mutar el estado de nuestros componentes con el hook de estado, un **componente controlado** es simplemente un componente en el que sus valores son controlados por React.

## Creando el formulario para crear un nuevo TODO

En nuestro archivo *AppUi.js* importaremos y añadiremos un componente *TodoForm*:

```jsx
import React from "react";
import { TodoContext } from "../TodoContext";
import { TodoCounter } from "../TodoCounter";
import { TodoSearch } from "../TodoSearch";
import { TodoList } from "../TodoList";
import { TodoItem } from "../TodoItem";
import { TodoForm } from "../TodoForm";
import { CreateTodoButton } from "../CreateTodoButton";
import { Modal } from "../Modal";

function AppUI() {
	const { error, loading, searchedTodos, completeTodo, deleteTodo, openModal, setOpenModal } =
		React.useContext(TodoContext);
        
	return (
		<React.Fragment>
			<TodoCounter />
			<TodoSearch />
			<TodoList>
				{error && <p>Desespérate, hubo un error...</p>}
				{loading && <p>Estamos cargando, no desesperes...</p>}
				{!loading && !searchedTodos.length && <p>¡Crea tu primer TODO!</p>}
				{searchedTodos.map((todo) => (
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
					<TodoForm />
				</Modal>
			)}
			<CreateTodoButton setOpenModal={setOpenModal} />
		</React.Fragment>
	);
}
export { AppUI };
```

En un momento crearemos este componente, primero necesitamos añadir una función para añadir nuestro nuevo TODO, dentro de nuestro contexto para utilizarla en nuestro formulario.

### TodoContext

```jsx
import React from 'react';
import { useLocalStorage } from './useLocalStorage';

const TodoContext = React.createContext();

function TodoProvider(props) {
  const {
    item: todos,
    saveItem: saveTodos,
    loading,
    error,
  } = useLocalStorage('TODOS_V1', []);
  const [searchValue, setSearchValue] = React.useState('');
  const [openModal, setOpenModal] = React.useState(false);

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
  // Función para añadir un nuevo TODO
  const addTodo = (text) => {
    const newTodos = [...todos];
    newTodos.push({
      completed: false,
      text,
    });
    saveTodos(newTodos);
  };

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
    <TodoContext.Provider value={{
      loading,
      error,
      totalTodos,
      completedTodos,
      searchValue,
      setSearchValue,
      searchedTodos,
      addTodo,
      completeTodo,
      deleteTodo,
      openModal,
      setOpenModal,
    }}>
      {props.children}
    </TodoContext.Provider>
  );
}

export { TodoContext, TodoProvider };
```

### TodoForm.js

Ahora que ya tenemos prácticamente todo, solo queda utilizar la función *addTodo* para añadir nuestro TODO desde nuestro modal.

```jsx
import React from 'react';
import { TodoContext } from '../TodoContext';
import './TodoForm.css';

function TodoForm() {
  // Creamos un estado para nuestro nuevo TODO
  const [newTodoValue, setNewTodoValue] = React.useState('');
  // Desestructuramos las funciones que necesitamos para añadir un TODO y cerrar nuestro modal
  const {
    addTodo,
    setOpenModal,
  } = React.useContext(TodoContext);
  
  // Creamos una función para actualizar el estado de nuestro nuevo TODO
  const onChange = (event) => {
    setNewTodoValue(event.target.value);
  };
  
  // Función para cerrar el modal
  const onCancel = () => {
    setOpenModal(false);
  };
  
  // Función para agregar nuestro nuevo TODO
  const onSubmit = (event) => {
    // prevent default para evitar recargar la página
    event.preventDefault();
    // Utilizamos nuestra función para añadir nuestro TODO
    addTodo(newTodoValue);
    // Cerramos nustro modal
    setOpenModal(false);
    // También estaría bien resetear nuestro formulario
    setNewTodoValue('')
  };

  return (
    <form onSubmit={onSubmit}>
      <label>Escribe tu nuevo TODO</label>
      <textarea
        value={newTodoValue}
        onChange={onChange}
        placeholder="Cortar la cebolla para el almuerzo"
      />
      <div className="TodoForm-buttonContainer">
        <button
          type="button"
          className="TodoForm-button TodoForm-button--cancel"
          onClick={onCancel}
          >
          Cancelar
        </button>
        <button
          type="submit"
          className="TodoForm-button TodoForm-button--add"
        >
          Añadir
        </button>
      </div>
    </form>
  );
}

export { TodoForm };
```

También le podemos añadir unos estilos a nuestro formulario:

### TodoForm.css

```css
form {
  width: 90%;
  max-width: 300px;
  background-color: #fff;
  padding: 33px 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

label {
  text-align: center;
  font-weight: bold;
  font-size: 20px;
  color: #1E1E1F;
  margin-bottom: 26px;
}

textarea {
  background-color: #F9FBFC;
  border: 2px solid #202329;
  border-radius: 2px;
  box-shadow: 0px 5px 50px rgba(32, 35, 41, 0.25);
  color: #1E1E1F;
  font-size: 20px;
  text-align: center;
  padding: 12px;
  height: 96px;
  width: calc(100% - 25px);
}

textarea::placeholder {
  color: #A5A5A5;
  font-family: 'Montserrat';
  font-weight: 400;
}

textarea:focus {
  outline-color: #61DAFA;
}

.TodoForm-buttonContainer {
  margin-top: 14px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.TodoForm-button {
  cursor: pointer;
  display: inline-block;
  font-size: 20px;
  color: #202329;
  font-weight: 400;
  width: 120px;
  height: 48px;
  border-radius: 2px;
  border: none;
  font-family: 'Montserrat';
}

.TodoForm-button--add {
  background: #61DAFA;
  box-shadow: 0px 5px 25px rgba(97, 218, 250, 0.5);
}

.TodoForm-button--cancel {
  background: transparent;
}
```

Si tienes un estilo parecido al resultado final, te animamos a que le des tu personalidad a tu aplicación, no solamente de estilos, también agrega nuevas funcionalidades, rompe el código, mejóralo, la práctica es algo de lo más importante para aprender.

¡Esperamos ver tus resultados!