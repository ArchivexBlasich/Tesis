# Estructura de la Presentación de Defensa de Tesis
## "Diseño, Implementación y Despliegue de un Sistema de Firma Electrónica de Documentos On-Premise para la FACET"

**Autor:** Fabricio Blasich — Ingeniería en Computación, FACET/UNT  
**Tutores:** Mgter. Carlos Albaca Paraván · Mgter. Esteban Daniel Volentini  
**Fecha de defensa:** 26 de mayo de 2026  
**Duración estimada:** 20 minutos de exposición + 6 minutos de demostración en vivo  
**Formato:** RevealJS, pantalla 1920×1080, transición fade entre slides, zoom en secciones  
**Total de diapositivas:** 25

---

## Bloque 1 — Introducción (Diapositivas 1–2)

### Diapositiva 1 · Portada
Título completo del trabajo, nombre del autor, tutores, fecha de defensa y logotipos de FACET/UNT. Es la primera pantalla que ve el jurado. El orador saluda y presenta el trabajo.

### Diapositiva 2 · Tabla de Contenidos
Lista los cinco bloques temáticos de la presentación:
1. Contexto y Problemática
2. Objetivos del Trabajo
3. Estado del Arte y Selección de Plataforma
4. Infraestructura y Arquitectura de Despliegue
5. Demostración en Vivo

---

## Bloque 2 — Contexto y Problemática (Diapositivas 3–4)

### Diapositiva 3 · Separador de Sección — "Contexto y Problemática"
Pantalla de transición que marca el inicio de la primera sección. Fondo oscuro (#0b1120), número y título de sección con tipografía grande. Sin texto oral, solo avanzar.

### Diapositiva 4 · El Problema — Proceso de Firma Actual en la FACET
Diagrama de flujo SVG (izquierda) que ilustra el proceso manual actual: el usuario descarga el PDF, busca una herramienta externa, lo firma, abre el correo y lo reenvía al siguiente firmante, repitiendo el ciclo.
A la derecha, cuatro tarjetas que nombran los problemas: (1) Pérdida de tiempo administrativo en tareas repetitivas, (2) Errores humanos — correos perdidos y archivos sin adjuntar, (3) Falta de trazabilidad — sin registro centralizado ni estado por trámite, (4) Uso ineficiente del almacenamiento — el mismo archivo replicado en decenas de equipos y correos.

---

## Bloque 3 — Objetivos del Trabajo (Diapositivas 5–7)

### Diapositiva 5 · Separador de Sección — "Objetivos del Trabajo"
Pantalla de transición. Fondo índigo oscuro (#1e1b4b). Sin texto oral.

### Diapositiva 6 · Objetivo General — Nuevo Proceso Automatizado
Flowchart SVG horizontal con cuatro pasos que se revelan progresivamente con clics:
- Paso 1 — Carga Única: el usuario sube el PDF una sola vez a la plataforma web.
- Paso 2 — Configuración Visual: define firmantes y posición física de cada firma en el documento.
- Paso 3 — Motor de Automatización: Documenso notifica y gestiona el flujo sin intervención manual.
- Paso 4 — Salida Trazable: documento firmado, con sello criptográfico, validable públicamente y almacenado en la infraestructura de la FACET.

### Diapositiva 7 · Objetivos Específicos
Cuatro anillos animados que se revelan uno a uno:
1. Relevamiento y Selección — evaluar alternativas open source on-premise.
2. Arquitectura y Políticas — diseñar el despliegue, backups y gestión de usuarios.
3. Implementación Piloto — validar con usuarios reales y medir usabilidad.
4. Documentación y Transferencia — manuales de operación para garantizar continuidad.

---

## Bloque 4 — Estado del Arte y Selección de Plataforma (Diapositivas 8–13)

### Diapositiva 8 · Separador de Sección — "Estado del Arte y Selección de Plataforma"
Pantalla de transición. Fondo azul cielo (#0369a1). Sin texto oral.

### Diapositiva 9 · Panorama del Mercado — Soluciones SaaS
Tabla comparativa de las tres plataformas SaaS dominantes: DocuSign, Dropbox Sign y Adobe Sign. Columnas: costo por usuario (entre $24 y $25/mes), límite de envíos, residencia de datos y costo estimado para 20 usuarios. Resultado: entre $480 y $500/mes, es decir cerca de $6.000/año en moneda extranjera, con datos almacenados en infraestructura del proveedor (AWS/Azure) fuera del país. Conclusión: se descartan las opciones SaaS por costo y falta de soberanía de datos.

### Diapositiva 10 · Panorama del Mercado — Soluciones Open Source
Dos tarjetas de proyecto al estilo GitHub:
- **Documenso** (documenso/documenso) — 12.900 estrellas, TypeScript/Next.js/PostgreSQL, self-hosted, estándar PAdES, descripción: "The open source DocuSign alternative."
- **DocuSeal** (docusealco/docuseal) — 16.900 estrellas, Ruby on Rails/Vue.js, self-hosted, legaltech. Descripción: "Open source DocuSign alternative."
Ambos proyectos cumplen el requisito de soberanía de datos. La diferencia está en el stack y en las funcionalidades incluidas en la versión libre.

### Diapositiva 11 · Comparativa Open Source — Documenso vs DocuSeal
Tabla detallada de cinco criterios:
- Gestión de Roles (RBAC): Documenso ✓ Community Ed. — DocuSeal ✕ Enterprise Edition (pago).
- Login con Google (SSO): Documenso ✓ Community Ed. — DocuSeal ✕ Enterprise Edition (pago).
- Branding Personalizado: Documenso ✓ Community Ed. — DocuSeal ✕ Enterprise Edition (pago).
- Stack Tecnológico: Documenso usa Remix + Prisma/PostgreSQL — DocuSeal usa Ruby on Rails/PostgreSQL.
- Licencia: ambos AGPL-3.0.
DocuSeal bloquea funcionalidades institucionales esenciales detrás de un plan pago. Documenso las incluye en la versión libre. **Documenso es seleccionado.** La tabla muestra la insignia "✓ Seleccionado" junto al logo de Documenso.

### Diapositiva 12 · ¿Por qué Documenso? — Modelo Organizacional
Explica el modelo jerárquico: Organización → Teams → Miembros. El mapeo con la FACET es directo: FACET = Organización, cada departamento (DEEC, Física, Matemática, etc.) = Team. Los documentos de cada departamento viven en su espacio aislado. Un docente en dos departamentos pertenece a los dos teams simultáneamente sin configuración adicional. Documenso implementa roles granulares por organización y por team (Administrador, Gerente, Miembro). DocuSeal, en cambio, trata a todos como administradores — un problema de seguridad en entornos institucionales.

### Diapositiva 13 · ¿Por qué Documenso? — Integraciones Externas
Diagrama de tres hexágonos con las integraciones utilizadas:
- **MinIO** (almacenamiento S3): los PDFs no se guardan en el disco del servidor sino en un bucket MinIO que corre en la propia infraestructura de la FACET. Protocolo compatible con S3 de Amazon.
- **Brevo** (email): relay SMTP gratuito que permite hasta 300 correos diarios. Cubre el volumen institucional sin costo adicional.
- **Google OAuth 2.0** (autenticación): los docentes y administrativos ingresan con su cuenta Google de la UNT sin crear contraseñas nuevas. Reduce la fricción de adopción.

---

## Bloque 5 — Infraestructura y Arquitectura de Despliegue (Diapositivas 14–21)

### Diapositiva 14 · Separador de Sección — "Infraestructura y Arquitectura de Despliegue"
Pantalla de transición. Fondo azul marino oscuro (#132f4c). Sin texto oral.

### Diapositiva 15 · Conceptos Clave de la Infraestructura
Layout de dos servidores revelados por capas con clics:
- **Servidor 1 (App):** Hardware físico → Proxmox VE (hipervisor open source con KVM y LXC) → Contenedor LXC → Coolify PaaS + Traefik Reverse Proxy → Contenedores Docker individuales (Documenso, PostgreSQL, MinIO, Browserless).
- **Servidor 2 (NAS):** Hardware físico → TrueNAS (gestión de discos con RAID) → MinIO (bucket S3 on-premise).
La separación física entre el servidor de aplicación y el servidor de almacenamiento simplifica los backups y mejora la resiliencia.

### Diapositiva 16 · Diagrama General de Arquitectura
Imagen de fondo de pantalla completa con el diagrama de red completo. Zona WAN (usuario/internet) → Router de borde FACET con Nginx (primer proxy, terminación TLS externa) → Red interna → Contenedor LXC con Traefik → Contenedores Docker (Documenso). Flujos auxiliares: Documenso ↔ Brevo (SMTP), Documenso ↔ Google OAuth, Documenso ↔ MinIO NAS (protocolo S3). Todo dentro de la red institucional, sin datos saliendo a la nube.

### Diapositiva 17 · Stack de Documenso — Contenedores Docker
Imagen de fondo de pantalla completa con el diagrama interno del stack Docker orquestado por Coolify. Tres contenedores: **PostgreSQL** (solo metadata: estado de trámites, usuarios, permisos — no almacena PDFs para evitar crecimiento descontrolado), **Documenso** (la aplicación principal) y **Browserless** (Chrome virtual en segundo plano que resuelve un problema de integración: la imagen oficial de Documenso no incluye Chromium para renderizar el certificado visual en el PDF; Browserless actúa como delegado de renderizado y permite completar el ciclo de firma sin modificar la imagen oficial).

### Diapositiva 18 · Dimensionamiento del Almacenamiento
Gráfico de dona SVG (izquierda) mostrando que los 2 TB asignados representan el 11% del servidor TrueNAS total. Cadena de cálculo (derecha):
- Punto de partida: 300 correos/día (límite Brevo gratuito)
- ÷ 6 notificaciones por trámite → 50 trámites/día
- × 20 MB por trámite (PDF original + PDF firmado en MinIO)
- = 1 GB/día de crecimiento proyectado
- × 1.825 días (5 años de retención ILM)
- = 1,825 TB → **cuota asignada: 2 TB** (margen de seguridad del 10%)

### Diapositiva 19 · Políticas de Backup y Retención
Tres tarjetas en grilla:
1. **Base de datos PostgreSQL:** volcado lógico automático diario a las 03:00 AM guardado en bucket MinIO aislado. Retención 30 días. RPO: 24 horas. Restauración desde la interfaz gráfica de Coolify sin comandos manuales.
2. **Configuración del entorno:** script bash a las 04:00 AM que empaqueta docker-compose, variables de entorno y el certificado de firma .p12 codificado en Base64. Tiempo de reconstrucción estimado: 30 minutos.
3. **Documentos (MinIO):** política ILM de 5 años sobre el bucket de documentos firmados. El certificado .p12 es el elemento crítico: sin él no se pueden emitir nuevas firmas aunque se recupere la base de datos.

### Diapositiva 20 · Rendimiento del Sistema
Captura de pantalla de Netdata (monitoreo en tiempo real, lado izquierdo) tomada durante una prueba de carga con 5 documentos firmados simultáneamente. Cuatro tarjetas de métricas:
- RAM en reposo: 400 MB (4 contenedores juntos)
- Pico de RAM: 1,33 GB / 8 GB asignados = **16% de uso**
- Pico de CPU: **12,5%**
- Conclusión: más del 83% de RAM y 87% de CPU disponibles incluso bajo carga. Margen amplio para escalar sin nuevo hardware.

### Diapositiva 21 · ¿Firma Electrónica o Firma Digital?
Slide de encuadre legal. Dos grupos de texto estructurados:
- **Lo que el sistema cumple técnicamente:** identificación unívoca del firmante mediante procedimiento matemático + garantía de integridad del documento (cualquier modificación posterior invalida la firma).
- **Distinción legal — Ley 25.506, Art. 9:** para ser Firma Digital el certificado debe ser emitido por una Autoridad Certificante licenciada por el Estado Nacional. El sistema usa un certificado autofirmado institucional → emite **Firma Electrónica**, no Firma Digital. Tiene plena validez administrativa dentro de la FACET para todos sus circuitos internos.

---

## Bloque 6 — Demostración en Vivo (Diapositivas 22–23)

### Diapositiva 22 · Separador de Sección — "Demostración en Vivo"
Pantalla de transición. Fondo azul petróleo (#0c4a6e). Sin texto oral.

### Diapositiva 23 · Demo en Vivo
Pantalla de espera animada con tres anillos pulsantes concéntricos y badge central "Demo en Vivo" con punto de estado verde parpadeante. La demostración dura aproximadamente 6 minutos sobre el sistema real en `documentos.facet.unt.edu.ar`. Flujo: login con Google UNT → subir PDF → configurar firmantes y posición de firma → enviar trámite → mostrar notificación por email → completar firma desde el link del correo → descargar PDF final → verificar sello criptográfico.

---

## Bloque 7 — Cierre (Diapositivas 24–25)

### Diapositiva 24 · Separador de Sección — "¿Preguntas?"
Pantalla de transición. Fondo oscuro (#0b1120), texto "¿Preguntas?" en tipografía grande. Apertura del espacio para preguntas del jurado.

### Diapositiva 25 · Gracias
Pantalla de cierre con animación de confetti (180 piezas, 7 colores) disparada al entrar a la slide. Texto central: "¡Gracias!" El orador agradece brevemente y queda a disposición del jurado durante las preguntas. Permanecer en esta pantalla durante toda la ronda de preguntas.

---

## Resumen Cuantitativo

| Bloque | Slides | Contenido principal |
|---|---|---|
| Introducción | 1–2 | Portada + tabla de contenidos |
| Contexto y Problemática | 3–4 | Separador + flujo actual con problemas |
| Objetivos | 5–7 | Separador + objetivo general (flowchart) + 4 objetivos específicos |
| Estado del Arte | 8–13 | Separador + SaaS + Open Source + comparativa + modelo org + integraciones |
| Infraestructura | 14–21 | Separador + conceptos clave + arquitectura + stack Docker + almacenamiento + backup + rendimiento + encuadre legal |
| Demo | 22–23 | Separador + pantalla de demo en vivo |
| Cierre | 24–25 | Preguntas + Gracias |

**Tecnologías mencionadas en la presentación:** Documenso, DocuSeal, DocuSign, Dropbox Sign, Adobe Sign, Proxmox VE, LXC, KVM, Coolify, Traefik, Docker, PostgreSQL, MinIO, Brevo, Google OAuth 2.0, TrueNAS, Netdata, Browserless, AGPL-3.0, PAdES, Ley 25.506.
