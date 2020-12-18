---
title: Uso de conjuntos de reglas para transformar direcciones URL
description: Puede implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritos en un lenguaje de secuencias de comandos (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones.
uuid: 9fed0c83-67b7-4483-a9b4-322e6a483449
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: abcff903-204b-4ab6-87d8-6f0ce63d7b41
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 5%

---


# Uso de conjuntos de reglas para transformar direcciones URL {#using-rulesets-to-transform-urls}

Puede implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritos en un lenguaje de secuencias de comandos (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones. Cada regla consta de al menos una condición y una acción. Una regla evalúa los datos XML según las condiciones y, si se cumple una condición, toma la acción adecuada. Algunos ejemplos de conjuntos de reglas son:

* Añadiendo un sufijo de tipo MIME. Muchos servicios y sitios Web requieren sufijos de imagen, como agregar `.jpg` a una dirección URL.
* Creación de una ruta de carpeta a la dirección URL para fines de optimización de motores de búsqueda (SEO).

   Consulte [Compatibilidad de Adobe Dynamic Media Classic con SEO](/help/assets/assets/s7_seo.pdf).

* Añadir metadatos a la dirección URL para fines de optimización de motores de búsqueda (SEO).

   Consulte [Compatibilidad de Adobe Dynamic Media Classic con SEO](/help/assets/assets/s7_seo.pdf).

* Configuración de la disposición del contenido para activar una descarga.
* Simplifique las direcciones URL de plantilla del servicio de imágenes para su personalización. Por ejemplo: convierta `rgb{XX,YY,ZZ}` en el `\redXX\greenYY\blueZZ` listo para RTF

* Solicite que se codifiquen determinados caracteres, como `$`, `{` y `}`, y que se descodifiquen determinados caracteres para ImageServer. Por ejemplo, Facebook no funciona bien con las direcciones URL que contienen caracteres especiales.

   Consulte [Eliminación de caracteres especiales de las direcciones URL](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

En el contexto de Dynamic Media, los sitios web que utilizan un sistema basado en XML para administrar la información de los recursos pueden cargar archivos XML a Dynamic Media. Puede designar uno de estos archivos como archivo de conjunto de reglas de preprocesamiento para servir recursos de Dynamic Media. Este archivo reestructura el formato de protocolo de URL estándar para satisfacer la lógica comercial de los sistemas que se integran con Dynamic Media. Especifique un archivo XML que sirva como ruta de archivo de definiciones de conjunto de reglas.

>[!CAUTION]
>
>Tenga precaución al utilizar conjuntos de reglas; pueden evitar que el contenido de Dynamic Media se muestre en el sitio web.

Hay disponibles conjuntos de reglas de ejemplo que pueden ayudarle a crear su propio conjunto de reglas.
Consulte [Referencia del conjunto de reglas](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Al igual que con la creación de todos los conjuntos de reglas, asegúrese de que el archivo XML sea válido antes de cargarlo mediante un programa de validador XML como xmlvalid.
Consulte también [Resolución de problemas de conjuntos de reglas](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Además, asegúrese de probar primero el conjunto de reglas en un entorno de ensayo que no afecte al entorno de producción activo.
Los entornos de producción y los entornos de ensayo generalmente requieren inicios de sesión diferentes.

Consulte la aplicación de escritorio [Adobe Dynamic Media Classic para obtener información de inicio de sesión](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Consulte también [Uso de la imagen &#39;asset&#39; en lugar de &#39;is&#39; en un conjunto de reglas](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Para implementar conjuntos de reglas XML:**

1. Inicie sesión en su cuenta de Dynamic Media Classic:

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Adobe proporcionó las credenciales y el inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con el servicio de asistencia técnica.

1. Cargue el archivo del conjunto de reglas haciendo lo siguiente:

   * En la barra de navegación global, haga clic en **[!UICONTROL Cargar]**.
   * En la página **[!UICONTROL Cargar]**, cerca de la esquina superior izquierda, haga clic en **[!UICONTROL Examinar]**.
   * En el cuadro de diálogo **[!UICONTROL Abrir]**, busque el archivo del conjunto de reglas (XML).
   * Seleccione el archivo y haga clic en **[!UICONTROL Abrir]**.
   * En la parte derecha de la página **[!UICONTROL Cargar]**, seleccione una carpeta de destino para el archivo del conjunto de reglas.
   * Cerca de la parte inferior de la página, asegúrese de que **[!UICONTROL Publicar después de cargar]** está marcado.
   * En la esquina inferior derecha de la página, haga clic en **[!UICONTROL Enviar carga]**.
   * En la barra de navegación global, haga clic en **[!UICONTROL Trabajos]** para comprobar el estado del trabajo de carga. Cuando la columna **[!UICONTROL Estado]** de la página **[!UICONTROL Trabajo]** indica Carga finalizada, continúe con los pasos siguientes.

1. En la barra de navegación situada cerca de la parte superior de la página, haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Ajustes de publicación > Servidor de imágenes]**.
1. En la página **[!UICONTROL Publicación del servidor de imágenes]**, en el grupo **[!UICONTROL Administración de catálogos]**, busque **[!UICONTROL Ruta del archivo de definición de conjunto de reglas]** y haga clic en **[!UICONTROL Seleccionar]**.
1. En la página **[!UICONTROL Seleccionar archivo de definición de conjunto de reglas (XML)]**, busque el archivo de conjunto de reglas y, en la esquina inferior derecha de la página, haga clic en **[!UICONTROL Seleccionar]**.
1. En la esquina inferior derecha de la página Configuración, haga clic en **[!UICONTROL Cerrar]**.
1. Ejecute un trabajo de publicación de Image Server.

   Las condiciones del conjunto de reglas se aplican en las solicitudes a los servidores de imágenes de Dynamic Media activos.

   Si realiza cambios en el archivo del conjunto de reglas, los cambios se aplican inmediatamente al volver a cargar y publicar el archivo del conjunto de reglas actualizado.

