---
title: Inicio y parada de la línea de comandos
description: Obtenga información sobre cómo iniciar y detener Adobe Experience Manager desde la línea de comandos.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Inicio y parada de la línea de comandos{#command-line-start-and-stop}

## Iniciar Adobe Experience Manager desde la línea de comandos {#starting-adobe-experience-manager-from-the-command-line}

El script `start` está disponible en *el directorio &lt;cq-installation>/bin*. Se proporcionan las versiones UNIX® y Windows. El script inicia la instancia instalada en el directorio *&lt;cq-installation>*.

Estas dos versiones admiten una lista de variables de entorno que pueden utilizarse para iniciar y ajustar la instancia de Adobe Experience Manager AEM ().

<table>
 <tbody>
  <tr>
   <td><strong>Variable de entorno </strong></td>
   <td><strong>Descripción </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>Puerto TCP utilizado para los scripts de estado y detención <br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>Nombre de host<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>Interfaz que este servidor debe escuchar <br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>Modos de ejecución separados por comas <br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>Nombre del archivo jarr<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAS</td>
   <td>Uso de JAAS (si es verdadero)<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAS_CONFIG</td>
   <td>Ruta de acceso de la configuración de JAAS <br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>Opciones de JVM predeterminadas<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>AEM Algunos modos de ejecución, entre ellos autor y publicación, deben configurarse antes de comenzar la ejecución por primera vez y no se pueden cambiar posteriormente. AEM Antes de configurar una instancia de que se usa en la producción, consulte [documentación sobre los modos de ejecución](/help/sites-deploying/configure-runmodes.md) para obtener más información.

### Ejemplo de script start.bat de la plataforma Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Ejemplo de script de inicio de la plataforma UNIX® {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>AEM El script de inicio inicia el inicio rápido de la aplicación instalado en la carpeta &lt;cq-installation>/app *de*.

## Detención de Adobe Experience Manager {#stopping-adobe-experience-manager}

AEM Para detener la, siga uno de estos procedimientos:

* Según la plataforma que utilice:

   * AEM Si ha iniciado el proceso desde un script o desde la línea de comandos, presione **Ctrl+C** para apagar el servidor.
   * AEM Si ha utilizado la secuencia de comandos de inicio en UNIX®, debe utilizar la secuencia de comandos de detención para detener la ejecución de los programas de la aplicación de la.

* AEM Si ha empezado a hacer clic en el archivo jar, haga clic en el botón **Activar** de la ventana de inicio (el botón cambia a **Desactivar**) para cerrar el servidor.

  ![chlimage_1-63](assets/chlimage_1-63.png)

## Detención de Adobe Experience Manager desde la línea de comandos {#stopping-adobe-experience-manager-from-the-command-line}

El script `stop` está disponible en *el directorio &lt;cq-installation>/bin*. Se proporcionan las versiones UNIX® y Windows. El script detiene la instancia en ejecución instalada en el directorio *&lt;cq-installation>*.

### Ejemplo de script de detención de plataforma UNIX® {#unix-platform-stop-script-example}

```shell
./stop
```

### Ejemplo de script stop.bat de la plataforma Windows {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Si solo desea preconfigurar el repositorio (sin reubicarlo), solo tiene que:

* Extraer `repository.xml` a la ubicación requerida

* actualizar `repository.xml` según sea necesario

* crear `bootstrap.properties` y definir `repository.config`

De nuevo, antes de iniciar la instalación real.
