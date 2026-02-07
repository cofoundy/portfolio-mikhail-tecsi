# Propuesta de Diseno: Mikhail Tecsi — PRO S/.150

## Analisis

- **Profesion:** Abogado / Academico / Investigador en Filosofia del Derecho e IA
- **Industria:** Academia / Derecho / Filosofia
- **Audiencia objetivo:** Academia, universidades, revistas juridicas, investigadores
- **Vibe deseado:** Elegante, sobrio, academico, distinguido
- **Lo que tiene:** Ya tiene contenido excelente (9 publicaciones, 4+ conferencias, 5 edu entries)
- **Lo que le falta:** Scroll animations, mejor jerarquia visual, hover effects, polish general

## Que Significa "Pro" (S/.150)

El portfolio YA tiene buen contenido y custom sections (Publications, Conferences). Lo que necesita:

1. **Scroll reveal animations** (IntersectionObserver)
2. **Mejorar cards y secciones** (sombras, bordes, mejor spacing)
3. **Hover effects** en publications/conferences cards
4. **Better visual hierarchy** (section headers con acento)
5. **Section dividers** (lineas decorativas en ciruela)
6. **Improved timeline** en experiencia
7. **Stats/metrics highlight** (9 publicaciones, 5+ conferencias, 3 paises)
8. **Typography refinement** (mejor uso de Playfair Display)

---

## Paleta Final (del cliente — NO cambiar)

| Token | Color | Uso |
|-------|-------|-----|
| **Background** | `#FBF7F2` | Fondo principal. Blanco calido, elegante. |
| **Text Primary** | `#222222` | Negro suave. Legibilidad. |
| **Accent** | `#3B1B4A` | Ciruela/berenjena. Headings, accents, badges. |
| **Secondary** | `#102A43` | Azul tinta. Company names, secondary emphasis. |
| **Surface** | `#F5F0EA` | Cards, secciones alternas. Crema suave. |
| **Surface Border** | `#E8E0D6` | Bordes de cards. Sutil. |
| **Accent Light** | `#3B1B4A1A` | 10% opacity del acento para hover backgrounds. |

---

## Tipografia (mantener, refinar)

| Rol | Font | Cambio |
|-----|------|--------|
| **Headings** | **Playfair Display** | Mantener. Usar mas consistente en section headers. |
| **Body** | **Inter** | Mantener. |
| **Accent** | **Fira Code** (opcional) | Para publication links o metadata. |

---

## Mejoras por Seccion

### 1. HERO — Agregar animacion de entrada + metricas
```
ANTES:
  MH initials + nombre + titulo + email button

AHORA:
  MH initials (fade-in + scale) +
  nombre (blur-in delayed) +
  titulo (stagger fade) +
  ── linea decorativa ciruela ──
  [9 Publicaciones] [5+ Conferencias] [3 Paises]  ← NUEVO
  email button (fade-up delayed)
```
- Agregar mini stats row debajo del titulo
- Animacion: stagger fade-in, 0.15s entre items

### 2. ABOUT — Agregar iconos de areas + reveal
```
ANTES:
  Texto + skill badges estaticos

AHORA:
  Texto con reveal-left animation +
  "Areas de Investigacion" con icon highlights:
  ⚖️ Filosofia del Derecho
  🤖 IA Legal
  📚 Argumentacion Juridica

  Skill badges con hover effect (scale + accent bg)
```

### 3. EDUCATION — Timeline mejorado + badges
```
ANTES:
  Cards simples con fondo surface

AHORA:
  Timeline vertical con connector line en ciruela +
  Date pills mejorados (mas visibles) +
  Achievement badges con accent-colored border +
  Stagger reveal animation (0.15s entre cards) +
  "En curso" badge animado para PhD
```

### 4. PUBLICATIONS — Cards mejoradas + hover
```
ANTES:
  Year badge + titulo + journal, sin hover

AHORA:
  Year badge con gradient (ciruela → navy) +
  Titulo en hover: underline slide animation +
  Journal name en italic + icon de enlace externo +
  Card hover: translateY(-2px) + shadow-md +
  Fade-in stagger animation on scroll +
  "Ver PDF" button para los que tienen link
```

### 5. CONFERENCES — Grid mejorado + badges
```
ANTES:
  2-col grid, role badges simples

AHORA:
  2-col grid con mejor spacing +
  Role badges con borde ciruela +
  Location con icon 📍 +
  Year prominente +
  Card hover: subtle scale(1.01) + border-accent +
  Reveal animation from left/right alternating
```

### 6. PROJECTS (Research) — Numbered cards mejoradas
```
ANTES:
  Numbered cards (01-04), skill tags

AHORA:
  Numbered cards con accent-colored number +
  Description truncada con "Leer mas" expandible +
  Skill tags con hover effect +
  Card reveal-scale animation
```

### 7. EXPERIENCE — Timeline pro
```
ANTES:
  Timeline con dots simples

AHORA:
  Timeline con grow animation (line grows on scroll) +
  Dots que se llenan al hacer scroll (outline → filled) +
  Company name en azul tinta (bold) +
  Date pills mas prominentes +
  Bullet points con accent-colored bullet markers
```

### 8. HEADER — Glass effect mejorado
```
ANTES:
  6 nav items, basic glass on scroll

AHORA:
  Glass effect con backdrop-blur-lg +
  Active section indicator (underline en ciruela) +
  Scroll progress indicator (thin line at top) +
  Smooth scroll to sections
```

### 9. FOOTER — Mejorado con contexto
```
ANTES:
  Nombre + location + email + copyright

AHORA:
  "Portfolio Academico" tagline +
  Nombre con Playfair Display +
  Location + email +
  Linea decorativa ciruela +
  "Construido con ♥ por Cofoundy"
```

---

## Motion Design Plan

### Scroll Reveals (PRINCIPAL MEJORA)
```css
.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s ease-out;
}
.reveal.active {
  opacity: 1;
  transform: translateY(0);
}
.reveal-left { transform: translateX(-30px); }
.reveal-right { transform: translateX(30px); }
.reveal-scale { transform: scale(0.95); }
```
- Threshold: 0.15
- Stagger: 0.12s entre siblings
- Usar IntersectionObserver en `<script>` tag de index.astro

### Hero Entrance
- Initials MH: scale(0.9→1) + opacity(0→1), 0.6s
- Nombre: blur(8px→0), 0.5s, delayed 0.2s
- Titulo: fade-in, delayed 0.4s
- Stats row: stagger fade-up, delayed 0.6s
- Email button: fade-up, delayed 0.8s

### Hover Effects
- Publication cards: translateY(-3px) + shadow-md, 0.25s
- Conference cards: scale(1.01) + border-color(transparent→accent), 0.2s
- Skill badges: scale(1.05) + bg-accent/10, 0.15s
- Timeline entries: border-left-width(2→4px), 0.2s
- Nav items: text-decoration underline slide

### Micro-Interactions
- Timeline line: grow on scroll (height animation via IntersectionObserver)
- "En curso" badge: subtle pulse, 3s infinite
- External link icons: slight rotate(0→5deg) on hover
- Section headers: accent underline reveals on scroll

### Mobile
- Reduce translateY to 20px
- Reduce stagger to 0.08s
- prefers-reduced-motion: opacity only
- Conference grid: 1 column on mobile
- Larger touch targets (48px min)

---

## Diferencias vs. Current

| Aspecto | Antes | Ahora (Pro) |
|---------|-------|-------------|
| Scroll | Estatico | Full IntersectionObserver reveals |
| Hero | Fade-in basico | Stagger + blur + stats row |
| Cards | Planas | Hover effects + shadows + transitions |
| Timeline | Dots + line | Grow animation + fill on scroll |
| Header | Basic glass | Glass + active indicator + scroll progress |
| Typography | Inconsistente | Playfair Display consistente en headers |
| Section dividers | Ninguno | Lineas decorativas en ciruela |
| Stats | Ninguno | Mini stats row en hero |
| Badges | Basicos | Gradient + border + hover |

---

## Lo que NO cambia
- Contenido (ya esta excelente)
- Paleta de colores (respetamos las preferencias del cliente)
- Layout general de secciones (ya esta bien organizado)
- Custom sections (Publications, Conferences — ya existen)
- Avatar MH con iniciales (sin foto)
- Solo email como contacto

---

*Pro = Polish visual + animaciones + hover effects. Contenido ya es solido.*
