---
title: Modelado de datos - Modelo de David Nuescheler
seo-title: Data Modeling - David Nuescheler's Model
description: Recomendaciones de modelado de contenido de David Nuescheler
seo-description: David Nuescheler's content modelling recommendations
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 0%

---

# Modelado de datos - Modelo de David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Origen {#source}

Los siguientes detalles son ideas y comentarios expresados por David Nuescheler.

David fue cofundador y CTO of Day Software AG, un proveedor líder de software global de gestión de contenido e infraestructura de contenido, que fue adquirido por Adobe en 2010. Ahora es socio y vicepresidente de Tecnología empresarial en Adobe y también lidera el desarrollo de JSR-170, la interfaz de programación de aplicaciones (API) del Repositorio de Contenido Java (JCR), el estándar tecnológico para la administración de contenido.

También se pueden ver más actualizaciones en [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## Introducción a David {#introduction-from-david}

En varias discusiones encontré que los desarrolladores están algo incómodos con las características y funcionalidades presentadas por JCR cuando se trata de modelado de contenido. Aún no hay guía y muy poca experiencia sobre cómo modelar contenido en un repositorio y por qué un modelo de contenido es mejor que el otro.

Mientras que en el mundo relacional la industria del software tiene mucha experiencia en cómo modelar datos, todavía estamos en las primeras etapas para el espacio del repositorio de contenido.

Me gustaría comenzar a llenar este vacío expresando mis opiniones personales sobre cómo se debería modelar el contenido, con la esperanza de que algún día esto pueda convertirse en algo más significativo para la comunidad de desarrolladores, que no es solamente &quot;mi opinión&quot; sino algo que es más generalmente aplicable. Consideren que esta es mi primera puñalada que evoluciona rápidamente.

>[!NOTE]
>
>Renuncia de responsabilidad: Estas directrices expresan mis opiniones personales, a veces polémicas. Espero con interés debatir estas directrices y perfeccionarlas.

## Siete reglas simples {#seven-simple-rules}

### Regla #1: Datos primero, estructura después. Tal vez. {#rule-data-first-structure-later-maybe}

#### Explicación {#explanation-1}

Recomiendo no preocuparme por una estructura de datos declarada en el sentido ERD. Inicialmente.

Aprenda a amar nt:unstructured (y amigos) en desarrollo.

Creo que Stefano lo resume bastante bien.

Mi conclusión: La estructura es costosa y en muchos casos es completamente innecesario declarar explícitamente la estructura al almacenamiento subyacente.

Existe un contrato implícito sobre la estructura que la aplicación utiliza de forma inherente. Digamos que almaceno la fecha de modificación de una publicación de blog en una propiedad lastModified . Mi aplicación sabrá automáticamente leer la fecha de modificación de esa misma propiedad de nuevo, realmente no hay necesidad de declarar eso explícitamente.

Las restricciones de datos adicionales, como las obligatorias o las restricciones de tipo y valor, solo deben aplicarse cuando sea necesario por motivos de integridad de los datos.

#### Ejemplo {#example-1}

El ejemplo anterior del uso de un `lastModified` La propiedad Date en, por ejemplo, el nodo &quot;blog post&quot;, no significa que sea necesario un nodo especial. Definitivamente usaría `nt:unstructured` para mis nodos de anuncios de blog al menos inicialmente. Ya que en mi aplicación de blogueo todo lo que voy a hacer es mostrar la fecha de lastModified de todas maneras (posiblemente &quot;ordenado por&quot;) apenas me importa si es una fecha en absoluto. Como implícitamente confío en mi aplicación de escritura de blog para poner una &quot;fecha&quot; ahí de todos modos, realmente no hay necesidad de declarar la presencia de un `lastModified` fecha en el formulario a de nodetype.

### Regla #2: Impulse la jerarquía de contenido, no permita que suceda. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Explicación {#explanation-2}

La jerarquía de contenido es un recurso muy valioso. Así que no dejen que suceda, diseñen. Si no tiene un nombre &quot;bueno&quot;, legible en lenguaje natural para un nodo, probablemente sea algo que debería reconsiderar. Los números arbitrarios casi nunca son un &quot;buen nombre&quot;.

Si bien puede ser extremadamente fácil poner rápidamente un modelo relacional existente en un modelo jerárquico, se debe pensar en ese proceso.

En mi experiencia, si uno piensa en el control de acceso y la contención, normalmente son buenos controladores para la jerarquía de contenido. Piense en ello como si fuera su sistema de archivos. Puede incluso usar archivos y carpetas para modelarlos en el disco local.

Personalmente prefiero las convenciones de jerarquía sobre el sistema de escritura de nodos en muchos casos inicialmente, e introducir la escritura más tarde.

>[!CAUTION]
>
>La forma en que se estructura un repositorio de contenido también puede afectar al rendimiento. Para obtener el mejor rendimiento, el número de nodos secundarios conectados a nodos individuales en un repositorio de contenido no debe superar en general los 1000.
>
>Consulte [¿Cuántos datos puede gestionar CRX?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) para obtener más información.

#### Ejemplo {#example-2}

Yo modelaría un simple sistema de blogueo como sigue. Tenga en cuenta que inicialmente ni siquiera me importan los respectivos tipos de nodos que uso en este momento.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Creo que una de las cosas que se hacen evidentes es que todos entendemos la estructura del contenido basado en el ejemplo sin más explicaciones.

Lo que puede ser inesperado inicialmente es por qué no almacenaría los &quot;comentarios&quot; con el &quot;post&quot;, que se debe al control de acceso que me gustaría que se aplicara de una manera razonablemente jerárquica.

Con el modelo de contenido anterior puedo permitir fácilmente que el usuario &quot;anónimo&quot; &quot;cree&quot; comentarios, pero mantener al usuario anónimo en base a solo lectura para el resto del espacio de trabajo.

### Regla #3: Los espacios de trabajo son para clone(), merge() y update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Explicación {#explanation-3}

Si no utiliza `clone()`, `merge()` o `update()` en su aplicación un solo espacio de trabajo es probablemente el camino a seguir.

&quot;Nodos correspondientes&quot; es un concepto definido en la especificación JCR. Básicamente, se reduce a nodos que representan el mismo contenido, en diferentes llamados espacios de trabajo.

JCR introduce el concepto muy abstracto de Workspaces que deja a muchos desarrolladores sin claro qué hacer con ellos. Me gustaría proponer que su uso de espacios de trabajo se ponga a prueba a continuación.

Si tiene una superposición considerable de nodos &quot;correspondientes&quot; (esencialmente, los nodos con el mismo UUID) en varios espacios de trabajo, probablemente utilice los espacios de trabajo correctamente.

Si no hay superposición de nodos con el mismo UUID, probablemente esté abusando de los espacios de trabajo.

Los espacios de trabajo no deben utilizarse para el control de acceso. La visibilidad del contenido para un grupo determinado de usuarios no es un buen argumento para separar las cosas en diferentes espacios de trabajo. JCR incluye &quot;Control de acceso&quot; en el repositorio de contenido para proporcionarlo.

Los espacios de trabajo son el límite para las referencias y la consulta.

#### Ejemplo {#example-3}

Utilice espacios de trabajo para cosas como:

* v1.2 de su proyecto vs. v1.3 de su proyecto
* un estado de contenido &quot;desarrollo&quot;, &quot;control de calidad&quot; y &quot;publicado&quot;

No utilice espacios de trabajo para cosas como:

* directorios raíz del usuario
* contenido distinto para diferentes audiencias de destino como pública, privada, local, ...
* bandejas de entrada de correo para distintos usuarios

### Regla n.º 4: Cuidado con los hermanos del mismo nombre. {#rule-beware-of-same-name-siblings}

#### Explicación {#explanation-4}

Aunque los elementos del mismo nombre (SNS) se han introducido en la especificación para permitir la compatibilidad con estructuras de datos diseñadas para y expresadas a través de XML y, por lo tanto, son extremadamente valiosos para JCR, SNS viene con una sobrecarga y complejidad sustanciales para el repositorio.

Cualquier ruta al repositorio de contenido que contiene un SNS en uno de sus segmentos de ruta se vuelve mucho menos estable, si se elimina o reordena un SNS, tiene un impacto en las rutas del resto de SNS y sus hijos.

Para importar XML o interactuar con SNS XML existente puede ser necesario y útil, pero nunca he utilizado SNS y nunca lo haré en mis modelos de datos de &quot;campo verde&quot;.

#### Ejemplo {#example-4}

Uso de

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

en lugar de

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### Regla #5: Referencias consideradas nocivas. {#rule-references-considered-harmful}

#### Explicación {#explanation-5}

Las referencias implican integridad referencial. Considero importante entender que las referencias no solo añaden un coste adicional para el repositorio que administra la integridad referencial, sino que también son costosas desde la perspectiva de la flexibilidad del contenido.

Personalmente me aseguro de usar solo referencias cuando realmente no puedo lidiar con una referencia colgante y de otro modo usar una ruta, un nombre o un UUID de cadena para hacer referencia a otro nodo.

#### Ejemplo {#example-5}

Supongamos que permito las &quot;referencias&quot; de un documento a otro documento b). Si modelo esta relación utilizando propiedades de referencia esto significa que los dos documentos están vinculados a nivel de repositorio. No puedo exportar/importar el documento a) individualmente, ya que el destino de la propiedad de referencia puede no existir. Otras operaciones como combinar, actualizar, restaurar o clonar también se ven afectadas.

Así que modelaría esas referencias como &quot;referencias débiles&quot; (en JCR v1.0 esto básicamente se reduce a propiedades de cadena que contienen el uuid del nodo de destino) o simplemente usaría una ruta. A veces la ruta es más significativa para empezar.

Creo que hay casos de uso en los que un sistema realmente no puede funcionar si una referencia está colgando, pero simplemente no puedo encontrar un buen ejemplo &quot;real&quot; pero simple de mi experiencia directa.

### Regla 6: Los archivos son archivos. {#rule-files-are-files}

#### Explicación {#explanation-6}

Si un modelo de contenido expone algo que incluso de forma remota *huele* como un archivo o una carpeta que intento usar (o ampliar desde) `nt:file`, `nt:folder` y `nt:resource`.

En mi experiencia, muchas aplicaciones genéricas permiten la interacción con nt:folder y nt:files implícitamente y saben cómo manejar y mostrar esos eventos si se enriquecen con información meta adicional. Por ejemplo, una interacción directa con implementaciones de file server como CIFS o WebDAV sentadas sobre JCR se vuelve implícita.

Creo que como buena regla general se podría usar lo siguiente: Si necesita almacenar el nombre de archivo y el tipo mime, entonces `nt:file`/ `nt:resource` es una muy buena coincidencia. Si puede tener varios &quot;archivos&quot;, una carpeta nt:folder es un buen lugar para almacenarlos.

Si necesita añadir metainformación para el recurso, digamos una propiedad &quot;author&quot; o &quot;description&quot;, amplíe `nt:resource` no la variable `nt:file`. Rara vez extiendo nt:file y extiendo con frecuencia `nt:resource`.

#### Ejemplo {#example-6}

Supongamos que a alguien le gustaría subir una imagen a una entrada de blog en:

```xml
/content/myblog/posts/iphone_shipping
```

y tal vez la reacción intestinal inicial sería añadir una propiedad binaria que contenga la imagen.

Aunque ciertamente hay buenos casos de uso para usar solamente una propiedad binaria (digamos que el nombre es irrelevante y el tipo mime es implícito) en este caso, recomendaría la siguiente estructura para mi ejemplo de blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Regla #7: Las identificaciones son malas. {#rule-ids-are-evil}

#### Explicación {#explanation-7}

En las bases de datos relacionales, los ID son un medio necesario para expresar relaciones, por lo que las personas tienden a usarlas también en modelos de contenido. Principalmente por razones equivocadas.

Si el modelo de contenido está lleno de propiedades que terminan en &quot;Id&quot;, probablemente no esté aprovechando la jerarquía correctamente.

Es cierto que algunos nodos necesitan una identificación estable durante todo su ciclo de vida. Mucho menos de lo que podría pensar. mix:referceable proporciona un mecanismo de este tipo integrado en el repositorio, por lo que no es necesario encontrar un medio adicional para identificar un nodo de forma estable.

Tenga también en cuenta que los elementos pueden ser identificados por ruta, y tanto como los &quot;enlaces simbólicos&quot; tienen mucho más sentido para la mayoría de los usuarios que los enlaces duros en un sistema de archivos unix, una ruta tiene sentido para que la mayoría de las aplicaciones hagan referencia a un nodo de destino.

Más importante aún, es **mix**:referenciable, lo que significa que se puede aplicar a un nodo en el momento en que realmente necesite hacer referencia a él.

Digamos que solo porque le gustaría poder hacer referencia potencialmente a un nodo de tipo &quot;Documento&quot; no significa que el tipo de nodo &quot;Documento&quot; tenga que extenderse de mix:referceable de forma estática, ya que se puede agregar dinámicamente a cualquier instancia del &quot;Documento&quot;.

#### Ejemplo {#example-7}

Uso de:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

en lugar de:

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```
