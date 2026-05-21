# Design Spec: modulo3.html — Módulo 3 EVA Interactivo

**Fecha:** 2026-05-13  
**Archivo de salida:** `metodologia/modulo3.html`  
**Despliegue:** standalone → embed via `<iframe srcdoc>` en Schoology

---

## Objetivo

Página educativa única, rica e interactiva para el Módulo 3 del Profesorado de Informática (Metodología de la Educación a Distancia). Consolida contenido de 4 bloques temáticos en una sola experiencia no-lineal con navegación por pestañas, modales, videos embebidos y recursos enlazados.

---

## Arquitectura

Archivo HTML único autocontenido (`<style>` y `<script>` embebidos). Sin dependencias externas excepto iframes de YouTube. Compatible con cualquier browser moderno.

---

## Layout y Navegación

### Header
- Gradiente `#1a237e → #283593 → #1565c0`
- Título: "Módulo 3: Construcción de un Curso en un EVA y el Rol Docente"
- Badge: "Profesorado de Informática · Metodología EaD"
- Subtítulo breve sobre el módulo

### Tab Bar (sticky, visible al hacer scroll)
Cuatro pestañas con ícono + label:

| # | Ícono | Label |
|---|-------|-------|
| 1 | 🏠 | Inicio |
| 2 | 🏗️ | Elementos del EVA |
| 3 | 🧑‍🏫 | El Tutor Virtual |
| 4 | 📁 | Organización y Recursos |

Transición animada (fade + slide) al cambiar de pestaña.

---

## Contenido por Pestaña

### Tab 1 — Inicio
- Texto introductorio sobre EVA (de `contenido.md` Página 1)
- 3 tarjetas "resumen rápido" (cada una es un card clickeable que salta a su pestaña):
  - Elementos del EVA → tab 2
  - El Tutor Virtual → tab 3
  - Organización y Recursos → tab 4
- Cita destacada sobre el cambio de paradigma docente

### Tab 2 — Elementos del EVA
**Recursos multimedia:**
- Video 2 (YouTube `Vo9hgfltwPU`): "Componentes o elementos de un curso en línea"
- Video 3 (YouTube `6SHunbIQ-Lo`): "Ejemplo de Elementos Básicos de un Curso Virtual"

**Componentes interactivos:**
- Grid de 6 cards (los 6 espacios fundamentales) — cada card abre un **modal** con descripción extendida
- Diagrama visual "Sección General vs. Sección de Desarrollo" con 2 columnas coloreadas
- Bloque destacado "La Separación Clave": Resources (azul) vs. Actividades (rojo/naranja) con ejemplos en cada lado

**Recursos externos:**
- Link al canal CFORMA (contexto de los videos)

### Tab 3 — El Tutor Virtual
**Recursos multimedia:**
- Video 4 (YouTube `j3xqo3pabZM`): "Procesos, estrategias y evaluación de la Educación Multimodal"

**Componentes interactivos:**
- 4 cards grandes en grid 2×2 (funciones: Pedagógica, Social, Administrativa, Técnica) — cada card abre **modal** con descripción extendida y ejemplo práctico
- Lista de los 5 Roles Específicos (Badia et al., 2017) como tarjetas numeradas con tooltip/expand al click

**Recursos externos:**
- Botón "📄 Ver PDF: Badia, Meneses y García (2017)" → link al PDF local `Modulo3/Recursos/Badia_Meneses_Garcia_ES_2017.pdf`
- Botón "📄 Ver PDF: El Tutor Virtual" → link al PDF local `Modulo3/Recursos/El_tutor.pdf`

### Tab 4 — Organización y Recursos
**Recursos multimedia:**
- Video 1 (YouTube `ZJUNys88EEI`): "CFORMA - Estructura de elementos para cursos online"

**Componentes interactivos:**
- 3 "folder cards" animadas (Estándares, Recursos, Misceláneos) con ícono de carpeta — cada una abre **modal** con subcarpetas y ejemplos
- Bloque "Evaluación Multimodal" con 3 pasos visuales (timeline horizontal)

---

## Sistema de Modales

- Overlay oscuro semi-transparente
- Modal centrado, max-width 640px, border-radius 14px
- Header con título + botón ✕
- Cuerpo con contenido extendido (texto + lista + íconos)
- Cierre: click en ✕, click en overlay, tecla Escape
- Animación: fade-in + scale desde 0.9 a 1.0

---

## Videos

Cada video se embebe como `<iframe>` de YouTube con:
- `width="100%"`, `height="315"` (o responsive via padding-top trick)
- `frameborder="0"`, `allowfullscreen`
- `loading="lazy"`
- Título descriptivo sobre el iframe

---

## Paleta y Tipografía

| Token | Valor |
|-------|-------|
| Primary | `#1a237e` |
| Primary light | `#1565c0` |
| Accent | `#e65100` |
| Accent soft | `#fff8e1` |
| Background | `#f0f4f8` |
| Card bg | `#ffffff` |
| Border | `#e2e8f0` |
| Text | `#1a1a2e` |
| Text muted | `#555` |

Fuente: `system-ui, -apple-system, 'Segoe UI', sans-serif`

---

## Responsividad

- Grids colapsan a 1 columna en ≤ 600px
- Tab bar colapsa a íconos solos (sin label) en ≤ 480px
- Videos con aspect-ratio 16:9 fluido

---

## Links a Recursos Reales

Todos los recursos externos se abren en `target="_blank" rel="noopener"`:

| Recurso | URL / Path |
|---------|-----------|
| Video 1 | `https://www.youtube.com/watch?v=ZJUNys88EEI` |
| Video 2 | `https://www.youtube.com/watch?v=Vo9hgfltwPU` |
| Video 3 | `https://www.youtube.com/watch?v=6SHunbIQ-Lo` |
| Video 4 | `https://www.youtube.com/watch?v=j3xqo3pabZM` |
| PDF 1 | `Modulo3/Recursos/Badia_Meneses_Garcia_ES_2017.pdf` |
| PDF 2 | `Modulo3/Recursos/El_tutor.pdf` |

---

## Decisiones descartadas

- CSS externo (no portable para embed iframe)
- Frameworks JS (Vanilla JS es suficiente y mantiene el archivo autocontenido)
- Múltiples archivos HTML (usuario aprobó single-file)
