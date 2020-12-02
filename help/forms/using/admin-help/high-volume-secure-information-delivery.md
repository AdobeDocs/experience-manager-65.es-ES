---
title: Envío de información segura de gran volumen
seo-title: Envío de información segura de gran volumen
description: La seguridad de los documentos apoya la asociación de licencias a los usuarios, en lugar de a los documentos en entornos de producción masiva.
seo-description: La seguridad de los documentos apoya la asociación de licencias a los usuarios, en lugar de a los documentos en entornos de producción masiva.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Envío de información segura de alto volumen {#high-volume-secure-information-delivery}

En un entorno de producción en masa, como el que genera facturas mensuales garantizadas para una compañía de telecomunicaciones, la creación de licencias específicas para cada documento puede convertirse en un proceso que consume muchos recursos. En estos casos, la seguridad de los documentos apoya la asociación de licencias a los usuarios, en lugar de a los documentos. La licencia generada para un usuario se utiliza para todos los documentos protegidos para ese usuario.

Una ventaja de este enfoque es que el tamaño de la base de datos de seguridad de documento no aumenta de forma lineal con los documentos, sino con el número de usuarios. Además, como debe crear la licencia una sola vez para un usuario, la protección posterior de documentos mediante estas políticas se hace más rápida. Todas estas documentos admiten funciones como acceso sin conexión, caducidad del documento y revocación.

La seguridad de documento también admite Políticas abstractas. Las directivas abstractas son plantillas de directiva que contienen todos los atributos de directiva, como la configuración de seguridad de documento y los derechos de uso, pero que no contienen una lista de entidades principales. Los administradores pueden crear cualquier cantidad de directivas a partir de la directiva abstracta con diferentes principios que deben tener acceso a los documentos. Los cambios realizados en la política abstracta no afectan a las políticas reales que se generan a partir de las políticas abstractas.

En el caso de la generación de facturas mensuales para una compañía de telecomunicaciones, se crea una política abstracta, se crean usuarios y, a continuación, se generan licencias únicas para cada usuario. Las licencias se aplican posteriormente a los documentos de cada usuario.

La creación de una directiva abstracta solo se admite mediante el SDK de Java para seguridad de documento. Sin embargo, puede administrar las directivas que cree a partir de la política abstracta desde las páginas web de seguridad de documento. Las directivas que se crean con este método tienen un comportamiento idéntico al que se crea a partir de páginas web de seguridad de documento.

Consulte [Programación con AEM formularios](https://www.adobe.com/go/learn_aemforms_programming_63) para obtener más información.
