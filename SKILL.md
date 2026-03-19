---
name: component-gallery
description: >
  Usar esta skill SIEMPRE que el usuario pida crear, diseñar, documentar o mejorar
  un componente de UI. Aplica cuando mencionen palabras como: botón, modal, dropdown,
  accordion, input, formulario, card, navbar, toast, badge, tabs, table, skeleton,
  spinner, breadcrumb, pagination, tooltip, popover, stepper, o cualquier elemento
  de interfaz. También activar cuando pregunten por naming de componentes, variantes,
  estados, accesibilidad, o cuando digan que un componente "se ve mal" o tiene
  problemas de spacing, padding o margin. Usar aunque no mencionen explícitamente
  "design system" ni "component.gallery".
---

# Component Gallery Skill

Skill para crear componentes de UI de alta calidad, agnósticos de framework,
con referencias cruzadas a component.gallery y a los design systems de Material
Design (Google), Atlassian y Carbon (IBM).

---

## Flujo de trabajo obligatorio

Ante cualquier pedido de componente, seguir este orden:

1. **Identificar** el nombre canónico del componente (ver references/components.md)
2. **Verificar** si el sitio tiene info actualizada con fetch (ver sección Fetch dinámico)
3. **Elegir** implementación: Tailwind o CSS nativo (ver sección Decisión CSS/Tailwind)
4. **Aplicar** reglas visuales de esta skill antes de escribir código
5. **Referenciar** cómo lo resuelven los design systems (ver references/)
6. **Entregar** el componente con sus variantes, estados y notas de accesibilidad

---

## Obtener información actualizada de component.gallery

Seguir este orden de fallback. Pasar al siguiente nivel solo si el anterior falla.

### Nivel 1 — Fetch directo
```
URL: https://component.gallery/components/{nombre-en-kebab-case}
```
Si responde con contenido útil, extraer: nombres alternativos, variantes,
notas de accesibilidad, y qué design systems lo implementan.

### Nivel 2 — web_search (fallback automático si fetch falla con 403/timeout)
```
Queries a usar en orden de preferencia:
  1. "{componente} site:component.gallery"
  2. "{componente} component.gallery design systems"
  3. "{componente} UI component variants accessibility"
```
De los resultados, extraer especialmente los snippets de component.gallery
(source: "The Component Gallery") que suelen contener nombres alternativos
y definiciones precisas del componente.

### Nivel 3 — Base local (siempre disponible)
Usar `references/components.md`. Cubre los ~40 componentes más comunes
con variantes, estados y notas de accesibilidad documentadas manualmente.

**Regla:** Nunca bloquear la generación del componente esperando datos externos.
Si los niveles 1 y 2 no aportan información nueva, proceder directamente con
la base local y documentarlo en la respuesta.

---

## Decisión: Tailwind vs CSS nativo

Usar esta tabla para decidir. No mezclar enfoques en el mismo componente
salvo que sea estrictamente necesario y se documente el porqué.

| Situación | Usar |
|---|---|
| Prototipo rápido, sin design system propio | Tailwind |
| Proyecto con tokens de diseño propios (colores, spacing custom) | CSS nativo con variables |
| Componente altamente dinámico (estados JS, animaciones complejas) | CSS nativo |
| Proyecto ya usa Tailwind en su codebase | Tailwind |
| Necesita theming (dark mode, multi-brand) | CSS nativo con `prefers-color-scheme` |
| Componente simple y estático | Tailwind |
| Animaciones, transiciones finas, pseudo-elementos complejos | CSS nativo |

**Regla de oro:** Si el componente necesita más de 12 clases de Tailwind para
un solo elemento, ese elemento probablemente necesita CSS nativo.

---

## Reglas visuales — Modelo de caja y spacing

Estas son las reglas que la IA viola con más frecuencia. Aplicarlas siempre,
sin excepción, antes de escribir cualquier código de componente.

### 1. Spacing semántico, no acumulativo

❌ MAL — acumular clases hasta que "se vea bien":
```html
<div class="mt-2 mb-4 pt-3 pb-2 px-4 mx-2">...</div>
```

✅ BIEN — spacing con propósito claro:
```html
<!-- Padding interno del componente: p-4 -->
<!-- Margin externo lo decide el padre o el layout -->
<div class="p-4">...</div>
```

**Regla:** El padding es responsabilidad del componente.
El margin es responsabilidad del layout que lo contiene.
Un componente bien escrito nunca debería necesitar margin externo propio.

### 2. Colapso de márgenes (margin collapse)

En CSS nativo, los márgenes verticales entre elementos en flujo normal se
colapsan. Tailwind usa `box-sizing: border-box` globalmente pero NO previene
el colapso de márgenes.

✅ Para evitar colapso inesperado usar Flexbox o Grid en el contenedor padre:
```html
<div class="flex flex-col gap-4">
  <!-- Los gap reemplazan margin-top/bottom y nunca colapsan -->
  <div>Elemento 1</div>
  <div>Elemento 2</div>
</div>
```

**Regla:** Preferir `gap` sobre `margin` para separar elementos hermanos.

### 3. Modelo de caja explícito

En CSS nativo, siempre declarar `box-sizing: border-box` en componentes custom:
```css
.component {
  box-sizing: border-box; /* padding y border incluidos en el width/height */
  padding: 1rem;
  width: 100%; /* no desborda */
}
```

En Tailwind, `border-box` ya está activado globalmente. No es necesario
declararlo, pero hay que recordar que `w-full` + `border` + `p-4` NO desborda.

### 4. Flexbox: los errores más comunes

❌ MAL:
```html
<!-- shrink-0 innecesario en items que no deberían crecer -->
<!-- items-center en eje equivocado -->
<div class="flex items-center justify-between mt-4 mb-4 px-3 py-3">
```

✅ BIEN:
```html
<div class="flex items-center justify-between p-3 gap-2">
```

**Reglas de Flexbox:**
- `items-center` afecta el eje transversal (vertical en row, horizontal en column)
- `justify-center` afecta el eje principal
- Los hijos de un flex container tienen `flex-shrink: 1` por defecto — agregar
  `shrink-0` solo cuando el elemento no debe achicarse (iconos, avatares, badges)
- `flex-1` en un hijo = ocupa todo el espacio disponible. Usar con intención.

### 5. Texto y alineación

❌ No usar `text-center` en contenedores, usarlo en el elemento de texto:
```html
<!-- MAL: todo el contenedor centrado, afecta elementos hijos inesperadamente -->
<div class="flex flex-col text-center">

<!-- BIEN: solo el texto que debe centrarse -->
<div class="flex flex-col">
  <h2 class="text-center">Título</h2>
  <p>Párrafo alineado a la izquierda</p>
</div>
```

### 6. Responsive y tamaños

- Nunca hardcodear `width` o `height` en píxeles salvo para elementos de
  tamaño fijo (avatares, iconos, badges de conteo)
- Usar `min-h-*` en lugar de `h-*` cuando el contenido puede crecer
- En Tailwind: `w-full` en el componente, el contenedor limita el ancho
- En CSS nativo: `max-width` + `width: 100%` para componentes fluidos

### 7. Z-index y stacking context

Componentes flotantes (Modal, Tooltip, Dropdown, Popover) crean stacking
contexts. Usar una escala consistente:

```css
/* Escala recomendada */
--z-dropdown: 100;
--z-sticky: 200;
--z-overlay: 300;
--z-modal: 400;
--z-toast: 500;
--z-tooltip: 600;
```

En Tailwind, usar clases custom o la escala por defecto (z-10, z-20... z-50).
Documentar siempre qué z-index usa cada componente flotante.

---

## Estructura de entrega de un componente

Todo componente generado por esta skill debe seguir esta estructura:

```
## [Nombre canónico] — [Nombres alternativos]

### Descripción breve
Una oración sobre qué hace y cuándo usarlo.

### Variantes
Lista de variantes documentadas (con código)

### Estados
- Default
- Hover / Focus
- Active / Pressed
- Disabled
- Loading (si aplica)
- Error / Success (si aplica)

### Código
[Tailwind o CSS nativo según la decisión tomada]

### Accesibilidad
- Role ARIA correcto
- Atributos requeridos
- Comportamiento de teclado

### Referencias en design systems
[Cómo lo resuelven Material, Atlassian y Carbon — ver references/]
```

---

## Archivos de referencia

Cargar el archivo correspondiente según lo que se necesite.
No cargar todos los archivos en cada respuesta — solo los relevantes.

| Archivo | Cuándo cargarlo |
|---|---|
| `references/components.md` | Siempre que se genere un componente |
| `references/material.md` | Cuando el usuario mencione Material, Google, o quiera ver la referencia |
| `references/atlassian.md` | Cuando el usuario mencione Atlassian, Jira, Confluence, o quiera ver la referencia |
| `references/carbon.md` | Cuando el usuario mencione Carbon, IBM, o quiera ver la referencia |

Para consultas generales sobre componentes, cargar solo `references/components.md`.
Para consultas con referencia a un DS específico, cargar components.md + ese DS.

---

## Notas de accesibilidad universales

Aplicar en todos los componentes sin excepción:

- **Contraste:** mínimo 4.5:1 para texto normal, 3:1 para texto grande (WCAG AA)
- **Focus visible:** nunca usar `outline: none` sin reemplazarlo con un indicador visible
- **Interacción por teclado:** Tab para navegar, Enter/Space para activar, Escape para cerrar overlays
- **Semántica HTML:** usar el elemento nativo correcto antes de recurrir a `div` con role
- **Texto alternativo:** imágenes decorativas con `alt=""`, imágenes informativas con `alt` descriptivo
