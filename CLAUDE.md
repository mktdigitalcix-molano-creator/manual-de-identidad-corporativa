# CLAUDE.md — Skillia LMS
> Fuente de verdad para desarrollo local y colaboración con IA (Claude, Copilot, etc.)
> Última actualización: 2026-06

---

## Contexto del proyecto

**Skillia** es una plataforma LMS B2B para instituciones educativas peruanas (colegios, institutos, universidades). El modelo de negocio es membresía anual por institución.

### Stack principal
| Capa | Tecnología |
|---|---|
| CMS / LMS | WordPress + MasterStudy Theme (Pro) + WPLMS |
| Dev local | LocalWP |
| Automatización | n8n (motor de flujos, crons, pipelines) |
| Base de datos externa | Baserow (tabla `usuarios`, tabla `formes`) |
| IA conversacional | Flowise (widget web embed + WhatsApp bot vía n8n) |
| Vector store | Qdrant (contexto de aprendizaje por alumno) |
| Gamificación | GamiPress (puntos y rankings en WPLMS) |
| Analítica interna | Metabase (dashboard equipo Skillia) |
| Email marketing | Brevo (secuencias de reactivación) |
| Videollamadas | Zoom (integración nativa WPLMS) |
| Control de versiones | Git + GitHub (este repo) |

### Para qué sirve
- Gestión de cursos asignados por institución (no marketplace público)
- Onboarding automatizado de alumnos vía Asistente Personal + n8n pipeline SKL-01
- Tutoría inteligente 24/7: Flowise en web + WhatsApp bot, misma fuente de verdad en Baserow
- Analítica de retención: score de riesgo de deserción con umbrales de intervención automática
- Reportes de rendimiento para coordinadores e instituciones

### Lo que NO forma parte del MVP
- WooCommerce (excluido explícitamente — ver Flujo de trabajo v4.0)
- Registro público / auto-inscripción de alumnos
- AI Lab de MasterStudy (solo disponible en Pro Plus, no incluido en la licencia actual)
- Reports & Analytics nativos de MasterStudy (ídem, solo Pro Plus)

---

## Convenciones

### Tipografía
- **Principal (títulos, CTAs):** Outfit — Bold para títulos, Semi Bold para navegación y subtítulos
- **Secundaria (cuerpo):** Manrope — Regular para párrafos, Medium para etiquetas

### Paleta de colores — tokens oficiales
```
Verde Lima      #84CC16   → USO: CTAs únicamente. Nunca decorativo neutral.
Turquesa        #14B8A6   → USO: progreso medio, highlights secundarios
Azul            #2563EB   → USO: acciones primarias, links, barra 3 del isotipo
Azul Medianoche #0F172A   → USO: cuerpo de texto, fondos oscuros
Ámbar Motivador #F59E0B   → USO: alertas, badges de logro
Gris Glaciar    #F1F5F9   → USO: fondos de sección, cards
Blanco          #FFFFFF   → USO: fondo principal
```

> ⚠️ ACCESIBILIDAD: `#84CC16` y `#14B8A6` NO pasan WCAG 2.1 AA para texto de cuerpo.
> Usar SOLO para elementos decorativos, íconos o texto grande (>18px bold). Nunca para párrafos.

### Mapeo paleta → MasterStudy Theme Options
> [PENDIENTE] Definir qué color Skillia va en cada campo de Theme Options > General:
> - Main color → `[PENDIENTE]`
> - Secondary color → `[PENDIENTE]`
> - Accent (Course Player) → `[PENDIENTE]`
> - Danger → `[PENDIENTE]`
> - Success → `[PENDIENTE]`

### Header
- Estilo seleccionado: `[PENDIENTE — elegir entre: Online Courses / Academy / Distance Learning]`
- Logo: imagotipo completo (isotipo + wordmark "Skillia")
- Logo blanco: versión sobre fondos oscuros requerida por Theme Options > General
- Top Bar: habilitar redes sociales (Instagram, TikTok, YouTube, WhatsApp Business)
- Login/Register: enlazados a la página LMS custom `[PENDIENTE — definir URL]`

### Naming de páginas y templates
> [PENDIENTE] Definir convención de naming para:
> - Page templates custom del child theme
> - Shortcodes reutilizables
> - Ejemplo sugerido: `page-[rol]-[funcion]` → `page-alumno-dashboard`, `page-admin-activacion`

### CSS y child theme
> [PENDIENTE] Definir si se usa:
> - Solo Theme Options (sin CSS custom)
> - Child theme con `style.css` propio
> - Hoja de estilos adicional vía wp_enqueue_scripts

---

## Patrones prohibidos

### Marca
- ❌ No usar "alumno" ni "estudiante" → usar "tú" en comunicación directa
- ❌ No usar "fácil" → usar "claro"
- ❌ No usar "fracaso" → usar "intento"
- ❌ Verde Lima (`#84CC16`) como color decorativo neutro → solo para acciones (botones, CTAs, progreso)
- ❌ No saturar layouts → el espacio vacío es parte de la identidad de marca

### Desarrollo
- ❌ No activar WooCommerce en ningún entorno (excluido del MVP)
- ❌ No hardcodear colores fuera de los tokens definidos arriba
- ❌ No usar `!important` en CSS custom sin documentar el motivo
- ❌ No crear roles WordPress ad-hoc sin actualizar la tabla de roles (ver sección Roles)
- ❌ No llamar endpoints de n8n directamente desde frontend — siempre vía REST API Bridge

---

## Comandos

### Entorno local (LocalWP)
```bash
# Sitio local levantado con LocalWP — no requiere comandos manuales
# Acceso: http://skillia.local  [PENDIENTE — confirmar dominio local]
# Admin WP: http://skillia.local/wp-admin

# Acceder a la terminal del sitio desde LocalWP > Open Site Shell
```

### Git / GitHub (desde VS Code terminal)
```bash
# Primer push del repo (una sola vez)
git init
git add .
git commit -m "feat: initial commit — CLAUDE.md Skillia"
git branch -M main
git remote add origin https://github.com/[TU_USUARIO]/[NOMBRE_REPO].git
git push -u origin main

# Flujo diario
git add .
git commit -m "tipo: descripción corta del cambio"
git push

# Tipos de commit recomendados:
# feat:     nueva funcionalidad
# fix:      corrección de bug
# docs:     cambios en documentación
# style:    cambios visuales sin lógica
# config:   cambios en configuración WP/plugins
```

### Build / Lint / Tests
> [PENDIENTE] Definir si el proyecto usa:
> - npm / yarn para assets (scripts, estilos del child theme)
> - WP-CLI para comandos de administración desde terminal
> - Alguna herramienta de lint para PHP/CSS

---

## Roles y permisos

### Roles Skillia vs. roles WordPress/WPLMS
| Rol Skillia | Rol WordPress equivalente | Permisos clave |
|---|---|---|
| Alumno | Student (WPLMS) | Ver cursos asignados, acceder a Flowise widget, ver puntos GamiPress |
| Docente / Instructor | Instructor (WPLMS) | Crear y editar contenido de cursos, ver progreso de alumnos |
| Coordinador | `[PENDIENTE]` | Ver reportes, gestionar grupos de alumnos |
| Asistente Personal (AP) | `[PENDIENTE]` | Acceso al mini-panel n8n para activación manual de alumnos |
| Admin Skillia | Administrator | Acceso total, configuración de plataforma |
| Admin Institución | `[PENDIENTE]` | Ver dashboards de su institución en Metabase |

> ⚠️ Activar "Restrict instructors from accessing the admin panel" en LMS Settings > General
> para que Instructores y roles limitados sean redirigidos a sus páginas de cuenta.

---

## Reglas para estados de UI

Todo componente interactivo debe manejar estos 4 estados mínimos:

### Estado vacío (empty)
- Alumno sin cursos asignados → mostrar mensaje + contacto con AP, NO pantalla en blanco
- Dashboard sin actividad → mostrar onboarding step (curso inicial de bienvenida)
- Flowise widget sin historial → saludo personalizado con nombre del alumno

### Estado de carga (loading)
- Habilitar "Loading animation" en LMS Settings > General para páginas LMS
- Para respuestas de Flowise: mostrar indicador de escritura ("está escribiendo...")
- Para crons n8n: no bloquear UI — procesos en background, notificar por WhatsApp al completar

### Estado de error (error)
- REST API Bridge caído: mostrar mensaje genérico, NO exponer detalles del endpoint
- Flowise no disponible: redirigir a WhatsApp bot como canal alternativo
- Score de riesgo no calculable (datos incompletos): tratar como score 0, no mostrar error al alumno

### Estado crítico / overflow (score de deserción)
| Score | Estado UI visible para alumno | Acción automática backend |
|---|---|---|
| 0–7 | Normal, sin cambios | — |
| >7 | Nudge motivacional sutil en dashboard | WhatsApp: tip del día + recordatorio de meta |
| >15 | — (invisible para alumno) | Secuencia Brevo: email día 3/7/14 |
| >25 | — (invisible para alumno) | Alerta Metabase equipo + reporte a institución |

---

## Integraciones externas

### n8n — Pipeline SKL-01
> [PENDIENTE] Documentar:
> - URL del webhook de activación: `https://n8n.skilliaeducation.com/form/activar-alumno`
> - Estructura del payload que envía el formulario del AP
> - Variables de entorno requeridas en n8n

### Baserow
> [PENDIENTE] Documentar:
> - URL de la instancia
> - Nombre exacto de tablas: `usuarios`, `formes` (confirmar nombres reales)
> - Campos clave de tabla `usuarios`: nombre, email, institución, curso_actual, puntos, etapa (`nuevo` / `activo`)
> - Token de API y cómo está almacenado (variable de entorno, no hardcodeado)

### Flowise
> [PENDIENTE] Documentar:
> - URL del endpoint del chatflow
> - Snippet de embed para WPLMS (dónde se inserta en el tema)
> - Conexión con Qdrant: nombre del collection, embedding model usado

### Qdrant
> [PENDIENTE] Documentar:
> - URL de la instancia
> - Nombre del collection de contexto de aprendizaje
> - Proceso de indexación de nuevo contenido de curso

### REST API Bridge (WPLMS ↔ n8n)
> [PENDIENTE] Documentar:
> - Endpoint base
> - Autenticación (API key, bearer token)
> - Eventos que disparan el bridge: creación de perfil, progreso de lección, quiz completado

---

## Configuración MasterStudy (checklist de setup inicial)

### Theme Options > General
- [ ] Subir Site Logo (imagotipo color)
- [ ] Subir White-text Logo (imagotipo blanco)
- [ ] Definir Main color y Secondary color con paleta Skillia

### Theme Options > Header
- [ ] Seleccionar estilo de header
- [ ] Configurar Top Bar: teléfono, redes sociales
- [ ] Habilitar/deshabilitar Login/Register según flujo (alumnos no se auto-registran)

### LMS Settings > General
- [ ] Activar "Restrict instructors from accessing the admin panel"
- [ ] Configurar Course Builder Font Family → Outfit
- [ ] Activar Loading animation

### Plugins activos requeridos
- [ ] MasterStudy LMS (Pro — incluido con el tema)
- [ ] GamiPress + GamiPress WPLMS Integration
- [ ] Zoom (integración nativa WPLMS)
- [ ] `[PENDIENTE]` Plugin para embed de Flowise widget

---

## Referencias del proyecto

| Documento | Ubicación |
|---|---|
| Flujo de trabajo v4.0 | `/docs/Flujo_de_trabajo_v4_0.pdf` |
| Manual de Marca | `/docs/Manual_de_Marca.pdf` |
| Manual de Identidad Visual Corporativa | `/docs/Manual_de_Identidad_Visual_Corporativa.pdf` |
| BMC Skillia v2.0 | `/docs/BMC_SkillIA_v2_0.pdf` |
| Docs MasterStudy Theme | https://docs.stylemixthemes.com/masterstudy-theme-documentation |
| Docs MasterStudy LMS | https://docs.stylemixthemes.com/masterstudy-lms |
| Demo template referencia | https://masterstudy.stylemixthemes.com/lms-plugin/template-university/ |
