# Material Design — Referencia de Componentes

Fuente: https://m3.material.io/components
Versión de referencia: Material Design 3 (M3 / Material You)

---

## Filosofía de diseño relevante para componentes

Material Design usa **elevation** (elevación) como metáfora central. Los componentes
flotantes (dialogs, menus, tooltips) tienen sombras que indican su nivel en el stack.
En M3, la elevación se expresa con **color tonal** además de sombra — los contenedores
elevados toman un tinte del color primario.

**Tokens de spacing:** Material usa una escala base de 4dp.
Valores más comunes: 4 · 8 · 12 · 16 · 24 · 32 · 48 · 64dp

**Tipografía:** Sistema de roles tipográficos (Display · Headline · Title · Body · Label)
en lugar de tamaños fijos. Cada componente usa un rol específico.

---

## Cómo Material resuelve los componentes principales

### Button (Material)

Material define **5 variantes explícitas** con jerarquía clara:

| Variante | Uso | Estilo visual |
|---|---|---|
| Filled | Acción más importante | Fondo color primario sólido |
| Filled Tonal | Acción secundaria importante | Fondo tonal (secundario) |
| Outlined | Acción media importancia | Borde, sin fondo |
| Text | Acción baja importancia | Solo texto, sin borde |
| Elevated | Acción con énfasis en superficie | Sombra leve, sin relleno fuerte |

**Corner radius:** 20dp (totalmente redondeado — "full" en Tailwind)
**Height:** 40dp fijo
**Horizontal padding:** 24dp (con ícono: 16dp leading, 24dp trailing)
**Gap ícono-label:** 8dp

**Inspiración para implementación:**
```css
/* Filled button — Material 3 */
.btn-filled {
  background-color: var(--md-sys-color-primary);
  color: var(--md-sys-color-on-primary);
  border-radius: 20px;
  height: 40px;
  padding: 0 24px;
  /* State layer: pseudoelemento con opacity para hover/pressed */
}
.btn-filled:hover::before {
  background-color: var(--md-sys-color-on-primary);
  opacity: 0.08; /* hover state layer */
}
```

---

### Text Field (Material)

Material ofrece **dos variantes**:
- **Filled** — con fondo de color, underline en la base
- **Outlined** — borde completo, más claro visualmente

**Label flotante:** El label se anima desde dentro del campo (placeholder-like)
hacia arriba al hacer focus o cuando hay valor. Controversial desde perspectiva
de accesibilidad — muchos equipos prefieren label fijo superior.

**Supporting text:** Siempre debajo del campo. Error reemplaza el helper text.
**Leading/Trailing icons:** 48dp de área de toque mínima para iconos interactivos.

---

### Dialog (Material)

Material distingue:
- **Basic Dialog** — contenido libre, botones de texto al pie
- **Full-screen Dialog** — mobile, para formularios complejos
- **Alert Dialog** — confirmación, máximo 2 acciones

**Dimensiones desktop:** ancho mínimo 280dp, máximo 560dp
**Corner radius:** 28dp (containers en M3 son muy redondeados)
**Botones:** alineados a la derecha, acción principal a la derecha del todo

---

### Navigation (Material)

| Componente | Cuándo | Items |
|---|---|---|
| Navigation Bar (bottom) | Mobile, 3-5 destinos top-level | 3–5 |
| Navigation Rail | Tablet, modo landscape | 3–7 |
| Navigation Drawer | Desktop o cuando hay muchos destinos | Ilimitado |

**Bottom Nav:** altura 80dp, iconos de 24dp, label siempre visible (no solo en activo).

---

### Chips (Material)

Material tiene **4 tipos de chips** bien diferenciados:

| Tipo | Uso |
|---|---|
| Assist | Acciones inteligentes sugeridas |
| Filter | Filtrado de contenido (toggle) |
| Input | Representar input del usuario (removible) |
| Suggestion | Sugerencias de autocompletado |

**No usar chips como badges** — Material los ve como elementos interactivos.

---

### Snackbar (Material)

- Una sola línea de texto (máximo 2 en mobile)
- Máximo una acción (texto, no ícono)
- Auto-dismiss: 4 segundos mínimo, 10 segundos máximo
- No apilar — solo uno a la vez
- Posición: bottom-center en mobile, bottom-left en desktop

---

### FAB — Floating Action Button

Exclusivo de Material (otros design systems no lo tienen como patrón oficial).
Representa **la acción más importante y frecuente** de la pantalla.

Tamaños en M3:
- Small FAB: 40dp
- FAB: 56dp (estándar)
- Large FAB: 96dp
- Extended FAB: ancho variable, con label

**Regla:** Una sola FAB por pantalla. No usarla para acciones destructivas.

---

## Tokens de color — Sistema M3

M3 usa roles de color en lugar de colores directos:

| Token | Descripción |
|---|---|
| `primary` | Color principal de la marca |
| `on-primary` | Texto/iconos sobre primary |
| `primary-container` | Superficie con tinte primary (menos énfasis) |
| `on-primary-container` | Contenido sobre primary-container |
| `surface` | Superficie base de la UI |
| `surface-variant` | Superficie alternativa |
| `outline` | Bordes y divisores |
| `error` | Estados de error |

Este sistema de roles permite theming automático y dark mode sin reescribir
los componentes — solo cambian los valores de los tokens.
