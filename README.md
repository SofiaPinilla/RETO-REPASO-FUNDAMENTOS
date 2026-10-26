# Reto por equipos: personajes con PostgreSQL y Python

## 🎯 Objetivo del reto

Desarrollad una aplicación en Python para crear personajes, guardarlos en PostgreSQL y consultar sus datos. Todos los equipos trabajaréis con personajes y utilizaréis la tabla `characters` con los campos indicados en este enunciado.

**Modalidad:** por equipos. **Entrega:** un repositorio de GitHub por equipo.

> Este reto es para practicar, explorar y reforzar lo aprendido en clase. Los tres extras son opcionales.

## 🤝 Organización del trabajo

- Una persona creará el repositorio y añadirá al resto como colaboradores.
- Repartid las tareas y revisad el trabajo juntos.
- Deberéis al menos crear una PR.
- Podéis utilizar [Live Share de VS Code](https://visualstudio.microsoft.com/es/services/live-share/) para colaborar.

## 🪜 Reto base

### 1. Preparad el entorno con Docker

- Cread la carpeta del proyecto.
- Configurad primero un servicio PostgreSQL en Docker Compose y un volumen para conservar los datos.
- Definid las variables de configuración en un archivo `.env`, incluyendo `DATABASE_URL`.
- Comprobad la conexión desde la extensión PostgreSQL de VS Code que ya tenéis instalada.
- Cread los archivos de Python, la lista de dependencias y el Dockerfile antes de añadir el servicio de Python a Docker Compose.
- Excluid `.env` del repositorio y del contexto de construcción de la imagen. Incluid `.env.example` con valores de ejemplo.

### 2. Conectad Python con PostgreSQL

- Utilizad la librería `psycopg`.
- Leed la dirección de conexión desde `DATABASE_URL`.
- Mostrad un mensaje que permita comprobar que la conexión se ha establecido.

### 3. Cread la tabla `characters`

La tabla debe contener los siguientes campos:

| Campo | Tipo | Restricción |
|---|---|---|
| `id` | `INTEGER` | Clave primaria |
| `name` | `TEXT` | Obligatorio |
| `status` | `TEXT` | — |
| `species` | `TEXT` | — |
| `type` | `TEXT` | — |
| `gender` | `TEXT` | — |
| `origin_name` | `TEXT` | — |
| `location_name` | `TEXT` | — |
| `image` | `TEXT` | Opcional |
| `url` | `TEXT` | Opcional |
| `created` | `TIMESTAMPTZ` | — |

Podéis crear la tabla desde postgresql directamente.

### 4. Cread vuestro archivo en python

- Antes de seguir tenéis que tener creado vuestro archivo en python y su conexión a la abse de datos

### 5. Insertad los personajes

- Preparad los datos de vuestros personajes para guardarlos en la tabla.
- Utilizad inserciones normales con `INSERT` y `cur.executemany()`.

### 6. Comprobad el resultado

- Realizad un `SELECT` que recupere el identificador, el nombre y la especie de los primeros diez personajes, ordenados por identificador.
- Recuperad las filas con `fetchall()` y mostradlas en consola.
- Mostrad también el número total de personajes guardados.

### 7. Ejecutad el proyecto completo

La carga debe poder ejecutarse desde el contenedor de Python. Documentad cómo arrancar la base de datos, construir la imagen y ejecutar la aplicación.

**Resultado esperado:** personajes guardados en PostgreSQL y una muestra de los registros en la consola.

## 💡 Extras opcionales generales

Estos extras están disponibles para todos los equipos. Podéis hacer uno, varios o ninguno. Todos pueden realizarse de manera independiente una vez terminado el reto base.

### ⭐ Extra 1: visualización con Matplotlib

Cread una visualización a partir de los datos almacenados en PostgreSQL:

- Consultad cuántos personajes hay de cada especie.
- Representad el resultado en un gráfico de barras con Matplotlib.
- Situad las especies en el eje X y la cantidad de personajes en el eje Y.
- Añadid título y etiquetas legibles.
- Guardad el gráfico como `grafico.png` y haced que quede accesible desde vuestro ordenador al ejecutar el proyecto con Docker.

**Resultado esperado:** una imagen con el recuento por especie de los personajes que habéis cargado.

### ⭐ Extra 2: API con FastAPI

Cread una API con FastAPI que consulte los datos de PostgreSQL:

- Incluid una ruta `GET /` con un mensaje de bienvenida.
- Incluid una ruta `GET /species` que devuelva el recuento de personajes por especie.
- La respuesta de `/species` debe ser una lista JSON de objetos con los campos `species` y `count`.
- Obtened el recuento consultando la base de datos, sin escribir los resultados manualmente.
- Gestionad correctamente las conexiones a PostgreSQL.
- Ejecutad la API con Uvicorn en un servicio de Docker Compose y publicad un puerto para acceder desde el navegador.
- Comprobad las rutas y la documentación interactiva en `/docs`.

**Resultado esperado:** una API accesible desde vuestro ordenador que devuelva el recuento real de vuestra base de datos.

### ⭐ Extra 3: rellenad la base de datos desde una API

Ampliad el proyecto para importar personajes de la [API pública de Rick & Morty](https://rickandmortyapi.com/api/character).

Este extra propone investigar **cómo consumir una API desde Python**, un contenido que todavía no hemos trabajado en clase.

- Investigad la librería `requests` y cómo realizar una petición GET y leer una respuesta JSON.
- Consultad la [documentación de la API](https://rickandmortyapi.com/documentation/) para identificar los personajes y sus campos.
- Descargad al menos una página de personajes.
- Adaptad los datos recibidos a los campos de vuestra tabla. Guardad los nombres del origen y de la ubicación en `origin_name` y `location_name`.
- Insertad los personajes descargados en PostgreSQL desde Python.
- Evitad conflictos entre los identificadores importados y los de vuestros personajes. La importación debe conservar los personajes creados en el reto base.
- Gestionad posibles errores en la petición y documentad cómo ejecutar la importación.
- Como ampliación adicional, permitid descargar varias páginas mediante una variable de entorno `RM_PAGES`.

**Resultado esperado:** vuestra base de datos contiene también personajes importados de la API y podéis consultarlos desde Python.

## 📦 Entrega en GitHub

Entregad un enlace al repositorio del equipo por el canal indicado en clase.

El repositorio debe incluir:

- El código de la aplicación y las dependencias necesarias.
- El Dockerfile y la configuración de Docker Compose.
- Las sentencias SQL utilizadas.
- Los archivos de exclusión y `.env.example`, sin credenciales reales.
- Un `README.md` con los integrantes, el reparto de tareas, los pasos de ejecución y una muestra del resultado.
- Los archivos y resultados de los extras que hayáis completado.

**No subáis `.env`.** Aseguraos de que el repositorio sea accesible para su revisión.

[Diapositivas de ayuda de Git](https://marinadeempresas-my.sharepoint.com/:p:/g/personal/scpinilla_edem_es/EXLF_hosFdBGrxomRBcIXw4BrVLHWcDV-gOCGiuBJ0wdrw?e=Mi6d4S)

## ✅ Lista de comprobación

- [ ] PostgreSQL y Python funcionan con Docker Compose.
- [ ] La conexión utiliza `DATABASE_URL`.
- [ ] La tabla contiene los once campos indicados.
- [ ] Se han creado al menos diez personajes originales de tres especies diferentes.
- [ ] Los personajes se insertan con `executemany()` y consultas parametrizadas.
- [ ] Se muestran los primeros registros y el total guardado.
- [ ] Los cambios se confirman y los recursos se cierran correctamente.
- [ ] Todos los integrantes han contribuido al proyecto.
- [ ] El repositorio contiene instrucciones de ejecución y no incluye `.env`.

## 👥 Equipos

| Equipo | Integrantes |
|---|---|
| 1 | RAUL_FERRIS (MDES) · Jana Mei Cervera Monzó (MDIA) · JORGE_OLIVER (MDIA) · LOLA_BONET (MDIA) |
| 2 | ANTONIO_NAVARRO (MDES) · CHRISTIAN_VAZQUEZ (MDIA) · PABLO_LEGORBURO (MDIA) · JADE_LOPEZ (MDIA) |
| 3 | NICO_GOMEZ (MDES) · OSCAR_HERREROS (MDIA) · RAFA_BROTONS (MDIA) · JAVIER_MARTINEZ (MDIA) |
| 4 | JAIME_SANFELIX (MDES) · ANDRES_GIMENO (MDIA) · JUANJO_PRADES (MDIA) · INGRID (MDIA) |
| 5 | DAVID_GALLART (MDES) · Laura Soler Úbeda (MDIA) · HUGO_GAVILAN (MDIA) · JOAQUIN_VILLALOBOS (MDIA) |
| 6 | MARIO_GONZALEZ (MDES) · PABLO_CUNAT (MDIA) · IGNACIO-PINAZO (MDIA) · MANOLO_TORTAJADA (MDIA) |
| 7 | IGNACIO_IBÁÑEZ-RIZO (MDES) · LORENZO_SABBATINI (MDIA) · ALEJANDRO-CERVERA (MDIA) · LUCAS_OSEJO (MDIA) |
| 8 | RICARDO_ROMAN (MDES) · FRAN_ALAPONT (MDIA) · JORGE_DURA (MDIA) |
| 9 | CARLOS_GUTIERREZ (MDES) · ADRIAN_LAZARO (MDIA) · ANGEL_CARLOS_PEREZ (MDIA) |

## 📝 Valoración Docker

[Enlace valoración Docker](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=pVBtoIGmCke54xPWNTvJyDEzMUJZn2RIpZFlSKtDi5BUMldTSUpFOFNBQ05OVFdMTVVFVldPVjBDVCQlQCNjPTEu&ctx=%7B%22IDFormulario%22%3A%22cc4ad46b06bd8b8489944a8b7be0c2f535ce8b96453bd778ffa0cfcf6acabc35%22%2C%22Programa%22%3A%22M%C3%A1ster%20en%20Desarrollo%20Web%22%2C%22Grupo%22%3A%22A%22%2C%22Asignatura%22%3A%22FUNDAMENTOS%22%2C%22NombreDocente1%22%3A%22Sofia%20Pinilla%22%2C%22NombreDocente2%22%3A%22Javier%20Plaza%20Rosique%22%2C%22NombreDocente3%22%3A%220%22%7D)

