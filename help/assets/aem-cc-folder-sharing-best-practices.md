---
title: Uso compartido de carpetas en las  [!DNL Adobe Creative Cloud] prácticas recomendadas
description: Configure [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] para intercambiar carpetas con usuarios de Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] para compartir  [!DNL Adobe Creative Cloud] carpetas {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La función de uso compartido de carpetas [!DNL Experience Manager] a [!DNL Creative Cloud] está obsoleta. Adobe recomienda encarecidamente utilizar funciones más nuevas, como [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) o [Experience Manager desktop app](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Obtenga más información en [Prácticas recomendadas para la integración de Experience Manager y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] se puede configurar para permitir  [!DNL Assets] a los usuarios de en compartir carpetas con los usuarios de las  [!DNL Adobe Creative Cloud] aplicaciones, de modo que estén disponibles como carpetas compartidas en el servicio de  [!DNL Adobe Creative Cloud] recursos. La función se puede utilizar para intercambiar archivos entre equipos creativos y usuarios [!DNL Assets], especialmente cuando los usuarios creativos no tienen acceso a la implementación [!DNL Assets] (no están en la red empresarial).

Este tipo de integración se puede utilizar en los siguientes casos de uso, especialmente cuando se trabaja con usuarios que no tienen acceso directo a [!DNL Assets]:

* [!DNL Assets] los usuarios comparten un conjunto de recursos digitales específicos con usuarios de  [!DNL Adobe Creative Cloud] archivos (por ejemplo, un resumen creativo y un conjunto de recursos aprobados para trabajo de diseño para una nueva actividad de marketing).
* [!DNL Assets] los usuarios reciben nuevos archivos creados por los usuarios de la  [!DNL Adobe Creative Cloud] aplicación.

>[!NOTE]
>
>Antes de leer este documento, puede revisar las [prácticas recomendadas generales de integración de Experience Manager y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) para obtener información general sobre la integración.

## Información general {#overview}

[!DNL Experience Manager] el uso compartido de  [!DNL Creative Cloud] carpetas depende del uso compartido en el servidor de carpetas y archivos entre  [!DNL Assets] y  [!DNL Creative Cloud] cuentas. Los profesionales creativos, que utilizan la aplicación de escritorio [!DNL Creative Cloud] en sus escritorios, también pueden hacer que las carpetas compartidas estén disponibles directamente en sus discos mediante la tecnología [!DNL Adobe CreativeSync].

El diagrama siguiente proporciona una descripción general de la integración.

![chlimage_1-179](assets/chlimage_1-406.png)

La integración incluye los siguientes elementos:

* **[!DNL Experience Manager Assets]** implementado en la red empresarial (servicios administrados o locales): El uso compartido de carpetas se inicia aquí.
* **[!DNL Adobe Marketing Cloud Assets]servicio principal**: Actúa como intermediario entre  [!DNL Experience Manager] y los servicios de  [!DNL Creative Cloud] almacenamiento. Un administrador de una organización que utiliza la integración debe establecer una relación de confianza entre la organización de Marketing Cloud y la implementación [!DNL Assets]. También [definen una lista de colaboradores del Creative Cloud aprobados](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), que los usuarios [!DNL Assets] también pueden compartir carpetas para mayor seguridad.

* **[!DNL Creative Cloud]Servicios web de recursos**  (interfaz de usuario web de almacenamiento y  [!DNL Creative Cloud] archivos): Aquí es donde los usuarios específicos de la aplicación de Creative Cloud, con los que se compartió una  [!DNL Assets] carpeta, podrían aceptar la invitación y ver la carpeta en el almacenamiento de su cuenta de Creative Cloud.
* **aplicación de escritorio de Creative Cloud**: (Opcional) Permite el acceso directo a la carpeta o archivos compartidos desde el escritorio del usuario creativo a través de la sincronización con el almacenamiento de  [!DNL Creative Cloud] recursos.

## Características y limitaciones {#characteristics-and-limitations}

* **Propagación unidireccional de cambios:** los cambios del archivo se propagan solo en una dirección, desde el sistema ([!DNL Experience Manager]  o  [!DNL Creative Cloud Assets]), donde el recurso se creó originalmente (cargado). La integración no proporciona una sincronización bidireccional completamente automatizada entre los dos sistemas.
* **Versiones:**

   * [!DNL Experience Manager] solo crea versiones de un recurso en actualizaciones si el archivo se originó en  [!DNL Experience Manager] y se actualiza en él.
   * [!DNL Creative Cloud] Assets proporciona su propia  [función de versiones ](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) dirigida a las actualizaciones de Work in Progress (básicamente, almacena actualizaciones durante un máximo de 10 días)

* **Limitaciones de espacio:** los tamaños y volúmenes de archivos intercambiados están limitados por la cuota específica de  [Creative Cloud Assets ](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) para usuarios creativos (depende del nivel de suscripción) y una limitación de 5 GB de tamaño máximo de archivo. El espacio está limitado además por la cuota de recursos que la organización tiene en el servicio principal Adobe Marketing Cloud Assets.

* **Requisitos de espacio:** Los archivos de carpetas compartidas también deben almacenarse físicamente en  [!DNL Experience Manager] y luego en la  [!DNL Creative Cloud] cuenta, con una copia en caché en el servicio  [!DNL Marketing Cloud Assets] principal.
* **Redes y ancho de banda:**  Los archivos de carpetas compartidas y todas las actualizaciones deben transportarse a través de la red entre los sistemas. Debe asegurarse de que solo se compartan los archivos y las actualizaciones relevantes.
* **Tipo** de carpeta: El uso compartido de una  [!DNL Assets] carpeta del tipo  `sling:OrderedFolder`, no se admite en el contexto de uso compartido en  [!DNL Adobe Marketing Cloud]. Si desea compartir una carpeta, al crearla en [!DNL Assets], no seleccione la opción [!UICONTROL Pedido].

## Prácticas recomendadas {#best-practices}

Las prácticas recomendadas para aprovechar el uso compartido de carpetas [!DNL Experience Manager] a [!DNL Creative Cloud] incluyen:

* **Consideraciones sobre el volumen:** [!DNL Experience Manager] y el uso compartido de  [!DNL Creative Cloud] carpetas debe usarse para compartir un número menor de archivos, por ejemplo, relevantes para una campaña o actividad específica. Para compartir conjuntos más grandes de recursos, como todos los recursos aprobados de la organización, utilice otros métodos de distribución (por ejemplo, [!DNL Assets Brand Portal]) o la aplicación de escritorio [!DNL Experience Manager].
* **Evite compartir jerarquías profundas:** El uso compartido funciona de forma recursiva y no permite el uso compartido selectivo. Normalmente, solo las carpetas sin subcarpetas o con una jerarquía muy superficial, como un nivel de subcarpeta, deben considerarse para el uso compartido.
* **Carpetas independientes para el uso compartido unidireccional:** Las carpetas independientes deben utilizarse para compartir recursos finales de  [!DNL Assets] a  [!DNL Creative Cloud] archivos y para compartir recursos listos para el proceso creativo de vuelta de  [!DNL Creative Cloud] archivos a  [!DNL Assets]. Junto con una buena convención de nombres para estas carpetas, crea un entorno de trabajo más fácil de entender para los usuarios [!DNL Assets] y [!DNL Creative Cloud] por igual.
* **Evitar WIP en la carpeta compartida:**  La carpeta compartida no debe utilizarse para el trabajo en curso. Utilice una carpeta independiente en los archivos de Creative Cloud para realizar trabajos que requieran cambios frecuentes en el archivo.
* **Iniciar nuevo trabajo fuera de la carpeta compartida:**  Los nuevos diseños (archivos creativos) deben iniciarse en la carpeta WIP independiente de los archivos Creative Cloud y, cuando estén listos para compartirse con los  [!DNL Assets] usuarios, deben moverse o guardarse en la carpeta compartida.
* **Simplificar la estructura de uso compartido:** para una configuración operativa más manejable, piense en simplificar la estructura de uso compartido. En lugar de compartir con todos los usuarios creativos, las [!DNL Assets] carpetas solo deben compartirse con los representantes del equipo, como un director creativo o un administrador de equipos. El administrador del lado creativo recibiría los recursos finales, decidiría las asignaciones de trabajo y, a continuación, permitiría a los diseñadores trabajar en sus propias cuentas de Creative Cloud en los recursos de trabajo en curso. Pueden utilizar funciones de colaboración de Creative Cloud para coordinar el trabajo y, finalmente, seleccionar y colocar recursos que estén listos para compartir en [!DNL Assets] en su carpeta compartida lista para la creación.

El diagrama siguiente ilustra una configuración de ejemplo para crear nuevos diseños basada en los recursos finales existentes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
