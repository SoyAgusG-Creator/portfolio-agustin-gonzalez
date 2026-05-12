---
# CONTEXTO_CTX.md — Portfolio Agustín González
_Versión 1.0 — 2026-05-12_

---

## §1 IDENTIDAD
```yaml
proyecto: Portfolio Personal
operador: Agustín González (Agus)
email: 444agusgonzalez@gmail.com
modelo_ia: Claude Sonnet 4.6 (Claude Code)
etapa: producción — desplegado en Vercel
nicho: Video editor freelance, short-form & long-form content
ubicacion: Córdoba, Argentina
```

---

## §2 STACK TÉCNICO
```yaml
index.html: único archivo — HTML/CSS/JS sin build step
github_repo: SoyAgusG-Creator/portfolio-agustin-gonzalez
vercel: auto-deploy on push to master → portfolio-agustin-gonzalez.vercel.app
youtube: thumbnails via img.youtube.com/vi/ID/(hq|maxres)default.jpg
favicon: assets/AGLOGO.ico + assets/AGLogo.png (fallback)
assets: assets/ — imágenes locales, logo, foto hero
```

---

## §3 ARCHIVOS EXISTENTES
```
✅ index.html              — portfolio completo, en producción
✅ assets/AGLOGO.ico       — favicon principal
✅ assets/AGLogo.png       — favicon fallback
✅ assets/[foto-hero].jpg  — imagen hero desktop/mobile
✅ Backup/index.html       — copia de seguridad (este backup)
✅ Backup/CONTEXTO_CTX.md  — este archivo
```

---

## §4 ARQUITECTURA TÉCNICA
```
index.html
├── <head>         CSS custom properties, favicon, meta
├── <style>        todo el CSS inline
│   ├── :root      --bg:#090909  --o1:#ff6b35  --o2:#ff9500  --grad
│   ├── hero       CSS Grid: grid-template-rows: auto auto
│   ├── marquee    animation: mq 30s linear infinite / translateX(-50%)
│   ├── pvc-wrap   carrusel vertical (short content) — 3 visibles
│   ├── phc-wrap   carrusel horizontal (long/vsl/trailers) — 1 a la vez
│   └── @media     max-width:1100px breakpoint principal
├── <body>
│   ├── nav
│   ├── #hero      hero-text-top / hero-img-side / hero-text-bot
│   ├── marquee    logos de herramientas (duplicados para loop)
│   ├── #work      6 project cards (pvc1-3, phc4-6)
│   ├── #how       "How I Work" — 5 pasos
│   ├── #hle       HLE carousel horizontal
│   └── footer
└── <script>       openV(), pvcMove(), phcMove(), modal YouTube
```

---

## §5 FLUJOS DE DATOS CANÓNICOS
```
Edición local index.html
→ git add + commit + push (master)
→ Vercel auto-deploy
→ portfolio-agustin-gonzalez.vercel.app

Thumbnail video:
ID de YouTube → img.youtube.com/vi/ID/hqdefault.jpg (shorts/vertical)
ID de YouTube → img.youtube.com/vi/ID/maxresdefault.jpg (landscape)

Click en thumbnail:
onclick="openV('ID')" → modal overlay → iframe youtube.com/embed/ID?autoplay=1
```

---

## §6 DECISIONES BLOQUEADAS
```
D1: Single-file HTML — sin frameworks, sin build step
D2: Dark theme — fondo #090909, acentos naranja #ff6b35/#ff9500
D3: Deploy Vercel via GitHub push automático
D4: Thumbnails YouTube externos — no embeds en carruseles
D5: overflow-x:hidden en html Y body (fix iOS Safari scroll)
D6: HLE carousel offset hardcodeado 206px (200 + 6 gap)
D7: Carruseles short = vertical pvc; long/vsl/trailers = horizontal phc
D8: Hero: grid 2 columnas desktop; mobile imagen entre subtítulo y CTAs
```

---

## §7 ERRORES CONOCIDOS Y FIXES
```yaml
- error: YouTube Error 153 en videos unlisted
  fix: era protocolo file:// — resolver deployando a Vercel
  check: siempre testear en URL pública, no local

- error: overflow horizontal en mobile iOS Safari
  fix: overflow-x:hidden en html + body + max-width:100vw en body
  check: no solo en body

- error: @media block roto al insertar nueva regla responsive
  fix: merge de ambas reglas dentro de un solo bloque @media
  check: nunca abrir nuevo @media si ya existe uno para el mismo breakpoint

- error: video insertado en sección incorrecta (phc4 en vez de HLE)
  fix: revertir manualmente y reinsertar en el ID correcto
  check: verificar id del contenedor (pvc1-3, phc4-6, hle) antes de editar

- error: HLE carousel con offsetWidth=0 (timing DOM)
  fix: hardcodear 206px en vez de items[0].offsetWidth + 6
  check: items son flex: 0 0 200px — siempre 200px
```

---

## §8 OPTIMIZACIONES ACTIVAS
- Thumbnails lazy loading (`loading="lazy"`) en todos los `<img>`
- Marquee loop sin JS: solo CSS animation + HTML duplicado
- Sin dependencias externas (0 requests a CDN de JS/CSS)
- Un solo archivo HTML → 1 request inicial

---

## §9 PERFIL DEL OPERADOR
```yaml
nombre: Agus
idioma_trabajo: español rioplatense
estilo_comunicacion: directo, informal, eficiente
prefiere: cambios puntuales > rewrites completos
tolera: respuestas cortas sin explicación extendida
no_le_gusta: código comentado innecesariamente, over-engineering
velocidad: prefiere deploy rápido, iterar después
contexto_tecnico: conoce HTML/CSS básico, no es dev — delega a Claude
```

---

## §10 FRAMEWORK DE EVALUACIÓN
1. ¿Afecta un archivo solo? → editar directamente
2. ¿Requiere nuevo componente? → reusar patrón existente (pvc/phc thumb)
3. ¿Cambia layout? → testear breakpoint 1100px
4. ¿Nuevo video? → short usa hqdefault.jpg, landscape usa maxresdefault.jpg
5. ¿Cambio visual? → push a Vercel y verificar en producción

**Filtro rápido:** ¿Puedo editar solo index.html sin tocar nada más? → Sí → hacerlo.

---

## §11 ESTADO ACTUAL Y PENDIENTES
```yaml
listo:
  - 6 secciones de proyectos (pvc1-3, phc4-6)
  - Hero mobile/desktop con imagen
  - Marquee con logos de herramientas
  - Sección "How I Work" (5 pasos)
  - HLE carousel
  - Favicon AGLOGO
  - Deploy en Vercel activo
  - Último push: g24fLUx34ck (pvc2 #1) + z0w-HZa3c3w (pvc3 #2)

pendiente_inmediato: []

pendiente_mediano_plazo:
  - Evaluar animaciones (Three.js / GSAP) — pregunta pendiente del operador
  - SEO / meta og:image
```

---

## §12 REGLAS DE TRABAJO
```
R1: Editar solo index.html — nunca crear archivos JS/CSS separados
R2: Push a GitHub = deploy automático a Vercel
R3: Leer el bloque exacto antes de editar — evitar string not found
R4: Short videos → hqdefault.jpg; landscape → maxresdefault.jpg
R5: Verificar ID del contenedor antes de insertar video
R6: No abrir @media duplicados — merge en bloque existente
R7: No agregar comentarios al HTML salvo que Agus lo pida
R8: Respuestas cortas — Agus lee el diff, no necesita resumen
```

---
