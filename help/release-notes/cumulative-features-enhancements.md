---
title: Funciones clave acumulativas y mejoras en la versión de Adobe Experience Manager 6.5.
description: Una lista acumulativa de las funciones y mejoras clave realizadas en Adobe Experience Manager 6.5 con respecto a las ocho versiones de Service Pack anteriores.
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: eef3ad559612c338de0c4232aadc4133c910aaf8
workflow-type: tm+mt
source-wordcount: '3109'
ht-degree: 8%

---

# Funciones clave acumulativas y mejoras

Una lista acumulativa de las principales funciones y mejoras de Adobe Experience Manager 6.5 para las ocho versiones de Service Pack anteriores.

Consulte también [Notas de la versión del paquete de servicio más reciente de Adobe Experience Manager 6.5](/help/release-notes/release-notes.md).


## AEM 6.5, Service Pack 23: 22 de mayo de 2025

### Formularios {#forms-sp23}

* [Hipervínculos accesibles con estilo de texto mixto en archivos PDF estáticos](https://helpx.adobe.com/content/dam/help/es/experience-manager/6-5/forms/pdf/using-designer.pdf): Los hipervínculos que contienen estilos de texto mixtos en archivos PDF estáticos ahora están etiquetados como un solo elemento accesible. Esta mejora simplifica la estructura del árbol de etiquetas, mejora la navegación del lector de pantalla y admite un mejor cumplimiento de la accesibilidad.

* [Se ha actualizado la matriz de la plataforma compatible](/help/forms/using/aem-forms-jee-supported-platforms.md)

  La versión más reciente introduce actualizaciones en la matriz de plataformas admitidas, lo que garantiza la compatibilidad con las tecnologías más recientes.

   * Cliente de IBM® Content Manager 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8,4

   * Microsoft® SQL Server 2022

   * Controlador JDBC del servidor Microsoft® SQL 12.8

   * Red Hat® Enterprise Linux® 9 (Kernel 4.x, 64 bits)

* [Componente de archivo adjunto protegido](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment): como medida de seguridad, el componente ahora evita el envío de archivos con extensiones modificadas que intentan omitir las comprobaciones de tipo de archivo permitido. Estos archivos se bloquean durante el envío para garantizar que solo se aceptan tipos de archivo válidos.

## AEM 6.5, Service Pack 22: 21 de noviembre de 2024

### Sites {#sites}

[El editor universal](/help/sites-developing/universal-editor/introduction.md) ya está disponible en AEM 6.5 para casos de uso remoto con la aplicación de un paquete de funciones.

### [!DNL Assets]

La pestaña IPTC ahora admite los campos de texto [!UICONTROL Texto alternativo] y [!UICONTROL Descripción extendida]. (Assets-34918)

### Formularios {#forms-sp22}

#### Nuevas funciones de GA en AEM Forms {#ga-aem-forms-sp22}

* Se ha agregado compatibilidad para habilitar la incrustación de fuentes en las [API por lotes de comunicaciones interactivas](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel). Las comunicaciones interactivas ahora admiten la incrustación de fuentes Adobe Ming y Adobe Myungjo en archivos PDF generados mediante la API por lotes. Esta mejora garantiza una representación precisa del texto en los documentos generados, incluso cuando se utilizan subconjuntos de fuentes, lo que proporciona una compatibilidad mejorada con el contenido multilingüe en las salidas de PDF.

* [Tabla de API de contenido para accesibilidad de PDF](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api): AEM Forms en OSGi ahora es compatible con la nueva API de etiquetas de TDC para mejorar PDF en cuanto a estándares de accesibilidad. Hace que los archivos PDF sean más accesibles para los usuarios con tecnología de asistencia.

* [Resolución XDP del fragmento](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository): AEM Forms en OSGi ahora resuelve los XDP del fragmento a los que se hace referencia en los XDP principales y se almacenan en el repositorio de CRX de AEM.

* [Mejoras en el cumplimiento de PDF/A](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents): Ahora los usuarios pueden convertir archivos PDF a formatos PDF/A (1a, 2a, 3a) para fines de archivo, al tiempo que garantizan la accesibilidad y verifican el cumplimiento de estos estándares.

* **Compatibilidad con el cambio de tamaño automático de la fuente para documentos estáticos de PDF**: AEM Forms Designer, OutputService y FormsService ahora admiten el cambio de tamaño automático de fuentes para PDF estáticos. Si el usuario establece el tamaño de fuente 0 para los campos de texto, numéricos, de contraseña o de fecha y hora, el tamaño de fuente se ajusta automáticamente dentro de estos campos sin alterar el tamaño general del campo. Para utilizar la función, los usuarios pasan un indicador en el XCI personalizado: `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`.

#### Nuevas funciones de Beta en AEM Forms {#beta-aem-forms-sp22}

La función beta ofrece una oportunidad única para obtener acceso exclusivo a innovaciones de vanguardia y ayudar a dar forma a su desarrollo. ¿Quiere activar una función beta para sus entornos? Envíe un correo electrónico desde su dirección oficial a aem-forms-ea@adobe.com con la lista de funciones que le interesan.

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) y [servicios de CAPTCHA de torniquete de Cloudflare](/help/forms/using/integrate-adaptive-forms-turnstile.md): AEM Forms admite los siguientes servicios de Captcha:
   * Captcha protege los formularios de bots, spam y abusos automatizados al desafiar a los usuarios con un widget de casilla de verificación. Garantiza que solo los usuarios humanos procedan, mejorando la seguridad de las transacciones en línea.
   * Cloudflare Turnstile ofrece una medida de seguridad que tiene como objetivo proteger los formularios de bots automatizados, ataques maliciosos, spam y tráfico automatizado no deseado. Presenta una casilla de verificación en el envío del formulario para verificar que son humanos, antes de permitirles enviar el formulario.

* Versiones de formulario adaptable:
   * [Crear varias versiones de un formulario adaptable](/help/forms/using/add-versioning-reviews-comments.md): Ahora los usuarios pueden administrar fácilmente las variaciones de los formularios existentes. Este proceso simplifica el control de versiones y facilita la comparación para la optimización de formularios, todo ello dentro de un único flujo de trabajo optimizado.
   * [Comparar Forms adaptable](/help/forms/using/compare-forms-core-components.md): Ahora los usuarios pueden comparar fácilmente dos formularios para identificar diferencias. Facilita una colaboración fluida ya que permite a los miembros del equipo comparar revisiones y discutir cambios de forma eficaz.

## AEM 6.5, Service Pack 21: 6 de junio de 2024

### [!DNL Assets]

#### Mejoras

La pestaña IPTC ahora admite los campos de texto [!UICONTROL Texto alternativo] y [!UICONTROL Descripción extendida]. (Assets-34918)

#### Accesibilidad

* Si el estado de procesamiento de un recurso es Error o Error de metadatos, la interfaz de usuario de subtítulos y pistas de audio ahora funciona correctamente. (Assets-37281)
* Al guardar los metadatos de un recurso e intentar editarlos, ahora se muestra el nombre del idioma. (Assets-37281)

### [!DNL Forms]

* **Compatibilidad con credenciales de Oauth**: Una credencial nueva y más fácil de usar para la autenticación de servidor a servidor, que reemplaza la credencial de cuenta de servicio (JWT) existente. (NPR-41994)
* [Mejoras del editor de reglas en AEM Forms](/help/forms/using/rule-editor-core-components.md):
   * Compatibilidad para implementar condiciones anidadas con la funcionalidad `When-then-else`.
   * Validar o restablecer paneles y formularios, incluidos campos.
   * Compatibilidad con funciones modernas de JavaScript, como las funciones izquierda y flecha (compatibilidad con ES10) dentro de las funciones personalizadas.
* [API de AutoTag para la accesibilidad de PDF](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services): AEM Forms en OSGi ahora admite la nueva API de AutoTag para mejorar PDF para los estándares de accesibilidad al agregar etiquetas: párrafos y listas. Hace que los archivos PDF sean más accesibles para los usuarios con tecnología de asistencia.
* **Compatibilidad con PNG de 16 bits**: el servicio ImageToPdf de PDF Generator ahora admite la conversión de PNG con una profundidad de color de 16 bits.
* **Aplicar artefactos a bloques de texto individuales en XDP**: Forms Designer ahora permite a los usuarios establecer la configuración en bloques de texto individuales en archivos XDP. Esta capacidad permite controlar los elementos que se tratan como artefactos en los PDF resultantes. Estos elementos, como encabezados y pies de página, están disponibles para las tecnologías de asistencia. Las funciones principales incluyen marcar bloques de texto como artefactos e incrustar esta configuración en los metadatos XDP. El servicio de salida de Forms aplica esta configuración durante la generación de PDF, lo que garantiza un etiquetado adecuado de PDF/UA.
* **AEM Forms Designer está certificado con `GB18030:2022` estándar**: con la certificación `GB18030:2022`, ahora Forms Designer admite el conjunto de caracteres Unicode chino que le permite introducir caracteres chinos en todos los campos editables y cuadros de diálogo.
* [Compatibilidad con la ruta WebToPDF en el servidor JEE](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings) mediante el servicio PDF Generator ahora admite la ruta WebToPDF para convertir archivos HTML en documentos PDF en JEE. Esta compatibilidad se suma a las rutas existentes Webkit y WebCapture (solo Windows). Mientras que la ruta WebToPDF ya está disponible en OSGi y se amplía a JEE. Ahora, tanto en plataformas JEE como OSGi, el servicio PDF Generator admite las siguientes rutas en diferentes sistemas operativos:
   * **Windows**: Webkit, WebCapture, WebToPDF
   * **Linux®**: Webkit, WebToPDF


## AEM 6.5, Service Pack 20: 22 de febrero de 2024

### [!DNL Assets]

* Dynamic Media ahora es compatible con el formato de imagen HEIC sin pérdidas para Apple iOS/iPadOS. Consulte [fmt](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt) en la API de servicio y procesamiento de imágenes de Dynamic Media.
* El Administrador de varios sitios (MSM) ahora es compatible con estructuras de fragmentos de experiencias, incluidas carpetas y subcarpetas, para un despliegue masivo eficaz de fragmentos de experiencias en Live Copies.

### [!DNL Forms]

* **Informes de transacciones en AEM Forms en JEE**: la capacidad de informes de transacciones se ha introducido para AEM Forms en JEE. Permite un registro completo de las transacciones de documentos, como conversiones, representaciones y envíos. Esta mejora aumenta la eficacia y facilita un mejor mantenimiento de los registros. La función está desactivada de forma predeterminada. Puede habilitarlo desde la IU de administración.
* **Seguridad mejorada con compatibilidad con ECDSA**: AEM Forms ahora ofrece compatibilidad sólida con el algoritmo de firma digital de curva elíptica (ECDSA) en las pilas JEE y OSGi. Los usuarios ahora pueden firmar, certificar y verificar documentos de PDF con mayor seguridad. Los algoritmos de curva EC admitidos son:
   * Curva elíptica ECDSA P256 con algoritmo de resumen SHA256
   * Curva elíptica ECDSA P384 con algoritmo de resumen SHA384
   * Curva elíptica ECDSA P512 con algoritmo de resumen SHA512
* **Compatibilidad perfecta con Windows 11 para Forms Designer**: AEM Forms Designer ahora es compatible con Windows 11, lo que garantiza una instalación y un funcionamiento sin problemas. Los usuarios pueden actualizar con seguridad a Windows 11 sin tener que volver a instalar Forms Designer ni preocuparse por los problemas de compatibilidad, lo que garantiza un flujo de trabajo ininterrumpido.
* **Accesibilidad mejorada con la función &quot;Pie de ilustración&quot; personalizada en AEM Forms Designer**: AEM Forms Designer ahora incluye una función de accesibilidad personalizada llamada &quot;Pie de ilustración&quot;, que permite a los usuarios crear XDP con elementos de subtítulos personalizados. Esta función mejora la accesibilidad al permitir que los usuarios integren subtítulos personalizados en los diseños de sus documentos para que puedan mejorar la inclusividad y la experiencia del usuario.

## AEM 6.5, Service Pack 19: 7 de diciembre de 2023

* Se habilitó al usuario del Editor de páginas de sitios/Componente de imagen para hacer referencia a los recursos desde el Cloud Service de Assets remoto. (SITES-13448, SITES-13433)
* AEM ahora admite la ordenación del lado del servidor para una navegación más rápida por el proyecto en la vista de lista. Los nodos de proyecto se ordenan según la columna seleccionada por el usuario antes de aparecer en la interfaz.

### [!DNL Forms]

* **Nuevos componentes principales de formulario adaptable**: se agregan fichas verticales, términos y condiciones y casillas de verificación para mejorar la escalabilidad de los formularios.
   * **[Componente de casilla de verificación](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox)**: los Forms adaptables basados en componentes principales ahora pueden incluir un componente de casilla de verificación. Permite a los usuarios realizar elecciones binarias, seleccionando o anulando la selección de una opción en particular. Normalmente aparece como un pequeño cuadro en el que se puede hacer clic o pulsar para alternar entre dos estados: activado y desactivado. La casilla de verificación es un elemento de formulario común que se utiliza para presentar una opción sí/no o verdadero/falso.

   * **[Componente Términos y condiciones](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions)**: El Forms adaptable basado en componentes principales ahora incluye un componente Términos y condiciones. Los autores de formularios agregan esta sección para mostrar a los usuarios los términos, condiciones o acuerdos legales para el servicio, el producto o la plataforma. Este componente está diseñado para informar a los usuarios sobre las reglas, regulaciones y obligaciones que aceptan enviando el formulario.

     ![Fichas verticales, términos y condiciones y componentes de casilla de verificación](/help/forms/using/assets/forms-components.png)

   * **[Componente de pestañas verticales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)**: los Forms adaptables basados en componentes principales ahora pueden organizar el contenido del formulario en una lista vertical de pestañas, lo que proporciona un diseño estructurado y navegable. Las pestañas verticales de un formulario mejoran la experiencia del usuario al simplificar la navegación y organizar el contenido. Resultan especialmente útiles cuando el formulario contiene varias secciones o información compleja.

* **[Versión de 64 bits de AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: La versión de 64 bits de AEM Forms Designer ofrece rendimiento, escalabilidad y administración de memoria mejorados para potenciar su experiencia de creación de formularios. Con la arquitectura de 64 bits, puede abordar proyectos aún más grandes y complejos con facilidad, lo que garantiza flujos de trabajo de diseño sin problemas y eficiencia optimizada. Aumente sus capacidades de diseño de formularios y disfrute del futuro de AEM Forms Designer con esta versión de vanguardia.

* **[Conectar un Forms adaptable con Microsoft® SharePoint List](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: AEM Forms proporciona una integración predeterminada para enviar datos de formulario directamente a SharePoint List, lo que le permite utilizar las funciones de Listas de SharePoint. Puede configurar la lista de Microsoft® SharePoint como fuente de datos para un modelo de datos de formulario y utilizar la acción de envío Enviar mediante el modelo de datos de formulario para conectar un formulario adaptable con una lista de SharePoint.

* **[Compatibilidad para configurar las propiedades del documento de registro para los fragmentos de formulario adaptable](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: ahora puede personalizar fácilmente los fragmentos de formulario adaptable y sus campos en el editor de formularios adaptables.

* **XMLFM de 64 bits**: La iteración de 64 bits de XMLFM presenta un rendimiento, escalabilidad y administración de memoria mejorados. Es el primer servicio nativo de 64 bits implementado en el lado del servidor. Al aprovechar su capacidad inherente para acceder a mayores recursos de memoria en comparación con su homólogo de 32 bits, XMLFM de 64 bits permite una gestión perfecta de mayores cargas de trabajo de procesamiento. Este hito no solo representa un salto en el rendimiento, sino que también introduce mejoras clave en el marco de servicio nativo dentro del servidor de AEM Forms. Esta actualización equipa a AEM Forms Server para admitir sin problemas cualquier servicio nativo de 64 bits.

## AEM 6.5, Service Pack 18: 24 de agosto de 2023

* Assets, Dynamic Media - [Compatibilidad con múltiples subtítulos y pistas de audio para vídeos en Dynamic Media](/help/assets/video.md#about-msma): Ahora puede agregar fácilmente varios subtítulos y pistas de audio a un vídeo principal. Esta capacidad significa que los vídeos son accesibles para un público global. Puede personalizar un solo vídeo principal publicado para un público global en varios idiomas y seguir las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.
* Assets: desde los resultados de búsqueda, ahora puede navegar a la ubicación de la carpeta que contiene un recurso para permitirle realizar varias tareas de administración de recursos.
* El Selector de estrella de Sites en Fragmentos de contenido ha mejorado el rendimiento.
* Se habilitó al usuario del Editor de páginas de sitios/Componente de imagen para hacer referencia a los recursos desde el Cloud Service de Assets remoto.
* Para encontrar rápidamente un proyecto en la Vista de lista, donde puede tener muchos proyectos en el sistema, Adobe ahora admite la ordenación del lado del servidor. Los nodos del proyecto se ordenan en el servidor en función de la columna seleccionada por el usuario antes de procesarlos en la interfaz de usuario.
* AEM 6.5.18.0 admite MongoDB 5.0 a 6.0.

### [!DNL Forms]

* **[Tratamiento de errores mejorado con controladores de errores personalizados en el editor de reglas](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms)**. Ahora puede invocar una función personalizada (mediante la biblioteca de cliente) en respuesta a un error devuelto por un servicio externo. Además, puede proporcionar una respuesta adaptada a los usuarios finales. O bien, puede realizar acciones específicas en busca de errores devueltos por un servicio. Por ejemplo, puede invocar un flujo de trabajo personalizado en el backend para códigos de error específicos o informar al cliente de que el servicio está inactivo

* **[Paso mejorado del flujo de trabajo de Adobe Sign](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow-step-reference#sign-document-step)**: El paso del flujo de trabajo de Adobe Sign en los flujos de trabajo de AEM está disponible con las siguientes mejoras.

   * **Seguridad mejorada con autenticación basada en Id. de gobierno para Adobe Sign**: la autenticación basada en Id. de gobierno de Adobe Acrobat Sign ofrece un nivel de verificación adicional. Permite a los usuarios autenticar su identidad usando ID emitidos por el gobierno (licencia de conducir, identificación nacional, pasaporte). Al utilizar documentos de identificación de confianza, esta mejora añade un nivel adicional de confianza al proceso de firma, lo que lo hace ideal para situaciones que requieren una mayor seguridad, conformidad y validación del usuario.

   * **Transparencia mejorada con la pista de auditoría para documentos de Adobe Sign**: utilice la función Pista de auditoría para obtener información detallada sobre el ciclo de vida de sus documentos de Adobe Sign. Con la pista de auditoría, ahora puede mantener un registro completo de todas las acciones e interacciones relacionadas con sus documentos. Estas acciones e interacciones incluyen quién vio, editó o firmó el documento, junto con las marcas de tiempo de cada evento. Esta mejora es crucial para mantener el cumplimiento, resolver disputas y garantizar la integridad de los acuerdos digitales.


   * **Se han expandido las funciones de los destinatarios del Contrato más allá del Firmante**. Adobe Acrobat Sign le permite expandir las funciones de los destinatarios del Contrato más allá del Firmante para que coincidan mejor con sus requisitos de flujo de trabajo. Cuando se habilita, cada destinatario de un acuerdo tiene su función configurable individualmente, con firmante como predeterminado.


* **[Programa de instalación completo de AEM Forms en JEE](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)** - El Service Pack incluye un programa de instalación completo para AEM Forms en JEE que ofrece soporte para varias combinaciones de software nuevas, entre ellas:
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C en Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * Conector JDBC 8 de MySQL

Si va a instalar o planea utilizar el software más reciente para su Forms de AEM 6.5 en el entorno JEE, Adobe recomienda utilizar el programa de instalación completo de AEM 6.5.18.0 Forms en JEE. Para explorar la lista completa de software recién agregado y obsoleto, consulte la documentación de AEM Forms en JEE o AEM Forms en OSGi.

## AEM 6.5, Service Pack 17: 25 de mayo de 2023

* **Mejoras en la experiencia de búsqueda**: ahora puede realizar rápidamente las siguientes operaciones en los archivos que se muestran en los resultados de búsqueda:
   * Crear un flujo de trabajo
   * Crear una versión
   * Relacionar o desrelacionar archivos

  No es necesario desplazarse a la ubicación del recurso y ver sus propiedades para realizar estas operaciones.

* **Dynamic Media _Snapshot_**&#x200B;le permite obtener una vista previa de los modificadores de imagen y las optimizaciones de imágenes inteligentes, como la salida WebP o AVIF, la compresión según el ancho de banda y la escala de la proporción de píxeles del dispositivo, mediante imágenes de prueba o URL de Dynamic Media. A continuación, puede comparar inmediatamente cómo afecta cada configuración a la calidad y al tamaño del archivo.
Consulte la [Instantánea de Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot).
* **Flujo DASH con Dynamic Media**: Se ha iniciado un nuevo protocolo (DASH - Flujo adaptable dinámico a través de HTTP) para el flujo adaptable en la entrega de vídeo de Dynamic Media (con CMAF habilitado). Ya está disponible para todas las regiones.
* **Integración de Experience Manager Sites y fragmentos de contenido con Dynamic Media de próxima generación de Assets**: Los usuarios ahora pueden utilizar sus recursos alojados en la nube en Experience Manager Sites 6.5. Pueden crear y enviar esos recursos en instancias locales o de Managed Services.

### [!DNL Forms]

* **[Forms adaptable en el editor de páginas de AEM](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**: ahora puede usar el editor de páginas de AEM para crear y agregar rápidamente varios formularios a las páginas de sus sitios. Esta capacidad permite a los autores de contenido crear experiencias de captura de datos sin problemas dentro de las páginas de Sites mediante el uso de la potencia de los componentes de los formularios adaptables, incluido el comportamiento dinámico, las validaciones, la integración de datos, la generación de documentos de registro y la automatización del proceso empresarial. Puede hacer lo siguiente:
   * Cree un formulario adaptable arrastrando y soltando componentes de formulario en el componente Contenedor de Forms adaptable en el editor de AEM Sites o en los fragmentos de experiencias.
   * Utilice el asistente de Forms adaptable dentro del editor de AEM Sites para poder crear formularios independientes de cualquier página de Sites, lo que le proporciona la libertad de reutilizar dichos formularios en varias páginas.
   * Agregue varios formularios a una página de Sites, lo que optimizará la experiencia del usuario y proporcionará una mayor flexibilidad.
* **[Compatibilidad con reCAPTCHA Enterprise en Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)**: se ha agregado compatibilidad con reCAPTCHA Enterprise en Experience Manager Forms. Esta capacidad proporciona una protección mejorada contra actividades fraudulentas y spam, además de la compatibilidad existente con Google reCAPTCHA v2.
* **[Se ha agregado compatibilidad con Adobe Acrobat Sign para Administración Pública con Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**. AEM Forms ahora se integra con Adobe Acrobat Sign para Administración Pública (compatible con FedRAMP). Esta integración proporciona un nivel avanzado de cumplimiento y seguridad para las firmas electrónicas con envíos de formularios adaptables para cuentas asociadas con el gobierno (departamentos y agencias gubernamentales). Las integraciones con Adobe Acrobat Sign para gobiernos permiten a los socios y clientes gubernamentales de Adobe utilizar firmas electrónicas en Forms adaptable para algunas de las líneas de negocio más críticas y sensibles. Este nivel adicional de seguridad garantiza que todas las firmas electrónicas cumplan plenamente con la normativa FedRAMP Moderate, lo que proporciona tranquilidad a los clientes de la administración pública de Adobe.
* **Habilitar la integración de Salesforce con Experience Manager Forms para el intercambio de datos**: configure la integración entre Experience Manager Forms y la aplicación de Salesforce mediante el flujo de credenciales de cliente de OAuth 2.0. Esta capacidad permite la autenticación y autorización seguras y directas de la aplicación y permite una comunicación fluida sin la participación del usuario.
* **Optimización y funcionalidad mejorada del motor de flujo de trabajo**: aumente el rendimiento de los motores de flujo de trabajo al minimizar el número de instancias de flujo de trabajo. Además de los valores de estado `COMPLETED` y `RUNNING`, el flujo de trabajo también admite tres nuevos valores de estado: `ABORTED`, `SUSPENDED` y `FAILED`.

## AEM 6.5, Service Pack 16: 23 de febrero de 2023

Se inició el nuevo protocolo DASH (Dynamic Adaptive Streaming over HTTP) para la transmisión de velocidad de bits adaptable en la entrega de vídeo de Dynamic Media (con CMAF [Formato de aplicación de medios comunes] habilitado).

* El streaming adaptable (DASH/HLS) garantiza una mejor experiencia de visualización para los usuarios finales de los vídeos.
* DASH es el protocolo estándar internacional para la transmisión de vídeo adaptable y tiene una amplia aceptación en la industria.
* Disponible ahora en Asia-Pacífico y Norteamérica; próximamente en Europa-Oriente Medio-África.

### [!DNL Forms]

* [Forms adaptable sin encabezado](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/overview) permite a los desarrolladores crear, publicar y administrar formularios interactivos a los que se puede acceder e interactuar mediante API, en lugar de hacerlo a través de una interfaz gráfica de usuario tradicional.

* [Los componentes principales adaptables de Forms](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#features) son un conjunto de 24 componentes de código abierto compatibles con BEM creados sobre la base de los componentes principales de Adobe Experience Manager WCM. Estos componentes son de código abierto y proporcionan a los desarrolladores la capacidad de personalizar y ampliar fácilmente estos componentes para que coincidan con las necesidades específicas de su organización. Cualquier persona con habilidades existentes para personalizar [componentes principales de WCM](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/get-started/authoring) puede personalizar y aplicar estilo fácilmente a estos componentes.

* El servicio Extensiones de Reader en OSGi ahora proporciona opciones independientes para habilitar los derechos de uso de importación y exportación en una PDF para importar o exportar datos en Adobe Acrobat Reader.
