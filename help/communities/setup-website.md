---
title: Configurar estructura del sitio web
description: Obtenga información sobre cómo configurar la estructura del sitio web, incluidas las carpetas que se van a crear.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# Configurar estructura del sitio web {#setup-website-structure}

Para configurar el sitio web, las instrucciones siguientes describen las carpetas que se crean en las siguientes ubicaciones:

* `/apps/an-scf-sandbox`

  Aquí es donde residen las aplicaciones y plantillas personalizadas.

* `/etc/designs/an-scf-sandbox`

  Aquí es donde residen los elementos de diseño descargables.

* `/content/an-scf-sandbox`

  Aquí es donde residen las páginas web descargables.

El código de este tutorial depende de que el nombre de la carpeta principal sea el mismo para la aplicación, el diseño y el contenido. Si elige otro nombre para el sitio web, reemplace siempre `an-scf-sandbox` con el nombre que ha elegido.

>[!NOTE]
>
>Nombres:
>
>* Los nombres que se ven en CRXDE son nombres de nodo que forman la ruta al contenido accesible.
>* Los nombres de nodo pueden contener espacios, pero cuando se utilizan en un URI, el espacio debe codificarse como &#39;%20&#39; o &#39;+&#39;.
>* Los nombres de nodo pueden contener guiones y guiones bajos, pero deben codificarse cuando se haga referencia a ellos como un nombre de paquete dentro de un archivo Java™. Tanto los guiones como los guiones bajos se codifican con guiones bajos seguidos de su valor Unicode:
>
>   * el guión se convierte en &#39;_002d&#39;
>   * el guion bajo se convierte en &#39;_005f&#39;

## Configurar el directorio de aplicaciones (/apps) {#setup-the-application-directory-apps}

El directorio /apps en el repositorio contiene el código con implementa el comportamiento y el procesamiento de las páginas servidas desde el directorio /content.

El directorio /apps está protegido y no es accesible públicamente, como los directorios /content y /etc/designs.

1. Crear `/apps/an-scf-sandbox` carpeta.

   Uso de **[!UICONTROL CRXDE Lite]**, en el panel del explorador

   1. Seleccione el `/apps` carpeta.
   1. Clic con el botón derecho **[!UICONTROL Crear]**... o tire hacia abajo del **[!UICONTROL Crear...]** menú.
   1. Seleccionar **[!UICONTROL Crear carpeta...]**.
   1. En el **[!UICONTROL Crear carpeta]** diálogo, introduzca `an-scf-sandbox`.
   1. Haz clic en **[!UICONTROL OK]**.

1. Crear **[!UICONTROL componentes]** subcarpeta.

   1. Seleccione el `/apps/an-scf-sandbox` carpeta.
   1. Clic **[!UICONTROL Crear > Crear carpeta]**.
   1. En el **[!UICONTROL Crear carpeta]** diálogo, introduzca **[!UICONTROL componentes]**.
   1. Haz clic en **[!UICONTROL OK]**.

1. Crear **[!UICONTROL templates]** subcarpeta.

   1. Seleccione el `/apps/an-scf-sandbox` carpeta.
   1. Clic **[!UICONTROL Crear > Crear carpeta]**.
   1. En el **[!UICONTROL Crear carpeta]** diálogo, introduzca **[!UICONTROL templates]**.
   1. Haz clic en **[!UICONTROL OK]**.
   1. Volver a seleccionar `/apps/an-scf-sandbox`.
   1. Seleccionar **[!UICONTROL Guardar todo]**.

   Al igual que con cualquier proceso de edición, debe guardar con frecuencia. Si tiene problemas para introducir datos, puede deberse a que se ha agotado el tiempo de espera de inicio de sesión o a que debe guardar las ediciones anteriores.

1. La estructura del panel del explorador del CRXDE Lite debería tener un aspecto similar al siguiente:

   ![crxde-template](assets/crxde-template.png)

## Configurar el directorio de diseño (/etc/designs) {#setup-the-design-directory-etc-designs}

El directorio /etc/designs contiene las imágenes, los scripts y las hojas de estilo que se van a descargar junto con el contenido de la página.

1. Para utilizar la herramienta Diseñador en la IU clásica, vaya a [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Nota: Si utiliza el CRXDE Lite para crear un nodo de tipo `cq:Page`, el Control de acceso y la Replicación no se establecerían en la configuración predeterminada de una página.

1. En el panel del explorador, seleccione **[!UICONTROL Diseños]** y haga clic en **[!UICONTROL Nuevo]** > **[!UICONTROL Nueva página]**.

   Escriba

   * Título: **[!UICONTROL Una zona protegida de SCF]**
   * Nombre: **[!UICONTROL an-scf-sandbox]**
   * Seleccionar **[!UICONTROL Plantilla de página de diseño]**

   Haga clic en **[!UICONTROL Crear]**.

   ![design-template](assets/design-template.png)

1. Actualice el panel del explorador si no aparece la carpeta &quot;Zona protegida de SCF&quot;.

1. Vuelva al CRXDE Lite (http:// localhost:4502/crx/de) y expanda /etc/designs para ver el nodo llamado &quot;an-scf-sandbox&quot;.

   En el panel inferior derecho de CRXDE, puede ver las pestañas Propiedades, Control de acceso y Replicación para ver lo que se ha definido con la plantilla de la página de diseño.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## Configurar el directorio de contenido (/content) {#setup-the-content-directory-content}

El directorio /content del repositorio es donde reside el contenido del sitio web. Las rutas en /content comprenden las rutas de la URL para las solicitudes del explorador.

*Después* el [plantilla de página](initial-app.md#createthepagetemplate) se crea como parte de la aplicación inicial, el contenido de la página inicial se puede crear en función de la plantilla.... [**⇒**](initial-app.md)
