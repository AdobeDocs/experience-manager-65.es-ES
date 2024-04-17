---
title: Analytics con proveedores externos
description: Obtenga información sobre cómo configurar su propia instancia de fragmentos de Analytics genéricos para definir una nueva configuración de servicio.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# Analytics con proveedores externos {#analytics-with-external-providers}

Analytics puede proporcionarle información importante e interesante sobre el uso que se le da a su sitio web.

Hay varias configuraciones disponibles para la integración con el servicio adecuado, por ejemplo:

* [API de Rest](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

También puede configurar su propia instancia de **Fragmentos genéricos de Analytics** para definir una nueva configuración de servicio.

A continuación, la información se recopila mediante pequeños fragmentos de código que se agregan a las páginas web. Por ejemplo:

>[!CAUTION]
>
>No incluir scripts en `script` etiquetas.

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
>El sitio de demostración de Geometrixx-Outdoors está configurado de modo que los atributos proporcionados en las Propiedades de página se adjunten al código fuente html (justo encima de la variable `</html>` end (etiqueta) en el `js` script.
>
>Si su propio `/apps` no heredar del componente de página predeterminado ( `/libs/foundation/components/page`) usted (o sus desarrolladores) debe asegurarse de que las `js` los scripts se incluyen, por ejemplo, mediante lo siguiente: `cq/cloudserviceconfigs/components/servicescomponents`o utilizando un mecanismo similar.
>
>Sin esto, ninguno de los servicios (genérico, de Analytics, de Target, etc.) funcionará.

## Creación de un servicio con un fragmento de código genérico {#creating-a-new-service-with-a-generic-snippet}

Para la configuración básica:

1. Abra el **Herramientas** consola.
1. En el panel izquierdo, expanda **Configuraciones de Cloud Service**.
1. Doble clic **Fragmento de análisis genérico** para abrir la página:

   ![Fragmento de análisis genérico](assets/analytics_genericoverview.png)

1. Haga clic en + para agregar una nueva configuración mediante el cuadro de diálogo. Como mínimo, asigne un nombre, por ejemplo, Google Analytics:

   ![Crear configuración](assets/analytics_addconfig.png)

1. Clic **Crear**, el cuadro de diálogo de fragmento se abre inmediatamente: pegue el fragmento de JavaScript correspondiente en el campo:

   ![Edición del componente](assets/analytics_snippet.png)

1. Clic **OK** para guardar.

## Uso del nuevo servicio en páginas {#using-your-new-service-on-pages}

Una vez creada la configuración del servicio, debe configurar las páginas necesarias para utilizarlo:

1. Navegue hasta la página.
1. Abra el **Propiedades de página** de la barra de tareas, luego el **Cloud Service** pestaña.
1. Clic **Añadir servicio**, luego seleccione el servicio requerido. Por ejemplo, la variable **Fragmento de análisis genérico**:

   ![Añadir un servicio en la nube](assets/analytics_selectservice.png)

1. Clic **OK** para guardar.
1. Se le devolverá a la **Cloud Service** pestaña. El **Fragmento de análisis genérico** ahora aparece con el mensaje `Configuration reference missing`. Utilice la lista desplegable para seleccionar la instancia de servicio específica. Por ejemplo, google-analytics:

   ![Adición de la configuración de Cloud Service](assets/analytics_selectspecificservice.png)

1. Clic **OK** para guardar.

   Ahora, el fragmento se puede ver si ve el Origen de la página para la página.

   Una vez transcurrido un tiempo, puede ver las estadísticas recopiladas.

   >[!NOTE]
   >
   >Si la configuración se adjunta a una página que tiene páginas secundarias, estas también heredan el servicio.
