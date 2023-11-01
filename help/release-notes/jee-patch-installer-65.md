---
title: Programa de instalación de parches de AEM Forms JEE
description: Aprenda a utilizar el Instalador de parches de AEM Forms AEM JEE para solucionar problemas en componentes de Forms de la versión 6.5 de.
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: f0b59ff25f49f5ca12bc6966882f68b5231a9511
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 24%

---

# Programa de instalación de parches de AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Atención al cliente](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home&amp;lang=es#support) para obtener más información o para obtener el parche.

## Acerca del instalador de parches {#about-the-patch-installer}

AEM El instalador de parches JEE de Forms AEM 6.5 incluye todos los problemas corregidos para todos los componentes de JEE de Forms 6.5 que están disponibles hasta el lanzamiento de este parche. Consulte las últimas  [Notas de la versión de Service Pack](release-notes.md) para obtener una lista completa de los problemas corregidos.

## Requisitos previos para instalar el parche {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Instalación y configuración del parche {#installing-and-configuring-the-patch}

1. Realice una copia de seguridad del elemento &lt;*AEM raíz_de_formularios_de_*>/implementar carpeta. Es necesaria si decide desinstalar la corrección rápida.
1. Detenga el servidor de aplicaciones.
1. Extraiga el archivo del programa de instalación del parche en el disco duro.
1. En el directorio denominado según el sistema operativo que esté utilizando:

   * **Windows**
Vaya al directorio correspondiente del medio de instalación o a la carpeta del disco duro donde copió el programa de instalación y haga doble clic en el archivo aemforms65_cfp_install.exe.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Vaya al directorio correspondiente y, desde el símbolo del sistema, escriba `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Esto inicia un asistente de instalación que le guiará a través de la instalación.

1. En el panel Introducción, haga clic en **[!UICONTROL Siguiente]**.
1. En el **Elegir carpeta de instalación** , compruebe que la ubicación predeterminada mostrada es correcta para la instalación existente o haga clic en **[!UICONTROL Examinar]** AEM para seleccionar la carpeta alternativa en la que está instalado formularios de la y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información de resumen de parches de corrección rápida y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información del resumen previo a la instalación y haga clic en **[!UICONTROL Instalar]**.
1. Una vez finalizada la instalación, haga clic en **[!UICONTROL Siguiente]** para aplicar las actualizaciones de correcciones rápidas a los archivos instalados.

1. **[Solo para Windows]:** Haga lo siguiente:
   * Anule la selección del **Iniciar el Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Ejecutar **Administrador de configuración** mediante el uso de **ConfigurationManager.bat** archivo en `[aem-forms root]\configurationManager\bin`.

   * O anule la selección del **Iniciar el Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Antes de ejecutar **Administrador de configuración** usando **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, vaya a *`<AEMForms_Install_Dir>\configurationManager\bin`* directorio y reemplazar [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) y [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) archivos.

   >[!NOTE]
   >
   >Uso de **ConfigurationManager.bat** le ayuda a evitar actualizar manualmente el nombre de los archivos .lax.
   >

1. **[Solo para entornos basados en Unix]:**

   * El **Iniciar el Administrador de configuración** La casilla de verificación está seleccionada de forma predeterminada. Clic **[!UICONTROL Listo]** para ejecutar el Administrador de configuración instantáneamente o para ejecutarse **Administrador de configuración** más adelante, anule la selección de **Iniciar el Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Puede empezar **Administrador de configuración** más adelante, utilizando la secuencia de comandos adecuada en la `[AEM_forms_root]/configurationManager/bin` directorio.

1. Según el servidor de aplicaciones, elija uno de los siguientes documentos y siga las instrucciones del *AEM Configuración e implementación de formularios* sección.

   * [AEM Instalación e implementación de formularios de para JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_es)
   * [AEM Instalación e implementación de formularios en la aplicación de la interfaz de usuario para WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_es)

1. (Solo JBoss®) Después de instalar el parche y configurar el servidor, elimine los directorios tmp y de trabajo del servidor de aplicaciones JBoss®.

## Configuraciones posteriores a la implementación {#post-deployment-configurations}

### Configuraciones de SAML {#saml-configurations}

Si tiene configurada la autenticación SAML y tiene problemas con metadatos de IDP grandes, haga lo siguiente después de instalar el parche:

1. Establezca la siguiente propiedad del sistema en el servidor de aplicaciones:\
   `um.saml.enable.large.xml=true`
1. Reiniciar el servidor.
1. Elimine los proveedores de autenticación SAML existentes y agréguelos de nuevo para los dominios existentes, tal como se describe en la configuración de SAML.

## Módulos afectados {#impacted-modules}

* Servicios de documentos
* Seguridad de los documentos
* Base JEE

[Atención al cliente](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home&amp;lang=es#support)
