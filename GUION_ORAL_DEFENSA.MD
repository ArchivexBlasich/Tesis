Guion Oral - Defensa de Tesis (Fabricio Blasich)

Duración estimada: ~20 minutos de habla + 6 minutos de demostración en vivo.

---

## Diapositiva 1: Portada y Bienvenida

"Bueno, jurado, tutores, familia, amigos y público en general aquí presentes y a quienes nos siguen por la transmisión en vivo, bienvenidos a la defensa de mi trabajo de graduación titulado 'Diseño, Implementación y Despliegue de un Sistema de Firma Electrónica de Documentos On-Premise para la FACET'.

Este proyecto fue realizado bajo la tutoría del Magíster Carlos Albaca Paraván y el Magíster Esteban Daniel Volentini. Muchas gracias a todos por estar acá, la verdad que posta me hace muy feliz. Para arrancar, quiero ponerlos un poco en contexto sobre cuál fue la situación que motivó todo este desarrollo."

---

## Diapositiva 2: Tabla de Contenidos

01. Contexto y Problemática
02. Objetivos del Trabajo
03. Estado del Arte y Selección de Plataforma
04. Infraestructura y Arquitectura de Despliegue
05. Demostración en Vivo

---

## Diapositiva 3: [Sección 01 — Contexto y Problemática]

_(Transición de sección — sin texto oral, solo pasar la slide)_

---

## Diapositiva 4: El Problema (El Contexto Actual)

"Históricamente, en la FACET procesamos un volumen gigante de documentación que requiere firmas de autoridades y docentes. Hasta hoy, ese flujo era completamente manual y descentralizado.

[Diagrama de flujo]
¿Cómo funciona hoy? Un usuario necesita firmar un PDF, lo descarga en su computadora, busca una herramienta externa en internet para firmarlo, lo guarda, abre su correo, lo adjunta y se lo manda a la siguiente persona. Y este ciclo se repite por cada firmante.

Como se imaginarán, esto trae muchos problemas. Primero, una pérdida de tiempo administrativo enorme en tareas repetitivas. Segundo, errores humanos: correos que se pierden, archivos que no se adjuntan. Tercero, y muy crítico, la falta de trazabilidad. No tenemos un registro centralizado que nos diga a qué hora firmó cada persona ni en qué etapa exacta está el trámite. Y por último, un uso totalmente ineficiente del almacenamiento, porque el mismo archivo se replica decenas de veces en las computadoras y correos de cada usuario."

---

## Diapositiva 5: [Sección 02 — Objetivos del Trabajo]

_(Transición de sección — sin texto oral, solo pasar la slide)_

---

## Diapositiva 6: Objetivo General — Nuevo Proceso Automatizado

"Aquí explicaré cuál es la lógica de negocio, o qué se espera del sistema a implementar para que solucione la problemática actual.

[Flowchart de 4 pasos — se animan con clicks]

Paso 1 — Carga Única: el docente o alumno sube el PDF una sola vez al sistema. Nada de descargas ni reenvíos por email.

Paso 2 — Configuración Visual: directamente en la interfaz web, define quiénes deben firmar y en qué lugar físico del documento va la firma de cada uno.

Paso 3 — Motor de Automatización: Documenso se encarga del resto — notifica a cada firmante en su turno y gestiona el flujo sin intervención manual.

Paso 4 — Salida Trazable: el documento final queda firmado, con sello criptográfico, validable públicamente, y almacenado en la infraestructura de la FACET."

---

## Diapositiva 7: Objetivos Específicos del Trabajo

[4 círculos animados]

"Frente a todo esto, el objetivo general del trabajo fue diseñar, implementar y desplegar una solución llave en mano para automatizar y centralizar la gestión de firmas en la infraestructura de la facultad. Para alcanzarlo, me planteé cuatro objetivos específicos muy concretos:

01 · Relevamiento & Selección — evaluar alternativas Open Source On-Premise que se adapten a la institución.
02 · Arquitectura & Políticas — diseñar el despliegue, definir políticas de respaldo y gestión de usuarios.
03 · Implementación Piloto — validar la solución con usuarios reales y medir usabilidad.
04 · Documentación & Transferencia — elaborar manuales de operación para garantizar continuidad."

---

## Diapositiva 8: [Sección 03 — Estado del Arte y Selección de Plataforma]

_(Transición de sección — sin texto oral, solo pasar la slide)_

---

## Diapositiva 9: Comparativa SaaS

_(pendiente de redactar)_

---

## Diapositiva 10: Plataformas Open Source Evaluadas

_(pendiente de redactar)_

---

## Diapositiva 11: Comparativa Open Source — Documenso vs DocuSeal

_(pendiente de redactar)_

---

## Diapositiva 12: ¿Por qué Documenso? — Modelo Organizacional

"Una vez que decidimos que Documenso era la herramienta, vale la pena explicar por qué encaja tan bien con la estructura de la FACET — y no es solo por las funcionalidades técnicas.

Documenso tiene un modelo organizacional muy claro: existe una Organización raíz, y dentro de ella se crean Teams. Cada team es un espacio completamente aislado: tiene sus propios documentos, sus propias plantillas, y sus propios miembros. Los integrantes de un team solo ven lo que pertenece a ese team.

El mapeo con la FACET es casi exacto. La FACET es la Organización. Cada departamento — el DEEC, el Departamento de Física, Matemática, y así sucesivamente — se convierte en un Team. Y los documentos de cada departamento viven solo en ese espacio, sin interferir con los demás.

Ahora, ¿qué pasa con un docente que presta servicios en dos departamentos? Simplemente pertenece a los dos teams correspondientes, y la plataforma gestiona automáticamente qué documentos puede ver en cada contexto. Sin configuración adicional, sin lógica personalizada.

Y hay otro punto importante que diferencia a Documenso de DocuSeal en este aspecto: el modelo de roles. En Documenso, los usuarios pueden tener roles distintos tanto a nivel de organización como dentro de cada team — puede ser Administrador, Gerente o Miembro. Esto permite una gestión de permisos granular y real. DocuSeal, en cambio, trata a todos los usuarios como administradores, lo que es un problema grave de seguridad en un entorno institucional.

En resumen: Documenso no requería ser adaptado para la FACET — ya estaba diseñado para organizaciones como la nuestra."

---

## Diapositiva 13: ¿Por qué Documenso? — Integraciones Externas

"Documenso también está diseñado para integrarse con servicios externos, y en nuestra implementación aprovechamos tres de ellas.

Para el almacenamiento de documentos, en lugar de guardar los PDFs en el disco del servidor, los delegamos a MinIO — un servidor de objetos compatible con el protocolo S3 de Amazon — que corre en la propia infraestructura de la FACET. Esto nos da escalabilidad y separa el almacenamiento de la aplicación.

Para las notificaciones por email, usamos Brevo como relay SMTP. Su capa gratuita permite hasta 300 mails por día, lo cual cubre ampliamente nuestro volumen de envíos institucionales.

Y para la autenticación, habilitamos OAuth 2.0 con Google. Esto significa que los docentes y administrativos entran al sistema directamente con su cuenta de Google de la UNT, sin tener que crear ni recordar otra contraseña. Zero fricción en la adopción."

---
