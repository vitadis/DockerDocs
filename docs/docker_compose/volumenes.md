# Volúmenes en Docker

## 1. ¿Qué son los volúmenes?

Los volúmenes permiten almacenar y persistir datos generados o utilizados por los contenedores.

Su principal ventaja es que los datos se mantienen aunque el contenedor se elimine o se vuelva a crear.

Por ejemplo, una base de datos puede guardar su información en un volumen para evitar perderla al eliminar su contenedor.

## 2. Tipos de almacenamiento

Docker dispone de diferentes mecanismos para almacenar datos:

| Tipo | Descripción |
|---|---|
| `volume` | Almacena datos gestionados por Docker. Es la opción recomendada para persistir datos. |
| `bind mount` | Vincula una ruta concreta del equipo anfitrión con una ruta del contenedor. |
| `tmpfs` | Almacena datos temporalmente en memoria. Los datos desaparecen al detener o eliminar el contenedor. |

## 3. Volúmenes (Volumes)

Son espacios de almacenamiento gestionados por Docker, independientes del ciclo de vida de los contenedores.

Se utilizan habitualmente para bases de datos y aplicaciones que necesitan conservar información.

Ejemplo:

```bash
docker volume create datos_mysql
```

Este comando crea un volumen llamado `datos_mysql`.

Para utilizarlo en un contenedor:

```bash
docker run -d \
  --name mysql \
  -v datos_mysql:/var/lib/mysql \
  mysql:8.0
```

En este ejemplo, los datos de MySQL se almacenan en el volumen `datos_mysql`.

## 4. Bind mounts

Permiten compartir una carpeta o archivo del equipo anfitrión con un contenedor.

Son especialmente útiles durante el desarrollo, porque los cambios realizados en los archivos del equipo pueden reflejarse dentro del contenedor.

Ejemplo:

```bash
docker run -d \
  --name web \
  -v ./html:/usr/share/nginx/html \
  nginx:latest
```

En este caso:

- `./html`: carpeta del equipo anfitrión.
- `/usr/share/nginx/html`: carpeta dentro del contenedor.

## 5. Configuración de volúmenes en Docker Compose

Los volúmenes se pueden declarar en el apartado `volumes` del archivo `compose.yaml`.

Ejemplo:

```yaml
services:
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: ejemplo
    volumes:
      - datos_mysql:/var/lib/mysql

volumes:
  datos_mysql:
```

En este ejemplo:

- Se declara un volumen llamado `datos_mysql`.
- Se monta en `/var/lib/mysql`, donde MySQL almacena sus datos.
- Docker gestiona el almacenamiento del volumen.

## 6. Comandos principales

| Comando | Función |
|---|---|
| `docker volume ls` | Lista los volúmenes existentes. |
| `docker volume create nombre` | Crea un volumen. |
| `docker volume inspect nombre` | Muestra información del volumen. |
| `docker volume rm nombre` | Elimina un volumen. |
| `docker volume prune` | Elimina los volúmenes no utilizados. |

## 7. Consideraciones importantes

- Los volúmenes permiten conservar datos aunque se eliminen los contenedores.
- Eliminar un contenedor no elimina automáticamente los volúmenes con nombre.
- `docker compose down` no elimina normalmente los volúmenes con nombre.
- `docker compose down -v` elimina también los volúmenes declarados en el proyecto. **Puede provocar pérdida de datos.**
- Los volúmenes no sustituyen a las copias de seguridad.

## 8. Documentación oficial

- [Docker Volumes](https://docs.docker.com/engine/storage/volumes/)
- [Docker Bind Mounts](https://docs.docker.com/engine/storage/bind-mounts/)
- [Docker Compose: Volumes](https://docs.docker.com/reference/compose-file/volumes/)