---
title: Integración con las prácticas recomendadas de Adobe Creative Cloud
description: Prácticas recomendadas para integrar [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] para optimizar los flujos de trabajo de transferencia de recursos y lograr una alta velocidad de contenido.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
translation-type: tm+mt
source-git-commit: c4cfb709162ca8f8f6e8508516c39542347c6bc4
workflow-type: tm+mt
source-wordcount: '3254'
ht-degree: 16%

---

# [!DNL Adobe Experience Manager] y prácticas recomendadas de  [!DNL Creative Cloud] integración  {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] es una solución de administración de recursos digitales (DAM) con la que se puede integrar  [!DNL Adobe Creative Cloud] para ayudar a los usuarios de DAM a trabajar junto con los equipos creativos, lo que optimiza la colaboración en el proceso de creación de contenido.

[!DNL Adobe Creative Cloud] proporciona a los equipos creativos un ecosistema de soluciones y servicios para ayudarles a crear recursos digitales. Incluye aplicaciones de escritorio y móviles, servicios en la nube como almacenamiento con sincronización de escritorio o experiencia web, así como mercados como [!DNL Adobe Stock].

Siga leyendo para saber qué integraciones escoger entre el escritorio y el DAM de nivel empresarial en función de su caso de uso y cuáles son las prácticas recomendadas asociadas para los flujos de trabajo de conexión.

>[!NOTE]
>
>[!DNL Experience Manager] el uso compartido de  [!DNL Creative Cloud] carpetas está obsoleto y ya no se trata en esta guía. Adobe recomienda utilizar funciones más nuevas, como [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) o [Experience Manager desktop app](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html), para proporcionar al usuario creativo acceso a los recursos administrados en [!DNL Experience Manager].

## Necesidades de colaboración de creativos, especialistas en marketing y usuarios de DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superficies implicadas |
|---|---|---|
| Simplificar la experiencia para creativos en equipos de escritorio | Optimice el acceso a los recursos desde un DAM ([!DNL Experience Manager Assets]) para los profesionales creativos o, en términos más generales, para los usuarios de escritorio que trabajen en aplicaciones nativas de creación de recursos. Necesitan una forma sencilla y sencilla de descubrir, utilizar (abrir), editar y guardar cambios en [!DNL Experience Manager], así como cargar nuevos archivos. | escritorio Win o Mac; Aplicaciones [!DNL Creative Cloud] |
| Proporcionar activos listos para usar de alta calidad desde [!DNL Adobe Stock] | Los especialistas en marketing ayudan a acelerar el proceso de creación de contenido mediante la asistencia en el abastecimiento y descubrimiento de recursos. Los profesionales creativos utilizan los recursos aprobados directamente desde sus herramientas creativas. | [!DNL Experience Manager Assets];  [!DNL Adobe Stock] marketplace; campos de metadatos |
| Distribuir y compartir recursos por organizaciones | Los departamentos internos/las sucursales locales y los socios, distribuidores y agencias externos utilizan los recursos aprobados compartidos por la organización principal. La organización desea compartir de forma segura y transparente los recursos creados para una reutilización más amplia. | Brand Portal, Asset Share Commons |

## Las ofertas de Adobe para soportar la colaboración necesitan {#adobe-offerings-to-support-the-collaboration-need}

| Propuesta de valor para las personas implicadas | oferta de Adobe | Superficies implicadas |
|---|---|---|
| Los usuarios creativos descubren recursos de [!DNL Experience Manager], los abren y usan, editan y cargan cambios en [!DNL Experience Manager], así como cargan nuevos archivos en [!DNL Experience Manager], sin salir de las aplicaciones [!DNL Creative Cloud]. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator], y  [!DNL Adobe InDesign]. |
| Los usuarios empresariales simplifican la apertura y el uso de recursos, editan y cargan cambios en [!DNL Experience Manager] y cargan nuevos archivos en [!DNL Experience Manager] desde el entorno de escritorio. Utilizan una integración genérica para abrir cualquier tipo de recurso en la aplicación de escritorio nativa, incluidos los que no sean de Adobe. | [aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] aplicación de escritorio en escritorio Win y Mac |
| Los especialistas en marketing y los usuarios empresariales descubren, previsualizan, otorgan licencias y guardan y administran los [!DNL Adobe Stock] recursos desde [!DNL Experience Manager]. Los recursos con licencia y guardados proporcionan [!DNL Adobe Stock] metadatos seleccionados para un mejor gobierno. | [Integración de Experience Manager y Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interfaz web |

Este artículo se centra principalmente en los dos primeros aspectos de las necesidades de colaboración. La distribución y el abastecimiento de activos a escala se mencionan brevemente como un caso de uso. Para estas necesidades, considere Adobe Brand Portal o Asset Share Commons. Las soluciones alternativas como [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), las soluciones que se pueden crear en función de los componentes de [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Link Share](/help/assets/link-sharing.md), utilizando [Recursos Experience Manager](/help/assets/manage-assets.md) deben revisarse en función de requisitos específicos.

![conexiones del Creative Cloud para el Experience Manager, decida qué capacidad utilizar](assets/creative-connections-aem.png)

### Asignación de casos de uso y soluciones de Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Caso práctico    | [!DNL Adobe Asset Link] | Aplicación de escritorio de [!DNL Experience Manager]  | Observaciones / Otras soluciones |
|---|---|---|---|
| Discover : examinar carpetas DAM | Sí | [!DNL Experience Manager] Acciones de interfaz web y escritorio |  |
| Discover: acceso a colecciones DAM | Sí | [!DNL Experience Manager] Acciones de interfaz web y escritorio |  |
| Discover : busque recursos desde DAM | Sí | [!DNL Experience Manager] Acciones de interfaz web y escritorio |  |
| Usar - Abrir recurso | Sí | Sí | [Abrir desde interfaz web ](manage-assets.md#previewing-assets) o desde Finder |
| Usar: colocar un recurso de DAM en un documento | Sí: incrustar | Sí: vinculación o incrustación | [!DNL Experience Manager] la aplicación de escritorio proporciona acceso a los recursos como archivos en el sistema de archivos local. Estos vínculos en las aplicaciones nativas se representan mediante rutas locales. |
| Editar: abrir para edición | Sí: acción de cierre de compra | Sí: acción abierta (en el recurso compartido de red) | [El registro en ](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) AAL guarda el recurso en la cuenta de almacenamiento de Creative Cloud del usuario (sincronizada por la aplicación de Creative Cloud) de forma predeterminada. |
| Editar: trabajo en curso fuera de DAM | Sí: el recurso está disponible en la cuenta de almacenamiento del Creative Cloud del usuario sincronizada con el escritorio. | Sí |  |
| Editar: cargar cambios | Sí - [Acción de check-in](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) con comentario opcional | Sí |  |
| Cargar: un solo archivo | Sí: carga el documento activo actual | Sí | [Carga mediante la interfaz web](manage-assets.md#uploading-assets) |
| Cargar: varios archivos / estructuras de carpetas jerárquicas | No | Sí | [Cargue a través de una interfaz web ](manage-assets.md#uploading-assets) o a través de una herramienta o una secuencia de comandos personalizada. |
| Misc: usuario e inicio de sesión | Se reconoce el nombre del usuario Creative Cloud que ha iniciado sesión en la aplicación de escritorio de Creative Cloud (SSO) | [!DNL Experience Manager] usuario y credenciales | Los usuarios de ambas soluciones cuentan para la cuota de usuario [!DNL Experience Manager]. |
| Misc: red y acceso | Requiere acceso desde el escritorio del usuario a la implementación [!DNL Experience Manager] a través de la red | Requiere acceso desde el escritorio del usuario a la implementación [!DNL Experience Manager] a través de la red | [!DNL Adobe Asset Link] no comparte el entorno proxy de red. |
| Misc : migrar un gran número de recursos | No | No | [Guía de migración de recursos](assets-migration-guide.md) |

Para admitir casos de uso de distribución de recursos, se deben considerar otras soluciones:

* [Brand ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) Portal para un complemento configurable de SaaS  [!DNL Experience Manager Assets] para publicar recursos.
* Las soluciones personalizadas se crean en función del código [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* [!DNL Experience Manager] [vincular ](/help/assets/link-sharing.md) compartir para compartir recursos ad hoc mediante vínculos.
* [Experience Manager de activos ](/help/assets/manage-assets.md) con interfaz web con áreas para partes externas garantizadas por la configuración de control de  [!DNL Experience Manager] acceso y con los ajustes de configuración de red/TI necesarios, lo que proporciona acceso a estos usuarios externos a  [!DNL Experience Manager].

## Conceptos clave y casos de uso {#key-concepts-and-use-cases}

### Glosario de términos comunes {#glossary-of-common-terms}

* **Trabajo en curso o trabajo en curso creativo (WIP):** Fase del ciclo vital de los recursos en la que sufren varios cambios y, por lo general, no están listos para compartirse con equipos más amplios.
* **Recursos listos para el proceso creativo:** [!DNL Assets] que están listos para compartirse con un equipo más amplio, o bien han sido seleccionados o aprobados por el equipo creativo para compartirlos con equipos de marketing o de LOB.
* **Aprobaciones de recursos:** Proceso de aprobación que se ejecuta para los recursos ya cargados en DAM, que generalmente incluye aprobaciones de marca, aprobaciones legales, etc.
* **Recurso final:** Recurso que ha pasado por todas las aprobaciones/etiquetado de metadatos y está listo para que lo utilice el equipo superior. Este recurso se almacena en DAM y se pone a disposición de todos los usuarios (o de todos los interesados). Se puede utilizar en canales de marketing o en equipos creativos para crear diseños.
* **Cambio o actualización menor de recursos:** Un cambio rápido y pequeño en un recurso digital. A menudo se realiza como respuesta a una solicitud de edición, revisión o aprobación de recursos (por ejemplo, cambiar la posición, el tamaño del texto, ajustar la saturación/brillo, el color, etc.).
* **Cambio o actualización de recursos principales:** Un cambio en un recurso digital que requiere un trabajo considerable y que a veces debe hacerse durante un período de tiempo más largo. Generalmente incluye varios cambios. El recurso debe guardarse varias veces mientras se actualiza. Las principales actualizaciones de recursos suelen hacer que el recurso entre en una etapa de trabajo en curso.
* **DAM**: Administración de recursos digitales. En este documento, es sinónimo de [!DNL Experience Manager Assets], a menos que se mencione específicamente lo contrario.
* **Usuario creativo:** Un profesional creativo que crea recursos digitales mediante las aplicaciones y los servicios de Creative Cloud. En algunos casos, un usuario creativo puede ser miembro de un equipo creativo que puede utilizar Creative Cloud, pero no crea recursos digitales (como un director creativo o un administrador de equipo creativo).
* **Usuario de DAM:** Usuario típico de un sistema DAM. Según la organización, un usuario de DAM puede ser un usuario de marketing o no de marketing, por ejemplo un usuario de línea de negocios (LOB), bibliotecario, vendedor, etc.

### Consideraciones al utilizar la integración [!DNL Experience Manager] y [!DNL Creative Cloud] {#considerations-when-using-aem-and-creative-cloud-integration}

* Consulte [prácticas recomendadas de la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=en#best-practices-to-prevent-troubles)
* Consulte [Integración con Adobe Stock](aem-assets-adobe-stock.md)
* Consulte [Vínculo de recursos de Adobe](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Este es un breve resumen de las prácticas recomendadas para la integración [!DNL Experience Manager] y [!DNL Creative Cloud]. Lea el resto de este documento para conocer en detalle estos aspectos.

* **Para usuarios creativos que trabajan con en Photoshop, InDesign o Illustrator:** Adobe Asset Link ofrece la mejor experiencia de usuario, incluida la gestión del trabajo en curso en los recursos extraídos de [!DNL Experience Manager].
* **Para simplificar el acceso a los recursos desde el escritorio para cualquier aplicación o formato de archivo genérico:** utilice la aplicación de  [!DNL Experience Manager] escritorio.
* **Comprender por qué y cuándo almacenar recursos en DAM:** Actualizaciones que se pondrán a disposición del equipo de la organización al completo.
* **Tenga en cuenta el volumen de recursos compartidos:** Si el caso de uso es la distribución de recursos, la administración y la seguridad podrían ser los aspectos más importantes. Considere utilizar herramientas creadas para hacerlo a escala, como Brand Portal.
* **Comprenda el ciclo vital de los recursos:** Conozca cómo los distintos equipos administran los recursos en su organización
* **Gestione los ahorros frecuentes de los recursos con cuidado:** Adobe Asset Link se encarga de ello con PS, AI e ID. Para otras aplicaciones, no realice tareas de trabajo en curso en carpetas asignadas o compartidas a menos que necesite todos los cambios en DAM

### Acceso a [!DNL Adobe Stock] recursos desde [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[La ](/help/assets/aem-assets-adobe-stock.md) integración de Experience Manager y Adobe Stock permite a los  [!DNL Experience Manager] usuarios buscar, previsualizar, obtener licencias y guardar recursos  [!DNL Adobe Stock] desde  [!DNL Experience Manager]. Los [!DNL Stock] recursos con licencia y guardados han seleccionado [!DNL Stock] metadatos, que pueden utilizarse para buscarlos con filtros adicionales.

Algunos puntos importantes sobre esta integración:

* Cuando los recursos de existencias de Adobe se guardan en [!DNL Experience Manager], se convierten en [!DNL Assets] normales, con el binario guardado en el repositorio [!DNL Experience Manager]. Algunos metadatos relacionados con [!DNL Adobe Stock] se guardan para el recurso en [!DNL Experience Manager]; de lo contrario, el proceso de ingesta tiene el mismo aspecto que para cualquier otro archivo. Por ejemplo, si las etiquetas inteligentes están activas, estas se añaden a estos recursos al guardarlos.
* El recurso guardado en [!DNL Experience Manager] es una copia, no un vínculo en [!DNL Adobe Stock].

**Uso de recursos guardados  [!DNL Adobe Stock] en  [!DNL Experience Manager] en[!DNL Creative Cloud]**. Esta integración es independiente de [!DNL Adobe Asset Link], pero [!DNL Adobe Asset Link] reconoce estos recursos guardados de [!DNL Stock] de esa manera y muestra metadatos adicionales y un logotipo [!DNL Adobe Stock] en estos recursos en la interfaz de usuario de la extensión [!DNL Adobe Asset Link] en [!DNL Photoshop], [!DNL Illustrator] o [!DNL InDesign]. Los archivos están disponibles para explorar, abrir, etc., porque son recursos normales cuando se guardan en [!DNL Experience Manager].
Los usuarios creativos que trabajan en aplicaciones [!DNL Creative Cloud] con la extensión [!DNL Adobe Asset Link] presente, además de tener acceso a recursos con licencia desde [!DNL Adobe Stock] hasta [!DNL Experience Manager], también pueden utilizar el panel [!DNL Creative Cloud] Bibliotecas para buscar, obtener una vista previa y obtener la licencia de los recursos [!DNL Adobe Stock].
[!DNL Assets] de  [!DNL Adobe Stock] licencia y guardado en  [!DNL Experience Manager] estarán disponibles para los equipos más amplios que accedan a la  [!DNL Experience Manager Assets] implementación, mientras que los recursos de licencia de creativos  [!DNL Adobe Stock] mediante el panel  [!DNL Creative Cloud] Bibliotecas solo estarán disponibles de forma predeterminada en su  [!DNL Creative Cloud] cuenta.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## Acerca del almacenamiento de recursos en un DAM {#about-storing-assets-in-a-dam}

Para diseñar un flujo de trabajo eficiente entre los equipos creativos y los equipos de marketing/línea de negocios (LOB) y elegir las mejores capacidades de asistencia, es importante comprender cuándo y por qué los recursos se almacenan en DAM.

### Por qué los recursos se almacenan en DAM {#why-assets-are-stored-in-dam}

El almacenamiento de recursos en DAM los hace fácilmente accesibles y asequibles. Garantiza que numerosos usuarios de toda la organización o el ecosistema puedan aprovechar los recursos, lo que incluye socios, clientes, etc.

La mayoría de las organizaciones solo almacenan recursos que son relevantes para los procesos de marketing/LOB descendentes (publicándolos en canales como el canal web a través de [!DNL Experience Manager Sites] u otros canales servidos por Adobe Experience Cloud: Marketing Cloud, Advertising Cloud y medidos por Analytics Cloud, proporcionándolos a usuarios/socios, etc.). Además, las organizaciones almacenan activos que pueden estar sujetos a un proceso de revisión/aprobación en DAM. De esta manera, DAM almacena principalmente activos que tienen altas posibilidades de ser aprovechados y evita almacenar activos inactivos.

El almacenamiento de recursos también está sujeto a consideraciones técnicas y de utilización de recursos. DAM proporciona servicios adicionales en torno a los recursos almacenados, incluida la extracción de metadatos, el control de versiones, la generación de vistas previas/transcodificación, la administración de referencias y la adición de información de control de acceso. Estos servicios consumen tiempo y recursos de infraestructura adicionales.

A menudo, no es deseable almacenar todos los recursos y actualizaciones. Por ejemplo, si las actualizaciones de recursos específicos son de mala calidad y consumen recursos excesivos, es posible que los recursos no se almacenen en DAM.

#### Cuando los recursos se almacenan en DAM {#when-assets-are-stored-in-dam}

Los equipos creativos (y las organizaciones) no suelen estar interesados en almacenar recursos en cada etapa del ciclo de vida de los recursos. Por ejemplo, evitan almacenar recursos en los siguientes casos:

* Recursos que aún no se han finalizado o que están sujetos a experimentación.
* Recursos que no superan el ciclo de revisión del equipo creativo/interno.
* En comparación con el recurso en cuestión, el equipo tiene mejores candidatos para representar su trabajo en equipos externos.

Normalmente, las siguientes clases de activos se almacenan en DAM:

* Activos que han alcanzado un cierto vencimiento y que se consideran listos para compartirse.
* Recursos preseleccionados por el equipo creativo.
* Formatos de recurso específicos que el marketing puede utilizar o solicitar, según un contrato o acuerdo específico (por ejemplo, archivos JPG convertidos a partir de archivos RAW, TIFF/imágenes de originales PSD).

#### Cuando las actualizaciones de los recursos se almacenan en DAM {#when-updates-to-assets-are-stored-in-dam}

Como regla, solo las actualizaciones de los recursos que sean relevantes para el conjunto más amplio de usuarios de DAM deben almacenarse en DAM. Garantiza que los usuarios (funciones de marketing y similares) solo vean versiones relevantes en la cronología de recursos de DAM.

Normalmente, los cambios se relacionan con hitos importantes del ciclo vital de los recursos. Por ejemplo, el recurso listo para el marketing inicial o una actualización oficial basada en una solicitud o revisión proporcionada por el equipo creativo deben almacenarse y crearse versiones en DAM.

La actualización del equipo creativo para que la revise el equipo de marketing después de una solicitud de cambio en el recurso existente en DAM es un ejemplo de una actualización relevante. Debe almacenarse y crearse una versión en DAM para su posterior referencia o para volver a la versión anterior.

Los siguientes son ejemplos de actualizaciones que normalmente no son relevantes:

* Versiones anteriores de recursos cargados antes de que estén listos para su revisión de marketing
* Cambios creativos frecuentes en el recurso en la fase de trabajo en curso antes de que los equipos creativos y de marketing decidan que el recurso está listo

### Acceso de usuario a DAM {#user-access-to-dam}

[!DNL Assets] admite dos tipos de usuarios en función de su acceso a la  [!DNL Assets] implementación. Normalmente, los usuarios de la red empresarial (firewall) tienen acceso directo a DAM. Otros usuarios fuera de la red empresarial no tendrían acceso directo. El tipo de usuario determina qué integraciones se pueden utilizar desde el punto de vista técnico.

#### Usuarios creativos con acceso directo a DAM {#creative-users-with-direct-access-to-dam}

Normalmente, los equipos creativos internos o las agencias/profesionales creativos incorporados a la red interna tienen acceso a la implementación de DAM, incluido el inicio de sesión [!DNL Experience Manager]. [!DNL Experience Manager] y la infraestructura de red se puede configurar para permitir el acceso directo a partes externas -generalmente organizaciones de confianza como las agencias que trabajan para un cliente- para tener acceso a  [!DNL Experience Manager] través de la red, por ejemplo a través de VPN o lista de permitidos IP.

En estos casos, Adobe Asset Link o la aplicación de escritorio [!DNL Experience Manager] ayudan a proporcionar un acceso fácil a los recursos finales o aprobados y le permiten guardar en DAM recursos listos para la creación.

#### Usuarios creativos sin acceso a DAM {#creative-users-without-access-to-dam}

Las agencias externas y los trabajadores independientes sin acceso directo a la implementación de DAM pueden requerir acceso a los recursos aprobados o desean añadir sus nuevos diseños a DAM.

Utilice las siguientes estrategias para proporcionar acceso a los recursos finales/aprobados:

* Utilice la aplicación de escritorio si Asset Link no funciona.
* Utilice [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para distribuir recursos de forma segura a socios externos
* Utilice una implementación personalizada de un portal de distribución y abastecimiento basado en [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilice el control de acceso configurado en [!DNL Experience Manager] y la infraestructura de red necesaria (por ejemplo, la lista de permitidos VPN e IP) para proporcionar a las partes externas acceso a un área específica de contenido en su DAM. Pueden utilizar la [!DNL Experience Manager] interfaz de usuario web para obtener recursos y cargar contenido nuevo en su DAM.

#### Trabajo en curso en recursos de [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Como se explica en este documento, se recomienda llevar a cabo actualizaciones importantes de los recursos, a veces denominadas trabajo en curso, sin tener que cargar todas las ediciones guardadas en el archivo local en [!DNL Experience Manager] como cambios. Esto acelera el trabajo de un usuario de escritorio, limita el ancho de banda de red utilizado y mantiene la línea de tiempo de los recursos limpia y centrada en actualizaciones importantes controladas.

Adobe Asset Link ofrece una buena compatibilidad para este caso de uso:

* Cuando los usuarios con [!DNL Photoshop], [!DNL InDesign] o [!DNL Illustrator] intentan editar un archivo, ejecutan una operación de desprotección en el recurso dado
* El recurso se descarga en segundo plano, se coloca en la cuenta de Creative Cloud de los usuarios sincronizada con el disco por la aplicación de escritorio de Creative Cloud y el indicador de desprotección se activa en [!DNL Experience Manager] en el recurso para minimizar los conflictos de edición
* A partir de ahí, el usuario trabaja en un archivo que se almacena localmente en la ubicación sincronizada y puede seguir trabajando y guardando los cambios necesarios en cualquier frecuencia necesaria
* Además, como el recurso se encuentra en la cuenta de Creative Cloud, también está disponible en otros dispositivos que el usuario pueda tener (por ejemplo, se puede abrir o editar en una aplicación móvil de Creative Cloud dedicada) y se puede compartir con otros usuarios de Creative Cloud con fines de colaboración.
* Cuando el usuario creativo haya terminado con los cambios, puede ejecutar una operación de registro en ese archivo en su aplicación Creative Cloud, con un comentario opcional. El recurso correspondiente en [!DNL Experience Manager] recibe versiones y se actualiza con el nuevo binario. [!DNL Experience Manager] los usuarios como los especialistas en marketing o los usuarios de LOB tienen acceso a los principales cambios en los recursos o a hitos a través de la interfaz de usuario de la línea de tiempo de los  [!DNL Experience Manager] recursos.

[!DNL Experience Manager] la aplicación de escritorio proporciona un recurso compartido de red para los recursos abiertos en la aplicación nativa. De forma predeterminada, todos los cambios realizados localmente se cargan en [!DNL Experience Manager] automáticamente después de un rato. Con una configuración de este tipo, los ahorros frecuentes durante la fase de trabajo en curso se cargarían en [!DNL Experience Manager] y se versionarían, lo que crearía muchos desafíos de tráfico de red y escalabilidad potencial, por no mencionar versiones innecesarias en [!DNL Experience Manager].

El método recomendado aquí es usar una opción en la aplicación de escritorio [!DNL Experience Manager] para desactivar las actualizaciones automatizadas y cargar cambios en los recursos en [!DNL Experience Manager] manualmente, aprovechando la acción de cambios de carga en la interfaz de usuario del estado de los recursos de la aplicación.

#### Carga masiva a DAM {#bulk-upload-to-dam}

Puede que tenga que cargar simultáneamente un mayor número de archivos en DAM en algunos casos, por ejemplo:

* Carga de resultados de fotos o proyectos más grandes
* Carga de recursos proporcionados por agencias creativas
* Carga de recursos seleccionados de un conjunto mayor si la selección se realiza fuera de DAM

La descripción hace referencia a la carga de archivos operacionalmente (por ejemplo, cada semana o con cada sesión fotográfica), como parte normal del flujo de trabajo del usuario del escritorio. Las migraciones de recursos grandes no se tratan aquí.

Puede aprovechar las siguientes capacidades de carga:

* Para cargar carpetas grandes/jerárquicas de forma masiva, utilice la aplicación de escritorio [!DNL Experience Manager] que proporciona funcionalidad [de carga de carpetas](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem). También puede cargar estructuras de carpetas jerárquicas. [!DNL Assets] se cargan en segundo plano y, por lo tanto, no están vinculados a una sesión de explorador web
* Para cargar algunos archivos de una sola carpeta, arrástrelos directamente a la interfaz web o utilice la opción Crear de la interfaz web [!DNL Assets].
* Según los requisitos empresariales, también puede utilizar el cargador personalizado.

#### Administrar recursos digitales directamente desde el escritorio {#managing-digital-assets-directly-from-desktop}

Si utiliza Recursos compartidos de archivos de red para administrar recursos digitales, el uso del recurso compartido de red asignado por la aplicación de escritorio [!DNL Experience Manager] podría considerarse un sustituto conveniente. Al realizar la transición desde archivos compartidos de red, la interfaz web [!DNL Experience Manager] proporciona un completo conjunto de funcionalidades de administración de recursos digitales que van mucho más allá de lo posible en un recurso compartido de red (búsqueda, colecciones, metadatos, colaboración, vistas previas, etc.) y la aplicación de escritorio [!DNL Experience Manager] proporciona un práctico vínculo para conectar el repositorio DAM del lado del servidor con el trabajo en el escritorio.

Evite utilizar la aplicación de escritorio [!DNL Experience Manager] para administrar recursos directamente en el recurso compartido de red de [!DNL Assets]. Por ejemplo, evite utilizar la aplicación de escritorio [!DNL Experience Manager] para mover/copiar varios archivos. En su lugar, utilice la interfaz [!DNL Assets] para arrastrar carpetas desde Finder/Explorer al recurso compartido de red o utilice la función [!DNL Assets] Carga de carpetas.

#### Migración de recursos {#asset-migration}

Para planificar y ejecutar las migraciones de recursos desde un sistema existente a un nuevo sistema o la migración de un gran volumen de recursos almacenados en servidores, consulte la [Guía de migración](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] la aplicación de escritorio y  [!DNL Experience Manager] las  [!DNL Creative Cloud] integraciones no admiten estas migraciones. Debido a los grandes volúmenes de recursos que se van a ingerir, y a los requisitos adicionales en torno a la asignación, transformación e ingesta de metadatos, las migraciones deben manejarse con diferentes herramientas y enfoques.

>[!MORELIKETHIS]
>
>* [Vínculo de recurso de Adobe](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Prácticas recomendadas de la aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Manager Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integración de Experience Manager y Adobe Stock](aem-assets-adobe-stock.md)

