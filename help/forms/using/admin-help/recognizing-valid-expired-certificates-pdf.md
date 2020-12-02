---
title: Reconocimiento de certificados válidos y caducados en documentos PDF
seo-title: Reconocimiento de certificados válidos y caducados en documentos PDF
description: Obtenga información sobre cómo reconocer certificados válidos y caducados en documentos PDF.
seo-description: Obtenga información sobre cómo reconocer certificados válidos y caducados en documentos PDF.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Reconocimiento de certificados válidos y caducados en documentos PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Cuando se abre en Adobe Reader un documento PDF con derechos de uso aplicados por Extensiones de Reader, aparece una barra de estado que describe los derechos de uso específicos activados en el documento PDF.

Cuando caduca el certificado digital que especifica los derechos de uso de un documento PDF y se abre el documento PDF en Adobe Reader, aparece un cuadro de diálogo que informa al usuario de que el documento PDF tiene derechos de uso, pero estos derechos están deshabilitados. Aunque el mensaje indica que el documento PDF se alteró o alteró, no es necesariamente el caso. Adobe Reader muestra este mensaje cuando caduca un certificado o se modifica un documento. En Adobe Reader 7.0.x o posterior, no puede determinar qué caso es el problema en este momento.

Después de cerrar el cuadro de diálogo, Adobe Reader abre el documento PDF. Los derechos de uso aplicados con extensiones de Acrobat Reader DC no están disponibles, como se espera. Si el documento PDF es un formulario interactivo, los campos del formulario están bloqueados y el usuario no puede cambiar los datos del formulario.
