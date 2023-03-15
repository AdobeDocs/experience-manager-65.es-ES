---
title: ¿Qué entornos de prueba son necesarios?
seo-title: Which Test Environments are needed?
description: Se deben considerar varios entornos como parte de las pruebas
seo-description: Several environments should be considered as part of testing
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# ¿Qué entornos de prueba se necesitarán?{#which-test-environments-will-be-needed}

Para definir qué configuraciones se deben probar, se debe tener en cuenta lo siguiente:

**Desarrollo** - Para la unidad, y ciertas pruebas de integración.

**Pruebas** - Para la mayoría de las pruebas.

**Activo** - Para pruebas de rendimiento y de esfuerzo finales. También para pruebas de aceptación con el cliente.

También deberá decidir qué instancias necesitará dónde (normalmente, al menos una de cada una para todos los niveles de prueba):

**Autor** : Esta instancia permite a los autores introducir y publicar contenido.

**Publish** - Esta instancia presenta el sitio web en su forma publicada para el acceso de los visitantes.

Debe probarse junto con Dispatcher.

Por último, debe tenerse en cuenta el hardware real: cualquier prueba de rendimiento debe realizarse en un sistema lo más cerca posible del entorno en directo final. Por este motivo, también se recomienda dividir el lanzamiento del proyecto en un:

**Lanzamiento suave** - Disponibilidad reducida; lo que permite tiempo para pruebas de rendimiento, ajuste y optimización en condiciones realistas en el entorno de producción.

**Lanzamiento duro** - Disponibilidad total.
