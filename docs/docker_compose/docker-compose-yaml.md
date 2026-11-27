# Estructura del archivo YAML en Docker Compose

## 1. ¿Qué es el archivo compose.yaml?

`compose.yaml` es el archivo de configuración que utiliza Docker Compose para definir los diferentes servicios que componen una aplicación multicontenedor.

Mediante este archivo declaramos cómo deben configurarse y ejecutarse los contenedores, así como los recursos que necesitan para comunicarse y funcionar correctamente.

El formato utilizado es YAML, un lenguaje de serialización de datos que utiliza una estructura basada en indentación.

## 2. Estructura general

Un archivo `compose.yaml` utiliza diferentes propiedades para definir la infraestructura de nuestra aplicación.

Su estructura general es la siguiente:

```yaml
services:
  nombre_servicio:
    image: nombre_imagen
    ports:
      - "8080:80"
    environment:
      - VARIABLE=valor
    volumes:
      - datos:/ruta/contenedor
    networks:
      - red_aplicacion

volumes:
  datos:

networks:
  red_aplicacion:
```

Las principales secciones son:

- **services:** define los servicios que ejecutará nuestra aplicación.
- **volumes:** declara los volúmenes necesarios para almacenar y persistir datos.
- **networks:** declara las redes que permitirán la comunicación entre servicios.

## 3. Componentes principales

### 3.1. services

Es la sección principal del archivo. Aquí declaramos los diferentes servicios que forman nuestra aplicación.

Cada servicio representa una instancia de contenedor que se ejecutará utilizando una imagen determinada o una imagen construida mediante un Dockerfile.

### 3.2. image

Indica la imagen que utilizará el servicio para crear su contenedor.

```yaml
services:
  web:
    image: nginx:latest
```
> `NOTA:`
> Aquí puedes consultar las imágenes oficiales de Docker:
> https://hub.docker.com/search?badges=official
En este ejemplo utilizamos la imagen de Nginx para crear el contenedor del servicio `web`.

### 3.3. build

Permite indicar cómo construir una imagen utilizando un Dockerfile.

```yaml
services:
  web:
    build: .
```

El punto indica que Docker debe buscar el contexto de construcción en el directorio actual.

### 3.4. ports

Permite establecer una correspondencia entre los puertos del host y los del contenedor.

```yaml
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

En este ejemplo:

- `8080`: puerto del equipo anfitrión.
- `80`: puerto del contenedor.

Podremos acceder al servidor web mediante `http://localhost:8080`.

### 3.5. environment

Permite definir variables de entorno que estarán disponibles dentro del contenedor.

```yaml
services:
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: contraseña
      MYSQL_DATABASE: aplicacion
```

Estas variables permiten configurar el comportamiento de determinados servicios.

### 3.6. volumes

Permite asociar almacenamiento al contenedor para conservar datos o compartir archivos entre el host y el contenedor.

```yaml
services:
  db:
    image: mysql
    volumes:
      - datos:/var/lib/mysql
```

En este ejemplo asociamos el volumen `datos` al directorio donde MySQL almacena sus datos.

### 3.7. networks

Permite conectar diferentes servicios mediante redes virtuales.

```yaml
services:
  web:
    image: nginx
    networks:
      - red_aplicacion

  db:
    image: mysql
    networks:
      - red_aplicacion

networks:
  red_aplicacion:
```

Ambos servicios estarán conectados a la misma red y podrán comunicarse entre sí.

## 4. Ejemplo práctico

Vamos a definir una aplicación compuesta por dos servicios:

- **web:** servidor web Nginx.
- **db:** base de datos MySQL.

Archivo `compose.yaml`:

```yaml
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    networks:
      - red_aplicacion

  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: ejemplo
      MYSQL_DATABASE: aplicacion
    volumes:
      - datos:/var/lib/mysql
    networks:
      - red_aplicacion

volumes:
  datos:

networks:
  red_aplicacion:
```

En este ejemplo Docker Compose define dos servicios independientes que comparten una misma red. Además, el servicio de base de datos utiliza un volumen para conservar sus datos.

## 5. Consideraciones importantes

- La indentación es fundamental en YAML. Se recomienda utilizar espacios en lugar de tabulaciones.
- Los nombres de los servicios funcionan como identificadores dentro de Docker Compose.
- Las propiedades deben estar correctamente anidadas bajo el servicio correspondiente.
- No todas las propiedades son obligatorias. Dependen de las necesidades de cada servicio.
- Las secciones `volumes` y `networks` permiten declarar recursos que posteriormente pueden utilizar los servicios.
- No es necesario declarar manualmente una red para cada aplicación: Docker Compose crea una red predeterminada si no se especifica otra.

## 6. Documentación oficial

- [Compose file reference](https://docs.docker.com/reference/compose-file/)
- [Docker Compose overview](https://docs.docker.com/compose/)