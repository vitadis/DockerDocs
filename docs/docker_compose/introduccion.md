# Introducción a Docker Compose

## 1. ¿Qué es Docker Compose?

Docker Compose es una herramienta que permite definir y gestionar aplicaciones multicontenedor. Facilita la configuración y ejecución de diferentes servicios que funcionan mediante contenedores independientes y que pueden comunicarse entre sí.

En lugar de crear y configurar cada contenedor individualmente, podemos definir toda la infraestructura de nuestra aplicación mediante un único archivo de configuración.

## 2. Archivo de configuración

Docker Compose utiliza un archivo YAML, normalmente denominado `compose.yaml`, donde definimos los diferentes elementos que componen nuestra aplicación:

- **Services:** servicios que queremos ejecutar, como un servidor web o una base de datos.
- **Networks:** redes que permiten la comunicación entre los diferentes contenedores.
- **Volumes:** mecanismos para almacenar y persistir datos.
- **Environment:** variables de entorno utilizadas para configurar los servicios.

## 3. Arquitectura y funcionamiento

Docker Compose no crea máquinas virtuales, sino que gestiona contenedores independientes que comparten el kernel del sistema operativo anfitrión.

En sistemas Windows, Docker Desktop utiliza normalmente WSL 2 para proporcionar el entorno Linux necesario para ejecutar contenedores Linux.

La arquitectura simplificada sería:

1. **Sistema operativo:** Windows como sistema principal.
2. **WSL 2:** proporciona el kernel Linux necesario para ejecutar contenedores Linux.
3. **Docker Engine:** se encarga de crear y ejecutar los contenedores.
4. **Docker Compose:** define y gestiona los diferentes servicios que componen nuestra aplicación.

## 4. Docker Compose CLI

Docker Compose dispone de una interfaz de línea de comandos (CLI) que permite interactuar con los servicios definidos en el archivo `compose.yaml`.

Entre sus principales operaciones encontramos:

- Iniciar los servicios.
- Detener los servicios.
- Construir imágenes.
- Consultar los registros (logs).
- Acceder a los contenedores.
- Gestionar el ciclo de vida de la aplicación.

## 5. Ejemplo práctico

Imaginemos que queremos desplegar una aplicación web que necesita un servidor web y una base de datos.

Mediante Docker Compose podemos definir dos servicios:

- **web:** contenedor encargado de ejecutar el servidor web.
- **db:** contenedor encargado de ejecutar la base de datos MySQL.

Ambos servicios se definen en un mismo archivo `compose.yaml`, permitiendo gestionarlos conjuntamente y establecer la comunicación necesaria entre ellos.

## 6. Ventajas de Docker Compose

- **Centralización:** toda la configuración de los servicios se encuentra en un mismo archivo.
- **Facilidad de gestión:** permite iniciar y detener varios servicios conjuntamente.
- **Reproducibilidad:** facilita desplegar la misma configuración en diferentes entornos.
- **Comunicación:** permite establecer redes para conectar los diferentes contenedores.
- **Persistencia:** permite conservar datos mediante volúmenes.

## 7. Documentación oficial

- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Docker Compose CLI Reference](https://docs.docker.com/reference/cli/docker/compose/)