---
title: Ver información del sistema
seo-title: View system information
description: Descubra cómo puede ver gráficos de monitorización de recursos e información sobre el servidor que ejecuta AEM formularios.
seo-description: Learn how you can view resource monitoring charts and information about the server that is running AEM forms.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Ver información del sistema {#view-system-information}

La ficha Sistema muestra gráficos de supervisión de recursos e información sobre el servidor que ejecuta AEM formularios. Para acceder a esta información, en la consola de administración, haga clic en Monitor de estado en la esquina superior derecha de la página. Si está ejecutando AEM formularios en un entorno agrupado, la información mostrada es para el nodo seleccionado en la lista Servidor.

Para guardar la información actual del sistema como un archivo de propiedades, haga clic en Guardar.

El panel derecho de la ficha Sistema muestra representaciones gráficas de la siguiente información:

* Elementos de trabajo y recuento de trabajo
* Uso de montículos y montículos comprometidos
* Uso sin montículos y sin montículos comprometidos

Puede arrastrar el puntero a lo largo de la cronología para obtener valores para un punto en el tiempo en particular.

>[!NOTE]
>
>Los datos del gráfico, los valores de la información del servidor y el tiempo de reloj se actualizan cada 10 minutos. La información no se muestra en tiempo real.

El panel izquierdo de la ficha Sistema muestra la siguiente información sobre el servidor o nodo:

**Máquina virtual:** Versión Java Virtual Machine (JVM) en el servidor.

**Proveedor de máquina virtual:** Fabricante de la JVM.

**Versión de máquina virtual:** Número de versión de JVM

**Nombre del equipo:** Nombre de host del servidor en el que están instalados AEM formularios.

**Tiempo de espera:** Tiempo, en horas y minutos, que el servidor ha estado ejecutando.

**Compilador Just-In-Time:** Nombre del compilador que se está utilizando.

**Tiempo de compilación:** Cantidad de tiempo empleado en la compilación.

**Número de subprocesos en directo:** Número total de subprocesos presentes actualmente en el sistema de formularios AEM.

**Número máximo de subprocesos:** El mayor número de subprocesos en directo jamás registrado en el sistema.

**Número de clases cargadas:** Número de clases cargadas en la JVM.

**Número de clases descargadas:** Número de clases descargadas de la JVM.

**Superficie mínima:** Cantidad mínima de memoria que se utilizó.

**Montaje máximo:** Cantidad máxima de memoria que se utilizó.

**Nombre del sistema operativo:** Nombre del sistema operativo que se ejecuta en el servidor de AEM forms.

**Versión del sistema operativo:** Número de versión del sistema operativo que se ejecuta en el servidor de AEM forms.

**Arco del sistema operativo:** La arquitectura del sistema operativo en la que se ejecuta la JVM.

**Número de procesadores:** Número de procesadores del sistema.

**Argumentos de máquina virtual:** El argumento utilizado por la JVM.

**Ruta de clase:** Ruta de clase utilizada por la JVM.

**Ruta de biblioteca:** Ruta de biblioteca utilizada por la JVM.

**Ruta de clase de arranque:** Ruta de clase de arranque utilizada por la JVM.

**Tipo de servidor de aplicaciones:** Tipo de servidor de aplicaciones utilizado para ejecutar AEM formularios.

**Versión del servidor de aplicaciones:** Número de versión del servidor de aplicaciones utilizado para ejecutar AEM formularios.

**Proveedor del servidor de aplicaciones:** Fabricante del servidor de aplicaciones utilizado para ejecutar AEM formularios.

**Fecha de instalación:** Fecha (en formato aaaa-mm-dd) en que se instalaron AEM formularios.

**AEM versión de formularios:** Versión de AEM formularios instalados.

**Versión del parche:** AEM número de parche de formularios.

**Nombre de base de datos:** Tipo de base de datos utilizada por AEM formularios.

**Versión de la base de datos:** Número de versión de la base de datos utilizada por AEM formularios.

**Nombre de unidad de base de datos:** Nombre del controlador que utiliza la JVM para conectarse a la base de datos.

**Versión del controlador de base de datos:** Versión del controlador utilizado por la JVM para conectarse a la base de datos.

La variable **Guardar** permite guardar esta información del sistema en un archivo de propiedad.
