---
title: Creación de filtros de grupo de dispositivos
seo-title: Creating Device Group Filters
description: Crear un filtro de grupo de dispositivos para definir un conjunto de requisitos de capacidad de dispositivos
seo-description: Create a device group filter to define a set of device capability requirements
uuid: 30c0699d-2388-41b5-a062-f5ea9d6f08bc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 9fef1f91-a222-424a-8e20-3599bedb8b41
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
exl-id: 419d2e19-1198-4ab5-9aa0-02ad18fe171d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Creación de filtros de grupo de dispositivos{#creating-device-group-filters}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Cree un filtro de grupo de dispositivos para definir un conjunto de requisitos de capacidad de dispositivos. Cree tantos filtros como necesite para dirigirse a los grupos necesarios de capacidades del dispositivo.

Diseñe los filtros de modo que pueda utilizar combinaciones de ellos para definir los grupos de capacidades. Normalmente, hay superposición de las capacidades de diferentes grupos de dispositivos. Por lo tanto, puede utilizar algunos filtros con varias definiciones de grupo de dispositivos.

Después de crear un filtro, puede utilizarlo en la [configuración de grupo.](/help/sites-developing/mobile.md#creating-a-device-group)

## La clase Java de filtro {#the-filter-java-class}

Un filtro de grupo de dispositivos es un componente OSGi que implementa el [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) interfaz. Cuando se implementa, la clase de implementación proporciona un servicio de filtro que está disponible para las configuraciones de grupo de dispositivos.

La solución descrita en este artículo utiliza el plugin Apache Felix Maven SCR para facilitar el desarrollo del componente y el servicio. Por lo tanto, la clase Java de ejemplo utiliza la variable `@Component`y `@Service` anotaciones. La clase tiene la siguiente estructura:

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

* `getDescription`: Devuelve la descripción del filtro. La descripción aparece en el cuadro de diálogo de configuración del grupo de dispositivos.
* `getTitle`: Devuelve el nombre del filtro. El nombre aparece al seleccionar filtros para el grupo de dispositivos.
* `matches`: Determina si el dispositivo tiene las capacidades necesarias.

### Proporcionar el nombre y la descripción del filtro {#providing-the-filter-name-and-description}

La variable `getTitle` y `getDescription` los métodos devuelven el nombre y la descripción del filtro, respectivamente. El siguiente código ilustra la implementación más sencilla:

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

La codificación rígida del texto del nombre y la descripción es suficiente para los entornos de creación uni-lingües. Considere la posibilidad de externalizar las cadenas para uso multilingüe o para permitir el cambio de cadenas sin volver a compilar el código fuente.

### Evaluar Con Criterios De Filtro {#evaluating-against-filter-criteria}

La variable `matches` devuelve `true` si las capacidades del dispositivo cumplen todos los criterios del filtro. Evalúe la información proporcionada en argumentos de método para determinar si el dispositivo pertenece al grupo. Los siguientes valores se proporcionan como argumentos:

* Un objeto DeviceGroup
* Nombre del agente de usuario
* Un objeto Map que contiene las capacidades del dispositivo. Las claves Map son los nombres de las capacidades WURFL™ y los valores son los valores correspondientes de la base de datos WURFL™.

La variable [com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstants](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) contiene un subconjunto de los nombres de la capacidad WURFL™ en campos estáticos. Utilice estas constantes de campo como claves al recuperar valores del mapa de las capacidades del dispositivo.

Por ejemplo, el siguiente ejemplo de código determina si el dispositivo es compatible con CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

La variable `org.apache.commons.lang.math` proporciona el `NumberUtils` Clase .

>[!NOTE]
>
>Asegúrese de que la base de datos WURFL™ implementada en AEM incluye las capacidades que utiliza como criterios de filtro. (Consulte [Detección de dispositivos](/help/sites-developing/mobile.md#server-side-device-detection).)

### Filtro de ejemplo para tamaño de pantalla {#example-filter-for-screen-size}

El ejemplo de implementación de DeviceGroupFilter que se muestra a continuación determina si el tamaño físico del dispositivo cumple los requisitos mínimos. Este filtro está diseñado para añadir granularidad al grupo de dispositivos táctiles. El tamaño de los botones en la interfaz de usuario de la aplicación debe ser el mismo independientemente del tamaño de la pantalla física. El tamaño de otros elementos, como el texto, puede variar. El filtro permite la selección dinámica de una CSS concreta que controla el tamaño de los elementos de la interfaz de usuario.

Este filtro aplica criterios de tamaño a la variable `physical_screen_height` y `physical_screen_width` Nombres de propiedades WURFL™.

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

El valor String que devuelve el método getTitle aparece en la lista desplegable de las propiedades del grupo de dispositivos.

![filteraddtogroup](assets/filteraddtogroup.png)

Los valores de cadena que devuelven los métodos getTitle y getDescription se incluyen en la parte inferior de la página de resumen del grupo de dispositivos.

![filterdescription](assets/filterdescription.png)

### El archivo Maven POM {#the-maven-pom-file}

El siguiente código POM es útil si utiliza Maven para crear sus aplicaciones. El POM hace referencia a varios complementos y dependencias necesarios.

**Plugins:**

* Complemento Compilador Apache Maven: Compila las clases Java a partir del código fuente.
* Complemento Apache Felix Maven Bundle: Crea el paquete y el manifiesto
* Complemento Apache Felix Maven SCR: Crea el archivo descriptor de componente y configura el encabezado de manifiesto de componente de servicio.

**Dependencias:**

* `cq-wcm-mobile-api-5.5.2.jar`: Proporciona las interfaces DeviceGroup y DeviceGroupFilter .

* `org.apache.felix.scr.annotations.jar`: Proporciona las anotaciones Componente y Servicio .

Las interfaces DeviceGroup y DeviceGroupFilter están incluidas en el paquete de API móvil WCM Day Communique 5. Las anotaciones Felix están incluidas en el paquete de servicios declarativos Apache Felix. Puede obtener este archivo JAR del repositorio de Adobe público.

En el momento de la creación, 5.5.2 es la versión del paquete de API de WCM Mobile que se encuentra en la última versión de AEM. Usar la consola web de Adobe ([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)) para garantizar que esta es la versión del paquete que se implementa en su entorno.

**POM:** (El POM utilizará un groupId y una versión diferentes).

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

Añada el perfil en el que [Obtención del complemento Maven del paquete de contenido](/help/sites-developing/vlt-mavenplugin.md) proporciona al archivo de configuración de maven para utilizar el repositorio de Adobe público.
