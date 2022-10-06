---
title: Uso compartido de carpetas en [!DNL Adobe Creative Cloud] prácticas recomendadas
description: Configurar [!DNL Adobe Experience Manager] para permitir a los usuarios en [!DNL Experience Manager Assets] para intercambiar carpetas con usuarios de Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] a [!DNL Adobe Creative Cloud] uso compartido de carpetas {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La variable [!DNL Experience Manager] a [!DNL Creative Cloud] La función Uso compartido de carpetas está en desuso. Adobe recomienda encarecidamente utilizar funciones más nuevas, como [Vínculo de recurso de Adobe](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) o [aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Obtenga más información en [Prácticas recomendadas para la integración de Experience Manager y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] se puede configurar para permitir que los usuarios [!DNL Assets] para compartir carpetas con los usuarios de [!DNL Adobe Creative Cloud] para que estén disponibles como carpetas compartidas en la variable [!DNL Adobe Creative Cloud] servicio de activos. La función se puede utilizar para intercambiar archivos entre equipos creativos y [!DNL Assets] usuarios, especialmente cuando los usuarios creativos no tienen acceso al [!DNL Assets] implementación (no están en la red empresarial).

Este tipo de integración se puede utilizar en los siguientes casos de uso, especialmente cuando se trabaja con usuarios que no tienen acceso directo a [!DNL Assets]:

* [!DNL Assets] los usuarios comparten un conjunto de recursos digitales específicos con los usuarios de [!DNL Adobe Creative Cloud] (por ejemplo, un resumen creativo y un conjunto de recursos aprobados para trabajo de diseño para una nueva actividad de marketing).
* [!DNL Assets] los usuarios reciben nuevos archivos creados por [!DNL Adobe Creative Cloud] usuarios de la aplicación.

>[!NOTE]
>
>Antes de leer este documento, puede revisar el [Prácticas recomendadas para la integración de Experience Manager y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) para obtener una descripción general de la integración.

## Información general {#overview}

[!DNL Experience Manager] a [!DNL Creative Cloud] el uso compartido de carpetas depende del uso compartido de carpetas y archivos en el servidor entre [!DNL Assets] y [!DNL Creative Cloud] cuentas. Profesionales creativos que utilizan la variable [!DNL Creative Cloud] aplicación de escritorio en sus escritorios, puede además hacer que las carpetas compartidas estén disponibles directamente en sus discos mediante [!DNL Adobe CreativeSync] tecnología.

El diagrama siguiente proporciona una descripción general de la integración.

![chlimage_1-179](assets/chlimage_1-406.png)

La integración incluye los siguientes elementos:

* **[!DNL Experience Manager Assets]** implementado en la red empresarial (servicios administrados o locales): El uso compartido de carpetas se inicia aquí.
* **[!DNL Adobe Marketing Cloud Assets]servicio principal**: Actúa como intermediario entre [!DNL Experience Manager] y [!DNL Creative Cloud] servicios de almacenamiento. Un administrador de una organización que utiliza la integración debe establecer una relación de confianza entre la organización de Marketing Cloud y la [!DNL Assets] implementación. También [definir una lista de colaboradores del Creative Cloud aprobados](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), que [!DNL Assets] los usuarios también pueden compartir carpetas para mayor seguridad.

* **[!DNL Creative Cloud]Servicios web de recursos** (almacenamiento y [!DNL Creative Cloud] interfaz de usuario web de archivos): Aquí es donde los usuarios específicos de la aplicación de Creative Cloud, con los que un [!DNL Assets] se ha compartido, podría aceptar la invitación y ver la carpeta en el almacenamiento de su cuenta de Creative Cloud.
* **aplicación de escritorio de Creative Cloud**: (Opcional) Permite el acceso directo a la carpeta o archivos compartidos desde el escritorio del usuario creativo a través de la sincronización con [!DNL Creative Cloud] Almacenamiento de recursos.

## Características y limitaciones {#characteristics-and-limitations}

* **Propagación unidireccional de cambios:** Los cambios en los archivos se propagan en una sola dirección: desde el sistema ([!DNL Experience Manager] o [!DNL Creative Cloud Assets]), donde el recurso se creó originalmente (cargado). La integración no proporciona una sincronización bidireccional completamente automatizada entre los dos sistemas.
* **Versiones:**

   * [!DNL Experience Manager] solo crea versiones de un recurso en actualizaciones si el archivo se originó en [!DNL Experience Manager] y se actualiza allí.
   * [!DNL Creative Cloud] Assets proporciona su propio [función de versiones](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) que está dirigido a las actualizaciones de Work in Progress (básicamente, almacena actualizaciones durante un máximo de 10 días)

* **Limitaciones de espacio:** Los tamaños y volúmenes de archivos intercambiados están limitados por el [Cuota de recursos del Creative Cloud](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) para usuarios creativos (depende del nivel de suscripción) y una limitación de 5 GB de tamaño máximo de archivo. El espacio está limitado además por la cuota de recursos que la organización tiene en el servicio principal Adobe Marketing Cloud Assets.

* **Requisitos de espacio:** Los archivos de las carpetas compartidas también deben almacenarse físicamente en [!DNL Experience Manager] y luego en [!DNL Creative Cloud] cuenta, con una copia en caché en [!DNL Marketing Cloud Assets] servicio principal.
* **Redes y ancho de banda:** Los archivos de carpetas compartidas y todas las actualizaciones deben transportarse a través de la red entre los sistemas. Debe asegurarse de que solo se compartan los archivos y las actualizaciones relevantes.
* **Tipo de carpeta**: Uso compartido de [!DNL Assets] carpeta del tipo `sling:OrderedFolder`, no es compatible con el uso compartido en [!DNL Adobe Marketing Cloud]. Si desea compartir una carpeta, al crearla en [!DNL Assets], no seleccione el [!UICONTROL Pedido] .

## Prácticas recomendadas {#best-practices}

Prácticas recomendadas para aprovechar el [!DNL Experience Manager] a [!DNL Creative Cloud] el uso compartido de carpetas incluye:

* **Consideraciones sobre el volumen:** [!DNL Experience Manager] y [!DNL Creative Cloud] El uso compartido de carpetas debe utilizarse para compartir un número menor de archivos, por ejemplo, relevantes para una campaña o actividad específica. Para compartir conjuntos más grandes de activos, como todos los recursos aprobados de la organización, utilice otros métodos de distribución (por ejemplo, [!DNL Assets Brand Portal]) o [!DNL Experience Manager] aplicación de escritorio.
* **Evite compartir jerarquías profundas:** El uso compartido funciona de forma recursiva y no permite la desparticipación selectiva. Normalmente, solo las carpetas sin subcarpetas o con una jerarquía muy superficial, como un nivel de subcarpeta, deben considerarse para el uso compartido.
* **Separe las carpetas para un uso compartido unidireccional:** Las carpetas independientes deben usarse para compartir recursos finales de [!DNL Assets] a [!DNL Creative Cloud] archivos y para compartir recursos listos para creativos desde [!DNL Creative Cloud] archivos a [!DNL Assets]. Junto con una buena convención de nombres para estas carpetas, crea un entorno de trabajo más fácil de entender para [!DNL Assets] y [!DNL Creative Cloud] usuarios por igual.
* **Evite WIP en la carpeta compartida:** La carpeta compartida no debe utilizarse para el trabajo en curso (utilice una carpeta independiente en los archivos de Creative Cloud para llevar a cabo un trabajo que requiera cambios frecuentes en el archivo).
* **Inicie un nuevo trabajo fuera de la carpeta compartida:** Los nuevos diseños (archivos creativos) deben iniciarse en la carpeta WIP independiente en los archivos Creative Cloud y cuando estén listos para compartirse con [!DNL Assets] Los usuarios de deben moverse o guardarse en la carpeta compartida.
* **Simplifique la estructura de uso compartido:** Para una configuración operativa más manejable, piense en simplificar la estructura de uso compartido. En lugar de compartir con todos los usuarios creativos, [!DNL Assets] las carpetas solo deben compartirse con los representantes del equipo, como un director creativo o un administrador de equipos. El administrador del lado creativo recibiría los recursos finales, decidiría las asignaciones de trabajo y, a continuación, permitiría a los diseñadores trabajar en sus propias cuentas de Creative Cloud en los recursos de trabajo en curso. Pueden utilizar funciones de colaboración de Creative Cloud para coordinar el trabajo y, finalmente, seleccionar y colocar recursos que estén listos para volver a compartirse con [!DNL Assets] en su carpeta compartida lista para creativos.

El diagrama siguiente ilustra una configuración de ejemplo para crear nuevos diseños basada en los recursos finales existentes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
