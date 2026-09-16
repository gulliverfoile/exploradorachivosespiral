# 🌀 explorador

Un asistente modular de escritorio en **un solo archivo HTML**. Siete módulos independientes, un bus de eventos, arquitectura hexagonal. Sin backend, sin dependencias, sin build.

```
Un archivo · Siete módulos · Cero dependencias
```

---

## 📋 Tabla de contenidos

- [¿Qué es?](#-qué-es)
- [Las 7 pestañas](#-las-7-pestañas)
- [Cómo usarlo](#-cómo-usarlo)
- [Arquitectura](#-arquitectura)
- [Núcleo compartido](#-núcleo-compartido)
- [Dominio puro](#-dominio-puro)
- [Adaptadores](#-adaptadores)
- [Flujo de datos](#-flujo-de-datos)
- [Adaptador Enactivo](#-adaptador-enactivo)
- [Lo que NO es](#-lo-que-no-es)
- [Limitaciones por navegador](#-limitaciones-por-navegador)
- [Estructura del código](#-estructura-del-código)
- [Roadmap](#-roadmap)
- [Licencia](#-licencia)

---

## 🎯 ¿Qué es?

Un asistente modular que hace siete cosas distintas, todas comunicadas por eventos, todas siguiendo el mismo patrón hexagonal.

No es "un programa". Son **siete módulos en un mismo chasis**, como un coche con varios motores. Cada módulo (pestaña) puede vivir por su cuenta, pero todos comparten la misma fontanería: bus de eventos, persistencia, log y analizador de sentimiento.

### La metáfora

Es como una navaja suiza: cada herramienta es distinta, pero todas comparten el mismo mango, el mismo acero, el mismo mecanismo. Si un día quieres cambiar la hoja del juego por un destornillador (un clasificador de tickets, por ejemplo), solo cambias la hoja.

### Características técnicas

- **Un solo fichero HTML** — sin build, sin npm, sin servidor. Se abre y funciona.
- **Cero dependencias externas** — no carga ninguna librería de CDN. Todo es código propio.
- **Sin backend** — todo cliente. Usa `localStorage` para persistencia.
- **Módulos ES** — `<script type="module">` aísla el scope.
- **Arquitectura hexagonal** — dominio aislado, adaptadores en los bordes.
- **Bus de eventos** — ningún módulo llama directamente a otro.

---

## 🗂 Las 7 pestañas

| Pestaña | Qué hace | Requiere |
|---|---|---|
| 📁 **Organizador** | Explorador de ficheros + chat de comandos en lenguaje natural ("mover *.pdf a Documentos"). Menú contextual radial. | Chrome/Edge |
| 📝 **Texto** | Motor de tags → entidades → efectos. Detecta conceptos, genera entidades, activa sinergias. Piel de juego, motor genérico. | — |
| 🔬 **Lab** | Analizador de código con reglas JSON. Detecta `var`, `eval`, `console.log`, etc. Autofix básico. | — |
| 😸 **Avatar** | Cara en canvas que habla, con emociones interpoladas. Voz sintética del navegador. | — |
| 🎤 **Escuchar** | Transcriptor de voz con detección de emoción. Auto-restart tras pausas. | HTTPS/localhost |
| 🎵 **Audio** | Reproductor/sampler con física de atmósferas planetarias + grabación. Adaptador Enactivo. | — |
| 📋 **Log** | Registro de todo lo que pasa, con filtro por texto y colores por tipo de acción. | — |

### Detalle por pestaña

#### 📁 Organizador
- Abre carpetas del sistema con File System Access API.
- Árbol de ficheros navegable + lista de tarjetas.
- Menú contextual radial (anillo, abanico, espiral, columna) configurable desde JSON.
- Chat de comandos: `mover *.pdf a Documentos`, `renombrar X a Y`, `eliminar *.tmp`, etc.
- Entrada por voz para dictar comandos.

#### 📝 Texto
- Analiza texto libre y detecta tags vía reglas.
- Descubre tags no cubiertos por las reglas (candidatos).
- Expande tags con similares (diccionario + morfología + co-ocurrencia).
- Genera entidades ponderadas por tags coincidentes.
- Detecta sinergias (pares) y combos (cuentas mínimas).
- Resuelve efectos finales sumando entidades + sinergias + combos.
- Genera narrativa natural del resultado.

#### 🔬 Lab
- Analizador de código con reglas JSON editables.
- Detecta: `var`, `==`, `console.*`, `eval`, `TODO/FIXME`.
- Autofix: convierte `var → let`, quita logs, renombra símbolos.
- Carga reglas personalizadas desde JSON.
- Guarda en el fichero original o descarga.

#### 😸 Avatar
- Canvas circular con cara dibujada por código.
- Interpolación real entre emociones (positivo, negativo, neutro, sorpresa, enfado).
- Detección automática de emoción desde el texto.
- Voz sintética con `SpeechSynthesis`.
- Modo narración frase a frase.

#### 🎤 Escuchar
- Transcriptor continuo con `SpeechRecognition`.
- Detección de emoción en cada frase final.
- Auto-restart tras pausas de Chrome.
- Historial persistente.
- Diagnóstico de entorno (file://, sin HTTPS, sin soporte).

#### 🎵 Audio
- Carga cualquier audio local.
- Selección de fragmento arrastrando sobre la forma de onda.
- Sampler de 8 notas (Do4 a Do5) que aplican pitch y filtro.
- Física de atmósferas: Tierra, Marte, Venus, Titán.
- Minimapa con fuente arrastrable y oyente fijo.
- Grabación de capas con `MediaRecorder`.
- Adaptador Enactivo: compensa automáticamente cuando el volumen cae bajo umbral.

#### 📋 Log
- Registro centralizado de todas las acciones.
- Filtro por texto.
- Colores por tipo de acción.
- Exportable a `.txt`.

---

## 🚀 Cómo usarlo

### Requisitos

- Navegador moderno (Chrome o Edge para funcionalidad completa).
- Servidor local o HTTPS para voz (`SpeechRecognition`).
- Para el Organizador: Chrome/Edge (File System Access API).

### Ejecución

**Opción 1 — Abrir directamente** (funcionalidad limitada):

```bash
# Doble clic sobre el archivo, o:
open asistente-total.html
```

**Opción 2 — Servidor local** (recomendado, voz funcional):

```bash
# Python 3
python -m http.server 8000

# Node
npx serve

# Luego abre:
# http://localhost:8000/asistente-total.html
```

### Primer uso

1. Abre el archivo en Chrome/Edge.
2. Pestaña **📁 Organizador** → botón "Abrir carpeta" → elige una carpeta.
3. Pestaña **📝 Texto** → botón "Demo" → "Ejecutar".
4. Pestaña **🔬 Lab** → botón "Analizar".
5. Pestaña **😸 Avatar** → escribe texto → "Hablar".
6. Pestaña **🎵 Audio** → carga un mp3 → toca las notas.

---

## 🏗 Arquitectura

El sistema sigue el patrón **hexagonal** (puertos y adaptadores). El dominio está aislado en el centro; la infraestructura vive en los bordes. La comunicación entre capas se hace por un bus de eventos, no por llamadas directas.

```
╔══════════════════════════════════════════════════════════════════╗
║                        INFRAESTRUCTURA                           ║
║  FileSystemService · WebAudioEngine · MediaRecorderAdapter        ║
║  CanvasWaveformRenderer · AnalyserVisualizer · MinimapController  ║
║                                                                   ║
║  ╔════════════════════════════════════════════════════════════╗  ║
║  ║                       APLICACIÓN                            ║  ║
║  ║  App · LabUI · TextGameEngine · AvatarUI · TranscriptorUI   ║  ║
║  ║  AudioUI · LogUI · ContextMenuUI · TreeViewUI · FileListUI  ║  ║
║  ║                                                              ║  ║
║  ║  ╔══════════════════════════════════════════════════════╗   ║  ║
║  ║  ║                    DOMINIO                            ║   ║  ║
║  ║  ║  FilterDomain · TagDiscovery · TagRegistry            ║   ║  ║
║  ║  ║  Generator · SynergyEngine · Resolver                 ║   ║  ║
║  ║  ║  Atmosphere · SoundPropagator                         ║   ║  ║
║  ║  ║                                                        ║   ║  ║
║  ║  ║  (lógica pura — no toca DOM, red ni localStorage)     ║   ║  ║
║  ║  ╚══════════════════════════════════════════════════════╝   ║  ║
║  ╚════════════════════════════════════════════════════════════╝  ║
╚══════════════════════════════════════════════════════════════════╝

                    ┌─────────────────────┐
                    │     EventBus        │ ← mediador global
                    └─────────────────────┘
                             ↕
        Todos los módulos se comunican aquí, nunca directamente.
```

### Reglas de la arquitectura

1. **El dominio no conoce el exterior.** `FilterDomain` no sabe qué es un canvas ni un fichero. Solo procesa strings.
2. **La UI no llama al dominio directamente.** Pasa por el bus de eventos.
3. **Los adaptadores traducen.** `FileSystemService` convierte la File System Access API en métodos simples (`move`, `copy`, `delete`).
4. **Un servicio = una responsabilidad.** `SentimentAnalyzer` es único; no hay dos versiones.

---

## 🧠 Núcleo compartido

Cuatro servicios que todos los módulos usan. Ninguno tiene estado propio más allá del necesario.

| Servicio | Responsabilidad | API |
|---|---|---|
| **EventBus** | Mediador global. Los módulos publican eventos y se suscriben a ellos sin conocerse. | `on(event, cb) → unsubscribe` · `emit(event, payload)` |
| **PersistenceService** | Envoltorio de `localStorage` con JSON automático y manejo de errores. | `load(key, fallback)` · `save(key, value)` · `remove(key)` |
| **LoggerService** | Registro centralizado. Emite `log:updated` para que el panel de Log se refresque en vivo. | `log(action, details)` · `exportText()` |
| **SentimentAnalyzer** | Analiza texto y devuelve `positivo`, `negativo`, `sorpresa`, `enfado` o `neutro`. Compartido por Avatar y Transcriptor (DRY). | `analyze(text) → string` |

> **Nota:** antes había dos analizadores de sentimiento (uno con 4 palabras, otro con `return 'neutro'`). Ahora hay uno solo, más completo, usado por ambos módulos.

---

## 🎯 Dominio puro

Clases que **no tocan el DOM, ni la red, ni localStorage**. Podrían extraerse del archivo y ejecutarse en Node sin cambiar una línea.

### Motor de filtrado (compartido por Lab y Texto)

| Clase | Responsabilidad |
|---|---|
| **FilterDomain** | Toma texto + reglas + configuración, y devuelve coincidencias agrupadas por categoría, acción global y severidad máxima. Las reglas son JSON puro. |

### Motor de tags (usado por Texto)

| Clase | Responsabilidad |
|---|---|
| **TagRegistry** | Registro de tags con metadatos (nombre, color, efectos). |
| **TagDiscovery** | Encuentra tags en texto y propone similares. Tres modos: directo (reglas), candidatos (tokens no cubiertos), expansión (similares por diccionario o morfología). |
| **Generator** | Selecciona entidades del catálogo con peso proporcional a cuántos tags coinciden. |
| **SynergyEngine** | Detecta sinergias (pares de tags) y combos (cuentas mínimas de tags) activos entre las entidades generadas. |
| **Resolver** | Suma los efectos de entidades + sinergias + combos en un objeto final. |

### Motor de audio (usado por Audio)

| Clase | Responsabilidad |
|---|---|
| **Atmosphere** | Entidad que modela una atmósfera planetaria (presión, temperatura, masa molar, índice adiabático). Calcula velocidad del sonido, densidad y coeficiente de absorción por frecuencia. |
| **SoundPropagator** | Calcula cómo se atenúa y distorsiona un sonido entre una fuente y un oyente en la atmósfera actual. |

> **Ventaja de tener el dominio aislado:** puedes testear `FilterDomain.filter()` con un array de reglas y un string. No necesitas navegador. Puedes portar `Atmosphere.soundSpeed` a una calculadora científica. El dominio no depende de nada.

---

## 🔌 Adaptadores

Clases que **sí** tocan el mundo: DOM, canvas, Web Audio API, sistema de ficheros. Traducen APIs del navegador en métodos simples que el resto del sistema entiende.

| Adaptador | API que envuelve | Usado por |
|---|---|---|
| `FileSystemService` | File System Access API | Organizador, Lab |
| `WebAudioEngine` | Web Audio API | Audio |
| `MediaRecorderAdapter` | MediaRecorder API | Audio |
| `CanvasWaveformRenderer` | Canvas 2D | Audio |
| `AnalyserVisualizer` | AnalyserNode + Canvas | Audio |
| `MinimapController` | DOM + eventos de puntero | Audio |
| `ContextMenuUI` | DOM + geometría | Organizador |
| `VoiceInput`, `TranscriptorUI` | SpeechRecognition API | Organizador, Escuchar |
| `AvatarUI` | Canvas + SpeechSynthesis | Avatar |

---

## 🔄 Flujo de datos

Cómo viaja la información desde que el usuario hace algo hasta que se ejecuta la acción.

```
  Usuario
     │
     │ click / tecla / voz
     ▼
┌──────────────┐
│  UI (pestaña)│  ← el componente que ve el usuario
└──────┬───────┘
       │ emit('evento', payload)
       ▼
┌──────────────┐
│   EventBus   │  ← mediador global
└──────┬───────┘
       │ los suscritos reciben el evento
       ▼
┌──────────────┐
│  Módulo      │  ← LabUI, TextGameEngine, AudioUI...
└──────┬───────┘
       │ llama al dominio
       ▼
┌──────────────┐
│   Dominio    │  ← FilterDomain, Generator, Atmosphere...
└──────┬───────┘
       │ devuelve resultado
       ▼
┌──────────────┐
│  Adaptador   │  ← FileSystemService, WebAudioEngine...
└──────┬───────┘
       │ toca hardware / APIs del navegador
       ▼
  Sistema / Hardware
```

### Ejemplo concreto: pulsar "Analizar" en el Lab

1. El usuario pulsa **🔍 Analizar** → `LabUI.#analyze()`.
2. El Lab lee el código del textarea y llama a `FilterDomain.filter(code, rules, config)`.
3. El dominio recorre las reglas, aplica regex y devuelve coincidencias.
4. El Lab pinta los problemas en el panel y llama a `logger.log('LAB_ANALIZAR', ...)`.
5. El Logger emite `log:updated` por el bus.
6. El `LogUI` escucha ese evento y refresca el panel de Log.

**Nadie llamó a nadie directamente. Todo pasó por el bus.**

---

## 📌 Adaptador Enactivo

Un patrón que aparece en el módulo de Audio y que se puede aplicar en cualquier sitio.

> **Definición:** cuando un parámetro cae por debajo de un umbral de utilidad, el sistema **decide activamente compensar** en vez de dejar el resultado inútil.

### Cómo funciona en Audio

Al tocar una nota en Marte, la atenuación por distancia y densidad puede hacer que el sonido sea inaudible. En lugar de dejarlo así:

1. Se comprueba si `volumeFactor < 0.01` (umbral de audibilidad).
2. Si es así, se multiplica por una **ganancia de emergencia** configurable por el usuario (×1 a ×1000).
3. Se limita el resultado a un máximo de `1.5` para no saturar.
4. Se marca el parámetro con `degraded = true` y se muestra un aviso.

```js
// Extracto de AudioUI.#playNote()
if (adapted.volumeFactor < THRESH) {
  const boost = Math.min(this.#emergencyGain * 100, 150);
  adapted.volumeFactor = Math.min(adapted.volumeFactor * boost, 1.5);
  warning = `Volumen bajo: compensación ×${boost.toFixed(1)}`;
}
```

### Dónde más se podría aplicar

- **Avatar:** si el analizador no detecta emoción clara → forzar neutro con aviso.
- **Transcriptor:** si el reconocimiento no entiende → pedir repetir.
- **Lab:** si un autofix no mejora el código → dejarlo intacto y avisar.
- **Organizador:** si un comando afecta a demasiados ficheros → pedir confirmación reforzada.

Es un patrón **reutilizable**: cualquier módulo que reciba un input con umbral de utilidad puede usarlo.

---

## ❌ Lo que NO es

Para evitar expectativas equivocadas, esto es lo que **no** tienes:

| No es | Por qué |
|---|---|
| ❌ Un modelo de IA | No hay redes neuronales, no hay gradientes, no hay entrenamiento. Solo reglas y canvas. |
| ❌ Un LLM local | No ejecuta ningún transformer. No hay pesos. No hay tokenizador. |
| ❌ Un backend | Todo es cliente. No hay servidor, no hay API remota, no hay base de datos. |
| ❌ Una app de escritorio nativa | Es un HTML. Se ejecuta en el navegador. No hay binarios, no hay instalación. |
| ❌ Un producto | Es un experimento modular. Cada pieza funciona, pero no está optimizado para producción. |

### Sobre la analogía con Huawei/Nvidia

La arquitectura se parece a la de un "AI-native OS" porque ambos usan el mismo patrón (hexagonal + bus de eventos + adaptadores). Pero Huawei mete debajo modelos reales (Pangu) y hardware propio (Ascend, Kirin). Este proyecto mete reglas escritas y un canvas. La **forma** es la misma; la **carne** es distinta.

---

## ⚠️ Limitaciones por navegador

| Funcionalidad | Chrome/Edge | Firefox | Safari |
|---|---|---|---|
| Organizador (File System Access) | ✅ | ❌ | ❌ |
| SpeechRecognition (Escuchar, dictado) | ✅ | ❌ | ⚠️ |
| SpeechSynthesis (Avatar) | ✅ | ✅ | ✅ |
| Web Audio API (Audio) | ✅ | ✅ | ✅ |
| MediaRecorder (grabación) | ✅ | ✅ | ⚠️ |
| localStorage (persistencia) | ✅ | ✅ | ✅ |

### Notas importantes

- **`file://` bloquea SpeechRecognition.** Para usar voz necesitas servir el archivo por HTTPS o `localhost`.
- **Firefox no soporta File System Access API.** El Organizador no funcionará.
- **Safari tiene soporte parcial** de varias APIs modernas.

---

## 📁 Estructura del código

El HTML tiene este orden lógico:

```
1. <style>              — CSS completo con variables, paneles, componentes
2. HTML                  — topbar, tabs, paneles, drawer, overlay
3. <script type="module">
   │
   ├── NÚCLEO COMPARTIDO
   │   ├── EventBus
   │   ├── PersistenceService
   │   ├── LoggerService
   │   └── SentimentAnalyzer
   │
   ├── DOMINIO PURO
   │   ├── FilterDomain
   │   ├── TagDiscovery
   │   ├── TagRegistry
   │   ├── Generator
   │   ├── SynergyEngine
   │   ├── Resolver
   │   ├── Atmosphere
   │   └── SoundPropagator
   │
   ├── INFRAESTRUCTURA
   │   ├── FileSystemService
   │   ├── CommandParser
   │   ├── GeometryEngine
   │   ├── WebAudioEngine
   │   ├── MediaRecorderAdapter
   │   ├── CanvasWaveformRenderer
   │   ├── AnalyserVisualizer
   │   ├── MinimapController
   │   └── AtmosphereRepository
   │
   ├── UI (por pestaña)
   │   ├── Notifications
   │   ├── ContextMenuUI
   │   ├── TreeViewUI
   │   ├── FileListUI
   │   ├── VoiceInput
   │   ├── DrawerUI
   │   ├── LabUI
   │   ├── TextGameEngine + TextGameUI
   │   ├── AvatarUI
   │   ├── TranscriptorUI
   │   ├── AudioUI
   │   └── LogUI
   │
   └── APP (orquestador raíz)
       └── App
```

---

## 🛣 Roadmap

Ideas para futuras iteraciones (no implementadas):

- [ ] **Capa de persistencia con IndexedDB** — reemplazar `localStorage` por stores tipadas.
- [ ] **Retrieval para el motor de Texto** — búsqueda por similitud sobre corpus persistente.
- [ ] **Feedback loop** — botón "esto estuvo bien / mal" que ajusta pesos.
- [ ] **Versionado de reglas** — cada run guarda la versión que usó.
- [ ] **README interactivo** — versión HTML de esta documentación con navegación.
- [ ] **Exportación de config completa** — un solo JSON con reglas, catálogo, sinergias, combos.
- [ ] **Tema claro/oscuro por módulo** — independiente por pestaña.
- [ ] **Internacionalización** — español, inglés, francés.
- [ ] **Tests del dominio** — como el dominio es puro, se puede testear en Node.

---

## 📄 Licencia

Sin licencia definida. Uso libre mientras se mantenga la autoría.

Si lo usas como base para algo, agradecería una mención.

---

## 🙏 Créditos

Construido a partir de conversaciones y experimentos sobre arquitecturas modulares, patrones hexagonales y sistemas reactivos por eventos.

Inspiraciones directas:
- Patrón hexagonal (Alistair Cockburn)
- Event-driven architecture
- File System Access API
- Web Audio API
- SpeechRecognition / SpeechSynthesis

---

**Fin del README.**
