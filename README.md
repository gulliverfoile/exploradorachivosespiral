# 🌀 Asistente Total – Organizador, Laboratorio, Avatar y Transcriptor

**Una navaja suiza digital autocontenida que integra explorador de archivos, lanzador de juegos HTML, editor de código con análisis básico, avatar facial reactivo con voz y transcriptor de voz con detección de emociones. Todo desde el navegador, sin instalar nada.**

## ¿Qué es esto?

Un archivo HTML (más o menos largo) que reúne varias herramientas que normalmente usarías por separado:

- **📁 Organizador de archivos:** navega por tus carpetas, mueve, copia, renombra, borra archivos y cambia extensiones. Todo con un menú contextual en forma de abanico (o anillo, espiral, columna… tú eliges).
- **🎮 GameLoader:** carga juegos HTML desde tu disco, los empaqueta automáticamente para evitar errores de seguridad y los ejecuta en un contenedor virtual. Incluye un juego de demostración.
- **🔬 Laboratorio de código:** abre cualquier archivo de texto (JS, HTML, CSS…), edítalo con colores, analiza el código en busca de malas prácticas (`var`, `console.log`, `==`) y corrígelas con un clic. También permite renombrar variables de forma segura.
- **😸 Avatar (caritas):** una cara animada que refleja emociones (alegría, tristeza, sorpresa, enfado) según el texto que escribas. Puede hablar en voz alta con diferentes estilos y velocidades.
- **🎤 Transcriptor (escuchar):** reconocimiento de voz en tiempo real. Transcribe lo que dices, detecta la emoción en tus palabras y guarda un historial.
- **📋 Registro de acciones (log):** cada vez que mueves, copias o eliminas un archivo, queda registrado en un historial que puedes consultar y exportar como archivo `.txt`.

## 🚀 Cómo se usa

### Requisitos
- Un navegador basado en Chromium: **Chrome, Edge, Opera** (Firefox y Safari no permiten el acceso completo al sistema de archivos).
- Para probarlo en local: **Python 3** instalado (o cualquier otro servidor web estático).

### Pasos rápidos
1. Guarda el archivo como `asistente_total.html`.
2. Abre una terminal en la carpeta donde lo guardaste y ejecuta:
   ```bash
   python -m http.server 8000
En Chrome, visita http://localhost:8000/asistente_total.html.

Verás una barra superior con pestañas. Cada pestaña es una herramienta distinta:

📁 Organizador: haz clic en "Abrir carpeta", selecciona un directorio y empieza a gestionar archivos. Usa el chat para comandos como mover *.pdf a Documentos o el micrófono para dictar órdenes.

🎮 Juegos: pulsa "Iniciar servidor virtual (demo)" para ver un juego de ejemplo, o "Cargar carpeta de juego" para ejecutar tus propios juegos HTML.

🔬 Lab: haz clic en un archivo desde el organizador para abrirlo en el editor. Analiza, corrige y guarda cambios.

😸 Avatar: escribe un texto y pulsa "Hablar". La cara cambiará según el sentimiento de las palabras (puedes forzar una emoción con los botones inferiores).

🎤 Escuchar: pulsa el micrófono, habla y verás cómo transcribe y detecta tu estado de ánimo.

📋 Log: revisa todas las acciones realizadas sobre archivos y expórtalas si lo necesitas.

Atajos útiles
Ctrl+S en el laboratorio guarda el archivo que estás editando.

El menú contextual del organizador aparece al hacer clic izquierdo sobre un archivo (o clic derecho o pulsación larga en móvil).

Desde el botón ⚙️ puedes cambiar la geometría del menú, el tamaño de los botones y el modo de interacción.

🧠 Cómo funciona (arquitectura)
El código está organizado en módulos independientes que se comunican a través de un EventBus (un sistema de eventos). Así, cuando algo ocurre (por ejemplo, mueves un archivo), el módulo de archivos emite un evento y el módulo de log lo recoge sin que uno sepa nada del otro.

Principales piezas
EventBus: centralita de eventos.

PersistenceService: guarda configuraciones, frases, historiales… en localStorage.

FileSystemService: toda la magia de leer, escribir y modificar archivos reales usando la File System Access API (solo en Chromium).

GeometryEngine: calcula la posición de los botones del menú contextual según la forma elegida (abanico, anillo, espiral, columna).

ContextMenuUI: dibuja y anima el menú emergente.

TreeViewUI / FileListUI: muestran la estructura de carpetas y los archivos.

GameLoaderService: crea un “servidor virtual” con Blob URLs para que los juegos HTML funcionen sin problemas de CORS.

CodeEditorUI: carga dinámicamente CodeMirror y proporciona análisis básico de código.

AvatarService: gestiona el canvas, las emociones y la síntesis de voz (Web Speech API).

TranscriptorService: maneja el reconocimiento de voz (Web Speech API) y el historial de transcripciones.

LoggerService: registra y exporta las acciones realizadas sobre archivos.

App: orquesta todos los componentes, las pestañas y las acciones del usuario.

¿Por qué necesito un servidor local?
La API de acceso al sistema de archivos exige un contexto seguro (https:// o http://localhost). Con python -m http.server creamos ese contexto de forma rápida.

⚠️ Limitaciones
Solo funciona en navegadores Chromium (Chrome, Edge, Opera…). En Firefox o Safari no se puede usar la parte de gestión de archivos.

Los permisos de carpeta no se guardan entre recargas de página; tendrás que volver a seleccionar la carpeta cada vez que entres.

Mover o copiar archivos muy grandes (>100 MB) puede ser lento (la API actual obliga a leerlos enteros en memoria).

El analizador de código es básico (reglas personalizadas). No sustituye a un linter profesional.

El avatar y el transcriptor requieren conexión a internet para cargar las voces (aunque luego funcionan sin ella).

Hecho con curiosidad, café y la firme convicción de que las herramientas deben ser libres, transparentes y divertidas.
