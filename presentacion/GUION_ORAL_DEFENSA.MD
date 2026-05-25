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

"Antes de diseñar cualquier cosa, hice un relevamiento del mercado. Las tres plataformas más usadas para firma electrónica de documentos son DocuSign, Dropbox Sign y Adobe Sign. Como pueden ver en la tabla, los precios son prácticamente idénticos — entre 24 y 25 dólares por usuario por mes.

Para una institución como la FACET, con unos 20 usuarios activos, eso representa entre 480 y 500 dólares mensuales. Casi 6.000 dólares por año, en moneda extranjera, pagados a un proveedor externo.

Pero el costo económico no es el único problema. Fíjense en la columna de 'Residencia de Datos': las tres soluciones almacenan los documentos en infraestructura propia del proveedor — AWS, Azure — servidores fuera del país. Para documentación administrativa e institucional, eso es inaceptable desde el punto de vista de la soberanía de datos.

Esto descarta las opciones SaaS y nos obliga a buscar una alternativa que podamos instalar en nuestra propia infraestructura."

---

## Diapositiva 10: Plataformas Open Source Evaluadas

"Al descartar las opciones SaaS, el siguiente paso fue relevar el ecosistema open source. Las dos plataformas con mayor adopción en esta categoría son Documenso y DocuSeal — ambas se presentan como alternativas open source a DocuSign.

[Señalar tarjeta Documenso] Documenso tiene más de 12.900 estrellas en GitHub, está construido sobre TypeScript con Next.js y PostgreSQL, y permite despliegue en infraestructura propia.

[Señalar tarjeta DocuSeal] DocuSeal tiene más de 16.900 estrellas, usa Ruby on Rails con Vue.js en el frontend, y también soporta despliegue self-hosted.

Ambas cumplen con el requisito fundamental de soberanía de datos. Pero para elegir entre las dos, necesitaba hacer una comparativa más fina de sus funcionalidades concretas."

---

## Diapositiva 11: Comparativa Open Source — Documenso vs DocuSeal

"Cuando comparé las dos en detalle, emergió una diferencia crítica para el uso institucional.

[Señalar fila por fila]

La gestión de roles — que en la FACET es esencial porque hay administradores, jefes de departamento y usuarios regulares — en DocuSeal está bloqueada detrás de la Enterprise Edition. Lo mismo aplica al inicio de sesión con Google, que era un requisito para no pedirle a los docentes que creen otra contraseña. Y lo mismo para el branding personalizado.

En Documenso, las tres funcionalidades están disponibles en la Community Edition, libre y gratuita, bajo licencia AGPL-3.0.

Y tiene un detalle adicional que no es menor: mientras DocuSeal trata a todos los usuarios como administradores, Documenso implementa un modelo de roles granular tanto a nivel de organización como dentro de cada team. En un entorno institucional, eso no es un lujo, es un requisito de seguridad básico.

La elección fue Documenso."

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

## Diapositiva 14: [Sección 04 — Infraestructura y Arquitectura de Despliegue]

_(Transición de sección — sin texto oral, solo pasar la slide)_

---

## Diapositiva 15: Conceptos Clave de la Infraestructura

"Ahora que sabemos qué herramientas elegimos, veamos cómo las desplegamos concretamente.

La FACET ya contaba con un servidor físico corriendo Proxmox VE, un hipervisor open source muy usado en entornos universitarios. Proxmox nos ofrece dos modalidades de virtualización: máquinas virtuales completas a través de KVM, y contenedores ligeros a través de LXC. Nosotros optamos por un contenedor LXC, porque tiene un overhead mínimo — comparte el kernel del host y arranca en segundos — y es más que suficiente para nuestra carga de trabajo.

[CLICK]

Dentro de ese contenedor instalamos Coolify, que es el corazón operativo de todo el sistema. Coolify es una plataforma PaaS open source que gestiona el ciclo de vida completo de los servicios: despliegue, variables de entorno, actualizaciones y monitoreo, todo desde una interfaz web. Incluye Traefik como reverse proxy integrado, que se encarga automáticamente de provisionar los certificados TLS y de enrutar el tráfico HTTP hacia el servicio correcto según el dominio. Cada componente de la aplicación — Documenso, la base de datos PostgreSQL y MinIO — corre en su propio contenedor Docker, completamente aislado del resto.

[CLICK]

Y en paralelo, en un segundo servidor, tenemos el Servidor NAS. Ahí corre TrueNAS, que gestiona el almacenamiento de discos con redundancia RAID, y MinIO, que expone ese almacenamiento como un bucket compatible con el protocolo S3. De esta forma, los documentos firmados nunca viven en el mismo servidor que la aplicación — están separados físicamente, lo que simplifica los backups y mejora la resiliencia."

---

## Diapositiva 16: Diagrama General de Arquitectura

"Para cerrar esta sección, acá tienen el diagrama completo de la infraestructura.

Desde abajo hacia arriba: en la zona WAN tenemos al usuario final — un personal de la FACET — que accede desde la red universitaria o desde internet. El tráfico entra por el Router de Borde de la FACET, donde Nginx actúa como primer proxy y termina el TLS externo. Desde ahí el pedido viaja por la red interna hasta el contenedor LXC, donde Traefik lo recibe y lo despacha al contenedor Docker correspondiente — Documenso en este caso.

Si el flujo requiere enviar una notificación, Documenso la delega a Brevo vía SMTP. Si requiere autenticación, redirige al usuario al servidor de Google OAuth. Y si requiere guardar o recuperar un documento, habla directamente con MinIO en el Servidor NAS a través del protocolo S3.

Todo en la misma red institucional, sin ningún dato saliendo a la nube."

---

---

## Diapositiva 17: Stack de Documenso

i hacemos un 'zoom' dentro de la red privada que nos orquesta Coolify, llegamos al corazón del sistema: el stack de Documenso. 

Como ven en pantalla, aquí operan tres contenedores principales que se comunican de forma aislada. Primero, tenemos la base de datos **PostgreSQL**. Una decisión de diseño clave aquí fue utilizarla *exclusivamente* para guardar la metadata del sistema, es decir, el estado de los trámites, los usuarios y los permisos [1, 2]. Los archivos PDF no se guardan acá para evitar que la base de datos crezca descontroladamente y afecte el rendimiento [2].

[CLICK o señalar a Browserless]

Y en segundo lugar, pueden ver un servicio llamado **Browserless**. Este contenedor no estaba previsto en el diseño original, sino que nació de la necesidad de resolver un problema crítico de integración. 

Durante mis pruebas piloto, el sistema permitía cargar el documento y recolectaba las firmas correctamente, pero al final del proceso el trámite quedaba atrapado en un estado de 'PENDING' [3]. Analizando los registros de ejecución, detecté que el sistema fallaba al intentar generar la representación visual del certificado en el PDF porque la imagen oficial de Documenso en Docker no incluye los binarios de Chromium necesarios para dibujarlo [3, 4].

Para resolverlo de forma limpia, sin alterar la imagen oficial de Documenso ni romper su capacidad de actualización, implementé este contenedor Browserless [5]. Funciona como una instancia de Chrome virtual en segundo plano. Ahora, Documenso simplemente se conecta a él, le delega el trabajo pesado del renderizado gráfico del PDF, y el ciclo de firma se completa con éxito [5].

---

## Diapositiva 18: Dimensionamiento del Almacenamiento

"Ahora, una vez definida la arquitectura, el siguiente paso fue dimensionar el almacenamiento. Pero no asigné un número arbitrario: el cálculo parte del único límite operativo concreto que tenemos, que es el proveedor de correo.

Brevo, en su capa gratuita, permite 300 correos diarios. Cada trámite de firma genera, como mínimo, 6 notificaciones: las invitaciones a cada firmante y el aviso de finalización. Eso nos da un techo real de 50 trámites por día.

A 20 MB por trámite — considerando que MinIO guarda tanto el PDF original como la versión firmada — el crecimiento diario proyectado es de 1 GB.

Con una política de retención ILM de 5 años, que es el plazo razonable para documentos institucionales, eso nos da 1.825 TB de volumen máximo proyectado. Por eso asigné una cuota de 2 TB, con un margen de seguridad del 10%.

Y como ven en el gráfico de la izquierda: esos 2 TB representan apenas el 11% del servidor TrueNAS de la facultad. Es una asignación muy conservadora con respecto a la capacidad disponible."

---

## Diapositiva 19: Políticas de Backup y Retención

"Al operar On-Premise, la facultad asume la responsabilidad completa ante cualquier contingencia. Por eso diseñé una estrategia de backup estructurada en dos dominios con necesidades distintas.

El primero es la base de datos. PostgreSQL ejecuta un volcado lógico automático todos los días a las 3 de la mañana, que se guarda en un bucket de MinIO aislado del repositorio documental. La retención es de 30 días, lo que nos da un RPO — es decir, el máximo de datos que podemos perder — de 24 horas. Y si necesitamos restaurar, Coolify tiene integración directa para importar ese volcado desde la interfaz gráfica, sin necesidad de comandos manuales.

El segundo dominio es la configuración del entorno. Una hora después del volcado de base de datos — a las 4 de la mañana — un script bash empaqueta automáticamente los archivos docker-compose, las variables de entorno y, esto es lo más importante, el certificado de firma .p12 codificado en Base64.

¿Por qué es crítico ese certificado? Porque es lo que le da identidad institucional a cada firma generada por el sistema. Si el servidor falla por completo y recupero la base de datos pero no tengo ese certificado, no puedo emitir nuevas firmas. Con este backup, en cambio, puedo reconstruir el entorno completo en unos 30 minutos."

---

## Diapositiva 20: Rendimiento del Sistema

"Para cerrar la parte técnica, quiero mostrarles que el sistema no solo funciona correctamente, sino que lo hace con un consumo de recursos muy por debajo de lo que el hardware disponible puede ofrecer.

La captura de la izquierda es de Netdata, monitoreando en tiempo real el consumo durante una prueba de carga controlada: mandé a firmar 5 documentos al mismo tiempo.

En reposo, los cuatro contenedores juntos consumen apenas 400 MB de RAM. Durante la ráfaga, pueden ver ese comportamiento escalonado en el gráfico: ese es Browserless levantando sesiones de Chrome para renderizar los certificados en PDF. El pico de memoria llegó a 1.33 GB — con 8 GB asignados, eso es un 16% de uso. En CPU, el pico fue del 12.5%.

El resultado es claro: en el peor caso operativo que pude simular, el sistema usa el 16% de la memoria y el 12% del procesador. Tenemos más del 83% libre en RAM y casi el 88% libre en CPU. La facultad tiene margen más que holgado para escalar el uso sin necesitar más hardware."

---

## Diapositiva 21: ¿Firma Electrónica o Firma Digital?

"Antes de pasar a la demostración, quiero dejar claro el encuadre legal del sistema.

Documenso hace todo lo que la ley exige técnicamente: aplica un procedimiento matemático que identifica unívocamente al firmante, y garantiza la integridad del documento — cualquier modificación posterior invalida la firma.

Pero la Ley 25.506 tiene un requisito adicional para que algo se llame Firma Digital: el artículo 9 exige que el certificado haya sido emitido por una Autoridad Certificante licenciada por el Estado. Nosotros usamos un certificado autofirmado, generado dentro de la institución — sin ese respaldo externo.

Por eso el sistema emite Firma Electrónica, no Firma Digital. Pero eso no lo invalida: tiene plena validez administrativa dentro del ámbito de la FACET, para todos sus circuitos internos."

---

## Diapositiva 22: [Sección 05 — Demostración en Vivo]

_(Transición de sección — sin texto oral, solo pasar la slide)_

---

## Diapositiva 23: Demo en Vivo

_(~6 minutos. No hay guion oral fijo — es una demostración en pantalla con el sistema real.)_

**Secuencia de acciones:**

1. [ABRIR NAVEGADOR] Navegar a `documentos.facet.unt.edu.ar`
2. Iniciar sesión con cuenta institucional de Google UNT
3. Subir un documento PDF de prueba
4. Configurar los firmantes: agregar al menos dos destinatarios, posicionar los campos de firma en el documento
5. Enviar el trámite y mostrar el email de notificación que llega al firmante
6. Completar el proceso de firma desde el enlace del correo
7. Descargar el PDF final firmado y mostrar el sello criptográfico en el panel de validación

**Frases de apoyo durante la demo:**

- "Fíjense que el documento nunca sale de la infraestructura de la FACET — todo lo que ven acá está corriendo en el servidor físico del edificio."
- "El link que llega por email incluye un token de un solo uso — sin contraseña, sin registro."
- "Una vez que los firmantes completan el flujo, el sistema sella el PDF con el hash criptográfico y queda trazado el momento y el orden de cada firma."
- "Si abro el PDF en cualquier lector compatible con PAdES, puedo verificar la validez de la firma sin necesidad de acceder al sistema."

---

## Diapositiva 24: [Sección 06 — Preguntas]

_(Transición de sección — sin texto oral, solo pasar la slide)_

---

## Diapositiva 25: Gracias

"Eso es todo de mi parte. Muchas gracias.

Quedo a disposición del jurado."

_(Permanecer en pantalla durante las preguntas. No avanzar la slide.)_

---

## Notas Generales para la Defensa

- **Tiempo objetivo**: 20 min de presentación + 6 min de demo = 26 min totales. El tiempo límite habitual es 30 min.
- **Pausas**: Las marcas `[PAUSE]` son momentos para respirar y dejar que el jurado procese la información. No apresurar.
- **Preguntas anticipadas**:
  - *"¿Por qué no usaron una CA licenciada para emitir Firma Digital?"* → Respuesta: el proceso de licenciamiento ante la Secretaría de Modernización tiene un costo y un tiempo de tramitación que excedía el alcance del trabajo. La Firma Electrónica es suficiente para los circuitos internos de la FACET, y el diseño deja la puerta abierta para una futura integración con una CA habilitada.
  - *"¿Qué pasa si el servidor NAS falla?"* → Respuesta: MinIO corre sobre TrueNAS con RAID, que tolera la falla de un disco. Para falla total del servidor, la política de backup diario del sistema de archivos de MinIO permite restaurar hasta 24 horas atrás en otro hardware.
  - *"¿Cómo se manejan usuarios que se desvinculan de la institución?"* → Respuesta: el administrador puede desactivar la cuenta desde Coolify; el login con Google de la UNT se revoca automáticamente al dar de baja la cuenta institucional.
  - *"¿El sistema escala si la facultad crece en usuarios?"* → Respuesta: sí, los números de rendimiento muestran menos del 20% de uso en el peor caso. Además, el stack basado en Docker permite aumentar réplicas de Documenso sin modificar la infraestructura subyacente.
