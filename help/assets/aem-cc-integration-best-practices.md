---
title: Integración con las prácticas recomendadas de Adobe Creative Cloud
description: Prácticas recomendadas para integrar [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] para optimizar los flujos de trabajo de transferencia de recursos y lograr una velocidad de contenido alta.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '3248'
ht-degree: 16%

---


# [!DNL Adobe Experience Manager] y prácticas recomendadas  [!DNL Creative Cloud] de integración  {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] es una solución de administración de recursos digitales (DAM) con la que se puede integrar  [!DNL Adobe Creative Cloud] para ayudar a los usuarios de DAM a trabajar con equipos creativos, lo que optimiza la colaboración en el proceso de creación de contenido.

[!DNL Adobe Creative Cloud] proporciona a los equipos creativos un ecosistema de soluciones y servicios para ayudarlos a crear recursos digitales. Incluye aplicaciones de escritorio y móviles, servicios en la nube como almacenamiento con sincronización de escritorio o experiencia web, así como mercados como [!DNL Adobe Stock].

Siga leyendo para saber qué integraciones elegir entre el escritorio y el DAM de nivel empresarial en función de su caso de uso y cuáles son las prácticas recomendadas asociadas para los flujos de trabajo de conexión.

>[!NOTE]
>
>[!DNL Experience Manager] el uso compartido de  [!DNL Creative Cloud] carpetas está obsoleto y ya no se trata en esta guía. Adobe recomienda utilizar funciones más nuevas como [Vínculo de recursos de Adobe](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) o [Aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html) para proporcionar al usuario creativo acceso a los recursos administrados en [!DNL Experience Manager].

## Necesidades de colaboración de creativos, especialistas en mercadotecnia y usuarios de DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superficies involucradas |
|---|---|---|
| Simplifique la experiencia para creativos en equipos de escritorio | Racionalice el acceso a los recursos desde un DAM ([!DNL Experience Manager Assets]) para los profesionales creativos o, en términos más generales, para los usuarios de escritorio que trabajen en aplicaciones nativas de creación de recursos. Necesitan una manera sencilla y directa de descubrir, utilizar (abrir), editar y guardar los cambios en [!DNL Experience Manager], así como cargar nuevos archivos. | Win o Mac Desktop; [!DNL Creative Cloud] aplicaciones |
| Proporcionar recursos listos para usar de alta calidad desde [!DNL Adobe Stock] | Los especialistas en mercadotecnia ayudan a acelerar el proceso de creación de contenido mediante la ayuda en el descubrimiento y el abastecimiento de recursos. Los profesionales creativos utilizan los recursos aprobados directamente desde sus herramientas creativas. | [!DNL Experience Manager Assets];  [!DNL Adobe Stock] mercado; campos de metadatos |
| Distribuir y compartir recursos por organizaciones | Los departamentos internos/sucursales locales y los socios, distribuidores y agencias externos utilizan los recursos aprobados compartidos por la organización principal. La organización desea compartir de forma segura y transparente los recursos creados para una reutilización más amplia. | Brand Portal, Asset Share Commons |

## Las ofertas de Adobe para soportar la necesidad de colaboración {#adobe-offerings-to-support-the-collaboration-need}

| Propuesta de valor para las personas involucradas | Oferta de Adobe | Superficies involucradas |
|---|---|---|
| Los usuarios creativos descubren recursos de [!DNL Experience Manager], los abren y utilizan, editan y cargan cambios en [!DNL Experience Manager], así como cargan nuevos archivos en [!DNL Experience Manager] sin salir de las aplicaciones [!DNL Creative Cloud]. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator], y  [!DNL Adobe InDesign]. |
| Los usuarios comerciales simplifican la apertura y el uso de recursos, la edición y carga de cambios en [!DNL Experience Manager] y la carga de nuevos archivos en [!DNL Experience Manager] desde el entorno de escritorio. Utilizan una integración genérica para abrir cualquier tipo de recurso en la aplicación de escritorio nativa, incluidos los que no son de Adobe. | [Aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] aplicación de escritorio en Win y Mac |
| Los especialistas en marketing y los usuarios comerciales descubren, previsualización, otorgan licencias y guardan y administran los [!DNL Adobe Stock] recursos desde [!DNL Experience Manager]. Los recursos con licencia y guardados proporcionan [!DNL Adobe Stock] metadatos seleccionados para una mejor administración. | [Integración de Experience Manager y Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interfaz web |

Este artículo se centra principalmente en los dos primeros aspectos de las necesidades de colaboración. La distribución y el abastecimiento de activos a escala se mencionan brevemente como un caso de uso. Para estas necesidades, considere Adobe Brand Portal o Asset Share Commons. Las soluciones alternativas, como [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), soluciones que se pueden crear en base a los componentes [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Link Share](/help/assets/link-sharing.md), utilizando [Recursos Experience Manager](/help/assets/manage-assets.md) deben revisarse en base a requerimientos específicos.

![Conexiones de Creative Cloud para Experience Manager, decida qué capacidad utilizar](assets/creative-connections-aem.png)

### Asignación de casos de uso y soluciones de Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Caso práctico    | [!DNL Adobe Asset Link] | [!DNL Experience Manager] aplicación de escritorio | Comentarios y otras soluciones |
|---|---|---|---|
| Discover: examinar carpetas DAM | Sí | [!DNL Experience Manager] Acciones de interfaz web y escritorio |  |
| Discover: acceder a las colecciones DAM | Sí | [!DNL Experience Manager] Acciones de interfaz web y escritorio |  |
| Discover: buscar recursos desde DAM | Sí | [!DNL Experience Manager] Acciones de interfaz web y escritorio |  |
| Usar - abrir recurso | Sí | Sí | [Abrir desde ](manage-assets.md#previewing-assets) interfaz web o desde Finder |
| Usar - colocar recurso de DAM en un documento | Sí: incrustación | Sí: vinculación o incrustación | [!DNL Experience Manager] la aplicación de escritorio proporciona acceso a los recursos como archivos en el sistema de archivos local. Estos vínculos en las aplicaciones nativas se representan mediante rutas locales. |
| Editar: abrir para editar | Sí: acción de cierre de compra | Sí: acción abierta (en el recurso compartido de red) | [Desproteger en ](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) AALguarda el recurso en la cuenta de almacenamiento de Creative Cloud del usuario (sincronizado por la aplicación de Creative Cloud) de forma predeterminada. |
| Editar: trabajo en curso fuera de DAM | Sí: recurso disponible en la cuenta de almacenamiento del Creative Cloud del usuario sincronizada con el escritorio. | Sí |  |
| Editar - cargar cambios | Sí: [acción de ingreso](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) con comentario opcional | Sí |  |
| Cargar: archivo único | Sí: carga el documento activo actual | Sí | [Carga mediante interfaz web](manage-assets.md#uploading-assets) |
| Cargar: varios archivos / estructuras jerárquicas de carpetas | No | Sí | [Cargar mediante ](manage-assets.md#uploading-assets) interfaz web o mediante una herramienta o una secuencia de comandos personalizada. |
| Misc: usuario e inicio de sesión | Se reconoce al usuario Creative Cloud que ha iniciado sesión en la aplicación de escritorio Creative Cloud (SSO) | [!DNL Experience Manager] usuario y credenciales | Los usuarios de ambas soluciones cuentan para la cuota de usuario [!DNL Experience Manager]. |
| Misc: red y acceso | Requiere acceso desde el escritorio del usuario a la implementación [!DNL Experience Manager] a través de la red | Requiere acceso desde el escritorio del usuario a la implementación [!DNL Experience Manager] a través de la red | [!DNL Adobe Asset Link] no comparte el entorno de proxy de red. |
| Misc - Migrar un gran número de recursos | No | No | [Guía de migración de recursos](assets-migration-guide.md) |

Para admitir casos de uso de distribución de recursos, se deben considerar otras soluciones:

* [Brand ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) Portal para un complemento SaaS configurable  [!DNL Experience Manager Assets] para publicar recursos.
* Las soluciones personalizadas se crean en base al código [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* [!DNL Experience Manager] [compartir vínculos ](/help/assets/link-sharing.md) para compartir recursos ad hoc mediante vínculos.
* [Interfaz web de Recursos Experience Manager ](/help/assets/manage-assets.md) con áreas para partes externas protegidas por la configuración de  [!DNL Experience Manager] controles de acceso y con los ajustes de configuración de red/TI necesarios, lo que permite a estos usuarios externos acceder a  [!DNL Experience Manager].

## Conceptos clave y casos de uso {#key-concepts-and-use-cases}

### Glosario de términos comunes {#glossary-of-common-terms}

* **Trabajo en curso o trabajo en curso creativo (WIP):** Fase del ciclo vital de los recursos en la que sufren varios cambios y, por lo general, no están listos para compartirse con equipos más amplios.
* **Recursos listos para la creación:** [!DNL Assets] que están listos para compartirse con un equipo más amplio o han sido seleccionados o aprobados por el equipo creativo para compartirlos con equipos de marketing o de LOB.
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

Este es un breve resumen de las optimizaciones para la integración [!DNL Experience Manager] y [!DNL Creative Cloud]. Lea el resto de este documento para obtener una comprensión detallada de estos.

* **Para usuarios creativos que trabajan con en Photoshop, InDesign o Illustrator:** Adobe Asset Link ofrece la mejor experiencia de usuario, incluida la gestión del trabajo en curso en los recursos extraídos de [!DNL Experience Manager].
* **Para simplificar el acceso a los recursos desde el escritorio para cualquier aplicación o formato de archivo genérico:** utilice la aplicación  [!DNL Experience Manager] de escritorio.
* **Comprender por qué y cuándo almacenar recursos en DAM:** Actualizaciones que se pondrán a disposición del equipo de la organización al completo.
* **Tenga en cuenta el volumen de recursos compartidos:** Si el caso de uso es la distribución de recursos, la administración y la seguridad podrían ser los aspectos más importantes. Considere utilizar herramientas creadas para hacerlo a escala, como Brand Portal.
* **Comprenda el ciclo vital de los recursos:** Conozca cómo los distintos equipos administran los recursos en su organización
* **Gestione los ahorros frecuentes de los recursos con cuidado:** Adobe Asset Link se encarga de ello con PS, AI e ID. Para otras aplicaciones, no realice tareas de trabajo en curso en carpetas asignadas o compartidas a menos que necesite todos los cambios en DAM

### Acceso a [!DNL Adobe Stock] recursos desde [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[La ](/help/assets/aem-assets-adobe-stock.md) integración de Experience Manager y Adobe Stock permite a  [!DNL Experience Manager] los usuarios buscar, previsualización, licencia y guardar recursos  [!DNL Adobe Stock] en  [!DNL Experience Manager]. Los [!DNL Stock] recursos con licencia y guardados han seleccionado [!DNL Stock] metadatos, que pueden utilizarse para buscarlos con filtros adicionales.

Algunos puntos importantes sobre esta integración:

* Cuando los recursos de existencias de Adobe se guardan en [!DNL Experience Manager], se convierten en [!DNL Assets] normales, con el binario guardado en el repositorio [!DNL Experience Manager]. Algunos metadatos relacionados con [!DNL Adobe Stock] se guardan para el recurso en [!DNL Experience Manager]; de lo contrario, el proceso de ingestión tiene el mismo aspecto que para cualquier otro archivo. Por ejemplo, si las etiquetas inteligentes están activas, las etiquetas se agregan a estos recursos al guardarlos.
* El recurso guardado en [!DNL Experience Manager] es una copia, no un vínculo de nuevo en [!DNL Adobe Stock].

**Uso de recursos guardados  [!DNL Adobe Stock] en  [!DNL Experience Manager] en[!DNL Creative Cloud]**. Esta integración es independiente de [!DNL Adobe Asset Link], pero [!DNL Adobe Asset Link] reconoce estos recursos guardados de [!DNL Stock] de esa manera y muestra metadatos adicionales y un logotipo [!DNL Adobe Stock] en estos recursos en [!DNL Adobe Asset Link] la IU de extensión [!DNL Photoshop], [!DNL Illustrator] o [!DNL InDesign]. Los archivos están disponibles para explorarlos, abrirlos, etc. porque son recursos normales cuando se guardan en [!DNL Experience Manager].
Los usuarios creativos que trabajan en aplicaciones [!DNL Creative Cloud] con la extensión [!DNL Adobe Asset Link] presente, además de tener acceso a recursos con licencia ya existente de [!DNL Adobe Stock] a [!DNL Experience Manager], también pueden utilizar el panel [!DNL Creative Cloud] Bibliotecas para buscar, previsualización y obtener licencias de [!DNL Adobe Stock] recursos.
[!DNL Assets] los equipos más amplios que acceden a la  [!DNL Adobe Stock] implementación  [!DNL Experience Manager] podrán acceder a los recursos con licencia y guardados con licencia, mientras que los recursos con licencia de creativos  [!DNL Experience Manager Assets] mediante el panel  [!DNL Adobe Stock] Bibliotecas solo los ponen a disposición de los usuarios de forma predeterminada en su  [!DNL Creative Cloud]   [!DNL Creative Cloud] cuenta.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## Acerca del almacenamiento de recursos en un DAM {#about-storing-assets-in-a-dam}

Para diseñar un flujo de trabajo eficiente entre los equipos creativos y de marketing/línea de negocios (LOB) y elegir las mejores capacidades de soporte, es importante comprender cuándo y por qué los recursos se almacenan en DAM.

### Por qué los recursos se almacenan en DAM {#why-assets-are-stored-in-dam}

El almacenamiento de recursos en DAM hace que sean fácilmente accesibles y asequibles. Garantiza que numerosos usuarios de toda la organización o el ecosistema puedan aprovechar los recursos, lo que incluye socios, clientes, etc.

La mayoría de las organizaciones decide almacenar únicamente los recursos que son relevantes para los procesos de mercadotecnia/LOB descendentes (publicarlos en canales como el canal Web a través de [!DNL Experience Manager Sites] u otros canales proporcionados por Adobe Experience Cloud - Marketing Cloud, Advertising Cloud y medidos por Analytics Cloud, lo que proporciona a usuarios/socios, etc.). Además, las organizaciones almacenan activos que pueden estar sujetos a un proceso de revisión/aprobación en DAM. De este modo, DAM almacena principalmente activos que tienen altas posibilidades de aprovechar y evita almacenar activos inactivos.

El almacenamiento de recursos también está sujeto a consideraciones técnicas y de utilización de los recursos. DAM proporciona servicios adicionales en torno a los recursos almacenados, como la extracción de metadatos, el control de versiones, la generación de previsualizaciones/transcodificación, la administración de referencias y la adición de información de control de acceso. Estos servicios consumen más tiempo y recursos de infraestructura.

A menudo, no es deseable almacenar todos los recursos y las actualizaciones. Por ejemplo, si las actualizaciones de recursos específicos son de mala calidad y consumen recursos excesivos, es posible que los recursos no se almacenen en DAM.

#### Cuando los recursos se almacenan en DAM {#when-assets-are-stored-in-dam}

Los equipos creativos (y las organizaciones) no suelen estar interesados en almacenar recursos en cada etapa del ciclo vital de los recursos. Por ejemplo, evitan almacenar recursos en los siguientes casos:

* Recursos que aún no se han finalizado o que están sujetos a experimentación.
* Recursos que no superan el ciclo de revisión de equipo creativo/interno.
* En comparación con el activo en cuestión, el equipo tiene mejores candidatos para representar su trabajo en equipos externos.

Normalmente, los siguientes recursos de clases se almacenan en DAM:

* Activos que alcanzaron un cierto vencimiento y se consideran listos para compartirse.
* Recursos preseleccionados por el equipo creativo.
* Formatos de recurso específicos que se pueden utilizar o se solicitan mediante marketing, según un contrato o acuerdo específico (por ejemplo, archivos JPG convertidos a partir de archivos RAW, TIFF/imágenes de originales PSD).

#### Cuando las actualizaciones de los recursos se almacenan en DAM {#when-updates-to-assets-are-stored-in-dam}

Como regla general, solo las actualizaciones de los recursos que son relevantes para el conjunto más amplio de usuarios de DAM deben almacenarse en DAM. Garantiza que los usuarios (funciones de marketing y similares) solo vean versiones relevantes en la línea de tiempo de recursos de DAM.

Generalmente, los cambios se relacionan con hitos principales en el ciclo de vida de los recursos. Por ejemplo, el recurso listo para la comercialización inicial o una actualización oficial basada en una solicitud o revisión proporcionada por el equipo creativo deben almacenarse y crearse versiones en DAM.

La actualización del equipo creativo para su revisión por parte del equipo de marketing tras una solicitud de cambio en el recurso existente en DAM es un ejemplo de una actualización relevante. Debe almacenarse y crearse una versión en DAM para consulta adicional o para volver a la versión anterior.

Los siguientes son ejemplos de actualizaciones que normalmente no son relevantes:

* Versiones iniciales de los recursos cargados antes de que estén listos para la revisión de marketing
* Cambios creativos frecuentes en el recurso en la fase de trabajo en curso antes de que los equipos creativos y de marketing decidan que el recurso está listo

### Acceso del usuario a DAM {#user-access-to-dam}

[!DNL Assets] admite dos tipos de usuarios en función de su acceso a la  [!DNL Assets] implementación. Normalmente, los usuarios dentro de la red empresarial (servidor de seguridad) tienen acceso directo a DAM. Otros usuarios fuera de la red empresarial no tendrían acceso directo. El tipo de usuario determina qué integraciones se pueden utilizar desde el punto de vista técnico.

#### Usuarios creativos con acceso directo a DAM {#creative-users-with-direct-access-to-dam}

Generalmente, los equipos creativos internos o las agencias o los profesionales creativos integrados en la red interna tienen acceso a la implementación de DAM, incluido el inicio de sesión [!DNL Experience Manager]. [!DNL Experience Manager] y la infraestructura de red se puede configurar para permitir el acceso directo a las partes externas -generalmente organizaciones de confianza como las agencias que trabajan para un cliente- para tener acceso a  [!DNL Experience Manager] través de la red, por ejemplo a través de VPN o lista de permitidos IP.

En estos casos, el vínculo de recursos de Adobe o la aplicación de escritorio [!DNL Experience Manager] ayudan a facilitar el acceso a los recursos finales o aprobados y permiten guardar en DAM los recursos listos para la creación.

#### Usuarios creativos sin acceso a DAM {#creative-users-without-access-to-dam}

Es posible que las agencias externas y los autónomos que no tienen acceso directo a la implementación de DAM necesiten acceder a los recursos aprobados o deseen agregar sus nuevos diseños al DAM.

Utilice las siguientes estrategias para proporcionar acceso a los activos finales o aprobados:

* Utilice la aplicación de escritorio si Asset Link no funciona.
* Utilice [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para distribuir los recursos de forma segura a socios externos
* Utilice una implementación personalizada de un portal de distribución y abastecimiento basado en [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilice Control de acceso configurado en [!DNL Experience Manager] e infraestructura de red necesaria (por ejemplo, lista de permitidos de VPN e IP) para proporcionar a las partes externas acceso a un área dedicada de contenido en su DAM. Pueden utilizar [!DNL Experience Manager] interfaz de usuario web para obtener recursos y cargar contenido nuevo en su DAM.

#### Trabajo en curso sobre los activos de [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Como se explica en este documento, se recomienda llevar a cabo actualizaciones importantes de los recursos, a veces denominadas trabajo en curso, sin tener que cargar todas las ediciones guardadas en el archivo local a [!DNL Experience Manager] como cambios. Esto acelera el trabajo de un usuario de escritorio, limita el ancho de banda de red utilizado y mantiene la línea de tiempo de los recursos limpia y centrada en actualizaciones importantes y controladas.

Adobe Asset Link oferta una buena compatibilidad para este caso de uso:

* Cuando los usuarios con [!DNL Photoshop], [!DNL InDesign] o [!DNL Illustrator] intención de editar un archivo, ejecutan una operación de desprotección en el recurso dado
* El recurso se descarga en segundo plano, se coloca en la cuenta de Creative Cloud del usuario sincronizada con el disco por la aplicación de escritorio de Creative Cloud y el indicador de cierre de compra se activa [!DNL Experience Manager] en el recurso para minimizar los conflictos de edición
* A partir de ahí, el usuario trabaja en un archivo almacenado localmente en la ubicación sincronizada y puede seguir trabajando y guardando los cambios necesarios con cualquier frecuencia necesaria
* Además, como el recurso está en la cuenta de Creative Cloud, también está disponible en otros dispositivos que el usuario pueda tener (por ejemplo, puede abrirse o editarse en una aplicación móvil de Creative Cloud dedicada) y puede compartirse con otros usuarios de Creative Cloud con fines de colaboración.
* Cuando el usuario creativo ha terminado con los cambios, puede ejecutar una operación de protección en ese archivo en la aplicación Creative Cloud, con un comentario opcional. El recurso correspondiente de [!DNL Experience Manager] se versiona y se actualiza con el nuevo binario. [!DNL Experience Manager] los usuarios como los especialistas en marketing o los usuarios de LOB tienen acceso a los principales cambios de recursos o hitos mediante la interfaz de usuario de la línea de tiempo de  [!DNL Experience Manager] recursos.

[!DNL Experience Manager] la aplicación de escritorio proporciona un recurso compartido de red para los recursos abiertos en la aplicación nativa. De forma predeterminada, todos los cambios realizados localmente se cargan en [!DNL Experience Manager] automáticamente después de un breve tiempo. Con una configuración de este tipo, los ahorros frecuentes durante la fase de trabajo en curso se cargarían en [!DNL Experience Manager] y se versionarían, creando mucho tráfico de red y potenciales desafíos de escalabilidad, sin mencionar las versiones innecesarias en [!DNL Experience Manager].

El método recomendado aquí es utilizar una opción en la aplicación de escritorio [!DNL Experience Manager] para desactivar las actualizaciones automatizadas y cargar cambios en los recursos en [!DNL Experience Manager] manualmente, aprovechando la acción de cambios de carga en la interfaz de usuario de estado de recursos de la aplicación.

#### Carga masiva a DAM {#bulk-upload-to-dam}

Es posible que tenga que cargar simultáneamente un número mayor de archivos en DAM en algunos casos, por ejemplo:

* Carga de resultados de fotografías o proyectos más grandes
* Carga de recursos proporcionados por agencias creativas
* Carga de recursos seleccionados de un conjunto más grande si la selección se realiza fuera de DAM

La descripción se refiere a la carga de archivos operacionalmente (por ejemplo, cada semana o con cada sesión fotográfica), como parte normal del flujo de trabajo del usuario del escritorio. Las migraciones de recursos grandes no se cubren aquí.

Puede aprovechar las siguientes funciones de carga:

* Para cargar carpetas grandes o jerárquicas de forma masiva, utilice la aplicación de escritorio [!DNL Experience Manager] que proporciona la funcionalidad [de carga de carpetas](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem). También puede cargar estructuras de carpetas jerárquicas. [!DNL Assets] se cargan en segundo plano y, por lo tanto, no están vinculadas a una sesión de explorador Web
* Para cargar algunos archivos desde una sola carpeta, arrástrelos directamente a la interfaz web o utilice la opción Crear de la interfaz web [!DNL Assets].
* En función de los requisitos comerciales, también puede utilizar el cargador personalizado.

#### Administrar recursos digitales directamente desde el escritorio {#managing-digital-assets-directly-from-desktop}

Si utiliza Compartidos de archivos de red para administrar recursos digitales, el uso del recurso compartido de red asignado por la aplicación de escritorio [!DNL Experience Manager] podría considerarse un sustituto conveniente. Al realizar la transición desde los recursos compartidos de archivos de red, la [!DNL Experience Manager] interfaz web proporciona un completo conjunto de funciones de administración de activos digitales que van mucho más allá de lo posible en un recurso compartido de red (búsqueda, colecciones, metadatos, colaboración, previsualizaciones, etc.) y la aplicación de escritorio [!DNL Experience Manager] proporciona un vínculo práctico para conectar el repositorio DAM del lado del servidor con el trabajo en el escritorio.

Evite utilizar la aplicación de escritorio [!DNL Experience Manager] para administrar los recursos directamente en el recurso compartido de red de [!DNL Assets]. Por ejemplo, evite utilizar la aplicación de escritorio [!DNL Experience Manager] para mover o copiar varios archivos. En su lugar, utilice la interfaz [!DNL Assets] para arrastrar carpetas desde Finder/Explorer al recurso compartido de red o utilice la función [!DNL Assets] Carga de carpetas.

#### Migración de recursos {#asset-migration}

Para planificar y ejecutar migraciones de recursos desde un sistema existente a un nuevo sistema o migración de grandes volúmenes de recursos almacenados en servidores, consulte la [Guía de migración](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] la aplicación de escritorio y  [!DNL Experience Manager] las  [!DNL Creative Cloud] integraciones no admiten estas migraciones. Debido a los grandes volúmenes de recursos que se van a ingerir y a los requisitos adicionales en cuanto a la asignación, transformación e ingesta de metadatos, las migraciones deben gestionarse con diferentes herramientas y enfoques.

>[!MORELIKETHIS]
>
>* [Vínculo de recurso de Adobe](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Prácticas recomendadas de la aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Manager Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integración de Experience Manager y Adobe Stock](aem-assets-adobe-stock.md)

