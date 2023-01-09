---
title: Instalar y configurar Designer
seo-title: Installing and configuring Designer
description: Designer está disponible como programa de instalación independiente y se integra con Workbench. Aprenda a instalar Designer de forma independiente.
seo-description: Designer is available as a stand-alone installer and is also bundled with Workbench. Learn how to install stand-alone Designer.
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f3a5b5ce-2262-4d5d-a8ae-d59a3a4229e7
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: 85189a4c35d1409690cbb93946369244e8848340
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 76%

---

# Instalar y configurar Designer{#installing-and-configuring-designer}

## Requisitos previos {#pre-requisites}

* Instale la versión de 32 bits de  [Visual C++ 2019 redistribuible (x86)](https://learn.microsoft.com/es-es/cpp/windows/latest-supported-vc-redist?view=msvc-170). Asegúrese de que los paquetes de ejecución redistribuibles anteriores estén instalados antes de iniciar la instalación.
* Un usuario con derechos de administrador para instalar o desinstalar Designer.

## Instalar Designer {#install-designer}

Designer está disponible como programa de instalación independiente y se integra con Workbench. Si utiliza un programa de instalación independiente para Designer, realice los siguientes pasos:

1. Desinstale la versión anterior de AEM Forms Designer si ya está instalada.
1. Descargar Designer desde [Sitio web de licencias de Adobe](https://licensing.adobe.com/).

   >[!NOTE]
   >
   > * Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0) y versiones posteriores de Forms Designer también incluyen la versión de Service Pack. Por ejemplo, para el Service Pack 15, el número de versión es 6.5.15.20221112.1.0. En este ejemplo, 6.5.15 es la versión del Service Pack.


1. Inicie el programa de instalación de Designer haciendo doble clic en Setup.exe.
1. Continúe y proporcione sus detalles y número de serie en la pantalla Personalizar.
1. Si acepta el acuerdo de licencia, haga clic en Siguiente para continuar.
1. (Opcional) Si desea instalar Designer en una ubicación de su elección, modifique la ruta de instalación. Haga clic en Siguiente.
1. Haga clic en Atrás para cambiar las preferencias. Para instalar Designer, haga clic en Instalar.
1. Haga clic en Finalizar cuando finalice la instalación.

Como alternativa, puede instalar Designer a través de la línea de comandos utilizando el modo pasivo o silencioso.

* Instalación pasiva desde la línea de comandos: el programa de instalación muestra una barra de progreso que indica que la instalación está en curso, pero que no se muestran avisos ni mensajes de error. Una vez iniciada, no puede cancelar la instalación.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Instalación silenciosa desde la línea de comandos: el programa de instalación ejecuta la instalación sin mostrar una interfaz de usuario. No se muestran avisos, mensajes ni cuadros de diálogo. Una vez iniciada, no puede cancelar la instalación.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```
