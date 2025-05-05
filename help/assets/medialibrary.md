---
title: Uso de Media Library para la administración básica de recursos digitales
description: "[!DNL Experience Manager Assets] y Media Library para la administración de recursos."
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---


# Uso de Media Library para la administración básica de recursos {#manage-assets-using-media-library}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=es) |
| AEM 6.5 | Este artículo |

La plataforma [!DNL Adobe Experience Manager] proporciona diferentes capacidades para administrar recursos. Media Library permite a los usuarios cargar un pequeño número de recursos en el repositorio, buscarlos y utilizarlos en las páginas web y realizar tareas sencillas de administración de recursos en los recursos.

Media Library es una solución ligera de administración de activos digitales (DAM) que se suministra de forma gratuita con la licencia [!DNL Adobe Experience Manager Sites]. [!DNL Sites] es una oferta de Administración de contenido web (WCM). Media Library funciona con todas las funcionalidades de Experience Manager.

La licencia [!DNL Adobe Experience Manager Assets] está disponible por separado para su compra. [!DNL Experience Manager Assets] permite una administración sólida de los recursos a través de casos de uso empresariales, personalizaciones de metadatos, esquemas, búsquedas e interfaz de usuario, y muchas otras características además de lo que proporciona Media Library.

## Requisitos de licencia {#avail-media-library-license}

Los clientes que tengan la licencia [!DNL Sites] tienen derecho a usar Media Library. Funciona con todos los componentes de [!DNL Experience Manager].

Media Library se instala como parte de Sites. No se requiere ninguna licencia o paquete adicional más allá de la licencia e instalación de Sites.

## [!DNL Assets] frente a Media Library {#assets-and-media-library}

Experience Manager Assets proporciona funcionalidad DAM de nivel empresarial. La funcionalidad de Assets se entrega con [!DNL Experience Manager] en un solo paquete. Sin embargo, los usuarios que no hayan adquirido una licencia de Assets no tienen derecho a utilizar las funciones avanzadas de DAM. Sin la licencia de Assets, solo están disponibles [las características de Media Library](#use-media-library).

Si desea evitar el uso no intencionado de las características de [!DNL Assets] para las que no tiene licencia, quite todos los flujos de trabajo, componentes, taxonomías, opciones y el administrador de [!DNL Assets] de [!DNL Experience Manager], que son específicos de [!DNL Assets]. Al hacerlo, se evita que los usuarios usen accidentalmente características de [!DNL Assets] para las que no se obtuvo licencia.

## Uso de Media Library {#use-media-library}

Media Library proporciona funciones básicas de DAM para los siguientes casos de uso:

* Páginas web creadas con [!DNL Adobe Experience Manager Sites].
* Formularios adaptables y comunicaciones creadas con [!DNL Adobe Experience Manager Forms].
* Experiencias de pantalla digital creadas con [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] API de REST HTTP para operaciones sin encabezado.

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

Para usar la funcionalidad Media Library, puede usar la interfaz de usuario predeterminada [!DNL Experience Manager]. Media Library forma parte de la instalación de [!DNL Experience Manager Sites] y no se requiere ninguna interfaz o complemento independiente. Con la interfaz existente, los usuarios de Media Library tienen derecho a realizar las siguientes tareas:

* Cree carpetas para organizar los recursos.
* Cargar recursos.
* Recursos de Publish.
* Editar, mover y copiar recursos.
* Examinar, filtrar y buscar (incluye la búsqueda por similitudes) recursos.
* Agregue valores y edite los valores de los campos de metadatos, excepto Etiquetas inteligentes, que están disponibles en la ficha [!UICONTROL Básico] de la página [!UICONTROL Propiedades] de un recurso de forma predeterminada.
* Agregar y eliminar representaciones estáticas.
* Descargar carpetas, recursos y representaciones de recursos.
* Crear versiones de recursos.
* Cree y realice tareas de revisión en los recursos.
* Anotar recursos.
* Agregar recursos a [!DNL Sites] páginas mediante el buscador de contenido.
* Usar [!DNL Content Fragments].
* Use las API HTTP REST y GraphQL para [!DNL Content Fragments] y los recursos de medios a los que se hace referencia en la licencia de Sites.
* Integración de Marketing Cloud.
* Personalice y amplíe la interfaz de usuario de administración de recursos.
* Acceda al Generador de consultas (API) para ampliar la funcionalidad de búsqueda.
* Crear etiquetas estáticas.
* Crear proyectos y tareas.
* Flujo de actividad (cronología).
* Comentarios y anotaciones.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Muchos casos de uso de DAM avanzados los ha completado [!DNL Experience Manager Assets]. La licencia de Media Library le da derecho a realizar únicamente los casos de uso enumerados mediante Media Library. Si un caso de uso no aparece en la lista, no lo utilice con la licencia de Media Library. Si tiene alguna duda, póngase en contacto con el Servicio de atención al cliente de Adobe.

Tenga en cuenta que no puede utilizar etiquetas inteligentes, el vínculo [!DNL Asset], el selector [!DNL Asset], el etiquetado masivo, modificar los flujos de trabajo de recursos ni la interfaz de usuario estándar [!DNL Adobe Experience Manager] para acceder a Media Library sin la licencia [!DNL Assets].

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Funciones DAM en [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html?lang=es)
>* [[!DNL Experience Manager] Descripción del producto de Managed Services de 6.5](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] Descripción del producto on-premise de 6.5](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-on-premise.html)
