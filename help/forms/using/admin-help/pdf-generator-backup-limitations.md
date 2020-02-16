---
title: Limitaciones de copia de seguridad de PDF Generator
seo-title: Limitaciones de copia de seguridad de PDF Generator
description: Obtenga información sobre las limitaciones de copia de seguridad de PDF Generator.
seo-description: Obtenga información sobre las limitaciones de copia de seguridad de PDF Generator.
uuid: 9537ffde-4396-46d1-81ea-edcd25923ffb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 23386353-b2bf-49f1-947a-dd7587bba175
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Limitaciones de copia de seguridad de PDF Generator {#pdf-generator-backup-limitations}

No se puede realizar una copia de seguridad del directorio temporal que utiliza PDF Generator para convertir archivos. Aunque el servicio se restaurará correctamente, los datos se pueden perder porque el generador de PDF revisa y borra el contenido del directorio temporal a intervalos establecidos.
