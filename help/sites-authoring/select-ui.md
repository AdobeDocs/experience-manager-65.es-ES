---
title: Seleccionar la IU
seo-title: Selecting your UI
description: Configure qué interfaz utilizará para trabajar en AEM
seo-description: Configure which interface you will use to work in AEM
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 83%

---

# Seleccionar la IU{#selecting-your-ui}

Aunque la IU táctil es ahora la IU estándar y casi se ha alcanzado la paridad de funciones con la administración y edición de sitios, es posible que a veces el usuario desee cambiar a la [IU clásica](/help/sites-classic-ui-authoring/classicui.md). Hay varias opciones para hacerlo.

>[!NOTE]
>
>Para obtener más información sobre el estado de la paridad de funciones con la interfaz clásica, consulte el documento [Paridad de funciones de la IU táctil](/help/release-notes/touch-ui-features-status.md).

Hay varias ubicaciones en las que puede definir la IU que se utilizará:

* [Configuración de la IU predeterminada para su instancia](#configuring-the-default-ui-for-your-instance) Se establecerá la IU predeterminada para que se muestre cuando el usuario inicie sesión. No obstante, el usuario puede omitir esta acción y seleccionar otra IU para su cuenta o para la sesión actual.

* [Definición de la creación en la IU clásica para su cuenta](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account): esta opción establecerá la IU que se utilizará de forma predeterminada al editar páginas, aunque el usuario puede omitir esta acción y seleccionar otra IU para su cuenta o para la sesión actual.

* [Cambio a la IU clásica para la sesión actual](#switching-to-classic-ui-for-the-current-session) Esta opción cambia a la IU clásica para la sesión actual.

* En el caso de la [creación de páginas, el sistema anula ciertas opciones de la IU](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Varias opciones para cambiar a la interfaz de usuario clásica no están disponibles de forma inmediata, ya que deben configurarse específicamente para la instancia.
>
>Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

>[!NOTE]
>
>Las instancias actualizadas de una versión anterior conservarán la IU clásica para la creación de páginas.
>
>Después de la actualización, la creación de páginas no cambiará automáticamente a la IU táctil, pero puede configurarla con el [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) del **Servicio de modo de IU de creación WCM** ( `AuthoringUIMode` ). Consulte [Omisiones de IU del editor](#ui-overrides-for-the-editor).

## Configurar la IU predeterminada para su instancia {#configuring-the-default-ui-for-your-instance}

Los administradores del sistema pueden configurar la IU que se ve al principio y en el inicio de sesión utilizando la [asignación raíz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Las opciones predeterminadas del usuario o la configuración de la sesión pueden anular estos ajustes.

## Definición de la creación en la IU clásica para su cuenta {#setting-classic-ui-authoring-for-your-account}

Cada usuario puede tener acceso a sus [preferencias de usuario](/help/sites-authoring/user-properties.md#userpreferences) para definir si desea utilizar la IU clásica para la creación de páginas (en lugar de la IU predeterminada).

La configuración de la sesión puede anular estos ajustes.

## Cambio a la IU clásica para la sesión actual {#switching-to-classic-ui-for-the-current-session}

Al utilizar la IU táctil, puede ser que los usuarios de escritorio deseen cambiar a la IU clásica (solo para escritorio). Hay varios métodos para cambiar a la IU clásica para la sesión actual:

* **Vínculos de navegación** 

   >[!CAUTION]
   >
   >Esta opción para cambiar a la interfaz de usuario clásica no está disponible de forma inmediata, ya que debe configurarse específicamente para la instancia.
   >
   >
   >Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

   Si esta opción está activada, cuando pasa el cursor sobre una consola aplicable aparece un icono (el símbolo de un monitor) que, al tocar o hacer clic en él, abre la ubicación apropiada en la IU clásica.

   Por ejemplo, los vínculos de **Sitio** a **siteadmin**: 

   ![syui-01](assets/syui-01.png)

* **URL**

   Se puede acceder a la IU clásica mediante la URL de la pantalla de bienvenida en `welcome.html`. Por ejemplo:

   `https://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >Se puede acceder a la IU táctil a través de `sites.html`. Por ejemplo:
   >
   >
   >`https://localhost:4502/sites.html`

### Cambio a la IU clásica al editar una página {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>Esta opción para cambiar a la interfaz de usuario clásica no está disponible de forma inmediata, ya que debe configurarse específicamente para la instancia.
>
>Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

Si ese acceso está activado, la opción **Abrir la interfaz de usuario clásica** está disponible en el cuadro de diálogo **Información de la página**:

![syui-02](assets/syui-02.png)

### Omisiones de IU del editor {#ui-overrides-for-the-editor}

El sistema puede anular la configuración definida por un usuario o administrador del sistema durante la creación de una página.

* Al crear páginas:

   * Se fuerza el uso del editor clásico al acceder a la página mediante `cf#` en la dirección URL. Por ejemplo:
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * Se fuerza el uso del editor táctil al utilizar `/editor.html` en la URL o cuando se utiliza un dispositivo táctil. Por ejemplo:
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Los forzados son temporales y solo son válidos para esa sesión del navegador

   * Se definirá una cookie en función de si se puede pulsar ( `editor.html`) o clásica ( `cf#`).

* Al abrir páginas mediante `siteadmin`, se buscará:

   * La cookie
   * Una preferencia de usuario
   * Si no existe ninguna de estas opciones, se pasará de forma predeterminada a las definiciones establecidas en la [configuración OSGi](/help/sites-deploying/configuring-osgi.md) del **servicio de modo de IU de creación WCM** (servicio `AuthoringUIMode`).

>[!NOTE]
>
>Si [un usuario ya ha definido una preferencia para la creación de páginas](#settingthedefaultauthoringuiforyouraccount), no se anulará al cambiar la propiedad OSGi.

>[!CAUTION]
>
>Como ya se ha descrito, debido al uso de las cookies no se recomienda:
>
>* Editar la URL de forma manual: una URL no estándar podría provocar una situación desconocida y una falta de funcionalidad.
>* Tener ambos editores abiertos al mismo tiempo: por ejemplo, en ventanas independientes.

