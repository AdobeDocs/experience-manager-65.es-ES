---
title: Previsualización de recursos
description: Obtenga información sobre la previsualización de recursos en Dynamic Media
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
translation-type: tm+mt
source-git-commit: 43bf1416d9a35b979431466cc83b9baec66ae848

---


# Vista previa de recursos mediante la interfaz de software {#previewing-assets}

Puede utilizar la Previsualización para ver el aspecto que tendrá un recurso digital cargado cuando lo vea un cliente en su propio explorador web. El visor predeterminado incrustado entre dispositivos que se asigna al recurso se utiliza para la Previsualización.

Un visor es una colección de varios ajustes o &quot;ajustes preestablecidos&quot;, como el tamaño de visualización del visor, el comportamiento de zoom, las combinaciones de colores, los bordes, las fuentes, etc., que determinan la forma en que los usuarios vista los recursos de medios enriquecidos en las pantallas de sus equipos y en los dispositivos móviles.

Además de utilizar la función de Previsualización dedicada para vídeo, conjuntos de giros y conjuntos de imágenes, también puede realizar la previsualización de un recurso mediante los ajustes preestablecidos de visor que ha creado. O bien, utilice ajustes preestablecidos de imagen para previsualización de representaciones de imágenes.

* [Aplicación de ajustes preestablecidos de imagen](/help/assets/image-presets.md)
* [Aplicación de ajustes preestablecidos de visor](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Cuando se encuentra en una página web (Sites) en AEM, no puede obtener una vista previa de los recursos en el modo de **edición**. Debe ir al modo **Vista previa** haciendo clic en **Vista previa** en la esquina superior derecha.

Para activar o desactivar ajustes preestablecidos de visor en la interfaz de usuario, consulte [Gestión de ajustes preestablecidos](/help/assets/managing-viewer-presets.md)de visor.

**previsualización de recursos mediante la interfaz de usuario**

1. Desde **[!UICONTROL Adobe Experience Manager**, en la página **[!UICONTROL Navegación**, pulse **[!UICONTROL Assets]** y, a continuación, pulse **[!UICONTROL Archivos]** para acceder a los recursos.
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL List View]**.
1. (Opcional) Utilice la columna **[!UICONTROL Tipo]** para ordenar los recursos según el tipo de previsualización.
1. En la columna **[!UICONTROL Título]** , haga clic en el nombre del título (no en la imagen en miniatura) del recurso que desea previsualización.
1. Según el tipo de recurso en el que haya hecho clic, realice una de las siguientes acciones:

   <table>
    <tbody>
      <tr>
      <td><strong>Tipo de recurso en el que ha hecho clic</strong><br /> </td>
      <td><strong>¿Se puede realizar la previsualización de recursos en una representación concreta?</strong></td>
      <td><strong>¿Se puede previsualización de recursos en un visor concreto?</strong></td>
      </tr>
      <tr>
      <td><p>Imagen</p> </td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>previsualización de recursos en una representación concreta</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Representaciones </strong>en la lista y, a continuación, seleccione una representación concreta que desee previsualización.</li>
        </ul> <p><strong>previsualización de recursos en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Visores</strong> en la lista y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> <p>Utilice los iconos <strong>+</strong> y <strong>-</strong> para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Haga clic en <strong>Restablecer</strong> para devolver la imagen al zoom original.<br /> Si está en un dispositivo móvil, toque con el doble la imagen para acercarla mediante pasos. Cuando alcance el zoom máximo, toque con el doble la imagen de nuevo para restablecer el estado de zoom. Arrastre la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Multimedia</td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>previsualización de recursos en una representación concreta</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Representaciones </strong>en la lista y, a continuación, seleccione una representación concreta que desee previsualización.</li>
        </ul> <p>La selección de una representación de vídeo de mayor resolución en la previsualización puede hacer que el vídeo aparezca truncado. Esto se debe a que la previsualización de representación muestra la resolución exacta que verán los clientes, todo en el contexto del visor integrado que se utiliza para la previsualización.</p> <p>Cuando se previsualización un conjunto de vídeos adaptables en el nivel de recurso, las representaciones se agrupan en una única experiencia de reproducción. Es decir, el tamaño del vídeo adaptable es correcto para su visualización y reproducción con la mejor resolución en el contexto del dispositivo de visualización y la velocidad de conexión.<br /> </p> <p><strong>previsualización de un recurso en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Visores</strong> en la lista y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> </td>
      </tr>
      <tr>
      <td>Conjunto de imágenes</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>previsualización de un recurso en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Visores</strong> en la lista y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> <p>Utilice los iconos <strong>+</strong> y <strong>-</strong> para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Haga clic en <strong>Restablecer</strong> para devolver la imagen al zoom original.<br /> Si está en un dispositivo móvil, toque con el doble la imagen para acercarla mediante pasos. Cuando alcance el zoom máximo, toque con el doble la imagen de nuevo para restablecer el estado de zoom. Arrastre la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de giros</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>previsualización de un recurso en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Visores</strong> en la lista y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> <p>Utilice los iconos <strong>+</strong> y <strong>-</strong> para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Haga clic en <strong>Restablecer</strong> para devolver la imagen al zoom original.<br /> Si está en un dispositivo móvil, toque con el doble la imagen para acercarla mediante pasos. Cuando alcance el zoom máximo, toque con el doble la imagen de nuevo para restablecer el estado de zoom. Arrastre la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de medios mixtos</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>previsualización de un recurso en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Haga clic en <strong>Visores</strong> en la lista y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> <p>Utilice los iconos <strong>+</strong> y <strong>-</strong> para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Haga clic en <strong>Restablecer</strong> para devolver la imagen al zoom original.<br /> Si está en un dispositivo móvil, toque con el doble la imagen para acercarla mediante pasos. Cuando alcance el zoom máximo, toque con el doble la imagen de nuevo para restablecer el estado de zoom. Arrastre la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de carruseles</td>
      <td>No</td>
      <td>Sí</td>
      <td><strong>previsualización de un recurso en un visor concreto</strong>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione un visor que desee aplicar al recurso.</li>
        </ul> </td>
      </tr>
      <tr>
      <td>360 Video<br /> </td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>previsualización de recursos en una representación concreta</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, toque el icono para que aparezca la lista desplegable. Seleccione <strong>Representaciones</strong>y, a continuación, seleccione la representación que desea previsualización.</li>
        </ul> <p><strong>previsualización de recursos en un visor concreto</strong></p>
        <ul>
        <li>Cerca de la esquina superior izquierda de la página, toque el icono para que aparezca la lista desplegable. Seleccione <strong>Visores</strong>y, a continuación, seleccione un visor que desee aplicar al recurso.</li>
        </ul> <p>Utilice los iconos <strong>+</strong> y <strong>-</strong> para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Haga clic en <strong>Restablecer</strong> para devolver la imagen al zoom original.<br /> Si está en un dispositivo móvil, toque con el doble la imagen para acercarla mediante pasos. Cuando alcance el zoom máximo, toque con el doble la imagen de nuevo para restablecer el estado de zoom. Arrastre la imagen para desplazarse.</p> </td>
      </tr>
    </tbody>
    </table>

## Vista previa de recursos mediante un teclado {#keyboard-navigation-asset-preview}

1. En la interfaz de usuario de Recursos, desplácese hasta la carpeta que contenga el recurso cuya previsualización desee realizar.

1. En la carpeta, pulse la tecla `<Tab>` o las teclas de flecha del teclado para seleccionar el recurso.

1. Pulse `<Enter>` para abrir el recurso seleccionado en modo de previsualización.

1. Realice una de las acciones siguientes:
   * Para acercar, presione `<Tab>` para mover el enfoque al icono de acercar (+) y, a continuación, presione `<Enter>` una o más veces para acercarlo de forma incremental.
   * Para alejar, pulse `<Tab>` para desplazar el enfoque al icono de alejar (-) y, a continuación, pulse `<Enter>` una o varias veces para alejar gradualmente.
   * Para mover la vista de un recurso *ampliado* horizontal o verticalmente, presione las teclas de flecha correspondientes.
   * Pulse `<Shift>` + `<Tab>` para restablecer la vista y vuelva a centrar la atención en el recurso.
