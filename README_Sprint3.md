# FutbolWebApp: Sprint 3, Mejora visual

| | |
|---|---|
| **Rama** | `feature/mejoras-visuales-sprint3` |
| **Entrega** | 1 de diciembre de 2026 |
| **Cierre** | 8 de diciembre de 2026 |
| **Última actualización** | 27 de noviembre de 2026 |

Objetivo del sprint: seguir mejorando el aspecto visual de la aplicación con temática de fútbol y, a la vez, estudiar la documentación de DataFlex (Data Dictionaries, eventos y navegación).

Archivos propios modificados:
- `AppSrc/*.wo`: vistas de la aplicación.
- `AppSrc/Banderas.pkg`: funciones que generan el HTML de banderas, insignias, ligas, entrenador, plazas e iconos de posición.
- `AppHtml/CssStyle/application.css`: todo el estilo visual propio. Los archivos del framework (`theme.css`, `Index.html`) no se modifican.

---

## Estilo general
- Tema verde con fondo de césped y contenido en tarjetas oscuras estilo "marcador nocturno".

## Login
- Título propio con un balón que bota, el nombre de la app y un lema.
- Textos en español y botón **Entrar** con el estilo de la app.

## Listas (vistas Select)
- Cabecera con los títulos de las columnas en español (estilo marcador, texto dorado).
- **Banderas** junto a nacionalidades y países.
- **Insignias** de los equipos con sus colores (distintivo propio, no el escudo oficial).
- **Franja de colores** del club delante del nombre de jugadores y entrenadores.
- **Liga** en una etiqueta con la bandera de su país.
- Columna **Entrenador** en Equipos y Jugadores.
- Columna **Plazas** en Ligas: "3 / 20" con barra de ocupación (roja si la liga está llena).
- **Iconos** para cada posición (bota para las posiciones personalizadas).

## Fichas (vistas Zoom)
- Cabecera tipo **cromo** en las cinco fichas: franja del club, nombre, datos con etiquetas y un elemento grande a la derecha (dorsal, insignia, bandera, icono...).
- El cromo se actualiza solo al cambiar de registro (evento `OnNewCurrentRecord` de los DDO).
- En un registro nuevo muestra un aviso ("Nuevo jugador", "Nueva liga"...).

## Dashboard
- **Contador** de registros en cada tarjeta (por ejemplo "6 posiciones"), que se recalcula cada vez que se vuelve al Dashboard.

## Botones en español
- Listas: **Buscar** y **Nuevo**.
- Fichas: **Guardar**, **Editar**, **Eliminar** y **Deshacer cambios**.

## Corrección
- **Borrado de posiciones**: se añadió el DDO hijo `jugadorposicion` a la ficha de Posición, que el Data Dictionary necesita para poder borrar. Con `Cascade_Delete_State` a `False` no se borran en cascada las asignaciones de jugadores.