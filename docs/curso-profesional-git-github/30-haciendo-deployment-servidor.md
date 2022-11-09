# Haciendo deployment a un servidor

**Deploy** es el proceso que permite enviar al servidor uno o varios archivos. Este servidor puede ser de prueba, desarrollo o producción.

En el siguiente ejemplo veremos cómo se realiza el deployment de un documento en un servidor web básico.

## Pasos para hacer deployment en un servidor web:

- Entrar a la capeta de los archivos del servidor.

- Copiar link en clone, elegir entre HTTPS o SSH del repositorio a contribuir.

- En la carpeta deseada se clona el repositorio:

```
git clone url
Deploy:
```

- Realizar cambios y commit en GitHub.

- Traer al Repositorio local las actualizaciones para el servidor en la capeta de los archivos del servidor.

```
git pull ramaRemota main
```

Nota: Siempre se debe proteger el archivo .git. Dependiendo del software para el servidor web, existen diferentes maneras. La conexión entre GitHub y el servidor se puede realizar mediante: Travis (pago) o Jenkis (Open source).

