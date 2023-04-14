---
title: Instrucciones de instalación de parches de AEM Forms para AEM Forms
description: Instrucciones de instalación de Service Pack de AEM Forms para el entorno OSGi y JEE
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 01bf12ec46966ab2c78e2e825840230ea1bd3395
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 18%

---

# Instrucciones de instalación de AEM 6.5 Forms Service Pack {#aem-form-patch-installation-instructions}

## Información de la versión

| Producto | Adobe Experience Manager 6.5 Forms |
|---|---|
| Versión | 6.5.16.0 |
| Tipo | Versión de Service Pack |
| Fecha | 2 de marzo de 2023 |
| Descargar URL | [Últimas versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) |

>[!NOTE]
>
>Consulte las últimas [Notas de la versión de AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=es) para obtener una lista completa de los problemas corregidos.

## Novedades de Experience Manager Forms 6.5

Adobe Experience Manager (AEM) Forms Service Pack incluye funciones nuevas y actualizadas, como mejoras clave solicitadas por los clientes, mejoras de rendimiento, estabilidad y seguridad. AEM Forms lanza paquetes de servicios a intervalos regulares para proporcionar las últimas funciones y mejoras. Según la pila, elija una de las siguientes rutas para descargar e instalar el Service Pack en su entorno:

* [Descargue e instale Service Pack en un formulario AEM en un entorno JEE](#download-and-install-for-jee-service-pack)
* [Descargue e instale Service Pack en un formulario AEM en un entorno OSGi](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> Adobe publica un instalador completo cada 6º service pack. AEM 6.5 Forms Service Pack 12 (6.5.12.0) en JEE fue el último instalador completo. El instalador completo proporciona soporte para nuevas plataformas, mientras que el instalador regular de service pack incluye nuevas funciones, corrección de errores y mejoras generales. Si realiza una instalación nueva o planea utilizar el software más reciente para su AEM Forms 6.5 en el entorno JEE, Adobe recomienda utilizar AEM 6.5.12.0 Forms en el instalador completo de JEE lanzado el 3 de marzo de 2022, en lugar del instalador de AEM Forms 6.5 lanzado el 8 de abril de 2019. Después de utilizar el instalador completo, instale el Service Pack más reciente.

## Descargue e instale Service Pack en un formulario AEM en un entorno JEE {#download-and-install-for-jee-service-pack}

![Instalación de JEE](/help/forms/using/assets/jeeinstallation.png)

+++1. Haga una copia de seguridad de su entorno existente:

1. Haga una copia de seguridad de su [Repositorio CRX, Esquema de Base de Datos y GDS (Almacenamiento Global de Documentos)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. Haga una copia de seguridad de &lt;*AEM_forms_root*>/implementar carpeta.

>[!NOTE]
>
> Antes de ejecutar el instalador de Service Pack de AEM, asegúrese de tener privilegios de acceso de escritura en AEM directorio de instalación.

+++

+++2. Descargue el software necesario:

* [AEM Forms en JEE Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es)
* [Paquete de servicio de AEM](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=es)
* [Paquete de complemento de Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es)
* [Servlet de fragmento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. Instale AEM Forms en el paquete de servicios JEE:

1. Detenga el servidor de aplicaciones.
1. Extraiga el **Archivo del instalador de AEM Forms en JEE Service Pack** a su disco duro:

   * **Windows**
Vaya al directorio correspondiente del medio de instalación o la carpeta del disco duro donde copió el instalador y haga doble clic en el botón 
`aemforms65_cfp_install.exe` archivo.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux®**
Vaya al directorio apropiado, y desde un shell y escriba 
`./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Esto inicia un asistente de instalación que le guiará a través de la instalación.

1. En el panel Introducción, haga clic en **[!UICONTROL Siguiente]**.
1. En el **Elegir carpeta de instalación** , compruebe que la ubicación predeterminada mostrada es correcta para la instalación existente o haga clic en **[!UICONTROL Examinar]** para seleccionar la carpeta alternativa donde están instalados AEM formularios y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información de resumen del Service Pack y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información del resumen previo a la instalación y haga clic en **[!UICONTROL Instalar]**.
1. Una vez finalizada la instalación, haga clic en **[!UICONTROL Siguiente]** para aplicar las actualizaciones de correcciones rápidas a los archivos instalados.
1. **[Solo para Windows]:** Realice uno de los pasos siguientes:

   * Anule la selección de **Iniciar Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Ejecutar **Administrador de configuración** usando la variable **ConfigurationManager.bat** archivo ubicado en `[aem-forms root]\configurationManager\bin`.

   * O desmarque la opción **Iniciar Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Antes de ejecutarse **Administrador de configuración** using **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, vaya a *`<AEMForms_Install_Dir>\configurationManager\bin`* directorio y reemplazar [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) y [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) archivos.

      >[!NOTE]
      >
      >* Actualizar o reemplazar la variable **ConfigurationManager.bat** ayuda a evitar actualizar los archivos .lax manualmente.


1. **[Solo para Unix]:** La variable **Iniciar Administrador de configuración** está seleccionada de forma predeterminada. Haga clic en **[!UICONTROL Listo]** para ejecutar el Administrador de configuración instantáneamente o **Administrador de configuración** más tarde, anule la selección de la opción **Iniciar Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Puede empezar **Administrador de configuración** más adelante, utilizando la secuencia de comandos adecuada en la `[AEM_forms_root]/configurationManager/bin` directorio.

1. Según el servidor de aplicaciones, elija uno de los siguientes documentos y siga las instrucciones de la sección *Configuración e implementación de AEM formularios* para obtener más información.

   * [Instalación e implementación de AEM formularios para JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_es)
   * [Instalación e implementación de AEM formularios para WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_es)
   * [Instalación e implementación de AEM Forms para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65_es)
   * [Instalación e implementación de formularios AEM para JBoss® Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Instalación e implementación de formularios AEM para WebSphere® Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Instalación e implementación de AEM Forms para el clúster WebLogic](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> Después de instalar AEM Forms en el Service Pack JEE, debe eliminar el paquete de complementos de Forms de `crx-repository\install` antes de reiniciar el appserver. Descargue el último paquete de complementos de Forms desde el [Portal de distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

+++

+++4. Instalación del fragmento servlet

>[!NOTE]
>
> * En caso de que esté actualizando desde **AEM Service Pack 6.5.15.0**, no es necesario instalar el **fragmento servlet**. Si está actualizando desde una versión anterior a **AEM Service Pack 6.5.15.0**, es obligatorio instalar el **fragmento servlet**.
> * Es obligatorio instalar el **fragmento servlet** para todos los servidores de aplicaciones excepto los que se ejecutan en **JBoss® EAP 7.4.0**.



Para descargar e instalar el fragmento de servlet:

1. Si no ha descargado el fragmento, descárguelo desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. Inicie el servidor de aplicaciones, espere a que los registros se estabilicen y compruebe el estado del paquete.

1. Abra los paquetes de la consola web. La URL predeterminada es `http://[Server]:[Port]/system/console/bundles`.

1. Haga clic en Instalar/Actualizar. Elija el fragmento descargado, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Haga clic en ******Instalar o actualizar**. Espere a que el servidor de aplicaciones se estabilice

1. Detenga el servidor de aplicaciones.

+++

+++5. Instale el paquete de servicio  de AEM 

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se actualizó desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.
1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su [!DNL Experience Manager] instancia.
1. Descargue el Service Pack desde [Distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra el Administrador de paquetes y, a continuación, seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).
1. Seleccione el paquete y, a continuación, seleccione **[!UICONTROL Instalar]**.

**Instalación automática**

Hay dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL ExperienceManager] service pack.<!--       UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor esté disponible en línea.
El paquete se instala automáticamente.

* Utilice la variable [API HTTP del Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es). Uso  `cmd=install&recursive=true` para que se instalen los paquetes anidados.

   >[!NOTE]
   El paquete de servicio del Experience Manager no admite la instalación del Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

   **Validar la instalación**

   Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

   1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (spversion)` under [!UICONTROL Productos instalados].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. Todos los paquetes OSGi son: **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).
   1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.14 o posterior (utilice WebConsole: `/system/console/     bundles`).

+++

+++6. Instalación AEM paquete de complementos de Experience Manager Forms

1. Asegúrese de que ha instalado la variable [!DNL Experience Manager] service pack.
1. Descargue el paquete de complementos de Forms correspondiente que aparece en las [versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) para su sistema operativo.
1. Instale el paquete de complementos de Forms como se describe en [Instalación de paquetes de complementos de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
1. Si utiliza letras en Experience Manager 6.5 Forms, instale la variable [último paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

+++

## Descargue e instale Service Pack en un formulario AEM en un entorno OSGi {#download-and-install-for-osgi-service-pack}

![Pasos de instalación de OSGi](/help/forms/using/assets/osgiinstallation.png)


+++1. Haga una copia de seguridad de su entorno existente:

1. Haga una copia de seguridad de su [Repositorio CRX y Esquema de Base de Datos](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
Si instala AEM Forms service pack para la base de datos relacional, es obligatorio realizar una copia de seguridad de DB_schema.

+++

+++2. Descargue el software necesario:

* [Paquete de servicio de AEM](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=es)
* [Paquete de complemento de Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es)

+++

+++3. Instale el paquete de servicio  de AEM 

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se actualizó desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.
1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su [!DNL Experience Manager] instancia.
1. Descargue el Service Pack desde [Distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra el Administrador de paquetes y, a continuación, seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).
1. Seleccione el paquete y, a continuación, seleccione **[!UICONTROL Instalar]**.

**Instalación automática**

Hay dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL Experience Manager] service pack.<!--  UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Utilice la variable [API HTTP del Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es). Uso `cmd=install&recursive=true` para que se instalen los paquetes anidados.

   >[!NOTE]
   El paquete de servicio del Experience Manager no admite la instalación del Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

   **Validar la instalación**

   Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

   1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (spversion)` under [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. Todos los paquetes OSGi son: **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

      1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.14 o posterior (utilice la consola web: `/system/console/bundles`).

+++

+++4. Instalación AEM paquete de complementos de Experience Manager Forms

1. Asegúrese de que ha instalado la variable [!DNL Experience Manager] service pack.
1. Descargue el paquete de complementos de Forms correspondiente que aparece en las [versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) para su sistema operativo.
1. Instale el paquete de complementos de Forms como se describe en [Instalación de paquetes de complementos de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
1. Si utiliza letras en Experience Manager 6.5 Forms, instale la variable [último paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

+++

## Solución de problemas

* If **Cuadro de diálogo en la interfaz de usuario del Administrador de paquetes** sale durante la instalación del service pack, espere a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Normalmente, este problema se produce en el explorador Safari, pero puede ocurrir de forma intermitente en cualquier explorador.

* Compruebe los registros del monitor (error.log) una vez completada la instalación para cualquier actividad. Espere unos minutos hasta que no haya actividad en los registros. Reinicie la instancia de AEM.

* En caso de que obtenga un **error de servicio no disponible** después de instalar el paquete de servicio de AEM Forms 6.5.15.0, [instalar el fragmento y el paquete servlet](/help/forms/using/aem-service-pack-installation-solution.md) para solucionar el error.
