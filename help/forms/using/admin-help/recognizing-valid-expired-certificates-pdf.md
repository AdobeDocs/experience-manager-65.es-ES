---
title: Reconocimiento de certificados válidos y caducados en documentos de PDF
seo-title: Recognizing valid and expired certificates in PDF documents
description: Obtenga información sobre cómo reconocer certificados válidos y caducados en documentos de PDF.
seo-description: Learn how to recognize valid and expired certificates in PDF documents.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Reconocimiento de certificados válidos y caducados en documentos de PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Cuando se abre en Adobe Reader un documento de PDF que tiene derechos de uso aplicados por las extensiones de Reader, aparece una barra de estado que describe los derechos de uso específicos activados en el documento de PDF.

Cuando caduca el certificado digital que especifica los derechos de uso de un documento de PDF y se abre el documento de PDF en Adobe Reader, aparece un cuadro de diálogo en el que se indica al usuario que el documento de PDF tiene derechos de uso, pero estos derechos están desactivados. Aunque el mensaje indica que el documento del PDF se ha modificado o manipulado, no es necesariamente el caso. Adobe Reader muestra este mensaje cuando un certificado caduca o se modifica un documento. En Adobe Reader 7.0.x o posterior, no puede determinar qué caso es el problema actual.

Después de cerrar el cuadro de diálogo, Adobe Reader abre el documento PDF. Los derechos de uso que se aplicaron mediante extensiones de Acrobat Reader DC no están disponibles, como se espera. Si el documento del PDF es un formulario interactivo, los campos del formulario están bloqueados y el usuario no puede cambiar los datos del formulario.
