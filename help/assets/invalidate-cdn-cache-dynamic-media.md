---
title: Invalidar la caché de la red de entrega de contenido mediante Dynamic Media
description: Invalide el contenido almacenado en caché de la CDN (red de entrega de contenido) para actualizar rápidamente los recursos que Dynamic Media entrega, en lugar de esperar a que caduque la caché.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: CDN Cache
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
source-git-commit: b61157b0e9afa49ef72150ae0c1703a959d154be
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 1%

---


# Invalidación de la caché de CDN mediante Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

La red de distribución de contenido (CDN) almacena en caché los recursos de Dynamic Media para su entrega rápida a sus clientes. Sin embargo, cuando actualice esos recursos, quiere que los cambios surtan efecto inmediatamente en el sitio web. La depuración o invalidación de la caché de CDN permite actualizar rápidamente los recursos que Dynamic Media entrega. En lugar de esperar a que la caché caduque con un valor TTL (Tiempo de vida) (el valor predeterminado es diez horas), puede enviar una solicitud desde Dynamic Media para que la caché caduque en cuestión de minutos.



>[!IMPORTANT]
>
>Los pasos siguientes solo se aplican al modo Dynamic Media - Scene7 en Adobe Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) o posterior. Esta función de invalidación de CDN también requiere que utilice la CDN predeterminada que se incluye con Adobe Experience Manager - Dynamic Media. Esta función no admite ninguna otra CDN personalizada.<br>Si utiliza Dynamic Media en Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) o anterior, siga los pasos que se encuentran en [Invalidación de la caché de CDN mediante Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Para invalidar el contenido almacenado en caché de CDN para los recursos de Dynamic Media:**

*Parte 1 de 2: Creación de una plantilla de invalidación de CDN*

1. En Experience Manager 6.5.6 o posterior, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Invalidación de CDN]**.

   ![Función de validación de CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. En el **[!UICONTROL Plantilla de invalidación de CDN]** , realice una de las siguientes opciones según su escenario:

   | Situación | Opción |
   | --- | --- |
   | Ya he creado una plantilla de invalidación de CDN en el pasado utilizando Dynamic Media Classic. | La variable **[!UICONTROL Crear plantilla]** el campo de texto se rellena previamente con los datos de la plantilla. En este caso, puede editar la plantilla o continuar con el siguiente paso. |
   | Tengo que crear una plantilla. ¿En qué entran? | En el **[!UICONTROL Crear plantilla]** campo de texto, introduzca una URL de imagen (incluidos los ajustes preestablecidos de imagen o los modificadores) que haga referencia a `<ID>`, en lugar de un ID de imagen específico, como en el ejemplo siguiente:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Si la plantilla contiene solo `<ID>`y, a continuación, Dynamic Media rellena `https://<publishserver_name>/is/image/<company_name>/<ID>` donde `<publishserver_name>` es el nombre del servidor de publicación que se define en Configuración general en Dynamic Media Classic. La variable `<company_name>` es el nombre de la raíz de su empresa asociada a esta instancia de Experience Manager, y `<ID>` son los recursos seleccionados mediante el selector de recursos que se van a invalidar.<br>Cualquier anuncio de modificadores/ajustes preestablecidos `<ID>` se copian tal cual en la definición de la URL.<br>Solo imágenes, es decir, `/is/image` - se puede crear automáticamente en función de la plantilla.<br>Para `/is/content/`, la adición de recursos como vídeos o PDF mediante el selector de recursos no genera automáticamente direcciones URL. En su lugar, debe especificar estos recursos en la plantilla Invalidación de CDN o puede añadir manualmente la URL a dichos activos en *Parte 2 de 2: Configuración de las opciones de invalidación de CDN*.<br>**Ejemplos:**<br> En este primer ejemplo, la plantilla de invalidación contiene `<ID>` junto con la URL del recurso que tiene `/is/content`. Por ejemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media forma la dirección URL en función de esta ruta, con `<ID>` siendo los recursos seleccionados mediante el selector de recursos que desea invalidar.<br>En este segundo ejemplo, la plantilla de invalidación contiene la dirección URL completa del recurso utilizado en las propiedades web con `/is/content` (no depende del selector de recursos). Por ejemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` donde backpack es el ID del recurso.<br>Los formatos de recurso compatibles con Dynamic Media pueden invalidarse. Tipos de archivos de recursos que *not* se admiten para invalidación de CDN como PostScript®, PostScript® encapsulada, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word y formato de texto enriquecido.<br><br>・ Cuando cree la plantilla, pero asegúrese de prestar atención a la sintaxis y los errores tipográficos; Dynamic Media no valida ninguna plantilla.<br>・ La plantilla de invalidación de CDN puede guardar texto de hasta 2500 caracteres.<br>・ Especifique direcciones URL para cultivos inteligentes de imagen en esta plantilla de invalidación de CDN o en la **[!UICONTROL Agregar URL]** campo de texto en *Parte 2: Configuración de las opciones de Invalidación de CDN.*<br>・ Cada entrada de una plantilla de Invalidación de CDN debe estar en su propia línea.<br>・ El siguiente ejemplo de plantilla de Invalidación de CDN es solo para fines de demostración. |

   ![Plantilla de invalidación de CDN: Crear](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >La plantilla de invalidación de CDN puede guardar texto de hasta 2500 caracteres.

1. En la esquina superior derecha de la variable **[!UICONTROL Plantilla de invalidación de CDN]** página, seleccione **[!UICONTROL Guardar]** y, a continuación, seleccione **[!UICONTROL OK]**.<br>

   *Parte 2 de 2: Configuración de las opciones de invalidación de CDN*
   <br>

1. En Experience Manager as a Cloud Service, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Invalidación de CDN]**.

   ![Función de validación de CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. En el **[!UICONTROL Invalidación de CDN: añadir detalles]** seleccione los recursos para la invalidación de CDN.

   ![Invalidación de CDN: añadir detalles](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Si decide dejar las opciones **[!UICONTROL Invalidar los ajustes preestablecidos de imagen asociados a recursos en CDN]** *y* **[!UICONTROL Invalidar basado en plantilla]** sin marcar, la dirección URL base de los recursos seleccionados se forma para su invalidación. Utilice esta disposición de opciones solo para imágenes.


   | Opción | Descripción |
   | --- | --- |
   | **[!UICONTROL Anular los ajustes preestablecidos de imagen asociados a activos en la CDN]** | (Opcional) Al marcar esta opción, los recursos seleccionados y todas sus URL preestablecidas de imagen asociadas se forman automáticamente para la invalidación de la caché.<br>Los recursos y sus URL predefinidas asociadas se crean automáticamente para la invalidación. Esta opción solo funciona para recursos de imagen. |
   | **[!UICONTROL Invalidación basada en plantilla]** | (Opcional) Marque esta opción para utilizar solo la plantilla definida para la formación de URL. |
   | **[!UICONTROL Añadir recursos]** | Utilice el Selector de recursos para seleccionar los recursos que desea invalidar. Puede seleccionar recursos publicados o no publicados.<br>El almacenamiento en caché en la CDN se basa en URL, no en recursos. Por lo tanto, es necesario que conozca las direcciones URL completas que se encuentran en el sitio web. Después de determinar esas direcciones URL, puede agregarlas a la plantilla. A continuación, puede seleccionar y añadir esos recursos e invalidar las direcciones URL en un solo paso. <br>Utilice esta opción con **[!UICONTROL Invalidar los ajustes preestablecidos de imagen asociados a recursos en CDN]** o **[!UICONTROL Invalidación basada en plantilla]**, o ambas. |
   | **[!UICONTROL Añadir URL]** | Agregue o pegue manualmente rutas de URL completas a los recursos de Dynamic Media cuya caché de CDN desee invalidar. Utilice esta opción si no ha creado una plantilla de invalidación de CDN en ***Parte 1 de 2: Creación de una plantilla de invalidación de CDN*** y solo tienen unos pocos recursos para invalidar.<br>**Importante:** Cada URL que agregue debe estar en su propia línea.<br>Puede invalidar hasta 1000 direcciones URL a la vez. Si el número de direcciones URL en la variable **[!UICONTROL Agregar URL]** campo de texto bueno a 1000, no puede seleccionar **[!UICONTROL Siguiente]**. En estos casos, debe seleccionar **[!UICONTROL X]** a la derecha de un recurso seleccionado o de una URL añadida manualmente para eliminarlo de la lista de invalidación.<br>Especifique direcciones URL para los cultivos inteligentes de imagen en la plantilla Invalidación de CDN o en esta **[!UICONTROL Agregar URL]** campo de texto. |

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Invalidación de CDN: Confirmar]** en la **[!UICONTROL URL]** , puede ver una lista de una o más direcciones URL generadas a partir de la plantilla de invalidación de CDN creada anteriormente y los recursos que acaba de añadir.

   Por ejemplo, si utiliza el ejemplo de Plantilla de invalidación de CDN que se mostró en los pasos anteriores, supongamos que ha añadido un único recurso denominado `spinset`. Cuando vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Invalidación de CDN]**, resulta en las siguientes cinco direcciones URL generadas en la variable **[!UICONTROL Invalidación de CDN: Confirmar]** interfaz de usuario:

   ![Invalidación de CDN: Confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Si es necesario, seleccione **X** a la derecha de una URL para eliminarla del proceso de invalidación.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Submit]** para iniciar el proceso de invalidación de CDN.

## Solución de problemas de errores de invalidación de CDN

En todos los casos, se procesa todo el lote para su invalidación o se produce un error en todo el lote.

| Error | Explicación |
| --- | --- |
| *No se pudieron recuperar las direcciones URL de los recursos seleccionados.* | Se produce si se cumple cualquiera de los siguientes escenarios:<br>- No se encuentra una configuración de Dynamic Media.<br>: Hay una excepción al recuperar un usuario de servicio a través del cual se lee la configuración de Dynamic Media.<br>- El servidor de publicación o la raíz de empresa utilizada para formar las URL no se encuentran en la configuración de Dynamic Media. |
| *Algunas direcciones URL no están definidas correctamente. Corregir y volver a enviar.* | Se produce si la API de invalidación de caché de la CDN de IPS devuelve un error que indica que la URL se refiere a una empresa diferente. O bien, si la dirección URL no es válida según la validación realizada por IPS `cdnCacheInvalidation` API. |
| *No se pudo invalidar la caché de la CDN.* | Se produce si la solicitud de invalidación de caché de CDN falla por cualquier otro motivo. |
| *No se ha introducido ninguna dirección URL para invalidar.* | Se produce si no hay direcciones URL presentes en la variable **[!UICONTROL Invalidación de CDN: Confirmar]** y seleccione **[!UICONTROL Submit]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
