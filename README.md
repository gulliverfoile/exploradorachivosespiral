🌀 ORGANIZADOR ESPIRAL + CONTENEDOR DE JUEGOS
===============================================
v4.0 · PWA instalable · Abril 2025

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📌 ¿QUÉ ES?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Una aplicación web todo-en-uno que permite:
- Organizar archivos reales en tu disco duro/móvil 
  (mover, copiar, renombrar, eliminar, cambiar extensión).
- Ejecutar juegos HTML completos como si tuvieras un 
  servidor local, incluso offline.
- Usar comandos de voz para operaciones por lotes.
- Personalizar el menú contextual (geometría, botones).

No necesita instalación. Se abre en navegador Chrome/Edge,
y se puede instalar como PWA para usarla sin conexión.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 CÓMO SE USA
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. ABRE LA APLICACIÓN
   - En PC: arrastra el archivo .html a Chrome, o 
     usa un servidor local (python -m http.server 8000).
   - En móvil (Android): súbela a GitHub Pages y ábrela 
     en Chrome. Luego "Añadir a pantalla de inicio".

2. ORGANIZA TUS ARCHIVOS
   - Haz clic en "📁 Abrir carpeta" y selecciona una 
     carpeta de tu dispositivo.
   - Explora el árbol (panel derecho) y los archivos 
     (panel izquierdo).
   - Clic izquierdo en un archivo → aparece un menú 
     en abanico con acciones (mover, copiar, etc.).
   - Clic derecho o pulsación larga (móvil) también 
     abre el menú.
   - La geometría del menú (abanico, anillo, espiral, 
     columna) se cambia desde el panel de configuración ⚙️.

3. EJECUTA JUEGOS HTML
   - Ve a la pestaña "🎮 Juegos".
   - Pulsa "Cargar carpeta de juego" y selecciona la 
     carpeta que contiene tu juego (debe tener index.html).
   - El juego se guarda en la memoria local.
   - Pulsa "▶ Ejecutar" y el juego se cargará en un 
     iframe con todos sus archivos (CSS, JS, imágenes) 
     resueltos. ¡Sin errores de CORS!

   - Ya incluye un juego demo (Motor Pro) para probar.

4. USA COMANDOS DE VOZ O TEXTO
   - En el chat inferior escribe (o habla 🎤):
     • "mover *.pdf a Documentos"
     • "copiar foto_* a Fotos"
     • "renombrar .jpeg a .jpg"
     • "cambiar extension txt a html"
     • "eliminar *.tmp"

5. PERSONALIZA EL MENÚ
   - Pulsa el botón ⚙️.
   - Edita el JSON: cambia geometria, buttonSize, 
     acciones (puedes añadir/quitar botones).
   - Pulsa "Aplicar" y el menú se actualiza al instante.

6. MODO OSCURO
   - El botón 🌙 / ☀️ cambia el tema, y se recuerda 
     para la próxima visita.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚙️ CÓMO FUNCIONA INTERNAMENTE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
La aplicación está organizada en módulos separados 
que se comunican mediante un EventBus central:

🗂️ FileSystemService
   - Usa la File System Access API (solo Chrome/Edge)
     para leer/escribir/mover archivos reales.
   - Escanea carpetas recursivamente (hasta 3 niveles).
   - Todas las operaciones (mover, copiar, etc.) piden
     confirmación y reportan errores.

🧠 CommandParser
   - Interpreta comandos de texto como "mover *.pdf a X".
   - Convierte patrones (como *.pdf) en expresiones regulares.
   - Filtra archivos del árbol según esos patrones.

🌀 ContextMenuUI (el menú espiral)
   - Recibe un evento con la posición del icono.
   - Calcula la geometría seleccionada (abanico, anillo,
     espiral áurea, columna).
   - Escala automáticamente según el tamaño de pantalla.
   - Ajusta la posición si el menú se sale de los bordes.
   - Anima los botones desde el centro hacia afuera.

🌳 TreeViewUI (árbol de navegación)
   - Renderiza el árbol de carpetas/archivos.
   - Carga diferida: expande carpetas al hacer clic.
   - Emite eventos al seleccionar un nodo (para mostrar
     su contenido en el panel izquierdo).

📋 FileListUI (panel de resultados)
   - Muestra los archivos como tarjetas con iconos.
   - Según el modo de interacción (configurable), un clic
     puede abrir el menú o seleccionar el archivo.

🎮 GameLoader
   - Al cargar una carpeta de juego, lee todos los archivos
     (incluyendo subcarpetas) y los guarda como Blobs.
   - Para ejecutar un juego:
     1. Coge el index.html.
     2. Reemplaza todas las rutas relativas (src, href, 
        url() en CSS) por los Blobs correspondientes.
     3. Carga ese HTML modificado en un iframe.
   - El juego cree que está en un servidor, porque todos
     los recursos se cargan desde objetos en memoria 
     (data URIs/Blobs).

⚙️ DrawerUI (panel de configuración)
   - Carga y guarda la configuración en localStorage.
   - Al aplicar cambios, emite un evento global para que
     los demás componentes se actualicen.

🎤 VoiceInput
   - Usa la API SpeechRecognition (Chrome) para transcribir
     voz a texto y enviarlo al chat automáticamente.

💾 PersistenceService
   - Capa simple sobre localStorage para guardar:
     • Configuración del menú (geometría, botones).
     • Juegos guardados (lista de blobs).
     • Preferencia de tema (oscuro/claro).
     • Progreso (en el Motor Pro).

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ LIMITACIONES CONOCIDAS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
- La File System Access API solo funciona en Chrome,
  Edge y Opera (no en Firefox ni Safari). La parte de
  juegos sí funciona en cualquier navegador si los
  juegos se precargan manualmente.
- En móvil, File System Access solo está disponible
  en Android (Chrome). iOS no lo soporta aún.
- El contenedor de juegos reescribe rutas estáticas
  en el HTML, pero no intercepta peticiones fetch
  dinámicas ni XMLHttpRequest (juegos muy complejos
  podrían requerir un Service Worker adicional).
- No es un servidor real: no ejecuta PHP, Node.js,
  ni emula puertos TCP/UDP. Solo sirve archivos
  estáticos.
- Los juegos muy grandes (más de 50-100 MB) pueden
  consumir mucha memoria al guardarse como Blobs.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔮 FUTURAS MEJORAS POSIBLES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
- Service Worker para precargar juegos y que 
  funcionen completamente offline.
- Soporte para archivos ZIP (extraer automáticamente).
- Proxy de fetch para juegos más complejos.
- Sincronización con cuentas en la nube (opcional).
- Internacionalización.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
