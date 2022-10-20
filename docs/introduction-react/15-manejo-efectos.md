# Manejo de efectos

El **hook de efecto** en react nos permite ejecutar un pedazo de código cada vez que necesitemos, a lo largo de la vida de nuestro componente, también cuando se cumplan ciertas condiciones.

Algo curioso e importante de saber es que el código dentro de nuestro **hook de efecto** no se ejecuta como el resto del código, se ejecutará inicialmente justo antes de hacer el renderizado del HTML que resulte de nuestro código de React.

## Condiciones para nuestro hook de efecto

El hook de React, *useEffect*, puede recibir dos argumentos:

1. Función que se ejecutará en cada fase del ciclo de vida de nuestro componente.
2. Las condiciones de cuándo debe ejecutarse esta función dentro de un arreglo, cada que se actualice cualquier dato que le pasemos a este arreglo, se volverá a ejecutar nuestra función.

```jsx
React.useEffect(funcion, [dato1, dato2, datoN])
```

## Diferentes maneras de actualizar nuestros componentes

Existen tres diferentes maneras para aplicar el hook de efecto, todas funcionan diferente a la hora de re-renderizar nuestros componentes.

1. **Sin pasar un arreglo como segundo argumento: useEffect(funcion)**

Cuando no le pasamos un segundo argumento con las condiciones de cuándo se debe re-ejecutar nuestra función, React tomará como condiciones que se debe ejecutar nuestra función todas las veces que ocurra un re-renderizado, y también cada vez que se actualice alguna **prop** (Si es que el componente recibe alguna).

2. **Pasando un arreglo vacío: useEffect(funcion, [])**

Cuando pasamos un arreglo vacío, le estás diciendo a React que no hay ninguna condición para volver a ejecutar el código de nuestra función, entonces solamente se ejecutará en el renderizado inicial.

3. **Pasando un arreglo con datos: useEffect(funcion, [val1, val2, valN])**

Cuando especificas las condiciones dentro del arreglo del segundo parámetro, le estás diciendo a React que ejecute nuestra función en el renderizado inicial y también cuando algún dato del arreglo cambie.

## Simulando una petición a una API

Dentro de una aplicación web, al trabajar con APIs, existen muchos factores para determinar cuánto tardará en cargar nuestra aplicación, como la velocidad de nuestro internet, la distancia del servidor, etc.

Al trabajar con APIs también debemos tener en cuenta que puede tardar en cargar mucho nuestra aplicación, o incluso puede ocurrir algún error, todo esto lo debemos de manejar para mantener a nuestro usuario informado.

El hook de efecto nos permite saber cuando ya renderizó nuestra aplicación, así podemos mostrar un mensaje de cargando o alguna animación en lo que se completa la petición, también con JavaScript podemos manejar los errores con *try* y *catch*, y haciendo uso del hook de estado podemos guardar si está cargando o hubo algún error.

### App/index.js

```jsx
import React from 'react';
import { AppUI } from './AppUI';

function useLocalStorage(itemName, initialValue) {
  // Creamos el estado inicial para nuestros errores y carga
  const [error, setError] = React.useState(false);
  const [loading, setLoading] = React.useState(true);
  const [item, setItem] = React.useState(initialValue);
  
  React.useEffect(() => {
  // Simulamos un segundo de delay de carga 
    setTimeout(() => {
      // Manejamos la tarea dentro de un try/catch por si ocurre algún error
      try {
        const localStorageItem = localStorage.getItem(itemName);
        let parsedItem;
        
        if (!localStorageItem) {
          localStorage.setItem(itemName, JSON.stringify(initialValue));
          parsedItem = initialValue;
        } else {
          parsedItem = JSON.parse(localStorageItem);
        }

        setItem(parsedItem);
      } catch(error) {
        // En caso de un error lo guardamos en el estado
        setError(error);
      } finally {
        // También podemos utilizar la última parte del try/cath (finally) para terminar la carga
        setLoading(false);
      }
    }, 1000);
  });
  
  const saveItem = (newItem) => {
    // Manejamos la tarea dentro de un try/catch por si ocurre algún error
    try {
      const stringifiedItem = JSON.stringify(newItem);
      localStorage.setItem(itemName, stringifiedItem);
      setItem(newItem);
    } catch(error) {
      // En caso de algún error lo guardamos en el estado
      setError(error);
    }
  };

  // Para tener un mejor control de los datos retornados, podemos regresarlos dentro de un objeto
  return {
    item,
    saveItem,
    loading,
    error,
  };
}

function App() {
  // Desestructuramos los nuevos datos de nustro custom hook
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

  return (
    {/* Pasamos los valores de loading y error */}
    <AppUI
      loading={loading}
      error={error}
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

Una vez sabemos exactamente cuándo una aplicación está cargando y cuándo ha ocurrido algún error, podemos usar esta información para mostrar algo al usuario.

### App/AppUI.js

```jsx
import React from 'react';
import { TodoCounter } from '../TodoCounter';
import { TodoSearch } from '../TodoSearch';
import { TodoList } from '../TodoList';
import { TodoItem } from '../TodoItem';
import { CreateTodoButton } from '../CreateTodoButton';

// Desescructuramos las nuesvas props
function AppUI({
  loading,
  error,
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
        // Mostramos un mensaje en caso de que ocurra algún error
        {error && <p>Desespérate, hubo un error...</p>}
        // Mostramos un mensaje de cargando, cuando la aplicación está cargando lo sdatos
        {loading && <p>Estamos cargando, no desesperes...</p>}
        // Si terminó de cargar y no existen TODOs, se muestra un mensaje para crear el primer TODO
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

## NOTAS PROFESOR

💡 Como aprendimos en el minuto 04:57, podemos enviarle un segundo argumento a la función useEffect para determinar cuándo ejecutamos o no el código de nuestro efecto.

🔂 Podemos enviar un array vacío para decirle a nuestro efecto solo se ejecute una vez, cuando recién hacemos el primer render de nuestro componente.

👂 O también podemos enviar un array con distintos elementos para decirle a nuestro efecto que no solo ejecute el efecto en el primer render, sino también cuando haya cambios en esos elementos del array.

🔁 Si no enviamos ningún array como segundo argumento de nuestro efecto, esta función se ejecutará cada vez que nuestro componente haga render (es decir, cada vez que haya cambios en cualquiera de nuestros estados).

❓ ¿Cuál de estas opciones crees que debimos usar en nuestro efecto dentro de useLocalStorage?

Al menos por ahora, lo mejor habría sido enviar un array vacío para que nuestro efecto solo se ejecute una vez, en el primer amado a nuestro custom hook / render de nuestro componente. 😌

Lastimosamente, olvidé escribir ese segundo parámetro durante la clase. Esto hace que el código de mi efecto se ejecute cada vez que hay un cambio en el estado. Y como hacemos cambios a estado dentro del efecto, entonces el efecto se ejecutará sin parar todo el tiempo que usemos la aplicación. 😱

Afortunadamente, como todo el código del useEffect está envuelto en un setTimeout, cada ejecución del código de efecto tarda 1 segundo en volver a ejecutarse, por lo que la app no va a crashear. 😓

¡Este error podemos resolverlo en el siguiente curso de la saga! 🙏
Incluso podemos profundizar muchísimo más en este tipo de errores en un curso de optimización, rendimiento y debugging con React.js. 💚

💪 Mientras tanto, sé mejor que yo. No olvides escribir el segundo parámetro de tu efecto en useLocalStorage para que el código de tu efecto solo se ejecute una vez y no tengas problemas de rendimiento en tu versión de TODO Machine.

Eso puede ser un error o no dependiendo de lo que quieras lograr.

En nuestro caso queremos que ese llamado a la API ocurra solo una vez, cuando recién carga la página. Por eso usamos el array vacío.

Te adelanto que profundizaremos muchísimo más en cómo funcionan useEffect y useCallback con un **Curso de Optimización, Rendimiento y Debugging en React.js**.

La consola muestra un warning porque el efecto no volverá a correr aunque cambien esos estados y funciones que usa el mismo estado por dentro.

Te super invito a probar qué pasa en tu efecto cuando envías estados o actualizadores de estados en el array del useEffect. Y cómo useCallback afecta ese comportamiento. 😉

Aprovecho para aclarárselos:

- Una cosa es el render de React. Y otra cosa es el render en el navegador.

- React ejecuta el *useEffect* luego del render de React, pero antes del render en el navegador.

- En cambio, React ejecuta el *useLayoutEffect* luego del render de React y del render en el navegador.

## Lecturas recomendadas

- [Using the Effect Hook](https://reactjs.org/docs/hooks-effect.html)
- [5 estados clave para crear interfaces coherentes](https://platzi.com/blog/ui-stack/)
- [Casos Prácticos de useEffect y useLayoutEffect en React](https://platzi.com/blog/useeffect-uselayouteffect/)