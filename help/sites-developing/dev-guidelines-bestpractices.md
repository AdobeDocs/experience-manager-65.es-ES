---
title: 'Desarrollo de AEM: directrices y prácticas recomendadas'
seo-title: 'Desarrollo de AEM: directrices y prácticas recomendadas'
description: Directrices y mejores prácticas para la elaboración de AEM
seo-description: Directrices y mejores prácticas para la elaboración de AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%

---


# Desarrollo de AEM - Directrices y prácticas recomendadas{#aem-development-guidelines-and-best-practices}

## Directrices para el uso de plantillas y componentes {#guidelines-for-using-templates-and-components}

AEM componentes y plantillas forman un conjunto de herramientas muy potente. Los desarrolladores pueden utilizarlos para proporcionar a los usuarios comerciales, editores y administradores del sitio web la funcionalidad de adaptar sus sitios web a las cambiantes necesidades comerciales (agilidad del contenido), manteniendo al mismo tiempo el diseño uniforme de los sitios (protección de la marca).

Un desafío típico para una persona responsable de un sitio web, o conjunto de sitios web (por ejemplo, en una sucursal de una empresa global), es introducir un nuevo tipo de presentación de contenido en sus sitios web.

Supongamos que es necesario agregar una página de lista de noticias a los sitios web, que lista extractos de otros artículos ya publicados. La página debe tener el mismo diseño y estructura que el resto del sitio web.

La manera recomendada de abordar ese problema sería:

* Reutilice una plantilla existente para crear un nuevo tipo de página. La plantilla define de forma aproximada la estructura de la página (elementos de navegación, paneles, etc.), que se ajusta aún más con su diseño (CSS, gráficos).
* Utilice el sistema de párrafos (parsys/iparsys) en las nuevas páginas.
* Defina el derecho de acceso al modo Diseño de los sistemas de párrafos, de modo que solo las personas autorizadas (normalmente el administrador) puedan cambiarlos.
* Defina los componentes permitidos en el sistema de párrafos determinado para que los editores puedan colocar los componentes necesarios en la página. En nuestro caso, podría ser un componente de lista, que puede recorrer un subárbol de páginas y extraer la información según las reglas predefinidas.
* Los editores agregan y configuran los componentes permitidos, en las páginas de las que son responsables, para entregar la funcionalidad solicitada (información) a la empresa.

Esto ilustra cómo este enfoque permite a los usuarios y administradores contribuyentes del sitio web responder rápidamente a las necesidades comerciales, sin requerir la participación de equipos de desarrollo. Los métodos alternativos, como la creación de una nueva plantilla, suelen ser un ejercicio costoso que requiere un proceso de gestión del cambio y la participación del equipo de desarrollo. Esto hace que todo el proceso sea mucho más largo y costoso.

Por consiguiente, los desarrolladores de sistemas basados en AEM deben utilizar:

* plantillas y control de acceso al diseño del sistema de párrafos para la uniformidad y la protección de la marca
* sistema de párrafos, incluidas sus opciones de configuración para la flexibilidad.

Las siguientes reglas generales para desarrolladores tienen sentido en la mayoría de los proyectos habituales:

* Mantenga el número de plantillas bajo, tan bajo como el número de estructuras de páginas fundamentalmente diferentes en los sitios Web.
* Proporcione la flexibilidad y las capacidades de configuración necesarias a sus componentes personalizados.
* Maximice el uso de la potencia y flexibilidad de AEM sistema de párrafos: los componentes parsys e iparsys.

### Personalización de componentes y otros elementos {#customizing-components-and-other-elements}

Al crear sus propios componentes o personalizar un componente existente, suele ser más fácil (y seguro) reutilizar las definiciones existentes. Los mismos principios también se aplican a otros elementos dentro de AEM, por ejemplo el controlador de errores.

Esto se puede hacer copiando y superponiendo la definición existente. En otras palabras, copiando la definición de `/libs` a `/apps/<your-project>`. Esta nueva definición, en `/apps`, puede actualizarse según sus necesidades.

>[!NOTE]
>
>Consulte [Uso de Overlays](/help/sites-developing/overlays.md) para obtener más detalles.

Por ejemplo:

* [Personalización de un componente](/help/sites-developing/components.md)

   Esto implicaba superponer una definición de componente:

   * Cree una nueva carpeta de componentes en `/apps/<website-name>/components/<MyComponent>` copiando un componente existente:

      * Por ejemplo, para personalizar la copia del componente Texto:

         * de `/libs/foundation/components/text`
         * hasta `/apps/myProject/components/text`

* [Personalización de páginas mostradas por el controlador de errores](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   Este caso implica la superposición de un servlet:

   * En el repositorio, copie las secuencias de comandos predeterminadas:

      * de `/libs/sling/servlet/errorhandler/`
      * hasta `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**no debe** cambiar nada en la ruta `/libs`.
>
>Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y bien puede sobrescribirse al aplicar una revisión o un paquete de funciones).
>
>Para configuración y otros cambios:
>
>1. copie el elemento en `/libs` a `/apps`
>1. realizar cambios dentro de `/apps`


## Cuándo usar Consultas JCR y cuándo no usarlas {#when-to-use-jcr-queries-and-when-not-to-use-them}

Las Consultas JCR son una poderosa herramienta cuando se utilizan correctamente. Son adecuadas para:

* consultas reales del usuario final, como búsquedas de texto completo en contenido.
* ocasiones en las que el contenido estructurado debe encontrarse en todo el repositorio.

   En estos casos, asegúrese de que las consultas solo se ejecuten cuando sea absolutamente necesario, por ejemplo, en la activación de componentes o la invalidación de caché (a diferencia de, por ejemplo, los pasos de Flujos de trabajo, los controladores de Evento que déclencheur en modificaciones de contenido, Filtros, etc.).

Las Consultas JCR nunca deben utilizarse para solicitudes de procesamiento puras. Por ejemplo, las Consultas JCR no son apropiadas para

* procesamiento de navegación
* creación de una descripción general de los &quot;10 artículos de noticias más recientes&quot;
* visualización de recuentos de elementos de contenido

Para procesar contenido, utilice el acceso de navegación al árbol de contenido en lugar de realizar una Consulta JCR.

>[!NOTE]
>
>Si utiliza el [Generador de Consultas](/help/sites-developing/querybuilder-api.md), utilice Consultas JCR, ya que el Generador de Consultas genera Consultas JCR debajo del capó.


## Consideraciones de seguridad {#security-considerations}

>[!NOTE]
>
>También vale la pena hacer referencia a la [lista de comprobación de seguridad](/help/sites-administering/security-checklist.md).

### Sesiones JCR (Repositorio) {#jcr-repository-sessions}

Debe utilizar la sesión de usuario, no la sesión administrativa. Esto significa que debe utilizar:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect contra scripts entre sitios (XSS) {#protect-against-cross-site-scripting-xss}

La secuencia de comandos entre sitios (XSS) permite a los atacantes insertar código en páginas web vistas por otros usuarios. Esta vulnerabilidad de seguridad puede ser aprovechada por usuarios web malintencionados para evitar controles de acceso.

AEM aplica el principio de filtrar todo el contenido proporcionado por el usuario durante la salida. La prevención de XSS recibe la máxima prioridad durante el desarrollo y las pruebas.

Además, un firewall de aplicaciones web, como [mod_security para Apache](https://modsecurity.org), puede proporcionar un control central y confiable sobre la seguridad del entorno de implementación y protegerse contra ataques de scripts entre sitios no detectados anteriormente.

>[!CAUTION]
>
>El código de ejemplo proporcionado con AEM puede no protegerse de dichos ataques y generalmente depende del filtrado de solicitudes por un servidor de seguridad de aplicaciones web.

La hoja de trucos de la API XSS contiene la información que necesita conocer para utilizar la API XSS y hacer que una aplicación AEM sea más segura. Puede descargarlo aquí:

La hoja de trucos XSSAPI.

[Obtener archivo](assets/xss_cheat_sheet_2016.pdf)

### Seguridad de la comunicación para información confidencial {#securing-communication-for-confidential-information}

En cuanto a cualquier aplicación de Internet, asegúrese de que al transportar información confidencial

* el tráfico está asegurado mediante SSL
* El POST HTTP se utiliza si corresponde

Esto se aplica a la información que es confidencial para el sistema (como la configuración o el acceso administrativo) así como a la información confidencial para sus usuarios (como sus datos personales)

## Tareas de desarrollo distintas {#distinct-development-tasks}

### Personalización de páginas de error {#customizing-error-pages}

Las páginas de error se pueden personalizar para AEM. Esto es aconsejable para que la instancia no muestre los seguimientos de sling en los errores internos del servidor.

Consulte [Personalización de páginas de error que muestra el controlador de errores](/help/sites-developing/customizing-errorhandler-pages.md) para obtener más información.

### Abrir archivos en el proceso de Java {#open-files-in-the-java-process}

Dado que AEM acceder a un gran número de archivos, se recomienda configurar explícitamente para AEM el número de [archivos abiertos para un proceso de Java](/help/sites-deploying/configuring.md#open-files-in-the-java-process).

Para minimizar este problema, el desarrollo debe garantizar que cualquier archivo abierto se cierre correctamente tan pronto como sea posible (de manera significativa).
