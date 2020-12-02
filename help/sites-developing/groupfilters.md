---
title: Creación de Filtros de grupos de dispositivos
seo-title: Creación de Filtros de grupos de dispositivos
description: Crear un filtro de grupo de dispositivos para definir un conjunto de requisitos de capacidad de dispositivos
seo-description: Crear un filtro de grupo de dispositivos para definir un conjunto de requisitos de capacidad de dispositivos
uuid: 30c0699d-2388-41b5-a062-f5ea9d6f08bc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 9fef1f91-a222-424a-8e20-3599bedb8b41
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---


# Creación de Filtros de grupo de dispositivos{#creating-device-group-filters}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Cree un filtro de grupo de dispositivos para definir un conjunto de requisitos de capacidad de dispositivos. Cree tantos filtros como necesite para realizar el destinatario de los grupos necesarios de funciones de dispositivo.

Diseñe sus filtros para que pueda utilizar combinaciones de ellas y definir los grupos de funciones. Generalmente, las capacidades de los distintos grupos de dispositivos se superponen. Por lo tanto, puede usar algunos filtros con varias definiciones de grupos de dispositivos.

Después de crear un filtro, puede utilizarlo en la configuración de grupo [.](/help/sites-developing/mobile.md#creating-a-device-group)

## La clase Java de filtro {#the-filter-java-class}

Un filtro de grupo de dispositivos es un componente OSGi que implementa la interfaz [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html). Cuando se implementa, la clase de implementación proporciona un servicio de filtro que está disponible para las configuraciones de grupo de dispositivos.

La solución descrita en este artículo utiliza el complemento Apache Felix Maven SCR para facilitar el desarrollo del componente y el servicio. Por lo tanto, la clase Java de ejemplo utiliza las anotaciones `@Component`y `@Service`. La clase tiene la siguiente estructura:

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
public class myDeviceGroupFilter implements DeviceGroupFilter {

       public String getDescription() {
  return null;
 }

 public String getTitle() {
  return null;
 }

 public boolean matches(DeviceGroup arg0, String arg1, Map arg2) {
  return false;
 }

}
```

Debe proporcionar código para los siguientes métodos:

* `getDescription`:: Devuelve la descripción del filtro. La descripción aparece en el cuadro de diálogo de configuración Grupo de dispositivos.
* `getTitle`:: Devuelve el nombre del filtro. El nombre aparece al seleccionar filtros para el grupo de dispositivos.
* `matches`:: Determina si el dispositivo tiene las capacidades necesarias.

### Proporcionar el nombre y la descripción del filtro {#providing-the-filter-name-and-description}

Los métodos `getTitle` y `getDescription` devuelven el nombre y la descripción del filtro, respectivamente. El código siguiente ilustra la implementación más sencilla:

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

La precodificación del texto del nombre y la descripción es suficiente para los entornos de creación no lingüísticos. Considere la externalización de las cadenas para uso multilingüe o para activar el cambio de cadenas sin volver a compilar el código fuente.

### Evaluar con criterios de filtro {#evaluating-against-filter-criteria}

La función `matches` devuelve `true` si las capacidades del dispositivo cumplen todos los criterios del filtro. Evalúe la información proporcionada en los argumentos de método para determinar si el dispositivo pertenece al grupo. Los siguientes valores se proporcionan como argumentos:

* Un objeto DeviceGroup
* El nombre del agente de usuario
* Objeto Map que contiene las capacidades del dispositivo. Las claves de mapa son los nombres de la capacidad WURFL™ y los valores son los valores correspondientes de la base de datos WURFL™.

La interfaz [com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstances](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) contiene un subconjunto de los nombres de capacidad de WURFL™ en campos estáticos. Utilice estas constantes de campo como claves al recuperar valores del mapa de capacidades del dispositivo.

Por ejemplo, el siguiente ejemplo de código determina si el dispositivo admite CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

El paquete `org.apache.commons.lang.math` proporciona la clase `NumberUtils`.

>[!NOTE]
>
>Asegúrese de que la base de datos WURFL™ implementada en AEM incluye las funciones que utiliza como criterios de filtro. (Consulte [Detección de dispositivos](/help/sites-developing/mobile.md#server-side-device-detection)).

### Ejemplo de filtro para tamaño de pantalla {#example-filter-for-screen-size}

La implementación DeviceGroupFilter de ejemplo que se muestra a continuación determina si el tamaño físico del dispositivo cumple los requisitos mínimos. Este filtro está diseñado para añadir granularidad al grupo de dispositivos táctiles. El tamaño de los botones en la interfaz de usuario de la aplicación debe ser el mismo independientemente del tamaño de pantalla físico. El tamaño de otros elementos, como el texto, puede variar. El filtro habilita la selección dinámica de un CSS concreto que controla el tamaño de los elementos de la interfaz de usuario.

Este filtro aplica criterios de tamaño a los nombres de propiedades `physical_screen_height` y `physical_screen_width` WURFL™.

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.commons.lang.math.NumberUtils;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
@SuppressWarnings("unused")
public class ScreenSizeLarge implements DeviceGroupFilter {
    private int len=400;
    private int wid=200;
    public String getDescription() {

        return "Requires the physical size of the screen to have minimum dimensions " + len + "x" + wid+".";
    }

    public String getTitle() {
        return "Screen Size Large ("+len + "x" + wid+")";
    }

    public boolean matches(DeviceGroup deviceGroup, String userAgent,
            Map<String, String> deviceCapabilities) {

        boolean longEnough=true;
        boolean wideEnough=false;
        int dimension1=NumberUtils.toInt(deviceCapabilities.get("physical_screen_height"));
        int dimension2=NumberUtils.toInt(deviceCapabilities.get("physical_screen_width"));
        if(dimension1>dimension2){
            longEnough=dimension1>=len;
            wideEnough=dimension2>=wid;
        }else{
            longEnough=dimension2>=len;
            wideEnough=dimension1>=wid;
        }

        return longEnough && wideEnough;
    }
}
```

El valor String que devuelve el método getTitle aparece en la lista desplegable de las propiedades de grupo del dispositivo.

![filteraddtogroup](assets/filteraddtogroup.png)

Los valores de tipo String que devuelven los métodos getTitle y getDescription se incluyen en la parte inferior de la página de resumen del grupo de dispositivos.

![filterdescription](assets/filterdescription.png)

### El archivo Maven POM {#the-maven-pom-file}

El siguiente código POM resulta útil si utiliza Maven para crear sus aplicaciones. El POM hace referencia a varios complementos y dependencias requeridos.

**Plugins:**

* Complemento del compilador Apache Maven: Compila clases Java a partir del código fuente.
* Complemento Apache Felix Maven Bundle: Crea el paquete y el manifiesto
* Complemento Apache Felix Maven SCR: Crea el archivo descriptor de componente y configura el encabezado de manifiesto service-component.

**Dependencias:**

* `cq-wcm-mobile-api-5.5.2.jar`:: Proporciona las interfaces DeviceGroup y DeviceGroupFilter.

* `org.apache.felix.scr.annotations.jar`:: Proporciona las anotaciones Componente y Servicio.

Las interfaces DeviceGroup y DeviceGroupFilter se incluyen en el paquete de la API móvil de Day Community 5 WCM. Las anotaciones Felix se incluyen en el paquete de servicios declarativos Apache Felix. Puede obtener este archivo JAR del repositorio público de Adobe.

En el momento de la creación, 5.5.2 es la versión del paquete de API de WCM Mobile que se encuentra en la última versión de AEM. Utilice la consola web de Adobe ([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)) para asegurarse de que esta es la versión del paquete que se implementa en el entorno.

**POM:** (Su POM usará un groupId y una versión diferentes).

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
        xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.adobe.example.myapp</groupId>
      <artifactId>devicefilter</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>my app device filter</name>
      <url>https://dev.day.com/docs/en/cq/current.html</url>
  <packaging>bundle</packaging>
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-scr-plugin</artifactId>
            <executions>
                  <execution>
                    <id>generate-scr-scrdescriptor</id>
                    <goals>
                          <goal>scr</goal>
                    </goals>
                  </execution>
            </executions>
          </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
    </plugins>
</build>
<dependencies>
     <dependency>
         <groupId>com.day.cq.wcm</groupId>
         <artifactId>cq-wcm-mobile-api</artifactId>
         <version>5.5.2</version>
         <scope>provided</scope>
     </dependency>
     <dependency>
        <groupId>org.apache.felix</groupId>
        <artifactId>org.apache.felix.scr.annotations</artifactId>
        <version>1.6.0</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
</project>
```

Añada el perfil que la sección [Obtención del complemento Maven del paquete de contenido](/help/sites-developing/vlt-mavenplugin.md) proporciona al archivo de configuración principal para utilizar el repositorio público de Adobe.
