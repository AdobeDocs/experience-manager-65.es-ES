---
title: Administrar [!DNL Adobe Stock] recursos
description: Busque, busque, licencie y administre [!DNL Adobe Stock] recursos desde  [!DNL Adobe Experience Manager]. Utilice los recursos con licencia como cualquier otro recurso digital.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 13%

---


# Utilizar [!DNL Adobe Stock] recursos en [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

Las organizaciones pueden integrar su [!DNL Adobe Stock] plan empresarial con [!DNL Experience Manager Assets] para garantizar que los activos con licencia estén ampliamente disponibles para sus proyectos creativos y de mercadotecnia, con las poderosas capacidades de administración de activos de [!DNL Experience Manager].

[!DNL Adobe Stock]El servicio proporciona a diseñadores y empresas acceso a millones de fotos, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, verificados y libres de derechos de autor para todos sus proyectos creativos. [!DNL Experience Manager] los usuarios pueden buscar, previsualización y obtener licencias rápidamente de  [!DNL Adobe Stock] los recursos guardados en  [!DNL Experience Manager], sin salir de la  [!DNL Experience Manager] interfaz.

## Requisitos previos {#prerequisites}

La integración requiere un [plan [!DNL Adobe Stock] de empresa](https://stockenterprise.adobe.com/).

## Integrar [!DNL Experience Manager] y [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Para permitir la comunicación entre [!DNL Experience Manager] y [!DNL Adobe Stock], cree una configuración IMS y una configuración [!DNL Adobe Stock] en [!DNL Experience Manager].

>[!NOTE]
>
>Solo los administradores [!DNL Experience Manager] y [!DNL Admin Console] administradores de una organización pueden realizar la integración ya que requiere privilegios de administrador.

### Crear una configuración de IMS {#create-an-ims-configuration}

1. En la interfaz de usuario [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**. Haga clic en **[!UICONTROL Crear]** y seleccione **[!UICONTROL Solución de nube]** > **[!UICONTROL Adobe Stock]**.
1. Vuelva a utilizar un certificado existente o seleccione **[!UICONTROL Crear nuevo certificado]**.
1. Haga clic en **[!UICONTROL Crear certificado]**. Una vez creada, descargue la clave pública. Haga clic en **[!UICONTROL Siguiente]**. 
1. Añada la clave pública descargada en su cuenta de [!DNL Adobe Developer Console] servicio. Haga clic en **[!UICONTROL Siguiente]**. Deje abierta la pantalla [!UICONTROL Configuración de cuenta técnica de IMS de Adobe] para proporcionar los valores en breve.
1. Acceda a [Adobe Developer Console](https://console.adobe.io). Asegúrese de que su cuenta tenga permisos de administrador para la organización para la que se requiere la integración.
1. Haga clic en **[!UICONTROL Crear nuevo proyecto]** y haga clic en **[!UICONTROL Añadir API]**. Seleccione **[!UICONTROL Adobe Stock]** en la lista de las API disponibles para usted. Seleccione [!UICONTROL OAUTH 2.0 Web]. Configure y copie los distintos valores presentados.
1. En [!DNL Experience Manager] proporcione los valores en los campos titulados **[!UICONTROL Título]**, **[!UICONTROL Servidor de autorización]**, **[!UICONTROL Clave de API]**, **[!UICONTROL Secreto del cliente]** y **[!UICONTROL Carga útil]**. Consulte [inicio rápido de autenticación JWT](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md) para obtener información detallada sobre estos valores.

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Crear configuración [!DNL Adobe Stock] en [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Haga clic en **[!UICONTROL Crear]** para crear una configuración y asociarla con la configuración de IMS existente. Seleccione `PROD` como parámetro de entorno.
1. En el campo **[!UICONTROL Ruta de acceso de recursos con licencia]**, deje una ubicación tal cual. No cambie la ubicación donde desee almacenar los [!DNL Adobe Stock] recursos.
1. Complete la creación agregando todas las propiedades necesarias. Haga clic en **[!UICONTROL Guardar y cerrar]**.
1. Añada [!DNL Experience Manager] usuarios o grupos, que pueden obtener licencias para los recursos.

>[!NOTE]
>
>Si hay varias configuraciones [!DNL Adobe Stock], seleccione la configuración que desee en el panel [!UICONTROL Preferencias del usuario]. Para acceder al panel desde la página de inicio [!DNL Experience Manager], haga clic en el icono de usuario y, a continuación, haga clic en **[!UICONTROL Preferencias de usuario]** > **[!UICONTROL Configuración de almacenamiento]**.

## Utilizar y administrar [!DNL Adobe Stock] recursos en [!DNL Experience Manager] {#usemanage}

Con esta capacidad, las organizaciones pueden permitir que sus usuarios trabajen con [!DNL Adobe Stock] recursos en [!DNL Experience Manager Assets]. Desde la interfaz de usuario [!DNL Experience Manager], los usuarios pueden buscar [!DNL Adobe Stock] recursos y obtener licencias para los recursos necesarios.

Una vez que un recurso [!DNL Adobe Stock] tiene licencia en [!DNL Experience Manager], se puede utilizar y administrar como un recurso típico. En [!DNL Experience Manager], los usuarios pueden buscar y previsualización de los recursos; copiar y publicar los recursos; compartir los recursos en [!DNL Brand Portal]; acceder a los recursos y utilizarlos mediante la aplicación de escritorio [!DNL Experience Manager]; y así sucesivamente.

![Buscar  [!DNL Adobe Stock] recursos y filtrar los resultados de su  [!DNL Adobe Experience Manager] espacio de trabajo](assets/adobe-stock-search-results-workspace.png)

*Figura: Busque  [!DNL Adobe Stock] recursos y filtre los resultados de su  [!DNL Experience Manager] interfaz.*

**A.**[!DNL Adobe Stock] Busque recursos similares a los del ID de proporcionado. **B.** Busque recursos que coincidan con la selección de forma u orientación. **C.** Busque uno de los tipos de recurso más admitidos **D.** Abra o contraiga el panel de filtros **E.** Obtenga la licencia y guarde el recurso seleccionado en [!DNL Experience Manager]**F.**[!DNL Experience Manager] Guarde el recurso en con la marca de agua **G.**[!DNL Adobe Stock] Explore los recursos del sitio web de que sean similares al recurso **H.**[!DNL Adobe Stock] Vea los recursos seleccionados en el sitio web de . **I.** Número de recursos seleccionados de los resultados de búsqueda **J.** Cambie entre la vista de tarjeta y la vista de lista

### Buscar recursos {#find-assets}

Los usuarios [!DNL Experience Manager] pueden buscar recursos en [!DNL Experience Manager] y [!DNL Adobe Stock]. Cuando la ubicación de búsqueda no está limitada a [!DNL Adobe Stock], se muestran los resultados de búsqueda de [!DNL Experience Manager] y [!DNL Adobe Stock].

* Para buscar [!DNL Adobe Stock] recursos, haga clic en **[!UICONTROL Navegación]** > **[!UICONTROL Recursos]** > **[!UICONTROL Buscar en Adobe Stock]**.

* Para buscar recursos en [!DNL Adobe Stock] y [!DNL Experience Manager Assets], haga clic en search ![search](assets/do-not-localize/search_icon.png).

Como alternativa, escriba `Location: Adobe Stock` inicio en la barra de búsqueda para seleccionar [!DNL Adobe Stock] recursos. [!DNL Experience Manager] oferta las funciones avanzadas de filtrado de los recursos buscados, lo que permite a los usuarios iniciar rápidamente la sesión en los recursos necesarios mediante filtros como, por ejemplo, tipos de recursos admitidos, orientación de imagen y estado con licencia.

>[!NOTE]
>
>Los recursos buscados desde [!DNL Adobe Stock] se muestran en [!DNL Experience Manager]. [!DNL Adobe Stock] los recursos se recuperan y almacenan en el  [!DNL Experience Manager] repositorio solo después de que un usuario  [guarda una ](/help/assets/aem-assets-adobe-stock.md#saveassets) licencia de  [visitante y guarda un recurso](/help/assets/aem-assets-adobe-stock.md#licenseassets). Los recursos que ya están almacenados en [!DNL Experience Manager] se muestran y resaltan para facilitar la referencia y el acceso. Además, los recursos [!DNL Stock] se guardan con algunos metadatos adicionales para indicar el origen como [!DNL Stock].

![Buscar filtros  [!DNL Experience Manager] y  [!DNL Adobe Stock] recursos resaltados en los resultados de búsqueda](assets/aem-search-filters2.jpg)

*Figura: Buscar filtros  [!DNL Experience Manager] y  [!DNL Adobe Stock] recursos resaltados en los resultados de búsqueda.*

### Guarde y vista los recursos necesarios {#saveassets}

Seleccione un recurso que desee guardar en [!DNL Experience Manager]. Haga clic en [!UICONTROL Guardar] en la barra de herramientas en la parte superior y proporcione el nombre y la ubicación del recurso. Los recursos sin licencia se guardan localmente con una marca de agua.

La próxima vez que busque recursos, los recursos guardados se resaltarán con un distintivo para indicar que dichos recursos están disponibles en [!DNL Experience Manager Assets].

>[!NOTE]
>
>Los recursos añadidos recientemente muestran un distintivo Nuevo en lugar de un distintivo Con licencia.

### Recursos de licencia {#licenseassets}

Los usuarios pueden obtener licencias de [!DNL Adobe Stock] recursos mediante la cuota de su [!DNL Adobe Stock] plan empresarial. Al otorgar licencias a un recurso, éste se guarda sin marca de agua y está disponible para su búsqueda y uso en [!DNL Experience Manager Assets].

![Cuadro de diálogo para otorgar licencias y guardar  [!DNL Adobe Stock] recursos en  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)

*Figura: Cuadro de diálogo para obtener la licencia y guardar  [!DNL Adobe Stock] recursos en  [!DNL Experience Manager Assets].*

### Acceso a metadatos y propiedades de recursos {#access-metadata-and-asset-properties}

Los usuarios pueden acceder a los metadatos y previsualizaciones, incluidas las propiedades de metadatos [!DNL Adobe Stock] de los recursos guardados en [!DNL Experience Manager], y agregar **[!UICONTROL Referencias de licencia]** para un recurso. Sin embargo, las actualizaciones de la referencia de licencia no se sincronizan entre [!DNL Experience Manager] y [!DNL Adobe Stock] sitios Web.

Los usuarios pueden ver las propiedades de los recursos con y sin licencia.

![Vista y acceso a metadatos y referencias de licencia de recursos guardados](assets/metadata_properties.jpg)

*Figura: Vista y acceso a metadatos y referencias de licencia de los recursos guardados.*

## Limitaciones conocidas {#known-limitations}

* **No se muestra** la advertencia de imagen editorial: Al otorgar licencias a una imagen, los usuarios no pueden comprobar si una imagen es solo para uso editorial. Para evitar un posible uso indebido, los administradores pueden desactivar el acceso del Admin Console a los recursos editoriales.

* **Se muestra** un tipo de licencia incorrecto: Es posible que se muestre un tipo de licencia incorrecto en  [!DNL Experience Manager] para un recurso. Los usuarios pueden iniciar sesión en el sitio Web [!DNL Adobe Stock] para ver el tipo de licencia.

* **Los campos de referencia y los metadatos no se sincronizan**: Cuando un usuario actualiza un campo de referencia de licencia, la información de referencia de licencia se actualiza en el  [!DNL Experience Manager] sitio  [!DNL Adobe Stock] web, pero no en él. Del mismo modo, si el usuario actualiza los campos de referencia en el sitio Web [!DNL Adobe Stock], las actualizaciones no se sincronizan en [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutorial de vídeo sobre el  [!DNL Adobe Stock] uso de recursos con [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] ayuda del plan de empresa](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] Preguntas más frecuentes](https://helpx.adobe.com/stock/faq.html)

