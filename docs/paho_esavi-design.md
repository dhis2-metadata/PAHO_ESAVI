Paquete de vigilancia de ESAVI-Centinela - OPS - Documento de diseño del sistema

  

# Introducción

  
  

“Uno de los componentes esenciales del sistema de vacunación segura es la vigilancia de los eventos supuestamente atribuibles a la vacunación o inmunización (ESAVI). A través de esta vigilancia, se busca detectar de manera temprana cualquier evento adverso que ocurra luego de la vacunación, con el propósito de controlar y clasificar los riesgos relacionados con la vacuna, el proceso de fabricación, el transporte, el almacenamiento, la administración, así como con toda situación inherente a la persona vacunada, o para descartar la relación de dicho evento con la vacuna.” ([https://iris.paho.org/handle/10665.2/55384](https://iris.paho.org/handle/10665.2/55384))

  

OPS ha identificado la necesidad de varios países de tener acceso a sistemas de información que puedan utilizarse como ayuda en el proceso de registrar, notificar, investigar y clasificar ESAVIs, así como estandarizar los datos que serán enviados a su base de datos regional.  
  
Como parte de la respuesta a esta necesidad, se ha creado un paquete de metadatos en DHIS2 para esos fines. Los países pueden instalarlo en una instancia de DHIS2 propia, o utilizar la configuración como modelo para sus propios sistemas. En paralelo, OPS cuenta también con una instancia regional de DHIS2 para hospitales centinela, donde esta configuración y metadatos pueden observarse en funcionamiento.

  

# Resúmen del diseño del sistema

## Caso de uso

  

El programa Centinela es un programa de tracker para DHIS2 que registra datos de eventos de Efectos adversos supuestamente atribuibles a la vacunación e inmunización (ESAVI) y efectos adversos de interés especial (EVADIE). Ha sido configurado basado en el [Manual de vigilancia de eventos supuestamente atribuibles a la vacunación o inmunización en la Región de las Américas](https://iris.paho.org/handle/10665.2/55384)

de la OPSm, y en el [“Manual global de vigilancia de efectos adversos pos-vacunales](https://apps.who.int/iris/handle/10665/206144?locale-attribute=es&)” de la OMS.

  

El programa cuenta con la posibilidad de incluir los catálogos de CIE, MEDDRA y WHODrug y está mapeado a los requerimientos para transmisión de datos a Vigibase, la base de datos mundial de farmacovigilancia.

  

## Estructura del programa

### Resúmen del contenido

  

El paquete de centinela cuenta con un programa de datos individuales longitudinales (tracker) y con una batería de indicadores y visualizaciones básicas.  
  
El programa de tracker está dividido en cuatro etapas no repetibles que utilizan formularios personalizados. Para información general acerca de como utilizar DHIS2 Tracker, ver la [documentación] ([https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/tracking-individual-level-data/tracker-capture.html](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/tracking-individual-level-data/tracker-capture.html)).

  

### Diagrama del programa

  

![](https://lh4.googleusercontent.com/50IuMUIjuBpq6moIZ9EBU7A1t5zPXSTVyi0kYlbmzfdydi6IQ-iSZFfe25NaTbBIycDFV6dk00SR3yUsXeYoTZKz89c4hZq4k6PmOeh2sFsoBUxmycWtp4hXs4hIHkxtQMDpTCgIKkYZWliWadNsJ6zrozslOMcicpsjRLF0-LB6zt7Oy4yvOWRbJBWt)

### Explicación de la estructura

La idea es que este programa pueda ser utilizado por aquellos que reportan solo ESAVIs, o por aquellos países que reportan ESAVIs y EVADIEs, siendo la etapa de clasificación donde se determina que tipo de evento esta siendo registrado. En el caso de los primeros, se ocultaría la etapa “EVADIE” y las reglas de programa correspondientes.

  

### Etapas

  

El programa Centinela está dividido en cinco etapas.

  
  

#### Etapa de clasificación inicial

  

En esta etapa se determina si el evento es un ESAVI o EVADIE basado en una serie de preguntas. Dependiendo de la clasificación inicial se habilitarán las etapas correspondientes.

  

#### Etapa EVADIE

  

Solamente estaría disponible cuando el evento corresponda a un EVADIE.

  

#### Etapa Notificación ESAVI

  

La etapa de notificación ESAVI solo está disponible cuando el evento corresponde a un ESAVI, y es donde se registran los datos generales del ESAVI y una clasificación preliminar.

  

#### Etapa Investigación ESAVI

  

La etapa de investigación ESAVI solamente cuando es especificado que el evento requiere una investigación.

  

#### Etapa Clasificación final

  

Esta etapa normalmente es accesible solamente a nivel distrital o nacional (es decir, a un nivel superior), y es donde se confirman los resultados del ESAVI y la clasificación final

  

## Usuarios Potenciales

El programa está pensado para que los datos sean ingresados al nivel más bajo posible, pero dependiendo del flujo de trabajo, usuarios con distintos roles deberán poder acceder a las distintas etapas. Normalmente, las etapas de clasificación inicial y notificación serían accesibles por todos los usuarios que puedan reportar ESAVIs, y las demás etapas tendrían acceso restringido dependiendo las funciones que desempeñen en la tarea de reportar, investigar y clasificar ESAVIs.

  

Dependiendo de cómo se organice la implementación, hay distintas maneras de configurar el acceso usando los grupos de usuarios, roles, acceso a unidades organizativas, y acceso a las distintas etapas del programa. Antes de implementar, el país deberá aclarar el proceso de negocio para los ESAVI/EVADIE que deberá seguirse y quienes deben tener acceso a la información y a que nivel.

### Combinación de grupos de usuario, roles y acceso a unidad organizativa

  

  
Los grupos de usuario sirven para dar acceso a los distintos programas (por ejemplo, el programa de EVADIE). Y regular que nivel de acceso tienen los usuarios dentro de ese grupo al programa. El nivel de acceso está basado en datos y metadatos, y en poder ver o editar.

  

La combinación de grupo de usuarios, roles y acceso a unidad organizativa permitirá controlar la granularidad del acceso. Para más información acerca de la configuración de acceso compartido, ver la [documentación de DHIS2](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-236/configuring-the-system/users-roles-and-groups.html).  
  
![](https://lh5.googleusercontent.com/bbxvYoJ2PAYfDVvytG9NdgEnxATh-EeFXNyAtZRYNzzROXqrFvsFLXLSwY9_KFlHCTd7eRqzy813-PKLsJoj74K4HeYBmtE84c30ibnAw5xOViZAYelHLNJGWd2oEX4PidMENZeV3QyGDJubYxTpGOdWtJRtQgtwBUypSdFnqTDLmIFxyR5AEzsgG4Wc)  
  

  ### Grupos de usuarios básicos  
  
Para una implementación del módulo centinela donde los usuarios ingresan datos de EVADIE y ESAVI, recomendamos los siguientes grupos de usuarios básicos, con la posibilidad de incluir más granularidad a la operación (ver tabla siguiente):  
  
| User group                     | Descripción                                                                                                 | Acceso a unidad organizativa                                     | Datos                    | Metadatos    | Analytics    | Roles                                                                 |
|--------------------------------|-------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|--------------------------|--------------|--------------|-----------------------------------------------------------------------|
| Centinela: Entrada de datos    | Usuario final, persona que ingresa los datos en todas las etapas (ESAVI, EVADIE; Clasificación final, etc). | Unidad propia                                                    | Ver y editar (No borrar) | Ver          | Sin acceso   | Usuario de Entrada de datos - Tracker (Sin acceso a borrar una TEI)   |
| Supervisor de entrada de datos | Igual que usuario final, pero podrá borrar TEIs y enrollments en las unidades a las que tenga acceso        | Unidad propia /distrito/nacional dependiendo de la organización  | Ver y editar ( borrar)   | ver          | ver          | Usuario de Entrada de datos - Tracker Supervisor (de país/distrito) * |
| Análisis de datos              | Tendrá acceso a tableros, visualizaciones e indicadores                                                     | Unidad propia (Si es un usuario nacional, a nivel nacional, etc) | Ver                      | Ver          | Ver          | Usuario de Entrada de datos - Tracker                                 |
| Auditoria de datos nacional    | Podrá ver todos los datos y quién los ha ingresado pero no editarlos                                        | Unidades del país                                                | Ver                      | Ver          | Ver          | Supervisor (de país/distrito) *                                       |
| Administración de metadatos    | Podrá editar los formularios, tableros e indicadores, pero no ver datos                                     | Todas                                                            | Sin Acceso               | Ver y Editar | Ver y Editar | Configurador de metadatos                                             |
| Administrador de usuarios      | Podrá crear y asignar usuarios a distintos roles y unidades organizativas                                   | Unidades del país /Distrito/propias según corresponda            | NO                       | NO           | NO           | Creación y edición de usuarios                                        |
| Superusuario                   | Si                                                                                                          | Todas                                                            | Ver y Editar             | Ver y Editar | Ver y Editar | Todas                                                                 |
  
  

### Grupos de usuarios / roles con mayor granularidad

  

En el caso que distintas personas estén ingresando datos de ESAVI/EVADIE a distintos niveles, se podría dividir el acceso a las distintas secciones del programa basado en la posición de la persona y el nivel de decisión.  
  
  
| Grupo de Usuario (User group)   | Descripción                                                           | Acceso a unidad organizativa                                    | Acceso a Etapa                                        | Datos         | Metadatos  | Analytics  |
|---------------------------------|-----------------------------------------------------------------------|-----------------------------------------------------------------|-------------------------------------------------------|---------------|------------|------------|
| Centinela: ESAVI Notificación   | Usuario que ingresa los datos de notificación ESAVI al nivel más bajo | Unidad propia                                                   | Clasificación /  ESAVI (*Y EVADIE si fuese necesario) | Ver y editar  | Ver        | Sin acceso |
| Centinela: ESAVI Investigación  | Usuario que realiza la investigación ESAVI                            | Unidad propia /distrito/nacional dependiendo de la organización | Clasificación /  ESAVI / Investigación                | Ver y editar  | ver        | ver        |
| Centinela: ESAVI Nivel Superior | Usuario que realiza la Clasificación final del ESAVI                  | Nivel nacional /Distrital dependiendo de la organización        | Clasificación /  ESAVI / Investigación/Nivel Superior | Ver y editar  | Ver        | Ver        |

    
En caso de que el país quisiese incluso mayor granularidad de acceso, es posible agregar mas grupos y entre la combinación de roles, acceso a unidad organizativa y acceso a las distintas etapas y aplicaciones, poder lograr restringir el nivel de acceso deseado.

## Configuración del programa de tracker

El programa de Tracker CENTINELA incluído en este paquete debe considerarse un programa inicial que cumple con los requerimientos de OPS para la captura de datos de ESAVI. Este deberá adaptarse a la realidad nacional antes de comenzar a ser utilizado, en particular en el perfil de la persona. Las distintas etapas están configuradas con formularios personalizados que si van a cambiarse requieren conocimiento de CSS, javascript y HTML. Para ver una lista completa de todos los atributos y elementos de datos, referirse a la lista de metadatos.

  

### Placeholders

  

Algunos de los elementos de datos están asociados a un estándar terminológico. Distintos países optarán por distintos estándares, y por tanto, no los hemos incluído en este paquete. En vez de los catálogos estandarizados, hemos incluído un placeholder para que el país pueda incluir el estándar que sea adecuado a su contexto. Véase la guía de instalación para ver instrucciones de como configurar estos estándares.

####   
Lista de elementos que contienen un placeholder

  
Esta lista contiene actualmente el ejemplo del estándar de terminología que se está aplicando en la instancia regional.

  
| Nombre del elemento | Set de opciones actual en la instancia regional |
|---|---|
| ESAVII - Vaccine 1 name | CEN-Vacunas COVID (whodrug) |
| ESAVII - Vaccine 2 name | CEN-Vacunas COVID (whodrug) |
| ESAVII - Vaccine 3 name | CEN-Vacunas COVID (whodrug) |
| ESAVII - Vaccine 4 name | CEN-Vacunas COVID (whodrug) |
| ESAVI - C Diagnostico Final | ESAVI - Meddra |
| ESAVI - ComplicaAnomCongDx1 | ESAVI - Meddra |
| ESAVI - ComplicaAnomCongDx2 | ESAVI - Meddra |
| ESAVI - ComplicacionEmbDx1 | ESAVI - Meddra |
| ESAVI - ComplicacionEmbDx2 | ESAVI - Meddra |
| ESAVI - ComplicaFetalDx1 | ESAVI - Meddra |
| ESAVI - ComplicaFetalDx2 | ESAVI - Meddra |
| ESAVI - Drug Name 1 | CEN-medicamentos principio activo (whodrug) |
| ESAVI - Drug Name 2 | CEN-medicamentos principio activo (whodrug) |
| ESAVI - Drug Name 3 | CEN-medicamentos principio activo (whodrug) |
| ESAVI - Drug Name 4 | CEN-medicamentos principio activo (whodrug) |
| ESAVI - Drug Name 5 | CEN-medicamentos principio activo (whodrug) |
| ESAVI - Drug Name 6 | CEN-medicamentos principio activo (whodrug) |
| ESAVI - Drug Name 7 | CEN-medicamentos principio activo (whodrug) |
| ESAVI - Drug Name 8 | CEN-medicamentos principio activo (whodrug) |
| ESAVI - Drug Name 9 | CEN-medicamentos principio activo (whodrug) |
| ESAVI - Drug Presentation 1 | ESAVI - Forma Farm |
| ESAVI - Drug Presentation 2 | ESAVI - Forma Farm |
| ESAVI - Drug Presentation 3 | ESAVI - Forma Farm |
| ESAVI - Drug Presentation 4 | ESAVI - Forma Farm |
| ESAVI - Drug Presentation 5 | ESAVI - Forma Farm |
| ESAVI - Drug Presentation 6 | ESAVI - Forma Farm |
| ESAVI - Drug Presentation 7 | ESAVI - Forma Farm |
| ESAVI - Drug Presentation 8 | ESAVI - Forma Farm |
| ESAVI - Drug Presentation 9 | ESAVI - Forma Farm |
| ESAVI - Medical History 1 | ESAVI - Meddra |
| ESAVI - Medical History 2 | ESAVI - Meddra |
| ESAVI - Medical History 3 | ESAVI - Meddra |
| ESAVI - Medical History 4 | ESAVI - Meddra |
| ESAVI - Medical History 5 | ESAVI - Meddra |
| ESAVI - Medical History 6 | ESAVI - Meddra |
| ESAVI - Medical History 7 | ESAVI - Meddra |
| ESAVI - Medical History 8 | ESAVI - Meddra |
| ESAVI - Medical History 9 | ESAVI - Meddra |
| ESAVI - Nivel Subnacional | ESAVI - Distritos |
| ESAVI - OtroESAVI1 | ESAVI - Meddra |
| ESAVI - OtroESAVI2 | ESAVI - Meddra |
| ESAVI - OtroESAVI3 | ESAVI - Meddra |
| ESAVI - Vaccine Name 5 | CEN-Vacunas NO COVID (whodrug) |
| ESAVI - Vaccine Name 6 | CEN-Vacunas NO COVID (whodrug) |
| ESAVI - Vaccine Name 7 | CEN-Vacunas NO COVID (whodrug) |
| ESAVI - Vaccine Name 8 | CEN-Vacunas NO COVID (whodrug) |
| EVADIE - Medical History 1 | ESAVI - Meddra |
| EVADIE - Medical History 2 | ESAVI - Meddra |
| EVADIE - Medical History 3 | ESAVI - Meddra |
| EVADIE - Medical History 4 | ESAVI - Meddra |
| EVADIE - Medical History 5 | ESAVI - Meddra |
| EVADIE - Medical History 6 | ESAVI - Meddra |
| EVADIE - Medical History 7 | ESAVI - Meddra |
| EVADIE - Medical History 8 | ESAVI - Meddra |
| EVADIE - Medical History 9 | ESAVI - Meddra |

## Detalles de las etapas

  

Las etapas se han configurado con formularios custom en HTML, y un formulario con secciones en caso que se desee utilizar android. Las capturas de pantalla corresponden al formulario web personalizado.

### Registro inicial del caso

El registro inicial del caso son los datos de la persona deberán adecuarse a las necesidades del país cuando se hace una instalación nacional. Por ejemplo, cambiar el nombre de “municipio” a “cantones”, incluir reglas de validación al documento de identidad nacional, y modificar la lista de opciones a los lugares correspondientes.  
  
![](https://lh4.googleusercontent.com/XbupHpr9Lv1VV_2WaqZhFYfLWMmmEFNEzWitKjssG1r7Mjz-RNgkkteIvAcjTVxDtXuFHJDgNFUxmQ7gqrfItiDWzBgrKANYLRu_kn5dycTemUuhO5iYecQiv_AY2FHDgZ32XD6dUtaHhJHwHTnlNrwcjPGNmgQpmnwp6SiGyhhW3qCk5aG5Ct7Cvpmuhw)

  


| Etapa    | ID          | Nombre (ES)                           | Nombre (EN)                    | formName (ES)                         | formName (EN)                       | Tipo de valor | Option Set        |
|----------|-------------|---------------------------------------|--------------------------------|---------------------------------------|-------------------------------------|---------------|-------------------|
| Registro | NI0QRzJvQ0k | Fecha de nacimiento                   | Date of birth                  | Fecha de nacimiento                   | Date of Birth                       | DATE          |                   |
| Registro | eISp65Kw0Z7 | Municipio                             | District Level                 | Municipio                             | Municipality                        | TEXT          | ESAVI - Distritos |
| Registro | uV6lanmN4GO | Correo electrónico                    | Email                          | Correo electrónico                    | e-mail                              | EMAIL         |                   |
| Registro | sB1IHYu2xQT | Nombre                                | First Name                     | Nombre(s)                             | Name                                | TEXT          |                   |
| Registro | Xhdn49gUd52 | Dirección de residencia habitual      | Home Address                   | Dirección de residencia habitual      | Home Address                        | LONG_TEXT     |                   |
| Registro | fctSQp5nAYl | Número telefónico móvil               | Mobile phone number            | Número de teléfono móvil              | Mobile phone number                 | PHONE_NUMBER  |                   |
| Registro | Ewi7FUfcHAD | ID Nacional                           | National ID                    | No. de identidad                      | ID Number                           | TEXT          |                   |
| Registro | oindugucx72 | Sexo                                  | Sex                            | Sexo                                  | Sex                                 | TEXT          |                   |
| Registro | ENRjVGxVL6l | Apellidos                             | Surname                        | Apellidos del paciente                | The Patient's Surname (family name) | TEXT          |                   |
| Registro | KSr2yTdu1AI | Identificador ùnico del sistema (EPI) | Unique System Identifier (EPI) | Identificador ùnico del sistema (EPI) |                                     | TEXT          |                   |

### Etapa de clasificación inicial

En esta etapa se determina si el evento es un ESAVI o EVADIE basado en una serie de preguntas. Dependiendo de la clasificación inicial se habilitarán las etapas correspondientes.
 

![](https://lh5.googleusercontent.com/8w_-sTVP8_RkNGT4XL-bbTcleNw3XIk_rxXO9udN-WdmmgswyQ8QSXILI2nXV73UQcwGnSXb61v0KABdFNKNtojnlZAcm-X5qXU_269RqLc6mH2k6M7FlZdOZ_RjmWeXpGIxuiTI3Wrl32z8Uuhg1mVgN4hBXFQAlIOG7B1fgXfw6RN_pvFZK5LP3N0MPg)

  
### Etapa EVADIE
 

La etapa de EVADIE solamente estaría disponible cuando el evento que se registra no sea relacionado a una vacuna (ver reglas de programa).

  
![](https://lh6.googleusercontent.com/NrQ_8-oQnHBJKv42MMdI1pzObeFsGLXONg1pde9GofrJV76GhZYO0pf-SeaOtnDuuAMCTcpi8elzOjqoI6BKsRr5wB9HTptFMyIPBYKzQJzGYP3XnU4jTd6eNCBMJ8MYztb4o0maQ97ge-DGx34bQn2mo7GiUBOt_CkvJ0x7dx_3Oyh-qcl6VYylYxlllQ)

### Etapa Notificación ESAVI
  
La etapa de notificación ESAVI solo está disponible cuando el evento corresponde a un ESAVI, y es donde se registran los datos generales del ESAVI y una clasificación preliminar. En esta etapa se determina si el caso necesitará una investigación, y habilita la etapa correspondiente a aquellos usuarios que tengan acceso a la etapa de investigación

![](https://lh5.googleusercontent.com/C4MhW1R5c7JEkP_f_IwxAeuuh1OcdtlDv6eK3-Y2UdcOapEe4jIOkQpbmi_KQFiPUBr77eB6i-gUydkDXaKXbZLS_VOHp7WUsptx7t6X_09T6P5v3Go-NxiQUsVArSHkpLkiVuewLIDV66NnesY19P0UgbvckYKXZETOcZMVc1j_AuI7RHSZtP0IsaSiiQ)

.![](https://lh6.googleusercontent.com/mAdcNSmwHpLOsjcyXfNy_A79UUarKFKfDFs3H6YB8jgP0lLLPy6zgb4mQHDCPynW8rmbnbr9n1qY7ZkwRDY58lCz19mlHB9sE6IOfqbde28Kfd1mvhh6c--xQTd5e39JN5DOrnspuNmJw9AB3T8syDucWxDXX8TeqPae5-dJcPgx8yZlty02ru8bLTR5iw)
  

### Etapa Investigación ESAVI
La etapa de investigación ESAVI solamente cuando es especificado que el evento requiere una investigación en la etapa de ESAVI. En esta etapa se registra el trabajo de investigación realizado. Porque generalmente esto se registra a un nivel superior al lugar donde se notifica el ESAVI, esta etapa generalmente tiene acceso restringido con prioridad de acceso a personas que realizarán dicha investigación.  
  
La etapa está dividida en 8 secciones y una pregunta introductoria. Las distintas secciones (A-H) Se despliegan haciendo click en el título.

  

![](https://lh4.googleusercontent.com/tLIN6NLKDMWV3wPKMX_Ja9xR9mxlI0qkvVey_tT0njsmWkvPuNYEFtrcfIRqYRwnvbSZEIshO08PEwpl9aRK6ZNTreS00vxS4_W_37rFAnf7UKlrm4DQJ8TlAP3kEo76S9FpRFlCzWsFzMa8hkR7p5y2wbFozht6MIB86NTIbvnqGYuaK8xQ3TgHHRzyiA)

### Etapa Clasificación final

Esta etapa normalmente es accesible solamente a nivel distrital o nacional, y es donde se confirman los resultados del ESAVI y la clasificación final se registra.  

![](https://lh4.googleusercontent.com/CpErxMuC1xTeDvlCYCst_72cqpatx83l47dWbez9yMMXExKYYAJhOh18H5XkOOUssDwpbV5QdVUNOGzsMU5o6l_BtifQ8HdOMhckpH3WoJXF_wkmtbPP92bcKbsyEYIWK8R1OhnZFN2g27GQZsjCpxgK4LnzYz9_893nm2jn2SeK-JevJrKcCUBWnVw3HA)

## Analiticas

### Indicadores


DHIS2 calcula indicadores basados en los datos y genera visualizaciones preconfiguradas que son principalmente mostradas en los tableros de información. Usuarios, dependiendo de su acceso, pueden crear sus propias visualizaciones, mapas gráficas e indicadores.

Los indicadores en DHIS2 son cálculos basados en elementos de datos, y se dividen en indicadores simples (Numerador/denominador) e indicadores de programa (basados en un conteo por filtros). Elementos de datos que puedan accederse sin tener que incluir cálculos o filtros son agregados automáticamente. Por más información acerca de indicadores e indicadores de programa en DHIS2 ver la documentación.

  
Los indicadores incluidos dentro del paquete son los indicadores más básicos y no pueden considerarse como un set analítico extensivo.Una vez teniendo DHIS2 en una instancia propia podrían configurar nuevos indicadores o indicadores de programa. Para un análisis más avanzado, los datos pueden ser exportados y analizados en otra herramienta.


Para la exportación de datos, y en función del volumen y del análisis que se quiera establecer, se podría usar la propia API que provee dhis2. Mediante dicha API, se puede consultar tanto los datos “en tiempo real” como los datos “de análisis”. Las llamadas a la API dependerán del análisis que se quiera realizar. Además, hay que tener en cuenta que pueden definir políticas para la descarga de información (en función de lo actualizado que se quiera estar) y que estas llamadas se pueden realizar de manera programática mediante scripts en diferentes lenguajes de programación. El modelo de datos que es usado para descargar la información puede alterarse de manera programática para que la información a analizar sea lo más idónea para este proceso.

  
## Tableros

La primera versión de este paquete solamente cuenta con dos tablero resumidos muy simplificados para ESAVIs y EVADIEs. Cada país deberá configurar las visualizaciones e indicadores que desee conveniente. Las próximas versiones contarán con tableros más avanzados.

  

![](https://lh5.googleusercontent.com/z_EFpFScNLcNamKnRoHITEZCuy7L6TKhLAf69e_f9zI3Zh0DlPXuN3A5Wx4EldEBuFwCyJA2izpxyKLoNoTRugfzgi1FbAnm2DUC8oEvj8VfpPTXLgWtEoWdciCs09AgjXW2UNNis9WlFL3Ih4ruAfGRHgForg1QZGqL0TrCYT5D0Ei0NnGmYqQ2HGqLTw)

  
  

## Reglas de Validación / Reglas de Programa

El programa incluye reglas de Programa para mejorar el flujo de entrada de datos. Estas reglas de programa por lo general ocultan o muestran distintos elementos basados en los datos introducidos, o asignan valores a elementos de datos. A continuación se documentan algunas reglas de programa que podrán no resultar obvias.  
  
Además, al contar con formularios personalizados, existen reglas creadas en Javascript que están quemadas en el formulario.

### Clasificación entre EVADIE y ESAVI

En la etapa de clasificación hay dos reglas que determinan si el caso sería un ESAVI o un EVADIE

#### Para ocultar la etapa de EVADIE:

  

La regla gD1AnpykpOW oculta la etapa de EVADIE si la persona ha recibido alguna vacuna contra el Covid-19, o alguna vacuna que no sea para covid-19 y si se indica que se desea reportar el evento como un ESAVI

  

#### Para ocultar la etapa de ESAVI:

  

La regla ZQqgjqRwpAW Oculta la etapa de ESAVI si la persona no indica que ha recibido vacunas contra el COVID19 o alguna otra vacuna en los últimos dos meses

  

### Ocultar la etapa de Investigación

  

La regla gHILvWI48TV oculta la etapa de investigación si el elemento de datos donde se indica que necesita una investigación no está seleccionado

### Mensajería  
  

Tres reglas de mensajería se incluyen como ejemplo. Para poder utilizarlas deberá configurarse el sistema con un [gateway de sms](https://docs.dhis2.org/en/develop/using-the-api/dhis-core-version-238/sms.html) y/o un [servidor de correos electrónicos](https://docs.dhis2.org/en/develop/using-the-api/dhis-core-version-238/email.html), además de los destinatarios y mensajes correspondientes dentro de la pestaña de mensajería menú de mantenimiento del programa

  

-   La regla s9S655wmZ49 envía un e-mail cuando caso es menor de 18 años
    
-   La regla sZEsuziddGm envía un e-mail si se indica que la persona está embarazada en la etapa del ESAVI
    
-   La regla GpT5xMwHxeM envía un sms cuando se indica que el caso requiere una investigación
    

  

## Consideraciones
  

Ciertos procesos deberán tomarse en cuenta a la hora de instalar y modificar el paquete en una instancia propia.

### Catálogos estándar como set de opciones

Los catálogos como set de opciones no se encuentran disponibles en el archivo json del paquete de ESAVI, para obtenerlos deberán ponerse en contacto con OPS, y solicitarlos. Antes de hacerlo deberán obtener una licencia para aquellos estándares que así lo necesiten.
  

### Formularios personalizados

Los formularios no utilizan la interfaz estándar de DHIS2, sino que utilizan un frente de html y javascript para mejorar el flujo de trabajo. Esto quiere decir que antes de modificar los formularios deberá identificarse alguien del equipo que esté cómodo manejando esas tecnologías. El programa cuenta con formularios estándar y cuando se visualiza en android se decantara por ellos.  
  
Por favor referirse a la guía de instalación de paquetes para mas detalles de instalación
