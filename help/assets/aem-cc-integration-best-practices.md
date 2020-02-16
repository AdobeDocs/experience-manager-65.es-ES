---
title: Prácticas recomendadas para la integración de AEM y Creative Cloud
description: Prácticas recomendadas para integrar AEM con Adobe Creative Cloud para optimizar los flujos de trabajo de transferencia de recursos y lograr la máxima eficacia.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Prácticas recomendadas para la integración de AEM y Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

<!-- TBD: Reconcile with 6.4 article that's behind this article in terms of content streamlining and structuring.
-->

Recursos Adobe Experience Manager es una solución de administración de recursos digitales (DAM) que se puede integrar con Adobe Creative Cloud para ayudar a los usuarios de DAM a trabajar con equipos creativos, lo que optimiza la colaboración en el proceso de creación de contenido.

Adobe Creative Cloud ofrece a los equipos creativos un ecosistema de soluciones y servicios que les ayudan a crear recursos digitales. Incluye aplicaciones de escritorio y móviles, servicios en la nube como almacenamiento con sincronización de escritorio o experiencia web, así como mercados como Adobe Stock.

Siga leyendo para saber qué integraciones elegir entre el escritorio y el DAM de nivel empresarial según el caso de uso y cuáles son las prácticas recomendadas asociadas para los flujos de trabajo de conexión.

>[!NOTE]
>
>El uso compartido de carpetas de AEM a Creative Cloud ya no se incluye en esta guía. Adobe recomienda utilizar funciones más nuevas como [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) o la aplicación [de escritorio](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html) AEM para proporcionar al usuario creativo acceso a los recursos gestionados en AEM.

## Necesidades de colaboración de creativos, especialistas en mercadotecnia y usuarios de DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superficies involucradas |
|---|---|---|
| Simplifique la experiencia para creativos en equipos de escritorio | Racionalice el acceso a los recursos desde un DAM (Recursos AEM) para los profesionales creativos o, en términos más generales, para los usuarios de escritorio que trabajen en aplicaciones nativas de creación de recursos. Necesitan una forma sencilla y sencilla de descubrir, utilizar (abrir), editar y guardar cambios en AEM, así como cargar nuevos archivos. | Win o Mac Desktop; Aplicaciones de Creative Cloud |
| Proporcionar recursos listos para usar de alta calidad de Adobe Stock | Los especialistas en mercadotecnia ayudan a acelerar el proceso de creación de contenido mediante la ayuda en el descubrimiento y el abastecimiento de recursos. Los profesionales creativos utilizan los recursos aprobados directamente desde sus herramientas creativas. | Recursos AEM; Adobe Stock Marketplace; campos de metadatos |
| Distribuir y compartir recursos por organizaciones | Los departamentos internos/sucursales locales y los socios, distribuidores y agencias externos utilizan los recursos aprobados compartidos por la organización principal. La organización desea compartir de forma segura y transparente los recursos creados para una reutilización más amplia. | Brand Portal, Asset Share Commons |

## Ofertas de Adobe para satisfacer las necesidades de colaboración {#adobe-offerings-to-support-the-collaboration-need}

| Propuesta de valor para las personas involucradas | Oferta de Adobe | Superficies involucradas |
|---|---|---|
| Los usuarios creativos descubren recursos de AEM, los abren y utilizan, editan y cargan cambios en AEM, así como cargan nuevos archivos en AEM sin salir de las aplicaciones de Creative Cloud. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator e InDesign |
| Los usuarios empresariales simplifican la apertura y el uso de recursos, la edición y carga de cambios en AEM y la carga de nuevos archivos en AEM desde el entorno de escritorio. Utilizan una integración genérica para abrir cualquier tipo de recurso en la aplicación de escritorio nativa, incluidos los que no son de Adobe. | [Aplicación de escritorio de AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | Aplicación de escritorio AEM en Windows y Mac |
| Los especialistas en marketing y los usuarios empresariales descubren, previsualizan, otorgan licencias y guardan y gestionan los recursos de Adobe Stock desde AEM. Los recursos con licencia y guardados proporcionan metadatos seleccionados de Adobe Stock para mejorar la gestión. | [Integración de Experience Manager y Adobe Stock](aem-assets-adobe-stock.md) | Interfaz web de AEM |

Este artículo se centra principalmente en los dos primeros aspectos de las necesidades de colaboración. La distribución y el abastecimiento de activos a escala se mencionan brevemente como un caso de uso. Para estas necesidades, considere Adobe Brand Portal o Asset Share Commons. Las soluciones alternativas como [Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html), las soluciones que se pueden crear en función de los componentes de [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) , [Link Share](/help/assets/link-sharing.md), mediante [Experience Manager Assets](/help/assets/managing-assets-touch-ui.md) deben revisarse en función de requisitos específicos.

![Conexiones de Creative Cloud para AEM: Decidir qué capacidad utilizar](assets/creative-connections-aem.png)

### Asignación de casos de uso y soluciones de Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso de uso | Adobe Asset Link | Aplicación de escritorio de AEM | Comentarios y otras soluciones |
|---|---|---|---|
| Discover: examinar carpetas de AEM | Sí | Interfaz de usuario web de AEM + acciones de escritorio | Al explorar el recurso compartido de red, desactive las miniaturas para evitar la descarga de archivos binarios de recursos. |
| Discover: acceso a las colecciones de AEM | Sí | Interfaz de usuario web de AEM + acciones de escritorio |  |
| Discover: buscar recursos desde AEM | Sí | Interfaz de usuario web de AEM + acciones de escritorio |  |
| Usar - abrir recurso | Sí | Sí - para cualquier aplicación | [Abrir desde interfaz](managing-assets-touch-ui.md#previewing-assets) web o desde Finder |
| Uso: colocar recursos de AEM en un documento | Sí: incrustación | Sí: vinculación o incrustación | La aplicación de escritorio AEM permite acceder a los recursos como archivos en el sistema de archivos local. Estos vínculos en las aplicaciones nativas se representan mediante rutas locales. |
| Editar: abrir para editar | Sí: acción de cierre de compra | Sí: acción abierta (en el recurso compartido de red) | [La desprotección en AAL](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) guarda el recurso en la cuenta de almacenamiento en la nube creativa del usuario (sincronizada por la aplicación de Creative Cloud) de forma predeterminada. |
| Editar: trabajo en curso fuera de AEM | Sí: recurso disponible en la cuenta de almacenamiento de Creative Cloud del usuario sincronizada con el escritorio. | Sí |  |
| Editar - cargar cambios | Sí: acción [de](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) ingreso con comentario opcional | Sí |  |
| Cargar: archivo único | Sí: carga el documento activo actual | Sí | [Carga mediante interfaz web](managing-assets-touch-ui.md#uploading-assets) |
| Cargar: varios archivos / estructuras de carpetas jerárquicas | No | Sí | [Cargar mediante interfaz](managing-assets-touch-ui.md#uploading-assets)web;Herramienta o secuencias de comandos<br>personalizadas |
| Misc: usuario e inicio de sesión | Reconocimiento del usuario de Creative Cloud que ha iniciado sesión en la aplicación de escritorio de Creative Cloud (SSO) | Usuario/inicio de sesión de AEM | Los usuarios de ambas soluciones cuentan con la cuota de usuario de AEM. |
| Misc: red y acceso | Requiere acceso desde el escritorio del usuario a la implementación de AEM a través de la red | Requiere acceso desde el escritorio del usuario a la implementación de AEM a través de la red | Adobe Asset Link no comparte el entorno proxy de red. |
| Misc - Migrar un gran número de recursos | No | No | [Guía de migración](assets-migration-guide.md) |

Para admitir casos de uso de distribución de recursos, se deben considerar otras soluciones:

* [Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) para un complemento SaaS configurable en Recursos AEM para publicar recursos.
* Las soluciones personalizadas se crean en función de la base de código de [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) .
* Uso compartido [de](/help/assets/link-sharing.md) vínculos de AEM para compartir recursos ad hoc mediante vínculos.
* [Interfaz](/help/assets/managing-assets-touch-ui.md) web de AEM Assets con áreas para terceros externos protegidas por la configuración de AEM Access Control y con los ajustes de configuración de red/TI necesarios, lo que proporciona a estos usuarios externos acceso a AEM.

## Conceptos clave y casos de uso {#key-concepts-and-use-cases}

### Glosario de términos comunes {#glossary-of-common-terms}

* **** Trabajo en curso o trabajo en curso creativo (WIP): Fase del ciclo vital de los recursos en la que los recursos sufren varios cambios y, por lo general, no están listos para compartirse con equipos más amplios.
* **** Recursos listos para el creativo: Recursos que están listos para compartirse con un equipo más amplio o que han sido seleccionados o aprobados por el equipo creativo para compartirlos con equipos de marketing o de LOB.
* **** Aprobaciones de recursos: Proceso de aprobación que se ejecuta para los recursos ya cargados en DAM, que generalmente incluye aprobaciones de marca, aprobaciones legales, etc.
* **** Activo final: Recurso que ha pasado por todas las aprobaciones/etiquetado de metadatos y está listo para ser utilizado por el equipo más amplio. Este recurso se almacena en DAM y se pone a disposición de todos los usuarios (o de todos los interesados). Se puede utilizar en canales de marketing o en equipos creativos para crear diseños.
* **** Cambio o actualización menor de recursos: Un cambio rápido y pequeño en un recurso digital. A menudo se realiza como respuesta a una solicitud de edición, revisión o aprobación de recursos (por ejemplo, cambiar la posición, el tamaño del texto, ajustar la saturación/brillo, el color, etc.).
* **** Cambio o actualización de recursos principales: Un cambio en un activo digital que requiere un trabajo considerable y que a veces debe hacerse durante un período de tiempo más largo. Generalmente incluye varios cambios. El recurso debe guardarse varias veces mientras se actualiza. Las principales actualizaciones de recursos suelen hacer que el recurso entre en una etapa de trabajo en curso.
* **** DAM: Administración de recursos digitales. En este documento, es sinónimo de Recursos AEM Experience Manager, a menos que se mencione específicamente lo contrario.
* **** Usuario creativo: Un profesional creativo que crea recursos digitales mediante las aplicaciones y los servicios de Creative Cloud. En algunos casos, un usuario creativo puede ser miembro de un equipo creativo que puede utilizar Creative Cloud, pero no crea recursos digitales (como un director creativo o un administrador de equipo creativo).
* **** Usuario DAM: Usuario típico de un sistema DAM. Según la organización, un usuario de DAM puede ser un usuario de marketing o no de marketing, por ejemplo un usuario de línea de negocios (LOB), bibliotecario, vendedor, etc.

### Consideraciones al utilizar la integración de AEM y Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

* Consulte las prácticas recomendadas de la aplicación [de escritorio](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* Consulte Integración de [Adobe Stock](aem-assets-adobe-stock.md)
* Consulte [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Este es un breve resumen de las prácticas recomendadas para Experience Manager y la integración de Creative Cloud. Lea el resto de este documento para obtener una comprensión detallada de ellos.

* **** Para usuarios creativos, trabajar en Photoshop, InDesign o Illustrator: Adobe Asset Link ofrece la mejor experiencia de usuario, incluida la gestión limpia del trabajo en curso en los recursos extraídos de AEM
* **** Para simplificar el acceso a los recursos desde el escritorio para cualquier aplicación o formato de archivo genérico: usar la aplicación de escritorio AEM
* **** Comprender por qué y cuándo almacenar recursos en DAM: Actualizaciones que se pondrán a disposición del equipo más amplio de la organización
* **** Tenga en cuenta el volumen de recursos compartidos: Si el caso de uso es la distribución de recursos, la gobernanza y la seguridad podrían ser los aspectos más importantes. Considere utilizar herramientas creadas para hacerlo a escala, como Brand Portal.
* **** Comprenda el ciclo vital de los recursos: Conozca cómo los distintos equipos administran los recursos en su organización
* **** Gestione los ahorros frecuentes en los recursos con cuidado: Adobe Asset Link se encarga de ello con PS, AI e ID. Para otras aplicaciones, no realice tareas de trabajo en curso en carpetas asignadas o compartidas a menos que necesite todos los cambios en DAM

### Acceso a recursos de Adobe Stock desde Recursos AEM {#access-to-adobe-stock-assets-from-aem-assets}

[La integración](/help/assets/aem-assets-adobe-stock.md) de AEM y Adobe Stock permite a los usuarios de AEM buscar, obtener una vista previa, obtener licencias y guardar recursos de Adobe Stock en AEM. Los recursos con licencia y guardados de Adobe Stock han seleccionado metadatos de almacenamiento, que pueden utilizarse para buscarlos con filtros adicionales.

Algunos puntos importantes sobre esta integración:

* Cuando los recursos de las existencias de Adobe se guardan en AEM, se convierten en AEM Assets normales, con el binario guardado en el repositorio de AEM. Algunos metadatos relacionados con Adobe Stock se guardan para el recurso en AEM; de lo contrario, el proceso de inserción tiene el mismo aspecto que para cualquier otro archivo. Por ejemplo, si las etiquetas inteligentes están activas, las etiquetas se agregan a estos recursos al guardarlos.
* El recurso guardado en AEM es una copia, no un vínculo de vuelta a Adobe Stock.

**Trabajar con recursos guardados de Adobe Stock en AEM en Creative Cloud**. Esta integración es independiente de Adobe Asset Link, pero Adobe Asset Link reconoce estos recursos guardados de Stock de esa manera y muestra metadatos adicionales y un icono de Stock en estos recursos en la interfaz de usuario de la extensión Adobe Asset Link en Photoshop, Illustrator o InDesign. Los archivos están disponibles para su exploración, apertura, etc., ya que son recursos de AEM habituales cuando se guardan en AEM.
Los usuarios de Creative Cloud que trabajen en aplicaciones de Creative Cloud con la extensión Adobe Asset Link presente, además de tener acceso a recursos con licencia de Adobe Stock en AEM, también pueden utilizar el panel Bibliotecas de Creative Cloud para buscar, obtener una vista previa y obtener una licencia para los recursos de Adobe Stock.
Los recursos de Adobe Stock con licencia y guardados en AEM están disponibles para los equipos más amplios que acceden a la implementación de AEM Assets, mientras que los recursos de licencias de creativos de Adobe Stock a través del panel de bibliotecas de Creative Cloud solo están disponibles de forma predeterminada en su cuenta de Creative Cloud.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## Acerca del almacenamiento de recursos en un DAM {#about-storing-assets-in-a-dam}

Para diseñar un flujo de trabajo eficiente entre los equipos creativos y de marketing/línea de negocios (LOB) y elegir las mejores capacidades de soporte, es importante comprender cuándo y por qué los recursos se almacenan en DAM.

### Por qué los recursos se almacenan en DAM {#why-assets-are-stored-in-dam}

El almacenamiento de recursos en DAM hace que sean fácilmente accesibles y asequibles. Garantiza que numerosos usuarios de toda la organización o el ecosistema puedan aprovechar los recursos, lo que incluye socios, clientes, etc.

La mayoría de las organizaciones solo almacenan recursos que son relevantes para los procesos de marketing/LOB descendentes (publicándolos en canales como el canal web a través de AEM Sites u otros canales ofrecidos por Adobe Experience Cloud: Marketing Cloud, Advertising Cloud y medidos por Analytics Cloud, lo que proporciona a usuarios/socios, etc.). Además, las organizaciones almacenan activos que pueden estar sujetos a un proceso de revisión/aprobación en DAM. De este modo, DAM almacena principalmente activos que tienen altas posibilidades de aprovechar y evita almacenar activos inactivos.

El almacenamiento de recursos también está sujeto a consideraciones técnicas y de utilización de los recursos. DAM proporciona servicios adicionales en torno a los recursos almacenados, como la extracción de metadatos, el control de versiones, la generación de vistas previas/transcodificación, la administración de referencias y la adición de información de control de acceso. Estos servicios consumen más tiempo y recursos de infraestructura.

A menudo, no es deseable almacenar todos los recursos y las actualizaciones. Por ejemplo, si las actualizaciones de recursos específicos son de mala calidad y consumen recursos excesivos, es posible que los recursos no se almacenen en DAM.

#### Cuando los recursos se almacenan en DAM {#when-assets-are-stored-in-dam}

Los equipos creativos (y las organizaciones) no suelen estar interesados en almacenar recursos en cada etapa del ciclo vital de los recursos. Por ejemplo, evitan almacenar recursos en los siguientes casos:

* Recursos que aún no se han finalizado o que están sujetos a experimentación
* Recursos que no superan el ciclo de revisión creativo/interno del equipo
* En comparación con el activo en cuestión, el equipo tiene mejores candidatos para representar su trabajo en equipos externos

Normalmente, los siguientes recursos de clases se almacenan en DAM:

* Activos que alcanzaron un cierto vencimiento y se consideran listos para compartirse
* Recursos preseleccionados por el equipo creativo
* Formatos de recurso específicos que se pueden utilizar o se solicitan en la mercadotecnia, según un contrato o acuerdo específico (por ejemplo, archivos JPG convertidos a partir de archivos RAW, TIFF/imágenes de originales PSD)

#### Cuando las actualizaciones de los recursos se almacenan en DAM {#when-updates-to-assets-are-stored-in-dam}

Como regla general, solo las actualizaciones de los recursos que son relevantes para el conjunto más amplio de usuarios de DAM deben almacenarse en DAM. Garantiza que los usuarios (funciones de marketing y similares) solo vean versiones relevantes en la línea de tiempo de recursos de DAM.

Generalmente, los cambios se relacionan con hitos principales en el ciclo de vida de los recursos. Por ejemplo, el recurso listo para la comercialización inicial o una actualización oficial basada en una solicitud o revisión proporcionada por el equipo creativo deben almacenarse y crearse versiones en DAM.

La actualización del equipo creativo para su revisión por parte del equipo de marketing tras una solicitud de cambio en el recurso existente en DAM es un ejemplo de una actualización relevante. Debe almacenarse y crearse una versión en DAM para consulta adicional o para volver a la versión anterior.

Los siguientes son ejemplos de actualizaciones que normalmente no son relevantes:

* Versiones iniciales de los recursos cargados antes de que estén listos para la revisión de marketing
* Cambios creativos frecuentes en el recurso en la fase de trabajo en curso antes de que los equipos creativos y de marketing decidan que el recurso está listo

### Acceso del usuario a DAM {#user-access-to-dam}

Recursos AEM admite dos tipos de usuarios en función de su acceso a la implementación de Recursos AEM. Normalmente, los usuarios dentro de la red empresarial (servidor de seguridad) tienen acceso directo a DAM. Otros usuarios fuera de la red empresarial no tendrían acceso directo. El tipo de usuario determina qué integraciones se pueden utilizar desde el punto de vista técnico.

#### Usuarios creativos con acceso directo a DAM {#creative-users-with-direct-access-to-dam}

Normalmente, los equipos creativos internos o las agencias o los profesionales creativos integrados en la red interna tienen acceso a la instancia de DAM, incluido el inicio de sesión de AEM. La infraestructura de red y AEM se puede configurar para permitir el acceso directo a partes externas (generalmente organizaciones de confianza como las agencias que trabajan para un cliente) para tener acceso a AEM a través de la red (por ejemplo, a través de una lista blanca de VPN o IP).

En estos casos, Adobe Asset Link o la aplicación de escritorio de AEM ayudan a facilitar el acceso a los recursos finales o aprobados y permiten guardar en DAM los recursos listos para la creación.

#### Usuarios creativos sin acceso a DAM {#creative-users-without-access-to-dam}

Es posible que las agencias externas y los autónomos que no tienen acceso directo a la instancia de DAM necesiten acceder a los recursos aprobados o deseen añadir sus nuevos diseños al DAM.

Utilice las siguientes estrategias para proporcionar acceso a los activos finales o aprobados:

* Utilice la aplicación de escritorio si Asset Link no funciona.
* Utilice [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) para distribuir recursos de forma segura a socios externos
* Utilice una implementación personalizada de un portal de distribución y abastecimiento basado en [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilice el control de acceso configurado en AEM y la infraestructura de red necesaria (por ejemplo, la lista blanca de VPN e IP) para proporcionar a las partes externas acceso a un área dedicada de contenido en su DAM. Pueden utilizar la interfaz de usuario web de AEM para obtener recursos y cargar contenido nuevo en su DAM.

#### Trabajo en curso sobre los recursos de AEM {#work-in-progress-on-assets-from-aem}

Como se explica en este documento, se recomienda llevar a cabo actualizaciones importantes de los recursos, a veces denominadas trabajo en curso, sin que todas las ediciones guardadas en el archivo local se carguen también en AEM como cambios. Esto acelera el trabajo de un usuario de escritorio, limita el ancho de banda de red utilizado y mantiene la línea de tiempo de los recursos limpia y centrada en actualizaciones importantes y controladas.

Adobe Asset Link ofrece una buena compatibilidad para este caso de uso:

* Cuando los usuarios de Photoshop, InDesign o Illustrator intentan editar un archivo, ejecutan una operación de desprotección en el recurso determinado
* El recurso se descarga en segundo plano, se coloca en la cuenta de Creative Cloud de los usuarios sincronizada con el disco mediante la aplicación de escritorio de Creative Cloud y el indicador de cierre de compra se activa en AEM en el recurso para minimizar los conflictos de edición
* A partir de ahí, el usuario trabaja en un archivo almacenado localmente en la ubicación sincronizada y puede seguir trabajando y guardando los cambios necesarios con cualquier frecuencia necesaria
* Además, como el recurso está en la cuenta de Creative Cloud, también está disponible en otros dispositivos que el usuario pueda tener (por ejemplo, se puede abrir o editar en una aplicación móvil dedicada de Creative Cloud) y se puede compartir con otros usuarios de Creative Cloud con fines de colaboración.
* Cuando el usuario creativo haya terminado con los cambios, podrá ejecutar una operación de registro en ese archivo en la aplicación de Creative Cloud, con un comentario opcional. El recurso correspondiente en AEM se crea en versión y se actualiza con el nuevo binario. Los usuarios de AEM, como los especialistas en marketing o los usuarios de LOB, tienen acceso a los principales cambios de recursos o hitos a través de la interfaz de usuario de la línea de tiempo de recursos de AEM.

La aplicación de escritorio AEM ofrece un recurso compartido de red para los recursos abiertos en la aplicación nativa. De forma predeterminada, todos los cambios realizados localmente se cargan en AEM automáticamente después de un breve tiempo. Con una configuración de este tipo, los ahorros frecuentes durante la fase de trabajo en curso se cargarían en AEM y se versionarían, lo que crearía muchos problemas de tráfico de red y de escalabilidad potencial, por no hablar de versiones innecesarias en AEM.

El método recomendado aquí es utilizar una opción en la aplicación de escritorio de AEM para desactivar las actualizaciones automatizadas y cargar cambios en los recursos en AEM manualmente, aprovechando la acción de cambios de carga en la interfaz de usuario de estado de recursos de la aplicación.

#### Carga masiva a DAM {#bulk-upload-to-dam}

Es posible que tenga que cargar simultáneamente un número mayor de archivos en DAM en algunos casos, por ejemplo:

* Carga de resultados de fotografías o proyectos más grandes
* Carga de recursos proporcionados por agencias creativas
* Carga de recursos seleccionados de un conjunto más grande si la selección se realiza fuera de DAM

La descripción se refiere a la carga de archivos operacionalmente (por ejemplo, cada semana o con cada sesión fotográfica), como parte normal del flujo de trabajo del usuario del escritorio. Las migraciones de recursos grandes no se cubren aquí.

Puede aprovechar las siguientes funciones de carga:

* Para cargar carpetas grandes o jerárquicas de forma masiva, utilice la aplicación de escritorio de AEM que ofrece funciones de carga [de](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) carpetas. También puede cargar estructuras de carpetas jerárquicas. Los recursos se cargan en segundo plano y, por lo tanto, no están vinculados a una sesión de explorador Web
* Para cargar algunos archivos desde una sola carpeta, arrástrelos directamente a la interfaz web o utilice la opción Crear de la interfaz web de Recursos AEM.
* En función de los requisitos comerciales, también puede utilizar el cargador personalizado.

#### Administrar recursos digitales directamente desde el escritorio {#managing-digital-assets-directly-from-desktop}

Si utiliza Compartidos de archivos de red para administrar recursos digitales, el uso del recurso compartido de red asignado por la aplicación de escritorio de AEM podría considerarse un sustituto conveniente. Al realizar la transición desde los recursos compartidos de archivos de red, la interfaz web de AEM proporciona un completo conjunto de funciones de administración de recursos digitales que van mucho más allá de lo posible en un recurso compartido de red (búsqueda, colecciones, metadatos, colaboración, vistas previas, etc.), y la aplicación de escritorio de AEM proporciona un vínculo práctico para conectar el repositorio DAM del lado del servidor con el trabajo en el escritorio.

Evite utilizar la aplicación de escritorio de AEM para administrar recursos directamente en el recurso compartido de red de AEM Assets. Por ejemplo, evite utilizar la aplicación de escritorio de AEM para mover o copiar varios archivos. En su lugar, utilice la interfaz de usuario web de Recursos AEM para arrastrar carpetas de Finder/Explorer al recurso compartido de red o utilice la función de carga de carpetas de Recursos AEM.

#### Migración de recursos {#asset-migration}

Para planificar y ejecutar migraciones de recursos desde un sistema existente a un nuevo sistema o migración de grandes volúmenes de recursos almacenados en servidores, consulte la Guía [](/help/assets/assets-migration-guide.md)de migración. La aplicación de escritorio AEM y AEM para integraciones de Creative Cloud no admiten estas migraciones. Debido a los grandes volúmenes de recursos que se van a ingerir y a los requisitos adicionales en cuanto a la asignación, transformación e ingesta de metadatos, las migraciones deben gestionarse con diferentes herramientas y enfoques.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/in/enterprise/using/adobe-asset-link.html)
>* [Prácticas recomendadas de la aplicación de escritorio de AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [AEM Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integración de AEM y Adobe Stock](aem-assets-adobe-stock.md)

