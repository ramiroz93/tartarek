# Tartarek — Agente de Recomendación de Cursos

**🔗 Demo en vivo:** https://ramiroz93.github.io/tartarek/

Agente interno que sugiere qué cursos conviene repetir o lanzar, y hace matching automático entre esas ideas de curso y una base de hojas de vida (CVs), por palabras clave.

Extraído como pieza de portfolio de un sistema de gestión más grande ([VirtuallCorp — Sistema de Ventas](../sistema-ventas-virtualcorp-github)), donde vive como uno de sus módulos.

## Demo standalone

Este repo es 100% autocontenido: **abre `index.html` en el navegador y funciona**, sin backend, sin base de datos, sin claves de API. Los cursos, CVs y coincidencias son ficticios y se generan en el propio navegador al cargar la página.

## Qué muestra

- **Cursos a Repetir** — analiza doce meses de historial de ventas simulado y detecta qué cursos superaron el umbral de inscritos en su última edición y no tienen ya una repetición programada
- **Cursos Nuevos** — recomendaciones de cursos agrupadas por área, con temario de 7 puntos y nivel de importancia (1 a 5 estrellas) editable
- **Ideas de Curso** — bandeja de ideas (manuales o enviadas desde "Cursos Nuevos"), con matching de CVs por palabras clave y flujo para descartar candidatos o palabras demasiado genéricas
- **Buscar CV** — búsqueda de hojas de vida por contenido o por nombre de archivo, y detección de posibles CVs duplicados
- **Seguimiento** — pipeline de 4 etapas (llamada, temario, diapositivas, reunión) por curso ya asignado a un docente, con semáforo de fechas

## Cómo funciona el matching de CVs

En el sistema original, el matching corre en una Edge Function de Supabase que compara el contenido de la idea de curso contra el texto extraído de cada CV, ponderando las coincidencias de palabras clave (sin depender de un modelo de embeddings externo). En esta demo, el mismo criterio se reproduce en JavaScript en el navegador: se tokeniza el texto de la idea, se descartan palabras genéricas, y se comparan las palabras restantes contra el texto de cada CV de ejemplo — incluyendo la opción de "descartar" una palabra clave para que deje de generar coincidencias falsas en el futuro.

## Stack técnico

- JavaScript vanilla (sin framework, sin build step)
- En el sistema original: [Supabase](https://supabase.com) (Postgres + Edge Functions) como backend — en esta demo, reemplazado por datos y lógica de matching que corren enteramente en el navegador

> Repo de portfolio: no contiene CVs, cursos ni datos reales de ninguna persona o empresa.
