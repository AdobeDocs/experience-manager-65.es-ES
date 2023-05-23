---
title: AEM Selección de la interfaz de usuario en la
description: AEM Configure la interfaz que utilizará para trabajar en el trabajo de la interfaz de usuario de la interfaz de usuario de.
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 1%

---

# Selección de la IU{#selecting-your-ui}

Aunque la IU táctil ahora es la IU estándar y la paridad de características se ha alcanzado casi con la administración y edición de sitios, puede haber momentos en que el usuario desee cambiar a [IU clásica](/help/sites-classic-ui-authoring/classicui.md). Existen varias opciones para hacerlo.

>[!NOTE]
>
>Para obtener más información sobre el estado de la paridad de las características con la IU clásica, consulte la [Paridad de funciones de IU táctil](/help/release-notes/touch-ui-features-status.md) documento.

Hay varias ubicaciones en las que puede definir qué interfaz de usuario se va a utilizar:

* [Configuración de la interfaz de usuario predeterminada para la instancia](#configuring-the-default-ui-for-your-instance)
Esto establecerá la interfaz de usuario predeterminada que se mostrará al iniciar sesión el usuario, aunque es posible que el usuario pueda anularla y seleccionar una interfaz diferente para su cuenta o sesión actual.

* [Configuración de la creación de IU clásica para su cuenta](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
Esto establecerá la interfaz de usuario que se utilizará de forma predeterminada al editar páginas, aunque el usuario puede anularla y seleccionar otra interfaz de usuario para su cuenta o sesión actual.

* [Cambio a la IU clásica para la sesión actual](#switching-to-classic-ui-for-the-current-session)
Esto cambia a la IU clásica de la sesión actual.

* Para el caso de [Al crear páginas, el sistema realiza ciertas invalidaciones en la relación con la IU de](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Varias opciones para cambiar a la IU clásica no están disponibles de forma inmediata, sino que deben configurarse específicamente para su instancia.
>
>Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

>[!NOTE]
>
>Las instancias actualizadas desde una versión anterior conservarán la IU clásica para la creación de páginas.
>
>Después de la actualización, la creación de páginas no se cambiará automáticamente a la IU táctil, pero puede configurarla con el [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) de la **Servicio de modo de IU de creación de WCM** ( `AuthoringUIMode` service). Consulte [Anulaciones de IU del editor](#ui-overrides-for-the-editor).

## Configuración de la interfaz de usuario predeterminada para la instancia {#configuring-the-default-ui-for-your-instance}

Un administrador del sistema puede configurar la interfaz de usuario que se ve al iniciar y al iniciar sesión mediante [Asignación raíz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Esto se puede sobrescribir por los valores predeterminados de usuario o la configuración de sesión.

## Configuración de la creación de IU clásica para su cuenta {#setting-classic-ui-authoring-for-your-account}

Cada usuario puede acceder a su [preferencias de usuario](/help/sites-authoring/user-properties.md#userpreferences) para definir si desea utilizar la IU clásica para la creación de páginas (en lugar de la IU predeterminada).

Esto se puede anular mediante la configuración de la sesión.

## Cambio a la IU clásica para la sesión actual {#switching-to-classic-ui-for-the-current-session}

Al utilizar la IU táctil para escritorio, es posible que los usuarios deseen volver a la IU clásica (solo para escritorio). Existen varios métodos para cambiar a la IU clásica en la sesión actual:

* **Vínculos de navegación**

   >[!CAUTION]
   >
   >Esta opción para cambiar a la IU clásica no está disponible inmediatamente y debe configurarse específicamente para su instancia.
   >
   >
   >Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

   Si está activada, cada vez que pase el ratón sobre una consola aplicable, aparecerá un icono (símbolo de un monitor) y al pulsar o hacer clic en esta opción se abrirá la ubicación adecuada en la IU clásica.

   Por ejemplo, los vínculos de **Sites** hasta **siteadmin**:

   ![syui-01](assets/syui-01.png)

* **URL**

   Se puede acceder a la IU clásica utilizando la URL de la pantalla de bienvenida en `welcome.html`. Por ejemplo:

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
>Esta opción para cambiar a la IU clásica no está disponible inmediatamente y debe configurarse específicamente para su instancia.
>
>Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

Si está activado, **Abra la IU clásica** está disponible en el **Información de página** diálogo:

![syui-02](assets/syui-02.png)

### Anulaciones de IU del editor {#ui-overrides-for-the-editor}

El sistema puede anular la configuración definida por un usuario o un administrador del sistema en el caso de la creación de páginas.

* Al crear páginas:

   * Se fuerza el uso del editor clásico al acceder a la página mediante `cf#` en la dirección URL. Por ejemplo:
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * Se fuerza el uso del editor táctil al utilizar `/editor.html` en la dirección URL o al utilizar un dispositivo táctil. Por ejemplo:
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Cualquier forzamiento es temporal y solo es válido para la sesión del explorador

   * Se establecerá un conjunto de cookies en función de si la opción táctil está activada ( `editor.html`) o clásica ( `cf#`) se utiliza.

* Al abrir páginas mediante `siteadmin`, se comprobará la existencia de:

   * La cookie
   * Una preferencia de usuario
   * Si no existe ninguna de estas opciones, se usa de forma predeterminada la definición establecida en la variable [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) de la **Servicio de modo de IU de creación de WCM** ( `AuthoringUIMode` service).

>[!NOTE]
>
>If [un usuario ya ha definido una preferencia para la creación de páginas](#settingthedefaultauthoringuiforyouraccount), que no se anulará al cambiar la propiedad OSGi.

>[!CAUTION]
>
>Debido al uso de cookies, como ya se ha descrito, no se recomienda:
>
>* Editar manualmente la URL: una URL no estándar podría dar como resultado una situación desconocida y falta de funcionalidad.
>* Haga que ambos editores abran al mismo tiempo, por ejemplo, en ventanas independientes.

