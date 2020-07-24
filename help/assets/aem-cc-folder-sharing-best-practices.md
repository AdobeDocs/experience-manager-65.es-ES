---
title: Adobe Experience Manager a las prácticas recomendadas de uso compartido de carpetas de Adobe Creative Cloud
description: Configure Adobe Experience Manager para permitir que los usuarios de Recursos Experience Manager intercambien carpetas con usuarios de Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---


# Adobe Experience Manager al uso compartido de carpetas de Adobe Creative Cloud {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La función de Experience Manager de uso compartido de carpetas de Creative Cloud está en desuso. Adobe recomienda encarecidamente el uso de las nuevas funciones, como [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) o la aplicación [de escritorio](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)Experience Manager. Obtenga más información sobre las prácticas recomendadas [de integración de](/help/assets/aem-cc-integration-best-practices.md)Experience Manager y Creative Cloud.

Adobe Experience Manager se puede configurar para permitir que los usuarios de Recursos compartan carpetas con los usuarios de las aplicaciones de Adobe Creative Cloud, de modo que estén disponibles como carpetas compartidas en el servicio Adobe Creative Cloud Assets. La función se puede utilizar para intercambiar archivos entre equipos creativos y usuarios de Recursos, especialmente cuando los usuarios creativos no tienen acceso a la implementación de Recursos (no están en la red empresarial).

Este tipo de integración se puede utilizar en los siguientes casos de uso, especialmente cuando se trabaja con usuarios que no tienen acceso directo a Recursos:

* Los usuarios de Recursos comparten un conjunto de recursos específicos con usuarios de Adobe Creative Cloud Files (por ejemplo, un resumen creativo y un conjunto de recursos aprobados para el trabajo de diseño de una nueva actividad de marketing)
* Los usuarios de Recursos reciben nuevos archivos creados por los usuarios de la aplicación de Adobe Creative Cloud.

>[!NOTE]
>
>Antes de leer este documento, puede revisar las prácticas recomendadas [generales de integración de](/help/assets/aem-cc-integration-best-practices.md) Experience Manager y Creative Cloud para obtener una descripción general de nivel superior del tema.

## Información general {#overview}

El Experience Manager al uso compartido de carpetas de Creative Cloud depende del uso compartido de carpetas y archivos en el servidor entre Assets y las cuentas de Creative Cloud. Los profesionales de Creative Cloud, que utilizan la aplicación de escritorio de Creative Cloud en sus equipos de escritorio, también pueden hacer que las carpetas compartidas estén disponibles directamente en sus discos mediante la tecnología Adobe CreativeSync.

En el diagrama siguiente se proporciona una descripción general de la integración.

![chlimage_1-179](assets/chlimage_1-406.png)

La integración incluye los siguientes elementos:

* **Experience Manager Assets Server** implementado en la red empresarial (servicios gestionados o in situ): El uso compartido de carpetas se inicia aquí.
* **Servicio** principal de Recursos Adobe Marketing Cloud: Actúa como intermediario entre Experience Manager y los servicios de almacenamiento de Creative Cloud. El administrador de la compañía que utiliza la integración necesita establecer una relación de confianza entre la organización de Marketing Cloud y la implementación de Recursos. También [definen una lista de colaboradores](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html)aprobados de Creative Cloud, que los usuarios de Recursos también pueden compartir carpetas para mayor seguridad.

* **Servicios** web de Creative Cloud Assets (interfaz de usuario web de almacenamiento y Creative Cloud Files): Aquí es donde usuarios específicos de la aplicación de Creative Cloud, con los que se ha compartido una carpeta de recursos, pueden aceptar la invitación y ver la carpeta en el almacenamiento de su cuenta de Creative Cloud.
* **Aplicación** de escritorio de Creative Cloud: (Opcional) Permite el acceso directo a las carpetas o archivos compartidos desde el escritorio del usuario creativo mediante la sincronización con el almacenamiento de Creative Cloud Assets.

## Características y limitaciones {#characteristics-and-limitations}

* **Propagación unidireccional de cambios:** Los cambios en los archivos se propagan únicamente en una dirección, desde el sistema (Experience Manager o Creative Cloud Assets), donde se creó el recurso originalmente (se cargó). La integración no proporciona una sincronización bidireccional completamente automatizada entre los dos sistemas.
* **Versiones:**

   * Experience Manager solo crea versiones de un recurso en actualizaciones si el archivo se originó en el Experience Manager y se actualiza allí.
   * Creative Cloud Assets ofrece su propia función [de](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) control de versiones que está dirigida a las actualizaciones de Work in Progress (básicamente, almacena actualizaciones durante un máximo de 10 días)

* **Limitaciones de espacio:** Los tamaños y volúmenes de archivos intercambiados están limitados por la cuota [específica de](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud Assets para usuarios creativos (depende del nivel de suscripción) y una limitación de 5 GB de tamaño máximo de archivo. El espacio está limitado además por la cuota de recursos que la organización tiene en el servicio principal de Recursos de Adobe Marketing Cloud.

* **Requisitos de espacio:** Los archivos de las carpetas compartidas también deben almacenarse físicamente en el Experience Manager y, a continuación, en la cuenta de Creative Cloud, con una copia en caché en el servicio principal de Marketing Cloud Assets.
* **Redes y ancho de banda:** Los archivos de las carpetas compartidas y todas las actualizaciones deben trasladarse a través de la red entre los sistemas. Debe asegurarse de que solo se comparten los archivos y las actualizaciones relevantes.
* **Tipo** de carpeta: Compartir una carpeta de recursos del tipo `sling:OrderedFolder`, no se admite en el contexto de uso compartido en Adobe Marketing Cloud. Si desea compartir una carpeta, al crearla en Recursos, no seleccione la opción Pedido.

## Best practices {#best-practices}

Entre las prácticas recomendadas para aprovechar el uso compartido de Experience Manager en Creative Cloud se incluyen:

* **Consideraciones sobre el volumen:** El uso compartido de carpetas entre Experience Manager y Creative Cloud debe utilizarse para compartir un número menor de archivos, por ejemplo, relevantes para una campaña o actividad específica. Para compartir conjuntos más grandes de recursos, como todos los recursos aprobados en la organización, utilice otros métodos de distribución (por ejemplo, Assets Brand Portal) o la aplicación de escritorio de Experience Manager.

* **Evite compartir jerarquías profundas:** El uso compartido funciona de forma recursiva y no permite la desdistribución selectiva. Normalmente, solo se deben considerar para compartir las carpetas sin subcarpetas o con una jerarquía muy superficial, como un nivel de subcarpeta.
* **Separe las carpetas para compartir en un solo sentido:** Se deben utilizar carpetas independientes para compartir recursos finales de Recursos a archivos de Creative Cloud, así como para compartir recursos listos para la creación desde archivos de Creative Cloud a Assets. Junto con una buena convención de nombres para estas carpetas, crea un entorno de trabajo más fácil de entender tanto para los usuarios de Assets como de Creative Cloud.
* **Evite WIP en la carpeta compartida:** La carpeta compartida no debe utilizarse para el trabajo en curso; utilice una carpeta independiente en Creative Cloud Files para realizar un trabajo que requiera cambios frecuentes en el archivo.
* **Inicio del nuevo trabajo fuera de la carpeta compartida:** Los nuevos diseños (archivos creativos) deben iniciarse en la carpeta WIP independiente de Creative Cloud Files y, cuando estén listos para compartirse con los usuarios de Assets, deben moverse o guardarse en la carpeta compartida.
* **Simplifique la estructura de uso compartido:** Para una configuración operativa más manejable, piense en simplificar la estructura de uso compartido. En lugar de compartir con todos los usuarios creativos, las carpetas de recursos solo deben compartirse con los representantes del equipo, como un director creativo o un administrador de equipos. El administrador del lado creativo recibiría los recursos finales, decidiría las asignaciones de trabajo y, a continuación, dejaría que los diseñadores trabajaran en sus propias cuentas de Creative Cloud en los recursos de trabajo en curso. Pueden utilizar las funciones de colaboración de Creative Cloud para coordinar el trabajo y, por último, seleccionar y colocar los recursos que estén listos para volver a compartirse en Assets en su carpeta compartida lista para creativos.

El diagrama siguiente ilustra una configuración de ejemplo para crear nuevos diseños en función de los recursos finales existentes de Recursos.

![chlimage_1-180](assets/chlimage_1-407.png)
