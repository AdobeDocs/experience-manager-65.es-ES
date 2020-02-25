---
title: Configuración de la estructura del sitio web
seo-title: Configuración de la estructura del sitio web
description: Configuración de directorios
seo-description: Configuración de directorios
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
translation-type: tm+mt
source-git-commit: 4f4f2897000a0afe26a0dbcc4514e20befdb4114

---


# Configuración de la estructura del sitio web {#setup-website-structure}

Para configurar el sitio web, las instrucciones siguientes describen las carpetas que se van a crear en las ubicaciones siguientes:

* `/apps/an-scf-sandbox`
Aquí es donde residen las aplicaciones y plantillas personalizadas

* `/etc/designs/an-scf-sandbox`
Aquí es donde residen los elementos de diseño descargables

* `/content/an-scf-sandbox`
Aquí es donde residen las páginas Web descargables

El código de este tutorial dependerá de que el nombre de la carpeta principal sea el mismo para la aplicación, el diseño y el contenido. Si elige otro nombre para el sitio web, reemplace siempre `an-scf-sandbox` por el nombre que haya elegido.

>[!NOTE]
>
>Acerca de los nombres:
>
>* Los nombres que se ven en CRXDE son nombres de nodo que forman la ruta al contenido direccionable
>* Los nombres de nodo pueden contener espacios, pero cuando se utilizan en un URI, el espacio debe codificarse como &#39;%20&#39; o &#39;+&#39;
>* Los nombres de nodo pueden contener guiones y guiones bajos, pero deben codificarse cuando se hace referencia a ellos como un nombre de paquete dentro de un archivo Java. Tanto los guiones como los guiones bajos se escapan con un guión bajo seguido de su valor Unicode:
>
>   * el guión se convierte en &#39;_002d&#39;
>   * el guión bajo se convierte en &#39;_005f&#39;

## Configuración del directorio de aplicaciones (/apps) {#setup-the-application-directory-apps}

El directorio /apps del repositorio contiene el código con implementa el comportamiento y la representación de las páginas servidas desde el directorio /content.

El directorio /apps está protegido y no es accesible al público, al igual que los directorios /content y /etc/designs.

1. Create `/apps/an-scf-sandbox` folder.

   Uso de **[!UICONTROL CRXDE Lite]**, en el panel del explorador

   1. Seleccione la `/apps` carpeta
   1. **[!UICONTROL Haga clic con el botón secundario en]** Crear **[!UICONTROL ... o tire hacia abajo de]** Crear...menú
   1. **[!UICONTROL Seleccione]** Crear carpeta... .
   1. En el cuadro de diálogo **[!UICONTROL Crear carpeta]** , introduzca `an-scf-sandbox`
   1. Haga clic en **[!UICONTROL Aceptar]**

1. Crear subcarpeta **[!UICONTROL de componentes]** .

   1. Seleccione la `/apps/an-scf-sandbox` carpeta
   1. Haga clic en **[!UICONTROL Crear > Crear carpeta]**
   1. En el cuadro de diálogo **[!UICONTROL Crear carpeta]** , introduzca **[!UICONTROL componentes]**
   1. Haga clic en **[!UICONTROL Aceptar]**

1. Cree una subcarpeta **de plantillas **.

   1. Seleccione la `/apps/an-scf-sandbox` carpeta
   1. Haga clic en **[!UICONTROL Crear > Crear carpeta]**
   1. En el cuadro de diálogo **[!UICONTROL Crear carpeta]** , introduzca **[!UICONTROL plantillas]**
   1. Haga clic en **[!UICONTROL Aceptar]**
   1. Volver a seleccionar `/apps/an-scf-sandbox`
   1. Seleccione **[!UICONTROL Guardar todo]**
   Como con cualquier proceso de edición, guarde con frecuencia. Si tiene problemas con la introducción de datos, puede que se deba a que se agotó el tiempo de espera del inicio de sesión o a que necesite guardar las ediciones anteriores.

1. La estructura del panel del explorador de CRXDE Lite ahora debería tener este aspecto:

   ![chlimage_1-44](assets/chlimage_1-44.png)

## Configuración del directorio de diseño (/etc/designs) {#setup-the-design-directory-etc-designs}

El directorio /etc/designs contiene las imágenes, secuencias de comandos y hojas de estilo que se van a descargar junto con el contenido de la página.

1. Para utilizar la herramienta Designer en la IU clásica, vaya a [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Nota: Si utiliza CRXDE Lite para crear un Nodo de tipo `cq:Page`, el Control de acceso y la Replicación no se establecerían en la configuración predeterminada de una página.

1. En el panel del explorador, seleccione la carpeta **[!UICONTROL Diseños]** y, a continuación, haga clic en **[!UICONTROL Nuevo > Nueva página]**.

   Intro:

   * Título: **Un Simulador Para Pruebas SCF**
   * Nombre: **an-scf-sandbox**
   * Seleccionar plantilla de página **de diseño**
   Haga clic en **[!UICONTROL Crear]**

   ![chlimage_1-45](assets/chlimage_1-45.png)

1. Actualice el panel del explorador si no aparece la carpeta &quot;Simulador para pruebas de SCF&quot;.

1. Vuelva a CRXDE Lite (http:// localhost:4502/crx/de) y expanda /etc/designs para ver el nodo llamado &quot;an-scf-sandbox&quot;.

   En el panel inferior derecho de CRXDE, puede ver la ficha Propiedades, la ficha Control de acceso y la ficha Replicación para ver qué se definió con la plantilla Página de diseño.

   ![chlimage_1-46](assets/chlimage_1-46.png)

## Configuración del directorio de contenido (/content) {#setup-the-content-directory-content}

El directorio /content del repositorio es donde reside el contenido del sitio web. Las rutas de acceso de /content comprenden las rutas de la dirección URL para las solicitudes del explorador.

*Después* de crear la plantilla [de](initial-app.md#createthepagetemplate) página como parte de la aplicación inicial, el contenido de la página inicial se puede crear en función de la plantilla... .  [****](initial-app.md)
