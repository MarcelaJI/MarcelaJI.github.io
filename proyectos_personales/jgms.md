---
layout: default
title: JGMS — Automatización Empresarial
---

<div class="text-center mb-10">
  <p class="text-sm tracking-[0.2em] text-gray-500 mb-1">PROYECTO PERSONAL</p>
  <h1 class="text-3xl sm:text-5xl font-display font-bold tracking-wide neon-text m-0">JGMS — Automatización Empresarial</h1>
  <p class="mt-3 text-lg sm:text-xl text-gray-300 max-w-2xl mx-auto">Plataforma web privada que transforma un flujo administrativo manual basado en Excel en un sistema centralizado completamente automatizado.</p>

  <div class="flex flex-wrap justify-center gap-2 sm:gap-3 mt-6 text-sm">
    <span class="tag-btn">Backend: Go</span>
    <span class="tag-btn">Frontend: Next.js + React</span>
    <span class="tag-btn">PostgreSQL</span>
    <span class="tag-btn">Docker</span>
    <span class="tag-btn">JWT</span>
    <span class="tag-btn">Excel + PDF</span>
  </div>

  <div class="flex flex-wrap justify-center gap-4 mt-4 text-sm text-gray-400">
    <span>Rol: Full-Stack Developer & Arquitecta</span>
    <span class="text-gray-600">|</span>
    <span>Status: Desplegado privadamente</span>
  </div>
</div>

---

## El Problema

<section class="glass-panel p-5 sm:p-7 mb-8" markdown="1">

El proceso administrativo semanal de la empresa seguía un flujo completamente manual centrado en archivos Excel. Cada semana, un administrador debía:

- Recibir las horas trabajadas de cada empleado (por teléfono o mensaje)
- Copiar manualmente las horas en una hoja de cálculo de facturación
- Asignar cada trabajador a la empresa y proyecto correctos
- Registrar gastos de hotel, taxi y otros
- Calcular pagos, deducciones e impuestos a mano
- Generar la factura semanal en Excel
- Convertir manualmente la factura a PDF
- Guardar una copia del PDF en carpetas del sistema ("Save a Copy")
- Abrir Outlook, redactar el correo y adjuntar la factura
- Actualizar manualmente los archivos Excel maestros de pagos y deducciones
- Al final del mes, sumar manualmente todas las facturas semanales

</section>

### Desafíos del flujo manual

<div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-8" markdown="1">

<div class="glass-panel p-4">

<strong>🔴 Errores humanos frecuentes</strong><br>
Copiar horas manualmente entre documentos provocaba errores de transcripción. Un dígito mal puesto podía generar una factura incorrecta, un pago equivocado o una deducción mal calculada.

</div>

<div class="glass-panel p-4">

<strong>🔴 Información dispersa</strong><br>
Los datos del negocio vivían en múltiples archivos Excel independientes: pagos semanales, deducciones, facturas, resúmenes mensuales. No existía una fuente centralizada de verdad.

</div>

<div class="glass-panel p-4">

<strong>🔴 Tiempo excesivo</strong><br>
Completar el ciclo semanal (horas → factura → PDF → archivo → Excel → correo) tomaba horas de trabajo manual repetitivo. Cada semana era igual.

</div>

<div class="glass-panel p-4">

<strong>🔴 Sin trazabilidad</strong><br>
No había registro de quién hizo qué ni cuándo. Si una factura se enviaba dos veces o se olvidaba una semana, no había forma de detectarlo sistemáticamente.

</div>

</div>

---

## La Solución

<section class="glass-panel p-5 sm:p-7 mb-8" markdown="1">

### Una plataforma, un botón

Diseñé y construí una aplicación web privada que centraliza todo el flujo de trabajo en una única plataforma. El administrador ahora:

1. Inicia sesión de forma segura
2. Registra las horas y gastos semanales en un formulario web responsive
3. El sistema calcula automáticamente pagos, impuestos y totales
4. Genera la factura con un clic
5. Genera el PDF profesional automáticamente
6. Archiva una copia de forma automática
7. Exporta los 4 libros Excel que la empresa necesita
8. Revisa y aprueba la factura
9. Envía el correo con el PDF adjunto
10. Todo queda registrado en el log de actividad

**El resultado**: un proceso que tomaba horas se completa en minutos, desde cualquier dispositivo (móvil, tablet o desktop).

</section>

### Diagrama del flujo automatizado

<div class="terminal-shell mb-8">
  <div class="terminal-head">
    <div class="flex items-center gap-2">
      <span class="dot" style="background: #ff5f56;"></span>
      <span class="dot" style="background: #ffbd2e;"></span>
      <span class="dot" style="background: #27c93f;"></span>
    </div>
    <span class="text-gray-500 text-sm">workflow</span>
  </div>
  <div class="terminal-body font-mono text-[0.95rem] leading-relaxed">
    <pre class="text-gray-200 m-0" style="line-height: 1.8">
Registro semanal
  <span class="text-red-300">├──</span> Horas por empleado (Lun–Dom)
  <span class="text-red-300">├──</span> Gastos (hotel, taxi, otros)
  <span class="text-red-300">└──</span> Asignación multi-proyecto
       <span class="text-red-300">│</span>
       <span class="text-red-300">▼</span> <span style="color:#ff6f7c">Cálculos automáticos</span>
       <span class="text-red-300">│</span>   • Pagos a empleados (horas × tarifa + overtime 1.5x)
       <span class="text-red-300">│</span>   • Impuestos (IRS Pub 15-T, FICA, estatal)
       <span class="text-red-300">│</span>   • Per-diem, deducciones
       <span class="text-red-300">│</span>   • Ganancia de la empresa
       <span class="text-red-300">│</span>
       <span class="text-red-300">▼</span> <span style="color:#ff6f7c">Generación de factura</span>
       <span class="text-red-300">│</span>   • Numeración automática por empresa
       <span class="text-red-300">│</span>   • Cálculo de subtotal, impuestos, total
       <span class="text-red-300">│</span>
       <span class="text-red-300">▼</span> <span style="color:#ff6f7c">PDF + Archivo</span>
       <span class="text-red-300">│</span>   • Renderizado profesional (DejaVuSans)
       <span class="text-red-300">│</span>   • Archivado automático: AÑO/MES/EMPRESA/
       <span class="text-red-300">│</span>
       <span class="text-red-300">▼</span> <span style="color:#ff6f7c">Exportación Excel</span>
       <span class="text-red-300">│</span>   • 4 libros: Pagos, Trabajos, Deducciones, Resumen Mensual
       <span class="text-red-300">│</span>
       <span class="text-red-300">▼</span> <span style="color:#ff6f7c">Revisión y aprobación</span>
       <span class="text-red-300">│</span>   • Vista previa del PDF + correo
       <span class="text-red-300">│</span>   • Flujo de aprobación obligatorio
       <span class="text-red-300">│</span>
       <span class="text-red-300">▼</span> <span style="color:#ff6f7c">Envío de correo</span>
       <span class="text-red-300">│</span>   • SMTP con TLS + reintentos
       <span class="text-red-300">│</span>   • Safety gates: test/prod mode, require_invoice_approval
       <span class="text-red-300">│</span>   • Registro de resultado en auditoría
       <span class="text-red-300">│</span>
       <span class="text-red-300">▼</span> <span style="color:#27c93f">Dashboard actualizado + Actividad registrada</span>
    </pre>
  </div>
</div>

---

## Funcionalidades Clave

<div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-8">

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">🔐 Autenticación segura</h3>
<p class="text-gray-300 text-sm m-0">JWT con firma HMAC-SHA256, rotación automática de tokens, contraseñas hasheadas con bcrypt (costo 12), rutas protegidas por middleware.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">🏢 Multi-compañía</h3>
<p class="text-gray-300 text-sm m-0">Gestión independiente por empresa cliente: prefijo de facturación, plantillas, destinatarios de correo, configuración de modos test/producción.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">👷 Gestión de empleados</h3>
<p class="text-gray-300 text-sm m-0">Registro completo con W-4 (IRS), tarifa por hora, tarifa de cobro, estado fiscal por estado (FL, OH), per-diem, deuda acumulada.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">📊 Reportes semanales</h3>
<p class="text-gray-300 text-sm m-0">Formulario multi-proyecto: añade grupos de trabajo con empleados, 7 días de horas, gastos individuales y generales. Validación completa.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">🧾 Facturación automática</h3>
<p class="text-gray-300 text-sm m-0">Numeración por empresa en transacción atómica. Cálculo de mano de obra + gastos + impuestos. Soporte para número de factura personalizado.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">📄 PDF profesional</h3>
<p class="text-gray-300 text-sm m-0">Renderizado en Go con fuentes DejaVuSans embebidas en el binario. Tabla formateada, resumen con subtotal/tax/total. Sin dependencias externas.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">🗄️ Archivo automático</h3>
<p class="text-gray-300 text-sm m-0">Cada PDF se archiva automáticamente en estructura AÑO/MES/EMPRESA/. Elimina el proceso manual de "Save a Copy".</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">📑 Excel multi-libro</h3>
<p class="text-gray-300 text-sm m-0">Generación nativa de 4 libros: Pagos Semanales, Trabajos, Deducciones y Resumen Mensual con formato, colores y estilos profesionales.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">💰 Cálculo de impuestos</h3>
<p class="text-gray-300 text-sm m-0">IRS Pub 15-T (2025): FIT, Social Security 6.2%, Medicare 1.45%, FUTA, SUTA, impuesto estatal (FL 0%, OH 2.75%). Horas extra a 1.5x.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">✉️ Correo automatizado</h3>
<p class="text-gray-300 text-sm m-0">SMTP con STARTTLS y hasta 3 reintentos. Templates con variables (company, invoice, project). Safety gates: test mode, production_enabled.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">📈 Dashboard y reportes</h3>
<p class="text-gray-300 text-sm m-0">Ingresos semanales/mensuales, ganancia, facturas pendientes. 5 tipos de reportes exportables a PDF/Excel. Conciliación mensual.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-lg">📱 Mobile-first</h3>
<p class="text-gray-300 text-sm m-0">Diseño responsive completo. Todo el flujo semanal se puede completar desde un teléfono móvil. Sistema de diseño con tema claro/oscuro.</p>
</div>

</div>

---

## Stack Tecnológico

<section class="glass-panel p-5 sm:p-7 mb-8">

<div class="overflow-x-auto">
<table class="w-full text-sm text-gray-200">
  <thead>
    <tr class="border-b border-red-900/30 text-left text-gray-400">
      <th class="py-2 pr-4">Categoría</th>
      <th class="py-2 pr-4">Tecnología</th>
      <th class="py-2">Justificación</th>
    </tr>
  </thead>
  <tbody>
    <tr class="border-b border-red-900/10">
      <td class="py-2 pr-4 text-red-300">Frontend</td>
      <td class="py-2 pr-4 font-mono text-xs">Next.js 14 · React 18 · TypeScript · Tailwind CSS 3</td>
      <td class="py-2 text-gray-400">App Router, tipado estático, CSS utilitario, 21 páginas responsive. Sin librerías externas de UI.</td>
    </tr>
    <tr class="border-b border-red-900/10">
      <td class="py-2 pr-4 text-red-300">Backend</td>
      <td class="py-2 pr-4 font-mono text-xs">Go 1.25 · chi v5 · pgx v5</td>
      <td class="py-2 text-gray-400">Binario único, arquitectura en capas (handlers → services → repositories), 17 handlers HTTP.</td>
    </tr>
    <tr class="border-b border-red-900/10">
      <td class="py-2 pr-4 text-red-300">Base de datos</td>
      <td class="py-2 pr-4 font-mono text-xs">PostgreSQL 16 · Docker</td>
      <td class="py-2 text-gray-400">NUMERIC para cálculos financieros exactos. 14 tablas, 18 migraciones, 17 índices.</td>
    </tr>
    <tr class="border-b border-red-900/10">
      <td class="py-2 pr-4 text-red-300">Autenticación</td>
      <td class="py-2 pr-4 font-mono text-xs">JWT (HS256) · bcrypt</td>
      <td class="py-2 text-gray-400">Tokens de 1h con rotación automática a los 30 min. Contraseñas con costo 12.</td>
    </tr>
    <tr class="border-b border-red-900/10">
      <td class="py-2 pr-4 text-red-300">Excel</td>
      <td class="py-2 pr-4 font-mono text-xs">excelize v2</td>
      <td class="py-2 text-gray-400">Generación nativa .xlsx sin dependencias de Microsoft Office. 4 libros por reporte.</td>
    </tr>
    <tr class="border-b border-red-900/10">
      <td class="py-2 pr-4 text-red-300">PDF</td>
      <td class="py-2 pr-4 font-mono text-xs">go-pdf/fpdf</td>
      <td class="py-2 text-gray-400">Renderizado profesional con fuentes DejaVuSans embebidas en el binario.</td>
    </tr>
    <tr class="border-b border-red-900/10">
      <td class="py-2 pr-4 text-red-300">Email</td>
      <td class="py-2 pr-4 font-mono text-xs">go-mail · SMTP</td>
      <td class="py-2 text-gray-400">TLS/STARTTLS, reintentos, adjuntos PDF. Safety gates test/prod.</td>
    </tr>
    <tr class="border-b border-red-900/10">
      <td class="py-2 pr-4 text-red-300">Infra</td>
      <td class="py-2 pr-4 font-mono text-xs">Docker Compose · Nginx</td>
      <td class="py-2 text-gray-400">PostgreSQL en contenedor. Proxy reverso con HTTPS y enrutamiento por header.</td>
    </tr>
    <tr>
      <td class="py-2 pr-4 text-red-300">Testing</td>
      <td class="py-2 pr-4 font-mono text-xs">go test</td>
      <td class="py-2 text-gray-400">188 tests unitarios y de integración en backend. Cobertura: impuestos, Excel, PDF, email, API.</td>
    </tr>
  </tbody>
</table>
</div>

</section>

---

## Arquitectura

<div class="terminal-shell mb-8">
  <div class="terminal-head">
    <div class="flex items-center gap-2">
      <span class="dot" style="background: #ff5f56;"></span>
      <span class="dot" style="background: #ffbd2e;"></span>
      <span class="dot" style="background: #27c93f;"></span>
    </div>
    <span class="text-gray-500 text-sm">architecture</span>
  </div>
  <div class="terminal-body font-mono text-[0.92rem]">
    <pre class="text-gray-200 m-0" style="line-height: 1.7">
<span style="color:#ff6f7c">USUARIO</span> (Desktop / Tablet / Móvil — responsive)
  <span class="text-red-300">│</span>  HTTPS (TLS 1.2/1.3)
  <span class="text-red-300">▼</span>
<span style="color:#ff6f7c">NGINX</span> (Proxy reverso :443 → :3000 frontend | :8080 backend)
  <span class="text-red-300">│</span>
  <span class="text-red-300">├──────────────────────────────────┐</span>
  <span class="text-red-300">│</span>                                  <span class="text-red-300">│</span>
  <span class="text-red-300">▼</span>                                  <span class="text-red-300">▼</span>
<span style="color:#ff8b95">FRONTEND</span>                           <span style="color:#ff8b95">BACKEND</span>
Next.js 14 · React 18              Go 1.25 · chi v5
TypeScript · Tailwind              17 handlers · 14 services
<span style="color:#888">21 páginas client-side</span>             <span style="color:#888">10 repositories · 13 models</span>
  <span class="text-red-300">│</span>                                  <span class="text-red-300">│</span>
  <span class="text-red-300">│</span>  <span style="color:#666">fetch() + JWT Bearer</span>            <span class="text-red-300">│</span>  <span style="color:#666">pgx pool (25 conns)</span>
  <span class="text-red-300">│</span>                                  <span class="text-red-300">│</span>
  <span class="text-red-300">└──────────────┬───────────────────┘</span>
                 <span class="text-red-300">│</span>
                 <span class="text-red-300">▼</span>
        <span style="color:#ff6f7c">PostgreSQL 16</span> (Docker)
        <span style="color:#888">14 tablas · 18 migraciones</span>
        <span style="color:#888">NUMERIC para finanzas · Transacciones ACID</span>
                 <span class="text-red-300">│</span>
     <span class="text-red-300">┌───────────┼───────────┐</span>
     <span class="text-red-300">│</span>           <span class="text-red-300">│</span>           <span class="text-red-300">│</span>
     <span class="text-red-300">▼</span>           <span class="text-red-300">▼</span>           <span class="text-red-300">▼</span>
<span style="color:#ff8b95">EXCEL</span>     <span style="color:#ff8b95">PDF</span>       <span style="color:#ff8b95">EMAIL</span>
excelize   go-pdf     go-mail
<span style="color:#888">4 libros</span>  <span style="color:#888">facturas</span>   <span style="color:#888">SMTP+TLS</span>
    </pre>
  </div>
</div>

---

## Seguridad y Privacidad

<section class="glass-panel p-5 sm:p-7 mb-8">

Como profesional de ciberseguridad, la seguridad fue una prioridad desde el diseño inicial. La aplicación maneja información financiera y datos personales, por lo que se implementaron múltiples controles:

### Controles implementados

<div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mt-4">
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">JWT con firma HMAC-SHA256 y expiración de 1 hora</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">Contraseñas hasheadas con bcrypt (costo 12)</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">Rotación automática de tokens JWT</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">Middleware de autorización en todas las rutas protegidas</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">SQL parametrizado (pgx $1, $2) — prevención de SQL injection</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">Validación de entrada en handlers y servicios</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">CORS configurado con orígenes, métodos y headers permitidos</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">Variables de entorno para secretos (JWT_SECRET, SMTP_PASS, DATABASE_URL)</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">Safety gates en envío de correos (test mode, require_invoice_approval)</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">Transacciones ACID para integridad de datos financieros</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">Registro de actividad (audit log) de todas las operaciones sensibles</span>
</div>
<div class="border border-red-900/30 rounded-lg p-3">
<span class="text-green-400 text-sm">✓</span> <span class="text-gray-200 text-sm">Arquitectura privada — sin exposición pública, sin registro abierto</span>
</div>
</div>

### Hardening pendiente (roadmap)

<div class="mt-4 text-gray-400 text-sm">
<p class="mb-2"><span class="text-yellow-500">→</span> Rate limiting por IP para prevenir fuerza bruta en login</p>
<p class="mb-2"><span class="text-yellow-500">→</span> 2FA/MFA para cuentas de administrador</p>
<p class="mb-2"><span class="text-yellow-500">→</span> Security headers HTTP (CSP, HSTS, X-Frame-Options)</p>
<p class="mb-2"><span class="text-yellow-500">→</span> HttpOnly en cookies JWT para mitigar robo por XSS</p>
<p class="mb-2"><span class="text-yellow-500">→</span> Auditoría de accesos con IP y User-Agent</p>
<p class="mb-2"><span class="text-yellow-500">→</span> Escaneo automatizado de dependencias (govulncheck, npm audit)</p>
</div>

</section>

---

## Desarrollo Asistido por IA

<section class="glass-panel p-5 sm:p-7 mb-8">

Este proyecto fue desarrollado utilizando un flujo de trabajo de <strong>desarrollo asistido por inteligencia artificial</strong> con supervisión humana en cada etapa:

<div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mt-4 text-sm">
<div class="border border-red-900/30 rounded-lg p-3 text-center">
<p class="text-red-300 font-bold m-0">OpenCode + Gentle AI</p>
<p class="text-gray-400 mt-2 m-0">Orquestador SDD (Spec-Driven Development) coordinando agentes especializados para cada fase: exploración, propuesta, especificación, diseño, implementación y verificación.</p>
</div>
<div class="border border-red-900/30 rounded-lg p-3 text-center">
<p class="text-red-300 font-bold m-0">Documentación primero</p>
<p class="text-gray-400 mt-2 m-0">8 documentos de especificación (PROJECT_SPEC, BUSINESS_FLOW, DATABASE, AUTOMATIONS, SCREENS...) guiaron toda la implementación. La documentación es la fuente de verdad.</p>
</div>
<div class="border border-red-900/30 rounded-lg p-3 text-center">
<p class="text-red-300 font-bold m-0">Revisión adversarial</p>
<p class="text-gray-400 mt-2 m-0">4 agentes revisores independientes (Risk, Readability, Reliability, Resilience) evaluando cambios con criterios de seguridad, mantenibilidad y corrección.</p>
</div>
</div>

<p class="text-gray-400 text-sm mt-4">La IA fue utilizada como herramienta de aceleración y asistencia. Las decisiones de arquitectura, requisitos de negocio, validación de seguridad, testing y decisiones técnicas finales permanecieron bajo control humano en todo momento.</p>

</section>

---

## Proceso de Desarrollo

<div class="mb-8">
  <div class="flex flex-col gap-3">
    <div class="flex items-center gap-3">
      <span class="text-xs text-gray-500 w-16 text-right">Fase 1</span>
      <div class="flex-1 bg-red-900/20 rounded-full h-6 relative overflow-hidden border border-red-900/30">
        <div class="absolute inset-0 bg-red-800/40 w-full flex items-center pl-3 text-xs text-white">Fundación: Go, Next.js, PostgreSQL, auth JWT</div>
      </div>
    </div>
    <div class="flex items-center gap-3">
      <span class="text-xs text-gray-500 w-16 text-right">Fase 2</span>
      <div class="flex-1 bg-red-900/20 rounded-full h-6 relative overflow-hidden border border-red-900/30">
        <div class="absolute inset-0 bg-red-800/40 w-full flex items-center pl-3 text-xs text-white">CRUDs: Companies, Projects, Employees + W-4</div>
      </div>
    </div>
    <div class="flex items-center gap-3">
      <span class="text-xs text-gray-500 w-16 text-right">Fase 3</span>
      <div class="flex-1 bg-red-900/20 rounded-full h-6 relative overflow-hidden border border-red-900/30">
        <div class="absolute inset-0 bg-red-800/40 w-full flex items-center pl-3 text-xs text-white">Weekly Reports: horas multi-proyecto + gastos</div>
      </div>
    </div>
    <div class="flex items-center gap-3">
      <span class="text-xs text-gray-500 w-16 text-right">Fase 4</span>
      <div class="flex-1 bg-red-900/20 rounded-full h-6 relative overflow-hidden border border-red-900/30">
        <div class="absolute inset-0 bg-red-800/40 w-full flex items-center pl-3 text-xs text-white">Invoice + PDF + Archive + Excel + Email</div>
      </div>
    </div>
    <div class="flex items-center gap-3">
      <span class="text-xs text-gray-500 w-16 text-right">Fase 5</span>
      <div class="flex-1 bg-red-900/20 rounded-full h-6 relative overflow-hidden border border-red-900/30">
        <div class="absolute inset-0 bg-red-800/40 w-full flex items-center pl-3 text-xs text-white">Dashboard + 5 Reportes + Activity Log + Conciliación</div>
      </div>
    </div>
    <div class="flex items-center gap-3">
      <span class="text-xs text-gray-500 w-16 text-right">Fase 6</span>
      <div class="flex-1 bg-red-900/20 rounded-full h-6 relative overflow-hidden border border-red-900/30">
        <div class="absolute inset-0 bg-red-800/40 w-full flex items-center pl-3 text-xs text-white">IRS Pub 15-T + FICA + Overtime 1.5x + Per-diem</div>
      </div>
    </div>
    <div class="flex items-center gap-3">
      <span class="text-xs text-gray-500 w-16 text-right">Fase 7</span>
      <div class="flex-1 bg-red-900/20 rounded-full h-6 relative overflow-hidden border border-red-900/30">
        <div class="absolute inset-0 bg-red-800/40 w-full flex items-center pl-3 text-xs text-white">Testing: 188 tests unitarios y de integración</div>
      </div>
    </div>
    <div class="flex items-center gap-3">
      <span class="text-xs text-gray-500 w-16 text-right">Fase 8</span>
      <div class="flex-1 bg-red-900/20 rounded-full h-6 relative overflow-hidden border border-red-900/30">
        <div class="absolute inset-0 bg-red-800/40 w-[95%] flex items-center pl-3 text-xs text-white">Despliegue a producción (en progreso)</div>
      </div>
    </div>
  </div>
</div>

---

## Resultados e Impacto

<section class="glass-panel p-5 sm:p-7 mb-8">

<div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
<div class="text-center p-4">
<p class="text-3xl font-display neon-text m-0">Minutos</p>
<p class="text-gray-400 text-sm mt-1">vs. horas de trabajo manual previo</p>
</div>
<div class="text-center p-4">
<p class="text-3xl font-display neon-text m-0">Un clic</p>
<p class="text-gray-400 text-sm mt-1">para factura → PDF → archivo → Excel</p>
</div>
<div class="text-center p-4">
<p class="text-3xl font-display neon-text m-0">Cero</p>
<p class="text-gray-400 text-sm mt-1">copias manuales, cero Excels duplicados</p>
</div>
<div class="text-center p-4">
<p class="text-3xl font-display neon-text m-0">100%</p>
<p class="text-gray-400 text-sm mt-1">trazabilidad: cada acción queda registrada</p>
</div>
</div>

### Impacto cualitativo

- Eliminación del trabajo manual repetitivo en el ciclo semanal
- Centralización de toda la información del negocio en una base de datos PostgreSQL
- Reducción drástica de errores de transcripción entre documentos
- Trazabilidad completa: auditoría de quién hizo qué y cuándo
- Acceso desde cualquier dispositivo (móvil, tablet, desktop)
- Compatibilidad preservada con los archivos Excel existentes de la empresa
- Ciclo de aprobación obligatorio antes del envío de facturas

</section>

---

## Lo que Aprendí

<div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-8">

<div class="glass-panel p-4">
<h3 class="mt-0 text-sm neon-text">Traducir procesos de negocio a software</h3>
<p class="text-gray-300 text-xs m-0">Modelar un flujo administrativo real — con sus reglas, estados, excepciones y compatibilidad con procesos legacy — en un sistema de software relacional.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-sm neon-text">Arquitectura en capas con Go</h3>
<p class="text-gray-300 text-xs m-0">Diseñar y mantener una arquitectura handlers → services → repositories con inyección de dependencias manual, errores centinela y transacciones ACID.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-sm neon-text">Cálculos financieros y fiscales</h3>
<p class="text-gray-300 text-xs m-0">Implementar IRS Pub 15-T (2025), FICA, FUTA, SUTA, impuestos estatales, horas extra, per-diem — con precisión decimal exacta usando PostgreSQL NUMERIC.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-sm neon-text">Generación de documentos sin dependencias</h3>
<p class="text-gray-300 text-xs m-0">Excel nativo (.xlsx) con excelize y PDF con fuentes embebidas — sin requerir Microsoft Office ni LibreOffice en el servidor.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-sm neon-text">Seguridad desde el diseño</h3>
<p class="text-gray-300 text-xs m-0">Aplicar controles de seguridad (JWT, bcrypt, SQL parametrizado, safety gates, test mode) desde la fase de arquitectura, no como afterthought.</p>
</div>

<div class="glass-panel p-4">
<h3 class="mt-0 text-sm neon-text">Desarrollo asistido por IA con control humano</h3>
<p class="text-gray-300 text-xs m-0">Usar agentes de IA como herramientas de aceleración manteniendo el control sobre arquitectura, decisiones de seguridad, validación y calidad del código.</p>
</div>

</div>

---

## Estado del Proyecto

<div class="flex flex-wrap gap-4 mb-8 text-sm">
  <div class="glass-panel px-4 py-3 flex items-center gap-2">
    <span class="w-2 h-2 rounded-full bg-green-400"></span>
    <span class="text-gray-200">20 de 21 fases completadas</span>
  </div>
  <div class="glass-panel px-4 py-3 flex items-center gap-2">
    <span class="w-2 h-2 rounded-full bg-green-400"></span>
    <span class="text-gray-200">188 tests pasando</span>
  </div>
  <div class="glass-panel px-4 py-3 flex items-center gap-2">
    <span class="w-2 h-2 rounded-full bg-yellow-400"></span>
    <span class="text-gray-200">Despliegue a prod en progreso</span>
  </div>
  <div class="glass-panel px-4 py-3 flex items-center gap-2">
    <span class="w-2 h-2 rounded-full bg-green-400"></span>
    <span class="text-gray-200">Usado en producción privada</span>
  </div>
</div>

---

<section class="text-center pb-4">
  <h2 class="text-3xl sm:text-4xl mb-4 neon-text">¿Interesado/a en cómo abordo la automatización segura?</h2>

  <div class="flex flex-wrap justify-center gap-3 sm:gap-4 text-base sm:text-lg">
    <a class="tag-btn" href="mailto:ingridjimenez113@gmail.com">Email</a>
    <a class="tag-btn" href="https://github.com/MarcelaJi" target="_blank" rel="noopener noreferrer">GitHub</a>
    <a class="tag-btn" href="https://linkedin.com/in/marcela-jimenez-/" target="_blank" rel="noopener noreferrer">LinkedIn</a>
  </div>

  <p class="text-gray-600 text-xs mt-8">Este case study describe un proyecto privado. No se expone información confidencial de clientes, empleados, datos financieros ni infraestructura.</p>
</section>
