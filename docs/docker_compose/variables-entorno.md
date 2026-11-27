# Variables de entorno en Docker

## 1. ¿Qué son las variables de entorno?

Son valores de configuración que se pueden proporcionar a los contenedores sin tener que modificar el código de la aplicación.

Se utilizan habitualmente para configurar:

- Credenciales de bases de datos.
- Puertos y direcciones.
- Modos de ejecución (desarrollo o producción).
- Rutas y parámetros de configuración.

## 2. Definir variables de entorno en Docker

Se utiliza la opción `-e` o `--env` al ejecutar un contenedor.

Ejemplo:

```bash
docker run -d \
  --name mysql \
  -e MYSQL_ROOT_PASSWORD=1234 \
  -e MYSQL_DATABASE=tienda \
  mysql:8.0
```

En este ejemplo se establecen dos variables de entorno para configurar MySQL.

## 3. Variables de entorno en Docker Compose

En Docker Compose se utiliza la propiedad `environment` dentro de cada servicio.

Ejemplo:

```yaml
services:
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: 1234
      MYSQL_DATABASE: tienda
```

También se pueden definir mediante una lista:

```yaml
environment:
  - MYSQL_ROOT_PASSWORD=1234
  - MYSQL_DATABASE=tienda
```

Ambas formas permiten establecer variables de entorno dentro del contenedor.

## 4. Archivo .env

Docker Compose permite utilizar un archivo `.env` para almacenar valores de configuración y reutilizarlos en el archivo `compose.yaml`.

Ejemplo de `.env`:

```env
DB_PASSWORD=1234
DB_NAME=tienda
```

Ejemplo de `compose.yaml`:

```yaml
services:
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: ${DB_PASSWORD}
      MYSQL_DATABASE: ${DB_NAME}
```

Compose sustituye las expresiones `${...}` por los valores definidos en el archivo `.env`.

Por defecto, Compose busca este archivo en el directorio de trabajo del proyecto.

## 5. Diferencia entre environment y env_file

Ambas propiedades permiten configurar variables de entorno, pero funcionan de forma diferente.

| Propiedad | Descripción |
|---|---|
| `environment` | Define directamente las variables dentro del servicio o recibe valores mediante interpolación. |
| `env_file` | Carga variables desde uno o varios archivos externos y las introduce en el entorno del contenedor. |

Ejemplo de `env_file`:

```yaml
services:
  db:
    image: mysql:8.0
    env_file:
      - .env
```

## 6. Consultar variables de entorno

Para consultar las variables configuradas dentro de un contenedor:

```bash
docker exec mysql env
```

Para consultar una variable concreta:

```bash
docker exec mysql printenv MYSQL_DATABASE
```

También puedes utilizar:

```bash
docker compose config
```

Este comando muestra la configuración de Compose una vez procesadas las variables e interpolaciones.

## 7. Consideraciones importantes

- El archivo `.env` facilita la gestión de configuraciones.
- Es recomendable incluir `.env` en `.gitignore` si contiene información privada.
- No debes subir contraseñas, tokens ni credenciales a repositorios públicos.
- El archivo `.env` utilizado para interpolación no se introduce automáticamente dentro del contenedor: debes utilizar `environment` o `env_file`.
- Las variables de entorno no son un sistema seguro para gestionar secretos sensibles en producción. Para ello, Docker ofrece mecanismos como Secrets.

## 8. Documentación oficial

- [Docker Compose: Environment Variables](https://docs.docker.com/compose/how-tos/environment-variables/)
- [Docker Compose: env_file](https://docs.docker.com/reference/compose-file/services/#env_file)
- [Docker: Environment Variables](https://docs.docker.com/reference/cli/docker/container/run/#env)