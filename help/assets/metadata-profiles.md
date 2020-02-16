---
title: Perfiles de metadatos para personalizar los requisitos de metadatos de los recursos
description: Obtenga información sobre los perfiles de metadatos de los recursos. Obtenga información sobre cómo crear un perfil de metadatos y aplicarlo a los recursos de carpetas.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9658fbf8c918b9051a35e7477afa01af7722a662

---


# Metadata profiles {#metadata-profiles}

Un perfil de metadatos permite aplicar metadatos predeterminados a los recursos de una carpeta. Cree un perfil de metadatos y aplíquelo a una carpeta. Cualquier recurso que cargue posteriormente en la carpeta heredará los metadatos predeterminados configurados en el perfil de metadatos.

## Adición de un perfil de metadatos {#adding-a-metadata-profile}

1. Vaya a **[!UICONTROL Herramientas > Recursos > Perfiles]** de metadatos y toque **[!UICONTROL Crear]**.
1. Introduzca un título para el perfil de metadatos, por ejemplo Metadatos de ejemplo, y toque **[!UICONTROL Crear]**. Se muestra [!UICONTROL Editar formulario] para el perfil de metadatos.

   ![chlimage_1-197](assets/chlimage_1-480.png)

1. Haga clic en un componente y configure sus propiedades en la ficha **[!UICONTROL Configuración]** . Por ejemplo, haga clic en el componente **[!UICONTROL Descripción]** y edite sus propiedades.

   ![chlimage_1-198](assets/chlimage_1-481.png)

   Edite las siguientes propiedades para el componente **[!UICONTROL Descripción]** :

   * **[!UICONTROL Etiqueta]** de campo: el nombre para mostrar de la propiedad metadata. Solo sirve para la referencia del usuario.

   * **[!UICONTROL Asignar a propiedad]** : el valor de esta propiedad proporciona la ruta/nombre relativos al nodo del recurso donde se guarda en el repositorio. El valor siempre debe comenzar `./` porque indica que la ruta está debajo del nodo del recurso.
   ![chlimage_1-199](assets/chlimage_1-482.png)

   El valor especificado para **[!UICONTROL Asignar a propiedad]** se almacena como una propiedad en el nodo de metadatos del recurso. Por ejemplo, si especifica . `/jcr:content/metadata/dc:desc` como nombre de **[!UICONTROL Asignar a propiedad]**, Recursos AEM almacena el valor `dc:desc` en el nodo de metadatos del recurso.

   * **[!UICONTROL Valor]** predeterminado: utilice esta propiedad para agregar un valor predeterminado para el componente de metadatos. Por ejemplo, si especifica &quot;Mi descripción&quot;, este valor se asigna a la propiedad `dc:desc` en el nodo de metadatos del recurso.
   ![chlimage_1-200](assets/chlimage_1-483.png)

   >[!NOTE]
   >
   >Adición de un valor predeterminado a una nueva propiedad de metadatos (que no existe ya en la . `/jcr:content/metadata` ) no muestra la propiedad y su valor en la página Propiedades del recurso de forma predeterminada. Para ver la nueva propiedad en la página [!UICONTROL Propiedades] de los recursos, modifique el formulario de esquema correspondiente.

1. (Opcional) Agregue más componentes a Editar formulario desde la ficha **[!UICONTROL Generar formulario]** y configure sus propiedades en la ficha **[!UICONTROL Configuración]** . Las siguientes propiedades están disponibles en la ficha **[!UICONTROL Generar formulario]** :

| Componente | Propiedades |
|---|---|
| [!UICONTROL Sección de encabezado] | Etiqueta de campo, <br> descripción |
| [!UICONTROL Texto de una sola línea] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Texto con varios valores] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Número] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Fecha] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado |
| [!UICONTROL Etiquetas estándar] | Etiqueta de campo, <br> Asignar a propiedad, <br> Valor predeterminado, <br> Descripción |

![chlimage_1-201](assets/chlimage_1-484.png)

1. Toque o haga clic en **[!UICONTROL Hecho]**. El perfil de metadatos se agrega a la lista de perfiles de la página Perfiles **[!UICONTROL de]** metadatos.<br>


   ![Perfil de metadatos agregado en la página Perfiles de metadatos](assets/MetadataProfiles-page.png)

## Copiar un perfil de metadatos {#copying-a-metadata-profile}

1. En la página Perfiles **[!UICONTROL de]** metadatos, seleccione un perfil de metadatos para realizar una copia del mismo.

   ![chlimage_1-203](assets/chlimage_1-486.png)

1. Toque **[!UICONTROL Copiar]** desde la barra de herramientas.
1. En el cuadro de diálogo **[!UICONTROL Copiar perfil]** de metadatos, introduzca un título para la nueva copia del perfil de metadatos.
1. Toque **[!UICONTROL Copiar]**. La copia del perfil de metadatos aparece en la lista de perfiles de la página Perfiles **[!UICONTROL de]** metadatos.

   ![Una copia del perfil de metadatos agregado en la página Perfiles de metadatos](assets/copy-metadata-profile.png)

## Eliminar un perfil de metadatos {#deleting-a-metadata-profile}

1. En la página Perfiles **[!UICONTROL de]** metadatos, seleccione un perfil para eliminar.

   ![chlimage_1-205](assets/chlimage_1-488.png)

1. Pulse[] **[!UICONTROL Eliminar perfiles]** de metadatos en la barra de herramientas.
1. En el cuadro de diálogo, haga clic en **[!UICONTROL Eliminar]** para confirmar la operación de eliminación. El perfil de metadatos se elimina de la lista.

## Aplicar un perfil de metadatos a las carpetas {#applying-a-metadata-profile-to-folders}

Al asignar un perfil de metadatos a una carpeta, las subcarpetas heredan automáticamente el perfil de su carpeta principal. Esto significa que solo puede asignar un perfil de metadatos a una carpeta. Como tal, considere cuidadosamente la estructura de carpetas en la que carga, almacena, utiliza y archiva los recursos.

Si ha asignado un perfil de metadatos diferente a una carpeta, el nuevo perfil anula el perfil anterior. Los recursos de carpeta existentes anteriormente permanecen sin cambios. El nuevo perfil se aplica a los recursos que se agregan a la carpeta más adelante.

Las carpetas que tienen un perfil asignado se indican en la interfaz de usuario por el nombre del perfil que aparece en el nombre de la tarjeta.

![chlimage_1-205](assets/chlimage_1-489.png)

Puede aplicar perfiles de metadatos a carpetas específicas o globalmente a todos los recursos.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de metadatos existente que haya cambiado posteriormente. Consulte el artículo [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

### Aplicar perfiles de metadatos a carpetas específicas {#applying-metadata-profiles-to-specific-folders}

Puede aplicar un perfil de metadatos a una carpeta desde el menú **[!UICONTROL Herramientas]** o si está en la carpeta, desde **[!UICONTROL Propiedades]**. En esta sección se describe cómo aplicar perfiles de metadatos a las carpetas de ambos modos.

Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente que haya cambiado posteriormente. Consulte el artículo [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

#### Aplicación de perfiles de metadatos a carpetas desde la interfaz de usuario Perfiles {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Siga los pasos para aplicar el perfil de metadatos:

1. Toque el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Recursos > Perfiles]** de metadatos.
1. Seleccione el perfil de metadatos que desea aplicar a una o varias carpetas.

   ![chlimage_1-207](assets/chlimage_1-490.png)

1. Toque **[!UICONTROL Aplicar perfil de metadatos a las carpetas]** y seleccione la carpeta o varias carpetas que desee utilizar para recibir los recursos recién cargados y toque **[!UICONTROL Listo]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

#### Aplicación de perfiles de metadatos a carpetas desde Propiedades {#applying-metadata-profiles-to-folders-from-properties}

1. En el carril izquierdo, toque **[!UICONTROL Recursos]** y, a continuación, navegue a la carpeta a la que desee aplicar un perfil de metadatos.
1. En la carpeta, toque o haga clic en la marca de verificación para seleccionarla y, a continuación, toque o haga clic en **[!UICONTROL Propiedades]**.

1. Seleccione la ficha Perfiles **[!UICONTROL de]** metadatos, seleccione el perfil en el menú desplegable y toque **[!UICONTROL Guardar]**.

   ![chlimage_1-208](assets/chlimage_1-491.png)

   Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

### Aplicar un perfil de metadatos de forma global {#applying-a-metadata-profile-globally}

Además de aplicar un perfil a una carpeta, también puede aplicarlo de forma global para que cualquier contenido cargado en recursos de AEM en cualquier carpeta tenga aplicado el perfil seleccionado.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de metadatos existente que haya cambiado posteriormente. Consulte el artículo [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

**Para aplicar un perfil de metadatos de forma global, realice una de las siguientes acciones**

* Vaya a `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` y aplique el perfil adecuado y toque **[!UICONTROL Guardar]**.

   ![chlimage_1-209](assets/chlimage_1-492.png)

* Vaya a CRXDE Lite al nodo siguiente: `/content/dam/jcr:content`. Agregue la propiedad `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` y toque **Guardar todo**.

   ![chlimage_1-210](assets/chlimage_1-493.png)

## Quitar un perfil de metadatos de las carpetas {#removing-a-metadata-profile-from-folders}

Al eliminar un perfil de metadatos de una carpeta, las subcarpetas heredan automáticamente la eliminación del perfil de su carpeta principal. Sin embargo, cualquier procesamiento de archivos que se haya producido dentro de las carpetas permanece intacto.

Puede quitar un perfil de metadatos de una carpeta desde el menú **[!UICONTROL Herramientas]** o, si está en la carpeta, desde **[!UICONTROL Propiedades]**. En esta sección se describe cómo quitar perfiles de metadatos de las carpetas de ambos modos.

### Eliminar perfiles de metadatos de carpetas mediante la interfaz de usuario Perfiles {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Recursos > Perfiles]** de metadatos.
1. Seleccione el perfil de metadatos que desea eliminar de una carpeta o de varias carpetas.
1. Puntee en **[!UICONTROL Eliminar perfil de metadatos de las carpetas]** y seleccione la carpeta o varias carpetas que desee utilizar para eliminar un perfil y toque **[!UICONTROL Listo]**.

   Puede confirmar que el perfil de metadatos ya no se aplica a una carpeta porque el nombre ya no aparece debajo del nombre de la carpeta.

### Quitar perfiles de metadatos de carpetas mediante Propiedades {#removing-metadata-profiles-from-folders-via-properties}

1. Toque el logotipo de AEM, desplácese por **[!UICONTROL Recursos]** y, a continuación, por la carpeta desde la que desea quitar un perfil de metadatos.
1. En la carpeta, toque la marca de verificación para seleccionarla y, a continuación, **[!UICONTROL Propiedades]**.
1. Seleccione la ficha Perfiles **[!UICONTROL de]** metadatos, seleccione **[!UICONTROL Ninguno]** en el menú desplegable y haga clic en **[!UICONTROL Guardar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

>[!MORELIKETHIS]
>
>* [Perfiles para procesar metadatos, imágenes y vídeos](processing-profiles.md)
>* [Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles de procesamiento](/help/assets/organize-assets.md)

