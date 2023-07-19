---
title: Configuración del entorno de la cuenta
seo-title: Configuring Your Account Environment
description: AEM le permite configurar su cuenta y ciertos aspectos del entorno de creación
seo-description: AEM provides you with the capability to configure your account and certain aspects of the author environment
uuid: ef31be29-5c18-4dc9-ad51-fb001588b31e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b610e19c-f8d9-4ae2-b056-9fd5cf541261
docset: aem65
exl-id: 6079431d-7d08-4973-8bb4-a8d10626a795
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 63%

---

# Configuración del entorno de la cuenta  {#configuring-your-account-environment}

AEM le permite configurar su cuenta y ciertos aspectos del entorno de creación.

Mediante la opción [Usuario](/help/sites-authoring/user-properties.md#user-settings) del [encabezado](/help/sites-authoring/basic-handling.md#the-header) y el cuadro de diálogo [Mis preferencias](#userpreferences) asociado, puede modificar las opciones de usuario.

Comience por acceder a [Usuario](/help/sites-authoring/user-properties.md#user-settings) en el encabezado.

## Configuración de usuario {#user-settings}

El **Usuario** El cuadro de diálogo de configuración le permite acceder a:

* Suplantar como

   * Con el [Suplantar como](/help/sites-administering/security.md#impersonating-another-user) funcionalidad un usuario puede trabajar en nombre de otro usuario.

* Perfil

   * Ofrece un práctico enlace a su [configuración de usuario](/help/sites-administering/security.md))

* [Mis preferencias](/help/sites-authoring/user-properties.md#my-preferences)

   * Especifique las distintas preferencias exclusivas al usuario 

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### Mis preferencias {#my-preferences}

Puede acceder al cuadro de diálogo **Preferencias** a través de la opción [Usuario](/help/sites-authoring/user-properties.md#user-settings) en el encabezado.

Cada usuario puede establecer determinadas propiedades para sí mismo. 

![screen-shot_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **Idioma**

  Define el idioma que se utilizará para la interfaz de usuario del entorno de creación. Seleccione el idioma en la lista disponible.

  Esta configuración también se utiliza para la IU clásica.

* **Gestión de ventanas**

  Define el comportamiento para abrir ventanas. Seleccione:

   * **Varias ventanas** (Predeterminado)

      * Las páginas se abrirán en una nueva ventana.

   * **Ventana única**

      * Las páginas se abrirán en la ventana actual.

* **Mostrar las acciones del escritorio para Assets**

  AEM Esta opción requiere que utilice la aplicación de escritorio de la.

* **Color de anotación**

  Define el color predeterminado que se utiliza para realizar anotaciones.

   * Haga clic en el bloque de colores para abrir el selector de muestras y seleccionar un color.
   * Como alternativa, introduzca el código hexadecimal del color deseado en el campo. 

* **Presentación de fecha relativa**

  Para mejorar la legibilidad, AEM procesará las fechas dentro de los últimos siete días como fechas relativas (por ejemplo, hace tres días) y las fechas más antiguas como fechas exactas (por ejemplo, el 20 de marzo de 2017).

  Esta opción define el modo en que se muestran las fechas del sistema. Las opciones disponibles son las siguientes:

   * **Mostrar siempre la fecha exacta**: se muestra siempre la fecha exacta (nunca una fecha relativa).
   * **1 día**: se muestra la fecha relativa para las fechas dentro de un día; de lo contrario, se muestra una fecha exacta. 

   * **7 días (valor predeterminado)**: se muestra la fecha relativa para las fechas dentro de siete días; de lo contrario, se muestra una fecha exacta. 

   * **1 mes**: se muestra la fecha relativa para las fechas dentro de un mes; de lo contrario, se muestra una fecha exacta. 

   * **1 año**: se muestra la fecha relativa para las fechas dentro de un año; de lo contrario se muestra una fecha exacta. 

   * **Mostrar siempre la fecha relativa**: las fechas exactas nunca se muestran, y solo se muestran fechas relativas.

* **Habilitar métodos abreviados**

  AEM admite varios métodos abreviados del teclado para mejorar la eficiencia de la creación de contenido.

   * [Métodos abreviados del teclado para editar páginas](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [Métodos abreviados del teclado para las consolas](/help/sites-authoring/keyboard-shortcuts.md)

  Esta opción habilita los métodos abreviados de teclado. De forma predeterminada están habilitadas, pero se pueden deshabilitar, por ejemplo, si un usuario tiene ciertos requisitos de accesibilidad.

* **Usar experiencia de autoría clásica**

  Esta opción habilita [IU clásica](/help/sites-classic-ui-authoring/home.md)Creación de páginas basada en. De forma predeterminada, se utiliza la interfaz de usuario estándar.

* **Activar la página principal de los recursos**

  Esta opción solo está disponible si el administrador del sistema ha habilitado la experiencia de la página principal de los recursos para toda la organización.

* **Configuración de Stock**

  Esta opción permite especificar la configuración preferida de Adobe Stock y solo estará disponible si el administrador del sistema ha activado [Integración de Adobe Stock](/help/assets/aem-assets-adobe-stock.md).
