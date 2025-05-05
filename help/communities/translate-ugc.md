---
title: Traducción del contenido generado por el usuario
description: Descubra cómo la traducción de contenido generado por usuarios permite a los visitantes y miembros del sitio experimentar una comunidad global mediante la eliminación de las barreras lingüísticas.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# Traducción del contenido generado por el usuario {#translating-user-generated-content}

La característica de traducción para las comunidades de Adobe Experience Manager AEM () amplía el concepto de [traducción del contenido de la página](../../help/sites-administering/translation.md) al contenido generado por el usuario (UGC) publicado en los sitios de la comunidad mediante [componentes del marco de componentes sociales (SCF)](scf.md).

La traducción de UGC permite a los visitantes y miembros del sitio experimentar una comunidad global al eliminar las barreras lingüísticas.

Por ejemplo, supongamos lo siguiente:

* Un miembro de Francia publica una receta en francés en el foro comunitario de un sitio web multinacional de cocina.
* Otro miembro de Japón utiliza la función de traducción para traducir la receta del francés al japonés al déclencheur.
* Después de leer la receta en japonés, el miembro de Japón publicó un comentario en japonés.
* El miembro de Francia utiliza la función de traducción para traducir el comentario japonés al francés.
* Comunicación global.

## Información general {#overview}

Esta sección analiza específicamente cómo funciona el servicio de traducción con UGC. AEM También supone que tiene conocimientos sobre cómo conectar a un proveedor de servicios de traducción [&#128279;](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider)e integrar ese servicio en un sitio web mediante la configuración de un [marco de trabajo de integración de traducciones](../../help/sites-administering/tc-tic.md).

Cuando un proveedor de servicios de traducción está asociado con el sitio, cada copia de idioma del sitio mantiene sus propios hilos de UGC publicados a través de componentes de SCF como comentarios.

Cuando se configura una integración de traducción además del proveedor de servicios de traducción, es posible que cada copia de idioma del sitio comparta un solo hilo de UGC, lo que proporciona una comunicación global entre copias de idioma. En lugar de un hilo de discusión separado por idioma, el [almacén compartido global](#global-translation-of-ugc) configurado permite que todo el hilo sea visible independientemente de la copia de idioma que se esté viendo. Además, se pueden configurar varias configuraciones de integración de traducción que especifiquen diferentes almacenes compartidos globales para una agrupación lógica de participantes globales, como por regiones.

## El servicio de traducción predeterminado {#the-default-translation-service}

AEM Communities incluye una [licencia de prueba](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) para un [servicio de traducción predeterminado](../../help/sites-administering/tc-msconf.md) habilitado para varios idiomas.

Al [crear un sitio de la comunidad](sites-console.md), el servicio de traducción predeterminado se habilita al comprobar `Allow Machine Translation` desde el subpanel [TRADUCCIÓN](sites-console.md#translation).

>[!CAUTION]
>
>El servicio de traducción predeterminado es solo para demostración.
>
>Para un sistema de producción, se requiere un servicio de traducción con licencia. Si no tiene licencia, el servicio de traducción predeterminado debería estar [desactivado](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Traducción global de UGC {#global-translation-of-ugc}

Cuando un sitio web tiene varias [copias de idioma](../../help/sites-administering/tc-prep.md), el servicio de traducción predeterminado no reconoce que el UGC introducido en un sitio puede estar relacionado con el UGC introducido en otro. Esto ocurre cuando el UGC lo genera el mismo componente (la copia de idioma de la página que contiene el componente).

Es similar a grupos de personas que tratan un tema. No son conscientes de los comentarios que se hacen en grupos distintos a los suyos, en comparación con todos en un grupo grande que participan en una conversación.

Si se desea &quot;una conversación en grupo&quot;, es posible habilitar la traducción global en un sitio web con varias copias de idioma, de modo que todo el hilo sea visible independientemente de la copia de idioma que se esté viendo.

Por ejemplo, si se establece un foro en el sitio base, se crean copias de idioma y se habilita la traducción global, aparecerá en todas las copias de idioma un tema publicado en el foro en una copia de idioma. Lo mismo sucedería con cualquier respuesta, independientemente de la copia de idioma en la que se haya introducido la respuesta. El resultado sería que el tema y todo su hilo de respuestas serían visibles independientemente de la copia de idioma desde la que se visualice el tema.

>[!CAUTION]
>
>Cualquier UGC que existiera antes de la traducción global ya no es visible.
>
>Aunque el UGC todavía está en el [almacén común](working-with-srp.md), se encuentra en la ubicación del UGC específica del idioma, mientras que el nuevo contenido, agregado después de que se haya configurado la traducción global, se está recuperando de la ubicación del almacén compartido global.
>
>No hay ninguna herramienta de migración para mover o combinar contenido específico del idioma en el almacén compartido global.

### Configuración de integración de traducción {#translation-integration-configuration}

Para crear una integración de traducción, que integre un conector de servicio de traducción con el sitio web de la instancia de autor:

* Iniciar sesión como administrador
* Desde el [menú principal](http://localhost:4502/)
* Seleccionar **[!UICONTROL herramientas]**
* Seleccionar **[!UICONTROL operaciones]**
* Seleccionar **[!UICONTROL nube]**
* Seleccionar **[!UICONTROL Cloud Service]**
* Desplácese hacia abajo hasta **[!UICONTROL Integración de traducción]**

  ![integración de traducción](assets/translation-integration.png)

* Seleccionar **[!UICONTROL Mostrar configuraciones]**

  ![mostrar-configuración](assets/translation-integration1.png)

* Seleccione el icono `[+]` junto a **[!UICONTROL Configuraciones disponibles]** para poder crear una configuración.

#### Cuadro de diálogo Crear configuración {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL Configuración principal]**

  (Obligatorio) Normalmente, dejar como predeterminado. El valor predeterminado es `/etc/cloudservices/translation`.

* **[!UICONTROL Título]**

  (Obligatorio) Introduzca un título para mostrar de su elección. No hay valor predeterminado.

* **[!UICONTROL Nombre]**

  (Opcional) Introduzca un nombre para la configuración. De forma predeterminada, es un nombre de nodo basado en el Título.

* Seleccionar **[!UICONTROL Crear]**

#### Cuadro de diálogo Configuración de traducción {#translation-config-dialog}

![diálogo de configuración](assets/translation-integration3.png)

Para obtener instrucciones detalladas, consulte [Creación de una configuración de integración de traducción](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration).

* Pestaña **[!UICONTROL Sitios]**: puede dejar los valores predeterminados.

* Ficha **[!UICONTROL Communities]**:
   * **[!UICONTROL Proveedor de traducción]**
Seleccione el proveedor de traducción de la lista desplegable. El valor predeterminado es `microsoft`, el servicio de prueba.

   * **[!UICONTROL Categoría de contenido]**
Seleccione una categoría que describa el contenido que se está traduciendo. El valor predeterminado es `General.`

   * **[!UICONTROL Elegir Una Configuración Regional...]**
(Opcional) Al seleccionar una configuración regional para almacenar UGC, las publicaciones de todas las copias de idioma aparecen en una conversación global. Por convención, elija la configuración regional del [idioma base](sites-console.md#translation) del sitio web. Al elegir `No Common Store`, se deshabilita la traducción global. De forma predeterminada, la traducción global está desactivada.

* Pestaña **[!UICONTROL Assets]**: puede dejar los valores predeterminados.
* Seleccionar **[!UICONTROL Aceptar]**

#### Activación {#activation}

El nuevo servicio en la nube de integración de traducciones debe activarse en el entorno de Publish. Cuando se asocia con un sitio web, si aún no se ha activado, el flujo de trabajo de activación le solicita que publique esta configuración del servicio en la nube cuando se publique la página con la que está asociado.

## Administración de configuración de traducción {#managing-translation-settings}

>[!NOTE]
>
>**Idioma preferido**
>
>Al detectar si la publicación está en un idioma diferente al idioma preferido, se debe establecer el idioma preferido del visitante del sitio.
>
>El idioma preferido es la preferencia de idioma establecida en el perfil de un usuario, cuando el visitante del sitio ha iniciado sesión y ha especificado una preferencia de idioma.
>
>Cuando el visitante del sitio es anónimo o no ha especificado una preferencia de idioma en su perfil, el idioma preferido es el idioma base de la plantilla de página.

### Preferencia de usuario {#user-preference}

#### Perfil de usuario {#user-profile}

Todos los sitios de comunidades proporcionan un perfil de usuario que los miembros que han iniciado sesión pueden editar para identificarse ante la comunidad y establecer sus preferencias.

Una de estas opciones es mostrar siempre el contenido de la comunidad en el idioma que prefieran. De forma predeterminada, la configuración no está establecida y el valor predeterminado es la configuración del sistema. El usuario puede cambiar el ajuste a Activado o Desactivado para anular el ajuste del sistema.

Cuando las páginas se traducen automáticamente al idioma preferido del usuario, la interfaz de usuario para mostrar el texto original y mejorar la traducción sigue estando disponible.

![perfil de usuario](assets/translation-integration4.png)

### Configuración del sitio de comunidad {#community-site-setting}

Cuando se crea un sitio de la comunidad, se puede activar y configurar la opción de traducción. La configuración de traducción está en vigor para el contenido que los visitantes anónimos del sitio pueden ver, pero la configuración del perfil del usuario la anula.
