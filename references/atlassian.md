# Atlassian Design System — Referencia de Componentes

Fuente: https://atlassian.design/components
Productos de referencia: Jira, Confluence, Trello, Bitbucket

---

## Filosofía de diseño relevante

Atlassian DS está diseñado para **aplicaciones de productividad densas** — mucho
contenido, muchas acciones, usuarios expertos. Sus decisiones priorizan:
- **Densidad de información** sobre espaciado generoso
- **Claridad funcional** sobre expresividad visual
- **Consistencia entre productos** (Jira + Confluence + Bitbucket comparten el mismo DS)

**Escala de spacing:** 4px base. Valores: 2 · 4 · 6 · 8 · 12 · 16 · 20 · 24 · 32 · 40 · 48px

**Tokens de color:** Sistema semántico con roles: brand, neutral, blue, green, yellow, red, purple, teal

---

## Cómo Atlassian resuelve los componentes principales

### Button (Atlassian)

Atlassian tiene **6 apariencias** (llaman "appearance", no "variant"):

| Appearance | Uso |
|---|---|
| Primary | Acción más importante. Una por formulario/vista. |
| Default | Acciones secundarias. El más usado. |
| Subtle | Acciones terciarias, baja jerarquía |
| Link | Cuando el botón se comporta como link |
| Warning | Acciones que requieren precaución |
| Danger | Acciones destructivas |

**Spacing:** padding horizontal 12px (compact) o 16px (default). Height 32px (compact) o 40px (default).
**Corner radius:** 3px — característicamente cuadrado comparado con Material.
**Filosfía:** Los botones de Atlassian son deliberadamente "tranquilos" — no compiten con el contenido.

---

### Lozenge (Badge de estado — exclusivo de Atlassian)

El **Lozenge** es el componente más característico de Atlassian. Representa
el **estado de un item** (issue de Jira, PR de Bitbucket, etc.).

| Appearance | Color | Uso |
|---|---|---|
| Default | Gris | Estado neutro |
| Success | Verde | Completado, merged, done |
| Removed | Rojo | Eliminado, failed, closed |
| InProgress | Azul | En proceso, open |
| New | Púrpura | Nuevo, draft |
| Moved | Amarillo | Movido, warning |

**No confundir con Tag** (Atlassian también tiene Tag, que es removible e interactivo).
El Lozenge es **solo visual, no interactivo**.

---

### Text Field / Form (Atlassian)

Atlassian usa label **siempre fijo encima** del campo — nunca flotante.
Esto es una decisión explícita de accesibilidad.

**Anatomía:**
```
Label [Required indicator]
[Field — con placeholder descriptivo]
[Helper message]
[Error message — reemplaza helper]
```

**Spacing entre campos:** 16px entre cada form field (gap-4 en Tailwind).
**Error:** texto rojo debajo, sin ícono. El campo toma borde rojo.

**Inline validation:** Atlassian valida al perder foco (onBlur), no al tipear.

---

### Modal / Dialog (Atlassian)

Atlassian distingue claramente:
- **Modal** — contenido libre, scrolleable, con header y footer fijos
- **Popup / Inline Dialog** — flotante, anclado a un elemento, para confirmaciones rápidas

**Tamaños de Modal:**
- Small: 400px
- Medium: 600px (default)
- Large: 800px
- X-Large: 968px

**Header:** título grande, botón cerrar (X) a la derecha.
**Footer:** botones alineados a la derecha. Primary a la derecha del todo.
**Scroll:** el body del modal scrollea, header y footer son sticky.

---

### Inline Edit (exclusivo de Atlassian)

Patrón muy usado en Jira/Confluence: un texto que al hacer click se convierte
en un input editable, sin abrir un modal.

```
[Valor actual — apariencia de texto]
  → hover: muestra indicador de editable
  → click: se convierte en input con confirm/cancel
```

Muy útil para edición de campos individuales en vistas de detalle.

---

### Table (Atlassian)

Atlassian tiene uno de los sistemas de tabla más completos:
- **Dynamic Table:** sortable, con paginación integrada, loading state
- **Simple Table:** estática, solo datos
- **Tree Table:** filas expandibles con jerarquía

**Density:** compact (32px por fila) o default (40px por fila).
Las tablas de Atlassian son deliberadamente compactas para mostrar más datos.

---

### Flag (Toast/Notification — Atlassian)

Atlassian llama "Flag" a lo que otros llaman Toast o Snackbar.

**Diferencias con Material Snackbar:**
- Puede tener **múltiples acciones** (no solo una)
- Puede tener **descripción** además del título
- Se **apilan** (stack) — pueden aparecer varios simultáneamente
- Posición: top-right (no bottom como Material)
- No tienen auto-dismiss obligatorio — pueden ser persistentes

**Types:** Info · Success · Warning · Error

---

### Inline Message

Patrón exclusivo de Atlassian para **mensajes contextuales dentro del formulario**,
no como banner ni como toast, sino integrado en el flujo del contenido.

```
[ícono] Texto del mensaje de contexto
```

Más discreto que el Alert Banner, más permanente que el Flag.

---

## Tokens de color clave

```css
/* Atlassian color tokens (simplificados) */
--ds-background-brand-bold: #0052CC;        /* Jira blue */
--ds-background-danger-bold: #DE350B;       /* Red */
--ds-background-success-bold: #00875A;      /* Green */
--ds-background-warning-bold: #FF991F;      /* Yellow/Orange */
--ds-background-discovery-bold: #6554C0;    /* Purple */

--ds-text: #172B4D;                          /* Primary text */
--ds-text-subtle: #5E6C84;                  /* Secondary text */
--ds-text-disabled: #8993A4;               /* Disabled text */

--ds-border: #DFE1E6;                       /* Default border */
--ds-border-focused: #4C9AFF;              /* Focus ring */
```

**Filosofía de color de Atlassian:** Los colores son **funcionales**, no expresivos.
El azul Jira (#0052CC) es el color de acción, no de marca decorativa.
