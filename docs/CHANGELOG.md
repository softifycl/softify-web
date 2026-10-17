# Changelog — Softify Bot / Softify Setter

> **Producto:** Softify Bot — agente de IA que **atiende** (WhatsApp, Instagram, Messenger sobre el catálogo de Shopify) y que, desde la **v1.0.0**, incorpora el **Setter** (califica prospectos y **agenda ventas**).
> **Repos:** página web en `softifycl/softify-web`; producto/bot en `alejandrochungp/softify-whatsapp-webhook` (tenant `softify`).
> **Páginas públicas (misma versión y fechas):**
> - https://bot.softify.cl/changelog.html — changelog del **bot de atención + Setter** (este producto).
> - https://softify.cl/changelog.html — changelog del **Softify Setter** (vista del producto de ventas).
> **Dueño:** Agente Producto & Tecnología (Softify).
> **Formato:** [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/) adaptado — fecha · versión · Añadido / Cambiado / Arreglado.
> **Última actualización:** 2026-10-16.
>
> Las versiones **anteriores a v1.0.0 son retroactivas**: se asignaron agrupando por fecha los cambios reales
> del producto/bot (que no llevaba versionado). Desde la v1.0.0 el versionado se mantiene en cada release y **las
> dos páginas usan los mismos números y fechas**. Solo se documenta lo que **existe y fue probado**; lo
> implementado pero aún sin desplegar queda marcado.

---

## [No publicado]

_Nada pendiente de publicar por ahora._

---

## [v1.1.0] — 2026-10-16

### Añadido
- **Integración con CRM (EspoCRM, `crm.softify.cl`)**: el bot **lee** la ficha y el historial del contacto al
  atenderlo y **escribe** la etapa y una nota al cerrar la conversación o al alcanzar un hito. Si el CRM falla,
  no responde o el contacto no existe, el bot **nunca se bloquea**.
- **Resumen estructurado en la ficha**: quién es, motivo, necesidad, oferta mostrada, etapa, próximos pasos y fecha.
- **Flujo Lead → Cuenta + Contacto → Oportunidad** al calificar.
- **Agendador de ventas (beta)**: el bot ofrece **horarios reales** según la disponibilidad del calendario y **crea
  el evento** al elegir el cliente. Horario comercial Lun-Vie 10:00–12:00 y 15:00–17:00 (slots de 30 min,
  `America/Santiago`).
- **Conector de pipeline**: escribe los campos de negocio en el CRM (`cProducto`, `cPlan`, `cEtapaVenta`,
  `cCanalFuente`).
- **Branding Softify** en las apps de soporte: CRM (`crm.softify.cl`) y Firma electrónica (`firma.softify.cl`).

### Notas
- CRM y agendador fueron **probados contra el CRM y el calendario reales**; su operación en vivo con el bot queda
  **sujeta a la configuración de variables** en el entorno de producción.

---

## [v1.0.0] — 2026-10-15

> **Se incorpora el Setter**: el bot de atención pasa a incluir la función de ventas (califica y agenda) en el
> mismo agente.

### Añadido
- **Base de conocimiento del producto Softify Setter**: qué es, flujo completo (calificar → agendar → confirmar),
  modos de uso (Setter / Soporte / Mixto), **planes y precios** (Starter / Pro / Business), add-ons, **ICP y
  anti-ICP**, y reglas **anti-alucinación** para que el bot no invente precios ni capacidades.
- **Prompt mixto (soporte + setter)**: el mismo bot atiende soporte y hace función de setter según el caso.

### Cambiado
- Deploy de la base de conocimiento y el prompt a producción (healthcheck `GET /status` → `{"ok":true}`).

---

## [v0.4.0] — 2026-08-30

### Añadido
- **Identidad y tono humano del bot**: nunca se autodeclara bot/asistente, escribe **sin markdown**, sin signos
  dobles ni capitalización forzada, una idea por mensaje.
- **Imágenes de clientes** enviadas por WhatsApp llegan correctamente al hilo de supervisión (Slack).

### Arreglado
- Coherencia de identidad: el bot **nunca impersona** a personas del equipo y deriva al desarrollador cuando
  corresponde.
- Codificación UTF-8 en los textos de respuesta y aislamiento del upsell por cliente.

---

## [v0.3.x] — 2026-08-06 … 2026-08-17

### Añadido
- **Template de upgrade a plan de pago** y aviso al equipo cuando un cliente sube de plan.

### Arreglado
- Se eliminó el mensaje de fallback intermitente (validación del hilo) y se corrigió el modelo de IA.

---

## [v0.2.x] — 2026-07-14 … 2026-08-02

### Añadido
- **Template de reactivación a 24 h** para retomar conversaciones.

### Cambiado
- Identificador WABA de Softify correcto y nombre del modelo de IA actualizado.

### Arreglado
- **Aislamiento multi-cliente**: el bot filtra los eventos por número (`phone_number_id`) e ignora los de otros
  negocios; restauración de UTF-8.

---

## [v0.1.x] — 2026-05-19 … 2026-06-05

> **Lanzamiento inicial**: nace **Softify Bot** como chatbot multi-canal para tiendas Shopify, con el soporte
> técnico de las apps de Softify (e-Boleta y FreshStock FIFO) como primeros casos de uso.

### Añadido
- Bot **multi-cliente** (multi-tenant) con atención en **WhatsApp, Instagram y Messenger**.
- **Integración con el catálogo de Shopify** en tiempo real (si no hay match, lo dice — no inventa).
- **Recuperación de carritos abandonados** por WhatsApp (delay inteligente, límite diario, horarios).
- Personalización de respuestas por **perfil del cliente** (Klaviyo).
- **Modo campaña** para Cyber Days y peak seasons.
- **Onboarding conversacional** (configuración, certificado SII y seguimiento) y bienvenida a nuevas tiendas vía
  webhook.
- **Handoff a equipo humano** con hilo de supervisión por conversación (Slack).
- Polling de Instagram/Messenger cada 15 min (bandejas General y Requests) y respuesta a interacciones con
  historias de Instagram.

---

<!--
PROCESO: cada release/deploy relevante agrega su entrada ANTES de publicar las dos páginas.
- Editar este archivo (fuente).
- Reflejar en bot.softify.cl/changelog.html y softify.cl/changelog.html (misma versión/fecha, la más nueva arriba).
- Publicar con la skill `softify-web-publicar` (commit + push + checkout del subdominio en el droplet).
Fuente de verdad del producto: `softify-whatsapp-webhook/docs/CHANGELOG.md`.
-->
