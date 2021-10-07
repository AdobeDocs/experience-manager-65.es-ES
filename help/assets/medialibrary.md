---
title: Usar Media Library para la administración básica de recursos digitales
description: '[!DNL Experience Manager Assets] y Media Library para la administración de recursos.'
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
source-git-commit: 5462eb18c55a509712dab8fdbb653eb2d1889763
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Usar Media Library para la administración básica de recursos {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] platform proporciona diferentes funciones para administrar recursos. Media Library permite a los usuarios cargar un pequeño número de recursos en el repositorio, buscarlos y utilizarlos en las páginas web y realizar tareas sencillas de administración de recursos en los recursos.

Media Library es una solución ligera de administración de activos digitales (DAM) que viene con licencia [!DNL Adobe Experience Manager Sites] de cortesía. [!DNL Sites] es una oferta de administración de contenido web (WCM). Media Library funciona con todas las funcionalidades de Experience Manager.

[!DNL Adobe Experience Manager Assets] la licencia está disponible por separado para su compra. [!DNL Experience Manager Assets] permite una gestión sólida de los recursos mediante casos de uso empresariales, personalizaciones de metadatos, esquemas, búsquedas e interfaz de usuario, y muchas otras funciones además de las que proporciona Media Library.

## Requisitos de licencia {#avail-media-library-license}

Los clientes que tienen [!DNL Sites] licencia tienen derecho a utilizar Media Library. Funciona con todos los componentes de [!DNL Experience Manager].

Media Library se instala como parte de Sites. No se requiere licencia o paquete adicional más allá de la licencia e instalación de Sites.

## [!DNL Assets] versus Media Library {#assets-and-media-library}

Experience Manager Assets proporciona funcionalidad de DAM de nivel empresarial. La funcionalidad de los recursos se entrega con [!DNL Experience Manager] en un solo paquete. Sin embargo, los usuarios que no hayan adquirido una licencia de Assets no tienen derecho a utilizar las funciones avanzadas de DAM. Sin licencia de Assets, solo están disponibles [Media Library features](#use-media-library).

Si desea evitar el uso no intencionado de características [!DNL Assets] de las que no tiene licencia, elimine todos los flujos de trabajo, componentes, taxonomías, opciones específicos de [!DNL Assets] y el administrador [!DNL Assets] de [!DNL Experience Manager]. De hacerlo, evitará que los usuarios utilicen accidentalmente las características [!DNL Assets] que no obtuvo licencia.

## Uso de Media Library {#use-media-library}

Media Library abarca en general los siguientes casos de uso:

* Proporcione funciones básicas de DAM para páginas web creadas con [!DNL Adobe Experience Manager Sites].
* Los formularios adaptables y las comunicaciones creadas con [!DNL Adobe Experience Manager Forms].
* Experiencias de pantalla digital creadas con [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] API HTTP REST para operaciones sin encabezado.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Basic metadata properties
* Tag management
* Version control
* Static renditions
* Projects, tasks, workflow authoring
* Activity stream (timeline)
* Query Builder (API)
* Marketing Cloud integration
* User interface customization and extension
* Comments and annotation
-->

Para utilizar la funcionalidad de Media Library, puede utilizar la interfaz de usuario predeterminada [!DNL Experience Manager]. Media Library forma parte de la instalación de [!DNL Experience Manager Sites] y no se requiere ninguna interfaz ni complemento independiente. Con la interfaz existente, los usuarios de Media Library tienen derecho a realizar las siguientes tareas:

* Cree carpetas para organizar los recursos.
* Cargar recursos.
* Publicar recursos.
* Editar, mover y copiar recursos.
* Examinar, filtrar y buscar recursos (incluye la búsqueda por similitudes).
* Agregue valores a y edite los valores en los campos de metadatos, excepto el campo Etiquetas inteligentes , que están disponibles en la pestaña [!UICONTROL Básico] de la página [!UICONTROL Propiedades] de un recurso de forma predeterminada.
* Añada y elimine representaciones estáticas.
* Descargue carpetas, recursos y representaciones de recursos.
* Crear versiones de recursos.
* Cree y realice tareas de revisión en los recursos.
* Anotar recursos.
* Agregue recursos a páginas [!DNL Sites] a través del Buscador de contenido.
* Uso [!DNL Content Fragments].
* Utilice las API de HTTP REST y GraphQL para [!DNL Content Fragments] y los recursos de medios a los que se hace referencia, bajo licencia de Sites.
* Integración de Marketing Cloud.
* Personalice y amplíe la interfaz de usuario de administración de recursos.
* Acceda al Generador de consultas (API) para ampliar la funcionalidad de búsqueda.
* Crear etiquetas estáticas.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>[!DNL Experience Manager Assets] completa muchos casos de uso avanzados de DAM. La licencia de Media Library le da derecho a cumplir únicamente los casos de uso enumerados con Media Library. Si un caso de uso no aparece en la lista, no lo utilice con la licencia de Media Library. Si tiene alguna consulta, póngase en contacto con el servicio de atención al cliente de Adobe.

Tenga en cuenta que no puede utilizar etiquetas inteligentes, [!DNL Asset] vínculo, [!DNL Asset] selector, etiquetado masivo, modificación de flujos de trabajo de recursos sin [!DNL Assets] licencia.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Funciones DAM en [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Descripción del producto de Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 Descripción del producto local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

