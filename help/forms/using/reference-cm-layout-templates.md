---
title: Plantillas de carta de referencia
seo-title: Plantillas de carta de referencia
description: 'AEM Forms proporciona plantillas de diseño de cartas de gestión de correspondencia que puede utilizar para crear cartas rápidamente. '
seo-description: 'AEM Forms proporciona plantillas de diseño de cartas de gestión de correspondencia que puede utilizar para crear cartas rápidamente. '
uuid: 3b2312d9-daa0-435b-976f-4969b54c5056
products: SG_EXPERIENCEMANAGER/6.3/FORMS
content-type: reference
topic-tags: correspondence-management
discoiquuid: afeb9f4d-3feb-4a0e-8884-e3ec1309b33b
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Plantillas de carta de referencia {#reference-letter-templates}

In Correspondence Management, a letter template contains typical form fields, layout features such as a header and footer, and empty &quot;target areas&quot; for the placement of content.

Correspondence Management provides letter templates in the AEM Forms package [AEM-FORMS-REFERENCE-LAYOUT-TEMPLATES](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/fd/AEM-FORMS-6.3-REFERENCE-LAYOUT-TEMPLATES). For installing a package, see [How to Work With Packages](/help/sites-administering/package-manager.md). You can customize the templates in Designer according to your branding and business needs. The package includes the following templates:

* Clásica
* Classic Simple
* Balanced Left
* Equilibrado a la derecha
* Visual Left
* Visual Top
* Visual Top - Classic

Después de instalar el paquete, las plantillas de diseño (XDP) se muestran en la carpeta de plantillas en la siguiente ubicación:

`https://'[server]:[port]'/[context-root]/aem/forms.html/content/dam/formsanddocuments/templates-folder`

A continuación se muestran los campos comunes de todas las plantillas de este paquete:

* Fecha
* Saludo
* Cerrar texto
* Texto de firma

![Todas las plantillas de letras de CM enumeradas](assets/templatescorrespondence.png)

Después de instalar el paquete AEM-FORMS-6.3-REFERENCE-LAYOUT-TEMPLATES, las plantillas se muestran en la carpeta templates

## Clásica {#classic}

With a logo on top, Classic template is suitable for a plain professional letter.

![clásica](assets/classic.png)

PDF preview of a letter created using the Classic template

## Classic Simple {#classic-simple}

Includes fields to capture phone number and email address. A Classic Simple template is similar to the Classic template except that it does not have fields where you could enter the address of the recipient.

![Contact information fragment](assets/classicsimple.png)

previsualización en PDF de una carta creada con la plantilla Classic Simple

## Balanced Left {#balanced-left}

La plantilla Equilibrada izquierda incluye un logotipo a la izquierda de la letra.

![balancedleft](assets/balancedleft.png)

previsualización PDF de una carta creada con la plantilla Izquierda equilibrada

## Equilibrado a la derecha {#balanced-right}

La plantilla Equilibrada a la derecha tiene el logotipo de compañía a la izquierda y proporciona espacio para introducir la dirección de destinatarios en la propia carta. La plantilla Equilibrada a la derecha también incluye un pie de página que se reorganiza cuando la carta tiene varias páginas.

![balancedright](assets/balancedright.png)

previsualización PDF de una carta creada con la plantilla Derecha equilibrada

## Visual Left {#visual-left}

La plantilla Izquierda visual tiene un encabezado lateral a la izquierda de la página con el logotipo de compañía colocado sobre el encabezado lateral. La plantilla de Visual Left tiene un campo de asunto pero no un pie de página.

![visualleft](assets/visualleft.png)

PDF preview of a letter created using the Visual Left template

## Visual Top {#visual-top}

Visual Top template has visual margin on the top. The Visual Top template has a field for entering recipient&#39;s address on the page itself. The Visual Top template has the subject field and a footer that reflows for letters that extend to multiple pages.

![visualtop](assets/visualtop.png)

PDF preview of a letter created using the Visual Top template

## Visual Top - Classic {#visual-top-classic}

The Visual Top - Classic template has a header on top of the page with the company logo. The Visual Top - Classic template has a field to enter a subject but no footer.

![visualtopclassic](assets/visualtopclassic.png)

PDF preview of a letter created using the Visual Top - Classic template

