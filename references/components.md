# Referencia de Componentes — component.gallery

Fuente base: https://component.gallery/components/
Esta lista se complementa con fetch dinámico en tiempo de ejecución.

---

## Índice de componentes

### Acciones
- [Button](#button)
- [Icon Button](#icon-button)
- [Button Group](#button-group)
- [Toggle Button](#toggle-button)
- [Split Button](#split-button)
- [Floating Action Button](#floating-action-button)

### Formularios
- [Input / Text Field](#input--text-field)
- [Textarea](#textarea)
- [Select / Dropdown Select](#select--dropdown-select)
- [Combobox](#combobox)
- [Checkbox](#checkbox)
- [Radio Button](#radio-button)
- [Switch / Toggle](#switch--toggle)
- [Slider / Range](#slider--range)
- [Date Picker](#date-picker)
- [File Upload](#file-upload)
- [Search](#search)
- [Form](#form)

### Navegación
- [Navigation Bar / Navbar](#navigation-bar--navbar)
- [Sidebar / Nav Drawer](#sidebar--nav-drawer)
- [Tabs](#tabs)
- [Breadcrumb](#breadcrumb)
- [Pagination](#pagination)
- [Stepper / Progress Steps](#stepper--progress-steps)
- [Link](#link)
- [Menu / Context Menu](#menu--context-menu)

### Overlays y feedback
- [Modal / Dialog](#modal--dialog)
- [Tooltip](#tooltip)
- [Popover](#popover)
- [Toast / Snackbar](#toast--snackbar)
- [Alert / Banner](#alert--banner)
- [Loading Spinner](#loading-spinner)
- [Skeleton Loader](#skeleton-loader)
- [Progress Bar](#progress-bar)

### Contenido
- [Card](#card)
- [Accordion / Disclosure](#accordion--disclosure)
- [Table](#table)
- [List](#list)
- [Avatar](#avatar)
- [Badge / Tag / Chip](#badge--tag--chip)
- [Empty State](#empty-state)
- [Image](#image)
- [Divider / Separator](#divider--separator)
- [Carousel](#carousel)
- [Tree / Tree View](#tree--tree-view)
- [Rating](#rating)
- [File Attachment](#file-attachment)

### Layout
- [Header](#header)
- [Footer](#footer)
- [Segmented Control](#segmented-control)
- [Rich Text Editor](#rich-text-editor)

---

## Componentes detallados

### Button

**Nombres alternativos:** Action, CTA, Submit Button

**Cuándo usarlo:** Acción principal o secundaria que el usuario puede ejecutar.

**Variantes:**
- Primary — acción principal de la pantalla (una sola por vista)
- Secondary / Outlined — acción alternativa
- Ghost / Text — acción de baja prioridad
- Destructive / Danger — acciones irreversibles (eliminar, cancelar plan)
- Icon + Label — cuando el ícono refuerza la acción
- Loading — mientras procesa (reemplazar label con spinner)

**Estados:** Default · Hover · Focus · Active · Disabled · Loading

**Tamaños estándar:** sm (32px) · md (40px) · lg (48px)

**Accesibilidad:**
- Usar `<button type="button">` o `<button type="submit">` según contexto
- Nunca usar `<div>` o `<a>` para acciones sin navegación
- Estado disabled: `disabled` attribute (no solo clase CSS)
- Loading: `aria-busy="true"` + `aria-label` actualizado

---

### Icon Button

**Nombres alternativos:** Icon Action, Ghost Icon

**Cuándo usarlo:** Acción representada solo por ícono (cerrar, editar, eliminar en tablas).

**Reglas:**
- SIEMPRE incluir `aria-label` descriptivo
- Tamaño mínimo de área de toque: 44×44px (WCAG 2.5.5)
- El ícono en sí puede ser más pequeño (24px), el padding completa el área

---

### Button Group

**Nombres alternativos:** Segmented Control, Toggle Group, Toolbar

**Cuándo usarlo:** Opciones mutuamente excluyentes (vista lista/grilla, alineación de texto).

**Reglas:**
- Un solo elemento activo a la vez (comportamiento radio)
- O múltiples activos (comportamiento checkbox) — documentar cuál es
- `role="group"` con `aria-label` en el contenedor

---

### Input / Text Field

**Nombres alternativos:** Text Input, Form Field, Input Field

**Variantes:**
- Default
- With label (flotante o fija — preferir fija por accesibilidad)
- With helper text
- With character count
- With icon (leading / trailing)
- Error state
- Success state
- Disabled / Read-only

**Anatomía obligatoria:**
```
[Label]
[Leading icon?] [Input] [Trailing icon?] [Clear button?]
[Helper text / Error message]
```

**Accesibilidad:**
- `<label>` siempre asociado con `for` / `id` o `aria-label`
- Error: `aria-describedby` apuntando al mensaje de error + `aria-invalid="true"`
- Nunca usar `placeholder` como reemplazo de `label`

---

### Select / Dropdown Select

**Nombres alternativos:** Dropdown, Picker, Listbox

**Cuándo usarlo:** 5 o más opciones. Para menos de 5 opciones, considerar Radio Buttons.

**Regla de oro:** Si las opciones son menos de 3, usar Radio. Entre 3 y 5, depende del espacio. Más de 5, usar Select.

---

### Combobox

**Nombres alternativos:** Autocomplete, Typeahead, Search Select

**Cuándo usarlo:** Select con búsqueda integrada o creación de opciones nuevas.

**Diferencia con Select:** El usuario puede tipear para filtrar. Puede permitir valores no listados.

**Accesibilidad:** Patrón ARIA Combobox — uno de los más complejos. Referirse a WAI-ARIA Authoring Practices.

---

### Checkbox

**Cuándo usarlo:** Selección múltiple independiente. O una sola opción booleana (acepto términos).

**Estados especiales:**
- Indeterminate — cuando es padre de checkboxes hijos, algunos seleccionados y otros no
- `aria-checked="mixed"` para el estado indeterminate

---

### Switch / Toggle

**Nombres alternativos:** Toggle, On/Off Switch

**Cuándo usarlo:** Activar/desactivar una configuración con efecto inmediato (sin Submit).
Diferencia con Checkbox: el Switch tiene efecto inmediato. El Checkbox requiere enviar el formulario.

**Accesibilidad:** `role="switch"` + `aria-checked="true/false"`

---

### Modal / Dialog

**Nombres alternativos:** Dialog, Overlay, Lightbox, Popup

**Tipos:**
- Modal — bloquea interacción con el fondo (requiere acción del usuario)
- Non-modal / Drawer — no bloquea, el fondo sigue siendo interactivo
- Alert Dialog — confirmación de acción destructiva (requiere respuesta)
- Full-screen dialog — en mobile para formularios complejos

**Reglas de implementación:**
- Usar elemento nativo `<dialog>` cuando sea posible
- Focus trap: el foco debe quedar atrapado dentro del modal mientras está abierto
- Al cerrar: devolver foco al elemento que abrió el modal
- Escape cierra el modal
- `aria-modal="true"` + `aria-labelledby` apuntando al título
- Overlay con `z-index` según la escala documentada en SKILL.md

---

### Tooltip

**Cuándo usarlo:** Información adicional sobre un elemento al hacer hover/focus.
**NO usarlo para:** Información crítica (no visible en mobile), acciones, contenido extenso.

**Accesibilidad:**
- Debe ser accesible por teclado (no solo hover)
- `role="tooltip"` + `aria-describedby` en el elemento disparador
- Delay de aparición: 300-500ms (evitar parpadeo al mover el cursor)

---

### Toast / Snackbar

**Nombres alternativos:** Notification, Flash Message, Alert Toast

**Variantes:** Success · Error · Warning · Info · Loading

**Reglas:**
- Posición: esquina inferior derecha (desktop) o inferior centrado (mobile)
- Auto-dismiss: 4-6 segundos para mensajes informativos. Nunca para errores.
- Máximo 3 toasts simultáneos — hacer queue
- `role="status"` (informativos) o `role="alert"` (errores/acciones requeridas)
- `aria-live="polite"` para informativos, `aria-live="assertive"` para errores

---

### Alert / Banner

**Nombres alternativos:** Callout, Notice, Notification Banner, Inline Alert

**Diferencia con Toast:** El Alert es estático y está integrado en el layout.
El Toast es flotante y temporal.

**Variantes:** Info · Success · Warning · Error
**Con o sin:** ícono · título · acción · botón de cierre

---

### Card

**Nombres alternativos:** Tile, Panel, Item Card, Content Card

**Variantes:**
- Basic — solo contenedor con sombra/borde
- Interactive — clickeable (toda la card es un link o button)
- With media — imagen + contenido
- Horizontal — imagen lateral + contenido
- With actions — botones en el footer

**Reglas:**
- Si toda la card es clickeable: `<a>` o `<button>` como wrapper, no `<div>` con `onClick`
- Si tiene múltiples acciones: no anidar `<a>` dentro de `<a>`

---

### Accordion / Disclosure

**Nombres alternativos (fuente: component.gallery):** Arrow toggle · Collapse · Collapsible sections · Collapsible · Details · Disclosure · Expandable · Expander · ShowyHideyThing

**Cuándo usarlo:** Contenido que el usuario puede necesitar o no — FAQ, filtros, secciones secundarias.

**Advertencia de uso:** Al usar un accordion estás ocultando contenido. No usar para información esencial que el usuario siempre necesita ver.

**Modo exclusivo vs múltiple:**
- Exclusivo (solo un item abierto a la vez): implementar con cuidado — algunos usuarios quieren comparar contenido de dos ítems simultáneamente
- Múltiple (varios abiertos): es el comportamiento más flexible y accesible

**Implementación nativa (progresivamente mejorada):**
```html
<!-- Opción 1: HTML puro con <details> — sin JS necesario -->
<details>
  <summary>Título del panel</summary>
  <div>Contenido expandible</div>
</details>

<!-- Opción 2: Con JS para control total de ARIA -->
<div>
  <button aria-expanded="false" aria-controls="panel-1">Título</button>
  <div id="panel-1" hidden>Contenido</div>
</div>
```

**Nota sobre `<details>`:** Si JS está deshabilitado y el contenido usa un `<button>` para toggle, el usuario no puede acceder al contenido. Preferir `<details>/<summary>` como base y mejorar con JS.

**Accesibilidad:**
- `aria-expanded="true/false"` en el trigger (si no se usa `<details>`)
- `aria-controls` apuntando al panel
- El panel colapsado debe tener `hidden` o `display: none` (no solo `height: 0`)
- Navegación con teclado: Enter/Space para toggle, flechas para navegar entre items

---

### Tabs

**Cuándo usarlo:** Contenido relacionado dividido en secciones, donde solo una se muestra a la vez.
**NO usarlo para:** Navegación entre páginas (usar links), pasos de un proceso (usar Stepper).

**Accesibilidad:**
- `role="tablist"` en el contenedor
- `role="tab"` en cada pestaña
- `role="tabpanel"` en cada panel
- Navegación con flechas de teclado entre tabs (no Tab key)

---

### Badge / Tag / Chip

**Nombres alternativos:** Label, Pill, Lozenge (Atlassian), Tag

**Diferencias:**
- Badge — número o indicador de estado (notificaciones, status)
- Tag / Chip — categoría o metadato (puede ser removible)
- Lozenge — estado de un item (Atlassian terminology)

**Tamaño:** Nunca menor a 20px de alto. Padding horizontal mínimo 8px.

---

### Skeleton Loader

**Nombres alternativos:** Placeholder, Loading Skeleton, Ghost Loader

**Cuándo usarlo:** Mientras carga contenido de forma asíncrona.
**Regla:** El skeleton debe imitar la forma del contenido real (mismas proporciones).

**Accesibilidad:**
- `aria-busy="true"` en el contenedor mientras carga
- `aria-label="Cargando..."` o región live que anuncie cuando termina

---

### Table

**Variantes:**
- Basic — solo datos, sin interacción
- Sortable — columnas con orden ascendente/descendente
- Selectable — filas con checkbox
- With actions — acciones por fila (editar, eliminar)
- Expandable rows — filas con detalle colapsable
- Sticky header — encabezado fijo al hacer scroll
- Responsive — colapsa a cards en mobile

**Accesibilidad:**
- `<table>`, `<thead>`, `<tbody>`, `<th scope="col/row">` — nunca divs
- `aria-sort="ascending/descending/none"` en columnas ordenables
- Caption descriptivo con `<caption>` o `aria-label`

---

### Breadcrumb

**Accesibilidad:**
- `<nav aria-label="Breadcrumb">` como contenedor
- Lista `<ol>` (orden importa)
- Último item: `aria-current="page"`
- Separador decorativo: `aria-hidden="true"`

---

### Pagination

**Variantes:**
- Numbered — lista de páginas
- Previous/Next — sin números
- Load more — botón de carga
- Infinite scroll — automático

**Accesibilidad:**
- `<nav aria-label="Paginación">` como contenedor
- Página actual: `aria-current="page"`

---

### Loading Spinner

**Nombres alternativos:** Spinner, Activity Indicator, Loader, Throbber

**Cuándo usarlo:** Operación de duración desconocida. Para duración conocida, usar Progress Bar.

**Tamaños:** sm (16px) · md (24px) · lg (40px)

**Accesibilidad:**
- `role="status"` + `aria-label="Cargando"`
- El texto "Cargando" puede estar visualmente oculto (`sr-only`)

---

### Empty State

**Nombres alternativos:** Zero State, Blank State

**Anatomía:**
- Ilustración o ícono (opcional pero recomendado)
- Título descriptivo
- Descripción con contexto
- CTA principal (qué puede hacer el usuario)

**Regla:** El empty state debe explicar POR QUÉ está vacío y QUÉ hacer al respecto.

---

### Navigation Bar / Navbar

**Variantes:**
- Top navigation (desktop)
- Bottom navigation (mobile — max 5 items)
- Sidebar navigation (desktop, contenido denso)

**Accesibilidad:**
- `<nav aria-label="Principal">` (o el nombre que corresponda)
- Item activo: `aria-current="page"`
- Menús desplegables: patrón disclosure o menú ARIA

---

### Divider / Separator

**Nombres alternativos:** Rule, Horizontal Rule, Section Divider

**Uso:** Separación visual entre secciones. No abusar — preferir espaciado (gap/margin) primero.

**Accesibilidad:**
- `<hr>` para separadores semánticos
- `role="separator"` si es un div
- Decorativo puro: `aria-hidden="true"`

---

### Carousel

**Nombres alternativos (fuente: component.gallery):** Slider, Slideshow, Image Gallery, Content Rotator

**Cuándo usarlo:** Mostrar múltiples slides de contenido, uno o más a la vez. Navegación por swipe, scroll o botones.

**Advertencia de uso:** Los carousels tienen tasas de interacción muy bajas — considerar si el contenido realmente necesita este patrón o si puede mostrarse de otra forma (grid, lista).

**Accesibilidad:**
- `role="region"` + `aria-label="Galería de imágenes"` en el contenedor
- Botones prev/next con `aria-label` descriptivo
- Autoplay desactivado por defecto. Si existe, proveer botón de pausa visible
- `aria-live="polite"` para anunciar cambios de slide

---

### Tree / Tree View

**Nombres alternativos (fuente: component.gallery):** Tree, Directory, Nested list, File tree

**Cuándo usarlo:** Información jerárquica anidada — table of contents, explorador de archivos, menús multinivel.

**Accesibilidad:**
- `role="tree"` en el contenedor, `role="treeitem"` en cada nodo
- Nodos con hijos: `aria-expanded="true/false"`
- Navegación con flechas: derecha expande, izquierda colapsa o sube al padre

---

### Rating

**Nombres alternativos (fuente: component.gallery):** Star Rating, Rating Bar

**Cuándo usarlo:** Permitir al usuario ver y/o establecer una calificación por estrellas.

**Variantes:**
- Read-only — solo display
- Interactive — el usuario puede seleccionar valor
- Half-stars — permite medios puntos

**Accesibilidad:**
- Implementar como grupo de radio buttons cuando es interactivo
- `role="radiogroup"` + `aria-label="Calificación"` en el contenedor
- Cada estrella: `<input type="radio">` con `aria-label="X estrellas"`

---

### File Attachment

**Nombres alternativos (fuente: component.gallery):** File, Attachment, Document chip

**Cuándo usarlo:** Representar un archivo adjunto o descargable — distinto del File Upload (que es el input para subir).

**Anatomía:**
- Ícono del tipo de archivo
- Nombre del archivo
- Tamaño (opcional)
- Acción: descargar / eliminar (si es removible)

---

### Segmented Control

**Nombres alternativos (fuente: component.gallery):** Button Group toggle, Tab Bar, Toggle Group

**Cuándo usarlo:** Alternar entre opciones o vistas mutuamente excluyentes. Híbrido entre Button Group, Radio Buttons y Tabs.

**Diferencia con Tabs:** El Segmented Control cambia el estado de la vista actual. Las Tabs cambian el contenido mostrado.

**Diferencia con Radio Buttons:** Visual más compacto, generalmente sin label externo.

**Accesibilidad:**
- `role="group"` + `aria-label` en el contenedor
- Cada opción actúa como radio: una sola activa a la vez
- La opción activa: `aria-pressed="true"` o `aria-checked="true"`

---

### Rich Text Editor

**Nombres alternativos (fuente: component.gallery):** WYSIWYG Editor, RTE, Text Editor

**Cuándo usarlo:** Edición de contenido con formato (bold, italic, listas, links, imágenes).

**Advertencia:** Implementar un RTE desde cero es extremadamente complejo. En proyectos reales usar librerías probadas: Tiptap, Quill, ProseMirror, Slate.js.

**Consideraciones de accesibilidad:**
- El área editable debe tener `role="textbox"` + `aria-multiline="true"`
- La toolbar: `role="toolbar"` + `aria-label="Opciones de formato"`
- Cada botón de formato: `aria-pressed="true/false"` para estados toggle

---

### Header

**Nombres alternativos (fuente: component.gallery):** Site Header, Top Bar, App Bar (Material)

**Cuándo usarlo:** Elemento que aparece en la parte superior de todas las páginas. Contiene nombre del sitio, navegación principal, y acciones globales (búsqueda, perfil).

**Reglas:**
- `<header>` semántico como elemento raíz
- Debe contener `<nav>` si tiene links de navegación
- Sticky o fixed: documentar el z-index (ver escala en SKILL.md)

---

### Footer

**Nombres alternativos (fuente: component.gallery):** Site Footer, Bottom Bar

**Cuándo usarlo:** Parte inferior de la página — copyright, links legales, links a contenido relacionado.

**Reglas:**
- `<footer>` semántico como elemento raíz
- No usar para navegación principal — solo links secundarios y legales
