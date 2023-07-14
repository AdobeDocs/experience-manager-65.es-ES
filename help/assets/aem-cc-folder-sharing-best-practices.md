---
title: Compartir carpetas en [!DNL Adobe Creative Cloud] prácticas recomendadas
description: Configurar [!DNL Adobe Experience Manager] para permitir el ingreso de usuarios [!DNL Experience Manager Assets] para intercambiar carpetas con usuarios de Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] hasta [!DNL Adobe Creative Cloud] compartir carpetas {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>El [!DNL Experience Manager] hasta [!DNL Creative Cloud] La función de uso compartido de carpetas está obsoleta. El Adobe recomienda utilizar funciones más nuevas, como [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) o [aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Obtenga más información en [Prácticas recomendadas de integración de Experience Manager y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] se puede configurar para permitir a los usuarios [!DNL Assets] para compartir carpetas con los usuarios de [!DNL Adobe Creative Cloud] aplicaciones, por lo que están disponibles como carpetas compartidas en la [!DNL Adobe Creative Cloud] servicio de recursos. La función se puede utilizar para intercambiar archivos entre equipos creativos y [!DNL Assets] usuarios, especialmente cuando los usuarios creativos no tienen acceso a la [!DNL Assets] implementación (no están en la red de la empresa).

Este tipo de integración se puede utilizar en los siguientes casos de uso, especialmente cuando se trabaja con usuarios que no tienen acceso directo a [!DNL Assets]:

* [!DNL Assets] Los usuarios de comparten un conjunto de recursos digitales específicos con los usuarios de [!DNL Adobe Creative Cloud] archivos (por ejemplo, una descripción creativa y un conjunto de recursos aprobados para el trabajo de diseño de una nueva actividad de marketing).
* [!DNL Assets] los usuarios reciben los nuevos archivos creados por [!DNL Adobe Creative Cloud] usuarios de la aplicación.

>[!NOTE]
>
>Antes de leer este documento, puede revisar el [Prácticas recomendadas de integración de Experience Manager y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) para obtener una descripción general de la integración.

## Información general {#overview}

[!DNL Experience Manager] hasta [!DNL Creative Cloud] el uso compartido de carpetas se basa en el uso compartido de carpetas y archivos entre [!DNL Assets] y [!DNL Creative Cloud] cuentas. Profesionales creativos que utilizan el [!DNL Creative Cloud] aplicación de escritorio en sus escritorios, también puede hacer que las carpetas compartidas estén disponibles directamente en sus discos utilizando [!DNL Adobe CreativeSync] tecnología.

En el diagrama siguiente se proporciona una descripción general de la integración.

![chlimage_1-179](assets/chlimage_1-406.png)

La integración incluye los siguientes elementos:

* **[!DNL Experience Manager Assets]** implementado en la red empresarial (Managed Services o local): el uso compartido de carpetas se inicia aquí.
* **[!DNL Adobe Experience Cloud Assets]servicio principal**: actúa como intermediario entre [!DNL Experience Manager] y [!DNL Creative Cloud] servicios de almacenamiento. Un administrador de una organización que utiliza la integración debe establecer una relación de confianza entre la organización Experience Cloud y el administrador [!DNL Assets] implementación. También incluyen [definir una lista de colaboradores de Creative Cloud aprobados](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html), que [!DNL Assets] Los usuarios de también pueden compartir carpetas para mayor seguridad.

* **[!DNL Creative Cloud]Servicios web de Assets** (almacenamiento y [!DNL Creative Cloud] archivos (IU web): Aquí es donde los usuarios específicos de la aplicación Creative Cloud, con los que [!DNL Assets] se ha compartido la carpeta, podría aceptar la invitación y ver la carpeta en su almacenamiento de cuenta de Creative Cloud.
* **aplicación de escritorio de Creative Cloud**: (opcional) permite el acceso directo a carpetas y archivos compartidos desde el escritorio del usuario creativo mediante la sincronización con [!DNL Creative Cloud] Almacenamiento de recursos.

## Características y limitaciones {#characteristics-and-limitations}

* **Propagación unidireccional de cambios:** Los cambios de archivo se propagan en una sola dirección: desde el sistema ([!DNL Experience Manager] o [!DNL Creative Cloud Assets]), donde el recurso se creó (cargó) originalmente. La integración no proporciona una sincronización bidireccional y completamente automatizada entre los dos sistemas.
* **Versiones:**

   * [!DNL Experience Manager] solo crea versiones de un recurso en las actualizaciones si el archivo se originó en [!DNL Experience Manager] y se actualiza allí.
   * [!DNL Creative Cloud] Assets proporciona sus propios recursos [función de versiones](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) que se dirige a las actualizaciones de Work in Progress (básicamente, almacena actualizaciones durante un máximo de diez días)

* **Limitaciones de espacio:** Los tamaños y volúmenes de los archivos intercambiados están limitados por el [Cuota de recursos del Creative Cloud](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) para usuarios creativos (depende del nivel de suscripción) y una limitación de 5 GB de tamaño máximo de archivo. El espacio también está limitado por la cuota de recursos que la organización tiene en el servicio principal de Adobe Experience Cloud Assets.

* **Requisitos de espacio:** Los archivos de las carpetas compartidas también deben almacenarse físicamente en [!DNL Experience Manager] y luego en [!DNL Creative Cloud] cuenta, con una copia en caché en [!DNL Experience Cloud Assets] servicio principal.
* **Redes y ancho de banda:** Los archivos de las carpetas compartidas y todas las actualizaciones deben transportarse a través de la red entre los sistemas. Asegúrese de que solo se comparten los archivos y las actualizaciones relevantes.
* **Tipo de carpeta**: compartiendo un [!DNL Assets] carpeta del tipo `sling:OrderedFolder`, no es compatible en el contexto del uso compartido en [!DNL Adobe Experience Cloud]. Si desea compartir una carpeta, al crearla en [!DNL Assets], no seleccione la opción [!UICONTROL Ordenado] opción.

## Prácticas recomendadas {#best-practices}

Prácticas recomendadas para usar [!DNL Experience Manager] hasta [!DNL Creative Cloud] compartir carpetas incluye:

* **Consideraciones sobre el volumen:** [!DNL Experience Manager] y [!DNL Creative Cloud] El uso compartido de carpetas debe utilizarse para compartir un número menor de archivos, por ejemplo, relevantes para una campaña o actividad específica. Para compartir conjuntos de recursos más grandes, como todos los recursos aprobados de la organización, utilice otros métodos de distribución (por ejemplo, [!DNL Assets Brand Portal]) o [!DNL Experience Manager] aplicación de escritorio.
* **Evite compartir jerarquías profundas:** El uso compartido funciona de forma recursiva y no permite el uso compartido selectivo. Normalmente, solo se deben tener en cuenta para el uso compartido las carpetas sin subcarpetas o con una jerarquía superficial, como un nivel de subcarpeta.
* **Separe las carpetas para compartir en un solo sentido:** Se deben usar carpetas independientes para compartir los recursos finales de [!DNL Assets] hasta [!DNL Creative Cloud] archivos y para compartir recursos listos para la creatividad desde [!DNL Creative Cloud] archivos a [!DNL Assets]. Junto con una buena convención de nombres para estas carpetas, crea un entorno de trabajo más fácil de entender para [!DNL Assets] y [!DNL Creative Cloud] usuarios por igual.
* **Evitar WIP en la carpeta compartida:** La carpeta compartida no debe utilizarse para Trabajo en curso: utilice una carpeta independiente en Archivos de Creative Cloud para realizar trabajos que requieran cambios frecuentes en el archivo.
* **Iniciar nuevo trabajo fuera de la carpeta compartida:** Los nuevos diseños (archivos creativos) deben iniciarse en la carpeta independiente WIP en Archivos de Creative Cloud y cuando estén listos para compartirse con [!DNL Assets] usuarios, deben moverse o guardarse en la carpeta compartida.
* **Simplifique la estructura de uso compartido:** Para una configuración operativa más manejable, piense en simplificar la estructura de uso compartido. En lugar de compartir con todos los usuarios creativos, [!DNL Assets] las carpetas solo deben compartirse con los representantes del equipo, como un director creativo o un administrador de equipo. El administrador del lado creativo recibiría los recursos finales, decidiría las asignaciones de trabajo y, a continuación, permitiría a los diseñadores trabajar en sus propias cuentas de Creative Cloud en los recursos de WIP. Pueden utilizar funciones de colaboración Creative Cloud para coordinar el trabajo y, finalmente, seleccionar y colocar los recursos listos para compartir en [!DNL Assets] en su carpeta compartida lista para la creación.

El diagrama siguiente ilustra un ejemplo de configuración para crear diseños basados en recursos finales existentes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
