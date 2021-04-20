---
title: Entrega de información segura de gran volumen
seo-title: Entrega de información segura de gran volumen
description: La seguridad de los documentos admite la asociación de licencias a usuarios, en lugar de a documentos en entornos de producción masiva.
seo-description: La seguridad de los documentos admite la asociación de licencias a usuarios, en lugar de a documentos en entornos de producción masiva.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Entrega de información segura de gran volumen {#high-volume-secure-information-delivery}

En un entorno de producción masiva, como uno que genera facturas mensuales seguras para una empresa de telecomunicaciones, la creación de licencias específicas para cada documento puede convertirse en un proceso intensivo en recursos. En estos casos, la seguridad de los documentos permite la asociación de licencias a los usuarios, no a los documentos. La licencia generada para un usuario se utiliza para todos los documentos protegidos para ese usuario.

Una ventaja de este enfoque es que el tamaño de la base de datos de seguridad del documento no aumenta linealmente con los documentos, sino con el número de usuarios. Además, como necesita crear la licencia una sola vez para un usuario, la protección posterior de los documentos mediante estas políticas se vuelve más rápida. Para todos estos documentos se admiten funciones como acceso sin conexión, caducidad de documentos y revocación.

La seguridad de los documentos también admite directivas abstractas. Las políticas abstractas son plantillas de directiva que contienen todos los atributos de directiva, como la configuración de seguridad del documento y los derechos de uso, pero no contienen una lista de entidades principales. Los administradores pueden crear cualquier cantidad de políticas a partir de la política abstracta con diferentes principios que deben tener acceso a los documentos. Los cambios realizados en la política abstracta no afectan a las políticas reales que se generan a partir de las políticas abstractas.

En el caso de la generación de facturas mensuales para una empresa de telecomunicaciones, se crea una política abstracta, se crean usuarios y, a continuación, se generan licencias únicas para cada usuario. Las licencias se aplican posteriormente a los documentos de cada usuario.

La creación de una directiva abstracta solo se admite mediante el SDK de Java para la seguridad de documentos. Sin embargo, puede administrar las políticas que crea a partir de la política abstracta de las páginas web de seguridad del documento. Las políticas que se crean mediante este método tienen un comportamiento idéntico al de las creadas en páginas web de seguridad de documentos.

Consulte [Programación con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_63) para obtener más información.
