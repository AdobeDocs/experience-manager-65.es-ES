---
title: Usar la biblioteca de medios para la administración básica de recursos digitales
description: '[!DNL Experience Manager Assets] y Biblioteca de medios para la administración de recursos.'
contentOwner: AG
role: Arquitecto, Encabezado
translation-type: tm+mt
source-git-commit: 15c525746a613eb33cd09b7ff476f43aa18b146b
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---


<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Usar la biblioteca de medios para la administración básica de recursos {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] platform proporciona diferentes funciones para administrar recursos. La biblioteca de medios permite a los usuarios cargar un pequeño número de recursos en el repositorio, buscarlos y utilizarlos en las páginas web y realizar tareas sencillas de administración de recursos en los recursos.

Media Library es una solución ligera de administración de activos digitales (DAM) que viene con licencia [!DNL Adobe Experience Manager Sites] de cortesía. [!DNL Sites] es una oferta de administración de contenido web (WCM). La biblioteca de medios funciona con todas las funciones de Experience Manager.

[!DNL Adobe Experience Manager Assets] la licencia está disponible por separado para su compra. [!DNL Experience Manager Assets] permite una gestión sólida de los recursos mediante casos de uso empresariales, personalizaciones de metadatos, esquemas, búsquedas e interfaz de usuario, y muchas otras funciones además de las que proporciona la biblioteca multimedia.

## Requisitos de licencia {#avail-media-library-license}

Los clientes con licencia [!DNL Sites] tienen derecho a usar la biblioteca multimedia. Funciona con todos los componentes de [!DNL Experience Manager].

La biblioteca de medios se instala como parte de Sites. No se requiere licencia o paquete adicional más allá de la licencia e instalación de Sites.

## [!DNL Assets] frente a la biblioteca multimedia  {#assets-and-media-library}

Recursos de Experience Manager proporciona funcionalidad DAM de nivel empresarial. La funcionalidad de los recursos se entrega con [!DNL Experience Manager] en un solo paquete. Sin embargo, los usuarios que no hayan adquirido una licencia de Assets no tienen derecho a utilizar las funciones avanzadas de DAM. Sin licencia de Assets, solo están disponibles las [funciones de la biblioteca multimedia](#use-media-library).

Si desea evitar el uso no intencionado de características [!DNL Assets] de las que no tiene licencia, elimine todos los flujos de trabajo, componentes, taxonomías, opciones específicos de [!DNL Assets] y el administrador [!DNL Assets] de [!DNL Experience Manager]. De hacerlo, evitará que los usuarios utilicen accidentalmente las características [!DNL Assets] que no obtuvo licencia.

## Usar la biblioteca multimedia {#use-media-library}

La biblioteca de medios abarca en general los siguientes casos de uso:

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

Para utilizar la funcionalidad Biblioteca de medios, puede utilizar la interfaz de usuario predeterminada [!DNL Experience Manager]. La biblioteca multimedia forma parte de la instalación de [!DNL Experience Manager Sites] y no se requiere ninguna interfaz ni complemento independiente. Con la interfaz existente, los usuarios de la biblioteca de medios tienen derecho a realizar las siguientes tareas:

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

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
-->

>[!IMPORTANT]
>
>[!DNL Experience Manager Assets] completa muchos casos de uso avanzados de DAM. La licencia de la biblioteca de medios le permite completar solo los casos de uso enumerados mediante la biblioteca de medios. Si un caso de uso no aparece en la lista, no lo utilice con la licencia de Media Library. Si tiene alguna consulta, póngase en contacto con el Servicio de atención al cliente de Adobe.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Funciones DAM en [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Descripción del producto de Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 Descripción del producto local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

