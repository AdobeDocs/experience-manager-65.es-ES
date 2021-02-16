---
title: Instalación del paquete de funciones 18912 para la migración masiva de recursos
description: El paquete de funciones 18912 le permite realizar ingestas masivas de recursos mediante FTP o migrar recursos de Dynamic Media Classic a Dynamic Media en AEM. Este paquete de funciones opcional está disponible en la compatibilidad con Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: d6ae8bffa2d9d59f5656b9344d8826128f12885c
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Instalación del paquete de funciones 18912 para la migración masiva de recursos{#installing-feature-pack-for-bulk-asset-migration}

La instalación del paquete de funciones 18912 es *opcional*.

El paquete de funciones 18912 le permite realizar ingestas masivas de recursos directamente en Dynamic Media, en modo Scene7 en AEM mediante FTP, o migrar recursos de Dynamic Media Classic a Dynamic Media, en modo Scene7 en AEM. El paquete de funciones está disponible en [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

>[!NOTE]
>
>Aunque es posible utilizar el paquete de funciones para migrar recursos por su cuenta de forma masiva del modo Dynamic Media Classic al modo Dynamic Media - Scene 7 en AEM o migrar recursos de forma masiva mediante la función de FTP de Dynamic Media Classic, Adobe *no* recomienda este método debido a la complejidad que implica.
>
>Por lo tanto, los paquetes de funciones de migración, como éste, sólo se *admiten como parte de un proyecto de migración cuando se realizan mediante [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).*

Antes de instalar el paquete de funciones, primero debe crear un usuario de servicios y proporcionar esa información al servicio de asistencia de Adobe.

Consulte también [Configuración de Dynamic Media - modo Scene7](/help/assets/config-dms7.md).

**Para instalar el paquete de funciones 18912 para la migración masiva de recursos**

1. En la instancia de AEM, vaya a **[!UICONTROL Herramientas > Seguridad > Usuarios]** y seleccione **[!UICONTROL Crear usuario]**. Este usuario de servicio debe tener *permisos de lectura/escritura* para `/content/dam.`
1. En los campos **[!UICONTROL ID]** y **[!UICONTROL Contraseña]**, introduzca un nombre de usuario y una contraseña; por ejemplo, **Usuario de FTP**. Este nombre aparece en la línea de tiempo como el usuario que creó el recurso. Cuando se carga un recurso desde FTP, se considera que se crea al cargarlo en el servidor FTP y se transfiere a AEM.
1. Póngase en contacto con [Servicio de atención al cliente empresarial de Adobe para obtener Experience Manager](https://helpx.adobe.com/es/contact/enterprise-support.ec.html) para solicitar acceso al paquete de funciones 18912 para descargarlo. Es posible que necesite la siguiente información cuando se ponga en contacto con la asistencia técnica:

   * Dirección IP del servidor para la instancia de Autor, incluido el número de puerto (de forma predeterminada, el número de puerto es 4502).
   * Nombre de usuario y contraseña del usuario del servicio de AEM del paso anterior.

1. El Servicio de atención al cliente de Adobe Enterprise para AEM le proporciona las credenciales de FTP y acceso al paquete de funciones 18912.
1. Cuando reciba el paquete de funciones 18912, instálelo.

   Consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md) para obtener más información sobre el uso de distribución de software y paquetes en AEM.
