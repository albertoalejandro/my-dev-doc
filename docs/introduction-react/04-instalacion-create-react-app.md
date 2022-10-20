# Instalación con Create React App

Una manera muy sencilla de crear un proyecto con React es utilizando **Create React App**, así puedes **iniciar un proyecto** sin preocuparte por la configuración de herramientas como webpack o babel.

💡 Aunque siempre será mejor si nosotros hacemos esta configuración desde cero, ya que tendremos mayor control de todo e incluso nuestra aplicación tendría un mejor rendimiento.

## Maneras de instalar React

Existen varias formas de trabajar con React, cada una tiene sus ventajas y desventajas, siempre que trabajemos con React necesitaremos las dependencias react y react-dom.

### React en JavaScript vanilla

Podemos importar los scripts del código fuente de React, existen las versiones para **desarrollo** que nos facilita debuggear y para **producción** que está optimizada para el producto final.

React con JavaScript vanilla casi no se usa, lo ideal es crear un entorno de desarrollo que facilite nuestro trabajo.

### Configuración manual desde cero

Es la mejor manera si queremos tener control absoluto de nuestro entorno de desarrollo, necesitamos emplear y configurar varias herramientas.

#### Create React App

Esta es la manera más simple y rápida para trabajar con React, solo necesitamos ejecutar el comando: 
```
npx create-react-app nombre-del-proyecto 
```
o 
```
npx create-react-app nombre-del-proyecto --template typescript
``` 
para typescript y en unos instantes tendremos un entorno de desarrollo totalmente configurado para comenzar a trabajar.

## Entorno de Create React App

Dentro de este entorno tenemos un archivo *package.json* en el que se encuentran nuestros scripts, dependencias y meta datos de nuestro proyecto, también tendremos dos carpetas principales:

1. **public/:** Es la carpeta pública en donde tendremos nuestro archivo HTML y algunos assets
2. **src/:** Es la carpeta fuente, en donde tendremos todos nuestros archivos de trabajo

Dentro del *index.html* siempre tendremos un div con un id, como root que será la raíz de nuestro proyecto, y la usaremos para empezar a construir con JavaScript:

```js
 <!-- Aquí es en donde todo nuestro código será renderizado. -->
 <div id="root"></div>
```

## ¿Cómo inicializar nuestro servidor?

Para iniciar el entorno de desarrollo podemos ejecutar el comando *npm start*, con esto tendremos nuestro servidor corriendo en el puerto 3000 y también se refrescará automáticamente con cualquier cambio hecho en el proyecto. (A excepción de los cambios hechos en el archivo *index.js*).

## MIS NOTAS

Para instalar React:
https://github.com/facebook/react

npx: para instalar nuestras herramientas

```
npx create-react-app ./  
```
con npx nos aseguramos que coja la última versión de react
al final pones el nombre del proyecto pero si ya estamos dentro de la carpeta ponemos ./

Nota: no poner en mayúscula el nombre del directorio.

para iniciar la aplicación
npm start

Otra nota:

ReactDOM.render(QUE, DONDE)

Quiere decir que como primer parámetro el render recibe el componente que queremos renderizar y el segundo parámetro es donde lo vamos a mostrar