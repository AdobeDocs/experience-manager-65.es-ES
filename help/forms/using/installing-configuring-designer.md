---
title: Instalar y configurar Designer
description: Designer está disponible como programa de instalación independiente y se integra con Workbench. Aprenda a instalar Designer de forma independiente.
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
feature: Forms Designer
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 30%

---

# Instalar y configurar Designer{#installing-and-configuring-designer}

## Requisitos previos {#pre-requisites}

+++ Para AEM Forms Designer de 64 bits (recomendado)

* Instalar la versión de 64 bits de  [Visual C++ 2019 redistribuible (x64)](https://learn.microsoft.com/es-es/cpp/windows/latest-supported-vc-redist?view=msvc-170). Asegúrese de que los paquetes de ejecución redistribuibles anteriores estén instalados antes de iniciar la instalación.
* Usuario con derechos de administrador para instalar o desinstalar AEM Forms Designer.

+++

+++ Para AEM Forms Designer de 32 bits

* Instale la versión de 32 bits de  [Visual C++ 2019 redistribuible (x64)](https://learn.microsoft.com/es-es/cpp/windows/latest-supported-vc-redist?view=msvc-170). Asegúrese de que los paquetes de ejecución redistribuibles anteriores estén instalados antes de iniciar la instalación.
* Usuario con derechos de administrador para instalar o desinstalar AEM Forms Designer.

+++

>[!NOTE]
>
> AEM La versión de 64 bits del diseñador se introdujo con el paquete de servicio 19 de Forms de 6.5 (6.5.19.0) de.



## Instalar AEM Forms Designer {#install-designer}

Designer está disponible como programa de instalación independiente y se integra con Workbench. Si utiliza un programa de instalación independiente para AEM Forms Designer, realice los siguientes pasos:

1. Desinstale la versión anterior de AEM Forms Designer si ya está instalada.
1. Descargue AEM Forms Designer de 64 bits (recomendado) o AEM Forms Designer de 32 bits en función de sus necesidades.

   >[!NOTE]
   > 
   >* Forms AEM Designer de 32 bits está programado para dejar de utilizarse con los paquetes de servicio 20 (6.5.20.0) de Forms de 6.5 de. Adobe recomienda actualizar a Forms Designer de 64 bits.
   >* Forms AEM Designer de 64 bits solo está disponible para los paquetes de servicio 19 (6.5.19.0) o versiones posteriores de Forms de 6.5, o bien para las versiones posteriores.
   >* Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0) y la versión posterior de Forms Designer también incluyen la versión del paquete de servicio. Por ejemplo, para el paquete de servicio 15 el número de versión es 6.5.15.20221112.1.0. En este ejemplo, 6.5.15 es la versión del paquete de servicio.

1. Inicie el programa de instalación de AEM Forms Designer haciendo doble clic en setup.exe.
1. Continúe y proporcione sus detalles y el número de serie en la pantalla Personalización.

   >[!NOTE]
   >
   >* Obtenga su clave de licencia de Forms Designer de [Sitio web de licencias de Adobe](https://licensing.adobe.com/).

1. Si acepta el acuerdo de licencia, haga clic en Siguiente para continuar.
1. (Opcional) Si desea instalar Designer en una ubicación de su elección, modifique la ruta de instalación. Haga clic en Siguiente.
1. Haga clic en Atrás para cambiar las preferencias. Para instalar Designer, haga clic en Instalar.
1. Haga clic en Finalizar cuando finalice la instalación.

Como alternativa, puede instalar AEM Forms Designer a través de la línea de comandos utilizando el modo pasivo o silencioso.

* Instalación pasiva desde la línea de comandos: el programa de instalación muestra una barra de progreso que indica que la instalación está en curso, pero que no se muestran avisos ni mensajes de error. Una vez iniciada, no puede cancelar la instalación.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Instalación silenciosa desde la línea de comandos: el programa de instalación ejecuta la instalación sin mostrar una interfaz de usuario. No se muestran avisos, mensajes ni cuadros de diálogo. Una vez iniciada, no puede cancelar la instalación.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## Actualizar AEM Forms Designer {#update-forms-designer}

Existen dos casos al actualizar la última versión de AEM Forms Designer 6.5.16.0:

* **Caso 1**: Cuando el usuario tiene una versión de AEM Forms Designer anterior a la 6.5.15.0.
* **Caso 2**: Cuando el usuario tiene la versión 6.5.15.0 de AEM Forms Designer.

+++**Cuando el usuario tiene una versión de AEM Forms Designer anterior a la 6.5.15.0.**

Si utiliza un programa de instalación independiente para AEM Forms Designer, realice los siguientes pasos:

1. Antes de instalar **AEM Forms Designer 6.5.16.0**, los usuarios deben desinstalar cualquier versión anterior.
1. Descargar e instalar [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) AEM en la página Versiones de formularios de la plantilla de informes.
1. Después de la instalación correcta de **AEM Forms Designer 6.5.15.0**, descargar e instalar [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) haciendo doble clic en el archivo de instalación descargado .

+++

+++**Cuando el usuario tiene la versión 6.5.15.0 de AEM Forms Designer**

Si utiliza un programa de instalación independiente para AEM Forms Designer, realice los siguientes pasos:
1. Descargue la versión más reciente de AEM Forms Designer desde [Portal de distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
1. Instale la última versión de AEM Forms Designer haciendo doble clic en el archivo de instalación descargado.

+++