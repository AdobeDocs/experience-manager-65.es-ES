---
title: Limitaciones de copia de seguridad del generador de PDF
description: Obtenga información acerca de las limitaciones de backup del PDF Generator. No se puede realizar una copia de seguridad del directorio temporal que utiliza el PDF Generator, ya que borra el contenido a intervalos establecidos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 10%

---

# Limitaciones de copia de seguridad del generador de PDF {#pdf-generator-backup-limitations}

No se puede realizar una copia de seguridad del directorio temporal que utiliza el PDF Generator para convertir archivos. Aunque el servicio se restaure correctamente, los datos pueden perderse porque el PDF Generator revisa y borra el contenido del directorio temporal a intervalos establecidos.
