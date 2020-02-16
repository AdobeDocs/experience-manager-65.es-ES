---
title: Previsualización de recursos
description: Obtenga información sobre cómo obtener una vista previa de recursos en Dynamic Media
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Previewing assets{#previewing-assets}

Puede utilizar Vista previa para ver el aspecto que tendrá un recurso digital cargado cuando lo vea un cliente en su propio navegador web. El visor predeterminado incrustado entre dispositivos que se asigna al recurso se utiliza para la vista previa.

Un visor es una colección de varios ajustes o &quot;ajustes preestablecidos&quot;, como el tamaño de visualización del visor, el comportamiento de zoom, las combinaciones de colores, los bordes, las fuentes, etc., que determinan la forma en que los usuarios ven los recursos de medios enriquecidos en las pantallas de sus equipos y en los dispositivos móviles.

Además de utilizar la función de vista previa dedicada para vídeo, conjuntos de giros y conjuntos de imágenes, también puede obtener una vista previa de un recurso mediante los ajustes preestablecidos de visor que ha creado. O bien, utilice ajustes preestablecidos de imagen para previsualizar las representaciones de imágenes.

* [Aplicación de ajustes preestablecidos de imagen](/help/assets/image-presets.md)
* [Aplicación de ajustes preestablecidos de visor](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Cuando se encuentra en una página web (Sitios) en AEM, no puede obtener una vista previa de los recursos en el modo de **edición** . Debe ir al modo **Vista previa** haciendo clic en **Vista previa** en la esquina superior derecha.

Para activar o desactivar ajustes preestablecidos de visor en la interfaz de usuario, consulte [Gestión de ajustes preestablecidos](/help/assets/managing-viewer-presets.md)de visor.

**Para previsualizar recursos**

1. En **[!UICONTROL Adobe Experience Manager**, en la página de navegación **de** [!UICONTROL, toque **[!UICONTROL Recursos]** y, a continuación, **[!UICONTROL Archivos]** para acceder a los recursos.
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL List View]**.
1. (Opcional) Utilice la columna **[!UICONTROL Tipo]** para ordenar los recursos según el tipo de vista previa.
1. En la columna **[!UICONTROL Título]** , haga clic en el nombre del título (no en la imagen en miniatura) del recurso cuya vista previa desee obtener.
1. Según el tipo de recurso en el que haya hecho clic, realice una de las siguientes acciones:

   <table>
    <tbody>
      <tr>
      <td><strong>Tipo de recurso en el que ha hecho clic</strong><br /> </td>
      <td><strong>¿Se puede obtener una vista previa del recurso en una representación concreta?</strong></td>
      <td><strong>¿Se puede obtener una vista previa del recurso en un visor concreto?</strong></td>
      </tr>
      <tr>
      <td><p>Imagen</p> </td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>Vista previa del recurso en una representación concreta</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Representaciones </strong>en la lista y, a continuación, seleccione una representación concreta que desee previsualizar.</li>
        </ul> <p><strong>Para obtener una vista previa del recurso en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Visores</strong> en la lista y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> <p>Utilice los <strong>+</strong> y <strong>- </strong>iconos para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Haga clic en <strong>Restablecer</strong> para devolver la imagen al zoom original.<br /> Si está en un dispositivo móvil, toque dos veces la imagen para acercarla mediante pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado de zoom. Arrastre la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Multimedia</td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>Vista previa del recurso en una representación concreta</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Representaciones </strong>en la lista y, a continuación, seleccione una representación concreta que desee previsualizar.</li>
        </ul> <p>La selección de una representación de vídeo de mayor resolución para previsualizar puede hacer que el vídeo aparezca truncado. Esto se debe a que la vista previa de la representación muestra la resolución exacta que verán los clientes, todo en el contexto del visor integrado que se utiliza para la vista previa.</p> <p>Al obtener una vista previa de un conjunto de vídeos adaptables en el nivel de recurso, las representaciones se agrupan en una única experiencia de reproducción. Es decir, el tamaño del vídeo adaptable es correcto para su visualización y reproducción con la mejor resolución en el contexto del dispositivo de visualización y la velocidad de conexión.<br /> </p> <p><strong>Vista previa de un recurso en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Visores</strong> en la lista y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> </td>
      </tr>
      <tr>
      <td>Conjunto de imágenes</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Vista previa de un recurso en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Visores</strong> en la lista y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> <p>Utilice los <strong>+</strong> y <strong>- </strong>iconos para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Haga clic en <strong>Restablecer</strong> para devolver la imagen al zoom original.<br /> Si está en un dispositivo móvil, toque dos veces la imagen para acercarla mediante pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado de zoom. Arrastre la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de giros</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Vista previa de un recurso en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Visores</strong> en la lista y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> <p>Utilice los <strong>+</strong> y <strong>- </strong>iconos para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Haga clic en <strong>Restablecer</strong> para devolver la imagen al zoom original.<br /> Si está en un dispositivo móvil, toque dos veces la imagen para acercarla mediante pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado de zoom. Arrastre la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de medios mixtos</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Vista previa de un recurso en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Visores</strong> en la lista y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> <p>Utilice los <strong>+</strong> y <strong>- </strong>iconos para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Haga clic en <strong>Restablecer</strong> para devolver la imagen al zoom original.<br /> Si está en un dispositivo móvil, toque dos veces la imagen para acercarla mediante pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado de zoom. Arrastre la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de carruseles</td>
      <td>No</td>
      <td>Sí</td>
      <td><strong>Vista previa de un recurso en un visor concreto</strong>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione un visor que desee aplicar al recurso.</li>
        </ul> </td>
      </tr>
      <tr>
      <td>360 Video<br /> </td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>Vista previa del recurso en una representación concreta</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, toque el icono para que aparezca la lista desplegable. Seleccione <strong>Representaciones</strong>y, a continuación, seleccione la representación cuya vista previa desee obtener.</li>
        </ul> <p><strong>Para obtener una vista previa del recurso en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, toque el icono para que aparezca la lista desplegable. Seleccione <strong>Visores</strong>y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> <p>Utilice los <strong>+</strong> y <strong>- </strong>iconos para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Haga clic en <strong>Restablecer</strong> para devolver la imagen al zoom original.<br /> Si está en un dispositivo móvil, toque dos veces la imagen para acercarla mediante pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado de zoom. Arrastre la imagen para desplazarse.</p> </td>
      </tr>
    </tbody>
    </table>
