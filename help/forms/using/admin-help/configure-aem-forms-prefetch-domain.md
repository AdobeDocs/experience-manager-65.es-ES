---
title: Configuración de AEM formularios para recuperar previamente información de dominio
seo-title: Configure AEM forms to prefetchdomain information
description: Configure AEM formularios para recuperar previamente la información del dominio si experimenta un tiempo de respuesta más lento debido a grupos profundamente anidados o si es miembro de muchos grupos.
seo-description: Configure AEM forms to prefetch domain information if you experience a slower response time due to deeply nested groups or if you are a member of many groups.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Configuración de AEM formularios para recuperar previamente información de dominio {#configure-aem-forms-to-prefetchdomain-information}

Los usuarios pueden experimentar un tiempo de respuesta más lento si pertenecen a muchos grupos (por ejemplo, 500 o más) o si los grupos están anidados en profundidad (por ejemplo, 30 niveles). Si tiene este problema, puede configurar AEM formularios para recuperar previamente información de ciertos dominios.

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración De Usuarios > Configuración > Importar Y Exportar Archivos De Configuración]**.
1. Para exportar la configuración actual a un archivo, haga clic en **[!UICONTROL Exportar]** y guarde el archivo de configuración en otra ubicación.
1. Añada el siguiente nodo (marcado en negrita):

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   En este ejemplo, se configuran varios dominios para la recuperación previa. Los nombres de dominio están separados por &quot;/&quot;. Esto se muestra en el ejemplo anterior con *Domain_Name1*, *Domain_Name2* y *Domain_Name3*.

1. Para importar el archivo actualizado, en Administración de usuarios, haga clic en **[!UICONTROL Configuración > Importar Y Exportar Archivos De Configuración]**.
1. Haga clic en **[!UICONTROL Examinar]** para buscar el archivo, haga clic en Importar y, a continuación, haga clic en **[!UICONTROL OK]**.
