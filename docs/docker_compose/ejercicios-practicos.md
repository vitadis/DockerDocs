# Ejercicios prácticos de Docker Compose

**Objetivo:** consolidar los conocimientos de Docker Compose mediante 10 ejercicios prácticos, desde la definición de servicios básicos hasta el despliegue y administración de aplicaciones multicontenedor.

Todos los ejercicios deberán realizarse utilizando Docker Compose y el archivo `compose.yaml` como herramienta principal de configuración y gestión.

---

# Nivel 1 — Fundamentos de Docker Compose

*Dificultad: Fácil*

## Ejercicio 1. Primer servicio con Compose

Crea tu primer proyecto utilizando Docker Compose.

**Requisitos:**

1. Crea un directorio llamado `primer-proyecto`.
2. Dentro, crea un archivo `compose.yaml`.
3. Define un servicio llamado `web` utilizando la imagen `nginx`.
4. Configura el servicio para que se ejecute en segundo plano.
5. Inicia el servicio utilizando `docker compose up -d`.
6. Comprueba el estado de los servicios.
7. Consulta los registros del servicio.
8. Detén los servicios.
9. Elimina la infraestructura del proyecto.

**Conceptos:** `services`, `image`, `docker compose up`, `ps`, `logs` y `down`.

## Ejercicio 2. Publicación de puertos y configuración de servicios

Crea un servidor web accesible desde tu equipo anfitrión.

**Requisitos:**

1. Crea un proyecto llamado `servidor-web`.
2. Define un servicio llamado `nginx`.
3. Utiliza la imagen oficial `nginx`.
4. Publica el puerto 80 del contenedor en el puerto 8080 de tu equipo.
5. Configura el nombre del contenedor mediante `container_name`.
6. Inicia el proyecto en segundo plano.
7. Accede desde el navegador a `http://localhost:8080`.
8. Consulta la configuración resultante mediante `docker compose config`.
9. Detén y elimina el proyecto.

**Conceptos:** `ports`, `container_name`, `docker compose config` y publicación de puertos.

---

# Nivel 2 — Configuración y almacenamiento

*Dificultad: Fácil - Intermedia*

## Ejercicio 3. Variables de entorno

Despliega una base de datos MySQL utilizando variables de entorno.

**Requisitos:**

1. Crea un proyecto llamado `mysql-compose`.
2. Define un servicio llamado `db`.
3. Utiliza la imagen `mysql:8.0`.
4. Configura las siguientes variables de entorno:
   - `MYSQL_ROOT_PASSWORD`
   - `MYSQL_DATABASE`
   - `MYSQL_USER`
   - `MYSQL_PASSWORD`
5. Configura una base de datos llamada `tienda`.
6. Publica el puerto 3306 del contenedor en el puerto 3307 del equipo.
7. Inicia el servicio.
8. Consulta los registros de inicialización de MySQL.
9. Comprueba que las variables se han aplicado correctamente.
10. Detén y elimina el proyecto.

**Conceptos:** `environment`, variables de entorno, configuración de servicios y registros.

## Ejercicio 4. Persistencia mediante volúmenes

Despliega MySQL utilizando almacenamiento persistente administrado por Docker Compose.

**Requisitos:**

1. Crea un proyecto llamado `mysql-volumes`.
2. Define un servicio `db` utilizando MySQL.
3. Declara un volumen llamado `datos_mysql`.
4. Asocia el volumen al directorio `/var/lib/mysql`.
5. Configura las variables de entorno necesarias.
6. Inicia el servicio.
7. Accede a MySQL y crea una base de datos llamada `empresa`.
8. Crea una tabla e introduce varios registros.
9. Detén y elimina los contenedores mediante Compose.
10. Vuelve a iniciar el proyecto.
11. Comprueba que la base de datos y los registros siguen existiendo.
12. Elimina el proyecto y comprueba qué sucede con el volumen.
13. Elimina el volumen explícitamente cuando ya no necesites los datos.

**Conceptos:** `volumes`, volúmenes nombrados, persistencia y `docker compose down -v`.

## Ejercicio 5. Bind mounts y sincronización de archivos

Despliega un servidor Nginx cuyo contenido web se encuentre en tu equipo anfitrión.

**Requisitos:**

1. Crea un proyecto llamado `web-bind-mount`.
2. Crea un directorio `web`.
3. Dentro, crea un archivo `index.html`.
4. Introduce contenido HTML personalizado.
5. Define un servicio `nginx` en `compose.yaml`.
6. Monta el directorio `web` del equipo en `/usr/share/nginx/html`.
7. Publica el puerto 8080.
8. Inicia el servicio.
9. Accede desde el navegador a `http://localhost:8080`.
10. Modifica el archivo `index.html` desde tu equipo.
11. Comprueba que los cambios aparecen al actualizar el navegador sin recrear el contenedor.
12. Detén y elimina el proyecto.

**Conceptos:** bind mounts, `volumes`, rutas relativas y sincronización de archivos.

---

# Nivel 3 — Redes y administración multicontenedor

*Dificultad: Intermedia*

## Ejercicio 6. Comunicación entre servicios

Crea una infraestructura formada por dos servicios Nginx conectados mediante una red personalizada.

**Requisitos:**

1. Crea un proyecto llamado `red-compose`.
2. Define dos servicios llamados `web1` y `web2`.
3. Utiliza la imagen `nginx` en ambos servicios.
4. Declara una red personalizada llamada `red_aplicacion`.
5. Conecta ambos servicios a esa red.
6. Configura los alias de red necesarios para identificar los servicios.
7. Inicia la infraestructura.
8. Comprueba que ambos servicios están conectados a la red.
9. Accede desde un servicio al otro utilizando su nombre DNS.
10. Consulta la configuración de red mediante `docker compose config`.
11. Detén y elimina la infraestructura.

**Conceptos:** `networks`, redes personalizadas, comunicación entre servicios, DNS interno y alias.

## Ejercicio 7. Aplicación multicontenedor con Compose

Despliega una infraestructura formada por un servidor web y una base de datos.

**Servicios:**

- `web`: servidor Nginx.
- `db`: base de datos MySQL.

**Requisitos:**

1. Crea un proyecto llamado `aplicacion-compose`.
2. Define ambos servicios en `compose.yaml`.
3. Configura las variables de entorno necesarias para MySQL.
4. Publica el puerto 8080 del servicio web.
5. Declara una red personalizada llamada `red_app`.
6. Conecta ambos servicios a la red.
7. Configura una dependencia entre `web` y `db` mediante `depends_on`.
8. Inicia todos los servicios.
9. Comprueba el estado de los contenedores.
10. Consulta los registros individualmente.
11. Accede a la base de datos desde el servicio correspondiente.
12. Reinicia únicamente el servicio `db`.
13. Detén y elimina la infraestructura.

**Conceptos:** múltiples servicios, `depends_on`, redes, variables de entorno y administración individual de servicios.

---

# Nivel 4 — Configuración avanzada y proyectos completos

*Dificultad: Intermedia - Avanzada*

## Ejercicio 8. Configuración externa mediante archivos `.env`

Reestructura el proyecto anterior para separar la configuración sensible de la definición de los servicios.

**Requisitos:**

1. Crea un proyecto llamado `configuracion-externa`.
2. Crea un archivo `compose.yaml`.
3. Crea un archivo `.env`.
4. Define las siguientes variables:
   - `MYSQL_ROOT_PASSWORD`
   - `MYSQL_DATABASE`
   - `MYSQL_USER`
   - `MYSQL_PASSWORD`
   - `MYSQL_PORT`
5. Utiliza las variables del archivo `.env` dentro de `compose.yaml`.
6. Configura los puertos mediante interpolación de variables.
7. Declara una red personalizada.
8. Declara un volumen persistente para MySQL.
9. Añade el archivo `.env` a `.gitignore`.
10. Comprueba la configuración resultante mediante `docker compose config`.
11. Inicia los servicios.
12. Modifica una variable del archivo `.env`.
13. Aplica los cambios necesarios y comprueba el comportamiento.
14. Detén y elimina la infraestructura sin perder los datos persistentes.

**Conceptos:** `.env`, interpolación de variables, `environment`, `.gitignore`, `config` y persistencia.

## Ejercicio 9. Construcción de imágenes mediante Docker Compose

Crea una aplicación web utilizando una imagen personalizada construida desde un Dockerfile.

**Requisitos:**

1. Crea un proyecto llamado `build-compose`.
2. Crea un directorio `app`.
3. Dentro, crea un `Dockerfile`.
4. Utiliza `nginx` como imagen base.
5. Crea un archivo `index.html` con contenido personalizado.
6. Define un servicio llamado `web` en `compose.yaml`.
7. Configura la construcción de la imagen mediante `build`.
8. Establece el contexto de construcción.
9. Configura el Dockerfile que debe utilizarse.
10. Asigna un nombre personalizado a la imagen construida.
11. Publica el puerto 8080.
12. Construye e inicia el servicio mediante Compose.
13. Modifica el contenido de la aplicación.
14. Reconstruye la imagen y comprueba los cambios.
15. Consulta las imágenes y servicios del proyecto.
16. Detén y elimina la infraestructura.

**Conceptos:** `build`, `context`, `dockerfile`, `image`, construcción de imágenes y reconstrucción de servicios.

## Ejercicio 10. Proyecto final: infraestructura completa de gestión de tareas

Desarrolla una infraestructura completa para una aplicación de gestión de tareas utilizando Docker Compose.

La infraestructura estará formada por tres servicios:

- `web`: servidor Nginx que actúa como punto de entrada.
- `app`: aplicación propia construida mediante un Dockerfile.
- `db`: base de datos MySQL.

### 1. Estructura del proyecto

Organiza el proyecto de la siguiente manera:

```text
gestion-tareas/
├── compose.yaml
├── .env
├── .gitignore
├── README.md
│
├── app/
│   ├── Dockerfile
│   └── archivos de la aplicación
│
└── web/
    ├── default.conf
    └── index.html
```

### 2. Configuración de servicios

- Define los tres servicios en `compose.yaml`.
- Utiliza imágenes oficiales cuando corresponda.
- Construye la imagen de `app` mediante un Dockerfile.
- Configura los puertos necesarios.
- Establece las dependencias entre servicios.
- Configura las políticas de reinicio de los servicios.

### 3. Configuración de redes

- Declara una red personalizada llamada `red_tareas`.
- Conecta los tres servicios a dicha red.
- Permite que `app` se comunique con `db` utilizando el nombre del servicio.
- Evita publicar innecesariamente el puerto de MySQL en el equipo anfitrión.

### 4. Persistencia de datos

- Declara un volumen llamado `datos_tareas`.
- Asocia el volumen al directorio de datos de MySQL.
- Comprueba que la información persiste después de eliminar los contenedores.
- Evita eliminar accidentalmente los datos al detener la infraestructura.

### 5. Variables de entorno

- Crea un archivo `.env`.
- Configura las credenciales de MySQL.
- Utiliza interpolación de variables en `compose.yaml`.
- Añade `.env` a `.gitignore`.
- Evita introducir credenciales directamente en el archivo Compose.

### 6. Administración de la infraestructura

Realiza las siguientes operaciones utilizando exclusivamente Docker Compose:

- Validar la configuración.
- Construir las imágenes.
- Iniciar todos los servicios.
- Consultar el estado de los servicios.
- Consultar los registros.
- Acceder a los contenedores.
- Reiniciar servicios individualmente.
- Detener servicios.
- Reconstruir imágenes después de modificar el Dockerfile.
- Eliminar la infraestructura conservando los volúmenes.
- Volver a desplegar la aplicación.

### 7. Documentación

Crea un archivo `README.md` que incluya:

- Finalidad del proyecto.
- Función de cada servicio.
- Estructura de directorios.
- Tecnologías utilizadas.
- Configuración de las variables de entorno.
- Funcionamiento de las redes.
- Gestión de los volúmenes.
- Instrucciones para iniciar y detener la infraestructura.
- Procedimiento para reconstruir las imágenes.

**Conceptos:** Docker Compose, servicios, Dockerfile, build, redes, volúmenes, variables de entorno, dependencias, políticas de reinicio y administración de aplicaciones multicontenedor.

---

# Recomendaciones

- Completa los ejercicios en orden.
- Utiliza exclusivamente Docker Compose para administrar los recursos de los ejercicios.
- Intenta resolver cada ejercicio sin consultar soluciones.
- Comprueba la configuración mediante `docker compose config`.
- Utiliza `docker compose ps` y `docker compose logs` para diagnosticar problemas.
- No elimines volúmenes sin comprobar antes qué datos contienen.
- Guarda los archivos `compose.yaml`, `.env.example`, Dockerfiles y demás configuraciones en tu repositorio.
- Documenta los problemas encontrados y cómo los has solucionado.

**Objetivo final:** ser capaz de definir, construir, desplegar, configurar y administrar infraestructuras multicontenedor utilizando Docker Compose.
