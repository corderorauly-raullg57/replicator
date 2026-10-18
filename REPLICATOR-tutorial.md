# REPLICATOR · Tutorial completo

**Motor de ingeniería de guiones virales.** Desmonta un video que funciona, mide su ritmo y su estructura, y te entrega un guion nuevo con tu idea y el mismo ADN.

---

## Índice

1. [Qué hace REPLICATOR](#1--qué-hace-replicator)
2. [Antes de empezar](#2--antes-de-empezar)
3. [Configuración inicial (lo más importante)](#3--configuración-inicial-lo-más-importante)
4. [Cómo está organizada la app](#4--cómo-está-organizada-la-app)
5. [Pantalla ORIGEN: cargar el video o el enlace](#5--pantalla-origen-cargar-el-video-o-el-enlace)
6. [Pantalla ANÁLISIS: entender por qué funciona](#6--pantalla-análisis-entender-por-qué-funciona)
7. [Pantalla RÉPLICA: tu guion nuevo](#7--pantalla-réplica-tu-guion-nuevo)
8. [Empaque, Métricas, Biblioteca y Exportar](#8--empaque-métricas-biblioteca-y-exportar)
9. [Recetas: el mejor camino según lo que tengas](#9--recetas-el-mejor-camino-según-lo-que-tengas)
10. [Cómo leer los resultados](#10--cómo-leer-los-resultados)
11. [Consejos para obtener los mejores resultados](#11--consejos-para-obtener-los-mejores-resultados)
12. [Solución de problemas](#12--solución-de-problemas)
13. [Atajos de teclado y glosario](#13--atajos-de-teclado-y-glosario)

---

## 1 · Qué hace REPLICATOR

La idea de la app en una frase: **un video viral no funciona por suerte, funciona por una estructura que se puede medir y repetir.**

REPLICATOR hace tres cosas:

| Paso | Qué hace | Resultado |
|---|---|---|
| **1. Obtener** | Lee el video (archivo o enlace) y saca todo lo que puede: audio, imagen, texto, título, métricas, comentarios. | Los datos en bruto del original. |
| **2. Analizar** | Mide pausas, cortes de cámara, velocidad de habla y movimiento. Detecta el gancho, 18 disparadores psicológicos y la función de cada bloque. Reconstruye el **guion del original** (literal o pre-guion). | El "ADN" del video: qué dice, cuándo lo dice y por qué retiene. |
| **3. Replicar** | Toma esa estructura y la rellena con **tu idea**, conservando los tiempos, las pausas, los cortes y la función de cada parte. | Un guion listo para grabar, con dirección de cámara, texto en pantalla, ganchos A/B, títulos y hashtags. |

> **Importante:** se replica la **estructura**, no el contenido. El ritmo, el tipo de gancho y el orden de los bloques no tienen derechos de autor. El texto, la imagen y la música del original sí. Graba siempre con tu voz, tu producto y tus pruebas.

---

## 2 · Antes de empezar

### Qué necesitas

- **Una computadora con Google Chrome o Microsoft Edge actualizados.** En el móvil la app abre, pero algunas funciones (captura de pestaña y carpetas de modelos) solo van en PC.
- **Internet la primera vez**, para cargar el motor de transcripción (unos 20 MB) y, si no los tienes, los modelos. Después, casi todo funciona sin conexión.
- El archivo **`replicator.html`**.

### Cómo abrir la app

- **Opción simple:** doble clic en `replicator.html`. Se abre en el navegador.
- **Opción recomendada:** subirla a un hosting (por ejemplo Netlify o GitHub Pages) y abrirla desde su dirección web. Así el navegador guarda mejor la configuración, los modelos y la biblioteca.

> Todo se procesa **en tu equipo**: los videos que subes **no se envían a ningún servidor**. Solo salen a internet las consultas a la IA y a YouTube que tú configures.

---

## 3 · Configuración inicial (lo más importante)

La primera vez que abres la app aparece el asistente **⚙ Configuración**, con 4 pasos. Para volver a él cuando quieras:

- botón **⚙ Configuración** (arriba a la derecha), o
- un clic en la **barra de estado** junto a él, que muestra algo como `🎙 whisper-base · local · ✦ Gemini · ▶ YT`.

> **Regla de oro:** en cada paso hay un botón **🧪 Probar**. No des nada por bueno hasta ver el ✓ verde. Si algo falla, la app te dice el motivo exacto.

---

### Paso 1 · Transcripción (convertir la voz del video en texto)

Para esto la app usa **Whisper**, un reconocedor de voz que funciona dentro del navegador y da **tiempos exactos** de cada frase.

Tienes tres opciones:

#### Opción A · "Ya los tengo en la PC" 📁

1. Pulsa **Elegir carpeta** y selecciona la carpeta donde guardas los modelos. Puede ser la carpeta general: la app busca dentro.
2. La app te muestra una tabla con:
   - **Modelos compatibles encontrados**: nombre, precisión (q8, fp16…), tamaño y ubicación.
   - **Modelos que hay pero no sirven en el navegador**, por ejemplo archivos `.pt` de Whisper para Python o `ggml-*.bin` de whisper.cpp.
3. Marca uno y pulsa **✔ Usar el modelo marcado**.
4. Pulsa **🧪 Probar transcripción**.

La carpeta **se recuerda**. Como mucho, el navegador te pedirá "Permitir" una vez por sesión.

**Formato que sirve en el navegador (ONNX).** La carpeta del modelo debe contener:

```
config.json
tokenizer.json
preprocessor_config.json
onnx/encoder_model_quantized.onnx
onnx/decoder_model_merged_quantized.onnx
```

(Es el formato de los modelos de `huggingface.co/Xenova/whisper-…`.) Si tus modelos son de otro tipo, usa la opción B: la app puede descargar la versión compatible **en esa misma carpeta**.

#### Opción B · "Descargarlos" ⬇

1. Elige el modelo:

   | Modelo | Tamaño | Para qué |
   |---|---|---|
   | **Tiny** | ~40 MB | PC con poca memoria o internet muy limitado. Menos preciso. |
   | **Base** | ~80 MB | **Recomendado.** Buen equilibrio. |
   | **Small** | ~250 MB | El más preciso. Necesita un PC con más memoria. |

2. Elige dónde guardarlo:
   - **Guardar en una carpeta**: queda en tu disco, como cualquier archivo.
   - **Guardar en el navegador**: queda dentro de Chrome o Edge.
3. Pulsa **🧪 Probar transcripción**. Ahí se descarga **una sola vez**. A partir de entonces la app lo usa sin internet.

#### Opción C · "Sin transcripción" ✋

Pegarás el guion o subirás un `.srt`. El análisis de pausas, cortes e imagen sigue funcionando. Y si tienes IA configurada, la app puede **reconstruir el guion** igualmente (ver paso 2).

#### Idioma de los videos

Elige **Español**, **Inglés**, **Portugués** o **Detectar automáticamente**. Si sabes el idioma, indícalo: Whisper acierta más.

---

### Paso 2 · Inteligencia artificial

La IA es la que **reconstruye el guion del original** cuando no hay transcripción, **escribe tu guion réplica** a partir de tu idea, y amplía el análisis, los títulos y los hashtags.

> Sin IA la app funciona, pero pierdes lo más valioso: el pre-guion y la réplica escrita a tu medida. **Configúrala.**

#### Qué IA elegir

| Proveedor | Coste | Internet | Ve imágenes | Cuándo elegirlo |
|---|---|---|---|---|
| **Google Gemini** | Gratis (con límite diario) | Sí | **Sí** | **La mejor opción general.** Analiza también los fotogramas del video. |
| **Groq** | Gratis (con límite) | Sí | Según modelo | Muy rápido. Buen texto con `llama-3.3-70b-versatile`. |
| **OpenRouter** | Modelos `:free` gratis | Sí | Según modelo | Muchos modelos para elegir. |
| **Ollama** | Gratis | **No** (una vez instalado) | Con `llava` o `qwen2.5-vl` | Si quieres que todo quede en tu PC. Necesita un PC potente. |
| **LM Studio** | Gratis | **No** | Según modelo | Como Ollama, pero con ventana gráfica. |
| **Otro compatible OpenAI** | Según servicio | Sí | Según modelo | DeepSeek, Mistral o un servidor propio. |
| **Sin IA** | — | — | — | Solo motor local. |

#### Cómo configurarla

1. Toca la tarjeta del proveedor. La **Dirección (Base URL)** y un **Modelo** se rellenan solos.
2. Si es un servicio en la nube, pega tu **Clave API**.
3. Pulsa **🔎** para ver los modelos disponibles y elige uno.
4. Elige el **Tono** de los textos: directo, cercano, autoridad, provocador o educativo.
5. Pulsa **🧪 Probar conexión** y espera el "Conexión correcta ✓".

#### Cómo conseguir las claves gratis

- **Gemini:** entra en `aistudio.google.com/apikey` con tu Gmail → **Create API key** → copia la clave.
- **Groq:** entra en `console.groq.com/keys` → **Create API Key**.
- **OpenRouter:** entra en `openrouter.ai/keys` → **Create Key**. Usa modelos cuyo nombre termine en `:free`.

#### Si usas Ollama o LM Studio (en tu PC)

- **Ollama:**
  1. Instálalo y descarga un modelo: `ollama pull qwen2.5:7b-instruct` (o `qwen2.5vl` si quieres que vea imágenes).
  2. Si la prueba dice "No se pudo conectar", cierra Ollama y ábrelo con la variable `OLLAMA_ORIGINS=*`. Eso permite que la página se conecte.
- **LM Studio:** ve a **Developer → Start Server** y activa **CORS**.

> **Si vives en Cuba u otro país con servicios restringidos:** algunos servicios en la nube pueden no responder desde tu conexión. Las soluciones son usar una VPN, o usar **Ollama o LM Studio**, que funcionan sin internet.

---

### Paso 3 · YouTube API (opcional, muy recomendado para YouTube)

Con la **clave oficial y gratuita de YouTube**, la app obtiene de cualquier video:

- vistas, likes y comentarios **exactos**
- fecha, duración, categoría e idioma
- las **etiquetas ocultas** del video
- los suscriptores del canal y la proporción **vistas / suscriptores** (detector de virales)
- los **25 comentarios más relevantes**, de donde salen ideas para nuevos videos

El cupo es de 10.000 unidades al día y cada análisis gasta unas 3: unos **3.000 videos al día**.

#### Cómo conseguir la clave (5 minutos)

La app tiene esta misma guía con botones que abren cada página:

1. Entra en **Google Cloud** (`console.cloud.google.com`) con tu Gmail. Acepta las condiciones. **No pide tarjeta.**
2. **Crea un proyecto:** selector de proyectos (arriba a la izquierda) → **Proyecto nuevo** → nombre `Replicator` → **Crear**. Comprueba que quede seleccionado.
3. **Habilita la API:** en la biblioteca de APIs busca **YouTube Data API v3** → **Habilitar**.
4. **Crea la clave:** **APIs y servicios → Credenciales → + Crear credenciales → Clave de API**. Copia la clave (empieza por `AIza…`).
5. **Protégela:** en la clave → **Restricciones de API** → solo **YouTube Data API v3**. En **Restricciones de aplicación** deja **Ninguna**.
6. Pégala en la app y pulsa **🧪 Probar clave**.

**Errores típicos al probar la clave:**

| Mensaje | Qué hacer |
|---|---|
| "Falta habilitar YouTube Data API v3" | Haz el punto 3 y espera 1–2 minutos. |
| "La clave no es válida" | Cópiala de nuevo completa. |
| "Restricción de sitios web o de IP" | Pon **Ninguna** en Restricciones de aplicación. |
| "Se agotó el cupo" | Se renueva cada día, hacia las 3:00 am hora de Cuba. |
| "No hay conexión / ubicación" | Usa una VPN, o que alguien de confianza fuera del país cree la clave y te la envíe. |

> La clave solo lee datos **públicos** de YouTube y se guarda solo en tu navegador. No la publiques.

---

### Paso 4 · Listo

Resumen de lo configurado: ✓ verde lo probado, ⚠ lo que falta probar. Pulsa **✔ Empezar a usar REPLICATOR**.

---

## 4 · Cómo está organizada la app

```
┌──────────────────────────────────────────────────────────────────────┐
│ REPLICATOR   [1 Origen][2 Análisis][3 Réplica]…   estado  ⚙  ⬇Exportar│  ← barra superior
├──────┬───────────────────────────────────────────────┬───────────────┤
│Origen│                                               │ Índice Viral  │
│Análi.│          PANTALLA PRINCIPAL                   │ ADN temporal  │
│Répli.│                                               │ Disparadores  │
│Empaq.│                                               │ Exportar      │
│Métr. │                                               │               │
│Biblio│                                               │               │
│Ayuda │                                               │               │
└──────┴───────────────────────────────────────────────┴───────────────┘
 menú lateral                                            panel lateral
```

- **Pasos (arriba):** se marcan con ✓ a medida que completas cada etapa. Puedes tocarlos para saltar.
- **Barra de estado:** muestra qué transcripción, qué IA y si hay clave de YouTube. Tócala para configurar.
- **Panel lateral derecho:** siempre visible (en pantallas grandes):
  - **Índice Viral**: nota de 0 a 100 y sus 5 componentes.
  - **ADN temporal**: la barra de colores de los bloques del guion.
  - **Disparadores detectados**: las técnicas psicológicas encontradas.
  - **Exportar**: todos los formatos.
- **Ayuda:** resumen rápido dentro de la app.

---

## 5 · Pantalla ORIGEN: cargar el video o el enlace

Aquí empieza todo. Tiene cuatro bloques.

### 5.1 · Materia prima (pestañas)

| Pestaña | Para qué sirve |
|---|---|
| **📹 Analizar video** | **La mejor opción.** Al elegir el archivo, **el análisis completo empieza solo**: audio, imagen, transcripción y análisis forense. |
| **📝 Pegar guion** | Pegar una transcripción. Admite texto normal, líneas con tiempo (`0:05 texto`) o un SRT/VTT completo. |
| **📄 Subir .srt/.vtt** | Subtítulos con tiempos reales. La réplica hereda el ritmo exacto. |
| **⌨ Comandos** | Comandos de `yt-dlp` y Whisper para usuarios avanzados. |

**Qué mide el análisis de video (todo en tu equipo):**

1. **Audio:** pausas y silencios reales, porcentaje del tiempo con voz y dinámica de volumen.
2. **Imagen:** cortes de cámara fotograma a fotograma, duración de cada plano, movimiento, brillo del primer fotograma y storyboard automático.
3. **Transcripción:** con el método configurado (Whisper, micrófono o ninguno).
4. **Análisis forense:** bloques, disparadores, curva de retención e índice viral.

Cada paso muestra su barra de progreso. Si uno falla, los demás siguen.

> **Modo micrófono:** reproduce el video por los altavoces y lo "escucha". Es una alternativa si Whisper no está disponible. Sube el volumen y no hables mientras tanto.

### 5.2 · Analizar desde un enlace

Pega el enlace (YouTube, TikTok, Facebook o Instagram) y pulsa **🔗 Analizar enlace**. La app saca todo lo que la plataforma permite:

| Plataforma | Qué se obtiene automáticamente |
|---|---|
| **YouTube** con clave API | Datos oficiales completos (métricas, etiquetas, canal, comentarios). Además intenta los **subtítulos** y el **video** para el análisis completo. |
| **YouTube** sin clave | Título, autor, métricas aproximadas y, si los servidores públicos responden, subtítulos y video. |
| **TikTok** | Título, autor y el texto de la publicación con sus hashtags. |
| **Facebook / Instagram** | Lo poco que den (a veces título y autor). |

Debajo verás una lista con ✓ (obtenido) o ! (no disponible) para cada dato.

> **TikTok, Facebook e Instagram no permiten que una web baje sus videos.** No es un fallo de la app. Para el análisis completo usa una de las soluciones de la sección 5.3.

**Botones de este bloque:**

- **✍ Todo a mano**: abre el formulario de datos sin necesidad de enlace.
- **Limpiar todo**: borra el análisis actual para empezar de cero.

### 5.3 · Diagnóstico y soluciones

Cuando algo no se puede obtener, aparece un recuadro naranja con:

- **qué pasó y por qué**
- **pasos concretos para resolverlo**, con comandos listos para **copiar**
- **botones** que te llevan directamente a la solución

Las soluciones más útiles:

| Solución | Cuándo usarla | Cómo funciona |
|---|---|---|
| **🎥 Capturar pestaña** | TikTok, Facebook o Instagram en PC con Chrome o Edge | 1) Abre el video en otra pestaña (mejor a pantalla completa). 2) Pulsa **Empezar captura**, elige **"Pestaña de Chrome"** y marca **"Compartir también el audio de la pestaña"**. 3) Reprodúcelo entero. 4) Pulsa **Detener**. La app analiza la grabación como si hubieras subido el video: **cortes y pausas reales**. |
| **📹 Subir video** | Si puedes guardar el video | TikTok: **Compartir → Guardar video**. O graba la pantalla del móvil **con audio multimedia** y sube la grabación. |
| **⏱ Marcar a mano** | Cuando no hay forma de tener el video | Ver abajo. |
| **📝 Pegar transcripción** | YouTube | En el video: **…más → Mostrar transcripción** → copia todo y pégalo. Los tiempos se conservan. |
| **✦ Reconstruir con IA** | Siempre que falte el guion | La IA crea el pre-guion (sección 6.1). |

### 5.4 · Datos del análisis (formulario guiado)

Aparece al analizar un enlace o con **✍ Todo a mano**. Tiene dos partes.

**1. Tabla de calidad.** Muestra qué datos tienes y cuáles faltan, con una nota de **calidad** (básico, bueno o completo). Cuanto más completa, mejor el análisis.

**2. Campos para completar a mano:**

- **Título, autor, duración y formato** (vertical u horizontal).
- **Cortes de cámara**: momentos separados por espacios, por ejemplo `0:02.1 0:04.5 0:07`.
- **Pausas / silencios**: tramos desde-hasta, por ejemplo `0:08-0:08.6 0:15-0:16.2`.
- **Descripción del post** (con hashtags).
- **Primer fotograma**: sube una captura de pantalla; la app mide su brillo y contraste.
- **Métricas**: vistas, likes, comentarios y compartidos. Acepta `1.2M`, `35K`, `12.500`.

Al terminar pulsa **✔ Analizar con estos datos**.

#### ⏱ Marcar en vivo (cortes y pausas)

Herramienta para medir el ritmo **mirando el video**:

1. Pulsa **⏱ Marcarlos en vivo mientras lo veo**.
2. Si el video está en la app, el tiempo se toma del propio video. Si no, pulsa **▶ Empezar cronómetro** a la vez que das play.
3. Marca:
   - **✂ CORTE** (o tecla **C** / **espacio**) en cada cambio de plano.
   - **⏸ PAUSA** (o tecla **P**): **mantenla pulsada** mientras dure el silencio.
4. Pulsa **■ Fin del video** al terminar y luego **✔ Guardar marcas**.

> **Truco:** míralo una vez entero para entenderlo, y márcalo en la segunda pasada.

### 5.5 · Objetivo de tu video

| Campo | Para qué sirve |
|---|---|
| **Plataforma destino** | Ajusta hashtags y recomendaciones (TikTok, Shorts, Reels, Facebook, YouTube largo). |
| **Duración objetivo (s)** | Duración de tu réplica. Toma automáticamente la del original; cámbiala si quieres otra. |
| **Tu ritmo (palabras/min)** | Tu velocidad al hablar. Sirve para calcular cuántas palabras caben en cada bloque. Lo normal es 150–170. |

---

## 6 · Pantalla ANÁLISIS: entender por qué funciona

Arriba tienes tres botones:

- **⚡ Analizar (motor local)**: vuelve a analizar con los datos actuales.
- **✦ Ampliar con IA**: la IA reescribe propósito, técnica, acción visual y sonido de cada bloque, y propone títulos y hashtags.
- **＋ Notas visuales**: escribes lo que ves en el original (`0:04 corte a producto en mano`) y se fusiona con los bloques.

### 6.1 · 🎬 Guion del original (la pieza clave)

Es la base de todo. Puede ser de tres tipos:

| Tipo | De dónde sale | Fiabilidad |
|---|---|---|
| **Transcripción literal estructurada** | Whisper, subtítulos o texto pegado, organizado en bloques por la IA. | Alta: es lo que se dice de verdad. |
| **Pre-guion reconstruido por IA** | La IA lo deduce de título, descripción, etiquetas, comentarios, cortes, pausas y **fotogramas**. | La estructura y el mensaje son fiables. Las frases pueden no ser literales; salen **en cursiva y marcadas "reconstruido"**. |
| **Esqueleto sin IA** | Los tiempos reales de los planos con textos guía entre corchetes. | Solo estructura; tienes que completar los textos. |

**Cuándo se crea:**

- **Solo:** si analizas un video o enlace sin texto y tienes IA configurada.
- **A mano:** con **✦ Reconstruir el guion con IA**, o con **✦ Estructurar y anotar con IA** si ya hay transcripción.

**Qué muestra:**

- **Resumen:** de qué trata y qué promete.
- **Fórmula de estructura:** por ejemplo `Negación → credencial → secreto → mecanismo → prueba → CTA`.
- **Formato** (talking head, tutorial, POV, lista…) y **cómo funciona el gancho**.
- **Fidelidad del texto** (0–100 %) y **por qué funciona**.
- **Tabla bloque a bloque:** tiempo, tipo, lo que se dice, la intención, el texto en pantalla y lo que se ve.

**Botones:**

- **✔ Usar para el análisis**: normalmente ya se aplica solo.
- **✏ Editar el texto**: corrige frases y vuelve a analizar.
- **📋 Copiar** y **⬇ .txt**.
- **🧬 Replicar con mi idea →**: te lleva a la réplica.
- **↻ Regenerar con IA**.
- **↺ Volver a la transcripción original**: deshace la estructuración.
- **☐ Enviar fotogramas a la IA**: actívalo solo si tu modelo ve imágenes (Gemini, GPT-4o, llava, qwen-vl). Si el modelo no las acepta, la app reintenta solo con texto.

### 6.2 · Puntuaciones principales

Cinco tarjetas:

- **Índice viral**
- **Gancho 0–3 s**
- **Disparadores**
- **Retención estimada**
- **Ritmo y pausas**

El significado de cada una está en la [sección 10](#10--cómo-leer-los-resultados).

### 6.3 · Ritmo, pausas y silencios

- **Velocidad de habla** (palabras por minuto), **pausas** (cuántas dramáticas y cuántas de aire muerto), **pausa más larga**, **silencio inicial**, **tiempo con voz** y **variación de ritmo**.
- **Línea de tiempo:**
  - onda azul = voz
  - franjas naranjas = pausas
  - franjas rojas = pausas problemáticas
  - líneas rosas = cortes de cámara
  - barra inferior de colores = bloques del guion
- **Tabla de pausas:** momento, duración, tipo, después de qué frase, y qué significa.

La etiqueta del título indica de dónde salen los datos: *medido en el audio real*, *marcado a mano* o *estimado por marcas de tiempo*.

### 6.4 · Lenguaje visual

- **Cortes de cámara** (y cortes por minuto), **duración media del plano**, **cortes en los primeros 3 s**, **plano más largo** y **movimiento**.
- **Storyboard automático:** un fotograma por plano. Al tocar uno, el video se abre en ese momento.
- **Primer fotograma:** brillo y contraste. Avisa si es demasiado oscuro para una miniatura.

### 6.5 · YouTube · datos oficiales (con clave API)

- Vistas, **vistas por día**, **likes / vistas**, **comentarios / vistas** y **vistas / suscriptores** (🚀 si supera ×3: viral real).
- **Etiquetas ocultas**, que se pueden copiar.
- **Lo que dice el público:** los comentarios más relevantes, los **temas que se repiten** y cuántos son preguntas.

> **Las preguntas de los comentarios son guiones listos para tu próximo video.**

### 6.6 · Publicación

Analiza el texto del post: número de caracteres, hashtags (lo óptimo es 3–6), emojis, si la primera línea tiene gancho y si incluye CTA.

### 6.7 · Curva de retención proyectada

Estimación de qué porcentaje del público seguiría viendo en cada momento:

- **Suben la curva:** los disparadores y los cortes.
- **La bajan:** las pausas largas y los tramos sin estímulo.

Es **orientativa**: sirve para ver **dónde** se cae el interés, no para predecir cifras exactas.

### 6.8 · Por qué funciona · Riesgos y mejoras

Listas en lenguaje claro:

- **Verde:** lo que hace bien.
- **Rojo:** los riesgos, con el momento exacto.
- **Naranja:** las mejoras concretas.

### 6.9 · Guion forense (bloque a bloque)

Cada bloque muestra:

- **Tiempo y duración**, y el **tipo** de bloque (HOOK, LOOP, STORY, etc.).
- **La frase**, con las cifras resaltadas. Si es reconstruida, lleva la etiqueta "reconstruido".
- **Ritmo:** palabras, palabras por segundo, cortes y pausa interna.
- **Acción visual, texto en pantalla, sonido y propósito.**
- **Técnicas detectadas:** pasa el ratón por encima para ver la explicación.
- **Plantilla:** la frase convertida en variables, por ejemplo `Deja de comprarte {{PRODUCTO}} antes de ver esto`.
- **Etiqueta de riesgo:** ÓPTIMO, ATENCIÓN o RIESGO ALTO.
- **editar**: cambia la frase, el tipo o la acción visual.

Entre bloques aparece **"pausa X s"** cuando el original deja un silencio.

---

## 7 · Pantalla RÉPLICA: tu guion nuevo

### 7.1 · ✦ Replicar con IA desde tu idea (recomendado)

1. Escribe **tu idea** con detalle: qué vendes o enseñas, qué resultado prometes y qué quieres que haga el espectador.

   > **Ejemplo:** "Vendo un curso de repostería para principiantes. Quiero que vean que con 3 ingredientes pueden hacer un pastel que parece de tienda, y que me escriban PASTEL para recibir la receta."

2. Completa **Público**, **Palabra para comentar (CTA)** y **Tono**.
3. Pulsa **✦ Escribir mi guion réplica**.

La IA respeta el **mismo número de bloques, el mismo orden, la misma función y técnica** de cada uno, los tiempos, las pausas y un máximo de palabras por bloque. **No copia frases del original**: traslada su mecánica a tu idea.

La plataforma y la duración se toman de **Origen → Objetivo de tu video**. Tu idea queda guardada aunque cambies de pantalla.

### 7.2 · Alternativa sin IA · plantilla de réplica

Rellena los campos: Marca, Producto, Público, Dolor, Deseo, Prueba, Oferta, Plazo, Cifra, Porcentaje, Cantidad, Palabra CTA y Nicho. Los marcados con **●** aparecen en este guion.

Luego pulsa **🧬 Generar guion réplica**. Opciones:

- **Ajustar a la duración objetivo:** estira o comprime los tiempos.
- **CTA agresivo:** añade una frase de urgencia al final.

Los campos que no rellenes aparecen como `[PRODUCTO]` para que los completes a mano.

### 7.3 · Lo que recibes

- **✦ Tu video** (con IA): consejos de grabación, CTA alternativos y el texto para la publicación.
- **Ganchos alternativos (A/B):** graba 3 y compara cuál retiene más a los 3 segundos.
- **Guion de grabación**, bloque a bloque:
  - frase exacta, cámara y acción, texto en pantalla, sonido, cortes heredados del original y función psicológica
  - **"deja una pausa de X s (como el original)"** donde corresponde
  - indicador de longitud: **encaja** / **largo** (recorta) / **corto** (añade o deja respirar)
- **Copiar guion completo (teleprompter)**.
- **Checklist de producción**, con casillas para marcar.
- **Descargas:** subtítulos `.srt`, plan de edición `.csv` (se abre en Excel) e informe `.md`.

---

## 8 · Empaque, Métricas, Biblioteca y Exportar

### Empaque

- **Títulos o primeras líneas** puntuados por patrón viral, con botón para copiar.
- **Hashtags** según nicho y plataforma: un set corto (5) o todos. Consejo: 3–5 específicos rinden más que 30 genéricos.
- **Ideas para la miniatura / frame 0**, junto al primer fotograma del original.
- **Franjas horarias orientativas.** Confírmalas con tus propias estadísticas.
- **✦ Mejorar con IA** genera títulos y hashtags nuevos.

### Métricas

Vistas, likes, comentarios y compartidos del original, y tres indicadores calculados:

- **Engagement** = (likes + comentarios + compartidos) / vistas. Más de 4 % es muy bueno.
- **Comentarios por like:** alto significa que genera conversación.
- **Compartidos por vista:** la señal más fuerte de viralidad.

Si la plataforma no las publica, cópialas de la app y pulsa **Guardar métricas**.

### Biblioteca

- **💾 Guardar proyecto actual**: guarda el análisis, el guion y la réplica en el navegador.
- **Abrir** o **borrar** proyectos guardados.
- **Exportar o importar** toda la biblioteca en JSON. Úsalo como **copia de seguridad** o para pasarla a otro equipo.

### Exportar (panel lateral o botón ⬇ Exportar)

| Formato | Contenido |
|---|---|
| **Informe .html** | Informe completo con storyboard. Ábrelo en el navegador o imprímelo a PDF. |
| **Informe .md** | Igual, en texto (Markdown). |
| **Guion réplica .srt** | Subtítulos de tu guion, para CapCut o cualquier editor. |
| **Plan de edición .csv** | Tabla bloque a bloque para Excel: tiempos, frase, cámara, texto y sonido. |
| **Proyecto .json** | Copia completa del proyecto. |
| **PDF (imprimir)** | Imprime la pantalla actual. |

---

## 9 · Recetas: el mejor camino según lo que tengas

### Receta A · Tienes el archivo del video (resultado máximo) ⭐

1. **Origen → 📹 Analizar video** → elige el archivo.
2. Espera los 4 pasos. Lo hace solo.
3. **Análisis:** revisa el *Guion del original* y las métricas de ritmo y pausas.
4. **Réplica → ✦ Escribir mi guion réplica** con tu idea.
5. Exporta el `.srt` y el `.csv` y graba.

### Receta B · Enlace de YouTube

1. Configura la **clave de YouTube** (paso 3) y la **IA** (paso 2).
2. **Origen → 🔗 Analizar enlace**.
3. Si bajan los subtítulos y el video, el análisis es completo. Si no:
   - **Pegar transcripción** (Mostrar transcripción en YouTube), o
   - **🎥 Capturar pestaña**, o
   - deja que la IA **reconstruya el pre-guion**.
4. Revisa los **comentarios del público**: ideas para tus próximos videos.
5. **Réplica con tu idea.**

### Receta C · Enlace de TikTok, Instagram o Facebook

1. **🔗 Analizar enlace** para obtener el título, el texto y los hashtags.
2. Elige **una** forma de conseguir el ritmo real:
   - **🎥 Capturar pestaña** (PC). **La mejor.**
   - **Guardar el video** (TikTok: Compartir → Guardar video) o **grabar la pantalla del móvil con audio**, y subirlo.
   - **⏱ Marcar en vivo** cortes y pausas.
3. Escribe las **métricas** en el formulario (vistas, likes, comentarios, compartidos).
4. Deja que la IA **reconstruya el guion**, o pega el texto si lo tienes.
5. **Réplica con tu idea.**

### Receta D · Solo tienes el texto o una idea de estructura

1. **Origen → 📝 Pegar guion** (mejor con tiempos: `0:03 texto`).
2. Análisis → Réplica.
3. Si no tienes tiempos, la app los estima con tu ritmo de palabras por minuto.

---

## 10 · Cómo leer los resultados

### Índice viral (0–100)

| Componente | Peso | Qué mide |
|---|---|---|
| **Gancho 0–3 s** | 30 % | Fuerza de los primeros 3 segundos: disparadores, cifras, longitud, si habla de "tú". |
| **Disparadores** | 20 % | Densidad de técnicas psicológicas por bloque. |
| **Retención estimada** | 20 % | Área bajo la curva de retención. |
| **Ritmo y pausas** | 20 % | Velocidad de habla, aire muerto, silencio inicial y duración de los planos. |
| **CTA** | 10 % | Si hay llamada a la acción clara al final. |

| Nota | Lectura |
|---|---|
| 0–19 | semilla |
| 20–39 | mejorable |
| 40–59 | fuerte |
| 60–79 | alta viralidad |
| 80–100 | máquina viral |

### Tipos de bloque

| Bloque | Función |
|---|---|
| **HOOK** | Detener el scroll en menos de 1,5 s con una promesa concreta. |
| **LOOP** | Abrir una curiosidad que solo se cierra al final. |
| **PAIN** | Activar el dolor del público para que se reconozca. |
| **STORY** | Humanizar con una historia y bajar las defensas. |
| **SOLUTION** | Presentar el mecanismo, el "cómo" inesperado. |
| **PROOF** | Mostrar evidencia: antes/después, cifras o capturas. |
| **TRANSFORM** | El resultado final, de antes a después. |
| **BRIDGE** | Transición que sube el ritmo. |
| **CTA** | Convertir la atención en acción (comentar, guardar, seguir). |

### Tipos de pausa

| Pausa | Duración | Lectura |
|---|---|---|
| **Respiración** | menos de 0,55 s | Natural, mantiene el ritmo. |
| **Pausa dramática** | 0,55–1,3 s | Con intención: funciona antes de una revelación o una cifra. |
| **Aire muerto** | más de 1,3 s | Se pierde gente: recórtala o tápala con imagen o sonido. |
| **Silencio inicial** | cualquiera al inicio | Cuesta retención: el video debe arrancar ya. |

### Los 18 disparadores psicológicos

Interrupción de patrón · Sesgo de negatividad · Brecha de curiosidad · Loop abierto · Especificidad numérica · Autoridad / experiencia · Prueba social / evidencia · Escasez / urgencia · Identificación · Transformación · Narrativa · Contraste / revelación · Llamada a la acción · Bandera de retención · Carga emocional · Dirección al tú · Pregunta retórica · Estructura de lista.

En la app, pasa el ratón por cada etiqueta para ver por qué funciona.

### Referencias rápidas para formato corto

| Métrica | Valor recomendado |
|---|---|
| Velocidad de habla | 140–200 palabras/min |
| Duración media de plano | 1–3 s |
| Cortes en los primeros 3 s | al menos 1 |
| Plano más largo | menos de 5 s |
| Silencio inicial | menos de 0,3 s |
| Hashtags | 3–6 |
| Likes / vistas (YouTube) | más de 2 % bueno, más de 4 % excelente |
| Vistas / suscriptores | más de 1× bien, más de 3× viral |

---

## 11 · Consejos para obtener los mejores resultados

1. **Configura todo y prueba cada paso** antes de analizar: transcripción ✓, IA ✓ y YouTube ✓.
2. **El video real gana a todo.** Con el archivo (o la captura de pestaña) la app **mide**. Sin él, **estima**.
3. **Usa Gemini con "enviar fotogramas"** activado: el pre-guion mejora mucho cuando la IA ve las imágenes.
4. **Si la IA reconstruye el guion, revísalo.** Usa **✏ Editar el texto** para corregir frases que no encajen, sobre todo el gancho.
5. **Analiza 3–5 videos virales del mismo nicho** y guárdalos en la Biblioteca. Si se repite la misma fórmula, esa es la que funciona en tu nicho.
6. **Elige originales que superen a su audiencia** (vistas / suscriptores mayor que 3×): son virales por estructura, no por fama.
7. **Escribe tu idea con detalle** en la réplica: producto, resultado concreto, cifra creíble, público y CTA. Cuanto más concreta, mejor el guion.
8. **Respeta las pausas marcadas.** Son donde el original crea tensión.
9. **Graba el gancho 5 veces** y quédate con la toma de más energía. Prueba los ganchos A/B en publicaciones distintas.
10. **Mira la indicación de longitud** ("largo", "encaja", "corto") antes de grabar: si una línea es "larga", no cabe en su tiempo.
11. **Lee los comentarios del público** del original: las preguntas repetidas son tus próximos 10 videos.
12. **Haz copia de seguridad** de la Biblioteca (Exportar JSON) de vez en cuando.

---

## 12 · Solución de problemas

| Problema | Causa probable | Solución |
|---|---|---|
| "El navegador no puede abrir este video" | Formato HEVC/H.265 (iPhone), MKV o AVI | Conviértelo a MP4 (H.264) con HandBrake o CapCut. La app te da el comando para copiar. |
| "No se pudo leer el audio" | Video sin sonido o códec raro | Convierte el audio a AAC, o marca las pausas a mano. |
| "No se detectó voz" | Video solo con música o con texto en pantalla | Copia los textos en pantalla como guion con tiempos (`0:03 texto`), o deja que la IA lo reconstruya. |
| "La transcripción automática no está configurada" | No completaste el paso 1 | ⚙ Configuración → paso 1. |
| "No se pudo cargar el motor de transcripción" | Sin internet la primera vez | Conéctate una vez. Después funciona sin conexión. |
| "Faltan archivos del modelo" | La carpeta del modelo está incompleta o no es ONNX | Elige otro modelo, o descarga la versión compatible en esa carpeta. |
| El modelo se vuelve a descargar cada vez | App abierta como archivo y el navegador no guarda | Usa la opción "Guardar en una carpeta", o abre la app desde un hosting. |
| La IA "no se pudo conectar" (Ollama) | Falta permitir conexiones | Abre Ollama con `OLLAMA_ORIGINS=*`. |
| La IA "no se pudo conectar" (LM Studio) | Servidor apagado o sin CORS | Developer → Start Server → activa CORS. |
| La IA da "clave no válida" o "límite de uso" | Clave incorrecta o cupo diario agotado | Revisa la clave, espera al día siguiente o cambia de modelo. |
| "El modelo no acepta imágenes" | Modelo sin visión | La app reintenta solo con texto; o desmarca "enviar fotogramas". |
| La captura de pestaña no tiene sonido | No marcaste "Compartir audio" | Repite la captura y marca la casilla de audio. |
| La captura no detecta bien los cortes | El video ocupaba poca parte de la pestaña | Ponlo a **pantalla completa** antes de capturar. |
| No se bajan los subtítulos o el video de YouTube | Servidores públicos caídos | Pega la transcripción, captura la pestaña o usa `yt-dlp`. |
| TikTok, Instagram o Facebook sin métricas | La plataforma no las publica | Cópialas de la app al formulario. |
| "No hay espacio en el navegador" | Biblioteca muy grande | Exporta la biblioteca y borra proyectos viejos. |

---

## 13 · Atajos de teclado y glosario

### Atajos

| Tecla | Acción |
|---|---|
| **Ctrl + Enter** | Analizar y abrir la pantalla Análisis |
| **Ctrl + S** | Exportar el informe .html |
| **C** o **espacio** (en ⏱ Marcar en vivo) | Marcar un corte |
| **P** mantenida (en ⏱ Marcar en vivo) | Marcar una pausa mientras dure |
| **Enter** en el campo del enlace | Analizar enlace |

### Glosario

- **Gancho (hook):** los primeros 1–3 segundos, que deciden si la persona se queda.
- **CTA (llamada a la acción):** lo que pides al final (comentar, guardar, seguir).
- **Plano:** tramo de video entre dos cortes de cámara.
- **Aire muerto:** silencio largo sin estímulo visual ni sonoro.
- **Pre-guion:** guion reconstruido por la IA cuando no hay transcripción. Es fiable en estructura y aproximado en las frases exactas.
- **Whisper:** sistema de reconocimiento de voz que transcribe con tiempos exactos.
- **ONNX:** formato de modelo que puede ejecutar el navegador.
- **Clave API:** "llave" que te dan Google, Groq, etc. para usar sus servicios desde la app.
- **SRT / VTT:** archivos de subtítulos con tiempos.
- **Engagement:** interacción del público en relación con las vistas.

---

*REPLICATOR analiza estructuras para inspirar contenido original. Descarga solo material propio o con permiso, y crea siempre con tu voz, tu producto y tus pruebas.*
