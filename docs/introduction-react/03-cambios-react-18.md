---
sidebar_position: 3
---

# Cambios en React 18: ReactDOM.createRoot

React 18 fue publicado el 29 de marzo de 2022. Sus cambios más importantes van a ayudar muchísimo para optimizar el render e hidratación de aplicaciones o componentes de React en el DOM. El más importante, crucial y significativo fue la migración de **ReactDOM.render** a **ReactDOM.createRoot**.

En la próxima clase vamos a usar **Create React App**, una de las herramientas más populares para instalar un entorno de desarrollo con React.js de forma muy rápida. **No hay absolutamente ningún problema si decides usar React 18**. Solo ten en consideración los cambios para hacer el render principal de tu aplicación.

## Migración de ReactDOM.render a ReactDOM.createRoot

Antes de React 18:

```js
const root = document.getElementById('root');
ReactDOM.render(e(LikeButton), root);
```

Desde React 18:

```js
const rootElement = document.getElementById('root');
const root = ReactDom.createRoot(rootElement);
root.render(e(LikeButton));
```

Antes de React 18:

```js
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

Desde React 18:

```js
const rootElement = document.getElementById('root');
const root = ReactDom.createRoot(rootElement);

root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

## Actualizaciones de React

En los siguientes recursos puedes estudiar más a detalle los cambios de React y ReactDOM en su versión 18:

- [React Conf 2021: anuncios, cambios y el futuro de React.js](https://platzi.com/blog/react-conf-2021/)
- [CHANGELOG de React](https://github.com/facebook/react/blob/main/CHANGELOG.md)
- [React 18 is now available on npm!](https://reactjs.org/blog/2022/03/29/react-v18.html)
- [How to Upgrade to React 18](https://reactjs.org/blog/2022/03/08/react-18-upgrade-guide.html)

Además, si quieres conocer un poco más a fondo la filosofía y principios de diseño de React para elegir cómo hacer sus actualizaciones, te recomiendo tomar la siguiente clase:

- [Filosofía y principios de diseño en React](https://platzi.com/clases/2457-react-patrones-render/40852-filosofia-y-principios-de-diseno-en-react/)

