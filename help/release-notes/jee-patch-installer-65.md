---
title: Instalador de parches de AEM Forms JEE
description: nulo
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
translation-type: tm+mt
source-git-commit: c1af919d4c0fd984249e1a7009274c63b8ce9adb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---


# Instalador de parches JEE de AEM Forms {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Póngase en contacto con el ](https://www.adobe.com/account/sign-in.supportportal.html) servicio de soporte técnico para obtener más información o el parche.

## Acerca del instalador de parches {#about-the-patch-installer}

El instalador de parches de Forms JEE de AEM 6.5 incluye todos los problemas solucionados para todos los componentes de AEM 6.5 Forms JEE disponibles hasta el lanzamiento de este parche. Consulte las [Notas de revisión de Service Pack](sp-release-notes.md) más recientes para obtener una lista completa de los problemas solucionados.

## Requisitos previos para instalar el parche {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Instalación y configuración del parche {#installing-and-configuring-the-patch}

1. Realice una copia de seguridad de la carpeta &lt;*AEM_forms_root*>/deploy. Es necesario si decide desinstalar la corrección rápida.
1. Detenga el servidor de aplicaciones.
1. Extraiga el archivo de archivo del instalador de parches en el disco duro.
1. En el directorio denominado según el sistema operativo que esté utilizando:

   * ****
WindowsVaya al directorio correspondiente del medio de instalación o la carpeta del disco duro donde copió el instalador y haga clic con el botón doble en el archivo aemforms65_cfp_install.exe.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`
   * ****
LinuxDesplácese al directorio adecuado y, desde un símbolo del sistema, escriba 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Esto inicia un asistente de instalación que lo guiará a través de la instalación.

1. En el panel Introducción, haga clic en **[!UICONTROL Siguiente]**.
1. En la pantalla Elegir carpeta de instalación, verifique que la ubicación predeterminada que se muestra es correcta para la instalación existente o haga clic en **[!UICONTROL Examinar]** para seleccionar la carpeta alternativa donde se instalan AEM formularios y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información de Resumen de parches de Corrección rápida y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información del resumen previo a la instalación y haga clic en **[!UICONTROL Instalar]**.
1. Una vez finalizada la instalación, haga clic en **[!UICONTROL Siguiente]** para aplicar las actualizaciones de correcciones rápidas a los archivos instalados.

1. Anule la selección de la opción Administrador de configuración de Inicio antes de hacer clic en Finalizado. Antes de ejecutar el administrador de configuración mediante **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, vaya al directorio *&lt;AEMForms_Install_Dir>\configurationManager\bin* y actualice **axis.jar** a **axis-1.4.1.1.1.1.1.1.1.1.1.1.1.1.1.1 jar** en los siguientes archivos:

   * ConfigurationManager.lax
   * ConfigurationManager_IPv6.lax

1. La casilla de verificación Administrador de configuración de Inicio está seleccionada de forma predeterminada. Haga clic en **[!UICONTROL Listo]** para ejecutar Configuration Manager.

1. Para ejecutar Configuration Manager más adelante, anule la selección de la opción Administrador de configuración de Inicio antes de hacer clic en Finalizado. Puede inicio Configuration Manager más adelante utilizando la secuencia de comandos adecuada en el directorio `[AEM_forms_root]/configurationManager/bin`.

1. Según el servidor de aplicaciones, elija uno de los siguientes documentos y siga las instrucciones de la sección *Configuración e implementación de formularios AEM*.

   * [Instalación e implementación de formularios AEM para JBoss](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Instalación e implementación de formularios AEM para WebSphere](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Solo JBoss) Después de instalar el parche y configurar el servidor, elimine los directorios tmp y de trabajo del servidor de aplicaciones JBoss.

## Configuraciones posteriores a la implementación {#post-deployment-configurations}

### Configuraciones de SAML {#saml-configurations}

Si tiene configurada la autenticación SAML y tiene problemas con metadatos de IDP de gran tamaño, haga lo siguiente después de instalar el parche:

1. Establezca la siguiente propiedad del sistema en el servidor de aplicaciones:\
   `um.saml.enable.large.xml=true`
1. Reinicie el servidor.
1. Elimine los proveedores de autenticación de SAML existentes y agréguelos de nuevo para los dominios existentes, tal como se describe en la configuración de SAML.

## Módulos afectados {#impacted-modules}

* Servicios de documento
* :Seguridad de los documentos
* Base JEE

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
