

# _Paquete de vigilancia de ESAVIs Centinela - OPS_ - Documento de diseño del sistema


# Introducción

_“Uno de los componentes esenciales del sistema de vacunación segura es la vigilancia de los eventos supuestamente atribuibles a la vacunación o inmunización (ESAVI). A través de esta vigilancia, se busca detectar de manera temprana cualquier evento adverso que ocurra luego de la vacunación, con el propósito de controlar y clasificar los riesgos relacionados con la vacuna, el proceso de fabricación, el transporte, el almacenamiento, la administración, así como con toda situación inherente a la persona vacunada, o para descartar la relación de dicho evento con la vacuna.” ([https://iris.paho.org/handle/10665.2/55384](https://iris.paho.org/handle/10665.2/55384)) _

_La OPS ha identificado la necesidad de varios países de tener acceso a sistemas de información que puedan utilizarse como ayuda en el proceso de registrar, notificar, investigar y clasificar ESAVIs._


# Resúmen del diseño del sistema


## Caso de uso

El programa Centinela es un programa de tracker para DHIS2 que registra datos de eventos de Efectos adversos supuestamente atribuibles a la vacunación e inmunización (ESAVI) y efectos adversos de interés especial (EVADIE). Ha sido configurado basado en el [Manual de vigilancia de eventos supuestamente atribuibles a la vacunación o inmunización en la Región de las Américas](https://iris.paho.org/handle/10665.2/55384)

 de la OPSm, y en el [“Manual global de vigilancia de efectos adversos pos-vacunales](https://apps.who.int/iris/handle/10665/206144?locale-attribute=es&)” de la OMS. 

El programa cuenta con la posibilidad de incluir los catálogos de CIE, MEDDRA y WHODrug y está mapeado a los requerimientos para transmisión de datos a Vigibase, la base de datos mundial de farmacovigilancia.


## Estructura del programa


### Resúmen del contenido

El paquete de centinela cuenta con un programa de datos individuales longitudinales (tracker) y con una batería de indicadores y visualizaciones básicas.  \
 
El programa de tracker está dividido en cuatro etapas no repetibles que utilizan formularios personalizados. Para información general acerca de como utilizar DHIS2 Tracker, ver la [documentación] ([https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/tracking-individual-level-data/tracker-capture.html](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/tracking-individual-level-data/tracker-capture.html)).


### Diagrama del programa



![Image1](images/image1.png "Diagrama del flujo de trabajo")



### Explicación de la estructura 

_La idea es que este programa pueda ser utilizado por aquellos que reportan solo ESAVIs, o por aquellos países que reportan ESAVIs y EVADIEs, siendo la etapa de clasificación donde se determina que tipo de evento esta siendo registrado.  En el caso de los primeros, se ocultaría la etapa “EVADIE” y las reglas de programa correspondiente. _


### Etapas

_El programa Centinela está dividido en cinco etapas. Para un resúmen de como ingresar datos, véase la guía rápida de uso del programa: LINK A QUICKGUIDE_


#### Etapa de clasificación inicial

_En esta etapa se determina si el evento es un ESAVI o EVADIE basado en una serie de preguntas. Dependiendo de la clasificación inicial se habilitarán las etapas correspondientes._


#### Etapa EVADIE

_Solamente estaría disponible cuando el evento corresponda a un EVADIE._


#### Etapa Notificación ESAVI

_La etapa de notificación ESAVI solo está disponible cuando el evento corresponde a un ESAVI, y es donde se registran los datos generales del ESAVI y una clasificación preliminar._


#### Etapa Investigación ESAVI

_La etapa de investigación ESAVI solamente cuando es especificado que el evento requiere una investigación._


#### Etapa Clasificación final

_Esta etapa normalmente es accesible solamente a nivel distrital o nacional (es decir, a un nivel superior), y es donde se confirman los resultados del ESAVI y la clasificación final_


## Usuarios Potenciales

El programa está pensado para que los datos sean ingresados al nivel más bajo posible. Dependiendo de cómo se organice la implementación, hay distintas maneras de configurar el acceso usando los grupos de usuarios, roles, acceso a unidades organizativas, y acceso a las distintas etapas del programa. Antes de implementar, el país deberá aclarar el proceso de negocio para los ESAVI/EVADIE que deberá seguirse y quienes deben tener acceso a la información y a que nivel.


### Combinación de grupos de usuario, roles y acceso a unidad organizativa

 
Los grupos de usuario sirven para dar acceso a los distintos programas (por ejemplo, el programa de EVADIE). Y regular que nivel de acceso tienen los usuarios dentro de ese grupo al programa. El nivel de acceso está basado en datos y metadatos, y en poder ver o editar.

La combinación de grupo de usuarios, roles y acceso a unidad organizativa permitirá controlar la granularidad del acceso. Para más información acerca de la configuración de acceso compartido, ver la [documentación de DHIS2](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-236/configuring-the-system/users-roles-and-groups.html). 



<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")



Grupos de usuarios básicos 
 
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


## Mayor granularidad

En caso de que el país quisiste mauor granularidad de acceso, es posible agregar mas grupos y entre la combinación de roles, acceso a unidad organizativa y acceso a las distintas etapas y aplicaciones, poder lograr restringir el nivel de acceso deseado.


# Configuración del programa de tracker

El programa de Tracker CENTINELA incluído en este paquete debe considerarse un programa inicial que cumple con los requerimientos de OPS para la captura de datos de ESVI. Este deberá adaptarse a la realidad nacional antes de comenzar a ser utilizado, en particular en el perfil de la persona. Las distintas etapas están configuradas con formularios personalizados que si van a cambiarse requieren conocimiento de CSS, javascript y HTML. 



### Placeholders

Algunos de los elementos de datos están asociados a un estándar terminológico. Distintos países optarán por distintos estándares, y por tanto, no los hemos incluído en este paquete. En vez de los catálogos estandarizados, hemos incluído un placeholder para que el país pueda incluir el estándar que sea adecuado a su contexto. Véase la guía de instalación para ver instrucciones de como configurar estos estándares. 


####  Lista de elementos que contienen un placeholder 


Esta lista contiene actualmente el ejemplo del estándar de terminología que se está aplicando en la instancia regional. 


<table>
  <tr>
   <td>Nombre del elemento
   </td>
   <td>Set de opciones actual en la instancia regional
   </td>
  </tr>
  <tr>
   <td>AEFI - Vaccine 1 name
   </td>
   <td>CEN-Vacunas COVID (whodrug)
   </td>
  </tr>
  <tr>
   <td>AEFI - Vaccine 2 name
   </td>
   <td>CEN-Vacunas COVID (whodrug)
   </td>
  </tr>
  <tr>
   <td>AEFI - Vaccine 3 name
   </td>
   <td>CEN-Vacunas COVID (whodrug)
   </td>
  </tr>
  <tr>
   <td>AEFI - Vaccine 4 name
   </td>
   <td>CEN-Vacunas COVID (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - C Diagnostico Final
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - ComplicaAnomCongDx1
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - ComplicaAnomCongDx2
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - ComplicacionEmbDx1
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - ComplicacionEmbDx2
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - ComplicaFetalDx1
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - ComplicaFetalDx2
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Name 1
   </td>
   <td>CEN-medicamentos principio activo (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Name 2
   </td>
   <td>CEN-medicamentos principio activo (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Name 3
   </td>
   <td>CEN-medicamentos principio activo (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Name 4
   </td>
   <td>CEN-medicamentos principio activo (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Name 5
   </td>
   <td>CEN-medicamentos principio activo (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Name 6
   </td>
   <td>CEN-medicamentos principio activo (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Name 7
   </td>
   <td>CEN-medicamentos principio activo (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Name 8
   </td>
   <td>CEN-medicamentos principio activo (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Name 9
   </td>
   <td>CEN-medicamentos principio activo (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Presentation 1
   </td>
   <td>ESAVI - Forma Farm
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Presentation 2
   </td>
   <td>ESAVI - Forma Farm
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Presentation 3
   </td>
   <td>ESAVI - Forma Farm
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Presentation 4
   </td>
   <td>ESAVI - Forma Farm
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Presentation 5
   </td>
   <td>ESAVI - Forma Farm
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Presentation 6
   </td>
   <td>ESAVI - Forma Farm
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Presentation 7
   </td>
   <td>ESAVI - Forma Farm
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Presentation 8
   </td>
   <td>ESAVI - Forma Farm
   </td>
  </tr>
  <tr>
   <td>ESAVI - Drug Presentation 9
   </td>
   <td>ESAVI - Forma Farm
   </td>
  </tr>
  <tr>
   <td>ESAVI - Medical History 1
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Medical History 2
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Medical History 3
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Medical History 4
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Medical History 5
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Medical History 6
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Medical History 7
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Medical History 8
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Medical History 9
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Nivel Subnacional
   </td>
   <td>ESAVI - Distritos
   </td>
  </tr>
  <tr>
   <td>ESAVI - OtroESAVI1
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - OtroESAVI2
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - OtroESAVI3
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>ESAVI - Vaccine Name 5
   </td>
   <td>CEN-Vacunas NO COVID (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Vaccine Name 6
   </td>
   <td>CEN-Vacunas NO COVID (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Vaccine Name 7
   </td>
   <td>CEN-Vacunas NO COVID (whodrug)
   </td>
  </tr>
  <tr>
   <td>ESAVI - Vaccine Name 8
   </td>
   <td>CEN-Vacunas NO COVID (whodrug)
   </td>
  </tr>
  <tr>
   <td>EVADIE - Medical History 1
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>EVADIE - Medical History 2
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>EVADIE - Medical History 3
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>EVADIE - Medical History 4
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>EVADIE - Medical History 5
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>EVADIE - Medical History 6
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>EVADIE - Medical History 7
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>EVADIE - Medical History 8
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
  <tr>
   <td>EVADIE - Medical History 9
   </td>
   <td>ESAVI - Meddra
   </td>
  </tr>
</table>



# Detalles de las etapas

Las etapas se han configurado con formularios custom en HTML, y un formulario con secciones en caso que se desee utilizar android. Las capturas de pantalla corresponden al formulario web custom.


## Registro inicial del caso

El registro inicial del caso son los datos de la persona deberán adecuarse a las necesidades del país cuando se hace una instalación nacional (Por ejemplo, cambiar el nombre de “municipio” a “cantones” y modificar la lista de opciones a los lugares correspondientes. \
 \


<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.png "image_tooltip")



## Etapa 1:Clasificación 


## Etapa de clasificación inicial

_En esta etapa se determina si el evento es un ESAVI o EVADIE basado en una serie de preguntas. Dependiendo de la clasificación inicial se habilitarán las etapas correspondientes._



<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.png "image_tooltip")



## Etapa EVADIE

_Solamente estaría disponible cuando el evento corresponda a un EVADIE._


## Etapa Clasificación final

_Esta etapa normalmente es accesible solamente a nivel distrital o nacional (es decir, a un nivel superior), y es donde se confirman los resultados del ESAVI y la clasificación final_


# Analytics


## Indicadores/ Indicadores

_DHIS2 calcula indicadores basados en los datos y genera visualizaciones preconfiguradas que son principalmente mostradas en los tableros de información. Usuarios, dependiendo de su acceso, pueden crear sus propias visualizaciones, mapas gráficas e indicadores._

_Los indicadores en DHIS2 son cálculos basados en elementos de datos, y se dividen en indicadores simples (Numerador/denominador) e indicadores de programa (basados en un conteo por filtros). Elementos de datos que puedan accederse sin tener que incluir cálculos o filtros son agregados automáticamente. Por más información acerca de indicadores e indicadores de programa en DHIS2 ver la documentación._

_Los indicadores incluidos dentro del paquete son los indicadores más básicos y no pueden considerarse como un set analítico extensivo.Una vez teniendo DHIS2 en una instancia propia podrían configurar nuevos indicadores o indicadores de programa. Para un análisis más avanzado, los datos pueden ser exportados y analizados en otra herramienta._

_Para la exportación de datos, y en función del volumen y del análisis que se quiera establecer, se podría usar la propia API que provee dhis2. Mediante dicha API, se puede consultar tanto los datos “en tiempo real” como los datos “de análisis”. Las llamadas a la API dependerán del análisis que se quiera realizar. Además, hay que tener en cuenta que pueden definir políticas para la descarga de información (en función de lo actualizado que se quiera estar) y que estas llamadas se pueden realizar de manera programática mediante scripts en diferentes lenguajes de programación. El modelo de datos que es usado para descargar la información puede alterarse de manera programática para que la información a analizar sea lo más idónea para este proceso.  _


### Indicadores de programa

_Documentación: https://docs.dhis2.org/en/use/android-app/program-indicators-supported.html _

_Lista de indicadores incluídos: XXXXX_


### Indicadores

_Documentación: [https://docs.dhis2.org/en/implement/database-design/aggregate-system-design/indicators.html#:~:text=In%20DHIS2%2C%20the%20indicator%20is,do%20not%20have%20a%20denominator](https://docs.dhis2.org/en/implement/database-design/aggregate-system-design/indicators.html#:~:text=In%20DHIS2%2C%20the%20indicator%20is,do%20not%20have%20a%20denominator)._

_ Lista de indicadores incluídos:


## Tableros:

_El programa cuenta con tres tableros básicos que deberán ser adaptados a las necesidades del país. Estos muestran visualizaciones basadas en lo indicadores descritos en la sección anterior._

_Tablero ESAVI_

_Tablero EVADIE_


# Validation rules / Program rules

_[any needed justification. Otherwise add ref to Installation guide]_

_program rules / managements for clinical decision-support tools to be added if relevant_


# Dashboards 



* _[Dashboards are included? Provide name and any specific info if required_
* _Provide table summary of the items in the dashboard (or provide an excel with such info) - name of item, title, type, indicators used_
* _Screenshot of dashboard items and provide description of content for each dashboard + supplementary screenshots for any item that might require further explanation]_
* _Please follow data visualization suggestions outlined here: _


# Special considerations

Ciertos procesos deberán tomarse en cuenta a la hora de instalar y modificar el paquete en una instancia propia. Por favor referirse a la guía de instalación de paquetes para mas detalles
