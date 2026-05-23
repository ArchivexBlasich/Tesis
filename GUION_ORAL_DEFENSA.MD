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

## Diapositiva 9: SaaS vs. On-Premise — USD 5.300/año para 20 usuarios

"Al empezar a investigar, la primera pregunta lógica era: ¿por qué no compramos algo que ya esté hecho?

Herramientas como DocuSign o Adobe Sign son excelentes, pero se comercializan como Software as a Service. Si hacemos los números, para apenas 20 usuarios el costo de licenciamiento supera los 5.300 dólares anuales — económicamente inviable para una universidad pública en nuestro contexto.

Por lo tanto, descartamos las soluciones comerciales y la investigación se centró de lleno en alternativas de código abierto que nos permitieran alojar el sistema en nuestros propios servidores, es decir, un modelo On-Premise."

---

## Diapositiva 10: DocuSeal vs. Documenso — Elegimos Documenso

"Dentro del mundo Open Source llegaron a la final dos grandes candidatos: DocuSeal y Documenso. Ambos permiten firmar documentos, pero cuando abrimos el capó y analizamos las licencias, la diferencia fue enorme para nuestro caso de uso.

DocuSeal restringe funciones vitales, como el control de acceso basado en roles, a su versión paga. Esto significa que cualquier usuario creado tendría permisos de administrador. Inviable para la facultad.

Documenso, en cambio, incluye en su versión comunitaria el control de roles, nos permite crear 'Equipos' que mapean perfectamente los distintos departamentos de la FACET, y tiene soporte nativo para autenticarnos con Google usando nuestros correos institucionales '@herrera'. Así que, sin dudarlo, Documenso fue el elegido."

---

## Diapositiva 11: [Sección 04 — Infraestructura y Arquitectura de Despliegue]

_(Transición de sección — sin texto oral, solo pasar la slide)_

---

## Diapositiva 12: Stack Tecnológico

"Ahora bien, muy lindo todo, pero ¿cómo levantamos este sistema? Les presento el stack tecnológico.

Como base de cómputo aprovechamos el servidor de la facultad que corre Proxmox. Sobre él, usamos un contenedor LXC para correr Docker. Para no administrar contenedores a mano, utilizamos Coolify — una plataforma PaaS que nos facilitó la orquestación y el manejo de variables de entorno.

Como base de datos transaccional usamos PostgreSQL. Pero atención acá: los PDFs firmados no se guardan en la base de datos, para eso usamos TrueNAS con MinIO, que es un almacenamiento de objetos compatible con S3. Esto nos permite separar la aplicación del almacenamiento.

Para los correos electrónicos integramos Brevo, que nos da un relay SMTP externo para garantizar que los mails no caigan en spam. Y finalmente, agregué Browserless — una instancia de Chrome virtual — fundamental porque la imagen de Documenso no lo traía por defecto y lo necesitábamos para renderizar el certificado visual de la firma en el PDF."

---

## Diapositiva 13: Arquitectura y Diagrama de Despliegue

"Acá es donde todo se une. Esta es la arquitectura de red y el diagrama de despliegue.

Imaginen a un profesor desde su casa en internet (la capa WAN). Su petición llega primero al router de borde de la FACET y es recibida por nuestro reverse proxy perimetral, un Nginx. Nginx maneja la seguridad SSL y reenvía el tráfico hacia adentro, al contenedor LXC donde vive nuestro orquestador Coolify.

Dentro de Coolify, tenemos otro proxy, Traefik, que enruta el tráfico hacia la red privada de Docker donde está encapsulado Documenso. Como pueden ver, Documenso se comunica internamente con PostgreSQL y con Browserless sin exponer esos puertos a internet.

Por último, fíjense en este flujo hacia MinIO. Tuvimos que resolver un desafío de red importante: Documenso requiere que el almacenamiento S3 tenga una única URL pública. Así que implementamos un contenedor proxy TCP llamado 'Socat' dentro de nuestra red virtual. Esto hace que todo el tráfico hacia el almacenamiento, ya sea que venga directo del navegador del usuario o desde el backend de Documenso, pase siempre filtrado y seguro por el proxy de la facultad antes de llegar a los discos físicos del TrueNAS. Nada queda expuesto al exterior de forma directa."

---

## Diapositiva 14: [Sección 05 — Demostración en Vivo]

_(Transición de sección — sin texto oral, solo pasar la slide)_

---

## Diapositiva 15: Conclusión y Paso a la Demo

"En conclusión, logramos una arquitectura robusta, de nivel empresarial, pero alojada en nuestros propios servidores y sin depender económicamente de un tercero. Hemos eliminado el problema del registro manual de usuarios cerrando el acceso únicamente a cuentas de Google institucionales, y tenemos un sistema de respaldo automático operando.

Todo este diseño de infraestructura se aprecia mucho mejor viéndolo funcionar. Así que ahora, en los próximos minutos, vamos a pasar a la demostración en vivo de la plataforma para que vean cómo un documento recorre todo este sistema."

_(Transición a la computadora para la demo en vivo — 5-7 minutos)_

---

## Diapositiva 16: ¡Muchas Gracias!

_(Slide final — disponible para preguntas del jurado)_
