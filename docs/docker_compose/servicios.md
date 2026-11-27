# Servicios en Docker Compose

## 1. ¿Qué es un servicio?

Un servicio define cómo se debe crear y ejecutar un contenedor dentro de una aplicación gestionada con Docker Compose.

Cada servicio representa normalmente un componente de la aplicación, como un servidor web, una base de datos o una API.

Una aplicación puede tener varios servicios que trabajan conjuntamente.

## 2. Definición de servicios

Los servicios se declaran dentro del apartado `services` del archivo `compose.yaml`.

Ejemplo:

```yaml
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"

  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: ejemplo
```

En este ejemplo se definen dos servicios:

- `web`: ejecuta un servidor web Nginx.
- `db`: ejecuta una base de datos MySQL.

Docker Compose gestiona ambos servicios y sus contenedores.

## 3. Propiedades principales de un servicio

| Propiedad | Descripción |
|---|---|
| `image` | Imagen que se utilizará para crear el contenedor. |
| `build` | Indica dónde está el Dockerfile para construir una imagen propia. |
| `ports` | Publica puertos del contenedor en el equipo anfitrión. |
| `environment` | Define variables de entorno. |
| `volumes` | Permite persistir datos o compartir archivos. |
| `networks` | Conecta el servicio con una o varias redes. |
| `depends_on` | Define dependencias entre servicios. |
| `restart` | Establece cuándo debe reiniciarse el contenedor. |

## 4. Comunicación entre servicios

Los servicios de un mismo proyecto Compose pueden comunicarse entre sí mediante una red compartida.

Docker Compose crea una red por defecto para los servicios del proyecto.

Para comunicarse, pueden utilizar el nombre del servicio como nombre de host.

Por ejemplo, desde el servicio `web` se puede acceder a la base de datos mediante el nombre `db`, siempre que ambos estén conectados a la misma red.

```yaml
services:
  web:
    image: nginx:latest

  db:
    image: mysql:8.0
```

## 5. Dependencias entre servicios

La propiedad `depends_on` permite establecer el orden de inicio entre servicios.

```yaml
services:
  web:
    image: nginx:latest
    depends_on:
      - db

  db:
    image: mysql:8.0
```

En este caso, Compose inicia el servicio `db` antes que `web`.

**Importante:** `depends_on` controla el orden de inicio, pero no garantiza que la aplicación del servicio dependiente esté lista para recibir conexiones.

## 6. Escalado de servicios

Docker Compose permite ejecutar varias instancias de un mismo servicio.

Por ejemplo:

```bash
docker compose up -d --scale web=3
```

Este comando solicita tres instancias del servicio `web`.

## 7. Comandos principales

| Comando | Función |
|---|---|
| `docker compose up -d` | Inicia los servicios en segundo plano. |
| `docker compose down` | Detiene y elimina los contenedores y redes del proyecto. |
| `docker compose ps` | Muestra los contenedores del proyecto. |
| `docker compose logs` | Muestra los registros de los servicios. |
| `docker compose restart` | Reinicia los servicios. |
| `docker compose stop` | Detiene los servicios sin eliminarlos. |

> `NOTAS:`
> Todos estos comandos se ejecutan dentro del directorio donde se encuentra tu fichero de configuración.
## 8. Documentación oficial

- [Docker Compose: Services](https://docs.docker.com/reference/compose-file/services/)
- [Docker Compose: Networking](https://docs.docker.com/compose/how-tos/networking/)
- [Docker Compose: CLI](https://docs.docker.com/reference/cli/docker/compose/)