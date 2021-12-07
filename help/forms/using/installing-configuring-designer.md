---
title: Instalar y configurar Designer
seo-title: Installing and configuring Designer
description: 'Designer está disponible como instalador independiente y también se incluye en Workbench. Aprenda a instalar Designer independiente.  '
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
source-git-commit: a3cf926bde4a4b3a0810058e84ac01012a4a3a57
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 30%

---

# Instalar y configurar Designer{#installing-and-configuring-designer}

## Requisitos previos {#pre-requisites}

El instalador de AEM Forms Designer requiere la versión de 32 bits de [Paquete de tiempo de ejecución redistribuible de Visual C++ 2012](https://support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0) y [Paquete de tiempo de ejecución redistribuible de Visual C++ 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Asegúrese de que los paquetes de tiempo de ejecución redistribuibles mencionados anteriormente estén instalados antes de iniciar la instalación.

Se requieren derechos de administrador para instalar o desinstalar Designer.

## Instalar Designer {#install-designer}

Designer está disponible como instalador independiente y también se incluye en WorkBench. Si utiliza un instalador independiente para Designer, realice los siguientes pasos:

1. Descargar Designer desde Adobe [Sitio web de licencias](https://licensing.adobe.com/).

   >[!NOTE]
   >
   >Si tiene instalada una versión anterior de Designer, desinstale la versión anterior antes de continuar.

1. Inicie el instalador de Designer haciendo doble clic en Setup.exe.
1. Continúe y proporcione sus detalles y número de serie en la pantalla Personalizar.
1. Si acepta el acuerdo de licencia, haga clic en Siguiente para continuar.
1. (Opcional) Si desea instalar Designer en una ubicación de su elección, modifique la ruta de instalación. Haga clic en Siguiente. 
1. Haga clic en Atrás para cambiar las preferencias. Para instalar Designer, haga clic en Instalar.
1. Haga clic en Finalizar cuando finalice la instalación.

Como alternativa, puede instalar Designer a través de la línea de comandos utilizando el modo pasivo o silencioso.

* Instalación pasiva de la línea de comandos: El instalador muestra una barra de progreso que indica que la instalación está en curso, pero que no se muestran mensajes de error ni mensajes de error. Una vez iniciada, no puede cancelar la instalación.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Instalación silenciosa de la línea de comandos: El instalador ejecuta la instalación sin mostrar una interfaz de usuario. No se muestran mensajes ni cuadros de diálogo. Una vez iniciada, no puede cancelar la instalación.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```


