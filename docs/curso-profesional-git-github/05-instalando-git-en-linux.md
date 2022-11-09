# Instalando Git en Linux

Cada distribución de Linux tiene un comando especial para instalar herramientas y actualizar el sistema. Aquí veremos un ejemplo de los comandos para instalar Git en Linux

```
sudo apt-get update
sudo apt install git
git --version
```

**Sudo** significa Super User DO. Se utiliza para correr comandos con credenciales de super usuario (sin restricciones).

En las distribuciones derivadas de Debian (como Ubuntu) el comando especial es ```apt-get```, en Red Hat es ```yum``` y en ArchLinux es ```pacman```. Cada distribución tiene su comando especial y debes averiguar cómo funciona para poder instalar Git.

Antes de hacer la instalación, debemos hacer una actualización del sistema. En nuestro caso, los comandos para hacerlo son ```sudo apt-get update``` y ```sudo apt-get upgrade```.

Con el sistema actualizado, ahora sí podemos instalar Git y, en este caso, el comando para hacerlo es ```sudo apt-get install git```. También puedes verificar que Git fue instalado correctamente con el comando ```git --version```.

### Notas

![Notas de Clase](./img/clase05-notas.png)

