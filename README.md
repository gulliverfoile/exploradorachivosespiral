 🌀 Organizador Espiral de Archivos

**Versión 3.0 – Adaptativa | Menú espiral áureo | Comandos por voz**

## ¿Qué es esto?

Una aplicación web que te permite **explorar, mover, copiar, renombrar y eliminar archivos** de tu disco duro (o memoria del móvil) usando una interfaz visual con un **menú espiral** que aparece justo donde haces clic.

No necesitas instalar nada. Solo un navegador moderno (Chrome, Edge, Opera) y abrir el archivo `organizador.html` con un servidor local o desde GitHub Pages.

## ¿Qué hace?

- **Explora carpetas** en un árbol desplegable (estilo explorador de Windows).
- **Muestra los archivos** como tarjetas con iconos.
- **Menú espiral áureo** que emerge desde el punto donde haces clic (o mantienes pulsado en móvil).
- **5 acciones rápidas** configurables: Mover, Copiar, Renombrar, Eliminar, Cambiar extensión.
- **Chat / consola de comandos** con reconocimiento de voz (escribe o habla órdenes como `mover *.pdf a Documentos`).
- **Modo oscuro** persistente.
- **Panel de configuración** donde puedes cambiar el menú, el tamaño de los botones y el modo de interacción, todo editando un JSON en caliente.
- **Adaptable a cualquier pantalla** (PC, tablet, móvil). La espiral escala y se reposiciona automáticamente para no salirse del viewport.

## Modos de interacción

Puedes elegir entre dos modos desde el panel ⚙️:

| Modo | PC (ratón) | Móvil (dedo) |
|------|------------|--------------|
| `menuDirecto` (por defecto) | Un clic izquierdo abre el menú espiral directamente | Pulsación larga (500 ms) abre el menú |
| `seleccionYMenu` | Un clic **selecciona** el archivo (borde azul). Doble clic abre el menú espiral. | Toque corto selecciona, pulsación larga abre el menú |

Además, en ambos modos:
- **Clic derecho** (PC) siempre abre el menú espiral.
- **Pulsación larga** (móvil) siempre abre el menú espiral.

## Cómo se usa

### Requisitos previos
- Un navegador compatible con la **File System Access API** (Chrome 86+, Edge 86+, Opera 72+).
- Para probarlo en PC: **servir el archivo con un servidor local** (no funciona abriendo el `.html` directamente desde `file://`).
- En móvil (Android): subirlo a **GitHub Pages** o similar, o usar un servidor local como `Termux` + `python`.

### Primeros pasos (PC)

1. Guarda el código como `organizador.html`.
2. Abre una terminal en la carpeta donde lo guardaste.
3. Ejecuta un servidor local. Con Python 3:
   ```bash
   python -m http.server 8000
Abre http://localhost:8000/organizador.html en Chrome.

Haz clic en "📁 Abrir carpeta" y selecciona un directorio de tu PC.

Explora el árbol (panel derecho) y los archivos (panel izquierdo).

Clic izquierdo sobre un archivo → aparece el menú espiral. Elige una acción.

Para comandos de voz, haz clic en el 🎤, habla y la orden se ejecutará automáticamente.

Primeros pasos (móvil)
Sube organizador.html a GitHub Pages (repositorio → Settings → Pages → Source: main, carpeta root).

Abre la URL en Chrome para Android.

Toca "📁 Abrir carpeta" y selecciona una carpeta de tu dispositivo.

Mantén pulsado un archivo → aparece el menú espiral. Elige la acción.

Puedes usar el chat o el micrófono para comandos rápidos.

Comandos de chat / voz
Escribe (o habla) frases como:

mover *.pdf a Documentos

copiar foto_* a Fotos

renombrar .jpeg a .jpg

cambiar extension txt a html

eliminar *.tmp

La aplicación te pedirá confirmación antes de ejecutar operaciones masivas.

Personalizar el menú
Pulsa el botón ⚙️ (esquina superior derecha).

Se abre un panel lateral con un editor JSON.

Puedes cambiar:

modoInteraccion: "menuDirecto" o "seleccionYMenu"

buttonSize: tamaño de los botones del menú (por defecto 48)

actions: lista de acciones, iconos y etiquetas.

Pulsa "Aplicar" y el menú se actualizará al instante.

Estructura del proyecto
El código está organizado en módulos independientes con un bus de eventos central:

EventBus: comunicación desacoplada entre componentes.

PersistenceService: guarda configuraciones en localStorage.

FileSystemService: toda la interacción con la File System Access API.

CommandParser: interpreta comandos de texto.

SpiralMenuUI: dibuja y anima el menú espiral.

TreeViewUI: panel de navegación en árbol.

FileListUI: panel de resultados (tarjetas de archivos).

VoiceInput: reconocimiento de voz.

DrawerUI: panel de configuración.

App: orquestador principal.

Limitaciones conocidas
Solo funciona dentro de la carpeta que selecciones (por seguridad del navegador).

En iOS, la File System Access API aún no está soportada.

Las operaciones de mover/renombrar en archivos muy grandes pueden ser lentas (copian el contenido).

La profundidad de escaneo del árbol está limitada a 3 niveles para no saturar.

¿Dudas o sugerencias? ¡A mejorar se ha dicho! 🚀
