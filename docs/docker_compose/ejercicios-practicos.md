# Ejercicios prácticos de Docker

**Objetivo:** consolidar los conocimientos de Docker mediante 10 ejercicios prácticos, desde la gestión básica de contenedores hasta la creación de aplicaciones multicontenedor con Docker Compose.

---

# Nivel 1 — Fundamentos

*Dificultad: Fácil*

## Ejercicio 1. Primer contenedor

1. Descarga la imagen `nginx` desde Docker Hub.
2. Comprueba que se ha descargado correctamente.
3. Crea un contenedor llamado `mi_servidor`.
4. Ejecuta el contenedor en segundo plano.
5. Comprueba que está en ejecución.
6. Consulta sus registros.
7. Detén el contenedor.
8. Vuelve a iniciarlo y finalmente elimínalo.

**Conceptos:** imágenes, contenedores y comandos básicos.

## Ejercicio 2. Servidor web con puertos

1. Ejecuta un contenedor Nginx llamado `servidor_web`.
2. Publica el puerto 80 del contenedor en el puerto 8080 de tu equipo.
3. Accede desde el navegador a `http://localhost:8080`.
4. Comprueba qué puertos tiene publicados el contenedor.
5. Detén y elimina el contenedor.

**Conceptos:** publicación de puertos, `-p`, `inspect` y comunicación entre host y contenedor.

---

# Nivel 2 — Configuración y almacenamiento

*Dificultad: Fácil - Intermedia*

## Ejercicio 3. Variables de entorno

1. Ejecuta un contenedor MySQL 8.
2. Configura la contraseña del usuario root mediante una variable de entorno.
3. Crea una base de datos llamada `tienda`.
4. Comprueba que las variables se han configurado correctamente.
5. Consulta los registros del contenedor.
6. Accede al contenedor y comprueba que MySQL está funcionando.

**Conceptos:** variables de entorno, `-e`, `exec` y `logs`.

## Ejercicio 4. Persistencia de datos mediante volúmenes

1. Crea un volumen llamado `datos_mysql`.
2. Ejecuta un contenedor MySQL utilizando ese volumen.
3. Crea una base de datos llamada `empresa`.
4. Crea una tabla e introduce varios registros.
5. Detén y elimina el contenedor.
6. Vuelve a crear otro contenedor utilizando el mismo volumen.
7. Comprueba que la base de datos y sus registros siguen existiendo.
8. Consulta la información del volumen.

**Conceptos:** volúmenes, persistencia de datos y ciclo de vida de los contenedores.

## Ejercicio 5. Bind mounts

1. Crea una carpeta llamada `web` en tu equipo.
2. Dentro de ella, crea un archivo `index.html`.
3. Introduce un pequeño contenido HTML.
4. Ejecuta un contenedor Nginx.
5. Monta la carpeta `web` del equipo en `/usr/share/nginx/html` del contenedor.
6. Accede desde el navegador al servidor web.
7. Modifica el archivo `index.html` desde tu equipo.
8. Actualiza el navegador y comprueba que los cambios aparecen sin recrear el contenedor.

**Conceptos:** bind mounts, rutas del host y rutas del contenedor.

---

# Nivel 3 — Redes y Docker Compose

*Dificultad: Intermedia*

## Ejercicio 6. Comunicación entre contenedores

1. Crea una red personalizada llamada `red_aplicacion`.
2. Ejecuta dos contenedores Nginx conectados a esa red.
3. Asigna los nombres `web1` y `web2`.
4. Comprueba que ambos contenedores están conectados a la red.
5. Accede desde `web1` a `web2` utilizando su nombre.
6. Consulta la información de la red.
7. Desconecta uno de los contenedores y comprueba que deja de pertenecer a la red.

**Conceptos:** redes bridge, comunicación entre contenedores, DNS interno y comandos de redes.

## Ejercicio 7. Primera aplicación con Docker Compose

Crea una aplicación formada por dos servicios:

- `web`: servidor Nginx.
- `db`: base de datos MySQL.

Requisitos:

1. Crea un directorio para el proyecto.
2. Crea un archivo `compose.yaml`.
3. Define los dos servicios.
4. Configura las variables de entorno necesarias para MySQL.
5. Publica el puerto 8080 del servicio web.
6. Inicia los servicios en segundo plano.
7. Comprueba que ambos contenedores están funcionando.
8. Consulta los registros de cada servicio.
9. Detén y elimina los servicios utilizando Docker Compose.

**Conceptos:** servicios, `compose.yaml`, variables de entorno, puertos y comandos Compose.

---

# Nivel 4 — Aplicaciones completas

*Dificultad: Intermedia - Avanzada*

## Ejercicio 8. Aplicación con persistencia y configuración externa

Amplía el ejercicio anterior incorporando una configuración más completa.

Requisitos:

1. Utiliza Docker Compose para gestionar los servicios.
2. Crea un archivo `.env` con las credenciales de MySQL.
3. Utiliza las variables del archivo `.env` dentro de `compose.yaml`.
4. Crea un volumen llamado `datos_mysql`.
5. Asocia el volumen al directorio de datos de MySQL.
6. Configura una red personalizada llamada `red_app`.
7. Conecta los servicios a esa red.
8. Comprueba que el servicio web puede comunicarse con la base de datos utilizando su nombre.
9. Elimina los contenedores y vuelve a iniciarlos.
10. Comprueba que los datos de MySQL siguen existiendo.

**Conceptos:** Docker Compose, `.env`, `environment`, volúmenes, redes y persistencia.

## Ejercicio 9. Crear una imagen personalizada

Crea tu propia imagen Docker utilizando un Dockerfile.

Requisitos:

1. Crea un directorio llamado `mi_imagen`.
2. Dentro, crea un archivo `index.html` con contenido HTML.
3. Crea un `Dockerfile` basado en la imagen `nginx`.
4. Copia el archivo HTML al directorio web de Nginx.
5. Construye una imagen llamada `mi_web`.
6. Ejecuta un contenedor utilizando tu imagen.
7. Publica el puerto 8080 del equipo anfitrión.
8. Comprueba desde el navegador que se muestra tu página.
9. Consulta las imágenes y contenedores creados.

**Conceptos:** Dockerfile, `FROM`, `COPY`, `build`, imágenes personalizadas y contenedores.

## Ejercicio 10. Proyecto final: aplicación multicontenedor

Desarrolla una infraestructura completa para una aplicación de gestión de tareas.

La aplicación debe contar con tres servicios:

- `web`: servidor web Nginx.
- `app`: aplicación propia construida mediante un Dockerfile.
- `db`: base de datos MySQL.

### Requisitos

**1. Estructura del proyecto**

Organiza el proyecto de la siguiente manera:

```text
gestion-tareas/
├── compose.yaml
├── .env
├── .gitignore
├── app/
│   ├── Dockerfile
│   └── archivos de la aplicación
└── web/
    └── index.html
```

**2. Servicios**

- Define los tres servicios en `compose.yaml`.
- Utiliza imágenes oficiales cuando corresponda.
- Construye la imagen del servicio `app` mediante un Dockerfile.
- Configura las dependencias entre servicios.

**3. Redes**

- Crea una red personalizada llamada `red_tareas`.
- Conecta los tres servicios a ella.
- Permite que la aplicación se comunique con MySQL utilizando el nombre del servicio.

**4. Volúmenes**

- Crea un volumen llamado `datos_tareas`.
- Utilízalo para conservar la información de MySQL.
- Comprueba que los datos sobreviven a la eliminación de los contenedores.

**5. Variables de entorno**

- Configura las credenciales de MySQL mediante un archivo `.env`.
- Evita escribir directamente las contraseñas en `compose.yaml`.
- Añade `.env` a `.gitignore`.

**6. Gestión de la infraestructura**

- Construye las imágenes necesarias.
- Inicia todos los servicios.
- Comprueba su estado.
- Consulta los registros.
- Accede a los contenedores.
- Reinicia los servicios.
- Detén y elimina la infraestructura sin perder los datos persistentes.

**7. Documentación**

Crea un `README.md` que explique:

- La finalidad del proyecto.
- La función de cada servicio.
- La estructura de directorios.
- Cómo iniciar y detener la aplicación.
- Cómo se gestionan las redes y los volúmenes.

**Conceptos:** Dockerfile, imágenes personalizadas, servicios, Compose, redes, volúmenes, variables de entorno y administración de contenedores.

---

# Recomendaciones

- Completa los ejercicios en orden.
- Intenta resolver cada apartado sin consultar soluciones.
- Comprueba el resultado de cada comando antes de continuar.
- Utiliza `docker inspect`, `docker logs` y `docker compose config` cuando necesites diagnosticar problemas.
- No elimines volúmenes sin comprobar antes qué datos contienen.
- Guarda los archivos de configuración y las soluciones en tu repositorio de apuntes.

**Objetivo final:** ser capaz de construir, configurar, ejecutar y administrar una aplicación multicontenedor utilizando Docker y Docker Compose.