---
title: Referencia del proceso de flujo de trabajo
seo-title: Workflow Process Reference
description: Referencia del proceso de flujo de trabajo
seo-description: null
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
source-git-commit: cf3b739fd774bc860d9906b9884d22fd532fd5dd
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 1%

---

# Referencia del proceso de flujo de trabajo{#workflow-process-reference}

AEM proporciona varios pasos de proceso que se pueden utilizar para crear modelos de flujo de trabajo. También se pueden agregar pasos de proceso personalizados para tareas que no están cubiertas por los pasos integrados (consulte [Creación de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md)).

## Características del proceso {#process-characteristics}

Para cada paso del proceso, se describen las siguientes características.

### Clase Java o Ruta ECMA {#java-class-or-ecma-path}

Los pasos del proceso se definen mediante una clase Java o un ECMAScript.

* Para los procesos de clase Java, se proporciona el nombre de clase completo.
* Para los procesos ECMAScript se proporciona la ruta al script.

### Carga útil {#payload}

La carga útil es la entidad sobre la que actúa una instancia de flujo de trabajo. La carga útil se selecciona implícitamente mediante el contexto dentro del cual se inicia una instancia de flujo de trabajo.

Por ejemplo, si se aplica un flujo de trabajo a una página AEM *P* then *P* se pasa de un paso a otro a medida que avanza el flujo de trabajo, con cada paso actuando de forma opcional sobre *P* de alguna manera.

En el caso más común, la carga útil es un nodo JCR en el repositorio (por ejemplo, una página AEM o un recurso). Una carga útil de Nodo JCR se pasa como una cadena que es una ruta JCR o un identificador JCR (UUID). En algunos casos, la carga útil puede ser una propiedad JCR (pasada como una ruta JCR), una URL, un objeto binario o un objeto Java genérico. Los pasos de proceso individuales que sí actúan en la carga útil generalmente esperan una carga útil de un tipo determinado o actúan de forma diferente según el tipo de carga útil. Para cada proceso descrito a continuación, se describe el tipo de carga útil esperado, si existe.

### Argumentos {#arguments}

Algunos procesos de flujo de trabajo aceptan argumentos especificados por el administrador al configurar el paso de flujo de trabajo.

Los argumentos se introducen como una sola cadena en la variable **Argumentos de proceso** en la variable **Propiedades** del editor de flujo de trabajo. Para cada proceso descrito a continuación, el formato de la cadena del argumento se describe en una gramática EBNF simple. Por ejemplo, lo siguiente indica que la cadena de argumento consta de uno o más pares delimitados por comas, donde cada par consta de un nombre (que es una cadena) y un valor, separados por dos puntos:

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Tiempo de espera {#timeout}

Después de este periodo de tiempo de espera, el paso del flujo de trabajo ya no funciona. Algunos procesos de flujo de trabajo respetan el tiempo de espera, mientras que para otros no se aplica y se ignora.

### Permisos {#permissions}

La sesión se transfirió al `WorkflowProcess` está respaldado por el usuario de servicio para el servicio de proceso de flujo de trabajo, que tiene los siguientes permisos en la raíz del repositorio:

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Si ese conjunto de permisos no es suficiente para su `WorkflowProcess` , debe utilizar una sesión con los permisos necesarios.

La manera recomendada de hacerlo es utilizar un usuario de servicio creado con el subconjunto de permisos necesario, pero mínimo, de permisos necesarios.

>[!CAUTION]
>
>Si está actualizando desde una versión anterior a AEM 6.2, es posible que tenga que actualizar la implementación.
>
>En versiones anteriores, la sesión de administrador se pasaba al `WorkflowProcess` implementaciones y luego podrían tener acceso completo al repositorio sin tener que definir ACL específicas.
>
>Los permisos ahora se definen como se ha indicado anteriormente ([Permisos](#permissions)). Como es el método recomendado para actualizar la implementación.
>
>También hay una solución a corto plazo disponible con fines de compatibilidad con versiones anteriores cuando no es posible realizar cambios en el código:
>
>* Uso de la consola web ( `/system/console/configMgr` localice el **Servicio de configuración del flujo de trabajo de Adobe Granite**
>
>* habilite el **Modo heredado de proceso de flujo de trabajo**
>
>Esto volverá al antiguo comportamiento de proporcionar una sesión de administrador al `WorkflowProcess` y proporcionar acceso sin restricciones a todo el repositorio una vez más.

## Procesos de control de flujo de trabajo {#workflow-control-processes}

Los siguientes procesos no realizan ninguna acción sobre el contenido. Sirven para controlar el comportamiento del propio flujo de trabajo.

### AbsoluteTimeAutoAdvancer (Absolute Time Auto Advancer) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

La variable `AbsoluteTimeAutoAdvancer` (Absolute Time Auto Advancer) se comporta de forma idéntica a **AutoAdvancer**, excepto que se excede el tiempo de espera en una fecha y hora determinadas, en lugar de después de un periodo de tiempo determinado.

* **Clase Java**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Carga útil**: Ninguno.
* **Argumentos**: Ninguno.
* **Tiempo de espera**: El proceso agota el tiempo de espera al alcanzar la hora y la fecha establecidas.

### AutoAdvancer (Auto Advancer) {#autoadvancer-auto-advancer}

La variable `AutoAdvancer` process avanza automáticamente el flujo de trabajo al siguiente paso. Si hay más de un posible paso siguiente (por ejemplo, si hay una división OR), este proceso avanzará en el flujo de trabajo a lo largo del *ruta predeterminada*, si se ha especificado uno, de lo contrario el flujo de trabajo no se avanzado.

* **Clase Java**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Carga útil**: Ninguno.
* **Argumentos**: Ninguno.
* **Tiempo de espera**: El tiempo de espera del proceso se agota después de establecer el tiempo de espera.

### ProcessAssembler (Conjunto de procesos) {#processassembler-process-assembler}

La variable `ProcessAssembler` process ejecuta varios subprocesos secuencialmente en un solo paso del flujo de trabajo. Para usar la variable `ProcessAssembler`, cree un solo paso de este tipo en el flujo de trabajo y establezca sus argumentos para indicar los nombres y argumentos de los subprocesos que desea ejecutar.

* **Clase Java**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Carga útil**: Un recurso DAM, AEM página o ninguna carga útil (depende de los requisitos de los subprocesos).
* **Argumentos**:

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **Tiempo de espera**: Respetado.

Por ejemplo:

* Extraiga los metadatos del recurso.
* Cree tres miniaturas de los tres tamaños especificados.
* Cree una imagen de JPEG a partir del recurso, suponiendo que este no sea originalmente un GIF ni un PNG (en cuyo caso no se crea ningún JPEG).
* Establezca la fecha de la última modificación en el recurso.

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## Procesos básicos {#basic-processes}

Los siguientes procesos realizan tareas sencillas o sirven de ejemplos.

>[!CAUTION]
>
>You ***must*** no cambie nada en la variable `/libs` ruta.
>
>Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y se puede sobrescribir al aplicar una corrección o un paquete de funciones).

### delete {#delete}

Se elimina el elemento de la ruta dada.

* **Ruta de ECMAScript**: `/libs/workflow/scripts/delete.ecma`

* **Carga útil**: Ruta de JCR
* **Argumentos**: Ninguna
* **Tiempo de espera**: Ignorado

### noop {#noop}

Este es el proceso nulo. No realiza ninguna operación, pero registra un mensaje de depuración.

* **Ruta de ECMAScript**: `/libs/workflow/scripts/noop.ecma`

* **Carga útil**: Ninguna
* **Argumentos**: Ninguna
* **Tiempo de espera**: Ignorado

### rule-false {#rule-false}

Este es un proceso nulo que devuelve `false` en el `check()` método.

* **Ruta de ECMAScript**: `/libs/workflow/scripts/rule-false.ecma`

* **Carga útil**: Ninguna
* **Argumentos**: Ninguna
* **Tiempo de espera**: Ignorado

### ejemplo {#sample}

Este es un proceso ECMAScript de muestra.

* **Ruta de ECMAScript**: `/libs/workflow/scripts/sample.ecma`

* **Carga útil**: Ninguna
* **Argumentos**: Ninguna
* **Tiempo de espera**: Ignorado

### LockProcess {#lockprocess}

Bloquea la carga útil del flujo de trabajo.

* **Clase Java:** `com.day.cq.workflow.impl.process.LockProcess`

* **Carga útil:** JCR_PATH y JCR_UUID
* **Argumentos:** Ninguna
* **Tiempo de espera:** Ignorado

El paso no tiene ningún efecto en las siguientes circunstancias:

* La carga útil ya está bloqueada
* El nodo de carga útil no contiene un nodo secundario jcr:content

### UnlockProcess {#unlockprocess}

Desbloquea la carga útil del flujo de trabajo.

* **Clase Java:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Carga útil:** JCR_PATH y JCR_UUID
* **Argumentos:** Ninguna
* **Tiempo de espera:** Ignorado

El paso no tiene ningún efecto en las siguientes circunstancias:

* La carga útil ya está desbloqueada
* El nodo de carga útil no contiene un nodo secundario jcr:content

## Procesos de versiones {#versioning-processes}

El siguiente proceso realiza una tarea relacionada con la versión.

### CreateVersionProcess {#createversionprocess}

Crea una nueva versión de la carga útil del flujo de trabajo (AEM página o recurso DAM).

* **Clase Java**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Carga útil**: Una ruta JCR o UUID que hace referencia a una página o a un recurso DAM
* **Argumentos**: Ninguna
* **Tiempo de espera**: Respetado
