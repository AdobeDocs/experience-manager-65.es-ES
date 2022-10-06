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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 4%

---

# Analytics con proveedores externos {#analytics-with-external-providers}

Analytics puede proporcionarle información importante e interesante sobre cómo se utiliza su sitio web.

Hay varias configuraciones listas para usar que se pueden integrar con el servicio adecuado, por ejemplo:

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

También puede configurar su propia instancia de **Fragmentos genéricos de Analytics** para definir una nueva configuración de servicio.

La información se recopila mediante pequeños fragmentos de código que se agregan a las páginas web. Por ejemplo:

>[!CAUTION]
>
>Las secuencias de comandos no se deben incluir en `script` etiquetas.

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

Estos fragmentos permiten recopilar datos y generar informes. Los datos reales recopilados dependen del proveedor y del fragmento de código real utilizado. Algunas estadísticas de ejemplo son:

* cuántos visitantes a lo largo del tiempo
* cuántas páginas visitaron
* términos de búsqueda utilizados
* páginas de aterrizaje

>[!CAUTION]
>
>El sitio de demostración de Geometrixx al aire libre está configurado para que los atributos proporcionados en las Propiedades de página se adjunten al código fuente html (justo encima de la `</html>` endtag) en el `js` secuencia de comandos.
>
>Si su `/apps` no heredar del componente de página predeterminado ( `/libs/foundation/components/page`) usted (o sus desarrolladores) deben asegurarse de que el `js` se incluyen las secuencias de comandos, por ejemplo, incluyendo `cq/cloudserviceconfigs/components/servicescomponents`o utilizando un mecanismo similar.
>
>Sin esto, ninguno de los servicios (Genérico, Analytics, Target, etc.) funcionará.

## Creación de un nuevo servicio con un fragmento genérico {#creating-a-new-service-with-a-generic-snippet}

Para la configuración básica:

1. Abra el **Herramientas** consola.
1. Expandir desde el panel izquierdo **Configuraciones de Cloud Services**.
1. Haga doble clic en **Fragmento genérico de Analytics** para abrir la página:

   ![](assets/analytics_genericoverview.png)

1. Haga clic en + para añadir una nueva configuración mediante el cuadro de diálogo; como mínimo, asigne un nombre, por ejemplo google analytics:

   ![](assets/analytics_addconfig.png)

1. Haga clic en **Crear**, el cuadro de diálogo de fragmento se abrirá inmediatamente y pegue el fragmento de javascript correspondiente en el campo :

   ![](assets/analytics_snippet.png)

1. Haga clic en **Aceptar** para guardar.

## Uso del nuevo servicio en las páginas {#using-your-new-service-on-pages}

Después de crear la configuración del servicio, debe configurar las páginas necesarias para utilizarla:

1. Vaya a la página .
1. Abra el **Propiedades de página** desde la barra de tareas y, a continuación, la variable **Cloud Services** pestaña .
1. Haga clic en **Añadir servicio** y, a continuación, seleccione el servicio requerido; por ejemplo, la variable **Fragmento genérico de Analytics**:

   ![](assets/analytics_selectservice.png)

1. Haga clic en **Aceptar** para guardar.
1. Volverá a la **Cloud Services** pestaña . La variable **Fragmento genérico de Analytics** ahora aparece en la lista con el mensaje `Configuration reference missing`. Utilice la lista desplegable para seleccionar la instancia de servicio específica; por ejemplo google-analytics:

   ![](assets/analytics_selectspecificservice.png)

1. Haga clic en **Aceptar** para guardar.

   Ahora se puede ver el fragmento si se ve el origen de la página para la página.

   Una vez transcurrido un período de tiempo adecuado, podrá ver las estadísticas que se han recopilado.

   >[!NOTE]
   >
   >Si la configuración está adjunta a una página que tiene páginas secundarias, también las heredan.
