---
title: Prácticas recomendadas para compartir carpetas de AEM con Creative Cloud
description: Configure Adobe Experience Manager (AEM) para permitir que los usuarios de Recursos AEM intercambien carpetas con usuarios de Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Prácticas recomendadas para compartir carpetas de AEM con Creative Cloud {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La función AEM to Creative Cloud Folder Sharing está en desuso. Adobe recomienda encarecidamente el uso de nuevas funciones como [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) o la aplicación [de escritorio](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)AEM. Obtenga más información sobre las prácticas recomendadas [](/help/assets/aem-cc-integration-best-practices.md)de integración de AEM y Creative Cloud.

Adobe Experience Manager (AEM) se puede configurar para permitir que los usuarios de Recursos AEM compartan carpetas con los usuarios de las aplicaciones de Adobe Creative Cloud, de modo que estén disponibles como carpetas compartidas en el servicio Adobe Creative Cloud Assets. La función se puede utilizar para intercambiar archivos entre equipos creativos y usuarios de Recursos AEM, especialmente cuando los usuarios creativos no tienen acceso a la instancia de Recursos AEM (no están en la red empresarial).

Este tipo de integración se puede utilizar en los siguientes casos de uso, especialmente cuando se trabaja con usuarios que no tienen acceso directo a Recursos AEM:

* Los usuarios de Recursos AEM comparten un conjunto de recursos específicos con usuarios de Archivos de Adobe Creative Cloud (por ejemplo, un resumen creativo y un conjunto de recursos aprobados para el trabajo de diseño de una nueva actividad de marketing)
* Los usuarios de AEM Assets reciben nuevos archivos creados por usuarios de la aplicación de Adobe Creative Cloud.

>[!NOTE]
>
>Antes de leer este documento, puede revisar las prácticas [recomendadas generales de integración de](/help/assets/aem-cc-integration-best-practices.md) AEM y Creative Cloud para obtener una descripción general de nivel superior del tema.

## Información general {#overview}

El uso compartido de carpetas de AEM a Creative Cloud depende del uso compartido de carpetas y archivos del lado del servidor entre AEM Assets y cuentas de Creative Cloud. Los profesionales de Creative Cloud, que utilizan la aplicación de escritorio de Creative Cloud en sus equipos de escritorio, también pueden hacer que las carpetas compartidas estén disponibles directamente en sus discos mediante la tecnología Adobe CreativeSync.

En el diagrama siguiente se proporciona una descripción general de la integración.

![chlimage_1-179](assets/chlimage_1-406.png)

La integración incluye los siguientes elementos:

* **AEM Assets server** implementado en la red empresarial (servicios gestionados o in situ): El uso compartido de carpetas se inicia aquí.
* **Servicio** principal de Recursos de Adobe Marketing Cloud: Actúa como intermediario entre los servicios de almacenamiento de AEM y Creative Cloud. El administrador de la empresa que utiliza la integración necesita establecer una relación de confianza entre la organización de Marketing Cloud y la instancia de Recursos AEM. También [definen una lista de colaboradores](https://marketing.adobe.com/resources/help/en_US/mcloud/t_admin_add_cc_user.html)aprobados de Creative Cloud, que los usuarios de Recursos AEM también pueden compartir carpetas para mayor seguridad.

* **Servicios** web de Creative Cloud Assets (almacenamiento y interfaz de usuario web de Creative Cloud Files): Aquí es donde usuarios específicos de la aplicación de Creative Cloud, con los que se ha compartido una carpeta de Recursos AEM, podrían aceptar la invitación y ver la carpeta en el almacenamiento de su cuenta de Creative Cloud.
* **Aplicación** de escritorio de Creative Cloud: (Opcional) Permite el acceso directo a carpetas o archivos compartidos desde el escritorio del usuario creativo mediante la sincronización con el almacenamiento de Creative Cloud Assets.

## Características y limitaciones {#characteristics-and-limitations}

* **** Propagación unidireccional de cambios: Los cambios en los archivos se propagan en una sola dirección, desde el sistema (AEM o Creative Cloud Assets), donde el recurso se creó originalmente (se cargó). La integración no proporciona una sincronización bidireccional completamente automatizada entre los dos sistemas.
* **Versiones:**

   * AEM solo crea versiones de un recurso al actualizar si el archivo se originó en AEM y se actualiza en él.
   * Creative Cloud Assets ofrece su propia función [de](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) control de versiones que está dirigida a las actualizaciones de Work in Progress (básicamente, almacena actualizaciones durante un máximo de 10 días)

* **** Limitaciones de espacio: Los tamaños y volúmenes de archivos intercambiados están limitados por la cuota [](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) específica de Creative Cloud Assets para usuarios creativos (depende del nivel de suscripción) y una limitación de 5 GB de tamaño máximo de archivo. El espacio se ve limitado además por la cuota de recursos que tiene la organización en el servicio principal Recursos de Adobe Marketing Cloud.

* **** Requisitos de espacio: Los archivos de las carpetas compartidas también deben almacenarse físicamente en AEM y, a continuación, en la cuenta de Creative Cloud, con una copia en caché en el servicio principal de Marketing Cloud Assets.
* **** Redes y ancho de banda: Los archivos de las carpetas compartidas y todas las actualizaciones deben trasladarse a través de la red entre los sistemas. Debe asegurarse de que solo se comparten los archivos y las actualizaciones relevantes.
* **Tipo** de carpeta: Compartir una carpeta de recursos del tipo `sling:OrderedFolder`, no se admite en el contexto de uso compartido en Adobe Marketing Cloud. Si desea compartir una carpeta, al crearla en Recursos AEM, no seleccione la opción Pedido.

## Best practices {#best-practices}

Entre las prácticas recomendadas para aprovechar AEM para compartir carpetas de Creative Cloud se incluyen:

* **** Consideraciones sobre el volumen: El uso compartido de carpetas de AEM/Creative Cloud debe utilizarse para compartir un número menor de archivos, por ejemplo, relevantes para una campaña o actividad específica. Para compartir conjuntos más grandes de recursos, como todos los recursos aprobados en la organización, utilice otros métodos de distribución (por ejemplo, AEM Assets Brand Portal) o la aplicación de escritorio AEM.

* **** Evite compartir jerarquías profundas: El uso compartido funciona de forma recursiva y no permite la desdistribución selectiva. Normalmente, solo se deben considerar para compartir las carpetas sin subcarpetas o con una jerarquía muy superficial, como un nivel de subcarpeta.
* **** Separe las carpetas para compartir en un solo sentido: Se deben utilizar carpetas independientes para compartir recursos finales de AEM Assets en archivos de Creative Cloud y para compartir recursos listos para la creación desde archivos de Creative Cloud a AEM Assets. Junto con una buena convención de nombres para estas carpetas, crea un entorno de trabajo más fácil de entender tanto para AEM Assets como para los usuarios de Creative Cloud.
* **** Evite WIP en la carpeta compartida: La carpeta compartida no debe utilizarse para el trabajo en curso; utilice una carpeta independiente en Creative Cloud Files para realizar un trabajo que requiera cambios frecuentes en el archivo.
* **** Inicie un nuevo trabajo fuera de la carpeta compartida: Los nuevos diseños (archivos creativos) deben iniciarse en la carpeta WIP independiente de Creative Cloud Files y, cuando estén listos para compartirse con los usuarios de AEM Assets, deben moverse o guardarse en la carpeta compartida.
* **** Simplifique la estructura de uso compartido: Para una configuración operativa más manejable, piense en simplificar la estructura de uso compartido. En lugar de compartir con todos los usuarios creativos, las carpetas de Recursos AEM solo deben compartirse con los representantes del equipo, como un director creativo o un administrador de equipos. El administrador del lado creativo recibiría los recursos finales, decidiría las asignaciones de trabajo y, a continuación, dejaría que los diseñadores trabajaran en sus propias cuentas de Creative Cloud en los recursos de trabajo en curso. Pueden utilizar las funciones de colaboración de Creative Cloud para coordinar el trabajo y, por último, seleccionar y colocar recursos listos para compartir en Recursos AEM en su carpeta compartida lista para creativos.

El diagrama siguiente ilustra una configuración de ejemplo para crear nuevos diseños en función de los recursos finales existentes de Recursos AEM.

![chlimage_1-180](assets/chlimage_1-407.png)
