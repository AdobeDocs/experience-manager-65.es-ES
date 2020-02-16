---
title: Configuración de la configuración del servicio
seo-title: Configuración de la configuración del servicio
description: Obtenga información sobre cómo configurar los servicios.
seo-description: Obtenga información sobre cómo configurar los servicios.
uuid: e95425a4-62f6-473e-b21b-d081c432e02d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 2fab4b0c-e5db-47cd-b85a-4ff5ad6eb178
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Configuración de la configuración del servicio {#configure-service-settings}

Puede utilizar la página Administración de servicios para configurar las opciones de cada uno de los servicios que forman parte de los formularios AEM. La configuración disponible varía en función del servicio que se esté configurando.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. Detenga el servicio antes de cambiarlo. (Consulte [Inicio y parada de servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)).
1. Haga clic en el nombre del servicio que desee configurar.
1. Si el servicio tiene una ficha Configuración, utilícela para cambiar la configuración del servicio. Consulte la lista de vínculos siguiente para obtener más información.

   >[!NOTE]
   >
   >No todos los servicios enumerados en la página Administración de servicios tienen una ficha Configuración. Para los procesos que ha creado, la ficha Configuración aparece sólo si ha agregado un parámetro de configuración al proceso en Workbench. (Consulte &quot;Parámetros de configuración&quot; en la Ayuda [de](https://www.adobe.com/go/learn_aemforms_workbench_63) Workbench.)


1. Haga clic en la ficha Seguridad y defina la configuración de seguridad del servicio. Consulte [Modificación de la configuración de seguridad de un servicio](configure-service-settings.md#modifying-security-settings-for-a-service).
1. Si el servicio tiene una ficha Extremos, utilícela para cambiar la configuración del extremo. Consulte [Administración de extremos](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md).
1. Haga clic en la ficha Agrupación y defina la configuración del agrupamiento. Consulte [Configuración del agrupamiento para un servicio](configure-service-settings.md#configuring-pooling-for-a-service).
1. Haga clic en Guardar para guardar los cambios o en Cancelar para descartarlos.
1. Seleccione la casilla de verificación situada junto al nombre del servicio y haga clic en Iniciar para reiniciar el servicio.

## Ajustes del servicio Flujo de trabajo de auditoría {#audit-workflow-service-settings}

Workbench permite registrar instancias de proceso tal como se ejecutan en tiempo de ejecución y, a continuación, reproducirlas para observar el comportamiento del proceso. (Consulte la Ayuda [de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).) Para conservar espacio en el sistema de archivos del servidor de formularios, puede limitar la cantidad de datos de registro de procesos almacenados. Puede configurar las siguientes propiedades del servicio Servicio de flujo de trabajo de auditoría ( `AuditWorkflowService`):

**** maxNumberOfRecordingInstances: Número máximo de grabaciones almacenadas. Cuando se almacena el número máximo, la grabación más antigua se elimina del sistema de archivos cuando se crea una nueva grabación. Esta propiedad resulta útil si suele crear muchas grabaciones y desea eliminar las grabaciones antiguas automáticamente. El valor predeterminado es 50.

**** MaxNumberOfRecordingEntries: El número máximo de entradas de datos que se pueden almacenar para cada grabación. Las entradas de datos son información sobre las operaciones del proceso. Se almacenan varias entradas para cada ejecución de una operación, como por ejemplo, si la operación se inició, si la operación se completó y si la ruta que lleva a la operación está completa. Esta propiedad es útil cuando los procesos pueden incluir muchas ejecuciones de operaciones, por ejemplo, cuando se encuentra un bucle interminable. El valor predeterminado es 50.

## configuración del servicio de formularios con código de barras {#barcoded-forms-service-settings}

El servicio de formularios con códigos de barras `(BarcodedFormsService)` extrae datos de códigos de barras de imágenes digitalizadas. El servicio acepta un formulario con código de barras (TIFF o PDF) como entrada y extrae la representación automática de los datos codificados por el código de barras.

Los siguientes ajustes están disponibles para el servicio de formularios con códigos de barras.

**** Leer a la izquierda: Cuando se selecciona, las imágenes de código de barras se escanean horizontalmente de derecha a izquierda.

**** A la derecha: Cuando se selecciona, las imágenes de códigos de barras se analizan horizontalmente de izquierda a derecha.

**** Leer: Cuando se selecciona, las imágenes de código de barras se escanean verticalmente de abajo a arriba.

**** Leer hacia abajo: Cuando se selecciona, las imágenes de código de barras se escanean verticalmente de arriba abajo.

***Nota **: De forma predeterminada, se seleccionan todas las opciones. Anule la selección de una opción solo si está seguro de que no aparecen códigos de barras de ese modo en los formularios.*

**** Ruta del archivo base: Ruta del archivo relativa a la cual se resuelven los parámetros de archivo de entrada y salida por lotes para las operaciones Ejecutar trabajo de archivo XML y Ejecutar trabajo de archivo plano. En las configuraciones agrupadas, la ruta de acceso del archivo base debe ser una ubicación del sistema de archivos compartido a la que todos los nodos del clúster tengan acceso de lectura y escritura.

**** Nombre de fuente de datos: Nombre del origen de datos utilizado para mantener información de estado e historial sobre los trabajos de procesamiento por lotes. La fuente de datos especificada debe admitir transacciones globales (XA).

## Configuración del servicio Central Migration Bridge (obsoleto) {#central-migration-bridge-service-settings}

El servicio Central Migration Bridge ( `CentralMigrationBridge`) invoca un subconjunto de la funcionalidad de Adobe Central Pro Output Server (Central), que incluye los comandos JFMERGE, JFTRANS y XMLIMPORT. Las operaciones del servicio Central Migration Bridge permiten reutilizar los siguientes recursos de Central en formularios AEM:

* diseño de plantilla (&amp;ast;.ifd)
* plantillas de salida (&amp;ast;.mdf)
* archivos de datos (&amp;último;.dat)
* archivos de preámbulo (&amp;ast;.pre)
* archivos de definición de datos (&amp;ast;.tdf)

El siguiente ajuste está disponible para el servicio Central Migration Bridge.

**** Directorio de instalación central: Directorio en el que está instalado Adobe Central 5.7.

## Conector de Repositorio de Contenido para la Configuración de Servicio de Documentum de EMC {#content-repository-connector-for-emc-documentum-service-settings}

Content Repository Connector para el servicio Documentum de EMC ( `EMCDocumentumContentRepositoryConnector`) permite crear procesos que interactúan con el contenido almacenado en un repositorio de Documentum.

El siguiente ajuste está disponible para el servicio Conector de repositorio de contenido para Documentum de EMC.

**** Ruta predeterminada del objeto de vínculo de recurso: La parte predeterminada de la ruta en el repositorio de Documentum para almacenar el objeto Asset Link. La ruta de acceso real consiste en la ruta predeterminada y la ubicación de la plantilla de formulario en el repositorio de formularios de AEM.

Por ejemplo, si la ruta de acceso predeterminada se establece en `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`y la plantilla de formulario se almacena en una carpeta `/Docbase/forms/`, el objeto Vínculo de recurso se almacena en la siguiente ubicación:

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

El valor predeterminado de esta configuración es `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## Conector de repositorio de contenido para configuración de servicio de IBM FileNet {#content-repository-connector-for-ibm-filenet-service-settings}

Content Repository Connector para IBM FileNet permite crear procesos que interactúan con contenido almacenado en un repositorio de IBM FileNet.

El siguiente ajuste está disponible para el conector de repositorio de contenido para el servicio IBM FileNet.

**** Ruta predeterminada del objeto de vínculo de recurso: La parte predeterminada de la ruta en el repositorio de IBM FileNet para almacenar el objeto Asset Link. La ruta de acceso real consiste en la ruta predeterminada y la ubicación de la plantilla de formulario en el repositorio de formularios de AEM.

Por ejemplo, si la ruta de acceso predeterminada se establece en `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`y la plantilla de formulario se almacena en una carpeta `/Docbase/forms/`, el objeto Vínculo de recurso se almacena en la siguiente ubicación:

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

El valor predeterminado de esta configuración es `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## Convertir configuración del servicio PDF {#convert-pdf-service-settings}

El servicio Convertir PDF ( `ConvertPdfService`) convierte documentos PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF). Convertir un documento PDF a PostScript es útil para la impresión desatendida basada en servidor en cualquier impresora PostScript. Convertir un documento PDF en un archivo TIFF de varias páginas resulta práctico al archivar documentos en sistemas de administración de contenido que no admiten documentos PDF.

Los siguientes ajustes están disponibles para el servicio Convertir PDF.

**** Tipo de transacción: Especifica cómo se debe propagar un contexto de transacción a una operación.

**** Requerido: Admite un contexto de transacción si existe uno; de lo contrario, se crea un nuevo contexto de transacción. Este es el valor predeterminado.

**** Requiere nuevo: Siempre crea un nuevo contexto de transacción. Si existe un contexto de transacción activo, se suspende.

**** Tiempo de espera de transacción (en segundos): El número de segundos que el proveedor de transacciones subyacente debe esperar antes de revertir una transacción que está ajustando esta operación. Este valor se ignorará si se propaga un contexto de transacción existente. El valor predeterminado es 180.

**** Resolución de umbral para afinación (en ppp): La resolución de imagen por debajo de la cual se aplica el suavizado (o suavizado) al texto, al arte lineal y a las imágenes, si ha seleccionado las opciones &quot;Aplicar suavizado a&quot; para esos elementos.

**** Aplicar suavizado al texto: Controla el suavizado del texto. Para desactivar el suavizado de texto y hacer que el texto sea más nítido y fácil de leer con un ampliador de pantalla, desactive esta casilla de verificación.

**** Aplicar suavizado a LineArt: Aplica suavizado para eliminar ángulos abruptos en las líneas.

**** Aplicar suavizado a las imágenes: Aplica suavizado para minimizar los cambios bruscos en las imágenes.

## Configuración del servicio Distiller {#distiller-service-settings}

El servicio Distiller ( `DistillerService`) convierte archivos PostScript, PostScript encapsulado (EPS) y PRN en archivos PDF a través de una red.

Los siguientes ajustes están disponibles para el servicio Distiller.

**** Configuración de Adobe PDF: Los siguientes ajustes preconfigurados se aplican al PDF generado:

* Impresión de alta calidad
* Páginas de gran tamaño
* PDFA1b CMYK 2005
* PDFA1b RGB 2005
* PDFX1a 2001
* PDFX3 2002
* Calidad de la prensa
* Tamaño de archivo más pequeño
* Estándar

La nueva configuración se puede crear a través de la interfaz de usuario de PDF Generator.

**** Configuración de seguridad: Configuración de seguridad preconfigurada que se aplica a documentos PDF generados. El valor predeterminado es Sin seguridad. Debe crear la configuración de seguridad mediante el generador de PDF y, a continuación, introducir la configuración aquí.

**** Tamaño del grupo: El tamaño inicial de la piscina. Cuando se implementa el servicio Distiller, este número se utiliza para determinar el número de instancias de implementación de servicio que se crean y asignan al grupo gratuito en espera de solicitudes de invocación. El contenedor de servicios puede responder inmediatamente a las solicitudes de invocación sin tener que inicializar primero una instancia de servicio.

## Configuración del servicio de Administración de documentos {#document-management-service-settings}

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, monitorear y optimizar procesos centrados en el ser humano. La compatibilidad con Content Services (obsoleto) finaliza el 31/12/2014. Consulte el documento [de ciclo vital del producto de](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)Adobe. Para obtener información sobre la configuración de Content Services (obsoleto), consulte [Administración de Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

El servicio de administración de documentos ( `DocumentManagementService`) permite a los procesos utilizar la funcionalidad de administración de contenido proporcionada por Content Services (obsoleto). Las operaciones de Administración de documentos proporcionan tareas básicas que son necesarias para mantener espacios y contenido en el sistema de administración de contenido. Algunos ejemplos de estas tareas son copiar, eliminar, mover, recuperar y almacenar contenido, crear espacios y asociaciones, y obtener y establecer atributos de contenido.

Los siguientes ajustes están disponibles para el servicio de administración de documentos.

**** Esquema de almacenamiento: Esquema del almacén en el que se encuentra el contenido. El valor predeterminado es área de trabajo.

**** Puerto HTTP: El puerto utilizado para acceder a Content Services (obsoleto). El valor predeterminado es 8080.

## Configuración del servicio de correo electrónico {#email-service-settings}

El correo electrónico se utiliza generalmente para distribuir contenido o proporcionar información de estado como parte de un proceso automatizado. El servicio de correo electrónico ( `EmailService`) permite a los procesos recibir mensajes de correo electrónico de un servidor POP3 o IMAP y enviar mensajes de correo electrónico a un servidor SMTP.

Por ejemplo, un proceso utiliza el servicio de correo electrónico para enviar un mensaje de correo electrónico con un archivo adjunto de formulario PDF. El servicio de correo electrónico se conecta a un servidor SMTP para enviar el mensaje de correo electrónico con los datos adjuntos. El formulario PDF está diseñado para permitir que el destinatario haga clic en Enviar después de completar el formulario. La acción hace que el formulario se devuelva como datos adjuntos al servidor de correo electrónico designado. El servicio Correo electrónico recupera el mensaje de correo electrónico devuelto y almacena el formulario completado en una variable de formulario de datos de proceso.

Los siguientes ajustes están disponibles para el servicio de correo electrónico.

**** Host SMTP: Dirección IP o dirección URL del servidor SMTP que se va a utilizar para enviar correo electrónico.

**** Número de puerto SMTP: El puerto utilizado para conectarse al servidor SMTP.

**** Autentificación SMTP: Seleccione si se requiere autenticación de usuario para conectarse al servidor SMTP.

**** Usuario SMTP: El nombre de usuario de la cuenta de usuario que se va a utilizar para iniciar sesión en el servidor SMTP.

**** Contraseña SMTP: La contraseña asociada a la cuenta de usuario SMTP.

**** Seguridad de transporte SMTP: Protocolo de seguridad que se utilizará para la conexión al servidor SMTP:

* Seleccione Ninguno si no se utiliza ningún protocolo (los datos se envían en texto sin formato)
* Seleccione SSL si se utiliza el protocolo Capa de sockets seguros.
* Seleccione TLS si se utiliza Seguridad de la capa de transporte.

**** Host POP3/IMAP: Dirección IP o dirección URL del servidor POP3 o IMAP que se va a utilizar para enviar correo electrónico.

**** Nombre de usuario POP3/IMAP: El nombre de usuario de la cuenta de usuario que se va a utilizar para iniciar sesión en el servidor POP3 o IMAP.

**** Contraseña POP3/IMAP: La contraseña asociada a la cuenta de usuario POP3 o IMAP.

**** Número de puerto POP3/IMAP: El puerto utilizado para conectarse al servidor POP3 o IMAP.

**** POP3/IMAP: Protocolo que se utiliza para enviar y recibir correos electrónicos.

**** Recibir seguridad de transporte: Protocolo de seguridad que se utilizará para la conexión al servidor SMTP:

* Seleccione Ninguno si no se utiliza ningún protocolo (los datos se envían en texto sin formato).
* Seleccione SSL si se utiliza el protocolo Capa de sockets seguros.
* Seleccione TLS si se utiliza Seguridad de la capa de transporte.

## Configuración del servicio de cifrado {#encryption-service-settings}

El servicio Cifrado ( `EncryptionService`) permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Un usuario autorizado puede descifrar el documento para obtener acceso al contenido. Si un documento PDF está codificado con una contraseña, el usuario debe especificar la contraseña abierta antes de poder ver el documento en Adobe Reader o Adobe Acrobat. Del mismo modo, si un documento PDF está cifrado con un certificado, el usuario debe descifrar el documento PDF con la clave pública correspondiente al certificado (clave privada) que se utilizó para cifrar el documento PDF.

El servicio Cifrado dispone de las siguientes opciones de configuración.

**** Servidor LDAP predeterminado al que conectarse: Nombre de host del servidor LDAP utilizado para recuperar certificados para el cifrado de documentos.

**** Puerto LDAP predeterminado al que conectarse: Número de puerto del servidor LDAP.

**** Nombre de usuario LDAP predeterminado: Si el servidor LDAP requiere autenticación, especifique el nombre de usuario que se utilizará para conectarse al servidor LDAP.

**** Contraseña LDAP predeterminada: Si el servidor LDAP requiere autenticación, especifique la contraseña que corresponde al nombre de usuario que se va a utilizar para conectarse al servidor LDAP.

***Nota **: Utilice la autenticación simple (nombre de usuario y contraseña) únicamente cuando la conexión esté protegida mediante SSL (mediante LDAPS).*

**Modo de compatibilidad:**

## Configuración del servicio FTP {#ftp-service-settings}

El servicio FTP ( `FTP`) permite que los procesos interactúen con un servidor FTP. Las operaciones del servicio FTP pueden recuperar archivos del servidor FTP, colocarlos en el servidor FTP y eliminar archivos del servidor FTP. Por ejemplo, los documentos como los informes generados a partir de un proceso pueden almacenarse en un servidor FTP para su distribución. O bien, un sistema externo puede generar algunos archivos en función de los pasos anteriores de un proceso. En un paso posterior del proceso, los archivos pueden transferirse a una ubicación remota.

Los siguientes ajustes están disponibles para el servicio FTP.

**** Host predeterminado: Dirección IP o dirección URL del servidor FTP.

**** Puerto predeterminado: El puerto utilizado para conectarse al servidor FTP. El valor predeterminado es 21.

**** Nombre de usuario predeterminado: Nombre de la cuenta de usuario que puede utilizar para acceder al servidor FTP. La cuenta de usuario debe tener suficientes privilegios para realizar las operaciones de FTP que este servicio requiere.

**** Contraseña predeterminada: La contraseña que se usará con el nombre de usuario especificado para la autenticación con el servidor FTP.

## Generar configuración de servicio PDF {#generate-pdf-service-settings}

El servicio Generar PDF ( `GeneratePDFService`) convierte los archivos en diversos formatos nativos en documentos PDF y convierte los documentos PDF a varios formatos de archivo.

Los siguientes ajustes están disponibles para el servicio Generar PDF.

**** Configuración de Adobe PDF: Nombre de la configuración de Adobe PDF preconfigurada que se aplicará a un trabajo de conversión, si esta configuración no se especifica como parte de los parámetros de invocación de API. La configuración de Adobe PDF se configura en la consola de administración, haciendo clic en Servicios > Generador de PDF > Configuración de Adobe PDF. Esta configuración solo se aplica a las conversiones basadas en PDFMaker.

**** Configuración de seguridad: Nombre de la configuración de seguridad preconfigurada que se aplicará a un trabajo de conversión, si esta configuración no se especifica como parte de los parámetros de invocación de API. La configuración de seguridad se configura en la consola de administración, haciendo clic en Servicios > Generador de PDF > Configuración de seguridad.

**** Configuración del tipo de archivo: Nombre de la configuración preconfigurada del tipo de archivo que se aplicará a un trabajo de conversión, si esta configuración no se especifica como parte de los parámetros de invocación de API. La configuración del tipo de archivo se configura en la consola de administración. Para ello, haga clic en Servicios > Generador de PDF > Configuración del tipo de archivo.

**** Usar Acrobat WebCapture (solo Windows): Cuando esta configuración es verdadera, el servicio Generar PDF utiliza Acrobat X Pro para todas las conversiones de HTML a PDF. Esto puede mejorar la calidad de los archivos PDF producidos a partir de HTML, aunque el rendimiento puede ser ligeramente inferior. El valor predeterminado es false.

**** Usar conversión de imágenes de Acrobat (solo Windows): Cuando esta configuración es verdadera, el servicio Generar PDF utiliza Acrobat X Pro para todas las conversiones de imagen a PDF. Esta configuración solo es útil si el mecanismo de conversión de Java puro predeterminado no puede convertir correctamente una proporción significativa de las imágenes de entrada. El valor predeterminado es false.

**** Habilitar las conversiones de AutoCAD basadas en Acrobat (solo Windows): Cuando esta configuración es verdadera, el servicio Generar PDF utiliza Acrobat X Pro para todas las conversiones de DWG a PDF. Esta configuración solo es útil si AutoCAD no está instalado en el servidor o si el mecanismo de conversión AutoCAD no puede convertir archivos correctamente.

**** Expresiones Regulares Para Encontrar Caracteres Especiales Prohibidos En Nombre De Usuario (Solo Windows): Especifica caracteres que interfieren con las operaciones de exportación de PDF y optimización de PDF cuando los caracteres aparecen en el nombre de un usuario.

**** Tamaño del grupo de imágenes a PDF: El tamaño del grupo del convertidor de imagen a PDF predeterminado (Java puro) en el servicio Generar PDF. Esta configuración controla el máximo de conversiones simultáneas de imagen a PDF que puede realizar el servicio Generar PDF. El valor predeterminado de este ajuste (recomendado para sistemas de un solo procesador) es 3, que puede aumentar en sistemas de varios procesadores.

**** Tamaño del grupo de archivos HTML a PDF: El tamaño del grupo del convertidor de HTML a PDF en el servicio Generar PDF. Esta configuración controla el máximo de conversiones simultáneas de HTML a PDF que puede realizar el servicio Generar PDF. El valor predeterminado de este ajuste (recomendado para sistemas de un solo procesador) es 3, que puede aumentar en sistemas de varios procesadores.

**** Tamaño del grupo de OCR: El tamaño del conjunto de servidores del PaperCaptureService que utiliza el generador de PDF para OCR. El valor predeterminado de este ajuste (recomendado para sistemas de un solo procesador) es 3, que puede aumentar en sistemas de varios procesadores. Esta configuración solo es válida en sistemas Windows.

**** Familia de fuentes de reserva para conversiones de HTML a PDF: Nombre de la familia de fuentes que se va a utilizar en documentos PDF cuando la fuente utilizada en el HTML original no está disponible para el servidor de formularios AEM. Especifique una familia de fuentes si espera convertir páginas HTML que utilicen fuentes no disponibles. Por ejemplo, las páginas creadas en idiomas regionales podrían utilizar fuentes no disponibles.

**Lógica de reintento para conversiones** nativas rige los reintentos de generación de PDF si falla el primer intento de conversión:

**No hay reintento**

No vuelva a intentar la conversión a PDF si ha fallado el primer intento de conversión

**Reintentar**

Reintente la conversión a PDF independientemente de si se ha alcanzado el umbral de tiempo de espera. La duración predeterminada del tiempo de espera para el primer intento es de 270 segundos.

**Vuelva a intentar si el tiempo lo permite**

Vuelva a intentar la conversión de PDF si el tiempo empleado para el primer intento de conversión fue inferior a la duración de tiempo de espera especificada. Por ejemplo, si la duración del tiempo de espera es de 270 y el primer intento de 200, PDF Generator volverá a tentarla. Si el primer intento consumió 270, la conversión no se volverá a intentar.

## Guías ES4 Utilidades configuración del servicio {#guides-es4-utilities-service-settings}

Al crear una guía, algunos recursos, como la definición de la guía, se incrustan en la guía. Los recursos también pueden existir como referencias a recursos de la aplicación almacenados localmente o en el servidor de formularios AEM. La Guía no contiene datos y los valores de la ubicación de envío y las entradas no son adecuados para todos los entornos externos.

En la mayoría de los casos, los servicios de procesamiento predeterminados de las guías son suficientes para preparar una guía para utilizarla en Workspace u otros entornos externos. (En la vista Servicios, en Workbench, el servicio predeterminado es Guías (sistema)/Procesos/Guía de procesamiento - 1.0). El servicio Guide Utilities ( `GuidesUtility`) le permite crear un proceso personalizado para procesar una guía, si es necesario.

Las operaciones de Guide Utilities le permiten agregar las siguientes tareas de procesamiento de la Guía a un proceso:

* Determinar si hay datos disponibles para rellenar la Guía con
* Incrustar los datos de la guía o convertirlos en un vínculo
* Convertir el contenido al que se hace referencia en direcciones URL a las que se puede acceder desde el exterior
* Sustituir valores en un documento HTML u otro contenedor, o convertirlos en direcciones URL a las que se pueda acceder desde el exterior
* Establecer la ubicación de envío
* Especificar valores de entrada
* Crear un parámetro para representar el contenido al que se hace referencia
* Si hay variaciones disponibles, establezca una variación

Los valores predeterminados del servicio Guide Utilities admiten la mayoría de los casos de uso. Sin embargo, si es necesario, puede cambiar los siguientes valores.

**** publicPaths: Esta opción está en desuso. No utilice esta opción con formularios AEM.

**** pathInfoExpiryInSeconds: Intervalo tras el cual caduca una solicitud de información de ruta de un cliente. El valor predeterminado es 1.

**** colateralExpiryInSeconds: Intervalo tras el cual caduca una solicitud de garantía de un cliente. El valor predeterminado es 315576000.

**** mismatchExpiryInSeconds: Intervalo después del cual caduca una solicitud de garantía de un cliente, cuando la etiqueta electrónica (etiqueta de entidad) no coincide. (Una eTag es un encabezado de respuesta HTTP). El valor predeterminado es 1.

**** guideContext: Raíz de contexto de la aplicación web Guías. Coincide con el valor establecido mediante la aplicación web Guías. El valor predeterminado es /Guides/.

**** secureRandomAlgorithm: El algoritmo que se usará al generar claves e identificadores. Este valor se pasa al método getInstance de la clase Java SecureRandom. El valor predeterminado es SHA1PRNG.

**** idBytes: Número de bytes aleatorios que se va a utilizar para un identificador de clave. El valor predeterminado es 6.

**** macAlgorithm: El algoritmo MAC (código de autenticación de mensajes) que se usará para la verificación de URL colateral. Este método se pasa al método getInstance de la clase Mac. El valor predeterminado es HmacSHA1.

**** macRefreshIntervalInMinutes: Cantidad de tiempo que una clave está activa. Cuando se ha activado una clave para este intervalo, se genera una nueva clave. La nueva clave se convierte en la clave activa. La clave activa anterior se conserva durante el 10 % del intervalo de actualización. Este comportamiento permite que las direcciones URL que se generan mediante la tecla antigua sigan funcionando en el conmutador de teclas. El valor predeterminado es 144000.

**** macOverlapIntervalInMinutes: Período de tiempo que la clave anterior seguirá siendo válida después de que se genere una nueva. El valor predeterminado es 1440 minutos (1 día).

**** macKeySeed: Un valor de inicialización para generar la dirección URL segura. Cuando se trata de una opción, la clave nunca se actualiza. La configuración de la misma inicialización en diferentes servidores dará como resultado que los servidores generen direcciones URL seguras que sean compatibles. Esto puede resultar útil si se utilizan varios servidores de formularios tras un equilibrador de carga. Introduzca una secuencia aleatoria de caracteres y números como raíz.

### Uso de guías en un clúster de servidores {#using-guides-in-a-server-cluster}

El procesamiento de una guía en un clúster de servidores que no utiliza sesiones adhesivas falla con una excepción NullPointerException. Una solicitud de guías aprovecha las direcciones URL seguras que, de forma predeterminada, son exclusivas del servidor en el que se generan. En un clúster que utiliza sesiones adhesivas, después de que una solicitud llegue a un nodo del clúster, todas las solicitudes posteriores para esa sesión o usuario se dirigen exclusivamente a ese servidor y todo está bien. En un clúster que no utiliza sesiones adhesivas, las solicitudes posteriores pueden visitar cualquier servidor del clúster. Si el servidor en el que se realizaron las solicitudes no es el servidor original, no se puede resolver la dirección URL segura.

Si utiliza guías en un clúster de servidores que no utiliza sesiones adhesivas, establezca el valor macKeySeed para el servicio GuidesUtility y, a continuación, detenga e inicie el clúster.

El valor macKeySeed es la raíz del generador de números aleatorios que se utiliza para generar las direcciones URL seguras. Al establecer este valor, cada nodo de clúster inicializa el generador de números aleatorios de la misma manera y tiene acceso a las mismas direcciones URL seguras. Puede utilizar cualquier cadena aleatoria para este valor de inicialización.

Cambie el valor macKeySeed cuando necesite actualizar las direcciones URL seguras. La actualización de las direcciones URL seguras depende de la directiva de seguridad y es similar a la política de actualización para cambiar la contraseña raíz maestra del servidor. macSeedValue es similar a la contraseña maestra para las direcciones URL seguras, ya que se utiliza para generar un nuevo número aleatorio único para su uso en la generación y recuperación seguras de direcciones URL.

Debe reiniciar el clúster porque macSeedValue es de solo lectura al iniciar el sistema. Todos los nodos deben reiniciarse para leer el valor, ya que lo utilizan de forma independiente para inicializar sus números aleatorios internos con el valor de inicialización.

## Configuración del servicio JDBC {#jdbc-service-settings}

El servicio JDBC ( `JdbcService`) permite a los procesos interactuar con bases de datos.

El siguiente ajuste está disponible para el servicio JDBC.

**** datasourceName: Un valor de cadena que representa el nombre JNDI del origen de datos que se va a utilizar para conectarse al servidor de la base de datos. El origen de datos debe definirse en el servidor de aplicaciones que aloja el servidor de formularios. El valor predeterminado es el nombre JNDI del origen de datos para la base de datos de formularios AEM.

## Configuración del servicio JMS {#jms-service-settings}

El servicio JMS ( `JMS`) permite la interacción con los proveedores del sistema de mensajería Java (JMS) que implementan tanto la mensajería punto a punto como la mensajería de publicación/suscripción.

Configure el servicio JMS con propiedades predeterminadas para que las operaciones de servicio puedan conectarse e interactuar con un proveedor JMS y un servicio JNDI asociado. Los valores de las propiedades del servicio se establecen en valores predeterminados según el servidor de aplicaciones JBoss. Cambie estos valores si utiliza un servidor de aplicaciones diferente para alojar formularios AEM.

Los siguientes ajustes están disponibles para el servicio JMS.

**** URL del proveedor: Dirección URL del proveedor de servicios JNDI. El valor predeterminado se basa en el servidor de aplicaciones JBoss. La siguiente URL son valores predeterminados para los servidores de aplicaciones que admiten los formularios AEM:

**** JBoss: `<server name>:1099`

**** WebLogic: `<server name>:7001`

**** WebSphere: `<server name>:2809`

**** Nombre de usuario JNDI: El nombre de usuario de la cuenta que se va a utilizar para autenticarse con el proveedor de servicios JNDI que se utiliza para buscar nombres de temas y colas. El valor predeterminado es invitado.

**** Contraseña JNDI: Contraseña asociada al nombre de usuario especificado para JNDI. El valor predeterminado es invitado.

**** Fábrica de contexto inicial: La clase Java que se va a utilizar como fábrica de contexto inicial. El servicio JMS utiliza esta clase para crear un contexto inicial, que es el punto de partida para resolver nombres de temas y colas. El valor predeterminado es la fábrica de contexto inicial para el servicio JMS en JBoss. Las siguientes clases son las fábricas de contexto iniciales para los servidores de aplicaciones que admiten los formularios AEM:

**** JBoss: org.jnp.interfaces.NamingContextFactory

**** WebLogic: weblogic.jndi.WLInitialContextFactory

**** WebSphere: com.ibm.websphere.aming.WsnInitialContextFactory

**** Nombre de usuario de la conexión: La contraseña asociada al nombre de usuario especificado para el nombre de usuario de la conexión. El valor predeterminado es invitado.

**** Contraseña de conexión: La contraseña asociada al nombre de usuario especificado para el nombre de usuario de la conexión. El valor predeterminado es invitado.

**** Otras propiedades: Par nombre de propiedad y valor que puede pasar al proveedor de servicios JNDI. Estas propiedades dependen de la implementación y configuración del proveedor que esté utilizando.

Los pares de nombre y valor de la propiedad están separados por punto y coma **;**. Por ejemplo, el siguiente texto muestra el valor que se especificaría para dos propiedades denominadas name1 y name2, con los valores value1 y value2, respectivamente:

`name1=value1;name2=value2`

## Ajustes del servicio LDAP {#ldap-service-settings}

El servicio LDAP ( `LDAPService`) proporciona operaciones para consultar directorios LDAP. Los directorios LDAP generalmente se utilizan para almacenar información sobre las personas, los grupos y los servicios de una organización.

Los siguientes ajustes están disponibles para el servicio LDAP.

**** Fábrica de contexto inicial: La clase Java que se va a utilizar como fábrica de contexto. Esta clase se utiliza para crear una conexión con el servidor LDAP. El valor predeterminado es com.sun.jndi.ldap.LdapCtxFactory, que es adecuado para la mayoría de los servidores LDAP.

**** URL del proveedor: Dirección URL que se va a utilizar para conectarse al servicio LDAP. El formato del valor es `ldap://server name:port`

*nombre* del servidor es el nombre del equipo que aloja el servidor LDAP

*puerto* es el puerto de comunicaciones que utiliza el servicio LDAP. El valor predeterminado es 389, que es el puerto estándar utilizado para las conexiones LDAP.

**** Nombre de usuario: El nombre de usuario de la cuenta de usuario que se va a utilizar para iniciar sesión en el servidor LDAP. La cuenta de usuario necesita tener permiso para conectarse al servidor y leer la información en el directorio LDAP.

Según el servidor LDAP, el nombre de usuario podría ser un nombre de usuario sencillo como `myname` o un DN, como `cn=myname,cn=users,dc=myorg`.

**** Contraseña: La contraseña que corresponde al nombre de usuario proporcionado para la configuración del nombre de usuario.

**** Otras propiedades: Un valor de cadena que representa otras propiedades y sus valores correspondientes que puede proporcionar al servidor LDAP. El valor tiene el siguiente formato:

`property=value;property=value;...`

## Configuración del servicio de configuración de Microsoft SharePoint {#microsoft-sharepoint-configuration-service-settings}

El servicio de configuración de Microsoft SharePoint `(MSSharePointConfigService)`permite especificar credenciales para el usuario de formularios AEM que tiene permisos de suplantación. Para obtener información sobre los permisos de suplantación, consulte [Configuración del conector para Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html).

Los siguientes ajustes están disponibles para el servicio de configuración de Microsoft SharePoint:

* Nombre de usuario para un usuario con permisos de suplantación
* Contraseña del usuario anterior

**Habilitar SSL (HTTPS):**

**** Tiempo de vida: Tiempo, en segundos, que este perfil de datos es válido y está almacenado en caché en el cliente. El valor predeterminado es 86400 (24 horas). Cuando una aplicación cliente se sincroniza con el servidor y ha transcurrido la cantidad de tiempo especificada, la aplicación cliente solicita un nuevo perfil de datos desde el servidor.

**** Cifrado: Especifica si se van a cifrar los datos almacenados en el dispositivo móvil.

**** Aplicación de formularios: Habilita la función Formularios en las aplicaciones cliente móviles. Cuando se selecciona esta opción, los usuarios pueden abrir formularios e iniciar procesos desde sus dispositivos móviles.

**** Aplicación Tareas: Habilita la función Tareas en las aplicaciones cliente móviles. Cuando se selecciona esta opción, los usuarios pueden acceder a sus listas de tareas y completar tareas desde sus dispositivos móviles.

**** Aplicación de servicios de contenido: Habilita la función Servicios de contenido en la aplicación cliente móvil. Esta función solo está disponible para iOS. Cuando se selecciona esta opción, los usuarios de iPhone y iPad pueden acceder a los archivos almacenados en el servidor WebDAV de su organización.

**** Compatibilidad sin conexión: Permite a los usuarios seguir utilizando las aplicaciones cliente móviles incluso cuando no tienen conexión con el servidor (por ejemplo, cuando están fuera del rango de celdas o en modo avión). Los usuarios también deben activar la opción Asistencia técnica sin conexión en sus dispositivos móviles. Esta función está disponible para dispositivos Android e iOS. De forma predeterminada, esta función está desactivada.

**Nota**: *Si la compatibilidad con sin conexión se ha activado y, a continuación, la deshabilita, los perfiles de datos de los usuarios se actualizan inmediatamente o en cuanto están en línea. Si un usuario ha estado trabajando sin conexión, todas las tareas pendientes se devuelven a su lista Tareas y todos los elementos de su cola, incluidos los formularios, tareas y formularios pendientes que contengan errores de validación, se eliminan de la cola.*

**** Android: Permite que los dispositivos Android se conecten al servidor.

**** Apple iOS: Permite que los iPhone y los iPad se conecten al servidor.

**** AIR: Permite que los dispositivos que ejecutan aplicaciones basadas en Adobe AIR® se conecten al servidor.

**** BlackBerry: Permite que los dispositivos BlackBerry se conecten al servidor.

**** Se requiere Android Microsoft Exchange ActiveSync: Especifica si el administrador de directivas de Microsoft Exchange ActiveSync (EAS) debe estar instalado y activo en dispositivos Android. Cuando se selecciona esta opción, EAS debe aplicarse en el dispositivo Android. Cuando esta opción no está seleccionada, no se realiza ninguna comprobación, aunque se siguen aplicando otros requisitos.

**** Longitud mínima del PIN para Android: Los dispositivos Android deben tener una configuración global que obligue a que el PIN o la contraseña tengan al menos esta longitud. No basta con tener un PIN de la longitud especificada. El sistema debe aplicar la longitud del PIN para que los usuarios no puedan quitarlo ni acortarlo más tarde. El valor predeterminado es 4.

**** Se retiene la contraseña máxima de Android antes de borrar: Los dispositivos Android tienen una configuración global que borra el sistema después de un número especificado de intentos de contraseña no válidos. Esta configuración global está habilitada y es igual o inferior al valor especificado aquí. El valor predeterminado es 5.

**** Eliminación del barrido de Android: Especifica lo que sucede cuando se produce una infracción de directiva en un dispositivo Android. Cuando se selecciona esta opción, se elimina la cuenta. Cuando esta opción no está seleccionada, se eliminan la contraseña de la cuenta almacenada y los datos almacenados en caché. No se realizan más intentos de sincronización hasta que el usuario corrija la infracción de la directiva.

## Ajustes del servicio de salida {#output-service-settings}

El servicio Output `(OutputService)`permite combinar datos de formulario XML con un diseño de formulario creado en AEM Forms Designer para crear una secuencia de salida de documento con uno de los siguientes formatos:

* Secuencia de salida de documento PDF o PDF/A.
* Un flujo de salida de Adobe PostScript.
* Un flujo de salida de Printer Control Language (PCL).
* Flujo de salida de lenguaje de programación Zebra (ZPL).

El flujo de salida se puede enviar a una impresora de red, una impresora local o un archivo de disco. Cuando se utiliza el servicio Output como parte de un proceso, también se puede enviar el flujo de salida a un destinatario de correo electrónico como archivo adjunto.

Los siguientes ajustes están disponibles para el servicio Output.

**** Tipo de transacción: Especifica cómo se debe propagar un contexto de transacción a una operación:

**** Requerido: admite un contexto de transacción si ya existe uno; de lo contrario, se crea un nuevo contexto de transacción. Este es el valor predeterminado.

**** Requiere nuevo: Siempre crea un nuevo contexto de transacción. Si existe un contexto de transacción activo, se suspende.

**** Tiempo de espera de transacción (en segundos): Número de segundos que el proveedor de transacciones subyacente espera antes de revertir una transacción que está ajustando esta operación. Este valor se ignora si se propaga un contexto de transacción existente.

Al procesar archivos de datos de gran tamaño o funcionar en un servidor ocupado, puede que sea necesario aumentar el tiempo de espera del servicio Output. Para cambiar el valor de tiempo de espera, asegúrese de que los servidores de hardware tienen la memoria adecuada y que la memoria está disponible para el montón de Java Application Server. El valor predeterminado es `180`.

## Configuración del servicio de configuración PDFG {#pdfg-config-service-settings}

Los siguientes ajustes están disponibles para el servicio de configuración PDFG ( `PDFGConfigService`).

**** Directorio de opciones de trabajo del usuario: Ruta de la carpeta del sistema de archivos donde el servicio c escribe los archivos de opciones de trabajo a los que puede acceder Acrobat Pro Extended. El valor predeterminado es [user.home]/Application Data/Adobe/Adobe PDF/Settings.

**** Directorio de inicio de PS: Ruta de la carpeta del sistema de archivos donde se guardan los archivos de inicio requeridos por Adobe Acrobat Distiller. El valor predeterminado es [user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**** Archivo de inicio de PS: Nombre del archivo de inicio requerido por Adobe Acrobat Distiller. El valor predeterminado es example.ps.

**** Tiempo de espera de conversión del servidor: Tiempo de espera máximo de conversión de trabajos (en segundos) para el servicio Generar PDF y el servicio Distiller. Esta configuración limita el tiempo de espera máximo de conversión que se puede especificar en el archivo config.xml y en las páginas de la consola de administración de PDF Generator. El valor predeterminado es 270.

**** Tiempo de espera global del servidor: Al realizar conversiones a PDF, un servidor de formularios tiene en cuenta el límite de tiempo de espera. Configure el valor de tiempo de espera para resolver el problema.

**** Prefijo de opciones de trabajo: Prefijo utilizado por el servicio Generar PDF para anteponer una cadena corta a los archivos de opciones de trabajo que crea temporalmente para su uso por Acrobat Distiller. El valor predeterminado es pdfg.

**** Aplicaciones no Unicode: Lista separada por comas de los nombres de aplicaciones que se sabe que no admiten Unicode. Esta lista se rellena previamente con los nombres de varias aplicaciones, cuya compatibilidad está preconfigurada en el generador de PDF. Si decide agregar compatibilidad para conversiones de PDF a través de otras aplicaciones de terceros que no admiten Unicode, debe agregarlas a esta lista. El valor predeterminado es Autocad,Excel,PowerPoint,Project,Publisher,Visio,Word,WordPerfect.

**** Recuento de grupos de subprocesos del servidor: Controla el tamaño del grupo de subprocesos que utiliza internamente el servicio Generar PDF para atender solicitudes de conversión de HTML a PDF que implican arañas de Web (conversión de páginas vinculadas accesibles desde la página principal). El valor predeterminado es 20.

**** Segundos del análisis de limpieza de PDFG: Consulte la sección Segundos de caducidad del trabajo para obtener más información.

**** Segundos de caducidad del trabajo: El servicio Generar PDF elimina los archivos de entrada en cuanto se convierten. Almacena los archivos de salida temporalmente, durante un período de tiempo determinado por los ajustes Segundos del análisis de limpieza de PDFG y Segundos de caducidad del trabajo.

La configuración Segundos de caducidad del trabajo especifica la antigüedad de un archivo o una carpeta vacía antes de que se pueda eliminar. La configuración de segundos de exploración de limpieza PDFG especifica la frecuencia con la que un subproceso de limpieza busca en las carpetas temporales archivos que se pueden eliminar.

Por ejemplo, si los segundos de caducidad del trabajo están establecidos en 100 y los segundos de exploración de limpieza de PDFG están establecidos en 200, el subproceso de limpieza se ejecuta cada 200 segundos y elimina los archivos que tienen 100 segundos o más.

El valor predeterminado de segundos de exploración de limpieza PDFG es `43200` (12 horas). El valor predeterminado de Segundos de Caducidad de Trabajo es `86400` (24 horas).

**** Configuración regional predeterminada: Se utiliza para anular la configuración regional predeterminada (país + idioma) del servidor en el que se implementa el servicio Generar PDF. Si no se especifica este parámetro, la configuración regional predeterminada se determina a partir del sistema operativo en el que se implementa el servicio. Este parámetro controla el idioma en el que se devuelven los mensajes de error a las API.

## configuración del servicio de servicios de datos del flujo de trabajo de formularios {#forms-workflow-data-services-service-settings}

Los siguientes servicios amplían los servicios de datos y exponen ensambladores que Workspace utiliza para hablar con el servidor. No cambie las opciones de configuración de estos servicios a menos que la asistencia técnica de Adobe le indique lo contrario. Estos servicios no están destinados al acceso directo:

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## Configuración del servicio remoto {#remoting-service-settings}

La mayoría de los servicios están configurados para que pueda acceder a ellos a través de AEM forms Remoting (obsoleto para formularios AEM). Para obtener información sobre AEM Forms Remoting (obsoleto para formularios AEM), consulte [Programación con formularios](https://adobe.com/go/learn_aemforms_programming_63)AEM.

Los siguientes ajustes están disponibles para el servicio Remoting.

**** Método de autenticación del cliente de Flex: Determina el tipo de respuesta que el servidor devuelve al cliente cuando el servicio invocado está habilitado para la seguridad, la operación invocada no admite invocaciones anónimas y el cliente pasa credenciales no válidas o no válidas. Elija entre Personalizado o Básico. El valor predeterminado es Básico.

**** Permitir Serialización De Clases No Serializables: La mayoría de los extremos de formularios AEM solo permiten utilizar clases serializables para la invocación. En versiones anteriores, el punto final Remoting permitía que se utilizaran clases no serializables para invocar clientes basados en Flex. Para evitar una vulnerabilidad de seguridad descrita en APS11-15, se ha cambiado. Si desea continuar utilizando clases no serializables con el extremo de Flex Remoting, seleccione esta casilla de verificación.

## Ajustes del servicio de repositorio {#repository-service-settings}

El servicio Repositorio ( `RepositoryService`) proporciona servicios de gestión y almacenamiento de recursos a los formularios AEM. Cuando los desarrolladores crean una aplicación, pueden implementar los recursos en el repositorio en lugar de en un sistema de archivos. Los recursos pueden incluir cualquier tipo de material colateral, incluidos formularios XML, formularios PDF (incluidos formularios de Acrobat), fragmentos de formulario, imágenes, perfiles, políticas, archivos SWF, archivos DDX, esquemas XML, archivos WSDL y datos de prueba.

Puede utilizar el repositorio predeterminado incluido con los formularios AEM o un repositorio de terceros (Content Server de Documentum de EMC, IBM FileNet Content Manager o IBM Content Manager).

El servicio Proveedor de repositorio es un delegado de servicio que actúa como interfaz de un servicio de proveedor. Esto le permite conectarse a una API común y no tiene que saber qué servicio de proveedor está implementando las capacidades de almacenamiento. El servicio Proveedor de repositorios proporciona almacenamiento de bases de datos para los recursos del servicio Repositorio.

El siguiente ajuste está disponible para el servicio Repositorio.

**** Servicio de proveedor: Nombre del servicio que se utiliza como proveedor de almacenamiento. El valor predeterminado es RepositoryProviderService.

## Configuración del servicio de firma {#signature-service-settings}

El servicio Signature ( `SignatureService`) permite a su organización proteger la seguridad y la privacidad de los documentos Adobe PDF que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que los documentos no se modifiquen. Al alterar un documento se rompe su firma. Dado que las características de seguridad se aplican al documento mismo, éste permanece seguro y controlado durante todo su ciclo de vida; más allá del servidor de seguridad, cuando se descarga sin conexión y cuando se envía de nuevo a su organización.

Los siguientes ajustes están disponibles para el servicio Signature.

**** Nombre Del Servicio SPI HSM Remoto: Esta opción se utiliza cuando el HSM está instalado en un equipo remoto. Especifique esta opción cuando los formularios AEM estén instalados en una ventana de 64 bits y utilice dispositivos HSM para firmar.

**** Dirección URL del servicio web remoto de HSM: Especifique esta opción cuando los formularios AEM estén instalados en Windows de 64 bits y utilice dispositivos HSM para firmar.

**** Certificación Para Incluir Cambios En La Carga Del Formulario: Cuando se selecciona esta opción, el estado del formulario XFA se certifica además de la plantilla XFA. Tenga en cuenta que habilitar esta opción puede tener un impacto negativo en el rendimiento. El valor predeterminado es true.

**** Ejecutar secuencias de comandos JavaScript de Document: Especifica si se deben ejecutar secuencias de comandos de JavaScript de documento durante las operaciones de firma. El valor predeterminado es false.

**** Procesar documentos con compatibilidad con Acrobat 9: Especifica si se activa la compatibilidad con Acrobat 9. Por ejemplo, cuando se selecciona esta opción, se activa la opción Certificación visible en archivos PDF dinámicos. El valor predeterminado es false.

**** Incrustar información de revocación al firmar: Especifica si la información de revocación está incrustada al firmar el documento PDF. El valor predeterminado es false.

**** Incrustar información de revocación al certificar: Especifica si la información de revocación está incrustada al certificar el documento PDF. El valor predeterminado es false.

**** Aplicar incrustación de información de revocación para todos los certificadosDurante la firma/certificación: Especifica si se produce un error en una operación de firma o certificación si no está incrustada la información de revocación válida para todos los certificados. Tenga en cuenta que si un certificado no contiene ninguna CRL o información de OCSP, se considera válido aunque no se recupere ninguna información de revocación. El valor predeterminado es false.

**** Orden de comprobación de revocación: Especifica el orden de comprobación de revocación cuando es posible realizar la comprobación mediante los mecanismos Lista de revocación de certificados (CRL) y Protocolo de estado de certificado en línea (OCSP). El valor predeterminado es OCSPFirst.

**** Tamaño Máximo De La Información De Archivo De Revocación: Tamaño máximo de la información de archivo de revocación en kilobytes. Los formularios AEM intentan almacenar la mayor cantidad de información de revocación posible sin superar el límite. El valor predeterminado es 10 KB.

**** Firmas De Soporte Creadas A Partir De Compilaciones Previas A La Versión De Productos De Adobe: Cuando se selecciona esta opción, la firma creada con la versión previa a la versión de los productos de Adobe se validará correctamente. El valor predeterminado es false.

**** Opción de hora de verificación: Especifica la hora de verificación del certificado de un firmante. El valor predeterminado es Hora segura en otro momento actual.

**** Utilice la información de revocación archivada en la firma durante la validación: Especifica si la información de revocación archivada con la firma se utiliza para la comprobación de revocación. El valor predeterminado es true.

**** Utilice La Información De Validación Almacenada En El Documento Para La Validación De Firmas: Cuando se selecciona esta opción, la información de validación (incluida la información de revocación y marca de hora) incrustada en el documento se utiliza para validar firmas. El valor predeterminado es true.

**** Máximo de sesiones de verificación anidadas permitidas: Número máximo de sesiones de verificación anidadas permitidas. Los formularios AEM utilizan este valor para evitar un bucle infinito al comprobar los certificados de firmante OCSP o CRL cuando el certificado OCSP o CRL no está configurado correctamente. El valor predeterminado es 10.

**** Máscara de reloj máxima para verificación: El tiempo máximo, en minutos, que la hora de firma puede ser posterior a la hora de validación. Si el sesgo del reloj es mayor que este valor, la firma no será válida. El valor predeterminado es de 65 minutos.

**** Caché de duración del certificado: Duración de un certificado, recuperado en línea o por otros medios, en la caché. El valor predeterminado es 1 día.

### Opciones de transporte {#transport-options}

**** Host proxy: Dirección URL del host proxy. Se utiliza solamente si se proporciona algún valor válido. No hay ningún valor predeterminado.

**** Puerto proxy: El puerto proxy. Escriba cualquier número de puerto válido entre 0 y 65535. El valor predeterminado es 80.

**** Nombre de usuario de inicio de sesión de proxy: El nombre de usuario de inicio de sesión del proxy. Solo se utiliza si se proporciona algún valor válido para el host proxy y el puerto proxy. No hay ningún valor predeterminado.

**** Contraseña de inicio de sesión de proxy: La contraseña de inicio de sesión del proxy. Solo se utiliza si se proporciona algún valor válido para el host proxy, el puerto proxy y el nombre de usuario de inicio de sesión proxy. No hay ningún valor predeterminado.

**** Límite máximo de descarga: Cantidad máxima de datos, en MB, que se pueden recibir por conexión. El valor mínimo es 1 MB y el valor máximo es 1024 MB. El valor predeterminado es 16 MB.

**** Tiempo de espera de conexión: Tiempo máximo de espera, en segundos, para establecer una nueva conexión. El valor mínimo es 1 y el valor máximo es 300. El valor predeterminado es 5.

**** Tiempo de espera del socket: Tiempo máximo de espera, en segundos, antes de que se produzca un tiempo de espera del socket (mientras se espera la transferencia de datos). El valor mínimo es 1 y el valor máximo es 3600. El valor predeterminado es 30.

### Opciones de validación de ruta {#path-validation-options}

**** Requerir directiva explícita: Especifica si la ruta de acceso debe ser válida para al menos una de las directivas de certificados asociadas al anclaje de confianza del certificado del firmante. El valor predeterminado es false.

**** Inhibir CUALQUIER Política: Especifica si se debe procesar el identificador de objeto de directiva (OID) si se incluye en un certificado. El valor predeterminado es false.

**** Inhibir asignación de directivas: Especifica si se permite la asignación de directivas en la ruta de certificación. El valor predeterminado es false.

**** Comprobar todas las rutas: Especifica si todas las rutas deben validarse o si la validación debe detenerse después de buscar la primera ruta válida. Seleccione true o false. El valor predeterminado es false.

**** Servidor LDAP: Servidor LDAP utilizado para buscar certificados para la validación de rutas. No hay ningún valor predeterminado.

**** Siga los URI del certificado AIA: Especifica si los identificadores de recursos uniformes (URI) del certificado AIA se procesan durante la detección de rutas. El valor predeterminado es false.

**** Se requiere la extensión de restricciones básicas en los certificados de CA: Especifica si la extensión del certificado de restricciones básicas de la entidad de certificación (CA) debe estar presente para los certificados de CA. Algunos certificados raíz certificados alemanes (7 y anteriores) no son compatibles con RFC 3280 y no contienen la extensión de restricción básica. Si se sabe que el certificado EE de un usuario se encadena hasta una raíz alemana de este tipo, anule la selección de esta casilla de verificación. El valor predeterminado es true.

**** Requerir firma de certificado válida durante la generación de cadenas: Especifica si el generador de cadenas requiere firmas válidas en los certificados utilizados para crear cadenas. Cuando se selecciona esta casilla de verificación, el generador de cadenas no genera cadenas con firmas RSA no válidas en los certificados. Considere la cadena CA > ICA > EE donde la firma de la CA en una ICA no es válida. Si este ajuste es cierto, la cadena de construcción se detendrá en el ICA, y la CA no se incluirá en la cadena. Si esta configuración es falsa, se genera la cadena completa de 3 certificados. Esta configuración no afecta a las firmas de DSA. El valor predeterminado es false.

### Opciones del proveedor de marca de hora {#timestamp-provider-options}

**** URL del servidor TSP: Dirección URL del proveedor de marca de hora predeterminado. Se utiliza solamente si se proporciona algún valor válido. No hay ningún valor predeterminado.

**** Nombre de usuario del servidor TSP: El nombre de usuario, si lo requiere el proveedor de marca de hora. Se utiliza solamente si se proporciona algún valor válido para la dirección URL. No hay ningún valor predeterminado.

**** Contraseña del servidor TSP: La contraseña del nombre de usuario anterior si la requiere el proveedor de marca de hora. Se utiliza solamente si se proporciona algún valor válido para la dirección URL y el nombre de usuario. No hay ningún valor predeterminado.

**** Algoritmo hash de solicitud: Especifica el algoritmo hash que se utilizará al crear la solicitud para el proveedor de marca de hora. El valor predeterminado es SHA1.

**** Estilo de comprobación de revocación: Especifica el estilo de comprobación de revocación utilizado para determinar el estado de confianza del certificado del proveedor de marca de tiempo a partir de su estado de revocación observado. El valor predeterminado es BestEffort.

**** Enviar cadena nonce: Especifica si se envía una cadena nonce con la solicitud de proveedor de marca de hora. Una cadena nonce puede ser una marca de fecha y hora, un contador de visitas en una página web o un marcador especial destinado a limitar o evitar la reproducción o reproducción no autorizada de un archivo. El valor predeterminado es true.

**** Usar marcas de hora caducadas durante la validación: Cuando se selecciona esta opción, las marcas de hora caducadas se pueden utilizar para recuperar los tiempos de validación de las firmas. El valor predeterminado es true.

**** Tamaño de respuesta TSP: Tamaño estimado, en bytes, de la respuesta TSP. Este valor debe representar el tamaño máximo de la respuesta de marca de tiempo que puede devolver el proveedor de marca de tiempo configurado. No cambie esto a menos que esté absolutamente seguro. El valor mínimo es 60B y el valor máximo es 10240B. El valor predeterminado es 4096B.

**Omitir extensión** del servidor TimeStamp: Seleccione la opción **Ignorar extensión** del servidor de TimeStamp para evitar que el servidor de AEM Forms se ponga en contacto con el servidor de marca de hora especificado. La selección de la opción ayuda a evitar errores de proceso que se producen debido al tiempo de espera de conexión entre AEM Forms y los servidores de marca de hora.

### Opciones de lista de revocación de certificados {#certificate-revocation-list-options}

**** Consultar primero URI local: Especifica si se debe dar preferencia a la ubicación CRL proporcionada en el URI local o en la lista CRL sobre cualquier ubicación especificada dentro de un certificado para comprobar la revocación. El valor predeterminado es false.

**** URI local para búsqueda de CRL: URL del proveedor CRL local. Este valor solo se consulta si la configuración Consultar URI local primero está establecida en true. No hay ningún valor predeterminado.

**** Estilo de comprobación de revocación: Especifica el estilo de comprobación de revocación utilizado para determinar el estado de confianza del certificado del proveedor CRL a partir de su estado de revocación observado. El valor predeterminado es BestEffort.

**** Servidor LDAP para búsqueda de CRL: El servidor LDAP utilizado para obtener las CRL (como www.ldap.com). Todas las consultas basadas en DN para CRL se dirigirán a este servidor. No hay ningún valor predeterminado.

**** Conectarse: Especifica si desea conectarse para recuperar una CRL. Si es false, solo se consultan las CRL almacenadas en caché (en el disco local o las incrustadas con la firma). El valor predeterminado es true.

**** Omitir fechas de validez: Especifica si se deben ignorar los tiempos thisUpdate y nextUpdate de la respuesta, lo que evita que estos tiempos tengan un efecto negativo en la validez de la respuesta. El valor predeterminado es false.

**** Requerir extensión AKI en CRL: Especifica si la extensión del identificador de clave de autoridad debe incluirse en una CRL. El valor predeterminado es false.

### Opciones de protocolo de estado de certificado en línea {#online-certificate-status-protocol-options}

**** URL del servidor OCSP: URL del servidor OCSP predeterminado. El uso del servidor OCSP especificado a través de esta URL depende de la configuración de la opción URL para consultar. No hay ningún valor predeterminado.

**** Opción de URL para consultar: Controla la lista y el orden de los servidores OCSP que se utilizan para realizar la comprobación de estado. El valor predeterminado es UseAIAInCert.

**** Estilo de comprobación de revocación: Especifica el estilo de comprobación de revocación que se utiliza al comprobar el certificado del servidor OCSP. El valor predeterminado es CheckIfAvailable.

**** Enviar cadena nonce: Especifica si se envía una cadena nonce con la solicitud OCSP. Una cadena nonce puede ser una marca de fecha y hora, un contador de visitas en una página web o un marcador especial destinado a limitar o evitar la reproducción o reproducción no autorizada de un archivo. El valor predeterminado es true.

**** Tiempo máximo de desvío del reloj: El sesgo máximo permitido, en minutos, entre el tiempo de respuesta y la hora local. El valor mínimo es 0 y el valor máximo es 2147483647m. El valor predeterminado es 5m.

**** Tiempo de frescura de la respuesta: Tiempo máximo, en minutos, durante el cual una respuesta OCSP preconstruida se considera válida. El valor mínimo es 1m y el valor máximo permitido es 2147483647. El valor predeterminado es 525600 (un año).

**** Firmar solicitud OCSP: Especifica si se debe firmar la solicitud OCSP. El valor predeterminado es false.

**** Alias de credencial del firmante de la solicitud: Especifica el alias de credencial que se usará para firmar la solicitud de OCSP si la firma está habilitada. Solo se utiliza si la firma de la solicitud OCSP está habilitada. No hay ningún valor predeterminado.

**** Conectarse: Especifica si se va a conectar para realizar la comprobación de revocación. El valor predeterminado es true.

**** Omitir los tiempos thisUpdate y nextUpdate de la respuesta: Especifica si se deben ignorar los tiempos thisUpdate y nextUpdate de la respuesta, lo que evita que estos tiempos tengan un efecto negativo en la validez de la respuesta. El valor predeterminado es false.

**** Permitir extensión OCSPNoCheck: Especifica si se permite la extensión OCSPNoCheck en el certificado de firma de respuesta. El valor predeterminado es true.

**** Requerir extensión de CertHash OCSP ISIS-MTT: Especifica si se debe incluir una extensión hash de clave pública de certificado en las respuestas de OCSP. El valor predeterminado es false.

### Opciones de administración de errores para depuración {#error-handling-options-for-debugging}

**** Purgar caché de certificados en la siguiente llamada de API: Especifica si se depura la caché de certificados cuando se llama a la siguiente operación de servicio de firma. Después de llamar a la operación, esta opción se establece en false. El valor predeterminado es false.

**** Purgar caché CRL en la siguiente llamada de API: Especifica si se depura la caché CRL cuando se llama a la siguiente operación de servicio de firma. Después de llamar a la operación, esta opción se establece en false. El valor predeterminado es false.

**** Purgar caché OCSP en la siguiente llamada de API: Especifica si se depura la caché de OCSP cuando se llama a la siguiente operación de servicio de firma. Después de llamar a la operación, esta opción se establece en false. El valor predeterminado es false.

## Configuración del servicio de carpetas vigiladas {#watched-folder-service-settings}

El servicio Carpeta vigilada ( `WatchedFolder`) configura atributos comunes para todos los extremos de carpetas vigilados. También proporciona valores predeterminados para los extremos de carpeta observados. (Consulte [Configuración de los extremos](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)de carpeta vigilados). No se invoca en aplicaciones cliente externas ni se utiliza en procesos creados en Workbench.

Los siguientes ajustes están disponibles para el servicio Carpeta vigilada.

**** Expresión Cron: Expresión cron utilizada por cuarzo para programar la encuesta del directorio de entrada.

**** Repetir recuento: Número de veces que se sondea el directorio de entrada. El recuento de repetición predeterminado que se usará si no se especifica este valor en la configuración del extremo. Un valor de -1 indica la exploración indefinida del directorio. El valor predeterminado es -1.

**** Intervalo de repetición: El número predeterminado si hay segundos entre cada encuesta. Este valor se utiliza como intervalo de repetición a menos que se especifique un valor diferente en la configuración del extremo de la carpeta controlada. El valor predeterminado es 5. Consulte la descripción del ajuste Tamaño de lote para obtener más información.

**** Asíncrono: Identifica el tipo de invocación como asíncrono o sincrónico. Los procesos transitorios y sincrónicos sólo se pueden invocar sincrónicamente. El valor predeterminado es asincrónico.

**** Tiempo de espera: El valor predeterminado de tiempo, en segundos, tras el cual se recuperan los archivos de las carpetas de entrada. Si el archivo o la carpeta es anterior al tiempo especificado en el tiempo de espera, se selecciona para su procesamiento. El valor predeterminado es 0.

**** Tamaño del lote: Valor predeterminado del número de archivos o carpetas que se procesan por análisis. El valor predeterminado es 2.

La configuración de Repetir intervalo y Tamaño de lote determina cuántos archivos ha visto la carpeta se recogen en cada análisis. Watched Folder utiliza un grupo de subprocesos de Quartz para analizar la carpeta de entrada. El grupo de subprocesos se comparte con otros servicios. Si el intervalo de exploración es pequeño, los subprocesos analizan la carpeta de entrada con frecuencia. Si los archivos se sueltan con frecuencia en la carpeta vigilada, mantenga el intervalo de exploración pequeño. Si los archivos se retiran con poca frecuencia, utilice un intervalo de exploración mayor para que los demás servicios puedan utilizar los subprocesos.

Si se está extrayendo un gran volumen de archivos, haga que el tamaño del lote sea grande. Por ejemplo, si el servicio invocado por el extremo de la carpeta vigilada puede procesar 700 archivos por minuto y los usuarios sueltan los archivos en la carpeta de entrada a la misma velocidad, si se establece el tamaño del lote en 350 y el intervalo de repetición en 30 segundos, se ayudará a observar el rendimiento de la carpeta sin incurrir en el coste de digitalizar la carpeta vigilada con demasiada frecuencia.

Cuando los archivos se colocan en la carpeta vigilada, se muestran en una lista los archivos de entrada, lo que puede reducir el rendimiento si la digitalización se realiza cada segundo. El aumento del intervalo de exploración puede mejorar el rendimiento. Si el volumen de archivos que se van a soltar es pequeño, ajuste el tamaño del lote y el intervalo de repetición en consecuencia. Por ejemplo, si se pierden 10 archivos cada segundo, intente establecer el intervalo de repetición en 1 segundo y el tamaño del lote en 10.

En una configuración de clúster, el tamaño del lote de un extremo de carpeta vigilado no se escala a varios nodos de clúster. Por ejemplo, si el tamaño del lote se establece en `2` para un clúster de dos nodos y se selecciona la opción Aceleración, los nodos procesan los archivos de forma colectiva en lotes de dos en lugar de que cada nodo procese dos archivos a la vez.

**** Sobrescribir nombres de archivo duplicados: Una cadena booleana que especifica si la carpeta controlada sobrescribe los nombres de archivo de resultados duplicados y si se deben sobrescribir los documentos conservados con el mismo nombre.

**** Conservar carpeta: El valor predeterminado para la carpeta preserve. Esta carpeta se utiliza para copiar los archivos de origen en caso de que la entrada se procese correctamente. Este valor puede ser una ruta vacía, relativa o absoluta con un patrón de archivo como se describe en la configuración de la carpeta de resultados.

**** Carpeta de error: Nombre de la carpeta en la que se copian los archivos de error. Este valor puede ser una ruta vacía, relativa o absoluta con un patrón de archivo como se describe en la configuración de la carpeta de resultados.

**** Carpeta de resultados: Nombre predeterminado de la carpeta de resultados. Esta carpeta se utiliza para copiar los archivos de resultados en. Este valor puede ser una ruta vacía, relativa o absoluta con el siguiente patrón de archivo.

* %F = prefijo de nombre de archivo
* %E = extensión de nombre de archivo
* %Y = año (completo)
* %y = año (dos últimos dígitos)
* %M = mes
* %D = día del mes
* %d = día del año
* %H = hora (reloj de 24 horas)
* %h = hora (reloj de 12 horas)
* %m = minuto
* %s = segundo
* %l = milisegundo
* %R = número aleatorio (de 0 a 9)
* %P = id. de proceso o trabajo

Por ejemplo, si es el 17 de julio de 2009 a las 20.00 horas y usted especifica `C:/Test/WF0/failure/%Y/%M/%D/%H/`, la carpeta de resultados es `C:/Test/WF0/failure/2009/07/17/20`.

Si la ruta no es absoluta sino relativa, la carpeta se crea dentro de la carpeta controlada. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)de archivo.

***Nota **: Cuanto menor sea el tamaño de las carpetas resultantes, mejor será el rendimiento de la carpeta vigilada. Por ejemplo, si la carga estimada de la carpeta vigilada es de 1000 archivos por hora, pruebe un patrón como`result/%Y%M%D%H`para que se cree una nueva subcarpeta cada hora. Si la carga es más pequeña (por ejemplo, 1000 archivos por día), puede usar un patrón como`result/%Y%M%D`.*

**** Carpeta de etapa: Nombre predeterminado de la carpeta de escenario dentro de la carpeta controlada.

**** Carpeta de entrada: Nombre predeterminado de la carpeta de entrada dentro de la carpeta controlada.

**** Mantener si falla: Si es true, los archivos originales se conservan en la carpeta de errores si se produce un error.

**** Acelerador: Cuando se selecciona esta opción, se limita el número de trabajos de carpeta observados que procesan los formularios AEM en un momento dado. El valor Tamaño de lote determina el número máximo de trabajos (consulte Acerca de la limitación).

## Configuración del servicio Web {#web-service-service-settings}

El servicio Web ( `WebService`) permite a los procesos invocar operaciones de servicio Web.

El servicio Web permite a los procesos invocar operaciones de servicio Web. Por ejemplo, es posible que una organización desee integrar un proceso para almacenar y recuperar información como los datos de contacto y cuenta invocando los servicios Web expuestos de un proveedor de servicios. El servicio Web invoca un servicio Web especificado y pasa por los valores de cada uno de sus parámetros. A continuación, guarda los valores devueltos de la operación en una variable designada dentro de un proceso.

El servicio de servicio Web interactúa con los servicios Web enviando y recibiendo mensajes SOAP. El servicio también admite el envío de archivos adjuntos MIME, MTOM y SwaRef con mensajes SOAP mediante el protocolo WS-Attachment. Las interacciones del servicio Web son compatibles con los sistemas SAP y los servicios Web .NET.

Los siguientes ajustes están disponibles para el servicio Web.

**** Almacén de claves: Ruta completa del archivo del almacén de claves que contiene la clave privada que se usará para la autenticación. El servidor de formularios debe poder acceder al archivo.

**** Contraseña del almacén de claves: La contraseña del archivo de almacén de claves.

**** Tipo de almacén de claves: Tipo del almacén de claves. No proporcione ningún valor para utilizar el tipo de almacén de claves predeterminado configurado para la JVM que ejecuta el servidor de formularios. De lo contrario, proporcione uno de los siguientes valores:

* jks
* pkcs12
* cms
* jceks

**** Almacén de confianza: Ruta de acceso completa del archivo del almacén de confianza que contiene la clave pública del servidor del servicio Web.

**** Contraseña del almacén de confianza: La contraseña del archivo de almacén de confianza.

**** Tipo de almacén de confianza: El tipo del almacén de confianza. No proporcione ningún valor para utilizar el tipo de almacén de claves predeterminado configurado para la JVM que ejecuta el servidor de formularios. De lo contrario, proporcione uno de los siguientes valores:

* jks
* pkcs12
* cms
* jceks

## Ajustes del servicio de transformación XSLT {#xslt-transformation-service-settings}

El servicio de transformación XSLT ( `XSLTService`) permite a los procesos aplicar transformaciones de lenguaje de hoja de estilo extensible (XSLT) en documentos XML.

El siguiente ajuste está disponible para el servicio de transformación XSLT.

**** Nombre de fábrica: Nombre completo de la clase Java que se va a utilizar para realizar transformaciones XSLT. Si no se especifica ningún valor, se utiliza la fábrica predeterminada configurada en la máquina virtual Java que ejecuta el servidor de formularios.

## Modificación de la configuración de seguridad de un servicio {#modifying-security-settings-for-a-service}

el servidor de formularios le permite configurar la configuración de seguridad para cada servicio, lo que le permite configurar el control de acceso detallado en un nivel servicio por servicio.

Se instalan perfiles de seguridad predeterminados, que se pueden configurar para satisfacer las necesidades del sistema. Cada perfil de seguridad tiene un dominio asociado y se crea a nivel de usuario o de grupo.

### Modificar la configuración de seguridad de un servicio {#modify-security-settings-for-a-service}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en el servicio que desea configurar.
1. Haga clic en la ficha Seguridad.
1. En la lista Requerir llamadas para autenticar, seleccione Sí o No para especificar si el servicio se puede invocar con o sin credenciales.

   Si selecciona Sí, se debe autenticar al llamador del servicio y se debe autorizar al principal del usuario para que invoque el servicio; de lo contrario, se rechazará el intento de invocación.

   Si selecciona No, el llamador del servicio puede o no estar autenticado. La invocación del servicio siempre tendrá éxito porque no hay comprobación de autorización.

1. Para los servicios que contienen una o varias operaciones marcadas para acceso anónimo, seleccione o anule la selección de Acceso anónimo permitido. Cuando se habilita el acceso anónimo, cualquier usuario del sistema puede invocar operaciones en el servicio. Si el acceso anónimo está deshabilitado, se debe otorgar a los usuarios permiso para llamar al servicio e invocar operaciones. Los usuarios reciben estos permisos directamente o como parte de un grupo que tiene dichos permisos.
1. Para algunos servicios, la cuenta de usuario que ejecuta la operación afecta a los resultados. Por ejemplo, en Content Services (obsoleto), el usuario que almacena contenido se convierte en el propietario del contenido, lo que afecta a quién puede acceder más adelante al contenido. Si está utilizando un proceso para almacenar contenido, piense en qué usuario se utiliza para ejecutar el servicio de Document Management, ya que ese usuario será el propietario del contenido almacenado.

   Para especificar la identidad en tiempo de ejecución que utiliza un servicio para ejecutar operaciones, seleccione Especificar ejecución como, seleccione una opción de la lista asociada y, a continuación, haga clic en Guardar. Elija entre las siguientes opciones:

   **** Invocador: Utiliza la misma identidad que el usuario que invocó el servicio.

   **** Sistema: Utiliza el usuario del sistema para ejecutar el servicio con privilegios completos.

   **** Usuario con nombre: Permite ejecutar el servicio como un usuario específico. Cuando seleccione esta opción, haga clic en Seleccionar usuario para mostrar la página Seleccionar principal, donde puede buscar y seleccionar el usuario.

   Si no selecciona Especificar ejecución como, se utiliza el comportamiento predeterminado.

   >[!NOTE]
   >
   >Los servicios de procesamiento y envío que se utilizan con variables xfaForm, Document Form y Form siempre se ejecutan con la cuenta de usuario del sistema.

1. Haga clic en Agregar entidad de seguridad para especificar los permisos que los usuarios y grupos tienen para este servicio.
1. La pantalla Seleccionar entidad de seguridad muestra los usuarios y grupos configurados en Administración de usuarios. Si el usuario o grupo que desea no se muestra, utilice la función de búsqueda para encontrarlo. Haga clic en un nombre de usuario o grupo.
1. En la pantalla Agregar permisos, seleccione los permisos que desea asignar al usuario o grupo para este servicio:

   * **** INVOKE_PERM: Para invocar todas las operaciones en el servicio
   * **** MODIFY_CONFIG_PERM: Para modificar la configuración de un servicio
   * **** SUPERVISOR_PERM: Para ver los datos de instancia de proceso de un servicio creado a partir de un proceso
   * **** START_STOP_PERM: Para iniciar y detener un servicio
   * **** ADD_REMOVE_ENDPOINTS_PERM: Adición, eliminación y modificación de puntos finales de un servicio
   * **** CREATE_VERSION_PERM: Para crear una nueva versión del servicio
   * **** DELETE_VERSION_PERM: Para eliminar una versión del servicio
   * **** MODIFY_VERSION_PERM: Para modificar una versión del servicio
   * **** READ_PERM: Para ver el servicio
   * **** PROCESS_OWNER_PERM: Para su uso en una versión futura de formularios AEM. No utilice este permiso.
   * **** SERVICE_MANAGER_PERM: Para su uso en una versión futura de formularios AEM. No utilice este permiso.
   * **** SERVICE_AGENT_PERM: Para su uso en una versión futura de formularios AEM. No utilice este permiso.

1. Haga clic en Agregar.

### Quitar el principal de un perfil de seguridad {#remove-the-principal-from-a-security-profile}

1. En la página Administración de servicios, seleccione el servicio que desea configurar.
1. Haga clic en la ficha **Seguridad** , seleccione el perfil de seguridad que desea eliminar y haga clic en **Eliminar**.

## Configuración del agrupamiento para un servicio {#configuring-pooling-for-a-service}

Cada servicio puede aprovechar las capacidades de agrupación para gestionar las solicitudes de invocación entrantes. El uso de un grupo de servicios garantiza que las instancias de servicio se invoquen mediante un solo subproceso a la vez y se reutilicen en todas las solicitudes de invocación, lo que puede mejorar el rendimiento. También puede utilizar agrupamiento para especificar la opción Máximo de instancias de servicio asincrónicas, que permite a los servicios limitar el número de solicitudes administradas en paralelo.

### Habilitar agrupación {#enable-pooling}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en el servicio que desea configurar.
1. Haga clic en la ficha Agrupación.
1. En la lista Estrategia de procesamiento de solicitudes, seleccione Instancias agrupadas para todas las solicitudes.
1. En el cuadro Tamaño inicial del grupo de instancias de servicio, introduzca el tamaño inicial del grupo. Cuando se implementa el servicio, este número se utiliza para determinar el número de instancias de implementación de servicio que se crean y asignan al grupo gratuito, en espera de solicitudes de invocación. Esto permite que el contenedor de servicios responda inmediatamente a las solicitudes de invocación sin tener que inicializar primero una instancia de servicio.
1. En el cuadro Tamaño máximo del grupo de instancias de servicio, introduzca el número máximo de instancias en el grupo para un servicio determinado. Esta configuración controla el número de subprocesos que pueden ejecutar un servicio determinado en un momento determinado. El valor predeterminado es 0, lo que da como resultado un tamaño de grupo ilimitado.
1. En el cuadro Número máximo de instancias de servicio asincrónicas, introduzca el número máximo de instancias del grupo que se pueden utilizar para atender solicitudes asincrónicas en un momento dado. Esta configuración permite al servicio limitar el número de solicitudes que puede gestionar en paralelo.
1. En el cuadro Tiempo de espera de invocación, introduzca el número de milisegundos que hay que esperar para que un servicio esté disponible para una solicitud de invocación. Si no se especifica un valor para esta configuración, el valor predeterminado es 0, lo que no genera tiempo de espera.
1. Haga clic en Guardar.

### Eliminar agrupación {#remove-pooling}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en el servicio que desea configurar.
1. Haga clic en la ficha Agrupación.
1. En la lista Estrategia de procesamiento de solicitudes, seleccione Nueva instancia para cada solicitud o Instancia única para todas las solicitudes.

   **** Instancia única para todas las solicitudes: Se crea una instancia de servicio y se almacena en caché cuando la primera solicitud entra en el contenedor. Cada solicitud posterior utiliza la misma instancia de servicio para gestionar la solicitud.

   **** Nueva instancia para cada solicitud: Se crea una nueva instancia de servicio para cada invocación recibida.

1. Haga clic en Guardar.

