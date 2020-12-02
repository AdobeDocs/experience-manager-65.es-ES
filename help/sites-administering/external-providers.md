---
title: Analytics con proveedores externos
seo-title: Analytics con proveedores externos
description: Obtenga información sobre Analytics con proveedores externos.
seo-description: Obtenga información sobre Analytics con proveedores externos.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---


# Analytics con proveedores externos {#analytics-with-external-providers}

Analytics puede proporcionarle información importante e interesante sobre cómo se utiliza su sitio web.

Hay varias configuraciones listas para usar disponibles para la integración con el servicio adecuado, por ejemplo:

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

También puede configurar su propia instancia de los **fragmentos genéricos de Analytics** para definir una nueva configuración de servicio.

La información se recopila mediante pequeños fragmentos de código que se agregan a las páginas web. Por ejemplo:

>[!CAUTION]
>
>Las secuencias de comandos no se deben incluir en etiquetas `script`.

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

Estos fragmentos permiten recopilar datos y generar informes. Los datos reales recopilados dependen del proveedor y del fragmento de código utilizado. Las estadísticas de ejemplo incluyen:

* cuántos visitantes con el tiempo
* cantidad de páginas visitadas
* términos de búsqueda utilizados
* páginas de aterrizaje

>[!CAUTION]
>
>El sitio de demostración de Geometrixx-Outdoors está configurado de modo que los atributos proporcionados en las Propiedades de la página se anexen al código fuente HTML (justo encima de la `</html>` etiqueta final) en la secuencia de comandos `js` correspondiente.
>
>Si su propio `/apps` no hereda del componente de página predeterminado ( `/libs/foundation/components/page`) usted (o sus programadores) deben asegurarse de que se incluyen los `js` scripts correspondientes, por ejemplo incluyendo `cq/cloudserviceconfigs/components/servicescomponents` o utilizando un mecanismo similar.
>
>Sin esto, ninguno de los servicios (Genérico, Analytics, Destinatario, etc.) funcionará.

## Creación de un nuevo servicio con un fragmento genérico {#creating-a-new-service-with-a-generic-snippet}

Para la configuración básica:

1. Abra la consola **Herramientas**.
1. En el panel izquierdo, expanda **Configuraciones de Cloud Services**.
1. Haga clic con el botón doble en **Fragmento de análisis genérico** para abrir la página:

   ![](assets/analytics_genericoverview.png)

1. Haga clic en + para agregar una nueva configuración mediante el cuadro de diálogo; como mínimo, asigne un nombre, por ejemplo Google Analytics:

   ![](assets/analytics_addconfig.png)

1. Haga clic en **Crear**, el cuadro de diálogo de fragmento se abrirá inmediatamente y pegue el fragmento de código javascript correspondiente en el campo:

   ![](assets/analytics_snippet.png)

1. Haga clic en **Aceptar** para guardar.

## Uso del nuevo servicio en páginas {#using-your-new-service-on-pages}

Después de crear la configuración del servicio, ahora necesita configurar las páginas necesarias para utilizarla:

1. Vaya a la página.
1. Abra la **Propiedades de la página** desde la barra de tareas y, a continuación, la ficha **Cloud Services**.
1. Haga clic en **Añadir servicio** y seleccione el servicio requerido; por ejemplo: **Fragmento de Analytics genérico**:

   ![](assets/analytics_selectservice.png)

1. Haga clic en **Aceptar** para guardar.
1. Volverá a la ficha **Cloud Services**. El **fragmento de análisis genérico** aparece ahora con el mensaje `Configuration reference missing`. Utilice la lista desplegable para seleccionar la instancia de servicio específica; por ejemplo google-analytics:

   ![](assets/analytics_selectspecificservice.png)

1. Haga clic en **Aceptar** para guardar.

   Ahora se puede ver el fragmento si se vista el origen de página para la página.

   Una vez transcurrido un período de tiempo adecuado, podrá realizar la vista de las estadísticas que se han recopilado.

   >[!NOTE]
   >
   >Si la configuración se adjunta a una página que tiene páginas secundarias, también las heredan.
