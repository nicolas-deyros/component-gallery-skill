# Carbon Design System — Referencia de Componentes

Fuente: https://carbondesignsystem.com/components/overview/
Producto de referencia: IBM Cloud, Watson, productos enterprise de IBM

---

## Filosofía de diseño relevante

Carbon está diseñado para **productos enterprise e industriales** — dashboards
de datos, herramientas de análisis, plataformas cloud. Sus principios:
- **Grid system estricto:** 16 columnas, gutter de 32px (condensed: 16px)
- **Densidad ajustable:** tres modos — Regular · Condensed · Extra condensed
- **Tipografía IBM Plex** como sistema tipográfico propio
- **Datos primero:** los componentes están optimizados para mostrar información compleja

**Escala de spacing:** Múltiplos de 8px base: 2 · 4 · 8 · 12 · 16 · 24 · 32 · 40 · 48 · 64 · 80 · 96 · 160px
(Carbon llama a esto "spacing scale" y la documenta como $spacing-01 a $spacing-13)

---

## Cómo Carbon resuelve los componentes principales

### Button (Carbon)

Carbon tiene **5 tipos** con semántica muy precisa:

| Tipo | Color | Uso |
|---|---|---|
| Primary | Azul (#0F62FE) | La acción más importante. Una por sección. |
| Secondary | Gris oscuro | Acciones secundarias |
| Tertiary | Outline azul | Acciones opcionales |
| Ghost | Solo texto | Acciones de baja prioridad, en toolbars |
| Danger | Rojo | Acciones destructivas — existe en primary y ghost |

**Tamaños — Carbon tiene 5 tamaños formales:**

| Tamaño | Altura |
|---|---|
| Small | 32px |
| Medium | 40px |
| Large | 48px (default) |
| X-Large | 64px |
| 2X-Large | 80px |

**Corner radius:** 0px — Carbon es deliberadamente rectangular (sin border-radius).
Esta es la diferencia visual más notoria vs Material Design.

**Ícono:** siempre a la derecha del label (al contrario de Material que lo pone a la izquierda).

---

### Text Input (Carbon)

Carbon usa label **fijo encima**, nunca flotante. Como Atlassian, es una decisión de accesibilidad.

**Tres tamaños:**
- Small: 32px
- Medium: 40px
- Large: 48px (default)

**Anatomía:**
```
Label text [Optional indicator]
[Input — con placeholder]
[Helper text]
[Invalid text / Warning text]
```

**Particularidad de Carbon:** tiene estado **Warning** además de Error — para
validaciones no críticas que no bloquean el envío del formulario.

---

### Modal (Carbon)

Carbon llama **Composable Modal** al sistema de dialogs.

**Tamaños:**
- Extra Small: 320px
- Small: 480px
- Medium: 640px (default)
- Large: 800px

**Estructura fija:**
- Header con título (y opcional subtítulo)
- Body scrolleable
- Footer con máximo 2 botones
- Botón cerrar (X) siempre en el header

**Alert / Transactional Modal:** Para confirmación de acciones. Requiere input
del usuario (escribir una palabra para confirmar eliminación, por ejemplo).

---

### Notification (Carbon)

Carbon tiene el sistema de notificaciones más completo de los tres DS:

| Tipo | Descripción |
|---|---|
| Inline Notification | Dentro del contenido, contextual |
| Toast Notification | Flotante, esquina, temporal |
| Action Notification | Toast con acción |
| Callout | Estático, informativo, permanente |

**Posición de Toast:** top-right en desktop.
**Auto-dismiss:** configurable pero recomendado para success/info (no para error).

---

### Data Table (Carbon)

El componente más potente y completo de Carbon — diseñado para datos enterprise.

**Features:**
- Sorting por columna
- Filtrado global o por columna
- Selección de filas (con batch actions)
- Expansión de filas (inline detail)
- Toolbar con acciones
- Paginación integrada
- Descarga de datos
- Skeleton loading state

**Densidades:**
- Regular: 48px por fila
- Compact: 32px por fila
- Short: 40px por fila
- Tall: 64px por fila
- Extra tall: 80px por fila

**Filosofía:** Carbon asume que la tabla es el componente central de una aplicación
enterprise, por eso invierte más en ella que cualquier otro DS.

---

### Tag (Carbon)

Carbon usa Tag para categorización y estado. Diferencia con Atlassian Lozenge:
el Tag de Carbon puede ser **interactivo y removible**.

**Tipos:**
- Read-only — solo display
- Selectable — actúa como checkbox/toggle
- Operational — trigger de acciones
- Dismissible — con botón de cierre (X)

**Tamaños:** Small (18px) · Medium (24px) · Large (32px)

---

### Loading (Carbon)

Carbon tiene múltiples estados de loading bien diferenciados:

- **Loading spinner** — operación global, overlay de toda la página o sección
- **Inline Loading** — feedback junto a un button o campo (pequeño spinner + texto)
- **Skeleton** — placeholder de contenido durante carga inicial
- **Progress Bar** — para procesos con progreso medible

**Inline Loading** es característico de Carbon — muy útil para dar feedback
inmediato al hacer click en un botón sin bloquear toda la UI.

```
[Botón enviando...] → [Spinner] Enviando...
[Éxito]             → [Checkmark] Enviado
[Error]             → [X] Error al enviar
```

---

### Accordion (Carbon)

Carbon hace una distinción importante:
- **Flush Accordion** — sin borde lateral, separación solo con líneas horizontales
- **Default Accordion** — con borde izquierdo de acento

El ícono de expand/collapse va a la **derecha** del título (no a la izquierda como
muchas implementaciones por defecto).

---

## Grid System de Carbon

Fundamental para entender el layout de componentes Carbon:

```
16 columnas totales
Gutter default: 32px
Gutter condensed: 16px
Gutter narrow: 8px

Breakpoints:
  sm:  0-671px    → 4 columnas
  md:  672-1055px → 8 columnas
  lg:  1056-1311px → 16 columnas
  xl:  1312-1583px → 16 columnas
  max: 1584px+     → 16 columnas con max-width 1584px
```

---

## Tokens de color clave

```css
/* Carbon color tokens */
--cds-interactive: #0F62FE;          /* Azul IBM — acción principal */
--cds-interactive-hover: #0353E9;    /* Hover */
--cds-danger-01: #DA1E28;            /* Error / Danger */
--cds-warning: #F1C21B;              /* Warning */
--cds-success: #198038;              /* Success */

--cds-text-primary: #161616;         /* Texto principal */
--cds-text-secondary: #525252;       /* Texto secundario */
--cds-text-placeholder: #A8A8A8;     /* Placeholders */
--cds-text-disabled: #C6C6C6;        /* Deshabilitado */

--cds-layer-01: #F4F4F4;            /* Superficie base */
--cds-layer-02: #FFFFFF;            /* Superficie elevada */
--cds-border-strong-01: #8D8D8D;    /* Borde por defecto */
```

**Dark mode en Carbon:** Los tokens cambian de valor pero no de nombre.
`--cds-layer-01` es gris claro en light, gris oscuro en dark.
Esto permite theming completo sin cambiar el código de componentes.

---

## Lo más característico de Carbon vs los otros DS

| Aspecto | Carbon | Material | Atlassian |
|---|---|---|---|
| Border radius | 0px (rectangular) | Grande (20px en buttons) | Pequeño (3px) |
| Densidad | Alta / ajustable | Media | Alta |
| Foco principal | Datos / Enterprise | Mobile / Consumer | Productividad |
| Animaciones | Mínimas | Expresivas | Mínimas |
| Ícono en button | Derecha | Izquierda | Derecha |
| Label de input | Siempre fijo | Flotante | Siempre fijo |
