---
title: Instalación del paquete de características 18912 para la migración masiva de recursos
description: El paquete de funciones 18912 le permite ingerir recursos de forma masiva mediante FTP o migrar recursos de Dynamic Media Classic a Dynamic Media en AEM. Este feature pack opcional está disponible en la asistencia de Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Administración de activos
role: Profesional empresarial, administrador
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Instalación del paquete de características 18912 para la migración masiva de recursos{#installing-feature-pack-for-bulk-asset-migration}

La instalación del paquete de características 18912 es *opcional*.

El paquete de funciones 18912 le permite ingerir recursos de forma masiva directamente en Dynamic Media (modo Scene7 en AEM mediante FTP) o migrar recursos de Dynamic Media Classic a Dynamic Media (modo Scene7 en AEM). El paquete de funciones está disponible en [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

>[!NOTE]
>
>Aunque es posible utilizar el paquete de funciones para migrar de forma masiva recursos por su cuenta de Dynamic Media Classic a Dynamic Media - Scene 7 en modo AEM o para migrar de forma masiva recursos mediante la función FTP en Dynamic Media Classic, Adobe recomienda este método *no* debido a la complejidad implicada.
>
>De este modo, los paquetes de funciones de migración, como este, *solo* se admiten como parte de un proyecto de migración cuando se realizan mediante [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Antes de instalar el paquete de funciones, primero debe crear un usuario de servicio y proporcionar esa información al servicio de asistencia técnica de Adobe.

Consulte también [Configuración de Dynamic Media - Modo Scene7](/help/assets/config-dms7.md).

**Para instalar el paquete de características 18912 para la migración masiva de recursos**

1. En la instancia de AEM, vaya a **[!UICONTROL Tools > Security > Users]** y seleccione **[!UICONTROL Create User]**. Este usuario de servicio debe tener *permisos de lectura/escritura* para `/content/dam.`
1. En los campos **[!UICONTROL ID]** y **[!UICONTROL Password]**, introduzca un nombre de usuario y una contraseña; por ejemplo, **FTP User**. Este nombre aparece en la cronología como el usuario que creó el recurso. Cuando se carga un recurso desde FTP, se considera creado cuando se carga en el servidor FTP y se AEM.
1. Póngase en contacto con el [Servicio de atención al cliente de Adobe Enterprise para que el Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) solicite acceso al paquete de funciones 18912 para descargarlo. Es posible que necesite la siguiente información cuando contacte con el servicio de asistencia técnica:

   * Dirección IP del servidor para la instancia de Autor, incluido el número de puerto (de forma predeterminada, el número de puerto es 4502).
   * AEM nombre de usuario y contraseña del servicio del paso anterior.

1. El Servicio de atención al cliente de Adobe Enterprise para AEM le proporciona las credenciales de FTP y acceso al paquete de funciones 18912.
1. Cuando reciba el paquete de características 18912, instálelo.

   Consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md) para obtener más información sobre el uso de la distribución de software y los paquetes en AEM.
