---
title: AEM Configurar formularios para recuperar previamente información de dominio
description: AEM Configure formularios para recuperar previamente información de dominio si experimenta un tiempo de respuesta más lento debido a grupos profundamente anidados o si es miembro de muchos grupos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# AEM Configurar formularios para recuperar previamente información de dominio {#configure-aem-forms-to-prefetchdomain-information}

Los usuarios pueden experimentar un tiempo de respuesta más lento si pertenecen a muchos grupos (por ejemplo, 500 o más) o si los grupos están profundamente anidados (por ejemplo, 30 niveles). AEM Si tiene este problema, puede configurar los formularios de la para recuperar previamente información de ciertos dominios.

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

   En este ejemplo, se configuran varios dominios para la recuperación previa. Los nombres de dominio están separados por &quot;/&quot;. Esto se muestra en el ejemplo anterior con *Nombre_de_dominio1*, *Domain_Name2*, y *Domain_Name3*.

1. Para importar el archivo actualizado, en Administración de usuarios, haga clic en **[!UICONTROL Configuración > Importar Y Exportar Archivos De Configuración]**.
1. Clic **[!UICONTROL Examinar]** para buscar el archivo, haga clic en Importar y, a continuación, en **[!UICONTROL OK]**.
