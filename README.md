# Prototipo ATLAS — Fusión del equipo

Prototipo web de **Project ATLAS** (Portal del Colaborador gamificado), construido por **Top-Down Studios** como entregable de prototipo web. Es un solo archivo HTML autocontenido — no necesita instalación, servidor ni conexión a internet para funcionar (excepto para cargar las tipografías de Google Fonts).

## Cómo abrirlo

Haz doble clic en `prototipo_atlas_fusion.html` y ábrelo con cualquier navegador moderno (Chrome, Edge, Firefox, Safari). No requiere `npm install`, servidor local, ni build previo.

> Si algo no se ve bien al abrirlo como archivo local, sírvelo con un servidor simple (`python3 -m http.server`) y ábrelo desde `http://localhost:8000/` — pero en la mayoría de los navegadores no hace falta.

## Qué incluye

El prototipo tiene 3 vistas, accesibles desde las pestañas de arriba:

| Vista | Qué muestra |
|---|---|
| 🏢 **Hub** | La oficina 2D jugable — mueve tu avatar y entra a cada estación |
| 📋 **Vista de lista** | Los 19 servicios como tarjetas, cargados vía un fetch simulado (patrón de API real) |
| 🗄️ **Base de datos** | 5 tablas de datos simulados (Usuarios, Solicitudes, Nómina, Documentos, Tareas) |

### Las 19 estaciones (todas funcionales, no solo descriptivas)

| Estación | Qué puedes hacer |
|---|---|
| Mis datos personales | Editar tus datos; barra de completitud en vivo |
| Solicitudes a RH | Elegir tipo y fechas, ver el cálculo real de días efectivos (excluye fines de semana y festivos), enviar la solicitud, ver el estado dual (gerencia + RH) |
| Nómina | Recibo de pago formateado + descarga simulada |
| Documentos | Ver documentos, confirmar "leí y entendí" el reglamento, subir documentación pendiente |
| Avisos oficiales | Marcar comunicados como leídos |
| Tareas y proyectos | Actualizar el % de progreso con un slider en vivo |
| Capacitaciones y evaluaciones | Marcar como completada → resolver una mini evaluación → certificado simulado |
| Encuestas internas | Responder una pregunta → ver resultados agregados en barras |
| Muro | Leer post-its y publicar uno nuevo |
| Ideas de mejora | Votar ideas existentes y proponer una nueva |
| Actividades internas | Registrar asistencia → se sella tu pasaporte digital |
| Objetivos de equipo | Barra de avance colectivo (nunca el resultado individual) |
| Clock-in / Clock-out | Marcar entrada/salida, con racha de días |
| Asistente de IA | Chat real con 3 NPCs especializados (Nomi · Nómina, Rita · Solicitudes, Dax · Documentos) |
| Tienda de recompensas | Canjear puntos por recompensas — valida si te alcanza |
| Prestaciones | IMSS, fondo de ahorro con barra de progreso, finiquito (informativo) |
| Kardex de asistencia | Calendario mensual interactivo — cada día muestra su tipo (asistencia/descanso/festivo/permiso/vacaciones/incapacidad) por color y por letra, clic para el detalle |
| Publicaciones RH | Noticias, avisos, comunicados, eventos y políticas, con filtros por tipo y banner de importantes |
| Mis Colaboradores | Vista de supervisor: asistencia y avance de capacitación del equipo directo |

Todas las acciones relevantes suman puntos al contador de arriba a la derecha (motor de gamificación compartido). Las últimas 4 estaciones se agregaron después de revisar un prototipo de referencia en Figma Make hecho por el equipo — se adaptaron al estilo visual del hub en vez de copiar su lenguaje de dashboard SaaS.

## Quién construyó qué

| Integrante | Rol | Su pieza |
|---|---|---|
| **Oscar** | Videojuego | Movimiento del avatar con física real (aceleración/fricción), volteo por dirección, polvo de pasos |
| **Ximena** | Web | Vista de lista responsive, patrón de fetch simulado que alimenta el hub y el menú de acceso rápido |
| **Gregor** | Base de datos | Visor de las 5 tablas simuladas, con los campos oficiales de la especificación de vacaciones del socio formador |
| **Andrea** | Líder de equipo | Configurador de empresa (paleta, logo, nombre) con aplicación en vivo y verificador de contraste WCAG |
| **Maximiliano** | Reto (IA + accesibilidad) | Chat de NPCs con voz tipo Animal Crossing (bips sintéticos, sin voz real) y subtítulos sincronizados |

Cada quien construyó su parte por separado como componente independiente; este archivo es la fusión de las 5 piezas en un solo prototipo coherente.

## Accesibilidad

- **Alto contraste**: repaleta toda la interfaz a blanco/negro/amarillo — y siempre gana sobre los colores personalizados de la empresa, aunque estén aplicados.
- **Texto grande**: escala el tamaño de fuente en toda la app.
- **Reducir movimiento**: desactiva animaciones (bob del avatar, polvo de pasos, efecto de escritura del chat) — también respeta `prefers-reduced-motion` del sistema automáticamente.
- **Voz de NPC**: apagable sin perder información — el texto del chat siempre es legible completo, independientemente del estado de la voz.
- Navegación completa por teclado en estaciones, menú de acceso rápido y modales.

## Cómo están los datos

Todo el "backend" vive en memoria dentro del navegador (`appState` en JavaScript) — no hay servidor, base de datos ni persistencia real. **Recargar la página reinicia todo** a sus valores iniciales. Esto es intencional: es un prototipo de validación de experiencia, no el producto final.

## Qué NO es real (para tener claro en la demo)

- El chat de NPCs responde por coincidencia de palabras clave, no por un LLM real — eso se conecta en el backend de Unity más adelante.
- No hay autenticación, roles (RH/Gerencia) ni base de datos real detrás.
- Los montos de nómina, solicitudes y demás son datos de ejemplo fijos.

## Documentos relacionados del proyecto

Este prototipo complementa (no sustituye) los documentos ya entregados del proyecto: la Propuesta de Proyecto, el Plan de Trabajo, el backlog de Jira/Trello, el Game Design Document, y la especificación de vacaciones del socio formador (PeopleTech / Eslabón Systems).

## Próximos pasos

- Construir la versión real en Unity (este prototipo es la referencia de UX, no el motor final).
- Conectar el chat de NPCs a un LLM real vía el backend/proxy de Maximiliano.
- Reemplazar `appState` por llamadas reales a la API de Ximena y la base de datos de Gregor.
