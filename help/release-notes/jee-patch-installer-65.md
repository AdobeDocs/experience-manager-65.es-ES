---
title: Programa de instalación de parches de AEM Forms JEE
description: Aprenda a utilizar el Instalador de parches de AEM Forms AEM JEE para solucionar problemas en componentes de Forms de la versión 6.5 de.
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
hide: true
hidefromtoc: true
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 24%

---

# Programa de instalación de parches de AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Póngase en contacto con el servicio de asistencia](https://experienceleague.adobe.com/es?support-solution=General&amp;support-tab=home&amp;lang=es#support) para obtener más información o para obtener el parche.

## Acerca del instalador de parches {#about-the-patch-installer}

AEM El instalador de parches JEE de Forms AEM 6.5 incluye todos los problemas corregidos para todos los componentes de JEE de Forms 6.5 que están disponibles hasta el lanzamiento de este parche. Consulte las [Notas de la versión del paquete de servicio](release-notes.md) más recientes para obtener una lista completa de los problemas corregidos.

## Requisitos previos para instalar el parche {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Instalación y configuración del parche {#installing-and-configuring-the-patch}

1. AEM Realice una copia de seguridad de la carpeta &lt;*_forms_root*>/deploy. Es necesaria si decide desinstalar la corrección rápida.
1. Detenga el servidor de aplicaciones.
1. Extraiga el archivo del programa de instalación del parche en el disco duro.
1. En el directorio denominado según el sistema operativo que esté utilizando:

   * **Windows**
Vaya al directorio correspondiente del medio de instalación o a la carpeta del disco duro donde copió el programa de instalación y haga doble clic en el archivo aemforms65_cfp_install.exe.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Vaya al directorio apropiado y, desde un símbolo del sistema, escriba `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Esto inicia un asistente de instalación que le guiará a través de la instalación.

1. En el panel Introducción, haga clic en **[!UICONTROL Siguiente]**.
1. AEM En la pantalla **Elegir carpeta de instalación**, verifique que la ubicación predeterminada mostrada sea correcta para la instalación existente, o haga clic en **[!UICONTROL Examinar]** para seleccionar la carpeta alternativa en la que está instalado el formulario de y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información de resumen de parches de corrección rápida y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información del resumen previo a la instalación y haga clic en **[!UICONTROL Instalar]**.
1. Una vez finalizada la instalación, haga clic en **[!UICONTROL Siguiente]** para aplicar las actualizaciones de correcciones rápidas a los archivos instalados.

1. **[Solo para Windows]:** Haga lo siguiente:
   * Anule la selección de la opción **Iniciar el Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Ejecute **Administrador de configuración** utilizando el archivo **ConfigurationManager.bat** en `[aem-forms root]\configurationManager\bin`.

   * O anule la selección de la opción **Iniciar el Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Antes de ejecutar el **Administrador de configuración** con **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, vaya al directorio *`<AEMForms_Install_Dir>\configurationManager\bin`* y reemplace los archivos **ConfigurationManager.lax** y **ConfigurationManager_IPV6.lax** por los archivos más recientes [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) y [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax), busque y reemplace **axis-1.4.1.1.1.1.1.1 .jar** con **axis-1.4.1.2.jar** en estos dos archivos.

   >[!NOTE]
   >
   >El uso del archivo **ConfigurationManager.bat** le ayuda a evitar actualizar manualmente el nombre de los archivos .lax.
   >

1. **[Solo para usuarios basados en Unix]:**

   * La casilla de verificación **Iniciar el Administrador de configuración** está seleccionada de forma predeterminada. Haga clic en **[!UICONTROL Listo]** para ejecutar el Administrador de configuración al instante o para ejecutar el **Administrador de configuración** más tarde, anule la selección de la opción **Iniciar el Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Puede iniciar **Administrador de configuración** más tarde utilizando el script apropiado en el directorio `[AEM_forms_root]/configurationManager/bin`.

1. AEM Según el servidor de aplicaciones, elija uno de los siguientes documentos y siga las instrucciones de la sección *Configuración e implementación de formularios de la aplicación*.

   * AEM [Instalación e implementación de formularios de la aplicación para JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_es)
   * AEM [Instalación e implementación de formularios en la aplicación para WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_es)

1. (Solo JBoss®) Después de instalar el parche y configurar el servidor, elimine los directorios tmp y de trabajo del servidor de aplicaciones JBoss®.

## Configuraciones de implementación de Post {#post-deployment-configurations}

### Configuraciones de SAML {#saml-configurations}

Si tiene configurada la autenticación SAML y tiene problemas con metadatos de IDP grandes, haga lo siguiente después de instalar el parche:

1. Establezca la siguiente propiedad del sistema en el servidor de aplicaciones:\
   `um.saml.enable.large.xml=true`
1. Reinicie el servidor.
1. Elimine los proveedores de autenticación SAML existentes y agréguelos de nuevo para los dominios existentes, tal como se describe en la configuración de SAML.

>[!NOTE]
>
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

## Módulos afectados {#impacted-modules}

* Servicios de documentos
* Seguridad de los documentos
* Base JEE

[Póngase en contacto con el servicio de asistencia](https://experienceleague.adobe.com/es?support-solution=General&amp;support-tab=home&amp;lang=es#support)
