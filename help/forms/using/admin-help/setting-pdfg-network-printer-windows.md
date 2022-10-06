---
title: Configuración de una impresora de red PDFG (solo Windows)
seo-title: Setting up a PDFG Network Printer (Windows only)
description: Aprenda a configurar una impresora de red PDFG ( solo Windows )
seo-description: Learn how to set up a PDFG Network Printer ( Windows only )
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# Configuración de una impresora de red PDFG (solo Windows) {#setting-up-a-pdfg-network-printer-windows-only}

La impresora de red PDFG permite a los usuarios generar un documento PDF desde cualquier aplicación que admita la impresión. Después de que un usuario instale la impresora de red PDFG, una nueva impresora denominada *Generador de PDF* aparece en la sección Impresoras del Panel de control de Campaign de Windows. Si ya existe una impresora con el mismo nombre, se solicita al usuario que proporcione otro nombre.

La impresión en esta impresora desde cualquier aplicación envía el documento (en formato PostScript) al Generador de PDF, que convierte el archivo PostScript a PDF. Según la configuración de Generador de PDF, envía el documento de PDF al usuario como datos adjuntos a un mensaje de correo electrónico, reenvía el documento de PDF a un servicio o proceso de formularios AEM especificado o realiza ambas acciones.

Se requieren los siguientes pasos para configurar una impresora de red PDFG:

1. Configure las opciones de correo electrónico. (Consulte [Configuración de correo electrónico para la impresora de red PDFG](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).)
1. En la consola de administración, configure la impresora de red PDFG. (Consulte [Configuración de la configuración de la impresora de red PDFG](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings).)
1. Asegúrese de que los usuarios estén configurados con una dirección de correo electrónico válida en la base de datos de formularios AEM y asigne PDFGUserPermission a cada usuario. <!-- Fix broken link See Setting up and organizing users -->
1. Asegúrese de que JRE6 de 32 bits esté instalado en los equipos de los usuarios.
1. Instale la impresora en los equipos de los usuarios. (Consulte [Instalación de la impresora de red PDFG en el equipo de un usuario](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## Configuración de correo electrónico para la impresora de red PDFG {#configure-email-settings-for-pdfg-network-printer}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en provider.email_sendmail_service, especifique la configuración de SMTP y haga clic en Guardar.

## Configuración de la configuración de la impresora de red PDFG {#configure-the-pdfg-network-printer-settings}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Impresora de red PDFG
1. En las listas Configuración de Adobe PDF y Configuración de seguridad , seleccione las opciones que desea aplicar al PDF generado. Para obtener más información sobre esta configuración, consulte [Configuración de Adobe PDF](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) y [Configuración de la configuración de seguridad](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Para volver a enviar los PDF convertidos a los usuarios, seleccione la opción Enviar correo electrónico al archivo de PDF convertido de nuevo al usuario y especifique la siguiente información:

   * La dirección de correo electrónico que se utiliza para enviar PDF a los usuarios
   * El asunto del mensaje de correo electrónico
   * Encabezado, cuerpo y pie de página del mensaje de correo electrónico. En el mensaje de correo electrónico, &lt;receivername> se reemplaza por el nombre completo del usuario que imprimió el documento.

1. Para enviar los PDF convertidos a un servicio o proceso de formularios AEM, seleccione la opción Reenviar el PDF convertido al servicio o proceso de formularios AEM especificado y especifique la siguiente información:

   * Nombre del servicio que se va a invocar
   * Nombre de la operación del servicio que se va a invocar
   * El nombre del parámetro de entrada, tal como se especifica en el archivo component.xml del servicio o proceso. El documento del PDF se utilizará como valor para ese parámetro de entrada.

1. Haga clic en Guardar.

Si desea volver al texto de correo electrónico predeterminado original, haga clic en Restaurar contenido de correo electrónico.

## Instalación de la impresora de red PDFG en el equipo de un usuario {#install-pdfg-network-printer-on-a-user-s-computer}

Los usuarios que tengan la función de administrador PDFG o de usuario PDFG pueden instalar una impresora de red PDFG. Debe tener un JDK de 32 bits instalado en el equipo.

1. (Administradores PDFG) En la consola de administración, haga clic en Servicios > Generador de PDF > Impresora de red PDFG.

   (Usuarios de PDFG) Vaya a `http(s)://[host]:'port'/pdfgui` y haga clic en el enlace en Instalación de impresora de red PDFG.

1. En Instalación de impresora de red PDFG, haga clic en el enlace . Cuando se le solicite información de cuenta de usuario, especifique el nombre de usuario y la contraseña que utilizó en el paso 1 para iniciar sesión. Aparece un mensaje que indica que la impresora se ha instalado correctamente.

   ***nota **: Si la contraseña del usuario cambia, los usuarios deberán volver a instalar la impresora de red PDFG en sus equipos. No puede actualizar la contraseña desde la consola de administración.*

1. Haga clic en Aceptar.
