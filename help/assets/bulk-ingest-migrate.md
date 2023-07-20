---
title: Instalación del paquete de funciones 18912 para la migración masiva de recursos
description: El paquete de funciones 18912 permite realizar ingestas masivas de recursos a través de FTP, o migrar recursos de Dynamic Media Classic a Dynamic Media en Adobe Experience Manager. Este paquete de funciones opcional está disponible en la asistencia para Adobes.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: fc148a5f5e0fcaac2980dc73004fa92ac3b91fb3
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---

# Instalación del paquete de funciones 18912 para la migración masiva de recursos{#installing-feature-pack-for-bulk-asset-migration}

La instalación del paquete de funciones 18912 es *opcional*.

El paquete de funciones 18912 permite la ingesta masiva de recursos directamente en el modo Dynamic Media - Scene7 en Adobe Experience Manager a través del FTP. También le permite migrar recursos de Dynamic Media Classic al modo Dynamic Media - Scene7 en Experience Manager. El paquete de funciones está disponible en [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>Puede utilizar el paquete de funciones para migrar recursos en lote por su cuenta desde Dynamic Media Classic al modo Dynamic Media - Scene7 en Experience Manager. También puede migrar recursos en lote mediante la función FTP de Dynamic Media Classic. Sin embargo, el Adobe sí *no* le recomendamos que utilice cualquiera de estos métodos debido a la complejidad que implica.
>
>Como tal, este paquete de funciones de migración es *solamente* se admite como parte de un proyecto de migración cuando se realiza mediante [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Antes de instalar el paquete de funciones, cree un usuario de servicio y proporcione esa información al servicio de asistencia de Adobe.

Consulte también [Configuración de Dynamic Media: Modo Scene7](/help/assets/config-dms7.md).

**Para instalar el paquete de funciones 18912 para la migración masiva de recursos:**

1. En la instancia de Experience Manager, vaya a **[!UICONTROL Herramienta]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]** y seleccione **[!UICONTROL Crear usuario]**. Este usuario de servicio debe tener *lectura/escritura* permisos para `/content/dam.`
1. En el **[!UICONTROL ID]** y **[!UICONTROL Contraseña]** , introduzca un nombre de usuario y una contraseña; por ejemplo, **Usuario de FTP**. Este nombre aparece en la cronología como el usuario que creó el recurso. Cuando se carga un recurso desde FTP, se considera que un recurso se ha creado cuando se carga en el servidor FTP y se inserta en el Experience Manager.
1. Contacto [Adobe Asistencia al cliente para Experience Manager](https://experienceleague.adobe.com/?support-solution=General&amp;lang=es#support) para solicitar acceso al paquete de funciones 18912 para la descarga. Es posible que necesite la siguiente información cuando contacte con el servicio de asistencia:

   * Dirección IP del servidor para la instancia de autor, incluido el número de puerto (de forma predeterminada, el número de puerto es 4502).
   * Nombre de usuario y contraseña de usuario del servicio de Experience Manager del paso anterior.

1. Asistencia al cliente de Adobe para Experience Manager le proporciona las credenciales de FTP y acceso al paquete de funciones 18912.
1. Cuando reciba el paquete de funciones 18912, instálelo.

   Consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md) para obtener más información sobre el uso de Distribución de software y paquetes en Experience Manager.
