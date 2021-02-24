---
title: 'Prácticas recomendadas para compartir carpetas con [!DNL Adobe Creative Cloud] '
description: Configure [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] para intercambiar carpetas con usuarios de Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 18e62f8fb46de20e1668b2dcdcedf68fe4622b50
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] para compartir  [!DNL Adobe Creative Cloud] carpetas  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La función [!DNL Experience Manager] a [!DNL Creative Cloud] Uso compartido de carpetas está en desuso. Adobe recomienda enfáticamente utilizar las nuevas funciones como [Vínculo de recursos de Adobe](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) o [Aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Obtenga más información en [optimizaciones para la integración de Experience Manager y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] se puede configurar para permitir  [!DNL Assets] a los usuarios de para que compartan carpetas con los usuarios de  [!DNL Adobe Creative Cloud] aplicaciones, de modo que estén disponibles como carpetas compartidas en el servicio de  [!DNL Adobe Creative Cloud] recursos. La función se puede utilizar para intercambiar archivos entre equipos creativos y [!DNL Assets] usuarios, especialmente cuando los usuarios creativos no tienen acceso a la implementación [!DNL Assets] (no están en la red empresarial).

Este tipo de integración se puede utilizar en los siguientes casos de uso, especialmente cuando se trabaja con usuarios que no tienen acceso directo a [!DNL Assets]:

* [!DNL Assets] los usuarios comparten un conjunto de recursos digitales específicos con usuarios de  [!DNL Adobe Creative Cloud] archivos (por ejemplo, un resumen creativo y un conjunto de recursos aprobados para el trabajo de diseño de una nueva actividad de marketing).
* [!DNL Assets] los usuarios reciben nuevos archivos creados por los usuarios  [!DNL Adobe Creative Cloud] de la aplicación.

>[!NOTE]
>
>Antes de leer este documento, puede revisar las [optimizaciones generales de integración de Experience Manager y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) para obtener una visión general de la integración.

## Información general {#overview}

[!DNL Experience Manager] el uso compartido de  [!DNL Creative Cloud] carpetas depende del uso compartido por parte del servidor de carpetas y archivos entre  [!DNL Assets] y  [!DNL Creative Cloud] cuentas. Los profesionales creativos, que utilizan la aplicación de escritorio [!DNL Creative Cloud] en sus escritorios, también pueden hacer que las carpetas compartidas estén disponibles directamente en sus discos mediante la tecnología [!DNL Adobe CreativeSync].

En el diagrama siguiente se proporciona una descripción general de la integración.

![chlimage_1-179](assets/chlimage_1-406.png)

La integración incluye los siguientes elementos:

* **[!DNL Experience Manager Assets]** implementada en la red empresarial (servicios administrados o in situ): El uso compartido de carpetas se inicia aquí.
* **[!DNL Adobe Marketing Cloud Assets]servicio** principal: Actúa como intermediario entre  [!DNL Experience Manager] y servicios de  [!DNL Creative Cloud] almacenamiento. Un administrador de una organización que utiliza la integración necesita establecer una relación de confianza entre la organización de Marketing Cloud y la implementación [!DNL Assets]. También [definen una lista de colaboradores de Creative Cloud aprobados](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), que los usuarios [!DNL Assets] pueden compartir carpetas también para mayor seguridad.

* **[!DNL Creative Cloud]Servicios**  web de recursos (IU web de almacenamiento y  [!DNL Creative Cloud] archivos): Aquí es donde usuarios específicos de la aplicación Creative Cloud, con los que se compartió una  [!DNL Assets] carpeta, podrían aceptar la invitación y ver la carpeta en el almacenamiento de su cuenta Creative Cloud.
* **Aplicación** de escritorio Creative Cloud: (Opcional) Permite el acceso directo a carpetas o archivos compartidos desde el escritorio del usuario creativo mediante la sincronización con  [!DNL Creative Cloud] Assets almacenamiento.

## Características y limitaciones {#characteristics-and-limitations}

* **Propagación unidireccional de cambios:los cambios** de archivos se propagan solo en una dirección, desde el sistema ([!DNL Experience Manager] o  [!DNL Creative Cloud Assets]), donde el recurso se creó originalmente (se cargó). La integración no proporciona una sincronización bidireccional completamente automatizada entre los dos sistemas.
* **Versiones:**

   * [!DNL Experience Manager] solo crea versiones de un recurso en actualizaciones si el archivo se originó  [!DNL Experience Manager] y se actualiza allí.
   * [!DNL Creative Cloud] Assets ofrece su propia  [función de ](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) control de versiones que está dirigida a las actualizaciones de Work in Progress (básicamente, almacena actualizaciones de hasta 10 días)

* **Limitaciones de espacio:** los tamaños y volúmenes de archivos intercambiados están limitados por la cuota específica de recursos de  [Creative Cloud ](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) para usuarios creativos (depende del nivel de suscripción) y una limitación de 5 GB de tamaño máximo de archivo. El espacio está limitado además por la cuota de recursos que la organización tiene en el servicio principal de Adobe Marketing Cloud Assets.

* **Requisitos de espacio:** Los archivos de las carpetas compartidas también deben almacenarse físicamente en  [!DNL Experience Manager] y, a continuación, en la  [!DNL Creative Cloud] cuenta, con una copia en caché en el servicio  [!DNL Marketing Cloud Assets] principal.
* **Redes y ancho de banda:** Los archivos de las carpetas compartidas y todas las actualizaciones deben transportarse a través de la red entre los sistemas. Debe asegurarse de que solo se comparten los archivos y las actualizaciones relevantes.
* **Tipo** de carpeta: Compartir una  [!DNL Assets] carpeta del tipo  `sling:OrderedFolder`, no se admite en el contexto de compartir en  [!DNL Adobe Marketing Cloud]. Si desea compartir una carpeta, al crearla en [!DNL Assets], no seleccione la opción [!UICONTROL Pedido].

## Prácticas recomendadas {#best-practices}

Las prácticas recomendadas para aprovechar el uso compartido de carpetas [!DNL Experience Manager] a [!DNL Creative Cloud] incluyen:

* **Consideraciones sobre el volumen:** [!DNL Experience Manager] y el uso compartido de  [!DNL Creative Cloud] carpetas debe usarse para compartir un número menor de archivos, por ejemplo, relevantes para una campaña o actividad específica. Para compartir conjuntos más grandes de recursos, como todos los recursos aprobados en la organización, utilice otros métodos de distribución (por ejemplo, [!DNL Assets Brand Portal]) o [!DNL Experience Manager] aplicación de escritorio.
* **Evite compartir jerarquías profundas:** El uso compartido funciona de forma recursiva y no permite la anulación del uso compartido selectivo. Normalmente, solo se deben considerar para compartir las carpetas sin subcarpetas o con una jerarquía muy superficial, como un nivel de subcarpeta.
* **Carpetas independientes para el uso compartido unidireccional:** Las carpetas independientes se deben utilizar para compartir recursos finales de  [!DNL Assets] a  [!DNL Creative Cloud] archivos y para volver a compartir recursos listos para la creación de  [!DNL Creative Cloud] archivos a  [!DNL Assets]. Junto con una buena convención de nombres para estas carpetas, crea un entorno de trabajo más fácil de entender para los usuarios [!DNL Assets] y [!DNL Creative Cloud] por igual.
* **Evite el trabajo en curso en la carpeta compartida:la carpeta** compartida no debe utilizarse para el trabajo en curso; utilice una carpeta separada en Archivos Creative Cloud para realizar trabajos que requieran cambios frecuentes en el archivo.
* **Inicio de nuevo trabajo fuera de la carpeta compartida:** Los nuevos diseños (archivos creativos) deben iniciarse en la carpeta WIP independiente en Archivos Creative Cloud y, cuando estén listos para compartirse con  [!DNL Assets] los usuarios, deben moverse o guardarse en la carpeta compartida.
* **Simplifique la estructura de uso compartido:** para una configuración operativa más manejable, piense en simplificar la estructura de uso compartido. En lugar de compartir con todos los usuarios creativos, [!DNL Assets] carpetas deben compartirse únicamente con los representantes del equipo, como un director creativo o un administrador de equipos. El administrador del lado creativo recibiría los activos finales, decidiría las asignaciones de trabajo y, a continuación, dejaría que los diseñadores trabajaran en sus propias cuentas de Creative Cloud en los activos de WIP. Pueden utilizar las funciones de colaboración de Creative Cloud para coordinar el trabajo y, finalmente, seleccionar y colocar los recursos que estén listos para volver a compartirse en [!DNL Assets] en su carpeta compartida lista para creativos.

El diagrama siguiente ilustra una configuración de ejemplo para crear nuevos diseños en función de los recursos finales existentes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
