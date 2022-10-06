---
title: Instalador de parches JEE de AEM Forms
description: Instalador de parches JEE de AEM Forms
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 20%

---

# Instalador de parches JEE de AEM Forms {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Contacto con el servicio de asistencia](https://www.adobe.com/account/sign-in.supportportal.html) para obtener más información o para obtener el parche.

## Acerca del instalador de parches {#about-the-patch-installer}

El instalador de parches AEM 6.5 Forms JEE incluye todos los problemas corregidos para todos los componentes de AEM 6.5 Forms JEE disponibles hasta el lanzamiento de este parche. Consulte las últimas  [Notas de la versión de Service Pack](release-notes.md) para obtener una lista completa de los problemas corregidos.

## Requisitos previos para instalar el parche {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Instalación y configuración del parche {#installing-and-configuring-the-patch}

1. Haga una copia de seguridad de &lt;*AEM_forms_root*>/implementar carpeta. Es necesaria si decide desinstalar la corrección rápida.
1. Detenga el servidor de aplicaciones.
1. Extraiga el archivo del programa de instalación del parche en el disco duro.
1. En el directorio denominado según el sistema operativo que esté utilizando:

   * **Windows**
Vaya al directorio correspondiente del medio de instalación o la carpeta del disco duro donde copió el instalador y haga doble clic en el archivo aemforms65_cfp_install.exe.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**
Vaya al directorio correspondiente y, desde el símbolo del sistema, escriba 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Esto inicia un asistente de instalación que le guiará a través de la instalación.

1. En el panel Introducción, haga clic en **[!UICONTROL Siguiente]**.
1. En el **Elegir carpeta de instalación** , compruebe que la ubicación predeterminada mostrada es correcta para la instalación existente o haga clic en **[!UICONTROL Examinar]** para seleccionar la carpeta alternativa donde están instalados AEM formularios y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información de resumen de parches de corrección rápida y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información del resumen previo a la instalación y haga clic en **[!UICONTROL Instalar]**.
1. Una vez finalizada la instalación, haga clic en **[!UICONTROL Siguiente]** para aplicar las actualizaciones de correcciones rápidas a los archivos instalados.

1. **[Solo para Windows]:** Realice uno de los pasos siguientes:
   * Anule la selección de **Iniciar Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Ejecutar **Administrador de configuración** usando la variable **ConfigurationManager.bat** archivo ubicado en `[aem-forms root]\configurationManager\bin`.

   * O desmarque la opción **Iniciar Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Antes de ejecutarse **Administrador de configuración** using **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, vaya a *`<AEMForms_Install_Dir>\configurationManager\bin`* directorio y reemplazar [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) y [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) archivos.
   >[!NOTE]
   >Uso **ConfigurationManager.bat** ayuda a evitar la actualización manual del nombre de los archivos .lax.

1. **[Solo para Unix]:**

   * La variable **Iniciar Administrador de configuración** está seleccionada de forma predeterminada. Haga clic en **[!UICONTROL Listo]** para ejecutar el Administrador de configuración instantáneamente o **Administrador de configuración** más tarde, anule la selección de la opción **Iniciar Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Puede empezar **Administrador de configuración** más adelante, utilizando la secuencia de comandos adecuada en la `[AEM_forms_root]/configurationManager/bin` directorio.

1. Según el servidor de aplicaciones, elija uno de los siguientes documentos y siga las instrucciones de la sección *Configuración e implementación de AEM formularios* para obtener más información.

   * [Instalación e implementación de formularios AEM para JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Instalación e implementación de AEM formularios para WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Solo JBoss) Después de instalar el parche y configurar el servidor, elimine los directorios tmp y de trabajo del servidor de aplicaciones JBoss.

## Configuraciones posteriores a la implementación {#post-deployment-configurations}

### Configuraciones SAML {#saml-configurations}

Si tenía configurada la autenticación SAML y tiene problemas con los metadatos de IDP grandes, haga lo siguiente después de instalar el parche:

1. Establezca la siguiente propiedad del sistema en el servidor de aplicaciones:\
   `um.saml.enable.large.xml=true`
1. Reiniciar el servidor.
1. Elimine los proveedores de autenticación SAML existentes y agréguelos de nuevo para los dominios existentes, tal como se describe en la configuración de SAML.

## Módulos afectados {#impacted-modules}

* Servicios de documentos
* Document Security
* Base JEE

[Contacto con el servicio de asistencia](https://www.adobe.com/account/sign-in.supportportal.html)
