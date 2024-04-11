---
title: AEM Selección de la interfaz de usuario en la
description: Configure la interfaz que utilizará para trabajar en Adobe Experience Manager 6.5.
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 1%

---

# Selección de la IU{#selecting-your-ui}

La IU táctil de Adobe Experience Manager AEM () ahora es la IU estándar y la paridad de características casi se ha alcanzado con la administración y edición de sitios. Sin embargo, puede haber ocasiones en que el usuario desee cambiar al [IU clásica](/help/sites-classic-ui-authoring/classicui.md). Existen varias opciones para hacerlo.

>[!NOTE]
>
>Para obtener más información sobre el estado de la paridad de las características con la IU clásica, consulte la [Paridad de funciones de IU táctil](/help/release-notes/touch-ui-features-status.md) documento.

Hay varias ubicaciones en las que puede definir qué interfaz de usuario se va a utilizar:

* [Configuración de la interfaz de usuario predeterminada para la instancia](#configuring-the-default-ui-for-your-instance)
Esto establece la interfaz de usuario predeterminada para mostrar al iniciar sesión el usuario. El usuario puede anular esto y seleccionar una interfaz de usuario diferente para su cuenta o sesión actual.

* [Configuración de la creación de IU clásica para su cuenta](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
Esto establece que la interfaz de usuario sea la predeterminada al editar páginas, aunque el usuario puede anularla y seleccionar una interfaz de usuario diferente para su cuenta o sesión actual.

* [Cambio a la IU clásica para la sesión actual](#switching-to-classic-ui-for-the-current-session)
Cambia a la IU clásica para la sesión actual.

* Para el caso de [Durante la creación de páginas, el sistema realiza ciertas anulaciones en la relación con la interfaz de usuario de](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Varias opciones para cambiar a la IU clásica no están disponibles de forma inmediata, sino que deben configurarse para su instancia.
>
>Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

>[!NOTE]
>
>Las instancias actualizadas desde una versión anterior conservan la IU clásica para la creación de páginas.
>
>Después de la actualización, la creación de páginas no cambia automáticamente a la IU táctil, pero puede configurarla con el [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) de la **Servicio de modo de IU de creación de WCM** ( `AuthoringUIMode` service). Consulte [Anulaciones de IU del editor](#ui-overrides-for-the-editor).

## Configuración de la interfaz de usuario predeterminada para la instancia {#configuring-the-default-ui-for-your-instance}

Un administrador del sistema puede configurar la interfaz de usuario que se ve al iniciar y al iniciar sesión mediante [Asignación raíz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Esto se puede sobrescribir por los valores predeterminados de usuario o la configuración de sesión.

## Configuración de la creación de IU clásica para su cuenta {#setting-classic-ui-authoring-for-your-account}

Cada usuario puede acceder a su propio [preferencias de usuario](/help/sites-authoring/user-properties.md#userpreferences) para definir si desean utilizar la IU clásica para la creación de páginas, en lugar de la IU predeterminada.

Esto se puede anular mediante la configuración de la sesión.

## Cambio a la IU clásica para la sesión actual {#switching-to-classic-ui-for-the-current-session}

Al utilizar la IU táctil, es posible que los usuarios de escritorio deseen volver a la IU clásica (solo de escritorio). Existen varios métodos para cambiar a la IU clásica en la sesión actual:

* **Vínculos de navegación**

  >[!CAUTION]
  >
  >Esta opción para cambiar a la IU clásica no está disponible de forma inmediata, debe configurarse para su instancia.
  >
  >
  >Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

  Si está activada, cada vez que pase el ratón sobre una consola aplicable, aparecerá un icono (un símbolo de monitor). Al tocar o hacer clic en esta opción, se abre la ubicación adecuada en la IU clásica.

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
>Esta opción para cambiar a la IU clásica no está disponible de forma inmediata, debe configurarse para su instancia.
>
>Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

Si está activado, **Abra la IU clásica** está disponible en el **Información de página** diálogo:

![syui-02](assets/syui-02.png)

### Anulaciones de IU del editor {#ui-overrides-for-the-editor}

El sistema puede anular la configuración definida por un usuario o un administrador del sistema si existe la creación de páginas.

* Al crear páginas:

   * Se fuerza el uso del editor clásico al acceder a la página mediante `cf#` en la dirección URL. Por ejemplo:
     `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * Se fuerza el uso del editor táctil al utilizar `/editor.html` en la dirección URL o al utilizar un dispositivo táctil. Por ejemplo:
     `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Cualquier forzamiento es temporal y solo es válido para la sesión del explorador

   * Se establece un conjunto de cookies en función de si la opción táctil está activada ( `editor.html`) o clásica ( `cf#`) se utiliza.

* Al abrir páginas mediante `siteadmin`, se comprueba la existencia de lo siguiente:

   * La cookie
   * Una preferencia de usuario
   * Si no existe, el valor predeterminado son las definiciones establecidas en la variable [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) de la **Servicio de modo de IU de creación de WCM** ( `AuthoringUIMode` service).

>[!NOTE]
>
>If [un usuario ya ha definido una preferencia para la creación de páginas](#settingthedefaultauthoringuiforyouraccount), que no se anula al cambiar la propiedad OSGi.

>[!CAUTION]
>
>Debido al uso de cookies, como ya se ha descrito, no se recomienda:
>
>* Editar manualmente la URL: una URL no estándar podría dar como resultado una situación desconocida y falta de funcionalidad.
>* Haga que ambos editores abran al mismo tiempo, por ejemplo, en ventanas independientes.
