---
title: Creación de filtros de grupo de dispositivos
description: Cree un filtro de grupo de dispositivos para definir un conjunto de requisitos de capacidad de los dispositivos
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
exl-id: 419d2e19-1198-4ab5-9aa0-02ad18fe171d
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Creación de filtros de grupo de dispositivos{#creating-device-group-filters}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Cree un filtro de grupo de dispositivos para definir un conjunto de requisitos de capacidad de los dispositivos. Cree tantos filtros como necesite para dirigirse a los grupos necesarios de capacidades de dispositivos.

Diseñe los filtros de modo que pueda utilizar combinaciones de ellos para definir los grupos de capacidades. Normalmente, hay superposición de las capacidades de diferentes grupos de dispositivos. Por lo tanto, puede utilizar algunos filtros con varias definiciones de grupos de dispositivos.

Después de crear un filtro, puede utilizarlo en el [configuración del grupo.](/help/sites-developing/mobile.md#creating-a-device-group)

## La clase Filter Java™ {#the-filter-java-class}

Un filtro de grupo de dispositivos es un componente OSGi que implementa la variable [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) interfaz. Cuando se implementa, la clase de implementación proporciona un servicio de filtro disponible para las configuraciones de grupo de dispositivos.

La solución descrita en este artículo utiliza el complemento Apache Felix Maven SCR para facilitar el desarrollo del componente y el servicio. Por lo tanto, la clase Java™ de ejemplo utiliza la variable `@Component`y `@Service` anotaciones. La clase tiene la siguiente estructura:

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

Proporcione código para los siguientes métodos:

* `getDescription`: Devuelve la descripción del filtro. La descripción aparece en el cuadro de diálogo de configuración del grupo de dispositivos.
* `getTitle`: Devuelve el nombre del filtro. El nombre aparece al seleccionar filtros para el grupo de dispositivos.
* `matches`: Determina si el dispositivo tiene las capacidades requeridas.

### Proporción del nombre y la descripción del filtro {#providing-the-filter-name-and-description}

El `getTitle` y `getDescription` Los métodos de devuelven el nombre del filtro y la descripción, respectivamente. El siguiente código ilustra la implementación más sencilla:

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

Codificar el nombre y el texto de descripción es suficiente para entornos de creación multilingües. Considere la posibilidad de externalizar las cadenas para uso multilingüe o para habilitar el cambio de cadenas sin volver a compilar el código fuente.

### Evaluación según los criterios de filtro {#evaluating-against-filter-criteria}

El `matches` función devuelve `true` si las capacidades del dispositivo cumplen todos los criterios de filtro. Evalúe la información proporcionada en los argumentos del método para determinar si el dispositivo pertenece al grupo. Se proporcionan los siguientes valores como argumentos:

* Un objeto DeviceGroup
* El nombre del agente de usuario
* Objeto Map que contiene las funciones del dispositivo. Las claves de mapa son los nombres de capacidad WURFL™ y los valores son los valores correspondientes de la base de datos WURFL™.

El [com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstants](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) La interfaz contiene un subconjunto de los nombres de capacidad WURFL™ en campos estáticos. Utilice estas constantes de campo como claves al recuperar valores desde el Mapa de capacidades de dispositivo.

Por ejemplo, el siguiente ejemplo de código determina si el dispositivo admite CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

El `org.apache.commons.lang.math` El paquete proporciona el `NumberUtils` clase.

>[!NOTE]
>
>AEM Asegúrese de que la base de datos WURFL™ implementada para incluir las capacidades que utiliza como criterio de filtro. (Consulte [Detección de dispositivos](/help/sites-developing/mobile.md#server-side-device-detection).)

### Filtro De Ejemplo Para El Tamaño De Pantalla {#example-filter-for-screen-size}

El ejemplo de implementación de DeviceGroupFilter que se muestra a continuación determina si el tamaño físico del dispositivo cumple los requisitos mínimos. Este filtro está diseñado para agregar granularidad al grupo de dispositivos táctiles. El tamaño de los botones en la interfaz de usuario de la aplicación debe ser el mismo independientemente del tamaño de la pantalla física. El tamaño de otros elementos, como el texto, puede variar. El filtro permite la selección dinámica de un CSS concreto que controla el tamaño de los elementos de la interfaz de usuario.

Este filtro aplica criterios de tamaño a `physical_screen_height` y `physical_screen_width` WURFL™ nombres de propiedades.

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

El valor de tipo String que devuelve el método getTitle aparece en la lista desplegable de las propiedades del grupo de dispositivos.

![filteraddtogroup](assets/filteraddtogroup.png)

Los valores de tipo String que devuelven los métodos getTitle y getDescription se incluyen en la parte inferior de la página de resumen del grupo de dispositivos.

![filterdescription](assets/filterdescription.png)

### El archivo POM de Maven {#the-maven-pom-file}

El siguiente código POM es útil si utiliza Maven para crear sus aplicaciones. El POM hace referencia a varios complementos y dependencias necesarios.

**Complementos:**

* Complemento del compilador de Apache Maven: compila clases de Java™ a partir del código fuente.
* Complemento Apache Felix Maven Bundle: Crea el paquete y el manifiesto
* Complemento Apache Felix Maven SCR: Crea el archivo descriptor de componente y configura el encabezado de manifiesto del componente de servicio.

**Dependencias:**

* `cq-wcm-mobile-api-5.5.2.jar`: proporciona las interfaces DeviceGroup y DeviceGroupFilter.

* `org.apache.felix.scr.annotations.jar`: proporciona las anotaciones Componente y Servicio.

Las interfaces DeviceGroup y DeviceGroupFilter se incluyen en el paquete de la API móvil de WCM de la comunicación de día 5. Las anotaciones de Felix se incluyen en el paquete de servicios declarativos de Apache Felix. Puede obtener este archivo JAR del repositorio de Adobe público.

AEM En el momento de la creación, 5.5.2 es la versión del paquete de la API móvil de WCM que se encuentra en la última versión de. Usar la consola web de Adobe ([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)) para asegurarse de que esta sea la versión del paquete implementada en su entorno.

**POM:** (El POM utiliza un groupId y una versión diferentes).

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

Añada el perfil que el [Obtención del complemento Maven del paquete de contenido](/help/sites-developing/vlt-mavenplugin.md) proporciona al archivo de configuración de maven para utilizar el repositorio de Adobe público.
