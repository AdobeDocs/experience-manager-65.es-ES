---
title: Ver información del sistema
description: AEM Obtenga información sobre cómo ver gráficos de monitorización de recursos e información sobre el servidor que ejecuta formularios en la aplicación de la versión de la aplicación de datos de la aplicación de la versión de.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
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

**Máquina virtual:** Versión de máquina virtual Java (JVM) en el servidor.

**Proveedor de máquina virtual:** fabricante de JVM.

**Versión de máquina virtual:** Número de versión de JVM

AEM **Nombre de equipo:** Nombre de host del servidor donde se instalaron los formularios de la.

**Tiempo de actividad:** El tiempo, en horas y minutos, que el servidor ha estado funcionando.

**Compilador Just-In-Time:** nombre del compilador que se está utilizando.

**Tiempo de compilación:** Cantidad de tiempo empleado en la compilación.

**Número de subprocesos de Live Threads AEM:** Número total de subprocesos presentes actualmente en el sistema de formularios de la.

**Número máximo de Threads:** El mayor número de subprocesos activos registrados en el sistema.

**Número de clases cargadas:** Número de clases cargadas en la JVM.

**Número de clases descargadas:** Número de clases descargadas de JVM.

**Montón mínimo:** Cantidad mínima de montón que se utilizó.

**Montón máximo:** Cantidad máxima de montón que se ha utilizado.

**Nombre del sistema operativo:** El nombre del sistema operativo que se ejecuta en el servidor de AEM Forms.

**Versión del sistema operativo:** Número de versión del sistema operativo que se ejecuta en AEM Forms Server.

**Arco del sistema operativo:** Arquitectura del sistema operativo en la que se está ejecutando JVM.

**Número de procesadores:** El número de procesadores del sistema.

**Argumentos de máquina virtual:** Argumento utilizado por JVM.

**Ruta de clase:** Ruta de clase utilizada por JVM.

**Ruta de biblioteca:** Ruta de biblioteca utilizada por JVM.

**Ruta de clase de arranque:** Ruta de clase de arranque utilizada por JVM.

AEM **Tipo de servidor de aplicaciones:** Tipo de servidor de aplicaciones usado para ejecutar formularios de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación.

AEM **Versión del servidor de aplicaciones:** Número de versión del servidor de aplicaciones utilizado para ejecutar formularios de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación.

AEM **Proveedor del servidor de aplicaciones:** Fabricante del servidor de aplicaciones que se usa para ejecutar formularios de la.

AEM **Fecha de instalación:** Fecha (en formato aaaa-mm-dd) en la que se instalaron los formularios de la.

AEM AEM **Versión de formularios de:** Versión de los formularios de formularios instalados.

AEM **Versión del parche:** número de parche de formularios de la aplicación de formularios de la aplicación.

AEM **Nombre de base de datos:** Tipo de base de datos usada por los formularios de la base de datos de los formularios de la.

AEM **Versión de la base de datos:** Número de versión de la base de datos usada por los formularios de la base de datos de los formularios de la base de datos de los formularios de datos.

**Nombre de la unidad de base de datos:** Nombre del controlador utilizado por JVM para conectarse a la base de datos.

**Versión del controlador de base de datos:** Versión del controlador utilizado por JVM para conectarse a la base de datos.

El botón **Guardar** le permite guardar esta información del sistema en un archivo de propiedades.
