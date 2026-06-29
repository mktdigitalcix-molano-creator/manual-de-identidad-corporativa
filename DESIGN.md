# Design System — Skillia

> **Convención de tokens:** todos los tokens siguen el esquema `--{rol}-100` para el valor base,
> `--{rol}-10` para tintes (≈10% de opacidad) y `--{rol}-hover` para estados de interacción.
> Ningún color, tamaño o espaciado puede usarse hardcodeado fuera de las tablas de este documento.
> Cuando la paleta evolucione, el cambio ocurre en el token, no en cada componente.

> **Alcance de dark mode:** el landing, la web pública y los emails **no usan dark mode**.
> El único contexto con dark mode es el **Course Player** de MasterStudy (activable por el alumno).
> No generar variantes oscuras de landing, catálogo, dashboard ni componentes de marketing.

> **Stack real:** WordPress + MasterStudy LMS + Elementor (skilliaeducation.com).
> Los tokens conviven con clases nativas del tema (`.masterstudy-*`). Los overrides de Skillia
> se aplican sobre esas clases vía CSS custom, sin tocar los archivos del tema.

---

## 1. Filosofía / Brand feel

### Personalidad
- **Técnico-accesible:** domina la tecnología pero la explica sin jerga
- **Confiable:** cumple con SUNEDU/MINEDU, soporte directo
- **Motivador:** cada interacción refuerza la sensación de avance
- **Estructurado:** claro, organizado, sin saturación visual

### Arquetipos
- **Primario — El Héroe:** Skillia entrega herramientas que enriquecen el aprendizaje de profesores, coordinadores y alumnos
- **Secundario — El Sabio:** soporte directo, control 100% del desarrollo, conocimiento del marco regulatorio peruano

### A qué se parece
- **Blackboard** en estructura y jerarquía institucional: serio, limpio, sin ruido visual, promesa clara antes que features
- **Plurall** en calidez de segmentación: cada usuario (alumno, docente, coordinador, institución) se ve reflejado en el mensaje

### A qué NO debe parecerse
- **Plurall en estética:** ilustraciones infantiles y mascotas no aplican al B2B institucional peruano
- **Blackboard en temperatura emocional:** frío y monocromático no comunica progreso ni motivación
- **Glassmorphism:** sin efectos de vidrio esmerilado, `backdrop-filter: blur` ni transparencias superpuestas
- **Neón:** sin colores eléctricos fluorescentes, brillos tipo glow ni bordes luminosos sobre fondos oscuros
- **Interfaces de tendencia efímera:** sin efectos de moda que requieran justificación para existir

### Audiencia
Empresa B2B — cuatro perfiles de usuario con pesos distintos en la decisión de compra:

| Perfil | Rol en decisión | Canal principal |
|---|---|---|
| Representante institucional | Decisor final | LinkedIn, Facebook, YouTube |
| Coordinador de curso | Influenciador | Instagram, TikTok, WhatsApp |
| Docente | Usuario frecuente | Facebook, Instagram, LinkedIn |
| Alumno | Usuario final | TikTok, WhatsApp, Instagram |

### Principio rector
> **"Institucional en estructura, humano en tono. Cada elemento comunica avance o no tiene lugar."**

Aplicación práctica:
- Si un elemento visual no refuerza progreso, confianza o claridad → se elimina
- Si un efecto visual requiere justificación para existir → no pertenece a Skillia
- El espacio vacío no es ausencia de diseño: es una señal activa de que Skillia es clara y organizada

---

## 2. Color tokens

| Token | HEX | OKLCH | Uso |
|---|---|---|---|
| `--bg-100` | `#FFFFFF` | `oklch(1.000 0.000 263.3)` | Fondo principal de página |
| `--surface-100` | `#F1F5F9` | `oklch(0.968 0.007 248.1)` | Cards, paneles, fondos de sección |
| `--border-100` | `#E2E8F0` | `≈ oklch(0.929 0.013 255.5)` *(verificar)* | Bordes, divisores, separadores |
| `--primary-100` | `#2563EB` | `oklch(0.546 0.215 262.9)` | Links, íconos activos, estados seleccionados |
| `--primary-10` | `#EFF6FF` | `≈ oklch(0.970 0.014 254.6)` *(verificar)* | Hover de botón secondary |
| `--accent-100` | `#84CC16` | `oklch(0.768 0.204 130.9)` | CTAs y señal de progreso activo |
| `--accent-hover` | `rgba(132,204,22,0.85)` | — | Hover de botón primary |
| `--success-100` | `#14B8A6` | `oklch(0.704 0.123 182.5)` | Indicadores de avance intermedio (turquesa) |
| `--positive-100` | `#166534` | `≈ oklch(0.448 0.119 152.3)` *(verificar)* | Texto de badge "Gratis / Free" |
| `--positive-10` | `#F0FDF4` | `≈ oklch(0.982 0.018 156.7)` *(verificar)* | Fondo de badge "Gratis / Free" |
| `--text-100` | `#0F172A` | `oklch(0.208 0.040 265.8)` | Texto principal, títulos, labels, sombras |
| `--muted-100` | `#5B6776` | `≈ oklch(0.493 0.030 252.0)` *(verificar)* | Texto secundario, placeholders, metadatos |
| `--warning-100` | `#F59E0B` | `oklch(0.769 0.165 70.1)` | Alertas, badges de urgencia |
| `--warning-10` | `rgba(245,158,11,0.12)` | — | Fondo de badge/alerta moderada |
| `--danger-100` | `#EF4444` | `≈ oklch(0.637 0.208 25.3)` *(verificar)* | Acciones destructivas e irreversibles |
| `--danger-10` | `rgba(239,68,68,0.10)` | — | Hover de botón danger, fondo de alerta crítica |
| `--overlay` | `rgba(15,23,42,0.50)` | — | Fondo de overlay tras modales |

> **Cambio v1.1 — `--muted-100` pasó de `#64748B` a `#5B6776`.**
> Motivo: `#64748B` fallaba WCAG AA sobre `--surface-100` (4.34:1 < 4.5:1).
> `#5B6776` da **5.93:1** sobre `#FFFFFF` y **5.41:1** sobre `#F1F5F9` → AA en ambas.

> **Nota OKLCH:** los valores marcados *(verificar)* son aproximaciones de conversión; deja que la
> herramienta de build (o un convertidor HEX→OKLCH) los confirme. El HEX es la fuente de verdad.

### Reglas semánticas por token

**`--bg-100` (#FFFFFF)**
- ✅ Fondo de página completa, hero y secciones principales
- ❌ No usar en cards (usar `--surface-100`) · No usar como fondo de botón

**`--surface-100` (#F1F5F9)**
- ✅ Cards de cursos, paneles de dashboard, fondos de sección alternados
- ❌ No usar como fondo de página completa · No apilar surface sobre surface sin separador

**`--border-100` (#E2E8F0)**
- ✅ Bordes de card, nav, tabs, inputs y divisores (siempre 0.5–1px)
- ❌ No usar como fondo ni como color de texto

**`--primary-100` (#2563EB)**
- ✅ Links activos · Íconos de estado seleccionado · Barra 3 del isotipo (meta)
- ❌ No usar como fondo de botón CTA (ese rol es de `--accent-100`) · No usar en texto de cuerpo

**`--accent-100` (#84CC16)**
- ✅ Botón "Solicita tu DEMO" y todos los CTAs primarios · Barra 1 del isotipo (inicio) · Indicador de progreso activo
- ❌ No usar en texto de cuerpo · No usar como decoración neutral · No usar en títulos sin función de acción
- ⚠️ **WCAG:** falla contraste AA para body text sobre `#FFFFFF` y `#F1F5F9`. Usar solo en elementos ≥18pt bold o con texto `--text-100` encima.

**`--success-100` (#14B8A6)**
- ✅ Barra 2 del isotipo (progreso intermedio) · Indicadores de avance en dashboard · Tags de estado "en curso"
- ❌ No usar en texto de cuerpo (falla WCAG AA sobre fondo blanco) — misma restricción que `--accent-100`

**`--positive-100` / `--positive-10` (#166534 / #F0FDF4)**
- ✅ Par exclusivo del badge "Gratis / Free": texto `--positive-100` sobre fondo `--positive-10`
- ❌ No reutilizar como verde genérico (no es la familia de `--accent-100` ni `--success-100`)

**`--text-100` (#0F172A)**
- ✅ Todo el cuerpo de texto (Manrope) · Títulos (Outfit) · Labels de formulario · Color base de todas las sombras
- ❌ No usar como color de fondo (usar `--bg-100` o `--surface-100`)

**`--muted-100` (#5B6776)**
- ✅ Texto de apoyo, metadatos, fechas · Placeholders de input · Subtítulos de menor jerarquía
- ❌ No usar para texto de cuerpo principal · No usar en CTAs ni labels de acción
- → Contraste sobre `#FFFFFF`: **5.93:1** ✅ AA · sobre `#F1F5F9`: **5.41:1** ✅ AA

**`--warning-100` / `--warning-10` (#F59E0B / 12%)**
- ✅ Badges de notificación urgente · Alertas de score de riesgo · Destacados motivacionales puntuales
- ❌ No usar como color principal de sección · No usar en texto sin fondo oscuro debajo

**`--danger-100` / `--danger-10` (#EF4444 / 10%)**
- ✅ Botones y acciones destructivas o irreversibles (eliminar) · Alertas de error · Score de riesgo "alto/muy alto"
- ❌ No usar como acento decorativo · No usar para errores no bloqueantes (eso es `--warning-100`)

### Nota de implementación
Todos los tokens deben declararse en `:root` del CSS global. Mapeo de overrides del tema:

```css
:root {
  /* Override de variables nativas del tema */
  --accent_color: #2563EB;   /* antes #385bce → ahora = --primary-100 */
  --primary_color: #0F172A;  /* antes #303441 → ahora = --text-100 */
}
```

---

## 3. Tipografía

### Stack con fallbacks
```css
/* Titulares, navegación, CTAs, estructura */
font-family: "Outfit", "Inter", system-ui, sans-serif;

/* Cuerpo, datos, descripción, lectura */
font-family: "Manrope", "Segoe UI", system-ui, sans-serif;
```

Lógica del fallback:
- `"Inter"` / `"Segoe UI"`: sans geométricas de sistema, preservan ritmo visual si Outfit/Manrope no cargan (redes corporativas, colegios, institutos en Perú)
- `system-ui`: SF Pro (macOS/iOS), Segoe UI (Windows), Roboto (Android). Siempre disponible
- `sans-serif`: comodín absoluto. Nunca cae en Times New Roman

### Regla de distinción entre fuentes
La distinción es **semántica, no de tamaño** — el mismo step puede usar Outfit o Manrope:
- **Outfit →** estructura, acción, jerarquía (nav, CTA, títulos, KPI labels, headers de tabla)
- **Manrope →** contenido, datos, lectura (cuerpo, placeholder, celdas, descripción, badges, notificaciones)

### Escala modular
| Step | px | Fuente | Peso | Uso principal |
|---|---|---|---|---|
| xs | 12 | Manrope | Regular 400 | Firma cargo, metadata, timestamps |
| sm | 14 | Outfit | SemiBold 600 | KPI labels, firma nombre, `th` de tabla |
| sm | 14 | Manrope | Medium 500 | Badges, toasts, input label, totales |
| base | 16 | Outfit | SemiBold 600 | Navegación |
| base | 16 | Outfit | Bold 700 | CTA botón, modal CTA |
| base | 16 | Manrope | Regular 400 | Card descripción, cuerpo modal, placeholder, texto ingresado, celda de dato |
| lg | 18 | Manrope | Regular 400 | Subtítulo hero, texto descriptivo |
| xl | 24 | Outfit | SemiBold 600 | Títulos de sección, card título, modal título |
| 2xl | 32 | Outfit | Bold 700 | Números KPI grandes, dashboard |
| 3xl | 48 | Outfit | SemiBold 600 | H1 hero principal |

Nota de escala:
- xs→base (+2px): granularidad fina para UI densa (dashboard, formularios, firma de email)
- xl→3xl (ratio ~1.33): saltos contundentes para jerarquía visual en hero y landing

### Pesos disponibles
| Peso | Valor | Rol |
|---|---|---|
| Regular | 400 | Cuerpo de texto largo (Manrope) |
| Medium | 500 | Badges, toasts, helpers, datos (Manrope) |
| SemiBold | 600 | Navegación, títulos, labels (Outfit) |
| Bold | 700 | CTAs, KPI números, cards (Outfit) |
| ExtraBold | 800 | Titulares TikTok/Reels (Outfit) |

### Uso por componente
| Componente | Step | px | Fuente | Peso | Origen |
|---|---|---|---|---|---|
| H1 Hero | 3xl | 48 | Outfit | SemiBold 600 | MIVC §5.3 |
| Subtítulo Hero | lg | 18 | Manrope | Regular 400 | MIVC §5.3 |
| Modal título | xl | 24 | Outfit | SemiBold 600 | Derivado |
| Card título | xl | 24 | Outfit | SemiBold 600 | Confirmado |
| Número KPI grande | 2xl | 32 | Outfit | Bold 700 | Confirmado |
| Navegación | base | 16 | Outfit | SemiBold 600 | MIVC §5.3 |
| CTA botón | base | 16 | Outfit | Bold 700 | MIVC §5.3 |
| Modal CTA | base | 16 | Outfit | Bold 700 | Derivado |
| Card descripción | base | 16 | Manrope | Regular 400 | Confirmado |
| Modal cuerpo | base | 16 | Manrope | Regular 400 | Derivado |
| Input placeholder | base | 16 | Manrope | Regular 400 | Derivado |
| Input texto ingresado | base | 16 | Manrope | Regular 400 | Derivado |
| Tabla celda dato | base | 16 | Manrope | Regular 400 | Derivado |
| KPI label / métrica | sm | 14 | Outfit | SemiBold 600 | Confirmado |
| Firma nombre | sm | 14 | Outfit | SemiBold 600 | MIVC §5.1 |
| Tabla header columna | sm | 14 | Outfit | SemiBold 600 | Derivado |
| Input label | sm | 14 | Manrope | Medium 500 | Derivado |
| Badge score riesgo | sm | 14 | Manrope | Medium 500 | Confirmado |
| Tabla celda total | sm | 14 | Manrope | Medium 500 | Derivado |
| Toast / notificación | sm | 14 | Manrope | Medium 500 | Derivado |
| Firma cargo | xs | 12 | Manrope | Regular 400 | MIVC §5.1 |

### Uso por canal
| Canal | Principal | Secundario |
|---|---|---|
| TikTok / Reels | Outfit ExtraBold | Manrope Medium |
| Catálogo WhatsApp | Outfit ExtraBold | Manrope Regular/Light |
| Web / Landing | Outfit SemiBold | Manrope Regular |
| Botones CTA | Outfit Bold | — |
| Email transaccional | Manrope Regular | Outfit SemiBold |
| Firma de email | Outfit SemiBold 14 | Manrope Regular 12 |
| WhatsApp bot (n8n) | Reglas propias de copy — ver Identidad Verbal | |

### Restricción WCAG
`--accent-100` (#84CC16) y `--success-100` (#14B8A6) solo en texto de botones CTA con tamaño mínimo
**Bold 18px**. Nunca en cuerpo de texto — fallan WCAG AA sobre `--bg-100` (#FFFFFF) y `--surface-100` (#F1F5F9).

---

## 4. Espaciado y layout

### Fuentes de los valores
- Escala base: Elementor 4.0.7 (instalado en skilliaeducation.com)
- Max-width y grids: MasterStudy / Elementor container estándar
- Aire vertical entre secciones: referencia Plurall (~80–100px)
- Principio rector: "espacio generoso, nunca saturar el layout" (MIVC §6.3)

### Escala de espaciado
| Token | px | Uso |
|---|---|---|
| `--space-1` | 4 | Micro — separación ícono/texto, dot/label |
| `--space-2` | 8 | XS — gap interno badges, spacing entre tags |
| `--space-3` | 12 | SM — padding chips, gap en filas densas |
| `--space-4` | 16 | MD — padding de card, gap entre campos |
| `--space-5` | 24 | LG — gutter de grid, separación entre cards |
| `--space-6` | 32 | XL — padding horizontal sección, entre bloques |
| `--space-7` | 48 | 2XL — padding vertical sección media |
| `--space-8` | 64 | 3XL — padding vertical sección principal |
| `--space-9` | 80 | 4XL — separación entre secciones landing |
| `--space-10` | 100 | 5XL — hero padding vertical, secciones ancla |

> **Referencia Plurall aplicada a Skillia:** Plurall usa secciones con ~80–100px de aire vertical
> entre bloques. Skillia adopta ese principio (`--space-9` / `--space-10`) pero mantiene fondos
> blancos y superficies limpias en lugar del color saturado de Plurall. El espacio es la señal de
> claridad y organización — no el color.

### Grid por contexto
| Contexto | Columnas | Max-width | Gutter | Breakpoint |
|---|---|---|---|---|
| Landing / Home | 12 col | 1200px | 24–32px | Todos |
| Catálogo de cursos | 3 col | 1200px | 24px | Desktop |
| Catálogo de cursos | 2 col | 100% | 16px | Tablet |
| Catálogo de cursos | 1 col | 100% | 16px | Móvil |
| Course Player | Fijo | 100% | 0px | Desktop |
| Dashboard alumno | 2 col | 1200px | 24px | Desktop |
| Metabase interno | 12 col | 100% | 16–24px | Todos |
| Panel activación n8n | 1 col | 560px | 24px | Todos |

### Breakpoints (Elementor + MasterStudy)
| Nombre | Rango | Comportamiento |
|---|---|---|
| Desktop | > 1024px | Layout completo, grid de 3 cols para cursos |
| Tablet | 768px – 1024px | Grid 2 cols, sidebar Course Player colapsable |
| Móvil | < 768px | 1 col, navegación en hamburger, Metabase responsive |

### Detalle Course Player (MasterStudy)
- Sidebar izquierda (currículo): **260px** fija / colapsable en tablet
- Contenido central (lección): fluido, ocupa el resto
- Sidebar derecha (Q&A, opcional): activar en MasterStudy → Course Player → Discussion Sidebar
- Gutter entre sidebar y contenido: **0px** — el player es inmersivo
- Widget Flowise: overlay flotante, no altera el grid

### Radios de borde
| Token | Valor | Uso |
|---|---|---|
| `--radius-sm` | 4px | Badges internos, chips pequeños |
| `--radius-md` | 8px | Inputs, botones, tooltips |
| `--radius-lg` | 12px | Cards de curso, modales, paneles |
| `--radius-pill` | 9999px | Badges de score de riesgo, tags categoría |
| `--radius-none` | 0px | Bordes con accent lateral (border-left / border-top) |

> **Regla:** `--radius-none` es **obligatorio** cuando se usa `border-left` o `border-top` como accent.
> Esquinas redondeadas solo con borde completo en los 4 lados.

### Sombras
| Token | Valor | Uso |
|---|---|---|
| `--shadow-none` | `none` | Estado default, elementos flat |
| `--shadow-sm` | `0 1px 3px rgba(15,23,42,0.08)` | Cards en hover, inputs en focus |
| `--shadow-md` | `0 4px 12px rgba(15,23,42,0.10)` | Modales, dropdowns |
| `--shadow-lg` | `0 8px 24px rgba(15,23,42,0.12)` | Overlays, sidebar Course Player |

> El color base de todas las sombras es `--text-100` (#0F172A, Azul Medianoche). Nunca sombras
> negras neutras que rompan la temperatura de color.

---

## 5. Componentes

> **Nota de implementación:** MasterStudy usa clases CSS propias por componente
> (`masterstudy-button`, `masterstudy-tabs`, etc.). Los overrides de Skillia se aplican sobre esas
> clases sin modificar los archivos del tema — solo CSS custom en Elementor → Custom CSS o en un
> child theme. Las fuentes Open Sans / Montserrat / Roboto del tema base deben reemplazarse (ver
> sección final "Overrides globales requeridos").

### Button
**Origen:** MasterStudy nativo (`.masterstudy-button`) + override Skillia
**Variantes nativas del tema:** primary / secondary / tertiary / outline / danger · **Tamaños nativos:** sm / md

**Variantes Skillia**

| Variante | Fondo | Texto | Borde | Uso | Hover |
|---|---|---|---|---|---|
| **Primary** (CTA) | `--accent-100` | `--text-100` | none | "Solicita tu DEMO", "Crear una cuenta" | `--accent-hover` |
| **Secondary** | transparent | `--primary-100` | 1.5px solid `--primary-100` | "Explorar Cursos", "Conocer más" | bg `--primary-10` |
| **Ghost** | transparent | `--text-100` | 0.5px solid `--muted-100` | "Descartar" en modales, acciones de bajo peso | bg `--surface-100` |
| **Danger** | transparent | `--danger-100` | 1.5px solid `--danger-100` | Eliminaciones, acciones irreversibles | bg `--danger-10` |

> ⚠️ **Un solo CTA primary por sección** — regla Blackboard.

**Estados**
| Estado | Comportamiento |
|---|---|
| default | Opacidad 1, sin sombra |
| hover | Primary → `--accent-hover`; resto ver tabla |
| active | `transform: scale(0.98)`, mismo bg que hover |
| disabled | Opacidad 0.4, `cursor: not-allowed`, no interactivo |
| loading | Spinner visible, texto oculto, mismas dimensiones |

**Especificaciones por tamaño**
| Prop | md (default) | sm |
|---|---|---|
| height | 40px | 32px |
| padding | 0 20px | 0 14px |
| border-radius | `--radius-md` (8px) | `--radius-md` (8px) |
| font | Outfit Bold 700 / 16px | Outfit SemiBold 600 / 14px |
| icon | left o right / 16px | left o right / 14px |

### Card de curso
**Origen:** MasterStudy LMS nativo — Elementor widget (`.masterstudy-course-card`)

**Anatomía (de arriba a abajo)**
1. Imagen thumbnail — ratio 16:9, lazy loading activo
2. Badge categoría — pill top-left sobre imagen · Manrope Medium 500 / 12px / bg `--surface-100` / color `--text-100`
3. Badge precio — pill top-right sobre imagen
   - "Gratis" → bg `--positive-10` / color `--positive-100`
   - Precio → bg `--text-100` / color `--bg-100`
4. Título del curso — Outfit SemiBold 600 / 24px / color `--text-100` · máx 2 líneas (`line-clamp: 2`)
5. Descripción corta — Manrope Regular 400 / 16px / color `--muted-100` · máx 2 líneas
6. Metadatos — fila horizontal con separadores · Manrope Regular 400 / 12px / color `--muted-100` · Nivel · Nº lecciones · Duración
7. CTA "Quiero ver el curso" — Button primary sm, ancho completo de la card
8. Ícono favoritos — corazón top-right, 20px

**Especificaciones**
```
background: var(--bg-100);
border: 0.5px solid var(--border-100);
border-radius: var(--radius-lg);   /* 12px */
padding: 0 0 16px 0;
contenido padding: 0 16px;
shadow hover: var(--shadow-md);
transición hover: box-shadow 250ms ease-out;
```
**Override Skillia requerido:** reemplazar Open Sans → Manrope y Montserrat → Outfit vía
`.masterstudy-course-card { font-family: ... }`.

### Navegación (Nav)
**Origen:** Elementor Header + MasterStudy theme (`.stm-lms-header` / `.elementor-nav-menu`)

**Anatomía**
- Izquierda: imagotipo Skillia (360×64px)
- Centro: Inicio / Novedades / Cursos — Outfit SemiBold 600 / 16px
- Derecha: búsqueda (lupa) + Registro (secondary sm) + Iniciar Sesión (ghost sm)

**Especificaciones**
```
height: 64px mínimo;
background: var(--bg-100);
border-bottom: 0.5px solid var(--border-100);
position: sticky; top: 0; z-index: 100;
link color: var(--text-100);
link hover: var(--primary-100);
link activo: var(--accent-100) con border-bottom 2px solid;
transición: color 150ms ease-out;
```

### Tabs de categoría
**Origen:** MasterStudy nativo (`.masterstudy-tabs`) · Estilo recomendado: `nav-md`

**Especificaciones**
```
Tab default: Manrope Medium 500 / 14px / var(--muted-100);
Tab hover:   color var(--text-100); transición 150ms;
Tab activo:  Manrope Medium 500 / 14px / var(--text-100);
             border-bottom: 2px solid var(--accent-100);
background: transparent;
track border: 0.5px solid var(--border-100);  /* línea inferior completa */
padding tab: 8px 16px;
dark_mode: false;  /* Skillia no usa dark mode en landing */
```

### Progress bar
**Origen:** MasterStudy nativo + GamiPress (`.masterstudy-progress`)

**Anatomía**
- Track (fondo): `--surface-100` / height 8px / radius pill
- Fill 0–33%: `--accent-100` (Verde Lima)
- Fill 34–66%: `--success-100` (Turquesa)
- Fill 67–100%: `--primary-100` (Azul)
- Label %: Manrope Medium 500 / 12px / `--muted-100`

**Especificaciones**
```
height: 8px;
border-radius: var(--radius-pill);  /* 9999px */
track-bg: var(--surface-100);
transición fill: width 400ms ease-out;
label position: derecha del track, centrado vertical;
```
> **Principio:** la secuencia Lima→Turquesa→Azul replica el isotipo. La barra de progreso ES el isotipo en movimiento.

### Course Player sidebar
**Origen:** MasterStudy Course Player nativo (`.masterstudy-course-player-curriculum`, `.masterstudy-curriculum-accordion`)

**Anatomía**
- Sidebar izquierda fija — 260px
- Módulo (acordeón): Outfit SemiBold 600 / 14px / `--text-100`
- Lección (ítem): Manrope Regular 400 / 14px
- Ícono tipo lección: `stmlms-icon` (font icon nativo)

**Estados de lección**
| Estado | Indicador |
|---|---|
| Completada | ícono check / color `--accent-100` |
| Activa | bg `--surface-100` / text `--text-100` / bold |
| Bloqueada | ícono candado / color `--muted-100` |
| Pendiente | color `--muted-100` / sin ícono especial |

**Especificaciones**
```
width: 260px (fija en desktop);
background: var(--bg-100);
border-right: 0.5px solid var(--border-100);
item height: 48px;
item padding: 0 16px;
dark mode: DISPONIBLE — único contexto con dark mode (ver alcance al inicio).
           Activar vía .masterstudy-dark-mode-button en Course Player Settings.
```

### Input / formulario
**Origen:** Derivado del sistema — confirmar contra render real de MasterStudy/Elementor.

| Elemento | Especificación |
|---|---|
| Label | Manrope Medium 500 / 14px / `--text-100` |
| Container | bg `--bg-100`; border 1px solid `--border-100`; `--radius-md`; height 44px; padding 0 12px |
| Placeholder | Manrope Regular 400 / 16px / `--muted-100` |
| Texto ingresado | Manrope Regular 400 / 16px / `--text-100` |
| Focus | border 1.5px solid `--primary-100`; `--shadow-sm` |
| Error | border 1.5px solid `--danger-100`; helper text Manrope Regular 400 / 12px / `--danger-100` |
| Disabled | bg `--surface-100`; opacidad 0.6; `cursor: not-allowed` |

### Toast / notificación
**Origen:** Derivado del sistema — confirmar contra render real.

```
background: var(--bg-100);
border-left: 4px solid {color por tipo};
border-radius: var(--radius-none);   /* obligatorio por accent en border-left */
box-shadow: var(--shadow-md);
padding: 12px 16px;
texto: Manrope Medium 500 / 14px / var(--text-100);
```
| Tipo | Color del accent (border-left) |
|---|---|
| info | `--primary-100` |
| éxito | `--accent-100` |
| advertencia | `--warning-100` |
| error | `--danger-100` |
| progreso | `--success-100` |

### Badge score de riesgo
**Origen:** Confirmado (score) + tintes derivados.

```
forma: pill; border-radius: var(--radius-pill);
font: Manrope Medium 500 / 14px;
padding: 4px 12px;
```
| Nivel | Fondo | Texto |
|---|---|---|
| Bajo | `--positive-10` | `--positive-100` |
| Moderado | `--warning-10` | `--warning-100` |
| Alto | `--danger-10` | `--danger-100` |
| Muy alto | `--danger-100` | `--bg-100` |

### Modal / overlay
**Origen:** Derivado del sistema — confirmar contra render real.

```
overlay: var(--overlay);  /* rgba(15,23,42,0.50) */
container bg: var(--bg-100);
border-radius: var(--radius-lg);  /* 12px */
box-shadow: var(--shadow-lg);
max-width: 560px;
padding: 24px;
```
- Badge contexto: pill superior (Manrope Medium 500 / 12px)
- Título: Outfit SemiBold 600 / 24px / `--text-100`
- Cuerpo: Manrope Regular 400 / 16px / `--text-100`
- CTA primario: Button **primary** · CTA secundario: Button **ghost**
- **Regla de copy:** un solo CTA primario por modal.

---

## 6. Movimiento e interacción

### Duraciones
| Token | Valor | Uso |
|---|---|---|
| `--motion-fast` | 150ms | Micro-interacciones: color de link, hover de tab, hover de nav |
| `--motion-base` | 250ms | Transiciones de superficie: box-shadow de card, fades |
| `--motion-slow` | 400ms | Entradas y progreso: fill de progress bar, aparición de modal |

### Easing
| Token | Valor | Uso |
|---|---|---|
| `--ease-out` | `ease-out` | Estándar para entradas y hovers (predeterminado) |
| `--ease-in-out` | `cubic-bezier(0.4, 0, 0.2, 1)` | Modales y paneles que entran y salen |

### Comportamientos de interacción
- **Hover de botón:** cambio de fondo según variante (ver §5), sin desplazamiento de layout
- **Active de botón:** `transform: scale(0.98)` — feedback táctil sutil, nunca rebote
- **Hover de card:** solo `box-shadow` (`--shadow-none` → `--shadow-md`) en 250ms; sin escalado ni elevación brusca
- **Progress bar:** `width` en 400ms `ease-out` — el avance siempre se anima, nunca salta
- **Dirección del movimiento:** toda composición y animación fluye **izquierda → derecha** y **abajo → arriba**, replicando la metáfora del avance del isotipo

---

## 7. Don'ts (anti-patrones)

Patrones explícitamente rechazados para Skillia (cada uno citado de revisión real):

**Estética**
- ❌ **Glassmorphism:** sin `backdrop-filter: blur`, vidrio esmerilado ni transparencias superpuestas
- ❌ **Neón:** sin colores fluorescentes, glow ni bordes luminosos sobre fondos oscuros
- ❌ **Tendencias efímeras:** ningún efecto de moda que requiera justificación para existir
- ❌ **Ilustraciones infantiles / mascotas** (estilo Plurall): no aplican al B2B institucional peruano

**Color**
- ❌ Colores hardcodeados fuera de la tabla de tokens (§2)
- ❌ `--accent-100` o `--success-100` en cuerpo de texto (falla WCAG AA)
- ❌ Sombras negras neutras — el color base de toda sombra es `--text-100`
- ❌ Reutilizar `--positive-100/-10` como verde genérico

**Layout**
- ❌ Más de **un CTA primario por sección** del landing (regla Blackboard)
- ❌ `position: fixed` en la plataforma WPLMS — el Course Player tiene su propio sistema de scroll
- ❌ Anidar scroll dentro de scroll en el Course Player
- ❌ Apilar `--surface-100` sobre `--surface-100` sin separador
- ❌ Esquinas redondeadas combinadas con accent en `border-left`/`border-top` (usar `--radius-none`)

**Composición**
- ❌ Rellenar con placeholder, secciones dummy o "data slop" (números/íconos sin función)
- ✅ El espacio vacío es una **señal activa de la marca**: comunica claridad y organización (MIVC §6.3)

---

## Overrides globales requeridos (hacer antes de cualquier componente)

El CSS real del tema trae tres stacks tipográficos que no son de Skillia:
`MasterStudy` (Open Sans + Montserrat), `Elementor kit` (Roboto + Roboto Slab). Reemplazar:

**1. Tipografía**
```
Elementor → Site Settings → Global Fonts
  Typography Primary:   Outfit  / Weight 600
  Typography Secondary: Manrope / Weight 400
  Typography Text:      Manrope / Weight 400
  Typography Accent:    Outfit  / Weight 500

MasterStudy → Theme Options → Typography
  Body font:    Manrope / 16px / 400
  Heading font: Outfit
```

**2. Color**
```
--accent_color:  #385bce → #2563EB   (= --primary-100)
--primary_color: #303441 → #0F172A   (= --text-100)
```
Los valores de Verde Lima y Turquesa ya están correctos en el CSS del tema como `--accent-100` y `--success-100`.

---

*Skillia Design System · v1.1 · fuente de verdad para Claude Design y desarrollo web.*
