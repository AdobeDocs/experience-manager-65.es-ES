---
title: Configuración de los extremos de correo electrónico
seo-title: Configuración de los extremos de correo electrónico
description: Obtenga información sobre cómo configurar los extremos de correo electrónico.
seo-description: Obtenga información sobre cómo configurar los extremos de correo electrónico.
uuid: d47bb45b-0e0e-43ca-9e25-e347d0e60206
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dcf15c42-9ec6-4d1c-ad41-083aa0b8c7ae
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '3766'
ht-degree: 0%

---


# Configuración de los extremos de correo electrónico {#configuring-email-endpoints}

Los extremos de correo electrónico permiten a los usuarios invocar un servicio mediante el envío de uno o varios documentos (como adjuntos de correo electrónico) a una cuenta de correo electrónico específica. La bandeja de entrada de correo electrónico actúa como punto de recopilación de los datos adjuntos. El servicio supervisa la bandeja de entrada y procesa los archivos adjuntos. Los resultados de la conversión se reenvían al usuario definido en el extremo.

Para un extremo de correo electrónico, los usuarios autorizados pueden invocar un proceso enviando archivos por correo electrónico a la cuenta adecuada. Los resultados se devolverán al usuario que envía la información (de forma predeterminada) o al usuario definido en la configuración del punto final.

Antes de configurar un extremo de correo electrónico, cree una cuenta de correo electrónico POP3 o IMAP para que la utilice el punto final. Configure una cuenta independiente para cada tipo de conversión. Por ejemplo, se puede configurar una cuenta para generar documentos PDF estándar a partir de archivos adjuntos entrantes y otra cuenta para generar documentos PDF seguros.

>[!NOTE]
>
>Cada dirección de correo electrónico debe asignarse a un solo extremo de correo electrónico. No puede configurar varios extremos de correo electrónico en una sola dirección de correo electrónico, aunque los extremos de correo electrónico adicionales estén deshabilitados.

Todos los extremos de correo electrónico se configuran con un nombre de usuario y una contraseña autorizados para la bandeja de entrada de correo electrónico, que son obligatorios al invocar el servicio. La cuenta de correo electrónico está protegida por el sistema de servidor de correo en el que está configurada.

Si los usuarios envían documentos con caracteres de idioma europeo occidental en nombres de archivos y rutas de conversión, deben utilizar una aplicación de correo electrónico que admita los tipos de codificación requeridos (Latin1 [ISO-8859-1], Europa Occidental [Windows] o UTF-8). Para obtener más información, consulte el documento *Instalación e implementación de AEM formularios* para su servidor de aplicaciones.

Antes de configurar un extremo de correo electrónico, configure el servicio de correo electrónico. (Consulte [Configuración de los extremos de correo electrónico predeterminados](configuring-email-endpoints.md#configure-default-email-endpoint-settings).) Los parámetros de configuración del servicio de correo electrónico tienen dos propósitos:

* Para configurar atributos comunes para todos los extremos de correo electrónico
* Proporcionar valores predeterminados para todos los extremos de correo electrónico

## Configurar SSL para un extremo de correo electrónico {#configure-ssl-for-an-email-endpoint}

Puede configurar POP3, IMAP o SMTP para utilizar la capa de sockets seguros (SSL) para un extremo de correo electrónico.

1. En el servidor de correo electrónico, habilite SSL para POP3, IMAP o SMTP según la documentación del fabricante.
1. Exporte un certificado de cliente desde el servidor de correo electrónico.
1. Utilice el programa keytool para importar el archivo de certificado de cliente al almacén de certificados de Java Virtual Machine (JVM) del servidor de aplicaciones. El procedimiento para este paso dependerá de las rutas de instalación de JVM y cliente.

   Por ejemplo, si está utilizando una instalación predeterminada de Oracle WebLogic Server con JDK 1.5.0 en Microsoft Windows Server® 2003, escriba el siguiente texto en un símbolo del sistema:

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. Cuando se le solicite, introduzca la contraseña (para Java, la contraseña predeterminada es `changeit`). Recibirá un mensaje que indica que el certificado se importó correctamente.
1. Utilice la consola de administración para agregar el extremo de correo electrónico al servicio.
1. Cree el extremo de correo electrónico en la consola de administración. Al configurar la configuración del punto final, seleccione SSL POP3/IMAP habilitado para los mensajes entrantes y SSL SMTP habilitado para los mensajes salientes y cambie las propiedades del puerto en consecuencia.

>[!NOTE]
>
>Sugerencia: Si tiene problemas al usar SSL, utilice un cliente de correo electrónico como Microsoft Outlook para comprobar si puede acceder al servidor de correo electrónico mediante SSL. Si el cliente de correo electrónico no puede acceder al servidor de correo electrónico, el problema está relacionado con la configuración del certificado o del servidor de correo electrónico.

## Configurar la configuración predeterminada del extremo de correo electrónico {#configure-default-email-endpoint-settings}

Puede utilizar la página Administración de servicios para configurar atributos comunes para todos los extremos de correo electrónico y para proporcionar valores predeterminados para todos los extremos de correo electrónico.

Para que el flujo de trabajo de los formularios reciba y gestione mensajes de correo electrónico entrantes de los usuarios, debe crear un extremo de correo electrónico para el servicio de Tarea completa. Este extremo de correo electrónico requiere una configuración adicional, como se describe en [Crear un extremo de correo electrónico para el servicio de Tarea completa](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

### Cambiar los valores predeterminados para los extremos de correo electrónico {#change-the-default-values-for-email-endpoints}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en Correo electrónico: 1.0 (el ID del componente es com.adobe.idp.dsc.provider.service.email.Email).
1. En la ficha Configuración, especifique la configuración predeterminada del extremo de correo electrónico y, a continuación, haga clic en Guardar.

### Configuración predeterminada de extremo de correo electrónico {#default-email-endpoint-settings}

**Expresión de cron:** La expresión de cron utilizada por cuarzo para programar la votación del directorio de entrada.

**Intervalo de repetición:** el número de veces que se repite la encuesta de directorio. El intervalo de repetición predeterminado es en segundos si no se especifica este valor en la configuración del extremo. El valor predeterminado es 10. Este valor no puede ser menor que 10.

**Recuento de repetición:** el número de veces que se sondea el directorio de entrada. El recuento de repetición predeterminado que se usará si no se especifica este valor en la configuración del extremo. Un valor de -1 indica la exploración indefinida del directorio. El valor predeterminado es -1.

**Retraso en inicios de trabajo:** el valor predeterminado, en segundos, de la demora antes de que el trabajo inicio para analizar el extremo. El valor predeterminado es 0.

**Tamaño de lote:** el número de correos electrónicos que procesa el receptor por escaneo para obtener un rendimiento óptimo. Un valor de -1 indica todos los correos electrónicos. El valor predeterminado es 2.

**Asincrónico:** identifica el tipo de invocación como asíncrono o sincrónico. Los procesos transitorios y sincrónicos sólo se pueden invocar sincrónicamente. El valor predeterminado es asincrónico.

**Patrón de dominio:** el patrón de nombre de dominio que se utiliza para filtrar los correos electrónicos entrantes. Por ejemplo, si se utiliza adobe.com, solo se procesará el correo electrónico de adobe.com; se omite el correo electrónico de otros dominios.

**Patrón de archivos:** los patrones de datos adjuntos de archivos entrantes que acepta el proveedor. Esto incluye archivos que tienen extensiones específicas (&amp;ast;.dat, &amp;ast;.xml), nombres específicos (datos) y expresiones compuestas en el nombre y la extensión (.[dD][aA]&#39;puerto&#39;). El valor predeterminado es &amp;ast;.&amp;ast;..

**Destinatarios de trabajo correctos:** una o varias direcciones de correo electrónico que se utilizan para enviar correos electrónicos que indican los trabajos realizados correctamente. De forma predeterminada, siempre se envía un mensaje de trabajo correcto al remitente del trabajo inicial. Se admiten hasta 100 destinatarios. Para desactivar esta configuración, deje este campo en blanco.

**Destinatarios del trabajo fallido:** una o varias direcciones de correo electrónico que se utilizan para enviar correos electrónicos para indicar que hay trabajos fallidos. De forma predeterminada, siempre se envía un mensaje de trabajo fallido al remitente que envió el trabajo inicial. Se admiten hasta 100 destinatarios. Para desactivar esta configuración, deje este campo en blanco.

**Host de bandeja de entrada:** el nombre de host de bandeja de entrada o la dirección IP que debe analizar el proveedor de correo electrónico.

**Puerto de la bandeja de entrada:** el número de puerto de la bandeja de entrada que debe analizar el proveedor de correo electrónico. Si el valor es 0, se utilizará el puerto IMAP o POP3 predeterminado.

**Protocolo de bandeja de entrada:** el protocolo de correo electrónico del extremo de correo electrónico que se va a utilizar para analizar la bandeja de entrada. Las opciones son IMAP o POP3. El servidor de correo de host de bandeja de entrada debe admitir estos protocolos.

**Tiempo de espera de la bandeja de entrada:** especifica la cantidad de tiempo que el punto final esperará antes de cancelar al intentar conectarse a la bandeja de entrada. Si no se adquiere una conexión antes de que se alcance el valor de tiempo de espera, la bandeja de entrada no se sondeará.

**Usuario de bandeja de entrada:** el nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico. Según el servidor de correo electrónico y la configuración, este nombre puede ser solamente la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.

**Contraseña de bandeja de entrada:** la contraseña del usuario de la bandeja de entrada.

**SSL POP3/IMAP habilitado:** cuando está seleccionado, habilita SSL.

**Host SMTP:** el nombre de host del servidor de correo electrónico que utiliza el proveedor de correo electrónico para enviar resultados y mensajes de error. Por ejemplo: mail.corp.example.com.

**Puerto SMTP:** el puerto que se utiliza para conectarse al servidor de correo. El valor predeterminado es 25.

**Usuario SMTP:** la cuenta de usuario del proveedor de correo electrónico que se utilizará cuando envíe un correo electrónico para obtener resultados y errores.

**Contraseña SMTP:** la contraseña de la cuenta SMTP. Algunos servidores de correo no requieren una contraseña SMTP.

**Enviar desde:** la dirección de correo electrónico (por ejemplo, user@company.com) utilizada para enviar notificaciones por correo electrónico de los resultados y errores. Si no especifica un valor Enviar desde, el servidor de correo electrónico intenta determinar la dirección de correo electrónico combinando el valor especificado en la configuración del usuario SMTP con un dominio predeterminado configurado en el servidor de correo electrónico. Si el servidor de correo electrónico no tiene un dominio predeterminado y no especifica un valor para Enviar desde, pueden producirse errores. Para asegurarse de que los mensajes de correo electrónico tienen la dirección del remitente correcta, especifique un valor para la configuración Enviar desde.

**SSL SMTP habilitado:** cuando está seleccionado, habilita SSL sobre SMTP.

**Incluir el cuerpo del mensaje de correo electrónico original como adjunto:** de forma predeterminada, cuando se envía un mensaje de correo electrónico al servidor de formularios, el texto original del mensaje se incluye en el cuerpo del mensaje. Para incluir el texto como un archivo adjunto, seleccione esta opción.

**Utilice la línea de asunto original para los mensajes de correo electrónico de resultados:** de forma predeterminada, el servidor de Forms utiliza los valores especificados en los ajustes Asunto del mensaje de correo electrónico de éxito y Asunto del mensaje de correo electrónico de error como línea de asunto al enviar los mensajes de correo electrónico de resultados. Para usar la misma línea de asunto que el correo electrónico original enviado al servidor, seleccione esta opción.

**Asunto de correo electrónico de éxito:** después de enviar un correo electrónico a un extremo de correo electrónico para inicio o continuar un proceso, recibirá un mensaje de correo electrónico de retorno del servidor de formularios de AEM. Si el correo electrónico se realiza correctamente, recibirá un mensaje de correo electrónico de éxito. Si el correo electrónico falla, recibirá un mensaje de correo electrónico de error que le informará del motivo del error. Esta configuración le permite especificar la línea de asunto de los mensajes de correo electrónico de éxito enviados para este extremo.

**Cuerpo de correo electrónico de éxito:** le permite especificar el texto principal de los mensajes de correo electrónico de éxito enviados para este extremo.

**Prefijo de asunto de correo electrónico de error:** permite especificar el texto utilizado al principio de la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo.

**Asunto de correo electrónico de error:** permite especificar la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo. Este texto se muestra después del prefijo Asunto del correo electrónico de error.

**Cuerpo de correo electrónico de error:** permite especificar la primera línea en el texto principal de los mensajes de correo electrónico de error enviados para este extremo.

**Información de resumen de correo electrónico:** cada mensaje de éxito o error incluye una sección que contiene el texto de correo electrónico original que se ha enviado al servidor de formularios. Esta configuración especifica el texto que aparece encima de esa sección.

**Validar la bandeja de entrada antes de crear/actualizar este extremo:** cuando se selecciona esta opción, el servidor de formularios comprueba si la configuración SMTP/POP3 es correcta antes de crear el extremo. Al hacer clic en Añadir, aparece un mensaje que indica si la cuenta de bandeja de entrada es válida. Si esta opción no está seleccionada, el servidor de AEM formularios crea el extremo sin validar la bandeja de entrada.

**Codificación de conjuntos de caracteres:** el formato de codificación que se va a utilizar para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que usará la mayoría de los usuarios fuera de Japón. Los usuarios de un entorno japonés pueden elegir ISO2022-JP.

**Carpeta de correo electrónico enviado con error:** especifica un directorio en el que almacenar los resultados si el servidor de correo SMTP no está operativo.

## Configuración del extremo de correo electrónico {#email-endpoint-settings}

Utilice la siguiente configuración para configurar un extremo de correo electrónico.

**Nombre:** una configuración obligatoria que identifica el punto final. No incluya un carácter &lt; porque trunca el nombre mostrado en Workspace. Si está introduciendo una dirección URL como nombre del extremo, asegúrese de que cumple las reglas de sintaxis especificadas en RFC1738.

**Descripción:** Descripción del extremo. No incluya un carácter &lt; porque trunca la descripción que se muestra en Workspace.

**Expresión Cron:** Introduzca una expresión cron si el correo electrónico debe programarse mediante una expresión cron.

**Recuento de repeticiones:** Número de veces que el extremo de correo electrónico explora la carpeta o el directorio. Un valor de -1 indica la digitalización indefinida. El valor predeterminado es -1.

**Intervalo de repetición:** la velocidad de exploración que utiliza el receptor para comprobar si hay correo entrante.

**Retraso cuando inicios de trabajo:** El tiempo de espera para analizar después de los inicios del Planificador.

**Tamaño de lote:** el número de correos electrónicos que procesa el receptor por escaneo para obtener un rendimiento óptimo. Un valor de -1 indica todos los correos electrónicos. El valor predeterminado es 2.

**Nombre de usuario:** una configuración obligatoria, que es el nombre de usuario que se utiliza al invocar un servicio de destinatario desde el correo electrónico. El valor predeterminado es SuperAdmin.

**Nombre de dominio:** una configuración obligatoria, que es el dominio del usuario. El valor predeterminado es DefaultDom.

**Patrón de dominio:** especifica los patrones de dominio del correo electrónico entrante que acepta el proveedor. Por ejemplo, si se utiliza adobe.com, solo se procesa el correo electrónico de adobe.com; se omite el correo electrónico de otros dominios.

**Patrón de archivos:** especifica los patrones de datos adjuntos de archivos entrantes que acepta el proveedor. Esto incluye archivos que tienen extensiones específicas (&amp;ast;.dat, &amp;ast;.xml), nombres específicos (datos) o expresiones compuestas en el nombre y la extensión (&amp;ast;..[dD][aA]&#39;puerto&#39;).

**Destinatarios del trabajo correctos:** una dirección de correo electrónico a la que se envían mensajes para indicar los trabajos que se han realizado correctamente. De forma predeterminada, siempre se envía un mensaje de trabajo correcto al remitente. Si escribe un remitente, los resultados del correo electrónico se envían al remitente. Se admiten hasta 100 destinatarios. Especifique destinatarios adicionales con direcciones de correo electrónico, separados por comas (,).

Para desactivar esta configuración, deje la configuración en blanco. En algunos casos, desea realizar un déclencheur de un proceso y no desea recibir una notificación por correo electrónico del resultado.

**Destinatarios de trabajo fallidos:** una dirección de correo electrónico a la que se envían mensajes para indicar que se han producido errores en los trabajos. De forma predeterminada, siempre se envía un mensaje de trabajo fallido al remitente. Si escribe un remitente, los resultados del correo electrónico se envían al remitente. Se admiten hasta 100 destinatarios. Especifique destinatarios adicionales con direcciones de correo electrónico, separados por comas (,).

Para desactivar esta configuración, deje la configuración en blanco. En algunos casos, desea realizar un déclencheur de un proceso y no desea recibir una notificación por correo electrónico del resultado.

**Host de bandeja de entrada:** el nombre de host de bandeja de entrada o la dirección IP que debe analizar el proveedor de correo electrónico.

**Puerto de bandeja de entrada:** el puerto que utiliza el servidor de correo electrónico. El valor predeterminado para POP3 es 110 y el valor predeterminado para IMAP es 143. Si SSL está habilitado, el valor predeterminado para POP3 es 995 y el valor predeterminado para IMAP es 993.

**Protocolo de bandeja de entrada:** el protocolo de correo electrónico del extremo de correo electrónico que se va a utilizar para analizar la bandeja de entrada. Los valores son IMAP o POP3. El servidor de correo de host de bandeja de entrada debe admitir estos protocolos.

**Tiempo de espera de la bandeja de entrada:** el tiempo de espera, en segundos, del proveedor de correo electrónico para que espere las respuestas de la bandeja de entrada.

**Usuario de bandeja de entrada:** el nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico. Según el servidor de correo electrónico y la configuración, este valor puede ser solo la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.

**Contraseña de bandeja de entrada:** la contraseña del usuario de la bandeja de entrada.

**SSL POP3/IMAP habilitado:** seleccione esta opción para obligar al proveedor de correo electrónico a utilizar SSL para analizar la bandeja de entrada. Asegúrese de que el servidor de correo admita SSL.

**Host SMTP:** el nombre de host del servidor de correo que utiliza el proveedor de correo electrónico para enviar resultados y mensajes de error.

**Puerto SMTP:** el valor predeterminado para el puerto SMTP es 25.

**Usuario SMTP:** la cuenta de usuario del proveedor de correo electrónico que se utilizará cuando envíe notificaciones por correo electrónico de resultados y errores.

**Contraseña SMTP:** la contraseña de la cuenta SMTP. Algunos servidores de correo no requieren una contraseña SMTP.

**Enviar desde:** la dirección de correo electrónico (por ejemplo, user@company.com) utilizada para enviar notificaciones por correo electrónico de los resultados y errores. Si no especifica un valor Enviar desde, el servidor de correo electrónico intenta determinar la dirección de correo electrónico combinando el valor especificado en la configuración del usuario SMTP con un dominio predeterminado configurado en el servidor de correo electrónico. Si el servidor de correo electrónico no tiene un dominio predeterminado y no especifica un valor para Enviar desde, pueden producirse errores. Para asegurarse de que los mensajes de correo electrónico tienen la dirección del remitente correcta, especifique un valor para la configuración Enviar desde.

**SSL SMTP habilitado:** seleccione esta opción para obligar al proveedor de correo electrónico a utilizar SSL para analizar la bandeja de entrada. Asegúrese de que el servidor de correo admita SSL.

**Carpeta de correo electrónico enviado con error:** especifica un directorio en el que almacenar los resultados si el servidor de correo SMTP no está operativo.

**asincrónico:** cuando se establece en sincrónico, se procesan todos los documentos de entrada y se devuelve una sola respuesta. Cuando se establece en asincrónico, se envía una respuesta por cada documento procesado.

Por ejemplo, se crea un extremo de correo electrónico para un servicio que toma un solo documento de Word y devuelve ese documento como archivo PDF. Se puede enviar un correo electrónico a la bandeja de entrada del extremo que contiene varios (3) documentos de Word. Cuando se procesan los tres documentos, si el extremo está configurado como sincrónico, se envía un único mensaje de correo electrónico de respuesta con los tres documentos adjuntos. Si el punto final es asincrónico, se envía un correo electrónico de respuesta después de convertir cada documento de Word a PDF. El resultado son tres correos electrónicos, cada uno con un único archivo PDF adjunto.

El valor predeterminado es asincrónico.

**Incluya el cuerpo del mensaje de correo electrónico original como datos adjuntos:** de forma predeterminada, cuando se envía un mensaje de correo electrónico al servidor de formularios, el texto original del mensaje se incluye en el cuerpo del mensaje. Para incluir el texto como un archivo adjunto, seleccione esta opción.

**Utilice la línea de asunto original para los mensajes de correo electrónico de resultados:** de forma predeterminada, el servidor de Forms utiliza los valores especificados en los ajustes Asunto del mensaje de correo electrónico de éxito y Asunto del mensaje de correo electrónico de error como línea de asunto al enviar los mensajes de correo electrónico de resultados. Para usar la misma línea de asunto que el correo electrónico original enviado al servidor, seleccione esta opción.

**Asunto de correo electrónico de éxito:** después de enviar un correo electrónico a un extremo de correo electrónico para inicio o continuar un proceso, recibirá un mensaje de correo electrónico de retorno del servidor de formularios de AEM. Si el correo electrónico se realiza correctamente, recibirá un mensaje de correo electrónico de éxito. Si el correo electrónico falla, recibirá un mensaje de correo electrónico de error que le informará del motivo del error. Esta configuración le permite especificar la línea de asunto de los mensajes de correo electrónico de éxito enviados para este extremo.

**Cuerpo de correo electrónico de éxito:** le permite especificar el texto principal de los mensajes de correo electrónico de éxito enviados para este extremo.

**Prefijo de asunto de correo electrónico de error:** permite especificar el texto utilizado al principio de la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo.

**Asunto de correo electrónico de error:** permite especificar la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo. Este texto se muestra después del prefijo Asunto del correo electrónico de error.

**Cuerpo de correo electrónico de error:** permite especificar la primera línea en el texto principal de los mensajes de correo electrónico de error enviados para este extremo.

**Información de resumen de correo electrónico:** cada mensaje de éxito o error incluye una sección que contiene el texto de correo electrónico original que se ha enviado al servidor de formularios. Esta configuración especifica el texto que aparece encima de esa sección.

**Valide la Bandeja de entrada antes de crear/actualizar este extremo:** cuando esta opción está seleccionada, el servidor de formularios comprueba si la configuración SMTP/POP3 es correcta antes de crear el extremo. Al hacer clic en Añadir, aparece un mensaje que indica si la cuenta de bandeja de entrada es válida. Si esta opción no está seleccionada, el servidor de AEM formularios crea el extremo sin validar la bandeja de entrada.

**Nombre de la operación:** este ajuste es obligatorio. Lista de operaciones que se pueden asignar al extremo de correo electrónico. La operación seleccionada aquí determina qué campos se muestran en las secciones Asignaciones de parámetros de entrada y Asignaciones de parámetros de salida.

**Asignaciones de parámetros de entrada:** se utiliza para configurar la entrada necesaria para procesar el servicio y la operación. Los dos tipos de entrada son literales y variables:

**Literal:** el correo electrónico utiliza el valor introducido en el campo al mostrarse.

**Variable:** Puede asignar una cadena del asunto, cuerpo, encabezado o dirección de correo electrónico del remitente del correo electrónico. Para ello, utilice una de las siguientes palabras clave: %SUBJECT%, %BODY%, %HEADER% o %SENDER%. Por ejemplo, si utiliza %SUBJECT%, el contenido del asunto del correo electrónico se utilizará como parámetro de entrada. Para recoger datos adjuntos, introduzca un patrón de archivo que el extremo de correo electrónico pueda utilizar para seleccionar los documentos adjuntos. Por ejemplo, al introducir &amp;ast;.pdf, se selecciona cualquier documento adjunto que tenga una extensión de nombre de archivo .pdf. Introducción de &amp;ast; selecciona cualquier documento adjunto. Al introducir example.pdf, se selecciona cualquier documento adjunto denominado example.pdf.

**Asignaciones de parámetros de salida:** se utiliza para configurar la salida del servicio y la operación. Los siguientes caracteres de los valores de asignación de parámetros de salida se expanden en el nombre del archivo adjunto:

**%** FRepresenta el nombre de archivo del archivo de origen (sin incluir una extensión).

**%** ERepresenta la extensión del archivo de origen.

Cualquier incidencia de la barra invertida (\) se sustituye por %%.

***nota **: Si el mensaje de solicitud de servicio incluye varios archivos adjuntos, no puede utilizar los parámetros %F y %E para la propiedad Asignaciones de parámetros de salida del extremo. Si la respuesta de servicios devuelve varios archivos adjuntos, no puede especificar el mismo nombre de archivo para más de un archivo adjunto. Si no sigue estas recomendaciones, el servicio invocado crea los nombres de los archivos devueltos y los nombres no son predecibles.*

Están disponibles los siguientes valores:

**Objeto único:** el proveedor de correo electrónico no tiene el destino de la carpeta de origen; los resultados se devuelven como datos adjuntos. El patrón es Result/%F.ps y devuelve Result%%sourcefilename.ps como archivo adjunto de nombre de archivo.

**Lista:** El patrón es Resultado/%F/ y devuelve Resultado%%sourcefilename%%file1 como archivo adjunto de nombre de archivo.

**Mapa:** el patrón es Resultado/%F/ y el destino de origen es Resultado%%sourcefilename%%file1 y Resultado%%sourcefilename%%file2. Si el mapa contiene más de un objeto y el patrón es Resultado/%F.ps, los archivos adjuntos del archivo de respuesta son Resultado%%sourcefilename1.ps (resultado 1) y Resultado%%sourcefilename2.ps (resultado 2).

## Crear un extremo de correo electrónico para el servicio de Tarea completa {#create-an-email-endpoint-for-the-complete-task-service}

Para que el flujo de trabajo de los formularios reciba y gestione mensajes de correo electrónico entrantes de los usuarios, debe crear un extremo de correo electrónico para el servicio de Tarea completa.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en Completar servicio de Tarea.
1. En la ficha Extremos, seleccione Correo electrónico en la lista desplegable y haga clic en Añadir.
1. En el cuadro Host de bandeja de entrada, escriba el nombre de host o la dirección IP del servidor de correo.
1. En el cuadro Usuario de la bandeja de entrada, escriba el nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico que ha creado para gestionar los envíos de formularios. Según el servidor de correo electrónico y la configuración, este nombre puede ser sólo la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.
1. En el cuadro Contraseña de bandeja de entrada, escriba la contraseña del usuario de la bandeja de entrada.
1. En el cuadro Host SMTP, escriba el nombre de host o la dirección IP del servidor de correo desde el que el proveedor de correo electrónico envía los resultados y los mensajes de error.
1. En el cuadro Usuario SMTP, escriba la cuenta de usuario del proveedor de correo electrónico que se utilizará al enviar el correo electrónico para obtener resultados y errores. Esta cuenta de usuario puede ser el mismo valor que utilizó para el usuario de la bandeja de entrada.
1. En el cuadro Contraseña SMTP, escriba la contraseña de la cuenta SMTP.
1. En la lista Nombre de la operación, seleccione invocar.
1. En la lista attachmentMap, seleccione Variable y escriba `*.*` en el cuadro adyacente. Esto envía todos los datos adjuntos de los mensajes de correo de entrada a una variable de mapa para el proceso de Tarea completa.
1. En la lista mailBody, seleccione variable y escriba `%BODY%` en el cuadro adyacente.
1. En la lista mailFrom, seleccione Variable y escriba `%SENDER%` en el cuadro adyacente. Esto asigna la dirección del remitente a los datos del proceso de Tarea completa.
1. En el cuadro de resultados, escriba `results`. Esto hace que la Tarea completa o el proceso de Inicio devuelvan una cadena de resultados.
1. Haga clic en Agregar.

