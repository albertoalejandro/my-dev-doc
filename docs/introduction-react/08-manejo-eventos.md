# Manejo de eventos

Manejar eventos en React es muy similar a manejar eventos en el DOM, solo necesitamos pasarle una propiedad **on + evento**, por ejemplo: *onClick, onChange, onMouseOve*r, que será igual a una función en la que estará el código que se ejecutará cuando ocurra dicho evento.

A diferencia de los eventos del DOM, para manejar eventos en React tenemos unas pequeñas diferencias en la sintaxis:

1. En React los eventos son nombrados usando ***camelCase***.
2. Tenemos que pasar una función, ya sea en línea o almacenada en una variable.
3. No puedes regresar *false* para prevenir el comportamiento por defecto, debes utilizar *preventDefault* explícitamente.

### HTML

```html
<button onclick="click()"></button>
```

### React
```jsx
<button onClick={click}></button>
```

## Pasando argumentos a escuchadores de eventos

En React no tenemos que ejecutar el código nosotros, React ya maneja esto por debajo, solo es necesario pasar una función, React solito la ejecutará cuando ocurra el evento que estemos escuchando.

Si necesitamos pasar argumentos a nuestras funciones, necesitamos encerrar nuestra función dentro de otra función, esto porque al pasarle argumentos a una función la estamos ejecutando, veamos un ejemplo:

```jsx
function CreateTodoButton(props) {
  const onClickButton = (msg) => {
    alert(msg);
  };
  
  return (
    <>
        {/* ✅ */}
        <button
          className="CreateTodoButton"
          onClick={() => onClickButton('Aquí se debería abrir el modal')}
        >
          +
        </button>
        {/* ❌ */}
        <button
          className="CreateTodoButton"
          onClick={onClickButton('Esta función se ejecuta al inicio, no al presionar el botón'}
        >
          +
        </button>
    </>
  );
}

```

✅ Es importante siempre pasar una función.

Dentro de estos eventos también puedes recibir como parámetro la información del evento, en donde puedes encontrar propiedades muy interesantes, como por ejemplo, el valor de algún *input*, con *event.target.value*.

```jsx
function TodoSearch() {
  const onSearchValueChange = (event) => {
    console.log(event.target.value);
  };
  
  return (
    <input
      className="TodoSearch"
      placeholder="Cebolla"
      onChange={onSearchValueChange}
    />
  );
}
```

## MIS NOTAS

```jsx
function CreateTodoButton() {
    return (
        <button 
            className="CreateTodoButton"
            onClick={() => console.log('click')}
        >+</button>
    );
}
```

si no ponemos la arrow function

```jsx
function CreateTodoButton() {
    return (
        <button 
            className="CreateTodoButton"
            onClick={console.log('click')}
        >+</button>
    );
}
```

el console.log se llamaría cada vez que se recargue la página

de otra manera:

```jsx
const onClickButton = () => {
    alert('Aquí se debería abrir el modal');
};

return (
    <button 
        className="CreateTodoButton"
        onClick={onClickButton}
    >+</button>
);
```
	
y si queremos pasar un mensaje dinámico:

```jsx
const onClickButton = (msg) => {
    alert(msg);
};

return (
    <button 
        className="CreateTodoButton"
        onClick={() => onClickButton('Aquí se debería abrir el modal')}
    >+</button>
);
```

## Lecturas recomendadas

- [Handling Events](https://reactjs.org/docs/handling-events.html)