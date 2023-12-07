---
title: Ver información del sistema
description: AEM Obtenga información sobre cómo ver gráficos de monitorización de recursos e información sobre el servidor que ejecuta formularios en la aplicación de la versión de la aplicación de datos de la aplicación de la versión de.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 1%

---

# Ver información del sistema {#view-system-information}

AEM La pestaña Sistema muestra gráficos de monitorización de recursos e información sobre el servidor que ejecuta los formularios de la. Para acceder a esta información, en la consola de administración, haga clic en Monitor de estado en la esquina superior derecha de la página. AEM Si está ejecutando formularios en un entorno agrupado, la información mostrada es para el nodo seleccionado en la lista Servidor.

Para guardar la información actual del sistema como un archivo de propiedades, haga clic en Guardar.

El panel derecho de la pestaña Sistema muestra representaciones gráficas de la siguiente información:

* Elementos de trabajo y recuento de trabajo
* Uso de pila y pila comprometida
* Uso sin montón y sin montón comprometido

Puede arrastrar el puntero a lo largo de la cronología para obtener los valores de un momento determinado.

>[!NOTE]
>
>Los datos de gráficos, los valores de información del servidor y la hora del reloj se actualizan cada 10 minutos. La información no se muestra en tiempo real.

El panel izquierdo de la ficha Sistema muestra la siguiente información sobre el servidor o nodo:

**Máquina virtual:** Versión de Java Virtual Machine (JVM) en el servidor.

**Proveedor de máquina virtual:** Fabricante de JVM.

**Versión de máquina virtual:** Número de versión de JVM

**Nombre de la máquina:** AEM Nombre del host del servidor en el que se instalan los formularios de.

**Tiempo de actividad:** El tiempo, en horas y minutos, que ha estado ejecutando el servidor.

**Compilador justo a tiempo:** Nombre del compilador que se está utilizando.

**Tiempo de compilación:** Cantidad de tiempo empleado en la compilación.

**Número de Live Threads:** AEM Número total de subprocesos presentes actualmente en el sistema de formularios de la.

**Número máximo de Threads:** Número máximo de subprocesos activos registrados en el sistema.

**Número de clases cargadas:** Número de clases cargadas en la JVM.

**Número de clases descargadas:** Número de clases descargadas de la JVM.

**Montón mínimo:** Cantidad mínima de pila que se ha utilizado.

**Montón máximo:** Cantidad máxima de pila que se ha utilizado.

**Nombre del sistema operativo:** Nombre del sistema operativo que se ejecuta en el servidor de AEM Forms.

**Versión del sistema operativo:** Número de versión del sistema operativo que se ejecuta en AEM Forms Server.

**Arco del sistema operativo:** Arquitectura del sistema operativo en la que se ejecuta JVM.

**Número de procesadores:** Número de procesadores del sistema.

**Argumentos de máquina virtual:** Argumento utilizado por JVM.

**Ruta de clase:** Ruta de clase utilizada por JVM.

**Ruta de biblioteca:** Ruta de biblioteca utilizada por JVM.

**Ruta de clase de arranque:** Ruta de clase de arranque utilizada por JVM.

**Tipo de servidor de aplicaciones:** AEM Tipo de servidor de aplicaciones que se utiliza para ejecutar formularios en la.

**Versión del servidor de aplicaciones:** AEM Número de versión del servidor de aplicaciones que se utiliza para ejecutar formularios de la.

**Proveedor de servidor de aplicaciones:** AEM Fabricante del servidor de aplicaciones que se utiliza para ejecutar los formularios de la.

**Fecha de instalación:** AEM Fecha (en formato aaaa-mm-dd) en la que se instalaron los formularios de la.

**AEM Versión de formularios de:** AEM Versión de los formularios instalados.

**Versión del parche:** AEM Número de parche de formularios de.

**Nombre de base de datos:** AEM Tipo de base de datos utilizada por los formularios de.

**Versión de base de datos:** AEM Número de versión de la base de datos utilizada por los formularios de.

**Nombre de unidad de base de datos:** Nombre del controlador utilizado por JVM para conectarse a la base de datos.

**Versión del controlador de base de datos:** La versión del controlador utilizado por JVM para conectarse a la base de datos.

El **Guardar** permite guardar esta información del sistema en un archivo de propiedades.
