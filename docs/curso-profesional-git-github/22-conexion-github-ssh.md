# Conexión a GitHub con SSH

La creación de las SSH es necesario solo una vez por cada computadora. Aquí conocerás **cómo conectar a GitHub usando SSH**.

Luego de crear nuestras llaves SSH podemos entregarle la llave pública a GitHub para comunicarnos de forma segura y sin necesidad de escribir nuestro usuario y contraseña todo el tiempo.

Para esto debes entrar a la [Configuración de Llaves SSH en GitHub](https://github.com/settings/keys), crear una nueva llave con el nombre que le quieras dar y el contenido de la llave pública de tu computadora.

Ahora podemos actualizar la URL que guardamos en nuestro repositorio remoto, solo que, en vez de guardar la URL con HTTPS, vamos a usar la URL con SSH:

```
ssh
git remote set-url origin url-ssh-del-repositorio-en-github
```

## Comandos para copiar la llave SSH:

- Mac:

```
pbcopy < ~/.ssh/id_rsa.pub
```

- Windows (Git Bash):

```
clip < ~/.ssh/id_rsa.pub
```

- Linux (Ubuntu):

```
cat ~/.ssh/id_rsa.pub
```

### Notas

![Notas de Clase](./img/clase22-notas.png)