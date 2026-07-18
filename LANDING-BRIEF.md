---
# DESIGN.md — Monitor de Consumo (landing page)
# Formato basado en la especificación google-labs-code/design.md:
# tokens legibles por máquina + prosa que explica el porqué.
name: monitorconsumo-landing
url: https://monitorconsumo.mrhapps.mx
colors:
  # La paleta viene directamente de la app y de su ícono.
  background: "#F5F5F7"          # gris Apple claro, fondo de página
  surface: "#FFFFFF"             # tarjetas / cards
  text-primary: "#1D1D1F"
  text-secondary: "#6E6E73"
  accent: "#0A84FF"              # azul macOS: CTAs y barras de progreso
  accent-hover: "#0060DF"
  gauge-green: "#59C247"         # degradado del ícono, para detalles/hero
  gauge-yellow: "#FAD426"
  gauge-orange: "#FC8F21"
  gauge-red: "#ED3329"
  dark-background: "#1C1C1E"     # modo oscuro (prefers-color-scheme)
  dark-surface: "#2C2C2E"
  dark-text-primary: "#F5F5F7"
  dark-text-secondary: "#98989D"
typography:
  fontFamily: "-apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Segoe UI', Roboto, sans-serif"
  headline: { fontSize: "56px", weight: 700, lineHeight: 1.1, letterSpacing: "-0.02em" }
  subheadline: { fontSize: "21px", weight: 400, lineHeight: 1.5 }
  sectionTitle: { fontSize: "36px", weight: 700, lineHeight: 1.2 }
  body: { fontSize: "17px", weight: 400, lineHeight: 1.6 }
  caption: { fontSize: "13px", weight: 400, lineHeight: 1.4 }
spacing:
  scale: [8, 16, 24, 40, 64, 96, 140]   # px; secciones separadas por 96–140
  maxWidth: "1080px"
rounding:
  card: "18px"
  button: "12px"
  screenshot: "14px"
components:
  cta-button:
    background: accent
    color: "#FFFFFF"
    padding: "16px 32px"
    fontSize: "17px"
    weight: 600
    shadow: "0 4px 14px rgba(10,132,255,0.35)"
  badge-pill:
    background: "rgba(0,0,0,0.05)"
    color: text-secondary
    fontSize: "13px"
    padding: "4px 12px"
    radius: "999px"
---

# Brief: landing page de Monitor de Consumo

**Para el agente/chat que construya esta página:** este documento contiene todo lo
necesario — estructura, copy final en español, tokens de diseño (front matter YAML,
úsalo como fuente de verdad), requisitos técnicos y assets. La página se sirve como
**sitio estático** en un VPS bajo `https://monitorconsumo.mrhapps.mx`. Genera un solo
`index.html` autocontenido (CSS inline o un solo archivo), sin frameworks ni build
steps. Debe soportar modo oscuro vía `prefers-color-scheme` y verse perfecta en móvil.

## Qué es el producto

**Monitor de Consumo** es una app **gratuita** de barra de menús para macOS que
muestra en tiempo real los límites de uso de **Claude Code** y **Codex**: sesión de
5 horas, límites semanales (todos los modelos y por modelo, p. ej. Fable), créditos
extra y cuándo se reinicia cada ventana. No requiere login propio: usa las sesiones
que el usuario ya tiene iniciadas en los CLIs, y las credenciales **nunca salen de la
Mac**. Notarizada por Apple, binario universal, macOS 14+. Autor: Alejandro Aguilera
(@mr_happs).

## Filosofía de diseño (prosa)

La página debe sentirse como una app nativa de macOS: aire, tipografía del sistema,
tarjetas blancas con esquinas continuas, sombras suaves. El acento de personalidad es
el **degradado del velocímetro** (verde→amarillo→naranja→rojo del ícono): úsalo con
moderación — una línea decorativa, el subrayado del headline o el fondo difuminado del
hero — nunca como fondo de secciones completas. Todo lo demás es sobrio: azul macOS
para acciones, grises Apple para texto. Cero stock photos, cero ilustraciones
genéricas: los únicos visuales son el ícono real y las capturas reales.

---

## Estructura y copy (final, en español)

### 1. Hero
- Logo pequeño (app-icon.png) + "Monitor de Consumo" arriba a la izquierda.
- **Headline:** `Tus límites de Claude y Codex, siempre a la vista.`
- **Subheadline:** `Una app de barra de menús para Mac que te dice cuánto te queda de
  sesión, de semana y de créditos — antes de que el "límite alcanzado" te corte la
  inspiración.`
- **CTA primario:** botón `Descargar gratis para Mac` → `/download/MonitorConsumo.zip`
- Debajo del botón, en caption: `macOS 14+ · Apple Silicon e Intel · Notarizada por Apple · 640 KB`
- **Visual:** captura `panel-screenshot.png` dentro de un marco de ventana mac
  (sombra grande, radius 14px). Idealmente sobre un fondo con el degradado del
  velocímetro muy difuminado.

### 2. El problema (sección corta, 2-3 líneas + 3 bullets)
Título: `¿Te ha pasado?`
Texto: `Estás en plena racha con Claude Code o Codex y de pronto: "has alcanzado tu
límite". Sin aviso, sin saber cuánto llevabas, sin saber cuánto falta para el reinicio.`
Bullets (con ✓ de beneficio):
- `Ve tu % restante en la barra de menús, sin abrir nada.`
- `Sabe exactamente cuándo se reinicia cada límite ("en 2d 8h").`
- `Decide con datos si esa tarea grande la corres hoy o mañana.`

### 3. Features (grid de 6 tarjetas, ícono SF-symbol-style + título + 2 líneas)
1. **Todo de un vistazo** — Sesión de 5 h, límites semanales (todos los modelos y por
   modelo, como Fable) y tus créditos extra, con barras de progreso y cuenta regresiva.
2. **Claude Code y Codex juntos** — Los dos servicios que usas para programar con IA,
   en un mismo panel. Muestra u oculta cada uno.
3. **Cero configuración** — Sin crear cuenta, sin API keys. Detecta las sesiones que ya
   tienes iniciadas en tus CLIs y funciona al instante.
4. **Privacidad primero** — Tus credenciales nunca salen de tu Mac. La app solo consulta
   los endpoints oficiales de uso de Anthropic y OpenAI. Sin analytics, sin servidores
   intermedios.
5. **A tu manera** — Elige qué muestra la barra de menús, el intervalo de actualización
   y si arranca al iniciar sesión.
6. **Siempre al día** — Te avisa dentro de la app cuando hay una versión nueva. Un clic
   y descargas la actualización.

### 4. Cómo funciona (3 pasos numerados, horizontal)
1. `Descarga y abre la app.` 2. `Aparece el velocímetro en tu barra de menús.`
3. `Haz clic y ve tus límites en tiempo real.`
(Nota bajo los pasos: `Requiere tener sesión iniciada en Claude Code y/o Codex CLI.`)

### 5. Galería
Por ahora solo `panel-screenshot.png` en grande (modo claro). Deja el grid preparado
para 2 capturas más (modo oscuro y ventana de Ajustes) con comentario HTML
`<!-- TODO: añadir capturas dark + ajustes -->`.

### 6. FAQ (acordeón, estas respuestas son REALES — no inventar otras)
- **¿Funciona en Apple Silicon?** Sí. El binario es universal: nativo en Apple Silicon
  (M1 en adelante) y en Macs Intel. Requiere macOS 14 Sonoma o posterior.
- **¿Es gratis?** Sí, completamente gratis.
- **¿Necesito crear una cuenta?** No. La app usa las sesiones que ya tienes iniciadas
  en Claude Code (`claude`) y/o Codex (`codex`). Si no usas esos CLIs, la app no tiene
  nada que mostrarte.
- **¿Qué pasa con mi privacidad?** Todo ocurre en tu Mac. La app lee las credenciales
  locales de tus CLIs y consulta únicamente los endpoints oficiales de uso de Anthropic
  y OpenAI. No hay analytics, ni tracking, ni servidores del desarrollador de por medio.
- **¿Es segura de instalar?** Sí: está firmada con Developer ID y notarizada por Apple,
  lo que significa que Apple escaneó el binario. Se abre con doble clic normal.
- **¿Cómo recibo actualizaciones?** La propia app te avisa cuando hay versión nueva y
  te lleva a la descarga. También puedes buscar actualizaciones manualmente en Ajustes.
- **¿Es una app oficial de Anthropic u OpenAI?** No. Es una herramienta independiente
  hecha por un desarrollador; Claude y Codex son marcas de sus respectivas empresas.

### 7. Social proof — OMITIR por ahora
No hay testimonios reales todavía. **No inventes testimonios.** Deja un comentario
`<!-- TODO: sección de testimonios cuando existan -->`. (Cuando los haya, irán entre
Features y FAQ.)

### 8. Footer
- Izquierda: ícono pequeño + `Monitor de Consumo` + `© 2026 Alejandro Aguilera`.
- Centro: enlaces `Privacidad` (→ /privacidad.html, genérala: página simple que diga
  que la app no recolecta ningún dato y que el sitio no usa cookies de tracking) y
  `Contacto` (→ mailto:yo@alejandroaguilera.mx).
- Derecha: badges de texto: `Notarizada por Apple` · `macOS 14+` · `Hecha en México 🇲🇽`.
- Línea final pequeña: `Claude es marca de Anthropic. Codex es marca de OpenAI. Esta
  app no está afiliada a ninguna de las dos.`

---

## Requisitos técnicos del sitio

1. **Estático y autocontenido**: un `index.html` (+ `privacidad.html`) sin dependencias
   externas (nada de CDNs, fuentes del sistema). Peso total < 1 MB sin contar capturas.
2. **Rutas que DEBEN existir en el servidor** (la app instalada depende de ellas):
   - `/download/MonitorConsumo.zip` — el binario (ya incluido en `deploy/download/`).
   - `/api/version.json` — feed de actualizaciones (ya incluido en `deploy/api/`).
     La app instalada consulta esta URL a diario; al publicar una versión nueva solo
     se sube el ZIP nuevo y se edita este JSON.
3. **SEO/OG**: `<title>Monitor de Consumo — límites de Claude y Codex en tu barra de menús</title>`,
   meta description con el subheadline, og:image con la captura, lang="es".
4. **Modo oscuro** via `prefers-color-scheme` usando los tokens `dark-*`.
5. **Responsive**: hero apilado en móvil, grid de features 3→2→1 columnas.
6. **El botón de descarga** apunta a `/download/MonitorConsumo.zip` con atributo
   `download`. Nada de "smart detection" de OS: es una app solo de Mac y se dice claro.

## Do's / Don'ts

- ✅ Tono directo y honesto, de desarrollador indie a desarrolladores. Tuteo.
- ✅ El degradado del velocímetro como acento decorativo puntual.
- ✅ Números y datos reales (640 KB, macOS 14+, 5 h, semanal).
- ❌ No inventar testimonios, cifras de usuarios ni logos de prensa.
- ❌ No usar logotipos oficiales de Anthropic/OpenAI (solo texto).
- ❌ No añadir analytics ni cookies (la promesa de privacidad aplica al sitio también).
- ❌ No headlines genéricos tipo "Potencia tu productividad con IA".

## Assets incluidos (carpeta `assets/`)

- `app-icon.png` — ícono maestro 1024×1024 (fondo transparente fuera del squircle).
- `panel-screenshot.png` — captura real del panel (720×~1250 @2x, modo claro).

## Estructura de despliegue en el VPS (carpeta `deploy/`)

```
monitorconsumo.mrhapps.mx/
├── index.html            ← lo genera este brief
├── privacidad.html       ← lo genera este brief
├── download/
│   └── MonitorConsumo.zip   (incluido, v1.1.0 notarizada)
└── api/
    └── version.json         (incluido)
```

**Flujo para publicar una actualización futura** (referencia para el dueño):
compilar con `./build_app.sh notarize` → subir el nuevo ZIP a `/download/` con el
mismo nombre → editar `version` y `release_notes` en `/api/version.json`. Todos los
usuarios verán el aviso de actualización en menos de 24 h.
