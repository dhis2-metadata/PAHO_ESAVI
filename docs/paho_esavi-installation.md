# Guía de instalación

  

## Descripción general

  

Todos nuestros paquetes lanzados contienen un paquete de etiquetas con información muy útil que debe verificarse antes de la instalación.

  

"paquete": {

"DHIS2Build": "58094d2",

"Versión DHIS2": "2.33.9",

"código": "ÁREA DE SALUD_INTERVENCIÓN",

"última actualización": "20210826T122409",

"locale": "es",

"nombre": "SALUD-AREA_INTERVENTION_TRK_1.X.X_DHIS2.33.9-en",

"tipo": "RASTREADOR",

"versión": "X.X.X"

},

  

Asegúrese de que el paquete DHIS2Version corresponda a la versión actual de DHIS2 que se ejecuta en su servidor/instancia. Además, asegúrese de que el idioma especificado en la configuración regional coincida con el de su país. Todos los paquetes vienen con traducciones, pero hacemos lanzamientos oficiales de paquetes totalmente traducidos bajo demanda.

Algunos ejemplos de pares de área de salud e intervención: TB-DRS, COVID19-CS (Vigilancia de Casos), EPI-VE (Programa Ampliado de Inmunizaciones - Eventos Vitales), MAL-FOCI (Focos de Malaria).

Instalación

  

## La instalación del módulo consta de varios pasos:

  

Preparación del archivo de metadatos con metadatos DHIS2.

Importación del archivo de metadatos a DHIS2.

Configuración de los metadatos importados.

Adaptación del programa después de ser importado

  

Se recomienda leer primero cada sección antes de iniciar el proceso de instalación y configuración en DHIS2. Se han identificado las secciones que no son aplicables, dependiendo de si está importando a una nueva instancia de DHIS2 oa una instancia de DHIS2 con metadatos ya presentes. El procedimiento descrito en este documento debe probarse en un entorno de prueba/escenario antes de repetirse o transferirse a una instancia de producción de DHIS2.

  

## Requisitos  
  

Para instalar el módulo, se requiere una cuenta de usuario administrador en DHIS2. El procedimiento descrito en este documento debe probarse en un entorno de prueba/escenario antes de ejecutarse en una instancia de producción de DHIS2.

Se debe tener mucho cuidado para garantizar que el servidor mismo y la aplicación DHIS2 estén bien protegidos, para restringir el acceso a los datos que se recopilan. Los detalles sobre cómo asegurar un sistema DHIS2 están fuera del alcance de este documento y nos referimos a la documentación de DHIS2.

Los paquetes de metadatos son autónomos, lo que significa que se pueden instalar solos. Sin embargo, vale la pena notar que algunos paquetes pueden contener algunos metadatos de otros paquetes, simplemente porque están relacionados. Por ejemplo, el tablero del paquete de seguimiento puede incluir una tabla comparativa que hace posible comparar los datos provenientes de un paquete agregado y los datos del paquete de seguimiento.

## Preparación del archivo de metadatos

NOTA: Si está instalando el paquete en una nueva instancia de DHIS2, puede omitir la sección "Preparación del archivo de metadatos" y pasar inmediatamente a la sección "Importación de un archivo de metadatos a DHIS2".

Si bien no siempre es necesario, a menudo puede resultar ventajoso realizar ciertas modificaciones en el archivo de metadatos antes de importarlo a DHIS2.

### Dimensión de datos predeterminada

En las primeras versiones de DHIS2, el UID de la dimensión de datos predeterminada se generaba automáticamente. Por lo tanto, aunque todas las instancias de DHIS2 tienen una opción de categoría predeterminada, una categoría de elemento de datos, una combinación de categoría y una combinación de opción de categoría, los UID de estos valores predeterminados pueden ser diferentes. Las versiones posteriores de DHIS2 tienen UID codificados para la dimensión predeterminada y estos UID se utilizan en los paquetes de configuración.



Para evitar conflictos al importar los metadatos, se recomienda buscar y reemplazar todo el archivo .json para todas las ocurrencias de estos objetos predeterminados, reemplazando los UID del archivo .json con los UID de la base de datos en la que se importará el archivo. La Tabla 1 muestra los UID que deben reemplazarse, así como los extremos de la API para identificar los UID existentes.

  | Objecto                     | UID         | API                                                     |
|-----------------------------|-------------|---------------------------------------------------------|
| Category                    | GLevLNI9wkl | ../api/categories.json?filter=name:eq:default           |
| Category option             | xYerKDKCefk | ../api/categoryOptions.json?filter=name:eq:default      |
| Category combination        | bjDvmb4bfuf | ../api/categoryCombos.json?filter=name:eq:default       |
| Category option combination | HllvX50cXC0 | ../api/categoryOptionCombos.json?filter=name:eq:default |
  

Por ejemplo, si importa un paquete de configuración a https://play.dhis2.org/demo, el UID de la combinación de opciones de categoría predeterminada podría identificarse a través de https://play.dhis2.org/demo/api/categoryOptionCombos.json?filter=name:eq:default as bRowv6yZOF2.

  

Luego, puede buscar y reemplazar todas las apariciones de HllvX50cXC0 con bRowv6yZOF2 en el archivo .json, ya que esa es la ID predeterminada en el sistema al que está importando. Tenga en cuenta que esta operación de búsqueda y reemplazo debe realizarse con un editor de texto sin formato, no con un procesador de textos como Microsoft Word.

  

###  Tipos de indicadores

  

El tipo de indicador es otro tipo de objeto que puede crear un conflicto de importación porque ciertos nombres se usan en diferentes bases de datos DHIS2 (por ejemplo, "Porcentaje"). Dado que los tipos de indicadores se definen simplemente por su factor y si son o no números simples sin denominador, no son ambiguos y se pueden reemplazar mediante una búsqueda y reemplazo de los UID. Esto evita posibles conflictos de importación y evita la creación de tipos de indicadores duplicados. La Tabla 2 muestra los UID que podrían reemplazarse, así como los extremos de la API para identificar los UID existentes

  

    Objeto Percentage / Porcentaje
    
    UID hmSnCXmLYwt
    
    API ../api/indicatorTypes.json?filter=número:eq:false&filter=factor:eq:100

  
  

### Tipo de entidad rastreada

  

Al igual que los tipos de indicadores, es posible que ya tenga tipos de entidades rastreadas en su base de datos DHIS2. Las referencias al tipo de entidad rastreada deben cambiarse para reflejar lo que hay en su sistema para que no cree duplicados. La Tabla 3 muestra los UID que podrían reemplazarse, así como los extremos de la API para identificar los UID existentes

  

    Objeto - Persona
    
    UID - MCPQUTHX1Ze
    
    API - ../api/trackedEntityTypes.json?filter=nombre:eq:Persona

  
  

## Metadatos genéricos

El paquete puede contener algunos metadatos etiquetados como "genéricos", es decir, con el prefijo "GEN -". Los metadatos genéricos se reutilizan en diferentes paquetes y normalmente solo están presentes en los elementos de datos. Es probable que ya tenga elementos similares en su base de datos, por lo que vale la pena verificar antes de instalar el paquete. Un ejemplo podrían ser los DE genéricos utilizados para almacenar datos de población: GEN - Población
  
## Importación de metadatos

El archivo de metadatos .json se importa a través de la aplicación Importar/Exportar de DHIS2. Es recomendable utilizar la función de "ejecución en seco" para identificar problemas antes de intentar realizar una importación real de los metadatos. Si la "ejecución en seco" informa de algún problema o conflicto, consulte la sección de conflictos de importación a continuación.

Si la importación de "simulacro"/"validación" funciona sin errores, intente importar los metadatos. Si la importación se realiza correctamente sin errores, puede proceder a configurar el módulo. En algunos casos, los conflictos o problemas de importación no se muestran durante la "ejecución de prueba", pero aparecen cuando se intenta la importación real. En este caso, el resumen de importación enumerará los errores que deben resolverse.

### Manejo de conflictos de importación

NOTA: Si está importando a una nueva instancia de DHIS2, no tendrá que preocuparse por los conflictos de importación, ya que no hay nada en la base de datos a la que esté importando con lo que pueda entrar en conflicto. Siga las instrucciones para importar los metadatos y luego vaya a la sección "Configuración adicional".

Hay varios conflictos diferentes que pueden ocurrir, aunque el más común es que hay objetos de metadatos en el paquete de configuración con un nombre, nombre abreviado y/o código que ya existe en la base de datos de destino. Hay un par de soluciones alternativas a estos problemas, con diferentes ventajas y desventajas. Cuál es más adecuado dependerá, por ejemplo, del tipo de objeto para el que se produzca un conflicto.

 
#### Alternativa 1

  

Cambie el nombre del objeto existente en su base de datos DHIS2 para el que existe un conflicto. La ventaja de este enfoque es que no es necesario modificar el archivo .json, ya que los cambios se realizan a través de la interfaz de usuario de DHIS2. Es probable que esto sea menos propenso a errores. También significa que el paquete de configuración se deja como está, lo que puede ser una ventaja, por ejemplo, cuando se utilizará material de capacitación y documentación basada en el paquete de configuración.

  

#### Alternativa 2

  

Cambie el nombre del objeto para el que existe un conflicto en el archivo .json. La ventaja de este enfoque es que los metadatos DHIS2 existentes se dejan como están. Esto puede ser un factor cuando existe material de formación o documentación como SOPs de diccionarios de datos vinculados al objeto en cuestión, y no implica ningún riesgo de confundir a los usuarios modificando los metadatos con los que están familiarizados.

  

Tenga en cuenta que tanto para la alternativa 1 como para la 2, la modificación puede ser tan simple como agregar un pequeño pre/post-fijo al nombre, para minimizar el riesgo de confusión.

  

#### Alternativa 3

  

Un tercer enfoque, más complicado, es modificar el archivo .json para reutilizar los metadatos existentes. Por ejemplo, en los casos en que ya existe un conjunto de opciones para un determinado concepto (por ejemplo, "sexo"), ese conjunto de opciones podría eliminarse del archivo .json y todas las referencias a su UID se reemplazarían con el conjunto de opciones correspondiente que ya está en la base de datos. La gran ventaja de esto (que no se limita a los casos en los que hay un conflicto de importación directo) es evitar la creación de duplicados.

  

## Órden de resultados

  

Para optimizar los resultados de búsqueda en sets de opciones, en particular los sets de opciones que contengan diccionarios de terminología, se recomienda ordenar las opciones por orden alfabético y por la longitud del string. Esto se puede lograr ejecutando el SQL que se encuentra a continuación:  

    with ordered as (
    
    select
    
    uid,
    
    name,
    
    code,
    
    row_number() OVER (ORDER BY length(name),name) AS sort_order
    
    from optionvalue
    
    where
    
    optionsetid =
    
    (select optionsetid from optionset where code = 'CODE_OF_OPTIONSET')
    
    )
    
    update optionvalue ov
    
    set sort_order = ord.sort_order
    
    from ordered ord
    
    where
    
    ov.uid = ord.uid and
    
    ov.optionsetid =
    
    (select optionsetid from optionset where code = 'CODE_OF_OPTIONSET');

