# FutbolWebApp

Este es mi trabajo de practicas de DataFlex,en el cual sincronizo la base de datos con Dataflex,una vez hecho eso me ha permitido gestionar ligas, equipos, entrenadores, jugadores y posiciones de fútbol, y todo conectado a base de datos MySQL.

**Autor:** Antonio José Navarro Ortega

---

## Herramientas que he usado

| Herramienta | Versión |
|---|---|
| DataFlex Studio (licencia Personal) | 2025 (25.0) |
| MySQL Server | 8.4.13 LTS |
| MySQL Connector/ODBC (64 bits, Unicode) | 26.10 |
| MySQL Workbench | 26.10 |
| Git y GitHub | Gitflow |

---

## Qué he hecho

1. He creado la base de datos en MySQL a partir del script que nos pasaron.
2. He creado el workspace y el proyecto **FutbolWebApp** (Mobile Web Project).
3. He conectado la base de datos con el proyecto (conexión `FOOTBALL`, driver `ODBC_DRV`).
4. He llevado a MySQL las tablas embebidas que vienen por defecto: `CodeType`, `CodeMast`, `WebAppSession`, `WebAppUser`, `WebAppServerProps` y `DFLastID`.
5. He traído a DataFlex las tablas de MySQL (`entrenador`, `equipo`, `jugador`, `jugadorposicion`, `liga` y `posicion`), con sus 5 relaciones y sus Data Dictionaries.
6. He creado las vistas **Select** y **Zoom** de `posicion`, `liga`, `equipo`, `entrenador` y `jugador`.
7. He añadido en `Dashboard.wo` una tarjeta para cada una de esas tablas.

Además, como extra, le he dado a la aplicación un aspecto con temática de fútbol (lo explico más abajo).

---

## Cómo ejecutarlo

1. Instalar **MySQL 8.4** y ejecutar el script `football.sql`, que crea la base de datos `football`.
2. Instalar **MySQL Connector/ODBC 26.10 (64 bits)**.
3. Revisar la conexión en `Data/DFConnId.ini` (usuario y contraseña de MySQL y nombre del driver ODBC).
4. Abrir el workspace con DataFlex Studio 2025, compilar y ejecutar `WebApp.src`.
5. Entrar en `http://localhost/FutbolWebApp` con el usuario **admin** y la contraseña **admin**.

---

## Cómo he organizado el trabajo con Gitflow

- `main`: el producto final.
- `develop`: donde he ido juntando cada funcionalidad cuando estaba terminada y funcionando.
- He creado una rama `feature` para cada funcionalidad y la he fusionado en `develop` al acabarla:
  - `feature/configuracion-bd`: puntos 4 y 5 (las tablas).
  - `feature/vista-posicion`, `feature/vista-liga`, `feature/vista-equipo`, `feature/vista-entrenador` y `feature/vista-jugador`: punto 6, una rama por vista.
  - `feature/dashboard-tiles`: punto 7, las tarjetas del Dashboard.
  - `feature/mejoras-visuales`: las mejoras visuales.
  - `feature/documentacion`: este README.

---

## Decisiones que he tomado y por qué

- **Nombre de la base de datos:** he usado `football`, que es el nombre que viene definido en el script que nos pasaron, para no modificarlo.
- **Tabla DFLastID:** DataFlex 2025 crea esta tabla de sistema sin ninguna columna, y MySQL no permite crear tablas sin columnas visibles (me daba el error 4028 al convertirla). Para poder llevarla a MySQL como pedía la tarea, le he añadido una columna contador (`Contador`). En una base de datos SQL el autoincremento lo hace la propia base de datos, así que esa columna no se llega a usar.
- **Conexión con MySQL:** he usado una cadena de conexión sin DSN, para que el proyecto no dependa de tener un origen de datos configurado en cada ordenador. El usuario y la contraseña van dentro de la cadena en `DFConnId.ini`, porque la aplicación web no conseguía leer la contraseña cifrada y fallaba al arrancar. Lo he dejado así porque es un proyecto de prácticas en local.
- **Campos de las fichas (vistas Zoom):** en las fichas que dependen de otra tabla (equipo → liga, entrenador y jugador → equipo) muestro el ID y el nombre de la tabla padre, con un botón de búsqueda para elegirla. El campo de la clave foránea (`LigaID` o `EquipoID`) no lo pongo en pantalla porque DataFlex lo rellena solo gracias a la relación. El resto de datos de la tabla padre se ven y se editan en su propia vista.
- **Campo `liga.Equipos`:** es un valor que viene guardado en la tabla. No se recalcula solo al crear o borrar equipos.

---

## Mejoras visuales (extra)

He puesto todos los estilos en `AppHtml/CssStyle/application.css`, sin tocar el tema original de DataFlex (`Df_Material`), para que no se pierdan si se actualiza:

- He cambiado la paleta del tema de azul a verde usando sus variables CSS.
- He puesto un fondo de césped a franjas en todas las pantallas.
- El Dashboard tiene tarjetas de colores, cada una con su icono.
- Las listas y las fichas tienen un estilo de "marcador nocturno".
- He añadido **banderas** en la nacionalidad de jugadores y entrenadores y en el país de las ligas. Las imágenes se cargan de [flagcdn.com](https://flagcdn.com), así que hace falta conexión a internet para verlas.
- Cada posición tiene su **icono**.
- Cada equipo tiene una **insignia** con sus iniciales y sus colores.

Las funciones que generan las banderas, los iconos y las insignias están en `AppSrc/Banderas.pkg`.