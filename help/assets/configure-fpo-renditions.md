---
title: Generar representaciones solo para ubicación para Adobe InDesign
description: Genere representaciones FPO de recursos nuevos y existentes mediante el flujo de trabajo de Experience Manager Assets y ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Generar representaciones solo para ubicación para Adobe InDesign {#fpo-renditions}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | Este artículo |

Cuando se colocan recursos de gran tamaño de Experience Manager en documentos de Adobe InDesign, un profesional creativo debe esperar un tiempo considerable después de enviarlos [colocar un recurso](https://helpx.adobe.com/indesign/using/placing-graphics.html). Mientras tanto, se bloquea al usuario el uso del InDesign. Esto interrumpe el flujo creativo y afecta negativamente a la experiencia del usuario. El Adobe permite colocar temporalmente representaciones de pequeño tamaño en documentos de InDesign para empezar. Cuando se requiere la salida final, por ejemplo, para los flujos de trabajo de impresión y publicación, los recursos originales de resolución completa reemplazan la representación temporal en segundo plano. Esta actualización asíncrona en segundo plano acelera el proceso de diseño para mejorar la productividad y no obstaculiza el proceso creativo.

Adobe Experience Manager AEM () proporciona representaciones que solo se utilizan para la ubicación (FPO). Estas representaciones de FPO tienen un tamaño de archivo pequeño, pero son de la misma proporción de aspecto. Si una representación de FPO no está disponible para un recurso, Adobe InDesign utiliza el recurso original en su lugar. Este mecanismo de reserva garantiza que el flujo de trabajo creativo se desarrolle sin interrupciones.

## Método para generar representaciones de FPO {#approach-to-generate-fpo-renditions}

Experience Manager permite muchos métodos para procesar imágenes que se pueden utilizar para generar las representaciones de FPO. Los dos métodos más comunes son utilizar flujos de trabajo de Experience Manager integrados y utilizar ImageMagick. Con estos dos métodos, se configura la generación de representación de los recursos recién cargados y de los recursos que existen en Experience Manager.

Puede utilizar ImageMagick para procesar imágenes, incluso para generar representaciones de FPO. Estas representaciones se reducen, es decir, las dimensiones en píxeles de la representación se reducen proporcionalmente si la imagen original tiene un PPI mayor que 72. Consulte [instalar y configurar ImageMagick para que funcione con Experience Manager Assets](best-practices-for-imagemagick.md).

|  | Uso del flujo de trabajo integrado de Experience Manager | Uso del flujo de trabajo ImageMagick | Observaciones |
|--- |--- |---|--- |
| Para nuevos recursos | Habilitar representación de FPO ([ayuda](#generate-renditions-of-new-assets-using-aem-workflow)) | Añadir la línea de comandos de ImageMagick en el flujo de trabajo del Experience Manager ([ayuda](#generate-renditions-of-new-assets-using-imagemagick)) | Experience Manager ejecuta el flujo de trabajo de recursos de actualización de DAM para cada carga. |
| Para recursos existentes | Habilitar la representación de FPO en un nuevo flujo de trabajo de Experience Manager dedicado ([ayuda](#generate-renditions-of-existing-assets-using-aem-workflow)) | Añadir la línea de comandos de ImageMagick en un nuevo flujo de trabajo de Experience Manager ([ayuda](#generate-renditions-of-existing-assets-using-imagemagick)) | Las representaciones de FPO de los recursos existentes se pueden crear bajo demanda o de forma masiva. |

>[!CAUTION]
>
>Cree los flujos de trabajo para generar representaciones modificando una copia de los flujos de trabajo predeterminados. Evita que los cambios se sobrescriban cuando se actualiza Experience Manager, por ejemplo, instalando un nuevo Service Pack.

## Generación de representaciones de nuevos recursos mediante el flujo de trabajo del Experience Manager {#generate-renditions-of-new-assets-using-aem-workflow}

A continuación se indican los pasos para configurar el modelo de flujo de trabajo de recursos de actualización de DAM para habilitar la generación de representaciones:

1. Clic **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**. Seleccionar **[!UICONTROL Recurso de actualización DAM]** y haga clic en **[!UICONTROL Editar]**.

1. Seleccionar **[!UICONTROL Procesar miniaturas]** y haga clic en **[!UICONTROL Configurar]**.

1. Clic **[!UICONTROL Representación de FPO]** pestaña. Seleccionar **[!UICONTROL Habilitar la creación de representaciones FPO]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. Ajuste de **[!UICONTROL Calidad]** y agregar o modificar **[!UICONTROL Lista de formatos]** valores según sea necesario. De forma predeterminada, la lista de tipos MIME para generar la representación de FPO es pjpeg, jpeg, jpg, gif, png, x-png y tiff. Haga clic en **[!UICONTROL Listo]**.

   >[!NOTE]
   >
   >La generación de representación es compatible con los tipos de archivo JPEG, GIF, PNG, TIFF, PSD y BMP.

1. Para activar los cambios, haga clic en **[!UICONTROL Sincronización]**.

>[!NOTE]
>
>Las imágenes de más de 1280 píxeles en un lado no conservan las dimensiones en píxeles de la representación FPO.

## Generar representaciones de nuevos recursos mediante ImageMagick {#generate-renditions-of-new-assets-using-imagemagick}

En Experience Manager, el flujo de trabajo de recursos de actualización de DAM se ejecuta cuando se carga un recurso nuevo. Para utilizar ImageMagick para procesar representaciones de recursos recién cargados, agregue un nuevo comando al modelo del flujo de trabajo.

1. Clic **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.

1. Seleccionar **[!UICONTROL Recurso de actualización DAM]** y haga clic en **[!UICONTROL Editar]**.

1. Clic **[!UICONTROL Alternar panel lateral]** en la esquina superior izquierda y busque paso de línea de comandos.

1. Arrastre el **[!UICONTROL Línea de comandos]** y agréguelo antes del **[!UICONTROL Procesar miniaturas]** paso.

1. Seleccionar **[!UICONTROL Línea de comandos]** y haga clic en **[!UICONTROL Configurar]**.

1. Añada la información que desee como personalizada **[!UICONTROL Título]** y **[!UICONTROL Descripción]**. Por ejemplo, la representación de FPO (con tecnología de ImageMagick).

1. En el **[!UICONTROL Argumentos]** pestaña, añadir relevante **[!UICONTROL Tipos MIME]** para proporcionar una lista de formatos de archivo a los que se aplica el comando.

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. En el **[!UICONTROL Argumentos]** , en la pestaña **[!UICONTROL Comandos]** , añada un comando ImageMagick relevante para generar representaciones de FPO.

   A continuación se muestra un comando de ejemplo que genera representaciones de FPO en formato JPEG, con una disminución de resolución de 72 PPP, con una configuración de calidad del 10 %, y gestiona archivos Adobe Photoshop de varias capas acoplando la salida:

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. Para activar los cambios, haga clic en **[!UICONTROL Sincronización]**.

Para obtener información detallada sobre las funciones de la línea de comandos de ImageMagick, consulte [https://imagemagick.org](https://imagemagick.org).

## Generar representaciones de recursos existentes mediante el flujo de trabajo del Experience Manager {#generate-renditions-of-existing-assets-using-aem-workflow}

Para utilizar el flujo de trabajo de Experience Manager para generar la representación de FPO de los recursos existentes, cree un modelo de flujo de trabajo de dedicado que utilice la opción de representación de FPO integrada.

1. Clic **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.

1. Para crear un modelo, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Crear modelo]**.

1. Añadir un elemento significativo **[!UICONTROL Título]** y **[!UICONTROL Nombre]**.

1. Seleccione el modelo y haga clic en **[!UICONTROL Editar]**. Clic **[!UICONTROL Información de página]** > **[!UICONTROL Abrir propiedades]**, y luego seleccione **[!UICONTROL Flujo de trabajo transitorio]**. Esto mejora la escalabilidad y el rendimiento.

1. Haga clic en ******[!UICONTROL Guardar y cerrar]**.

1. Clic **[!UICONTROL Alternar panel lateral]** en la esquina superior izquierda y busque paso de miniaturas de proceso.

1. Seleccionar **[!UICONTROL Procesar miniaturas]** y haga clic en **[!UICONTROL Configurar]**. Siga las [configuración para generar la representación de nuevos recursos mediante el flujo de trabajo del Experience Manager](#generate-renditions-of-new-assets-using-aem-workflow).

1. Para activar los cambios, haga clic en **[!UICONTROL Sincronización]**.


## Generar representaciones de recursos existentes mediante ImageMagick {#generate-renditions-of-existing-assets-using-imagemagick}

Para utilizar las capacidades de procesamiento de ImageMagick para generar la representación FPO de los recursos existentes, cree un modelo de flujo de trabajo dedicado que utilice la línea de comandos de ImageMagick para hacerlo.

1. Siga los pasos del paso 1 al paso 3 desde [configuración para generar la representación de recursos existentes mediante el flujo de trabajo del Experience Manager](#generate-renditions-of-existing-assets-using-aem-workflow) sección.

1. Siga el paso 4 al paso 8 desde [configuración para generar la representación de nuevos recursos mediante ImageMagick](#generate-renditions-of-new-assets-using-imagemagick) sección.


## Ver representaciones de FPO {#view-fpo-renditions}

Puede comprobar las representaciones de FPO generadas una vez finalizado el flujo de trabajo. En la interfaz de usuario de Experience Manager Assets, haga clic en el recurso para abrir una vista previa grande. Abra el carril izquierdo y seleccione Representaciones. También puede utilizar el método abreviado de teclado `Alt + 3` cuando la previsualización está abierta.

Clic **[!UICONTROL Representación de FPO]** para cargar su previsualización. De forma opcional, puede hacer clic con el botón derecho en la representación y guardarla en el sistema de archivos.

![rendition_list](assets/rendition_list.png)


## Sugerencias y limitaciones {#tips-limitations}

* Para utilizar la configuración basada en ImageMagick, instale ImageMagick en el mismo equipo que el Experience Manager.
* Para generar representaciones FPO de muchos recursos o de todo el repositorio, planifique y ejecute los flujos de trabajo durante la duración de poco tráfico. La generación de representaciones de FPO para un gran número de recursos es una actividad que requiere muchos recursos, y los servidores Experience Manager deben tener suficiente potencia de procesamiento y memoria disponibles.
* Para obtener información sobre rendimiento y escalabilidad, consulte [Ajustar ImageMagick](performance-tuning-guidelines.md).
* Para obtener información acerca de la administración genérica de recursos desde la línea de comandos, consulte [controlador de línea de comandos para procesar recursos](media-handlers.md).
