# 🌀 Organizador Total + Laboratorio de Código

**Un explorador de archivos, un lanzador de juegos HTML y un editor de código con análisis en tiempo real… todo en una sola aplicación web.**

## ¿Qué es esto?

Una herramienta que reúne tres funciones en una sola interfaz:

- **📁 Organizador de archivos:** navega por carpetas, mueve, copia, renombra y elimina archivos directamente desde el navegador, con un menú contextual en forma de abanico (o anillo, espiral, columna… configurable).
- **🎮 Lanzador de juegos (GameLoader):** carga juegos HTML desde tu disco, los empaqueta automáticamente para evitar errores de CORS y los ejecuta en un contenedor virtual. Incluye un juego de demostración.
- **🔬 Laboratorio de código:** abre cualquier archivo de texto (JS, HTML, CSS…), edítalo con resaltado de sintaxis, analiza el código en busca de malas prácticas (`var`, `console.log`, `==`), aplica correcciones automáticas y renombra variables con un clic.

Todo funciona **offline** (salvo la carga inicial de librerías externas como CodeMirror) y puede instalarse como una aplicación independiente (PWA) en tu escritorio o móvil.

## 🚀 Cómo se usa

### Requisitos
- Un navegador moderno basado en Chromium: **Chrome, Edge, Opera**. (Firefox y Safari no soportan la API de acceso a archivos local).
- Para probarlo en local: **Python 3** (u otro servidor estático).

### Primeros pasos (PC)
1. Guarda el archivo como `organizador_total.html`.
2. Abre una terminal en la carpeta donde lo guardaste y ejecuta:
   ```bash
   python -m http.server 8000
En Chrome, visita http://localhost:8000/organizador_total.html.

Usa las pestañas superiores para cambiar entre:

📁 Organizador – Explora y gestiona archivos.

🎮 Juegos – Carga juegos HTML o ejecuta el servidor virtual de demostración.

🔬 Laboratorio – Edita y analiza código.

Organizador de archivos
Haz clic en "📁 Abrir carpeta" y selecciona un directorio de tu ordenador.

Navega por el árbol de carpetas (panel derecho) o por las tarjetas (panel izquierdo).

Clic izquierdo en un archivo → menú contextual en abanico con acciones (Mover, Copiar, Renombrar, Eliminar, Cambiar extensión).

Escribe comandos como mover *.pdf a Documentos en la barra de chat o usa el micrófono (solo en Chrome).

Juegos (GameLoader)
Ve a la pestaña 🎮 Juegos.

Para probar el sistema, pulsa "🚀 Iniciar servidor virtual (demo)". Verás un juego de ejemplo.

Para cargar tu propio juego, pulsa "📂 Cargar carpeta de juego", selecciona la carpeta que contiene tu juego (debe tener un index.html). El juego se empaquetará y aparecerá en la lista. Pulsa "▶ Ejecutar" para jugar.

Laboratorio de código
Ve a la pestaña 🔬 Laboratorio.

Desde el explorador de archivos (pestaña Organizador), haz clic en un archivo .js, .html, .css, etc. Se abrirá automáticamente en el editor.

También puedes escribir código directamente.

Selecciona el lenguaje (JavaScript o HTML) en el desplegable.

Usa los botones para:

🔍 Analizar – Busca var, console.log, == y falta de alt en imágenes.

🔧 Corregir 'var' – Cambia todos los var por let.

🗑️ Quitar logs – Elimina todas las líneas con console.log.

✏️ Renombrar – Coloca el cursor sobre una variable y renómbrala en todo el archivo.

💾 Guardar – Guarda los cambios directamente en el archivo original.

❓ Ayuda – Muestra consejos rápidos de buenas prácticas.

⚙️ Cómo funciona
Arquitectura
El código está organizado en módulos independientes que se comunican a través de un EventBus (arquitectura hexagonal simplificada):

EventBus – Permite que los componentes reaccionen a eventos sin conocerse entre sí.

PersistenceService – Guarda configuraciones y lista de juegos en localStorage.

FileSystemService – Toda la interacción con la File System Access API (abrir carpetas, leer, escribir, mover, copiar…).

GeometryEngine – Calcula las posiciones de los botones del menú contextual según la geometría elegida (abanico, anillo, espiral, columna).

ContextMenuUI – Dibuja y anima el menú contextual.

TreeViewUI y FileListUI – Muestran la estructura de carpetas y los archivos.

GameLoaderService – Crea un “servidor virtual” en memoria usando Blob URLs para ejecutar juegos sin errores de CORS.

CodeEditorUI – Carga CodeMirror dinámicamente y proporciona análisis de código básico.

VoiceInput – Integra la Web Speech API para reconocimiento de voz.

App – Orquesta todos los componentes, maneja las pestañas y las acciones del usuario.

APIs del navegador utilizadas
File System Access API (showDirectoryPicker, getFile, createWritable, remove…)

Web Speech API (SpeechRecognition)

Blob URLs (URL.createObjectURL, revokeObjectURL)

CodeMirror (librería externa para el editor)

localStorage para persistencia

¿Por qué hace falta un servidor local?
La API de acceso al sistema de archivos solo funciona en contextos seguros (https:// o http://localhost). Al usar python -m http.server creamos un servidor local que cumple ese requisito.

⚠️ Limitaciones conocidas
Solo funciona en navegadores basados en Chromium (Chrome, Edge, Opera).

Los permisos de carpeta no se guardan entre sesiones; tendrás que volver a seleccionar la carpeta al recargar la página.

Mover o copiar archivos muy grandes (>100 MB) puede ser lento porque se leen completamente en memoria.

El analizador de código es básico (reglas personalizadas). No reemplaza a un linter profesional como ESLint.

El GameLoader no soporta juegos con módulos ES6 (import/export) a menos que los empaquetes antes con una herramienta como esbuild.

🧑‍💻 Créditos y filosofía
Este proyecto nació como un experimento en pocas horas, con el objetivo de aprender, divertirse y demostrar que se pueden crear herramientas potentes con tecnologías web estándar, sin dependencias pesadas.

La arquitectura es modular, el código está comentado y cada pieza puede reemplazarse o ampliarse fácilmente. Si quieres añadir otra pestaña, otro tipo de análisis o una nueva geometría de menú, solo tienes que crear un nuevo componente y conectarlo al EventBus.

¿Dudas, ideas, mejoras? ¡A trastear se ha dicho! 🚀🌀
