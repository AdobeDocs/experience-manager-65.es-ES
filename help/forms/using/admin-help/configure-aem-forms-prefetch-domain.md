---
title: Configuración de formularios AEM para recuperar previamente información de dominio
seo-title: Configuración de formularios AEM para recuperar previamente información de dominio
description: Configure los formularios AEM para recuperar previamente la información del dominio si experimenta un tiempo de respuesta más lento debido a grupos profundamente anidados o si es miembro de muchos grupos.
seo-description: Configure los formularios AEM para recuperar previamente la información del dominio si experimenta un tiempo de respuesta más lento debido a grupos profundamente anidados o si es miembro de muchos grupos.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de formularios AEM para recuperar previamente información de dominio {#configure-aem-forms-to-prefetchdomain-information}

Los usuarios pueden experimentar un tiempo de respuesta más lento si pertenecen a muchos grupos (por ejemplo, 500 o más) o si los grupos están anidados profundamente (por ejemplo, 30 niveles). Si tiene este problema, puede configurar formularios AEM para recuperar previamente información de determinados dominios.

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Configuración > Importar y exportar archivos]** de configuración.
1. Para exportar la configuración actual a un archivo, haga clic en **[!UICONTROL Exportar]** y guarde el archivo de configuración en otra ubicación.
1. Agregue el nodo siguiente (marcado en negrita):

   ```as3
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

1. Para importar el archivo actualizado, en Administración de usuarios, haga clic en **[!UICONTROL Configuración > Importar y exportar archivos]** de configuración.
1. Haga clic en **[!UICONTROL Examinar]** para buscar el archivo, haga clic en Importar y, a continuación, en **[!UICONTROL Aceptar]**.

