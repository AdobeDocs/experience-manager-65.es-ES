---
title: Configuración de la estructura del sitio web
seo-title: Setup Website Structure
description: Configuración de directorios
seo-description: Set up directories
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 1%

---

# Configuración de la estructura del sitio web {#setup-website-structure}

Para configurar su sitio web, las instrucciones siguientes describen las carpetas que se van a crear en las ubicaciones siguientes:

* `/apps/an-scf-sandbox`

   Aquí es donde residen las aplicaciones y plantillas personalizadas.

* `/etc/designs/an-scf-sandbox`

   Aquí es donde residen los elementos de diseño descargables.

* `/content/an-scf-sandbox`

   Aquí es donde residen las páginas web descargables.

El código de este tutorial dependerá de que el nombre de la carpeta principal sea el mismo para la aplicación, el diseño y el contenido. Si elige otro nombre para su sitio web, reemplace siempre `an-scf-sandbox` con el nombre que ha elegido.

>[!NOTE]
>
>Acerca de los nombres:
>
>* Los nombres que se ven en CRXDE son nombres de nodo que forman la ruta al contenido direccionable.
>* Los nombres de nodo pueden contener espacios, pero cuando se utilizan en un URI, el espacio debe codificarse como &#39;%20&#39; o &#39;+&#39;.
>* Los nombres de nodo pueden contener guiones y guiones bajos, pero deben codificarse cuando se hace referencia a ellos como nombre de paquete dentro de un archivo Java. Tanto los guiones como los guiones bajos se escapan con un guion bajo seguido de su valor Unicode:
   >
   >   * el guión se convierte en &#39;_002d&#39;
   >   * el guión bajo se convierte en &#39;_005f&#39;


## Configuración del directorio de aplicaciones (/apps) {#setup-the-application-directory-apps}

El directorio /apps del repositorio contiene el código con implementa el comportamiento y renderización de las páginas servidas desde el directorio /content.

El directorio /apps está protegido y no es accesible públicamente, al igual que los directorios /content y /etc/designs.

1. Crear `/apps/an-scf-sandbox` carpeta.

   Uso **[!UICONTROL CRXDE Lite]**, en el panel del explorador

   1. Seleccione el `/apps` carpeta.
   1. Clic con el botón derecho **[!UICONTROL Crear]**... o tire hacia abajo del **[!UICONTROL Crear...]** para abrir el Navegador.
   1. Select **[!UICONTROL Crear carpeta...]**.
   1. En el **[!UICONTROL Crear carpeta]** cuadro de diálogo, introduzca `an-scf-sandbox`.
   1. Haga clic en **[!UICONTROL Aceptar]**.

1. Crear **[!UICONTROL componentes]** subcarpeta.

   1. Seleccione el `/apps/an-scf-sandbox` carpeta.
   1. Haga clic en **[!UICONTROL Crear > Crear carpeta]**.
   1. En el **[!UICONTROL Crear carpeta]** cuadro de diálogo, introduzca **[!UICONTROL componentes]**.
   1. Haga clic en **[!UICONTROL Aceptar]**.

1. Crear **[!UICONTROL plantillas]** subcarpeta.

   1. Seleccione el `/apps/an-scf-sandbox` carpeta.
   1. Haga clic en **[!UICONTROL Crear > Crear carpeta]**.
   1. En el **[!UICONTROL Crear carpeta]** cuadro de diálogo, introduzca **[!UICONTROL plantillas]**.
   1. Haga clic en **[!UICONTROL Aceptar]**.
   1. Volver a seleccionar `/apps/an-scf-sandbox`.
   1. Select **[!UICONTROL Guardar todo]**.

   Al igual que con cualquier proceso de edición, guarde con frecuencia. Si tiene problemas al introducir datos, puede deberse a que se ha agotado el tiempo de espera de su inicio de sesión o a que necesita guardar ediciones anteriores.

1. La estructura del panel del explorador del CRXDE Lite debería tener este aspecto:

   ![crxde-template](assets/crxde-template.png)

## Configuración del directorio de diseño (/etc/designs) {#setup-the-design-directory-etc-designs}

El directorio /etc/designs contiene las imágenes, scripts y hojas de estilo que se van a descargar junto con el contenido de la página.

1. Para utilizar la herramienta Designer en la IU clásica, vaya a [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Nota: Si utiliza el CRXDE Lite para crear un nodo de tipo `cq:Page`, el Control de acceso y la replicación no se establecerían en la configuración predeterminada de una página.

1. En el panel del explorador, seleccione la opción **[!UICONTROL Diseños]** carpeta y, a continuación, haga clic en **[!UICONTROL Nuevo]** > **[!UICONTROL Nueva página]**.

   Escriba

   * Título: **[!UICONTROL Un Simulador para pruebas SCF]**
   * Nombre: **[!UICONTROL an-scf-sandbox]**
   * Select **[!UICONTROL Plantilla de página de diseño]**

   Haga clic en **[!UICONTROL Crear]**.

   ![plantilla de diseño](assets/design-template.png)

1. Actualice el panel del explorador si no aparece la carpeta &quot;Un espacio aislado de SCF&quot;.

1. Vuelva al CRXDE Lite (http:// localhost:4502/crx/de) y expanda /etc/designs para ver el nodo llamado &quot;an-scf-sandbox&quot;.

   En el panel inferior derecho de CRXDE, puede ver la pestaña Propiedades , la pestaña Control de acceso y la pestaña Replicación para ver qué se definió con la plantilla Página de diseño .

   ![crxde-configure-template](assets/crxde-configure-template.png)

## Configuración del directorio de contenido (/content) {#setup-the-content-directory-content}

El directorio /content del repositorio es donde reside el contenido del sitio web. Las rutas bajo /content comprenden las rutas de la dirección URL para las solicitudes del explorador.

*Después* el [plantilla de página](initial-app.md#createthepagetemplate) se crea como parte de la aplicación inicial, el contenido de la página inicial se puede crear en función de la plantilla.... [**Archivadores**](initial-app.md)
