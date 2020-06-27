---
title: ' [!DNL Adobe Stock] Administre recursos en [!DNL Adobe Experience Manager Assets].'
description: Buscar, recuperar, licenciar y [!DNL Adobe Stock] administrar recursos desde dentro [!DNL Adobe Experience Manager]. Utilice los recursos con licencia como cualquier otro recurso digital.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a61e1e9ffb132b59c725b2078f09641a3c2a479a
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 16%

---


# Utilizar [!DNL Adobe Stock] recursos en [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

Las organizaciones pueden integrar sus [!DNL Adobe Stock] planes empresariales con [!DNL Experience Manager Assets] el fin de garantizar que los activos con licencia estén disponibles en general para sus proyectos creativos y de marketing, con las potentes capacidades de administración de activos de [!DNL Experience Manager].

[!DNL Adobe Stock]El servicio proporciona a diseñadores y empresas acceso a millones de fotos, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, verificados y libres de derechos de autor para todos sus proyectos creativos. [!DNL Experience Manager] los usuarios pueden encontrar, previsualización y obtener licencias [!DNL Adobe Stock] de los recursos guardados en [!DNL Experience Manager]sin salir de la [!DNL Experience Manager] interfaz.

## Requisitos previos {#prerequisites}

La integración requiere un plan [Adobe Stock](https://stockenterprise.adobe.com/) empresarial y [!DNL Experience Manager] 6.5 o posterior. Para obtener más información sobre el Service Pack [!DNL Experience Manager] 6.5, consulte estas notas [de la versión](/help/release-notes/sp-release-notes.md).

## Integrar [!DNL Experience Manager] y [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Para permitir la comunicación entre [!DNL Experience Manager] y [!DNL Adobe Stock], cree una configuración IMS y una [!DNL Adobe Stock] configuración en [!DNL Experience Manager].

>[!NOTE]
>
>Solo [!DNL Experience Manager] los administradores y [!DNL Admin Console] administradores de una organización pueden realizar la integración ya que requiere privilegios de administrador.

### Create an IMS configuration {#create-an-ims-configuration}

1. Click on [!DNL Experience Manager] logo. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**. Haga clic en **[!UICONTROL Crear]** y seleccione **[!UICONTROL Solución de nube]** > **[!UICONTROL Adobe Stock]**.
1. Vuelva a utilizar un certificado existente o seleccione **[!UICONTROL Crear nuevo certificado]**.
1. Haga clic en **[!UICONTROL Crear certificado]**. Una vez creada, descargue la clave pública. Haga clic en **[!UICONTROL Siguiente]**. 
1. Indique los valores adecuados en los campos **[!UICONTROL Título]**, **[!UICONTROL Servidor de autorizaciones]**, **[!UICONTROL Clave de API]**, **[!UICONTROL Secreto del cliente]** y **[!UICONTROL Carga]**. Consulte [Inicio rápido de la autenticación JWT](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md) para obtener información detallada sobre cómo recuperar estos valores desde [!DNL Adobe I/O].
1. Añada la clave pública descargada en su cuenta [!DNL Adobe I/O] de servicio.

<!-- TBD: Update the URL when the new URL is available. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Crear [!DNL Adobe Stock] configuración en [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Haga clic en **[!UICONTROL Crear]** para crear una configuración y asociarla con la configuración de IMS existente. Seleccione `PROD` como parámetro de entorno.
1. En el campo Ruta **[!UICONTROL de recursos con]** licencia, deje una ubicación tal cual. No cambie la ubicación donde desea almacenar los [!DNL Adobe Stock] recursos.
1. Complete la creación agregando todas las propiedades necesarias. Click **[!UICONTROL Save &amp; Close]**.
1. Añada [!DNL Experience Manager] usuarios o grupos que puedan obtener licencias para los recursos.

>[!NOTE]
>
>Si hay varias [!DNL Adobe Stock] configuraciones, seleccione la configuración deseada en el panel Preferencias [!UICONTROL de] usuario haciendo clic en el logotipo *Usuario* en la esquina superior derecha de la interfaz de [!DNL Experience Manager] usuario.

## Uso y gestión de [!DNL Adobe Stock] recursos en [!DNL Experience Manager] {#usemanage}

Con esta capacidad, las organizaciones pueden permitir que sus usuarios trabajen con [!DNL Adobe Stock] los recursos de [!DNL Experience Manager Assets]. Desde la interfaz de usuario, los usuarios pueden buscar [!DNL Experience Manager] [!DNL Adobe Stock] recursos y obtener licencias para ellos.

Una vez que un [!DNL Adobe Stock] recurso tiene licencia en [!DNL Experience Manager], se puede utilizar y administrar como un recurso típico. En [!DNL Experience Manager], los usuarios pueden buscar y previsualización de los recursos; copiar y publicar los recursos; compartir los activos en [!DNL Brand Portal]; acceder a los recursos y utilizarlos mediante la aplicación de [!DNL Experience Manager] escritorio; y así sucesivamente.

![Busque recursos de Adobe Stock y filtre los resultados del espacio de trabajo de Adobe Experience Manager](assets/adobe-stock-search-results-workspace.png)

*Figura: Busque[!DNL Adobe Stock]recursos y filtre los resultados de la[!DNL Experience Manager]interfaz.*

**A.**[!DNL Adobe Stock] Busque recursos similares a los del ID de proporcionado. **B.** Busque recursos que coincidan con la selección de forma u orientación. **C.** Busque uno de los tipos de recurso más admitidos **D.** Abra o contraiga el panel de filtros **E.** Obtenga la licencia y guarde el recurso seleccionado en [!DNL Experience Manager]**F.**[!DNL Experience Manager] Guarde el recurso en con la marca de agua **G.**[!DNL Adobe Stock] Explore los recursos del sitio web de que sean similares al recurso **H.**[!DNL Adobe Stock] Vea los recursos seleccionados en el sitio web de . **I.** Número de recursos seleccionados de los resultados de búsqueda **J.** Cambie entre la vista de tarjeta y la vista de lista

### Buscar recursos {#find-assets}

Los [!DNL Experience Manager] usuarios pueden buscar recursos tanto en [!DNL Experience Manager] como en [!DNL Adobe Stock]. Cuando la ubicación de búsqueda no está limitada a [!DNL Adobe Stock], se muestran los resultados de la búsqueda [!DNL Experience Manager] y [!DNL Adobe Stock] .

* Para buscar [!DNL Adobe Stock] recursos, haga clic en **[!UICONTROL Navegación]** > **[!UICONTROL Recursos]** > **[!UICONTROL Buscar en Adobe Stock]**.

* Para buscar recursos en [!DNL Adobe Stock] y [!DNL Experience Manager Assets], haga clic en search ![search_icon](assets/search_icon.png).

Como alternativa, escriba `Location: Adobe Stock` inicio en la barra de búsqueda para seleccionar [!DNL Adobe Stock] recursos. [!DNL Experience Manager] oferta las funciones avanzadas de filtrado de los recursos buscados, lo que permite a los usuarios iniciar rápidamente la sesión en los recursos necesarios mediante filtros como, por ejemplo, tipos de recursos admitidos, orientación de imagen y estado con licencia.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] los recursos se recuperan y almacenan en [!DNL Experience Manager] el repositorio solo después de que un usuario [guarde un recurso](/help/assets/aem-assets-adobe-stock.md#saveassets) o [licencias y guarde un recurso](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Buscar filtros en Experience Manager y recursos de Adobe Stock resaltados en los resultados de búsqueda](assets/aem-search-filters2.jpg)

*Figura: Buscar filtros[!DNL Experience Manager]y recursos resaltados[!DNL Adobe Stock]en los resultados de búsqueda.*

### Guardar y vista de los recursos necesarios {#saveassets}

Seleccione un recurso en el que desee guardar [!DNL Experience Manager]. Haga clic en [!UICONTROL Guardar] en la barra de herramientas situada en la parte superior y proporcione el nombre y la ubicación del recurso. Los recursos sin licencia se guardan localmente con una marca de agua.

La próxima vez que busque recursos, los recursos guardados se resaltarán con un distintivo para indicar que dichos recursos están disponibles en [!DNL Experience Manager Assets].

>[!NOTE]
>
>Los recursos añadidos recientemente muestran un distintivo Nuevo en lugar de un distintivo Con licencia.

### Recursos de licencia {#licenseassets}

Los usuarios pueden obtener licencias de [!DNL Adobe Stock] recursos mediante la cuota de su plan de [!DNL Adobe Stock] empresa. Al otorgar licencias a un recurso, éste se guarda sin marca de agua y está disponible para su búsqueda y uso en [!DNL Experience Manager Assets].

![Cuadro de diálogo para obtener la licencia y guardar recursos de Adobe Stock en Recursos Experience Manager](assets/aem-stock_licenseandsave.jpg)

*Figura: Cuadro de diálogo para obtener la licencia y guardar[!DNL Adobe Stock]recursos en[!DNL Experience Manager Assets].*

### Acceso a metadatos y propiedades de recursos {#access-metadata-and-asset-properties}

Los usuarios pueden acceder a los metadatos y darles previsualización, incluidas las propiedades de los [!DNL Adobe Stock] metadatos de los recursos guardados en [!DNL Experience Manager], así como agregar referencias **[!UICONTROL de]** licencia para un recurso. Sin embargo, las actualizaciones de la referencia de licencia no se sincronizan entre [!DNL Experience Manager] y el [!DNL Adobe Stock] sitio web.

Los usuarios pueden ver las propiedades de los recursos con y sin licencia.

![Vista y acceso a metadatos y referencias de licencia de recursos guardados](assets/metadata_properties.jpg)

*Figura: Vista y acceso a metadatos y referencias de licencia de los recursos guardados.*

## Limitaciones conocidas {#known-limitations}

* **No se muestra** la advertencia de imagen editorial: Al otorgar licencias a una imagen, los usuarios no pueden comprobar si una imagen es solo para uso editorial. Para evitar un posible uso indebido, los administradores pueden desactivar el acceso a los recursos editoriales del Admin Console.

* **Se muestra** un tipo de licencia incorrecto: Es posible que se muestre un tipo de licencia incorrecto en [!DNL Experience Manager] para un recurso. Los usuarios pueden iniciar sesión en el [!DNL Adobe Stock] sitio web para ver el tipo de licencia.

* **Los campos de referencia y los metadatos no se sincronizan**: Cuando un usuario actualiza un campo de referencia de licencia, la información de referencia de licencia se actualiza en el [!DNL Experience Manager] sitio web, pero no en el [!DNL Adobe Stock] . Del mismo modo, si el usuario actualiza los campos de referencia del [!DNL Adobe Stock] sitio web, las actualizaciones no se sincronizan en [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutorial de vídeo sobre el uso de recursos de Adobe Stock con recursos de Experience Manager](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)
>* [Ayuda del plan empresarial de Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Preguntas más frecuentes sobre Adobe Stock](https://helpx.adobe.com/stock/faq.html)

