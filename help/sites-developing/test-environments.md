---
title: ¿Qué Entornos de prueba son necesarios?
seo-title: ¿Qué Entornos de prueba son necesarios?
description: Se deben considerar varios entornos como parte de las pruebas
seo-description: Se deben considerar varios entornos como parte de las pruebas
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# ¿Qué Entornos de prueba serán necesarios?{#which-test-environments-will-be-needed}

Para definir qué configuraciones se deben probar, debe tener en cuenta lo siguiente:

**Desarrollo** : para unidades y ciertas pruebas de integración.

**Prueba** : para la mayoría de las pruebas.

**Activo** : para pruebas de resistencia y rendimiento finales. También para pruebas de aceptación con el cliente.

También tendrá que decidir qué instancias necesitará donde (normalmente al menos una de cada uno para todos los niveles de prueba):

**Autor** : Esta instancia permite a los autores introducir y publicar contenido.

**Publicar** : Esta instancia presenta el sitio web en su forma publicada para el acceso desde visitantes.

Debe probarse junto con el despachante.

Por último, se debe considerar el hardware real: cualquier prueba de rendimiento debe realizarse en un sistema lo más cerca posible de la configuración del entorno final activo. Por este motivo, también se recomienda dividir el lanzamiento del proyecto en:

**Lanzamiento**  suave: disponibilidad reducida; que permite tiempo para pruebas de rendimiento, ajuste y optimización en condiciones realistas en el entorno de producción.

**Inicio**  duro: disponibilidad completa.
