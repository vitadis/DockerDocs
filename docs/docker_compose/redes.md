# Redes en Docker

## 1. ¿Qué son las redes en Docker?

Las redes en Docker permiten la comunicación entre contenedores y, cuando es necesario, entre los contenedores y el equipo anfitrión o redes externas.

Gracias a ellas, diferentes servicios pueden comunicarse sin necesidad de publicar todos sus puertos en el equipo anfitrión.

## 2. Tipos principales de redes

Docker dispone de varios controladores de red (*drivers*):

| Tipo | Descripción |
|---|---|
| `bridge` | Permite la comunicación entre contenedores de una misma red. Es el tipo habitual en proyectos locales. |
| `host` | El contenedor comparte la red del equipo anfitrión. |
| `none` | Desactiva la conectividad de red del contenedor. |
| `overlay` | Permite conectar contenedores distribuidos entre diferentes hosts Docker. |
| `macvlan` | Asigna una dirección MAC al contenedor para que aparezca como un dispositivo de la red física. |

## 3. Red bridge

Es uno de los tipos de red más utilizados en Docker.

Permite que los contenedores conectados a una misma red se comuniquen entre sí.

Existen dos situaciones habituales:

- **Bridge por defecto:** Docker conecta automáticamente los contenedores que no tienen otra red configurada.
- **Bridge personalizada:** permite una comunicación más sencilla mediante nombres de contenedor y proporciona un mayor control sobre la red.

En Docker Compose, los servicios se conectan automáticamente a una red predeterminada del proyecto.

## 4. Configuración de redes en Docker Compose

Las redes se declaran en el apartado `networks` del archivo `compose.yaml`.

Ejemplo:

```yaml
services:
  web:
    image: nginx:latest
    networks:
      - red_app

  db:
    image: mysql:8.0
    networks:
      - red_app

networks:
  red_app:
    driver: bridge
```

En este ejemplo:

- Se crea una red llamada `red_app`.
- Los servicios `web` y `db` se conectan a ella.
- Ambos servicios pueden comunicarse utilizando sus nombres como nombres de host.

## 5. Comunicación entre contenedores

Los contenedores conectados a una misma red pueden comunicarse utilizando el nombre del servicio y el puerto interno de destino.

Por ejemplo, si el servicio `db` utiliza MySQL en el puerto `3306`, otro servicio puede conectarse a:

```text
db:3306
```

**Importante:** no es necesario publicar el puerto `3306` en el equipo anfitrión para que otros servicios de la misma red puedan acceder a él.

## 6. Publicación de puertos

La propiedad `ports` permite conectar un puerto del equipo anfitrión con uno del contenedor.

```yaml
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
```

La sintaxis es:

```text
PUERTO_HOST:PUERTO_CONTENEDOR
```

En este caso:

- `8080`: puerto del equipo anfitrión.
- `80`: puerto interno del contenedor.

Podemos acceder al servidor desde el navegador mediante:

```text
http://localhost:8080
```

## 7. Comandos principales

| Comando | Función |
|---|---|
| `docker network ls` | Lista las redes existentes. |
| `docker network create mi_red` | Crea una red. |
| `docker network inspect mi_red` | Muestra información detallada de una red. |
| `docker network connect mi_red contenedor` | Conecta un contenedor a una red. |
| `docker network disconnect mi_red contenedor` | Desconecta un contenedor de una red. |
| `docker network rm mi_red` | Elimina una red. |
| `docker network prune` | Elimina las redes no utilizadas. |

## 8. Documentación oficial

- [Docker Networking](https://docs.docker.com/engine/network/)
- [Docker Compose: Networks](https://docs.docker.com/reference/compose-file/networks/)
- [Docker Network CLI](https://docs.docker.com/reference/cli/docker/network/)