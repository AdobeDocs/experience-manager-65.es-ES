---
title: Analytics con proveedores externos
seo-title: Analytics with External Providers
description: Obtenga información sobre Analytics con proveedores externos.
seo-description: Learn about Analytics with External Providers.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: ec4f24528089fe3de639b974ff4ab6f8807fc7fc
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 2%

---


# Analytics con proveedores externos {#analytics-with-external-providers}

Analytics puede proporcionarle información importante e interesante sobre el uso que se le da a su sitio web.

Hay varias configuraciones disponibles para la integración con el servicio adecuado, por ejemplo:

* [API de Rest](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

También puede configurar su propia instancia de **Fragmentos genéricos de Analytics** para definir nuevas configuraciones de servicio.

A continuación, la información se recopila mediante pequeños fragmentos de código que se añaden a las páginas web. Por ejemplo:

>[!CAUTION]
>
>Los scripts no deben incluirse en `script` etiquetas.

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

Estos fragmentos permiten recopilar datos y generar informes. Los datos reales recopilados dependen del proveedor y del fragmento de código real utilizado. Las estadísticas de ejemplo incluyen:

* cuántos visitantes con el tiempo
* cuántas páginas visitadas
* términos de búsqueda utilizados
* páginas de aterrizaje

>[!CAUTION]
>
>El sitio de demostración de Geometrixx-Outdoors está configurado de modo que los atributos proporcionados en Propiedades de página se anexen al código fuente html (justo encima de ). `</html>` endtag) en el `js` script.
>
>Si su propio `/apps` no heredar del componente de página predeterminado ( `/libs/foundation/components/page`) usted (o sus desarrolladores) debe asegurarse de que las `js` Los scripts de se incluyen, por ejemplo, incluyendo `cq/cloudserviceconfigs/components/servicescomponents`o utilizando un mecanismo similar.
>
>Sin esto, ninguno de los servicios (genérico, de Analytics, de Target, etc.) funcionará.

## Creación de un nuevo servicio con un fragmento genérico {#creating-a-new-service-with-a-generic-snippet}

Para la configuración básica:

1. Abra el **Herramientas** consola.
1. En el panel izquierdo, expanda **Configuraciones de Cloud Services**.
1. Haga doble clic en **Fragmento de análisis genérico** para abrir la página:

   ![Fragmento de análisis genérico](assets/analytics_genericoverview.png)

1. Haga clic en + para añadir una nueva configuración mediante el cuadro de diálogo; como mínimo, asigne un nombre, por ejemplo, Google Analytics:

   ![Crear configuración](assets/analytics_addconfig.png)

1. Clic **Crear**, el cuadro de diálogo de fragmento se abrirá inmediatamente: pegue el fragmento de javascript correspondiente en el campo:

   ![Edición del componente](assets/analytics_snippet.png)

1. Clic **OK** para guardar.

## Uso del nuevo servicio en páginas {#using-your-new-service-on-pages}

Una vez creada la configuración del servicio, ahora debe configurar las páginas necesarias para utilizarlo:

1. Navegue hasta la página.
1. Abra el **Propiedades de página** de la barra de tareas, luego el **Cloud Services** pestaña.
1. Clic **Añadir servicio** y, a continuación, seleccione el servicio necesario; por ejemplo, el **Fragmento de análisis genérico**:

   ![Añadir un servicio en la nube](assets/analytics_selectservice.png)

1. Clic **OK** para guardar.
1. Se le devolverá a la **Cloud Services** pestaña. El **Fragmento de análisis genérico** ahora aparece con el mensaje `Configuration reference missing`. Utilice la lista desplegable para seleccionar su instancia de servicio específica; por ejemplo, google-analytics:

   ![Adición de la configuración de Cloud Service](assets/analytics_selectspecificservice.png)

1. Clic **OK** para guardar.

   Ahora, el fragmento se puede ver si ve el Origen de la página para la página.

   Una vez transcurrido un período de tiempo adecuado, podrá ver las estadísticas que se han recopilado.

   >[!NOTE]
   >
   >Si la configuración se adjunta a una página que tiene páginas secundarias, estas también heredan el servicio.
