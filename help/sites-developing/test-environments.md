---
title: ¿Qué entornos de prueba son necesarios?
description: Se deben considerar varios entornos como parte de las pruebas
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# ¿Qué entornos de prueba son necesarios?{#which-test-environments-will-be-needed}

Para definir qué configuraciones se deben probar, se debe tener en cuenta lo siguiente:

**Desarrollo** - Para la unidad, y ciertas pruebas de integración.

**Pruebas** - Para la mayoría de las pruebas.

**Activo** - Para pruebas de rendimiento y de esfuerzo finales. También para pruebas de aceptación con el cliente.

Decida qué instancias necesita y dónde (normalmente al menos una de cada una para todos los niveles de prueba):

**Autor** : Esta instancia permite a los autores introducir y publicar contenido.

**Publish** - Esta instancia presenta el sitio web en su forma publicada para el acceso de los visitantes.

Probado con Dispatcher.

Por último, debe tenerse en cuenta el hardware real: cualquier prueba de rendimiento debe realizarse en un sistema lo más cerca posible del entorno en directo final. Por este motivo, también se recomienda dividir el lanzamiento del proyecto en un:

**Lanzamiento suave** - Disponibilidad reducida; lo que permite tiempo para pruebas de rendimiento, ajuste y optimización en condiciones realistas en el entorno de producción.

**Lanzamiento duro** - Disponibilidad total.
