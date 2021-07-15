---
title: Instalación del paquete de características 18912 para la migración masiva de recursos
description: El paquete de funciones 18912 le permite ingerir recursos de forma masiva mediante FTP o migrar recursos de Dynamic Media Classic a Dynamic Media en Adobe Experience Manager. Este feature pack opcional está disponible en la asistencia de Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Administración de activos
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Instalación del paquete de características 18912 para la migración masiva de recursos{#installing-feature-pack-for-bulk-asset-migration}

La instalación del paquete de características 18912 es *opcional*.

El paquete de funciones 18912 le permite ingerir recursos de forma masiva directamente en Dynamic Media: modo Scene7 en Adobe Experience Manager mediante FTP. También le permite migrar recursos de Dynamic Media Classic a Dynamic Media - modo Scene7 en el Experience Manager. El paquete de funciones está disponible en [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>Es posible que use el paquete de funciones para migrar de forma masiva los recursos por su cuenta de Dynamic Media Classic a Dynamic Media: modo Scene7 en Experience Manager. También puede migrar de forma masiva recursos mediante la función FTP de Dynamic Media Classic. Sin embargo, Adobe recomienda *no* que utilice cualquiera de estos métodos debido a la complejidad involucrada.
>
>Como tal, este paquete de características de migración *solo* se admite como parte de un proyecto de migración cuando se realiza mediante [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Antes de instalar el paquete de funciones, cree un usuario de servicio y proporcione esa información al servicio de asistencia técnica de Adobe.

Consulte también [Configuración de Dynamic Media - modo Scene7](/help/assets/config-dms7.md).

**Para instalar el paquete de características 18912 para la migración masiva de recursos:**

1. En la instancia de Experience Manager, vaya a **[!UICONTROL Herramienta]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]** y seleccione **[!UICONTROL Crear usuario]**. Este usuario de servicio debe tener *permisos de lectura/escritura* para `/content/dam.`
1. En los campos **[!UICONTROL ID]** y **[!UICONTROL Password]**, introduzca un nombre de usuario y una contraseña; por ejemplo, **FTP User**. Este nombre aparece en la cronología como el usuario que creó el recurso. Cuando se carga un recurso desde FTP, se considera creado cuando se carga en el servidor FTP y se envía al Experience Manager.
1. Póngase en contacto con el [Servicio de atención al cliente de Adobe Enterprise para que el Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) solicite acceso al paquete de funciones 18912 para descargarlo. Es posible que necesite la siguiente información cuando contacte con el servicio de asistencia técnica:

   * Dirección IP del servidor para la instancia de Autor, incluido el número de puerto (de forma predeterminada, el número de puerto es 4502).
   * nombre de usuario y contraseña del servicio de Experience Manager del paso anterior.

1. El Servicio de atención al cliente de Adobe Enterprise para Experience Manager le proporciona las credenciales de FTP y acceso al paquete de funciones 18912.
1. Cuando reciba el paquete de características 18912, instálelo.

   Consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md) para obtener más información sobre el uso de la distribución de software y los paquetes en el Experience Manager.
