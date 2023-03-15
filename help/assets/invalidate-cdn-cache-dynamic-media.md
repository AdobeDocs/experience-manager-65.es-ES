---
title: Invalidación de la caché de la red de distribución de contenido mediante Dynamic Media
description: Invalidar el contenido en caché de la red de distribución de contenido (CDN) le permite actualizar rápidamente los recursos que entrega Dynamic Media, en lugar de esperar a que la caché caduque.
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
ht-degree: 2%

---


# Invalidación de la caché de CDN mediante Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

La CDN (red de distribución de contenido) almacena en caché los recursos de Dynamic Media para una entrega rápida a sus clientes. Sin embargo, cuando realice actualizaciones en esos recursos, desea que los cambios surtan efecto inmediatamente en el sitio web. La depuración o invalidación de la caché de la CDN permite actualizar rápidamente los recursos que envía Dynamic Media. En lugar de esperar a que la caché caduque con un valor TTL (Tiempo de vida) (el valor predeterminado es de diez horas), puede enviar una solicitud desde Dynamic Media para que la caché caduque en cuestión de minutos.



>[!IMPORTANT]
>
>Los siguientes pasos se aplican únicamente al modo Dynamic Media - Scene7 en Adobe Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) o posterior. Esta función de invalidación de la CDN también requiere que utilice la CDN predeterminada integrada en Adobe Experience Manager - Dynamic Media. Esta función no admite ninguna otra CDN personalizada.<br>Si utiliza Dynamic Media en Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) o anterior, siga los pasos que se encuentran en [Invalidación de la caché de CDN mediante Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Para invalidar el contenido en caché de la CDN para los recursos de Dynamic Media:**

*Parte 1 de 2: Creación de una plantilla de invalidación de CDN*

1. En Experience Manager 6.5.6 o posterior, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Invalidación de CDN]**.

   ![Función de validación de CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. En el **[!UICONTROL Plantilla de invalidación de CDN]** , realice una de las siguientes opciones según su escenario:

   | Escenario | Opción |
   | --- | --- |
   | Ya he creado una plantilla de invalidación de CDN en el pasado mediante Dynamic Media Classic. | El **[!UICONTROL Crear plantilla]** El campo de texto se rellena previamente con los datos de la plantilla. En este caso, puede editar la plantilla o continuar con el siguiente paso. |
   | Tengo que crear una plantilla. ¿En qué puedo participar? | En el **[!UICONTROL Crear plantilla]** , introduzca una URL de imagen (incluidos los ajustes preestablecidos o modificadores de imagen) que haga referencia a `<ID>`, en lugar de un ID de imagen específico, como en el siguiente ejemplo:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Si la plantilla contiene solo `<ID>`y luego Dynamic Media rellena `https://<publishserver_name>/is/image/<company_name>/<ID>` donde `<publishserver_name>` es el nombre del servidor de publicación que se define en Configuración general en Dynamic Media Classic. El `<company_name>` es el nombre de la raíz de la empresa asociada a esta instancia de Experience Manager, y `<ID>` son los recursos seleccionados mediante el selector de recursos que se van a invalidar.<br>Cualquier ajuste preestablecido o modificador posterior `<ID>` se copian tal cual en la definición de la URL.<br>Solo imágenes, es decir, `/is/image` - se puede formar automáticamente en función de la plantilla.<br>Para `/is/content/`Sin embargo, añadir recursos, como vídeos o PDF, mediante el selector de recursos no genera automáticamente direcciones URL. En su lugar, debe especificar estos recursos en la plantilla de invalidación de CDN o puede agregar manualmente la URL a dichos recursos en *Parte 2 de 2: Configuración de las opciones de invalidación de CDN*.<br>**Ejemplos:**<br> En este primer ejemplo, la plantilla de invalidación contiene `<ID>` junto con la URL del recurso que tiene `/is/content`. Por ejemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media forma la dirección URL en función de esta ruta, con `<ID>` son los recursos seleccionados mediante el selector de recursos que desea invalidar.<br>En este segundo ejemplo, la plantilla de invalidación contiene la dirección URL completa del recurso utilizado en las propiedades web con `/is/content` (no depende del selector de recursos). Por ejemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` donde mochila es el ID del recurso.<br>Los formatos de recurso compatibles con Dynamic Media pueden invalidarse. Tipos de archivos de recursos que son *no* entre las opciones admitidas para la invalidación de la CDN se incluyen PostScript®, PostScript® encapsulada, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word y formato de texto enriquecido.<br><br>· Cuando cree la plantilla, pero asegúrese de prestar especial atención a la sintaxis y a los errores tipográficos; Dynamic Media no realiza ninguna validación de plantilla.<br>· La plantilla de invalidación de CDN puede guardar texto de hasta 2500 caracteres.<br>· Especifique las direcciones URL para los cultivos inteligentes de imagen en esta plantilla de invalidación de la CDN o en la **[!UICONTROL Añadir URL]** campo de texto en *Parte 2: Configuración de las opciones de invalidación de CDN.*<br>· Cada entrada de una plantilla de invalidación de CDN debe estar en su propia línea.<br>· El siguiente ejemplo de plantilla de invalidación de CDN es solo para fines de demostración. |

   ![Plantilla de invalidación de CDN: crear](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >La plantilla de invalidación de CDN puede guardar texto de hasta 2500 caracteres.

1. En la esquina superior derecha de la **[!UICONTROL Plantilla de invalidación de CDN]** página, seleccione **[!UICONTROL Guardar]**, luego seleccione **[!UICONTROL OK]**.<br>

   *Parte 2 de 2: Configuración de las opciones de invalidación de CDN*
   <br>

1. En Experience Manager as a Cloud Service, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Invalidación de CDN]**.

   ![Función de validación de CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. En el **[!UICONTROL Anulación de la CDN: Añadir detalles]** , seleccione los recursos para la invalidación de la CDN.

   ![Anulación de la CDN: Añadir detalles](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Si decide dejar las opciones **[!UICONTROL Invalidar ajustes preestablecidos de imagen asociados al recurso en CDN]** *y* **[!UICONTROL Invalidar según la plantilla]** Si no se selecciona, la dirección URL base de los recursos seleccionados se forma para su invalidación. Utilice esta disposición de opciones solo para imágenes.


   | Opción | Descripción |
   | --- | --- |
   | **[!UICONTROL Anular los ajustes preestablecidos de imagen asociados a activos en la CDN]** | (Opcional) Al marcar esta opción, los recursos seleccionados y todas sus URL de ajustes preestablecidos de imagen asociadas se forman automáticamente para invalidar la caché.<br>Los recursos y sus direcciones URL predefinidas asociadas se forman automáticamente para su invalidación. Esta opción solo funciona para recursos de imagen. |
   | **[!UICONTROL Invalidación basada en plantilla]** | (Opcional) Marque esta opción para utilizar solo la plantilla definida para la formación de URL. |
   | **[!UICONTROL Añadir recursos]** | Utilice el Selector de recursos para seleccionar los recursos que desea invalidar. Puede seleccionar recursos publicados o no publicados.<br>El almacenamiento en caché en la CDN se basa en URL, no en recursos. Por lo tanto, es necesario conocer las direcciones URL completas que se encuentran en el sitio web. Después de determinar esas direcciones URL, puede agregarlas a la plantilla. A continuación, puede seleccionar y añadir esos recursos e invalidar las direcciones URL en un solo paso. <br>Utilice esta opción con **[!UICONTROL Invalidar ajustes preestablecidos de imagen asociados al recurso en CDN]**, o **[!UICONTROL Invalidación basada en plantilla]**, o ambas. |
   | **[!UICONTROL Añadir URL]** | Agregue o pegue manualmente rutas URL completas a los recursos de Dynamic Media cuya caché de CDN desee invalidar. Utilice esta opción si no ha creado una plantilla de invalidación de CDN en ***Parte 1 de 2: Creación de una plantilla de invalidación de CDN*** y solo tienen unos pocos recursos para invalidar.<br>**Importante:** Cada dirección URL que agregue debe estar en su propia línea.<br>Puede invalidar hasta 1000 direcciones URL a la vez. Si el número de direcciones URL en la **[!UICONTROL Añadir URL]** el campo de texto es bueno a 1000, no puede seleccionar **[!UICONTROL Siguiente]**. En estos casos, debe seleccionar **[!UICONTROL X]** a la derecha del recurso seleccionado o de una URL añadida manualmente para eliminarla de la lista de invalidación.<br>Especifique las direcciones URL para los cultivos inteligentes de imagen en la plantilla de invalidación de CDN o en esta **[!UICONTROL Añadir URL]** campo de texto. |

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Invalidación de CDN: confirmar]** , en la **[!UICONTROL URL]** , puede ver una lista de una o más direcciones URL generadas a partir de la plantilla de invalidación de CDN creada anteriormente y los recursos que acaba de agregar.

   Por ejemplo, con el ejemplo de la plantilla de invalidación de CDN que se mostró en los pasos anteriores, supongamos que ha agregado un solo recurso denominado `spinset`. Cuando navegue a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Invalidación de CDN]**, genera las cinco direcciones URL generadas siguientes en la variable **[!UICONTROL Invalidación de CDN: confirmar]** interfaz de usuario:

   ![Invalidación de CDN: confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Si es necesario, seleccione **X** a la derecha de una URL para eliminarla del proceso de invalidación.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Enviar]** para iniciar el proceso de invalidación de la CDN.

## Solucionar errores de invalidación de CDN

En todos los casos, se procesa todo el lote para su invalidación o se produce un error en todo el lote.

| Error | Explicación |
| --- | --- |
| *Error al recuperar las direcciones URL de los recursos seleccionados.* | Se produce si se cumple cualquiera de los siguientes escenarios:<br>- No se ha encontrado ninguna configuración de Dynamic Media.<br>: Se produce una excepción al recuperar un usuario de servicio a través del cual se lee la configuración de Dynamic Media.<br>: Falta el servidor de publicación o la raíz de la empresa utilizada para formar las direcciones URL en la configuración de Dynamic Media. |
| *Algunas direcciones URL no están definidas correctamente. Corríjalo y vuelva a enviarlo.* | Se produce si la API de invalidación de caché de la CDN de IPS devuelve un error que indica que la dirección URL hace referencia a una compañía diferente. O bien, si la dirección URL no es válida según la validación realizada por IPS `cdnCacheInvalidation` API. |
| *Error al invalidar la caché de la CDN.* | Se produce si la solicitud de invalidación de la caché de la CDN falla por cualquier otro motivo. |
| *No se ha introducido ninguna URL para invalidar.* | Se produce si no hay direcciones URL presentes en el **[!UICONTROL Invalidación de CDN: confirmar]** página y selecciona **[!UICONTROL Enviar]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
