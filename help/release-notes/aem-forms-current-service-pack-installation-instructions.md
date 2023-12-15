---
title: Instrucciones de instalación de parches de AEM Forms para AEM Forms
description: Instrucciones de instalación del Service Pack de AEM Forms para el entorno OSGi y JEE
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 531eed9bb6d7792a6da0104b533a505738a64786
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 7%

---

# AEM Instrucciones de instalación del paquete de servicio de Forms de.5 {#aem-form-patch-installation-instructions}

## Información de la versión

| Producto | Adobe Experience Manager 6.5 Forms |
|---|---|
| Versión | 6.5.19.0 (OSGi), 6.5.19.1 (JEE) |
| Tipo | Versión del paquete de servicio |
| Fecha | 8 de diciembre de 2023 |
| Descargar URL | [Últimas versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) |

>[!NOTE]
>
>Consulte las últimas [AEM Notas de la versión de Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=es) para obtener una lista completa de los problemas corregidos.

## ¿Qué incluye Experience Manager Forms 6.5?

El paquete de servicio de Adobe Experience Manager AEM () Forms incluye funciones nuevas y actualizadas, como mejoras clave solicitadas por el cliente, de rendimiento, estabilidad y seguridad. AEM Forms lanza Service Packs a intervalos regulares para ofrecer las últimas funciones y mejoras. Según la pila de tecnología, elija una de las siguientes rutas para descargar e instalar el Service Pack en su entorno:

* [AEM Descargue e instale el Service Pack en un formulario de la aplicación en un entorno JEE de](#download-and-install-for-jee-service-pack)
* [AEM Descargar e instalar el Service Pack en un formulario de la aplicación en un entorno OSGi](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * Adobe lanza un instalador completo cada seis service pack. AEM 6.5 Forms Service Pack 18 (6.5.18.0) es el último programa de instalación completo de JEE. El instalador completo admite nuevas plataformas, mientras que el instalador normal de Service Pack incluye nuevas funciones, corrección de errores y mejoras generales. Si realiza una instalación nueva o planea utilizar el software más reciente para su Forms de 6.5 en el entorno JEE, Adobe AEM recomienda utilizar el instalador completo de Forms AEM 6.5.18.0 en JEE lanzado el 31 de agosto de 2023 en lugar del instalador de Forms AEM Forms 6.5 lanzado el 8 de abril de 2019 o el instalador de AEM 6.5.12.0 lanzado el 3 de marzo de 2022. Después de usar el instalador completo, instale el Service Pack más reciente.
> * La función de AEM Forms, como Forms adaptable, está disponible en [AEM Inicio rápido de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=es), se destinan únicamente a fines de exploración y evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms.

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## AEM Descargue e instale el Service Pack en un formulario de la aplicación en un entorno JEE de {#download-and-install-for-jee-service-pack}

![Instalación de JEE](/help/forms/using/assets/jeeinstallation.png)

+++1. Realice una copia de seguridad del entorno existente

1. Haga una copia de seguridad de su [Repositorio CRX, Esquema de base de datos y GDS (Global Document Storage)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. Haga una copia de seguridad de &lt;*AEM raíz_de_formularios_de_*>/implementar carpeta.

>[!NOTE]
>
> AEM AEM Antes de ejecutar el programa de instalación del paquete de servicio de, asegúrese de que dispone de privilegios de acceso de escritura en el directorio de instalación.

+++

+++2. Descargue el software necesario

* [AEM Forms en el paquete de servicio JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es)
* [AEM Paquete de servicio de](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=es)
* [Paquete de complemento de Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es)
* [Servlet de fragmento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++ 3. Instale los paquetes redistribuibles de Microsoft Visual C++

* Descargue e instale [Versión de 64 bits de los paquetes redistribuibles de Microsoft Visual C++ para Visual Studio 2015, 2017, 2019 y 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) AEM en el equipo en el que está instalado Forms de.5.

>[!NOTE]
>
> Asegúrese de instalar la versión redistribuible, incluso si está instalada una versión anterior, para garantizar la disponibilidad de la versión más reciente.

+++

+++3. Instale AEM Forms en el Service Pack de JEE:

1. Detenga el servidor de aplicaciones.
1. Extraiga el **Archivo del instalador de AEM Forms en JEE Service Pack** a su disco duro:

   * **Windows**
Vaya al directorio correspondiente del medio de instalación o a la carpeta del disco duro donde copió el programa de instalación y haga doble clic en el `aemforms65_cfp_install.exe` archivo.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Vaya al directorio adecuado, y desde un shell y escriba `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Esto inicia un asistente de instalación que le guiará a través de la instalación.

1. En el panel Introducción, haga clic en **[!UICONTROL Siguiente]**.
1. En el **Elegir carpeta de instalación** , compruebe que la ubicación predeterminada mostrada es correcta para la instalación existente o haga clic en **[!UICONTROL Examinar]** AEM para seleccionar la carpeta alternativa en la que está instalado formularios de la y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información de resumen del paquete de servicio y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información del resumen previo a la instalación y haga clic en **[!UICONTROL Instalar]**.
1. Una vez finalizada la instalación, haga clic en **[!UICONTROL Siguiente]** para aplicar las actualizaciones de correcciones rápidas a los archivos instalados.
1. **[Solo para Windows]:** Realice uno de los siguientes pasos:

   * Anule la selección del **Iniciar el Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Ejecutar **Administrador de configuración** mediante el uso de **ConfigurationManager.bat** archivo en `[aem-forms root]\configurationManager\bin`.

   * O anule la selección del **Iniciar el Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Antes de ejecutar **Administrador de configuración** usando **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, vaya a *`<AEMForms_Install_Dir>\configurationManager\bin`* y reemplace el **ConfigurationManager.lax** y **ConfigurationManager_IPV6.lax** con la última versión [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) y [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) archivos.

     >[!NOTE]
     >
     >* Actualizar o reemplazar el **ConfigurationManager.bat** le ayuda a evitar actualizar los archivos .lax manualmente.

1. **[Solo para entornos basados en Unix]:** El **Iniciar el Administrador de configuración** La casilla de verificación está seleccionada de forma predeterminada. Clic **[!UICONTROL Listo]** para ejecutar el Administrador de configuración instantáneamente o para ejecutarse **Administrador de configuración** más adelante, anule la selección de **Iniciar el Administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Puede empezar **Administrador de configuración** más adelante, utilizando la secuencia de comandos adecuada en la `[AEM_forms_root]/configurationManager/bin` directorio.

1. Según el servidor de aplicaciones, elija uno de los siguientes documentos y siga las instrucciones del *AEM Configuración e implementación de formularios* sección.

   * [AEM Instalación e implementación de formularios de para JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_es)
   * [AEM Instalación e implementación de formularios en la aplicación de la interfaz de usuario para WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_es)
   * [Instalación e implementación de AEM Forms para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65_es)
   * [AEM Instalación e implementación de formularios de para el clúster de JBoss®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [AEM Instalación e implementación de formularios en el clúster de WebSphere®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Instalación e implementación de AEM Forms para el clúster de WebLogic](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> Después de instalar AEM Forms en el Service Pack de JEE, debe quitar el paquete de complementos de Forms de `crx-repository\install` antes de reiniciar appserver. Descargue el último paquete de complementos de Forms desde [Portal de distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

+++

+++4. AEM Instale el fragmento del servlet (paquete de servicio 6.5.14.0 o anterior de)

>[!NOTE]
>
> * Si está realizando la actualización desde **AEM Paquete de servicio de 6.5.15.0**, la instalación del **fragmento de servlet** no es obligatorio. Para las versiones **AEM Paquete de servicio de 6.5.14.0** Para versiones anteriores, es obligatorio instalar el fragmento de servlet.
> * Es obligatorio instalar el **fragmento de servlet** para todos los servidores de aplicaciones excepto los que se ejecutan en **JBoss® EAP 7.4.0**.


Para descargar e instalar el fragmento de servlet:

1. Si no ha descargado el fragmento, descárguelo desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. Inicie el servidor de aplicaciones, espere a que los registros se estabilicen y compruebe el estado del paquete.

1. Abra los paquetes de la consola web. La URL predeterminada es `http://[Server]:[Port]/system/console/bundles`.

1. Haga clic en Instalar/actualizar. Elija el fragmento descargado, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Clic **Instalar** o **Actualizar**. Espere a que el servidor de aplicaciones se estabilice

1. Detenga el servidor de aplicaciones.

+++

+++5. AEM Instalar paquete de servicio de

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.
1. Antes de realizar la instalación, tome una instantánea o realice una copia de seguridad nueva de su [!DNL Experience Manager] ejemplo.
1. Descargue el Service Pack desde [Distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).
1. Seleccione el paquete y luego seleccione **[!UICONTROL Instalar]**.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL ExperienceManager] paquete de servicio.<!--       UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor está disponible en línea.
El paquete se instala automáticamente.

* Utilice el [API HTTP del Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es). Uso  `cmd=install&recursive=true` para instalar los paquetes anidados.

  >[!NOTE]
  >
  El Service Pack de Experience Manager no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Validación de la instalación**

  Para conocer las plataformas certificadas para trabajar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

   1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (spversion)` bajo [!UICONTROL Productos instalados].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. Todos los paquetes OSGi son **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web): `/system/console/bundles`).
   1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.14 o posterior de (utilice WebConsole: `/system/console/bundles`).

+++

+++6. AEM Instalación del paquete de complementos de Experience Manager Forms

1. Asegúrese de que ha instalado [!DNL Experience Manager] paquete de servicio.
1. Descargue el paquete de complementos de Forms correspondiente que aparece en las [versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) para su sistema operativo.
1. Instale el paquete de complementos de Forms como se describe en [Instalación de paquetes de complementos de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
1. Si utiliza cartas en Experience Manager 6.5 Forms, instale el [Último paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

+++

## AEM Descargar e instalar el Service Pack en un formulario de la aplicación en un entorno OSGi {#download-and-install-for-osgi-service-pack}

![Pasos de instalación de OSGi](/help/forms/using/assets/osgiinstallation.png)


+++1. Realice una copia de seguridad del entorno existente

1. Haga una copia de seguridad de su [Repositorio CRX y esquema de base de datos](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
Si instala el Service Pack de AEM Forms para la base de datos relacional, es obligatorio realizar una copia de seguridad de DB_schema.

+++

+++2. Descargue el software necesario

* [AEM Paquete de servicio de](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=es)
* [Paquete de complemento de Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es)

+++

+++ 3. Instale los paquetes redistribuibles de Microsoft Visual C++

* Descargue e instale [Versión de 64 bits de los paquetes redistribuibles de Microsoft Visual C++ para Visual Studio 2015, 2017, 2019 y 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) AEM en el equipo en el que está instalado Forms de.5.

>[!NOTE]
>
>
Asegúrese de instalar la versión redistribuible, incluso si está instalada una versión anterior, para garantizar la disponibilidad de la versión más reciente.

+++

+++4. AEM Instalar paquete de servicio de

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.
1. Antes de realizar la instalación, tome una instantánea o realice una copia de seguridad nueva de su [!DNL Experience Manager] ejemplo.
1. Descargue el Service Pack desde [Distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).
1. Seleccione el paquete y luego seleccione **[!UICONTROL Instalar]**.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL Experience Manager] paquete de servicio.<!--  UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor está disponible en línea. El paquete se instala automáticamente.
* Utilice el [API HTTP del Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es). Uso `cmd=install&recursive=true` para instalar los paquetes anidados.

  >[!NOTE]
  >
  El Service Pack de Experience Manager no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Validación de la instalación**

  Para conocer las plataformas certificadas para trabajar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

   1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (spversion)` bajo [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. Todos los paquetes OSGi son **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web): `/system/console/bundles`).

      1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.14 o posterior de (utilice la consola web: `/system/console/bundles`).

+++

+++4. Instalación del paquete de complementos de Adobe Experience Manager Forms AEM ()

1. Asegúrese de que ha instalado [!DNL Experience Manager] paquete de servicio.
1. Descargue el paquete de complementos de Forms correspondiente que aparece en las [versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) para su sistema operativo.
1. Instale el paquete de complementos de Forms como se describe en [Instalación de paquetes de complementos de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
1. Si utiliza cartas en Experience Manager 6.5 Forms, instale el [Último paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

+++

## Solución de problemas

* If **Cuadro de diálogo en la IU del Administrador de paquetes** sale durante la instalación del service pack y espere a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador antes de asegurarse de que las instalaciones se hayan realizado correctamente. Normalmente, este problema se produce en el explorador Safari, pero puede producirse de forma intermitente en cualquier explorador.

* Compruebe los registros del monitor (error.log) una vez que se haya completado la instalación de cualquier actividad. Espere unos minutos hasta que no haya actividad en los registros. Reinicie la instancia de AEM.

* En caso de que consigas una **error de servicio no disponible** después de instalar el paquete de servicio de AEM Forms 6.5.15.0 o posterior, [instalar el fragmento de servlet y el paquete](/help/forms/using/aem-service-pack-installation-solution.md) para corregir el error.
