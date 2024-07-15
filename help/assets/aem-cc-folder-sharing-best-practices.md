---
title: Uso compartido de carpetas en  [!DNL Adobe Creative Cloud] prácticas recomendadas
description: Configure [!DNL Adobe Experience Manager] para permitir que los usuarios de [!DNL Experience Manager Assets] puedan intercambiar carpetas con los usuarios de Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 0%

---

# Compartir carpetas de [!DNL Adobe Experience Manager] a [!DNL Adobe Creative Cloud] {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La característica de uso compartido de carpetas de [!DNL Experience Manager] a [!DNL Creative Cloud] está en desuso. Adobe recomienda usar funcionalidades más recientes, como [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) o [aplicación de escritorio para Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Obtenga más información en [Prácticas recomendadas para la integración de Experience Manager y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] se puede configurar para permitir que los usuarios de [!DNL Assets] compartan carpetas con los usuarios de las aplicaciones [!DNL Adobe Creative Cloud], de modo que estén disponibles como carpetas compartidas en el servicio de recursos de [!DNL Adobe Creative Cloud]. La característica se puede usar para intercambiar archivos entre los equipos creativos y los usuarios de [!DNL Assets], especialmente cuando los usuarios creativos no tienen acceso a la implementación de [!DNL Assets] (no están en la red empresarial).

Este tipo de integración se puede usar en los siguientes casos de uso, especialmente cuando se trabaja con usuarios que no tienen acceso directo a [!DNL Assets]:

* [!DNL Assets] usuarios comparten un conjunto de recursos digitales específicos con usuarios de [!DNL Adobe Creative Cloud] archivos (por ejemplo, un informe creativo y un conjunto de recursos aprobados para el trabajo de diseño de una nueva actividad de marketing).
* [!DNL Assets] usuarios reciben nuevos archivos creados por [!DNL Adobe Creative Cloud] usuarios de la aplicación.

>[!NOTE]
>
>Antes de leer este documento, puede revisar las [prácticas recomendadas generales de integración de Experience Manager y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) para obtener una descripción general de la integración.

## Información general {#overview}

El uso compartido de carpetas de [!DNL Experience Manager] a [!DNL Creative Cloud] se basa en el uso compartido de carpetas y archivos del lado del servidor entre las cuentas de [!DNL Assets] y [!DNL Creative Cloud]. Los profesionales creativos que usen la aplicación de escritorio [!DNL Creative Cloud] en sus escritorios también pueden hacer que las carpetas compartidas estén disponibles directamente en sus discos con la tecnología [!DNL Adobe CreativeSync].

En el diagrama siguiente se proporciona una descripción general de la integración.

![chlimage_1-179](assets/chlimage_1-406.png)

La integración incluye los siguientes elementos:

* **[!DNL Experience Manager Assets]** implementado en la red empresarial (Managed Services o local): el uso compartido de carpetas se inició aquí.
* **[!DNL Adobe Experience Cloud Assets]servicio principal**: actúa como intermediario entre [!DNL Experience Manager] y [!DNL Creative Cloud] servicios de almacenamiento. Un administrador de una organización que utiliza la integración debe establecer una relación de confianza entre la organización Experience Cloud y la implementación [!DNL Assets]. También [definen una lista de colaboradores de Creative Cloud aprobados](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html), a los que [!DNL Assets] usuarios pueden compartir carpetas para mayor seguridad.

* **[!DNL Creative Cloud]servicios web de Assets** (interfaz de usuario web de archivos de almacenamiento y [!DNL Creative Cloud]): aquí es donde los usuarios de la aplicación Creative Cloud específicos, con los que se compartió una carpeta [!DNL Assets], podrían aceptar la invitación y ver la carpeta en el almacenamiento de su cuenta de Creative Cloud.
* **aplicación de escritorio de Creative Cloud**: (opcional) permite el acceso directo a archivos o carpetas compartidos desde el escritorio del usuario creativo mediante la sincronización con el almacenamiento de Assets de [!DNL Creative Cloud].

## Características y limitaciones {#characteristics-and-limitations}

* **Propagación unidireccional de cambios:** Los cambios de archivo se propagan en una sola dirección: desde el sistema ([!DNL Experience Manager] o [!DNL Creative Cloud Assets]), donde se creó (cargó) originalmente el recurso. La integración no proporciona una sincronización bidireccional y completamente automatizada entre los dos sistemas.
* **Versiones:**

   * [!DNL Experience Manager] solo crea versiones de un recurso en las actualizaciones si el archivo se originó en [!DNL Experience Manager] y se actualiza allí.
   * [!DNL Creative Cloud] Assets proporciona su propia [característica de control de versiones](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) dirigida a las actualizaciones de Work in Progress (básicamente, almacena las actualizaciones durante un máximo de diez días)

* **Limitaciones de espacio:** Los tamaños y volúmenes de los archivos intercambiados están limitados por la [cuota de Assets de Creative Cloud](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) específica para usuarios creativos (depende del nivel de suscripción) y una limitación del tamaño máximo de archivo de 5 GB. El espacio también está limitado por la cuota de recursos que la organización tiene en el servicio principal de Adobe Experience Cloud Assets.

* **Requisitos de espacio:** Los archivos de las carpetas compartidas también deben almacenarse físicamente en [!DNL Experience Manager] y, a continuación, en la cuenta de [!DNL Creative Cloud], con una copia en caché en el servicio principal [!DNL Experience Cloud Assets].
* **Red y ancho de banda:** Los archivos de las carpetas compartidas y todas las actualizaciones deben transportarse a través de la red entre los sistemas. Asegúrese de que solo se comparten los archivos y las actualizaciones relevantes.
* **Tipo de carpeta**: no se admite el uso compartido de una carpeta [!DNL Assets] del tipo `sling:OrderedFolder` en el contexto del uso compartido en [!DNL Adobe Experience Cloud]. Si desea compartir una carpeta, al crearla en [!DNL Assets], no seleccione la opción [!UICONTROL Ordenado].

## Prácticas recomendadas {#best-practices}

Las prácticas recomendadas para usar el uso compartido de carpetas de [!DNL Experience Manager] a [!DNL Creative Cloud] incluyen:

* **Consideraciones sobre el volumen:** [!DNL Experience Manager] y [!DNL Creative Cloud] El uso compartido de carpetas debe usarse para compartir un número menor de archivos, por ejemplo, relevantes para una campaña o actividad específica. Para compartir conjuntos de recursos más grandes, como todos los recursos aprobados de la organización, use otros métodos de distribución (por ejemplo, [!DNL Assets Brand Portal]) o la aplicación de escritorio [!DNL Experience Manager].
* **Evite compartir jerarquías profundas:** El uso compartido funciona de forma recursiva y no permite el uso compartido selectivo. Normalmente, solo se deben tener en cuenta para el uso compartido las carpetas sin subcarpetas o con una jerarquía superficial, como un nivel de subcarpeta.
* **Carpetas independientes para uso compartido unidireccional:** Las carpetas independientes deben usarse para compartir recursos finales de [!DNL Assets] a [!DNL Creative Cloud] archivos y para compartir recursos listos para la creatividad de [!DNL Creative Cloud] archivos a [!DNL Assets]. Junto con una buena convención de nombres para estas carpetas, crea un entorno de trabajo más fácil de entender para los usuarios de [!DNL Assets] y [!DNL Creative Cloud] por igual.
* **Evitar trabajo en curso en la carpeta compartida:** No utilice una carpeta compartida para Trabajo en curso: utilice una carpeta independiente en Archivos de Creative Cloud para realizar trabajos que requieran cambios frecuentes en el archivo.
* **Iniciar nuevo trabajo fuera de la carpeta compartida:** Los nuevos diseños (archivos creativos) deben iniciarse en la carpeta WIP independiente en Archivos de Creative Cloud y, cuando estén listos para compartirse con los usuarios de [!DNL Assets], deben moverse o guardarse en la carpeta compartida.
* **Simplificar la estructura de uso compartido:** Para una configuración operativa más manejable, piense en simplificar la estructura de uso compartido. En lugar de compartir con todos los usuarios creativos, las carpetas de [!DNL Assets] deben compartirse únicamente con los representantes del equipo, como un director creativo o un administrador de equipo. El administrador del lado creativo recibiría los recursos finales, decidiría las asignaciones de trabajo y, a continuación, permitiría a los diseñadores trabajar en sus propias cuentas de Creative Cloud en los recursos de WIP. Pueden usar características de colaboración de Creative Cloud para coordinar el trabajo y, finalmente, seleccionar y colocar los recursos que estén listos para compartirse en [!DNL Assets] en su carpeta compartida lista para la creatividad.

El diagrama siguiente ilustra un ejemplo de configuración para crear diseños basados en recursos finales existentes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
