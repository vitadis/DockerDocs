# Comandos Docker

## 1. Información del sistema

| Comando | Función |
|---|---|
| `docker --version` | Muestra la versión de Docker. |
| `docker info` | Muestra información del entorno Docker. |
| `docker help` | Muestra la ayuda general. |
| `docker system df` | Muestra el espacio utilizado por Docker. |

## 2. Gestión de imágenes

| Comando | Función |
|---|---|
| `docker images` | Lista las imágenes locales. |
| `docker pull nginx` | Descarga una imagen. |
| `docker build -t mi_imagen .` | Construye una imagen desde un Dockerfile. |
| `docker rmi nginx` | Elimina una imagen. |
| `docker image inspect nginx` | Muestra información detallada de una imagen. |

## 3. Gestión de contenedores

| Comando | Función |
|---|---|
| `docker run nginx` | Crea y ejecuta un contenedor. |
| `docker run -d nginx` | Ejecuta un contenedor en segundo plano. |
| `docker ps` | Muestra los contenedores en ejecución. |
| `docker ps -a` | Muestra todos los contenedores. |
| `docker start nombre` | Inicia un contenedor detenido. |
| `docker stop nombre` | Detiene un contenedor. |
| `docker restart nombre` | Reinicia un contenedor. |
| `docker rm nombre` | Elimina un contenedor detenido. |
| `docker exec -it nombre bash` | Abre una terminal interactiva dentro del contenedor (si dispone de Bash). |
| `docker logs nombre` | Muestra los registros del contenedor. |
| `docker inspect nombre` | Muestra información detallada del contenedor. |

## 4. Puertos y ejecución

Al ejecutar un contenedor, se pueden utilizar diferentes opciones:

| Opción | Función |
|---|---|
| `-d` | Ejecuta el contenedor en segundo plano. |
| `-it` | Permite interactuar con el contenedor mediante una terminal. |
| `--name` | Asigna un nombre al contenedor. |
| `-p` | Publica un puerto del contenedor en el equipo anfitrión. |
| `-v` | Monta un volumen o bind mount. |
| `-e` | Define una variable de entorno. |
| `--rm` | Elimina automáticamente el contenedor al finalizar. |

Ejemplo:

```bash
docker run -d --name web -p 8080:80 nginx
```

## 5. Gestión de redes

| Comando | Función |
|---|---|
| `docker network ls` | Lista las redes. |
| `docker network create mi_red` | Crea una red. |
| `docker network inspect mi_red` | Muestra información de una red. |
| `docker network connect mi_red contenedor` | Conecta un contenedor a una red. |
| `docker network disconnect mi_red contenedor` | Desconecta un contenedor de una red. |
| `docker network rm mi_red` | Elimina una red. |

## 6. Gestión de volúmenes

| Comando | Función |
|---|---|
| `docker volume ls` | Lista los volúmenes. |
| `docker volume create datos` | Crea un volumen. |
| `docker volume inspect datos` | Muestra información de un volumen. |
| `docker volume rm datos` | Elimina un volumen. |
| `docker volume prune` | Elimina los volúmenes no utilizados. |

## 7. Gestión de Docker Compose

Ejecutar estos comandos desde el directorio del proyecto donde se encuentra `compose.yaml`.

| Comando | Función |
|---|---|
| `docker compose up` | Crea e inicia los servicios. |
| `docker compose up -d` | Inicia los servicios en segundo plano. |
| `docker compose down` | Detiene y elimina los contenedores y redes del proyecto. |
| `docker compose ps` | Muestra los contenedores del proyecto. |
| `docker compose logs` | Muestra los registros de los servicios. |
| `docker compose logs -f` | Sigue los registros en tiempo real. |
| `docker compose restart` | Reinicia los servicios. |
| `docker compose stop` | Detiene los servicios. |
| `docker compose build` | Construye o reconstruye las imágenes. |
| `docker compose exec servicio bash` | Abre una terminal dentro de un servicio (si dispone de Bash). |

## 8. Limpieza del sistema

| Comando | Función |
|---|---|
| `docker container prune` | Elimina los contenedores detenidos. |
| `docker image prune` | Elimina imágenes no utilizadas según los criterios de limpieza. |
| `docker network prune` | Elimina redes no utilizadas. |
| `docker volume prune` | Elimina volúmenes no utilizados. |
| `docker system prune` | Elimina recursos no utilizados, como contenedores detenidos, redes sin uso e imágenes colgantes. |
| `docker system prune -a` | Amplía la limpieza para incluir imágenes no utilizadas por contenedores existentes. |

**Precaución:** los comandos `prune` eliminan recursos. Revisa qué elementos se van a borrar antes de ejecutarlos, especialmente cuando contienen datos importantes.

## 9. Documentación oficial

- [Docker CLI](https://docs.docker.com/reference/cli/docker/)
- [Docker Compose CLI](https://docs.docker.com/reference/cli/docker/compose/)
- [Docker Commands](https://docs.docker.com/get-started/docker_cheatsheet.pdf)