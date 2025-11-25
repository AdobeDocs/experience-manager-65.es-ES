---
title: Programa de instalación de parches de AEM Forms JEE
description: Aprenda a utilizar el programa de instalación de parches de AEM Forms JEE para solucionar problemas en los componentes de AEM 6.5 Forms.
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
hide: true
hidefromtoc: true
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 100%

---

# Programa de instalación de parches de AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Contacte con Asistencia](https://experienceleague.adobe.com/es?support-solution=General&support-tab=home?lang=es#support) para obtener más información o el parche.

## Acerca del programa de instalación de parches {#about-the-patch-installer}

El programa de instalación de parches de AEM 6.5 Forms JEE incluye todos los problemas corregidos para todos los componentes de AEM 6.5 Forms JEE disponibles hasta el lanzamiento de este parche. Consulte las [Notas de la versión del Service Pack](release-notes.md) más recientes para obtener una lista completa de los problemas corregidos.

## Requisitos previos para instalar el parche {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Instalación y configuración del parche {#installing-and-configuring-the-patch}

1. Realice una copia de seguridad de la carpeta &lt;*AEM_forms_root*>/deploy. Es necesaria si decide desinstalar la corrección rápida.
1. Detenga el servidor de aplicaciones.
1. Extraiga el archivo del programa de instalación del parche en el disco duro.
1. En el directorio denominado según el sistema operativo que esté utilizando:

   * **Windows**
Vaya al directorio correspondiente del medio de instalación o a la carpeta del disco duro donde copió el programa de instalación, y haga doble clic en el archivo aemforms65_cfp_install.exe.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Vaya al directorio apropiado y, desde un símbolo del sistema, escriba `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Esto inicia un asistente de instalación que le guiará a través de la instalación.

1. En el panel Introducción, haga clic en **[!UICONTROL Siguiente]**.
1. En la pantalla **Elegir carpeta de instalación**, verifique que la ubicación predeterminada que se muestra es correcta para la instalación existente, o haga clic en **[!UICONTROL Examinar]** para seleccionar la carpeta alternativa en la que los formularios de AEM estén instalados y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información de resumen de parches de corrección rápida y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información del resumen previo a la instalación y haga clic en **[!UICONTROL Instalar]**.
1. Una vez finalizada la instalación, haga clic en **[!UICONTROL Siguiente]** para aplicar las actualizaciones de correcciones rápidas a los archivos instalados.

1. **[Solo para Windows]:** Haga lo siguiente:
   * Anule la selección de la opción **Iniciar el administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Ejecute el **administrador de configuración** mediante el archivo **ConfigurationManager.bat** en `[aem-forms root]\configurationManager\bin`.

   * O anule la selección de la opción **Iniciar el administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Antes de ejecutar el **administrador de configuración** con **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, vaya al directorio *`<AEMForms_Install_Dir>\configurationManager\bin`* y reemplace **ConfigurationManager.lax** y **ConfigurationManager_IPV6.lax** por los archivos [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) y [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) más recientes, y busque y reemplace **axis-1.4.1.1.jar** por **axis-1.4.1.2.jar** en estos dos archivos.

   >[!NOTE]
   >
   >El uso del archivo **ConfigurationManager.bat** le ayuda a evitar actualizar de forma manual el nombre de los archivos .lax.
   >

1. **[Solo para usuarios basados en Unix]:**

   * La casilla de verificación **Iniciar el administrador de configuración** está seleccionada de forma predeterminada. Haga clic en **[!UICONTROL Listo]** para ejecutar el administrador de configuración al instante o, para ejecutar el **administrador de configuración** más tarde, anule la selección de la opción **Iniciar el administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Puede iniciar el **administrador de configuración** más adelante utilizando el script adecuado en el directorio `[AEM_forms_root]/configurationManager/bin`.

1. Según el servidor de aplicaciones, elija uno de los siguientes documentos y siga las instrucciones de la sección *Configuración e implementación de AEM Forms*.

   * [Instalación e implementación de AEM Forms para JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_es)
   * [Instalación e implementación de AEM Forms para WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_es)

1. (Solo JBoss®) Después de instalar el parche y configurar el servidor, elimine los directorios tmp y de trabajo del servidor de aplicaciones JBoss®.

## Configuraciones posteriores a la implementación {#post-deployment-configurations}

### Configuraciones SAML {#saml-configurations}

Si tiene configurada la autenticación SAML y tiene problemas con metadatos de IDP grandes, haga lo siguiente después de instalar el parche:

1. Establezca la siguiente propiedad del sistema en el servidor de aplicaciones:\
   `um.saml.enable.large.xml=true`
1. Reinicie el servidor.
1. Elimine los proveedores de autenticación SAML existentes y añádalos de nuevo para los dominios existentes, tal como se describe en la configuración de SAML.

>[!NOTE]
>
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

## Módulos afectados {#impacted-modules}

* Servicios de documentos
* Seguridad de los documentos
* Base JEE

[Contacto con Asistencia](https://experienceleague.adobe.com/es?support-solution=General&support-tab=home?lang=es#support)
