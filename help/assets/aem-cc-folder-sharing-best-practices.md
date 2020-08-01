---
title: '[!Adobe Experience Manager DNL] [!DNL Adobe Creative Cloud] para compartir carpetas.'
description: ' [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] Configure el intercambio de carpetas con usuarios de Adobe Creative Cloud (CC).'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] a compartir [!DNL Adobe Creative Cloud] carpetas {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La función [!DNL Experience Manager] para compartir [!DNL Creative Cloud] carpetas está en desuso. Adobe recomienda encarecidamente el uso de las nuevas funciones, como [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) o la aplicación [de escritorio](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)Experience Manager. Obtenga más información sobre las prácticas recomendadas [de integración de](/help/assets/aem-cc-integration-best-practices.md)Experience Manager y Creative Cloud.

[!DNL Adobe Experience Manager] se puede configurar para permitir a los usuarios de [!DNL Assets] para que compartan carpetas con los usuarios de [!DNL Adobe Creative Cloud] las aplicaciones, de modo que estén disponibles como carpetas compartidas en el servicio de [!DNL Adobe Creative Cloud] recursos. La función se puede utilizar para intercambiar archivos entre equipos creativos y [!DNL Assets] usuarios, especialmente cuando los usuarios creativos no tienen acceso a la implementación (no están en la red empresarial) [!DNL Assets] .

Este tipo de integración se puede utilizar en los siguientes casos de uso, especialmente cuando se trabaja con usuarios que no tienen acceso directo a [!DNL Assets]:

* [!DNL Assets] los usuarios comparten un conjunto de recursos digitales específicos con usuarios de [!DNL Adobe Creative Cloud] archivos (por ejemplo, un resumen creativo y un conjunto de recursos aprobados para el trabajo de diseño de una nueva actividad de marketing).
* [!DNL Assets] los usuarios reciben nuevos archivos creados por los usuarios [!DNL Adobe Creative Cloud] de la aplicación.

>[!NOTE]
>
>Antes de leer este documento, puede revisar las optimizaciones [generales de integración de](/help/assets/aem-cc-integration-best-practices.md) Experience Manager y Creative Cloud para obtener una visión general de la integración.

## Información general {#overview}

[!DNL Experience Manager] el uso compartido de [!DNL Creative Cloud] carpetas depende del uso compartido por parte del servidor de carpetas y archivos entre [!DNL Assets] y [!DNL Creative Cloud] cuentas. Los profesionales creativos, que utilizan la aplicación de [!DNL Creative Cloud] escritorio en sus equipos de escritorio, también pueden hacer que las carpetas compartidas estén disponibles directamente en sus discos mediante [!DNL Adobe CreativeSync] tecnología.

En el diagrama siguiente se proporciona una descripción general de la integración.

![chlimage_1-179](assets/chlimage_1-406.png)

La integración incluye los siguientes elementos:

* **[!DNL Experience Manager Assets]** implementada en la red empresarial (servicios administrados o in situ): El uso compartido de carpetas se inicia aquí.
* **[!DNL Adobe Marketing Cloud Assets]servicio **principal: Actúa como intermediario entre[!DNL Experience Manager]y servicios de[!DNL Creative Cloud]almacenamiento. Un administrador de una organización que utiliza la integración necesita establecer una relación de confianza entre la organización de Marketing Cloud y la implementación[!DNL Assets]. También[definen una lista de colaboradores](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html)Creative Cloud aprobados, que[!DNL Assets]los usuarios pueden compartir carpetas también para mayor seguridad.

* **[!DNL Creative Cloud]Servicios **[!DNL Creative Cloud]web de recursos (interfaz de usuario web de archivos y almacenamientos): Aquí es donde usuarios específicos de la aplicación Creative Cloud, con los que se compartió una[!DNL Assets]carpeta, podrían aceptar la invitación y ver la carpeta en el almacenamiento de su cuenta Creative Cloud.
* **Aplicación** de escritorio Creative Cloud: (Opcional) Permite el acceso directo a carpetas o archivos compartidos desde el escritorio del usuario creativo mediante la sincronización con [!DNL Creative Cloud] Assets almacenamiento.

## Características y limitaciones {#characteristics-and-limitations}

* **Propagación unidireccional de cambios:** Los cambios en los archivos se propagan únicamente en una dirección, desde el sistema ([!DNL Experience Manager] o [!DNL Creative Cloud Assets]), donde el recurso se creó originalmente (se cargó). La integración no proporciona una sincronización bidireccional completamente automatizada entre los dos sistemas.
* **Versiones:**

   * [!DNL Experience Manager] solo crea versiones de un recurso en actualizaciones si el archivo se originó en [!DNL Experience Manager] y se actualiza allí.
   * [!DNL Creative Cloud] Assets ofrece su propia función [de](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) control de versiones que está dirigida a las actualizaciones de Work in Progress (básicamente, almacena actualizaciones de hasta 10 días)

* **Limitaciones de espacio:** Los tamaños y volúmenes de archivos intercambiados están limitados por la cuota [específica de recursos de](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud para usuarios creativos (depende del nivel de suscripción) y una limitación de 5 GB de tamaño máximo de archivo. El espacio está limitado además por la cuota de recursos que la organización tiene en el servicio principal de Recursos de Adobe Marketing Cloud.

* **Requisitos de espacio:** Los archivos de las carpetas compartidas también deben almacenarse físicamente en [!DNL Experience Manager] y luego en [!DNL Creative Cloud] la cuenta, con una copia en caché en el servicio [!DNL Marketing Cloud Assets] principal.
* **Redes y ancho de banda:** Los archivos de las carpetas compartidas y todas las actualizaciones deben trasladarse a través de la red entre los sistemas. Debe asegurarse de que solo se comparten los archivos y las actualizaciones relevantes.
* **Tipo** de carpeta: Compartir una [!DNL Assets] carpeta del tipo `sling:OrderedFolder`, no se admite en el contexto de compartir en [!DNL Adobe Marketing Cloud]. Si desea compartir una carpeta, al crearla en [!DNL Assets], no seleccione la opción [!UICONTROL Pedido] .

## Best practices {#best-practices}

Entre las prácticas recomendadas para aprovechar el uso compartido de [!DNL Experience Manager] dos [!DNL Creative Cloud] carpetas se incluyen:

* **Consideraciones sobre el volumen:** [!DNL Experience Manager] y [!DNL Creative Cloud] el uso compartido de carpetas debe utilizarse para compartir un número menor de archivos, por ejemplo, relevantes para una campaña o actividad específica. Para compartir conjuntos más grandes de recursos, como todos los recursos aprobados en la organización, utilice otros métodos de distribución (por ejemplo, [!DNL Assets Brand Portal]) o la aplicación de [!DNL Experience Manager] escritorio.
* **Evite compartir jerarquías profundas:** El uso compartido funciona de forma recursiva y no permite la desdistribución selectiva. Normalmente, solo se deben considerar para compartir las carpetas sin subcarpetas o con una jerarquía muy superficial, como un nivel de subcarpeta.
* **Separe las carpetas para compartir en un solo sentido:** Se deben utilizar carpetas independientes para compartir recursos finales de [!DNL Assets] a [!DNL Creative Cloud] archivos y para compartir recursos listos para la creación de [!DNL Creative Cloud] archivos a [!DNL Assets]. Junto con una buena convención de nombres para estas carpetas, crea un entorno de trabajo más fácil de entender tanto para [!DNL Assets] los usuarios como para [!DNL Creative Cloud] los usuarios.
* **Evite WIP en la carpeta compartida:** La carpeta compartida no se debe utilizar para el trabajo en curso: utilice una carpeta independiente en Archivos Creative Cloud para realizar trabajos que requieran cambios frecuentes en el archivo.
* **Inicio del nuevo trabajo fuera de la carpeta compartida:** Los nuevos diseños (archivos creativos) deben iniciarse en la carpeta WIP independiente de Archivos Creative Cloud y, cuando estén listos para compartirse con [!DNL Assets] los usuarios, deben moverse o guardarse en la carpeta compartida.
* **Simplifique la estructura de uso compartido:** Para una configuración operativa más manejable, piense en simplificar la estructura de uso compartido. En lugar de compartir con todos los usuarios creativos, las carpetas solo deben compartirse con los representantes del equipo, como un director creativo o un administrador de equipos. [!DNL Assets] El administrador del lado creativo recibiría los activos finales, decidiría las asignaciones de trabajo y, a continuación, dejaría que los diseñadores trabajaran en sus propias cuentas de Creative Cloud en los activos de WIP. Pueden utilizar funciones de colaboración de Creative Cloud para coordinar el trabajo y, finalmente, seleccionar y colocar los recursos que estén listos para volver a compartirse [!DNL Assets] en la carpeta compartida preparada para la creación.

El diagrama siguiente ilustra una configuración de ejemplo para crear nuevos diseños en función de los recursos finales existentes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
