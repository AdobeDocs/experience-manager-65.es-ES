---
title: Funciones clave acumulativas y mejoras en la versión de Adobe Experience Manager 6.5.
description: Una lista acumulativa de las funciones y mejoras clave realizadas en Adobe Experience Manager 6.5 con respecto a las ocho versiones de Service Pack anteriores.
content-type: reference
docset: aem65
feature: Release Information
role: User, Admin
source-git-commit: 4fab3f80e01c2b7c3e4ebdc4bffdedb6f5f39d11
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 19%

---


# Funciones clave acumulativas y mejoras

Una lista acumulativa de las principales funciones y mejoras de Adobe Experience Manager 6.5 para las ocho versiones de Service Pack anteriores.

Consulte también [Últimas notas de la versión de Adobe Experience Manager 6.5 Service Pack](/help/release-notes/release-notes.md).

## AEM.5, paquete de servicio 18: 7 de diciembre de 2023

* Se habilitó al usuario del Editor de páginas de sitios/Componente de imagen para hacer referencia a los recursos desde el Cloud Service de recursos remoto. (SITES-13448, SITES-13433)
* AEM Ahora admite la ordenación del lado del servidor para una navegación más rápida por el proyecto en la vista de lista. Los nodos de proyecto se ordenan según la columna seleccionada por el usuario antes de aparecer en la interfaz.

### [!DNL Forms]

* **Nuevos componentes principales de formulario adaptable**: Se agregan pestañas verticales, Términos y condiciones y Casilla de verificación para mejorar la escalabilidad de los formularios.
   * **[Componente Casilla](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: el Forms adaptable basado en componentes principales ahora puede incluir un componente de casilla de verificación. Permite a los usuarios realizar elecciones binarias, seleccionando o anulando la selección de una opción en particular. Normalmente aparece como un pequeño cuadro en el que se puede hacer clic o pulsar para alternar entre dos estados: activado y desactivado. La casilla de verificación es un elemento de formulario común que se utiliza para presentar una opción sí/no o verdadero/falso.

   * **[Componente Términos y condiciones](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: Forms adaptable basado en componentes principales ahora puede incluir un componente Términos y condiciones. Permite a los autores de Forms introducir una sección específica dentro del formulario en la que se presentan a los usuarios los términos, condiciones o acuerdos legales asociados al uso de un servicio, producto o plataforma. Este componente está diseñado para informar a los usuarios sobre las reglas, regulaciones y obligaciones que aceptan enviando el formulario.

     ![Pestañas verticales, términos y condiciones y componentes de casilla de verificación](/help/forms/using/assets/forms-components.png)

   * **[Componente de pestañas verticales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: Forms adaptable basado en componentes principales ahora puede organizar el contenido del formulario en una lista vertical de pestañas, lo que proporciona un diseño estructurado y navegable. El uso de pestañas verticales en un formulario puede mejorar la experiencia general del usuario al simplificar la navegación y mejorar la organización del contenido del formulario, especialmente en situaciones en que un formulario contiene varias secciones o información compleja.

* **[Versión de 64 bits de AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: la versión de 64 bits de AEM Forms Designer ofrece un rendimiento, una escalabilidad y una administración de memoria mejorados para potenciar su experiencia de creación de formularios. Con la arquitectura de 64 bits, puede abordar proyectos aún más grandes y complejos con facilidad, lo que garantiza flujos de trabajo de diseño sin problemas y eficiencia optimizada. Aumente sus capacidades de diseño de formularios y disfrute del futuro de AEM Forms Designer con esta versión de vanguardia.

* **[Conectar un Forms adaptable con Microsoft® SharePoint List](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: AEM Forms proporciona una integración OOTB para enviar datos de formulario directamente a SharePoint List, lo que le permite utilizar las funciones de Listas de SharePoint. Puede configurar la lista de Microsoft® SharePoint como fuente de datos para un modelo de datos de formulario y utilizar la acción de envío Enviar mediante el modelo de datos de formulario para conectar un formulario adaptable con una lista de SharePoint.

* **[Compatibilidad para configurar las propiedades del documento de registro para los fragmentos de formulario adaptable](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: Ahora puede personalizar fácilmente los fragmentos del formulario adaptable y sus campos en el editor de formularios adaptables.

* **XMLFM de 64 bits**: la iteración de 64 bits de XMLFM introduce un rendimiento, una escalabilidad y una administración de memoria mejorados. Es el primer servicio nativo de 64 bits implementado en el lado del servidor. Al aprovechar su capacidad inherente para acceder a mayores recursos de memoria en comparación con su homólogo de 32 bits, XMLFM de 64 bits permite una gestión perfecta de mayores cargas de trabajo de procesamiento. Este hito no solo representa un salto en el rendimiento, sino que también introduce mejoras clave en el marco de servicio nativo dentro del servidor de AEM Forms. Esta actualización equipa a AEM Forms Server para admitir sin problemas cualquier servicio nativo de 64 bits.

## AEM.5, paquete de servicio 18: 24 de agosto de 2023

* Recursos, Dynamic Media - [Compatibilidad con subtítulos múltiples y pistas de audio múltiple para vídeos en Dynamic Media](/help/assets/video.md#about-msma): ahora se pueden añadir fácilmente varios subtítulos y varias pistas de audio a un vídeo principal. Esta posibilidad significa que los vídeos son accesibles para todo el público global. Puede personalizar un solo vídeo principal publicado para un público global en varios idiomas y seguir las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.
* Recursos: desde los resultados de búsqueda, ahora puede navegar a la ubicación de la carpeta que contiene un recurso para permitirle realizar varias tareas de administración de recursos.
* El Selector de estrella de Sites en Fragmentos de contenido ha mejorado el rendimiento.
* Se habilitó al usuario del Editor de páginas de sitios/Componente de imagen para hacer referencia a los recursos desde el Cloud Service de recursos remoto.
* Para encontrar rápidamente un proyecto en la Vista de lista, donde puede tener muchos proyectos en el sistema, el Adobe ahora admite la ordenación del lado del servidor. Los nodos del proyecto se ordenan en el servidor en función de la columna seleccionada por el usuario antes de procesarlos en la interfaz de usuario.
* AEM 6.5.18.0 es compatible con MongoDB 5.0 a 6.0.

### [!DNL Forms]

* **[Tratamiento de errores mejorado con controladores de error personalizados en el editor de reglas](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html?lang=es)** : Ahora puede invocar una función personalizada (mediante la Biblioteca de clientes) en respuesta a un error devuelto por un servicio externo. Además, puede proporcionar una respuesta adaptada a los usuarios finales. O bien, puede realizar acciones específicas en busca de errores devueltos por un servicio. Por ejemplo, puede invocar un flujo de trabajo personalizado en el backend para códigos de error específicos o informar al cliente de que el servicio está inactivo

* **[Paso de flujo de trabajo de Adobe Sign mejorado](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step)** : El paso del flujo de trabajo de Adobe Sign AEM en Flujos de trabajo de está disponible con las siguientes mejoras.

   * **Seguridad mejorada con autenticación basada en Id. de gobierno para Adobe Sign** - La autenticación basada en documentos de identidad oficiales de Adobe Acrobat Sign ofrece un nivel adicional de verificación. Permite a los usuarios autenticar su identidad usando ID emitidos por el gobierno (licencia de conducir, identificación nacional, pasaporte). Al utilizar documentos de identificación de confianza, esta mejora añade un nivel adicional de confianza al proceso de firma, lo que lo hace ideal para situaciones que requieren una mayor seguridad, conformidad y validación del usuario.

   * **Transparencia mejorada con pista de auditoría para documentos de Adobe Sign** : utilice la función Pista de auditoría para obtener información detallada sobre el ciclo de vida de los documentos de Adobe Sign. Con la pista de auditoría, se puede mantener un registro completo de todas las acciones e interacciones relacionadas con los documentos. Esto incluye detalles como quién vio, editó o firmó el documento, junto con marcas de tiempo para cada evento. Esta mejora es crucial para mantener el cumplimiento, resolver disputas y garantizar la integridad de los acuerdos digitales.


   * **Se han ampliado las funciones de los destinatarios del Acuerdo más allá del Firmante** : Adobe Acrobat Sign permite ampliar las funciones de los destinatarios del acuerdo más allá del firmante para que coincidan mejor con los requisitos del flujo de trabajo. Cuando se habilita, cada destinatario de un acuerdo tiene su función configurable individualmente, con firmante como predeterminado.


* **[Programa de instalación completo de AEM Forms en JEE](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)** : El Service Pack incluye un instalador completo para AEM Forms en JEE que admite varias combinaciones de software nuevas, entre las que se incluyen:
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle de WebLogic 14C en Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * Conector JDBC 8 de MySQL

Si va a instalar o planea utilizar el software más reciente para su Forms de 6.5 en el entorno JEE, Adobe AEM recomienda utilizar el programa de instalación completo de Forms 6.5.18.0 en JEE de AEM. Para explorar la lista completa de software recién agregado y obsoleto, consulte la documentación de AEM Forms en JEE o AEM Forms en OSGi.

## AEM.5, paquete de servicio 17: 25 de mayo de 2023

* **Mejoras en la experiencia de búsqueda**: ahora puede realizar rápidamente las siguientes operaciones en los archivos que se muestran en los resultados de búsqueda:
   * Crear un flujo de trabajo
   * Crear una versión
   * Relacionar o desrelacionar archivos

  No es necesario desplazarse a la ubicación del recurso y ver sus propiedades para realizar estas operaciones.
* **Dynamic Media _Instantánea_**: Experimente con imágenes de prueba o URL de Dynamic Media para ver la salida de diferentes modificadores de imagen y optimizaciones de imágenes inteligentes para el tamaño de archivo (con entrega WebP y AVIF), el ancho de banda de la red y la proporción de píxeles del dispositivo. Consulte la [Instantánea de Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=es).
* **Streaming DASH con Dynamic Media** - Se ha lanzado la compatibilidad con el nuevo protocolo (DASH - Dynamic Adaptive Streaming over HTTP) para el streaming adaptable en la entrega de vídeo de Dynamic Media (con CMAF habilitado). Disponible ahora para todas las regiones, [habilitado mediante un ticket de asistencia](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Integración de Experience Manager Sites y fragmentos de contenido con Dynamic Media de próxima generación de recursos** : Los usuarios de Experience Manager Assets as a Cloud Service Next-Generation Dynamic Media ahora pueden utilizar esos recursos alojados en la nube para la creación y el envío con instancias on-premise o Managed Services de Experience Manager Sites 6.5.

### [!DNL Forms]

* **[Formularios adaptables en el editor de páginas de AEM](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**: ahora puede utilizar el editor de páginas de AEM para crear y agregar rápidamente varios formularios a sus páginas de Sites. Esta capacidad permite a los autores de contenido crear experiencias de captura de datos sin problemas dentro de las páginas de Sites mediante el uso de la potencia de los componentes de los formularios adaptables, incluido el comportamiento dinámico, las validaciones, la integración de datos, la generación de documentos de registro y la automatización del proceso empresarial. Puede hacer lo siguiente:
   * Cree un formulario adaptable arrastrando y soltando componentes de formulario en el componente contenedor de formularios adaptables en el editor de AEM Sites o en los fragmentos de experiencias.
   * Utilice el asistente de formularios adaptables dentro del editor de AEM Sites para poder crear formularios independientes de cualquier página de Sites, lo que le proporciona la libertad de reutilizar dichos formularios a través de varias páginas.
   * Agregue varios formularios a una página de Sites, lo que optimizará la experiencia del usuario y proporcionará una mayor flexibilidad.
* **[Compatibilidad con reCAPTCHA Enterprise en Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)**: Se ha añadido compatibilidad con reCAPTCHA Enterprise en Experience Manager Forms, que proporciona una protección mejorada contra actividades fraudulentas y spam, además de la compatibilidad con reCAPTCHA v2 de Google.
* **[Compatibilidad con Adobe Acrobat Sign para Administración Pública con Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**: AEM Forms ahora se integra con Adobe Acrobat Sign para Administración Pública (compatible con FedRAMP). Esta integración proporciona un nivel avanzado de cumplimiento y seguridad para las firmas electrónicas con envíos de formularios adaptables para cuentas asociadas con el gobierno (departamentos y agencias gubernamentales). La integración con Adobe Acrobat Sign para la Administración Pública permite a los socios de Adobe y a los clientes de la administración pública utilizar firmas electrónicas en los formularios adaptables para algunas de las líneas de negocio más importantes y sensibles. Este nivel adicional de seguridad garantiza que todas las firmas electrónicas cumplan plenamente con la normativa FedRAMP Moderate, lo que proporciona tranquilidad a los clientes de la administración pública de Adobe.
* **Habilitar la integración de Salesforce con Experience Manager Forms para el intercambio de datos**: configure la integración entre Experience Manager Forms y la aplicación Salesforce mediante el flujo de credenciales del cliente OAuth 2.0. Esta capacidad permite la autenticación y autorización seguras y directas de la aplicación y permite una comunicación fluida sin la participación del usuario.
* **Optimización y funcionalidad mejorada del motor de flujo de trabajo**: aumente el rendimiento de los motores de flujo de trabajo minimizando el número de instancias de flujo de trabajo. Además de `COMPLETED` y `RUNNING` valores de estado, el flujo de trabajo también admite tres nuevos valores de estado: `ABORTED`, `SUSPENDED`, y `FAILED`.

## AEM.5, paquete de servicio 16: 23 de febrero de 2023

Nuevo protocolo compatible con DASH (Dynamic Adaptive Streaming over HTTP) para el streaming de velocidad de bits adaptable en la entrega de vídeo de Dynamic Media (con CMAF) [Formato común de aplicación de medios] activada).

* El streaming adaptable (DASH/HLS) garantiza una mejor experiencia de visualización para los usuarios finales de los vídeos.
* DASH es el protocolo estándar internacional para la transmisión de vídeo adaptable y tiene una amplia aceptación en la industria.
* Disponible ahora en Asia-Pacífico y Norteamérica (se habilitará mediante un ticket de asistencia); próximamente en Europa-Oriente Medio-África.

Consulte [Habilitar DASH en su cuenta](/help/assets/video.md#enable-dash).

### [!DNL Forms]

* [Forms adaptable sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es) permita a los desarrolladores crear, publicar y administrar formularios interactivos a los que se puede acceder e interactuar mediante API, en lugar de hacerlo a través de una interfaz gráfica de usuario tradicional.

* [Componentes principales de Forms adaptable](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es#features) son un conjunto de 24 componentes de código abierto compatibles con BEM creados sobre la base de los componentes principales de Adobe Experience Manager WCM. Estos componentes son de código abierto y proporcionan a los desarrolladores la capacidad de personalizar y ampliar fácilmente estos componentes para que coincidan con las necesidades específicas de su organización. Cualquier persona con habilidades para personalizar [Componentes principales de WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html) Puede personalizar fácilmente y aplicar estilo a estos componentes.

* El servicio Extensiones de Reader en OSGi ahora proporciona opciones independientes para habilitar los derechos de importación y exportación de uso en un PDF para importar o exportar datos en Adobe Acrobat Reader.

## AEM.5, paquete de servicio 15: 24 de noviembre de 2022

### [!DNL Forms]

* AEM Forms Designer ya está disponible en [Configuración regional en español](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
* Ahora puede utilizar [OAuth2 para autenticarse con los protocolos de servidor de correo de Microsoft® Office 365 (SMTP e IMAP)](/help/forms/using/oauth2-support-for-mail-service.md).
* Puede establecer [Revalidar en el servidor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=es#enabling-server-side-validation-br) propiedad a true para identificar los campos ocultos para la exclusión de un documento de registro del lado del servidor.
* AEM Forms Designer requiere una versión de 32 bits de Visual C++ 2019 redistribuible (x86).

## AEM.5, paquete de servicio 14: 25 de agosto de 2022

Solo correcciones de errores.

## AEM.5, paquete de servicio 13: 26 de mayo de 2022

* Utilizar un CAPTCHA invisible en un formulario adaptable: ahora puede utilizar un CAPTCHA invisible para mostrar el desafío CAPTCHA solo si hay actividad sospechosa. Si no se encuentra ninguna actividad sospechosa, no se muestra el desafío CAPTCHA. Ayuda a evaluar la cumplimentación de formularios humanos sin requisitos de casilla de verificación, reducir los esfuerzos de personalización y mejorar la experiencia del usuario final.

* Se ha agregado compatibilidad para recuperar encabezados de respuesta en el postprocesador del modelo de datos de formulario para extremos REST.

* Ahora, al generar un archivo de traducción de formulario adaptable, la misma secuencia de textos que el archivo XLIFF generado es idéntica a la secuencia de componentes del formulario adaptable correspondiente.

* Cuando localiza un formulario adaptable y realiza incluso un pequeño cambio en el texto del idioma base, la traducción completa no aparece para todos los demás idiomas. El problema se corrige en [!DNL Experience Manager] 6.5.13.0.

* Mejoras de accesibilidad para Forms:

   * Se ha agregado compatibilidad para que los lectores de pantalla reconozcan el encabezado y el cuerpo de una tabla como entidades continuas y conectadas. Ayuda a los lectores de pantalla a navegar correctamente por las tablas. (NPR-37139)
   * Se ha agregado compatibilidad para que los lectores de pantalla dejen de navegar por el espacio de trabajo del HTML hasta que se abra un cuadro de diálogo.

## AEM.5, paquete de servicio 12: 24 de febrero de 2022

* Después de configurar una conexión entre las implementaciones remotas de DAM y Sites, los recursos en DAM remoto están disponibles en la implementación de Sites. Ahora puede realizar las operaciones de actualización, eliminación, cambio de nombre y movimiento en los recursos o carpetas DAM remotos. Las actualizaciones, con algún retraso, están disponibles automáticamente en la implementación de Sites.
* Ahora, los despliegues push de un origen de Live Copy a varias Live Copies son posibles de forma predeterminada, sin requerir una configuración de modelo.
* El estado de las operaciones asincrónicas en curso ahora se muestra en la interfaz de usuario para ayudar a evitar que los usuarios activen accidentalmente varias operaciones asincrónicas en la misma ruta.
* Las API de Analytics 2.0 admiten la autenticación basada en IMS.
* Compatibilidad con API para el fragmento de experiencia de tipo de oferta JSON.
* La solicitud de oferta ahora se proporciona para Eliminar oferta (API de fragmento de experiencia) en IMS.
* El repositorio integrado (Apache Jackrabbit Oak) sigue siendo 1.22.9.
