---
title: Configuración de extremos de correo electrónico
seo-title: Configuring email endpoints
description: Obtenga información sobre cómo configurar los extremos de los correos electrónicos.
seo-description: Learn how to configure email endpoints.
uuid: d47bb45b-0e0e-43ca-9e25-e347d0e60206
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dcf15c42-9ec6-4d1c-ad41-083aa0b8c7ae
exl-id: 33583a12-4f20-4146-baa4-c9854e454bbf
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '3757'
ht-degree: 0%

---

# Configuración de extremos de correo electrónico {#configuring-email-endpoints}

Los extremos de correo electrónico permiten a los usuarios invocar un servicio enviando uno o varios documentos (como archivos adjuntos de correo electrónico) a una cuenta de correo electrónico especificada. La bandeja de entrada de correo electrónico actúa como punto de recopilación de los archivos adjuntos. El servicio supervisa la bandeja de entrada y procesa los archivos adjuntos. Los resultados de la conversión se reenvían al usuario definido en el extremo.

Para un extremo de correo electrónico, los usuarios autorizados pueden invocar un proceso enviando archivos por correo electrónico a la cuenta adecuada. Los resultados se devolverán al usuario remitente (de forma predeterminada) o al usuario definido en la configuración del extremo.

Antes de configurar un extremo de correo electrónico, cree una cuenta de correo electrónico POP3 o IMAP para que la use el extremo. Configure una cuenta independiente para cada tipo de conversión. Por ejemplo, se puede configurar una cuenta para generar documentos de PDF estándar a partir de archivos adjuntos entrantes y otra cuenta para generar documentos de PDF seguros.

>[!NOTE]
>
>Cada dirección de correo electrónico debe asignarse únicamente a un extremo de correo electrónico. No puede configurar varios extremos de correo electrónico en una sola dirección, aunque los extremos de correo electrónico adicionales estén desactivados.

Todos los extremos de correo electrónico se configuran con un nombre de usuario y una contraseña autorizados para la bandeja de entrada de correo electrónico, que son necesarios al invocar el servicio. La cuenta de correo electrónico está protegida por el sistema de servidor de correo en el que está configurada.

Si los usuarios envían documentos con caracteres de idioma de Europa Occidental en nombres de ruta de archivo y conversión, deben utilizar una aplicación de correo electrónico que admita los tipos de codificación necesarios (Latin1 [ISO-8859-1], Europa Occidental [Windows] o UTF-8). Para obtener más información, consulte el documento *Instalación e implementación de AEM forms* para su servidor de aplicaciones.

Antes de configurar un extremo de correo electrónico, configure el servicio de correo electrónico. (Consulte [Configurar los parámetros de extremo de correo electrónico predeterminados](configuring-email-endpoints.md#configure-default-email-endpoint-settings)). Los parámetros de configuración del servicio de correo electrónico tienen dos propósitos:

* Para configurar atributos que sean comunes para todos los extremos de correo electrónico
* Para proporcionar valores predeterminados para todos los extremos de correo electrónico

## Configuración de SSL para un extremo de correo electrónico {#configure-ssl-for-an-email-endpoint}

Puede configurar POP3, IMAP o SMTP para que utilice Secure Sockets Layer (SSL) para un extremo de correo electrónico.

1. En el servidor de correo electrónico, habilite SSL para POP3, IMAP o SMTP según la documentación del fabricante.
1. Exporte un certificado de cliente desde el servidor de correo electrónico.
1. Utilice el programa keytool para importar el archivo de certificado de cliente al almacén de certificados de Java Virtual Machine (JVM) del servidor de aplicaciones. El procedimiento para este paso dependerá de las rutas de instalación de JVM y cliente.

   Por ejemplo, si está utilizando una instalación predeterminada de Oracle WebLogic Server con JDK 1.5.0 en Microsoft Windows Server® 2003, escriba el siguiente texto en un símbolo del sistema:

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. Cuando se le pida, introduzca la contraseña (para Java, la contraseña predeterminada es `changeit`). Recibirá un mensaje que indica que el certificado se importó correctamente.
1. Utilice la consola de administración para añadir el extremo de correo electrónico al servicio.
1. Cree el extremo de correo electrónico en la consola de administración. Al configurar los parámetros de extremo, seleccione POP3/IMAP SSL Enabled para los mensajes entrantes y SMTP SSL Enabled para los mensajes salientes, y cambie las propiedades del puerto en consecuencia.

>[!NOTE]
>
>Sugerencia: Si tiene problemas al usar SSL, utilice un cliente de correo electrónico como Microsoft Outlook para comprobar si puede acceder al servidor de correo electrónico mediante SSL. Si el cliente de correo electrónico no puede acceder al servidor de correo electrónico, el problema está relacionado con la configuración del certificado o del servidor de correo electrónico.

## Configuración de los parámetros de extremo de correo electrónico predeterminados {#configure-default-email-endpoint-settings}

Puede utilizar la página Administración de servicios para configurar atributos que son comunes para todos los extremos de correo electrónico y para proporcionar valores predeterminados para todos los extremos de correo electrónico.

Para que el flujo de trabajo de formularios reciba y gestione mensajes de correo electrónico entrantes de los usuarios, debe crear un extremo de correo electrónico para el servicio Tarea completa. Este extremo de correo electrónico requiere configuración adicional, tal como se describe en [Crear un extremo de correo electrónico para el servicio de tarea completa](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

### Cambiar los valores predeterminados para los extremos de correo electrónico {#change-the-default-values-for-email-endpoints}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios , haga clic en Correo electrónico: 1.0 (el ID de componente es com.adobe.idp.dsc.provider.service.email.Email).
1. En la ficha Configuración , especifique la configuración de extremo de correo electrónico predeterminada y, a continuación, haga clic en Guardar.

### Configuración de extremo de correo electrónico predeterminada {#default-email-endpoint-settings}

**Expresión Cron:** la expresión cron tal como la usa quartz para programar el sondeo del directorio de entrada.

**Intervalo de repetición:** el número de veces que se repite el sondeo del directorio. El intervalo de repetición predeterminado es en segundos si no se especifica este valor en la configuración del extremo. El valor predeterminado es 10. Este valor no puede ser inferior a 10.

**Recuento de repeticiones:** el número de veces que se sondea el directorio de entrada. El recuento de repetición predeterminado que se debe usar si este valor no se especifica en la configuración del extremo. Un valor de -1 indica la digitalización indefinida del directorio. El valor predeterminado es -1.

**Retraso al iniciar el trabajo:** Valor predeterminado, en segundos, del retraso antes de que el trabajo comience a analizar el extremo. El valor predeterminado es 0.

**Tamaño de lote:** el número de correos electrónicos que el receptor procesa por escaneo para obtener un rendimiento óptimo. El valor -1 indica todos los correos electrónicos. El valor predeterminado es 2.

**Asíncrono:** identifica el tipo de invocación como asíncrono o sincrónico. Los procesos transitorios y sincrónicos solo se pueden invocar sincrónicamente. El valor predeterminado es asíncrono.

**Patrón de dominio:** el patrón de nombre de dominio que se utiliza para filtrar correos electrónicos entrantes. Por ejemplo, si se utiliza adobe.com, solo se procesará el correo electrónico de adobe.com; se ignora el correo electrónico de otros dominios.

**Patrón de archivo:** los patrones de archivo adjunto entrantes que acepta el proveedor. Esto incluye archivos que tienen extensiones específicas (&amp;ast;.dat, &amp;ast;.xml), nombres específicos (datos) y expresiones compuestas en el nombre y la extensión (.[d][aA]&#39;puerto&#39;). El valor predeterminado es &amp;ast;.&amp;ast;.

**Destinatarios del trabajo correctos:** una o varias direcciones de correo electrónico que se usan para enviar correos electrónicos para indicar los trabajos que se han realizado correctamente. De forma predeterminada, siempre se envía un mensaje de trabajo correcto al remitente del trabajo inicial. Se admiten hasta 100 destinatarios. Para desactivar esta configuración, deje este campo en blanco.

**Destinatarios del trabajo con errores:** una o más direcciones de correo electrónico utilizadas para enviar correos electrónicos que indiquen los trabajos con errores. De forma predeterminada, siempre se envía un mensaje de trabajo fallido al remitente que envió el trabajo inicial. Se admiten hasta 100 destinatarios. Para desactivar esta configuración, deje este campo en blanco.

**Host de bandeja de entrada:** el nombre de host de la bandeja de entrada o la dirección IP que debe analizar el proveedor de correo electrónico.

**Puerto de la bandeja de entrada:** el número de puerto de la bandeja de entrada que debe analizar el proveedor de correo electrónico. Si el valor es 0, se utilizará el puerto IMAP o POP3 predeterminado.

**Protocolo de bandeja de entrada:** el protocolo de correo electrónico que el extremo de correo electrónico utilizará para analizar la bandeja de entrada. Las opciones son IMAP o POP3. El servidor de correo de host de la bandeja de entrada debe admitir estos protocolos.

**Tiempo de espera de la bandeja de entrada:** especifica la cantidad de tiempo que el punto final esperará antes de cancelarse al intentar conectarse a la bandeja de entrada. Si no se adquiere una conexión antes de que se alcance el valor de tiempo de espera, no se sondeará la bandeja de entrada.

**Usuario de bandeja de entrada:** el nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico. Según el servidor de correo electrónico y la configuración, este nombre solo puede ser la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.

**Contraseña de la bandeja de entrada:** la contraseña del usuario de la bandeja de entrada.

**POP3/IMAP SSL habilitado:** cuando se selecciona, activa SSL.

**Host SMTP:** el nombre de host del servidor de correo que utiliza el proveedor de correo electrónico para enviar resultados y mensajes de error. Por ejemplo, mail.example.com.

**Puerto SMTP:** puerto que se utiliza para conectar con el servidor de correo. El valor predeterminado es 25.

**Usuario SMTP:** la cuenta de usuario del proveedor de correo electrónico que se utiliza cuando envía un correo electrónico para obtener resultados y errores.

**Contraseña SMTP:** la contraseña de la cuenta SMTP. Algunos servidores de correo no requieren una contraseña SMTP.

**Enviar desde:** la dirección de correo electrónico (por ejemplo, user@company.com) que se utiliza para enviar notificaciones por correo electrónico de resultados y errores. Si no especifica un valor de Enviar desde, el servidor de correo electrónico intenta determinar la dirección de correo electrónico combinando el valor especificado en la configuración del usuario SMTP con un dominio predeterminado configurado en el servidor de correo electrónico. Si el servidor de correo electrónico no tiene un dominio predeterminado y no especifica ningún valor para Enviar desde, pueden producirse errores. Para asegurarse de que los mensajes de correo electrónico tienen la dirección de origen correcta, especifique un valor para la configuración Enviar desde .

**SMTP SSL habilitado:** cuando se selecciona, activa SSL sobre SMTP.

**Incluir el cuerpo del correo electrónico original como archivo adjunto:** de forma predeterminada, cuando se envía un correo electrónico al servidor de formularios, el texto original del mensaje se incluye en el cuerpo del mensaje. Para incluir el texto como archivo adjunto, seleccione esta opción.

**Utilice la línea del asunto original para los correos electrónicos de resultados:** de forma predeterminada, el servidor de Forms utiliza los valores especificados en los ajustes Asunto del correo electrónico de éxito y Asunto del correo electrónico de error como línea de asunto al enviar mensajes de correo electrónico de resultados. Para utilizar en su lugar la misma línea de asunto que el correo electrónico original enviado al servidor, seleccione esta opción.

**Asunto del correo electrónico de éxito:** después de enviar un correo electrónico a un extremo de correo electrónico para iniciar o continuar un proceso, recibe un mensaje de correo electrónico de retorno del servidor de formularios AEM. Si el correo electrónico se envía correctamente, recibirá un correo electrónico de éxito. Si el correo electrónico falla, recibirá un mensaje de correo electrónico de error que le informa del motivo del error. Esta configuración le permite especificar la línea de asunto de los mensajes de correo electrónico de éxito enviados para este extremo.

**Cuerpo de correo electrónico de éxito:** permite especificar el texto del cuerpo de los mensajes de correo electrónico de éxito enviados para este extremo.

**Prefijo de asunto de correo electrónico de error:** permite especificar el texto utilizado al principio de la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo.

**Asunto del correo electrónico de error:** permite especificar la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo. Este texto se muestra después del prefijo Error Email Subject .

**Cuerpo del correo electrónico de error:** permite especificar la primera línea del texto del cuerpo de los mensajes de correo electrónico de error enviados para este extremo.

**Información de resumen de correo electrónico:** cada mensaje de éxito o de error incluye una sección que contiene el texto de correo electrónico original que se envió al servidor de formularios. Esta configuración especifica el texto que aparece encima de esa sección.

**Validar la bandeja de entrada antes de crear/actualizar este extremo:** cuando se selecciona esta opción, el servidor de formularios comprueba si la configuración de SMTP/POP3 es correcta antes de crear el extremo. Al hacer clic en Agregar, aparece un mensaje que indica si la cuenta de la bandeja de entrada es válida. Si no se selecciona esta opción, el servidor de AEM forms crea el extremo sin validar la bandeja de entrada.

**Codificación de conjunto de caracteres:** el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que la mayoría de los usuarios fuera de Japón utilizarán. Los usuarios de un entorno japonés pueden elegir ISO2022-JP.

**Carpeta de correo electrónico enviado con error:** especifica un directorio en el que almacenar los resultados si el servidor de correo SMTP no está operativo.

## Configuración de extremo de correo electrónico {#email-endpoint-settings}

Utilice la siguiente configuración para configurar un extremo de correo electrónico.

**Nombre:** una configuración obligatoria que identifica el punto final. No incluya un carácter &lt; porque trunca el nombre mostrado en Workspace. Si introduce una URL como nombre del extremo, asegúrese de que cumple las reglas de sintaxis especificadas en RFC1738.

**Descripción:** Descripción del extremo. No incluya un carácter &lt; porque trunca la descripción mostrada en Workspace.

**Expresión Cron:** introduzca una expresión cron si el correo electrónico debe programarse usando una expresión cron.

**Recuento de repeticiones:** número de veces que el extremo del correo electrónico explora la carpeta o el directorio. Un valor de -1 indica escaneo indefinido. El valor predeterminado es -1.

**Intervalo de repetición:** la velocidad de digitalización que utiliza el receptor para comprobar el correo entrante.

**Retraso al iniciar el trabajo:** tiempo de espera para el análisis después de que se inicie el planificador.

**Tamaño de lote:** el número de correos electrónicos que el receptor procesa por escaneo para obtener un rendimiento óptimo. El valor -1 indica todos los correos electrónicos. El valor predeterminado es 2.

**Nombre de usuario:** una configuración obligatoria, que es el nombre de usuario que se utiliza al invocar un servicio de destinatario desde el correo electrónico. El valor predeterminado es SuperAdmin.

**Nombre de dominio:** una configuración obligatoria, que es el dominio del usuario. El valor predeterminado es DefaultDom.

**Patrón de dominio:** especifica los patrones de dominio del correo electrónico entrante que acepta el proveedor. Por ejemplo, si se utiliza adobe.com, solo se procesa el correo electrónico de adobe.com; se ignora el correo electrónico de otros dominios.

**Patrón de archivo:** especifica los patrones de archivo adjunto entrantes que acepta el proveedor. Esto incluye archivos que tienen extensiones específicas (&amp;ast;.dat, &amp;ast;.xml), nombres específicos (datos) o expresiones compuestas en el nombre y la extensión (&amp;ast;.[d][aA]&#39;puerto&#39;).

**Destinatarios del trabajo correctos:** una dirección de correo electrónico a la que se envían mensajes para indicar los trabajos que se han realizado correctamente. De forma predeterminada, siempre se envía un mensaje de trabajo correcto al remitente. Si escribe el remitente, los resultados del correo electrónico se envían al remitente. Se admiten hasta 100 destinatarios. Especifique destinatarios adicionales con direcciones de correo electrónico, separados por comas (,).

Para desactivar esta configuración, deje la configuración en blanco. En algunos casos, se desea almacenar en déclencheur un proceso y no se desea enviar una notificación por correo electrónico del resultado.

**Destinatarios de trabajos fallidos:**  dirección de correo electrónico a la que se envían mensajes para indicar los trabajos fallidos. De forma predeterminada, siempre se envía un mensaje de trabajo fallido al remitente. Si escribe el remitente, los resultados del correo electrónico se envían al remitente. Se admiten hasta 100 destinatarios. Especifique destinatarios adicionales con direcciones de correo electrónico, separados por comas (,).

Para desactivar esta configuración, deje la configuración en blanco. En algunos casos, se desea almacenar en déclencheur un proceso y no se desea enviar una notificación por correo electrónico del resultado.

**Host de bandeja de entrada:** el nombre de host de la bandeja de entrada o la dirección IP que debe analizar el proveedor de correo electrónico.

**Puerto de la bandeja de entrada:** puerto que utiliza el servidor de correo electrónico. El valor predeterminado para POP3 es 110 y el valor predeterminado para IMAP es 143. Si SSL está habilitado, el valor predeterminado para POP3 es 995 y el valor predeterminado para IMAP es 993.

**Protocolo de bandeja de entrada:** el protocolo de correo electrónico que el extremo de correo electrónico utilizará para analizar la bandeja de entrada. Los valores son IMAP o POP3. El servidor de correo de host de la bandeja de entrada debe admitir estos protocolos.

**Tiempo de espera de la bandeja de entrada:** tiempo de espera, en segundos, que el proveedor de correo electrónico espera para las respuestas de la bandeja de entrada.

**Usuario de la bandeja de entrada:** el nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico. Según el servidor de correo electrónico y la configuración, este valor puede ser solo la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.

**Contraseña de la bandeja de entrada:** la contraseña del usuario de la bandeja de entrada.

**POP3/IMAP SSL habilitado:** seleccione esta configuración para obligar al proveedor de correo electrónico a utilizar SSL para escanear la bandeja de entrada. Asegúrese de que su servidor de correo sea compatible con SSL.

**Host SMTP:** el nombre de host del servidor de correo que utiliza el proveedor de correo electrónico para enviar resultados y mensajes de error.

**Puerto SMTP:** el valor predeterminado del puerto SMTP es 25.

**Usuario SMTP:** la cuenta de usuario del proveedor de correo electrónico que se utiliza cuando envía notificaciones por correo electrónico de resultados y errores.

**Contraseña SMTP:** la contraseña de la cuenta SMTP. Algunos servidores de correo no requieren una contraseña SMTP.

**Enviar desde:** la dirección de correo electrónico (por ejemplo, user@company.com) que se utiliza para enviar notificaciones por correo electrónico de resultados y errores. Si no especifica un valor de Enviar desde, el servidor de correo electrónico intenta determinar la dirección de correo electrónico combinando el valor especificado en la configuración del usuario SMTP con un dominio predeterminado configurado en el servidor de correo electrónico. Si el servidor de correo electrónico no tiene un dominio predeterminado y no especifica ningún valor para Enviar desde, pueden producirse errores. Para asegurarse de que los mensajes de correo electrónico tienen la dirección de origen correcta, especifique un valor para la configuración Enviar desde .

**SMTP SSL habilitado:** seleccione esta configuración para obligar al proveedor de correo electrónico a utilizar SSL para explorar la bandeja de entrada. Asegúrese de que su servidor de correo sea compatible con SSL.

**Carpeta de correo electrónico enviado con error:** especifica un directorio en el que almacenar los resultados si el servidor de correo SMTP no está operativo.

**asíncrono:** cuando se establece en sincrónico, se procesan todos los documentos de entrada y se devuelve una sola respuesta. Cuando se establece como asíncrono, se envía una respuesta a cada documento que se procesa.

Por ejemplo, se crea un extremo de correo electrónico para un servicio que toma un solo documento de Word y devuelve ese documento como archivo PDF. Se puede enviar un correo electrónico a la bandeja de entrada del extremo que contiene varios (3) documentos de Word. Cuando se procesan los tres documentos, si el punto final está configurado como sincrónico, se envía un único correo electrónico de respuesta con los tres documentos adjuntos. Si el extremo es asincrónico, se envía un correo electrónico de respuesta después de convertir cada documento de Word a PDF. El resultado son tres correos electrónicos, cada uno con un único archivo adjunto de PDF.

El valor predeterminado es asíncrono.

**Incluir el cuerpo del correo electrónico original como archivo adjunto:** De forma predeterminada, cuando se envía un correo electrónico al servidor de formularios, el texto original del mensaje se incluye en el cuerpo del mensaje. Para incluir el texto como archivo adjunto, seleccione esta opción.

**Utilice la línea de asunto original para los correos electrónicos de resultados:** De forma predeterminada, el servidor de Forms utiliza los valores especificados en los ajustes Sujeto de correo electrónico de éxito y Asunto de correo electrónico de error como línea de asunto al enviar mensajes de correo electrónico de resultados. Para utilizar en su lugar la misma línea de asunto que el correo electrónico original enviado al servidor, seleccione esta opción.

**Asunto del correo electrónico de éxito:** después de enviar un correo electrónico a un extremo de correo electrónico para iniciar o continuar un proceso, recibe un mensaje de correo electrónico de retorno del servidor de formularios AEM. Si el correo electrónico se envía correctamente, recibirá un correo electrónico de éxito. Si el correo electrónico falla, recibirá un mensaje de correo electrónico de error que le informa del motivo del error. Esta configuración le permite especificar la línea de asunto de los mensajes de correo electrónico de éxito enviados para este extremo.

**Cuerpo de correo electrónico de éxito:** permite especificar el texto del cuerpo de los mensajes de correo electrónico de éxito enviados para este extremo.

**Prefijo de asunto de correo electrónico de error:** permite especificar el texto utilizado al principio de la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo.

**Asunto del correo electrónico de error:** permite especificar la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo. Este texto se muestra después del prefijo Error Email Subject .

**Cuerpo del correo electrónico de error:** permite especificar la primera línea del texto del cuerpo de los mensajes de correo electrónico de error enviados para este extremo.

**Información de resumen de correo electrónico:** cada mensaje de éxito o de error incluye una sección que contiene el texto de correo electrónico original que se envió al servidor de formularios. Esta configuración especifica el texto que aparece encima de esa sección.

**Valide la bandeja de entrada antes de crear/actualizar este extremo:**  cuando se selecciona esta opción, el servidor de formularios comprueba si la configuración de SMTP/POP3 es correcta antes de crear el extremo. Al hacer clic en Agregar, aparece un mensaje que indica si la cuenta de la bandeja de entrada es válida. Si no se selecciona esta opción, el servidor de AEM forms crea el extremo sin validar la bandeja de entrada.

**Nombre de la operación:** esta configuración es obligatoria. Lista de operaciones que se pueden asignar al extremo de correo electrónico. La operación que seleccione aquí determina qué campos se muestran en las secciones Asignaciones de parámetros de entrada y Asignaciones de parámetros de salida .

**Asignaciones de parámetros de entrada:** se utiliza para configurar la entrada necesaria para procesar el servicio y la operación. Los dos tipos de entrada son literales y variables:

**Literal:** el correo electrónico utiliza el valor introducido en el campo tal como se muestra.

**Variable:** puede asignar una cadena del asunto, el cuerpo, el encabezado o la dirección de correo electrónico del remitente del correo electrónico. Para ello, utilice una de las siguientes palabras clave: %SUBJECT%, %BODY%, %HEADER% o %SENDER%. Por ejemplo, si utiliza %SUBJECT%, el contenido del asunto del correo electrónico se utilizará como parámetro de entrada. Para recoger archivos adjuntos, introduzca un patrón de archivo que el extremo de correo electrónico pueda utilizar para seleccionar los documentos adjuntos. Por ejemplo, al introducir &amp;ast;.pdf, se selecciona cualquier documento adjunto que tenga una extensión de nombre de archivo .pdf. Introducción de &amp;ast; selecciona cualquier documento adjunto. Al introducir example.pdf, se selecciona cualquier documento adjunto denominado example.pdf.

**Asignaciones de parámetros de salida:** se utiliza para configurar la salida del servicio y la operación. Los siguientes caracteres en los valores de asignación de parámetros de salida se expanden en el nombre del archivo adjunto:

**%** FR representa el nombre de archivo del archivo de origen (sin incluir una extensión).

**%** ER representa la extensión del archivo de origen.

Cualquier incidencia de la barra invertida (\) se sustituye por %%.

***nota **: Si el mensaje de solicitud de servicio incluye varios archivos adjuntos, no puede usar los parámetros %F y %E para la propiedad Asignaciones de parámetros de salida del extremo. Si la respuesta de servicios devuelve varios archivos adjuntos, no se puede especificar el mismo nombre de archivo para más de un archivo adjunto. Si no sigue estas recomendaciones, el servicio invocado crea los nombres de los archivos devueltos y los nombres no son predecibles.*

Los valores disponibles son los siguientes:

**Objeto único:** el proveedor de correo electrónico no tiene el destino de la carpeta de origen; los resultados se devuelven como datos adjuntos. El patrón es Result/%F.ps y devuelve Result%%sourcefilename.ps como archivo adjunto de nombre de archivo.

**Lista:** el patrón es Result/%F/ y devuelve Result%%sourcefilename%%file1 como archivo adjunto de nombre de archivo.

**Mapa:** el patrón es Result/%F/ y el destino de origen es Result%%sourcefilename%%file1 y Result%%sourcefilename%%file2. Si el mapa contiene más de un objeto y el patrón es Result/%F.ps, los archivos adjuntos del archivo de respuesta son Result%%sourcefilename1.ps (output 1) y Result%%sourcefilename2.ps (output 2).

## Creación de un extremo de correo electrónico para el servicio Tarea completa {#create-an-email-endpoint-for-the-complete-task-service}

Para que el flujo de trabajo de formularios reciba y gestione mensajes de correo electrónico entrantes de los usuarios, debe crear un extremo de correo electrónico para el servicio Tarea completa.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios , haga clic en el servicio Completar tarea .
1. En la pestaña Endpoints , seleccione Email en la lista desplegable y haga clic en Add .
1. En el cuadro Host de bandeja de entrada, escriba el nombre de host o la dirección IP del servidor de correo.
1. En el cuadro Usuario de bandeja de entrada, escriba el nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico que creó para administrar los envíos de formularios. Según el servidor de correo electrónico y la configuración, este nombre puede ser solo la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.
1. En el cuadro Contraseña de la bandeja de entrada, escriba la contraseña del usuario de la bandeja de entrada.
1. En el cuadro Host SMTP, escriba el nombre de host o la dirección IP del servidor de correo desde el que el proveedor de correo electrónico envía los resultados y mensajes de error.
1. En el cuadro Usuario SMTP, escriba la cuenta de usuario del proveedor de correo electrónico que se utilizará cuando envíe correos electrónicos para obtener resultados y errores. Esta cuenta de usuario puede ser el mismo valor que utilizó para el usuario de la bandeja de entrada.
1. En el cuadro Contraseña SMTP, escriba la contraseña de la cuenta SMTP.
1. En la lista Nombre de la operación, seleccione invocar.
1. En la lista attachmentMap, seleccione Variable y escriba `*.*` en el cuadro adyacente. Esto envía todos los archivos adjuntos de los mensajes de correo entrantes a una variable de asignación para el proceso Tarea completa.
1. En la lista mailBody, seleccione la variable y escriba `%BODY%` en el cuadro adyacente.
1. En la lista mailFrom, seleccione Variable y escriba `%SENDER%` en el cuadro adyacente. Esto asigna la dirección del remitente a los datos de proceso Completar tarea .
1. En el cuadro de resultados, escriba `results`. Esto hace que la tarea completa o el proceso de inicio devuelvan una cadena de resultado.
1. Haga clic en Agregar.
