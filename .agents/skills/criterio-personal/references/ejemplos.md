Estos son algunos emails escritos por mi:

Buenas chicos.

Con respecto a lo que comentas persona_x, si, fundamental crear la fecha de firma local en tipo DATE y no sólo en timestamp. TIMESTAMP para temas informativos y la de DATE para hacer los joins, no hagáis joins con TIMESTAMP o el performance se va a ver muy afectado. También a la columna de DATE hay que agregarle un indice b-tree. En fact_duty también de necesitamos ese índice.

Con lo que comentas de realizado, recuerdo este problema con las fechas de firma. Podemos hacerlo como tú dices con las fechas de salida de los vuelos o aplicando sobre las horas de salida el mismo cálculo que hemos hecho para programado por ser consistentes (pese a que no sea real) , como quieras.

Con respecto a la URL del dashboard. ¿Quién se encarga en compañia_X de la gestión del hosting y dominios? Si me indicas me pongo en contacto con ellos y mapeamos las DNS. También veo útil facilitar un acceso desde la web de compañia_X para que este accesible de forma sencilla - que también lo comento con ellos.

Abrazo, buen finde.

---

Buenos días @persona_k 

¡Espero esté todo bien! 
La semana pasada estuve hablando con Roberto de IT de compañia_X para un tema de las DNS de Azure y vuestro hosting de cara a que podáis tener más accesible el Skynet en la web, pero me comentó que vosotros en la sección de compañia_y gestionáis por vuestra cuenta vuestro propio dominio y zonas DNS.

Intenté llamarte el viernes y hoy de nuevo, pero no he podido localizarte. 
Si te parece bien dime que disponibilidad tienes para gestionar esto y si no eres tu la persona con la que hacerlo, por favor redirígeme a quien esté gestionando el dominio. 

Un saludo,

---

Buenos días.

He estado analizando la métrica 12 y antes de seguir quiero lanzar una reflexión para que pensemos juntos como enfocarlo.
Sé que este no es el foco ahora, por lo que podemos comentarlo para cuando lo sea.

En la tabla fact_mensual_duty_programado es cierto que tenemos pre calculados los días_VV días_AT etc. Esto ayuda con el preprocesamiento e intuyo que parte de la razón por lo que se hizo fue para métricas como estas.
El problema viene ahora con el tema de las jerarquías de grupos y subgrupos y a la hora de hacer filtrados dinámicos. Es decir, al escoger grupos o subgrupos que impliquen intersecciones entre las columnas de los días y haya que hacer operaciones.

Aquí lo que ocurre es que, por estas jerarquías, las contabilizaciones hay que tratarlas con cuidado, ya que podríamos estar contabilizando de más dependiendo del filtro que escoja el usuario; y de ahí surgen los descuentos y los ajustes que plantea @persona_x para arreglarlo, vinculando a esos días tipo (columnas) las relaciones con subgrupo y grupo.

Sin embargo, leyendo las especificaciones, creo que esto podría añadir una complejidad bastante grande a nivel cálculos del backend, y además desaprovechar la ventaja de haberlo pre calculado anteriormente, porque ahora para mostrar el dato, se estarían haciendo siempre cálculos dinámicos donde se hacen esos ajustes en función del filtro del usuario.

Cuando he pensado en esto he llamado a persona_y para ver si esto estaba ocurriendo en alguna otra métrica porque me parecía raro que no hubiese ocurrido ya con alguna que usase fact_mensual_duty_programado, sobre todo tema de factor de prorrateo, días trabajados etc, pero da la casualidad de que no, porque no hay columnas de estas que se relacionen entre sí en función de ninguna combinación de filtros usada hasta ahora. (Pero esto me gustaría también confirmarlo contigo @persona_x  ; la única que se nos ha ocurrido es la de paternidad y maternidad que suma las columnas, pero no hay ninguna intersección complicada como si que ocurre en este caso).

Creo que para realizar todo esto sería más sencillo trabajar con las tablas base de duty fact_duty_programado porque en ella tenemos la relación del duty con su subgrupo y grupo. Y en vez de hacer sum(columna_tipo_dia) hay que hacer un count() donde aparezca el criterio filtrado por el usuario sin tener que estar haciendo ajustes. No obstante, la tabla de fact_mensual_duty_programado seguramente haya que seguir teniéndola en cuenta para los días presentes y el uso de alguna otra columna útil, pero esto se puede seguir haciendo con un join contra fact_duty_programado con la nomina, flota y periodo (haciendo un convert de la fecha)

Decidme como veis esto. Sobre todo @persona_x .
Si quedan dudas también decidme, que seguro que no me he explicado todo lo bien que me habría gustado.

Un saludo,


---

Buenas persona_x!

Espero que este correo te pille bien 😊
Quería proponerte un par de slots en esta semana para que nos viésemos un ratillo e intentar terminar de ver lo que empezamos a mover de cara a la posibilidad de trabajar juntos , los puestos de compañia_t etc.
Te propongo y me dices:
-	Hoy 01/06 a partir de las 17:30 
-	Miercoles 03/06 entre 12:00 y 15:00 o a partir de las 17:30
-	Viernes 05/06 me adapto a cuando me digas 

Abrazos y buena semana.


---

Buenas tardes.

Me gustaría concretar con vosotros la entrega de las primeras métricas de este nuevo entorno de Skynet con todos los cambios que se han llevado a cabo y aprovecharlo para que podáis vivir más de cerca lo que se va avanzando del proyecto.
Creo que es un buen momento para reflejar los esfuerzos y el progreso, y daros reporte de ello de forma dinámica en una reunión.

Ahora que ya llevamos un par de meses adentrados, estoy seguro de que es un buen punto de control para que nos deis feedback de vuestra visión y nos vendrá muy bien para seguir alineados.

Hemos pensado en que el viernes podría ser una buena fecha candidata para ello, aprovechando que suele ser un día con algo menos de carga de trabajo. ¿Os viene bien? ¿@compañia_X Nos podríais dar un par de opciones de slots para cuadrar la reunión?

Abrazos,


---

Buenos días,
Os paso resumen de la reu interna de seguimiento de ayer para esta semana, para que @persona_x  también esté informado:
•	Implementación del recálculo de ratios.
•	Retoques en métricas 1 y 2 reportados por persona_x.
•	Implementación métricas 3 y 19.
•	Se va a verificar el borrado y actualización (funcionalidad ETL implementada semanas atrás).
Todo en TRELLO ya

Para la próxima reu @persona_x  hay un tema con los DPAs que quiero que veamos:
•	Posibilida de tener una plantilla estandarizada para no depender del archivo de compañia_y y realizar siempre la carga sobre el mismo formato, evitando romper la integración.
•	Añadir una columna de periodo para no tener que obtener el periodo desde el nombre del archivo.
•	Entender cómo afecta esto al flujo de carga y actualización de la ETL, 2 opciones:
o	que el último paso recoja automáticamente el archivo si está ubicado en la ruta adecuada, o
o	que el proceso permita al usuario seleccionar/cargar el archivo de DPAs al final.
Gracias.


---

Buenos días persona_x.

Gracias por la aclaración, estamos contigo - creo que estamos todos en el mismo punto y sincronizados. Ya no le estamos dando más vueltas al tema, los correos anteriores iban con el objetivo de aclarar unos puntos que faltaban por entender respecto a datos faltantes que habían detectado desde compañia_l. Si crees que no son necesarios para el histórico, los dejamos fuera.

-	Como vimos en la anterior reunión, es necesario hacer el proceso de carga de ETL histórico, eso ya se decidió – vimos que no se puede volcar el parquet directamente porque la BDD está normalizada y no se puede deshacer de manera sencilla. Además el flujo montado actual está pensado para eso. Cargar el parquet y deshacer implicaría montar una cosa diferente. A raíz de eso es por lo que tu añadiste sobre el código actual (que vuelca a las tablas normalizadas) lo faltante, para de tal forma llegar a unos datos en la estructura, que cruzados entre si, son equivalentes al parquet. 
-	Con los TODO está persona_y, así como con las funcionalidades de la ETL de producción que son necesarias y que no son obvias, ya que se tienen que construir a partir de casos específicos y casuísticas con ejemplos como la falta de los códigos de reducción.

Creo que tras haber ido añadiendo progresivamente casos y especificaciones, así como por las modificaciones que han surgido, se ha dado lugar de forma natural a las iteraciones que estamos viendo.

Por favor @persona_y , cuando podamos validar todo esto coméntanos. Debería de ser una validación de datos así como una validación de la funcionalidad de la ETL para lo programado.
Yo en la reunión de mañana no estaré.

Gracias, abrazos,


---

Buenos días.

Gracias persona_x por el input.
Bajo mi visión, también tenía la sensación de que estábamos yendo por muy buen camino, pero leyendo tu email, entiendo que has detectado errores tanto de validación como sobre todo de comprensión de los detalles que has aportado a los notebooks ¿Es así? 

Ahora mismo lo prioritario es que los datos se procesen mediante la ETL de tal forma que se cumplan las validaciones y transformaciones necesarias y que has documentado para llegar a un set de datos idéntico al que se proporciona en los .parquet . En esta línea , tenía entendido que estaba claro este objetivo. @'persona_y ' entiendo que también había comprendido esto, y creo que deberíamos enfocar la reunión en entender que es lo que ha fallado. Si es un tema de no comprender el objetivo, los detalles o simplemente que no se había terminado completamente la validación. 
@persona_x  ¿se te había comunicado que estos datos estaban ya completamente validados y contrastados con los parquet y que se podía cerrar esa fase? Yo no tengo constancia de que se hubiese dado esto completamente por cerrado.

Por favor, @'persona_y ', mientras persona_x sigue revisando, te pido que repases las indicaciones que se dan en los notebooks para que verifiques que los pasos se están realizando y que lo que se ha desarrollado tiene sentido. De tal forma que cuando persona_x aporte los errores encontrados , podamos entender que no se ha comprendido correctamente.

@persona_x  de nuevo gracias por aportar los detalles y tu esfuerzo, no te preocupes que juntos vamos a canalizarlo para conseguir el objetivo.

Un saludo.


---


No, no!
Los correos están muy bien , y el nivel de detalle está siendo clave para alinearnos con lo que necesitáis, no quiero que se cambie nada de eso.

Por el vuelco a Trello, entiendo que eso cae más de nuestro lado, que suficiente carga de trabajo supone para ti la definición de todo. Pero siéntete libre de aportar por supuesto si quieres, te lo agradezco mucho …

A ver si hoy pudiéramos tener el circuito completo de programado con la funcionalidad de la ETL de carga y eliminación de archivos e integridad de datos. Es decir que si solo existiese el mundo de programado, se pudiese operar con la herramienta y sacar métricas tirando sql contra la bdd.

El melón de lo de Tableau, es como tu dices, un buen melón. Yo creo que esto va a depender del uso que se les de a las graficas. Si hay mucha interactividad, nivel de detalle etc, no cambiaría Tableau ni de broma. Hay muchas métricas que replicarlas en código propietario sería muy complicado. El argumento para vosotros que os hace plantear ese cambio, ¿Cuál es?. Por entenderlo y plantear…

Saludos


---

Buenas.

Si se va a dejar la concatenación para algunos, entonces lo haría para todos. Hacer el mapeo solo para esos par de casos no lo haría (FLOTA SMS , INSTRUCTOR -> FLOTA SMS); ya lo dejaría como está, por mantener consistencia de nuevo. Creo que quedarnos a medias no nos ayuda jajaja. 

Entiendo lo que dices, si crees que es lo mejor lo hacemos así. Pero para tema filtrado ya te digo que creo que puede ser un problema. Por ejemplo la métrica en la que se estudia el intercambio de vuelos entre cargos, ahora cuando alguien tenga varios cargos no vas a saber en la matriz si le englobas en ambas contabilizaciones solo en 1 , en ninguna... Y desagregar un concat para un join y desdoblar los datos es una movida. Pero bueno poco a poco. Seguramente me falte contexto y tú lo veas mejor esto con lo que tienes en la cabeza de las visualizaciones.

Lo que si que te aseguro es que el tema lentitud no era por el join con la tabla dim_piloto antigua. Tiene que ver con muchos otros factores de cálculos en tiempo de ejecución, periodos de datos escogidos en función de finalidad de la métrica (por ejemplo no tiene sentido sacar periodos de 1 año en una métrica que te da el detalle del intercambio diario de actividades) etc.
Pero ya resolveremos eso más adelante.

En conclusión , creo que lo que solicita @persona_x  es importante asique hagámoslo así @'persona_y ' y concatenemos para la mensual de piloto los cargos.

Tema prorrateo, es correcto tenerlo en esta tabla porque es una tabla con granularidad definida mensual , por tanto el prorrateo ese al ser mensual está correspondido con el dato.
Ahora ya estás dos últimas tablas que has mencionado digamos que son derivadas de las tablas clave (yo llamaría tablas clave a las que no se pueden replicar de ninguna otra) , no? Por lo que su procesamiento va a saltar después de volcar en tablas principales.
Todo esto antes de hacía a nivel SQL , pero se puede hacer a nivel ETL. En mi opinión SQL es más fácil y mucho más eficiente pero lo que veáis aquí.

Abrazos. 
Buen finde


---

Hola.

Yo personalmente está opción que dice Claude no la utilizaría de ninguna manera. Es una solución muy compleja que luego para hacer métricas va a complicar todo muchísimo. De hecho desde un punto de vista de arquitectura no es una buena solución.

Creo que la mejor alternativa es seguir el mismo patrón que con flota y reducción ¿no?

En caso de un mes haber varios cargos, en la del piloto dejaría VARIOS y en la de duty ya los tenemos ligados a las actividades. Por ser consistentes igual que hemos hecho con TRANSICION (si no en flota también podríamos haber concatenado | que igual la opción buena es concatenar UNICAMENTE para la tabla de pilotos, no digo que no) .
Pero en la tabla de los duties mantener el cargo acorde a cada actividad.

Sea la solución que sea el hecho de mantener absolutamente toda esta información va a traer un coste de complejidad a la hora del cálculo de métricas por como crucemos los datos para los filtros y demás. El orden jerárquico que había antes permitía simplificar  las cosas, se perdía algo de info pero era menos "messy". Igual se hacía con la flota y reducción.

Ya me decís lo que pensáis.

Saludos.


---


Hola a todos. 

He revisado todo, muchas gracias por el gran trabajo a ambos… @persona_x  el análisis nos ayuda muchísimo. Estás avanzando un montón y puedes respirar, que hay trabajo de sobra, no te agobies con los tiempos
@persona_y , el Excel que has hecho es fantástico, gran iniciativa. 

Un apunte sobre esto; con ciertas comprobaciones e implementaciones descritas en los notebooks, sobre todo las que son distintas eras (pero sin excluir al resto, que hay más), hay que tener en cuenta que en la ETL que despleguemos para producción y uso continuado, todo eso “ya no sirve”, porque hay que tener en cuenta únicamente el formato actual de las cosas. 
Entonces por limpieza de código y flujos de las reglas de negocio que si que aplican a los datos actuales, creo que es importante remarcar que dejemos separado bien esto. Para que la ETL sea fácilmente mantenible. Por un lado lo antiguo y por otro lado las funcionalidades de carga actuales. Así lo hicimos la vez anterior y creo que es la mejor decisión para futuro.

Saludos,

---


Estos son algunos reportes escritos por mi:

---

Web service IIS, su configuración se puede observar en el XML disponible en http://10.170.6.76:8082/InformeNET.svc?singleWsdl . 
El web service está configurado para aceptar distintas llamadas mediante el protocolo SOAP. Cuando se realiza una petición SOAP, el webservice está configurado para señalar a unos end-points configurados en .NET (o VB) . Esto servicios de .NET (o VB) se encargan de desencadenar las acciones necesarias para devolver lo que la solicitud requería. Por ejemplo si la solicitud es ObtenerInforme_Particular, el servicio recibirá distintos parámetros entre los cuales se encuentran, por ejemplo, el código de control del caso (C_Control) y el centro. Con estos datos el servicio invoca el procedimiento almacenado Web_BuscarAnalisis en la base de datos del centro pertinente. La respuesta tanto del procedimiento como del servicio es el pdf en base 64. 
El web service está configurado para poder recibir llamadas parametrizadas de varios tipos incluso para cada solicitud, es decir la solicitud ObtenerInforme_Particular podría recibir por parámetros no solo el código de control, sino también, por ejemplo el número de referencia.
Para hacer testing de estas llamadas se puede utilizar SOAPUI, siguiendo los siguientes pasos:
1.	Descargar SOAPUI
2.	Abrir SOAPUI y pulsar en el menu superior sobre SOAP
3.	En initial wsdl pegaremos la URL del webservice.
4.	SOAPUI reconocerá automaticamente los end-points y podremos seleccionar en la leyenda el tipo de solicitud que queremos hacer. Para este caso se escoge ObtenerInforme_Particular
5.	SOAPUI preparará una llamada estándar en la que podremos indicar para la realización de las pruebas lo siguiente: en el tag Parametros: Control=2023000001; en el tag Centro: Pontevedra_AP
6.	Al ejecutar la llamada en la parte de la derecha podremos encontrar la respuesta en XML que contendrá el pdf en base 64.
En la simulación anterior, al realizar la solicitud al webservice, el servicio asignado al endpoint ObtenerInforme_Particular invoca en la base de datos de Pontevedra_Ap el procedimiento Web_BuscarAnalisis pasándole los parámetros que se le haya especificado.

El procedimiento Web_BuscarAnalisis:
Primero identifica el tipo de llamada que se le está haciendo, separando la lógica en función del tipo de string recibido por parámetros. Para cada tipo de string se ha de aplicar una lógica diferente ya que es probable que haya que consultar distintas tablas de la base de datos. Sin embargo el objetivo del procedimiento es siempre devolver una tabla con varios campos entre los que se puede encontrar el codigo de control, el informe en binario, en xml... A continuación se muestran 2 posibles string que podría recibir el procedimiento, para los cuales se realiza una lógica distinta mirando en diferentes tablas de la base de datos
-	 Control=xxxxxx[|Idioma=12][|AdjuntarHCO=S][|Previsualizar=N][|EsWeb=S]
-	H18HQVIT10000972018032309202010041633|39777777|S

En el primer ejemplo se especifica un numero de control y otra serie de parametros opcionales. Para recuperar los datos que el procedimiento ha de devolver se utilizan las tablas de SRVCli o de Clientes. Esto permite recuperar datos esenciales y cargarlos en una tabla temporal #Web_BuscarAnalisis_Analisis, que se utiliza más adelante en un bloque común para todo el procedimiento. Por otro lado, para el segundo ejemplo, la manera de obtener estos mismos datos es diferente, ya que en este caso se está recibiendo por parámetros un número de petición del HIS y una referencia. Por tanto se ha de realizar la búsqueda del caso con estos parámetros utilizando otras tablas, como pueden ser las tablas propias que guardan información de las peticiones de los HIS (e.g. ESB_Peticion). Además si no se encuentran los datos requeridos, se ejecutará el procedimiento en los servidores vinculados al centro. 
Tras filtrar por cada tipo de escenario y distinguir entre los parámetros de entrada, el procedimiento Web_BuscarAnalisis ejecuta un bloque de código común en el que se recupera el informe.
Es interesante remarcar que el modelo de cada informe varía según el tipo de centro por lo que se ejecuta el procedimiento Impresion_ModeloImpresion_CalcularModeloInforme, que mediante una SQL dinámica cambia la condición de impresión utilizando la tabla Impresión_ModeloImpresion. Esta tabla contiene las reglas que determinan el modelo de impresión que se desea obtener.
Mediante la tabla Impresión_Plantilla se obtienen las plantillas del informe que se quiere imprimir, y el procedimiento de impresión, que se parametriza de forma dinámica con los datos que se han guardado anteriormente en la tabla temporal #Web_BuscarAnalisis_Analisis. Este procedimiento suele ser Impresion_ImprimirInforme, aunque para informes HTML se utiliza Web_Impresion_ImprimirInforme.
Impresión_ImprimirInforme se encarga de generar las plantillas, buscando en base de datos las pruebas de los análisis y creando el código necesario para más tarde procesar el PDF. Se incluyen estilos de CSS y la lógica necesaria para estructurar correctamente el display de las tablas, resultados de pruebas etc.
Finalmente el procedimiento Web_ BuscarAnalisis devuelve el resultado de todas las operaciones anteriores, informe pdf, informe binario , informe xml, cadena de conexión de la base de datos, el servidor etc. 
Estos datos se utilizan para que el servicio pueda devolver al request inicial el pdf en base 64, en el caso de nuestro ejemplo.


---

PROYECTO BI 
Actualización 26/06/2023

Estrategia de implementación:
Se está trabajando sobe una solución de proyecto generada en VisualStudio para DevExpressBI. Se establecen las conexiones y configuraciones y se diseñan los dashboards. Estos dashboards se guardan como xml para poderse importar en el futuro. El objetivo es que los dashboards se integren en la app nativa de ATLAS. Para la implantación se necesitan realizar ajustes futuros (ya planteados con persona_j).
A continuación, se muestran una serie de dashboards interactivos construidos en DevExpress con los KPI de número de análisis según turno, laboratorio y áreas de laboratorio. Se utilizan filtros de rangos filtración dinámica y drill down y drill up para desplazarse por distintos niveles de granularidad.

-	Filtro incluyendo los datos del ultimo año desagregados por turno y áreas. Vision detallada por laboratorio y tipo de paciente en la tabla pivot.

 





-	Filtro a turno de tarde en laboratorios de Mallorca y despliegue en la tabla pivot los análisis por tipo de paciente:

 

Sobre este dashboard se pueden realizar varios análisis dinámicos según las dimensiones mencionadas y utilizando distintos filtros.

Preocupaciones y foco actual:
Rendimiento. El rendimiento tanto de las consultas como de la experiencia de diseño de DevExpress resulta muy lento sobre todo en la interacción dinámica. Esto puede ser debido a varios factores que podrían estar condicionando la realidad, como podrían ser los recursos de mi máquina virtual que es la que ejecuta actualmente el proyecto de VS. En tal caso, el rendimiento en un entorno de producción real sería mayor. Ya que se desconoce, se está realizando un estudio de alternativas para las conexiones y el procesamiento de los datos.
Una de las mayores preocupaciones es brindar al cliente una experiencia de análisis de datos fluida. Para ello se están realizando pruebas de rendimiento para escoger la estrategia más apropiada para la visualización de datos y la arquitectura de la solución. 
Esta estrategia se basa en comprender técnicamente el plan de ejecución del motor de procesamiento y las posibles conexiones. A continuación, se muestra un esquema de la arquitectura actual.



Visión de arquitectura actual:

 
Estructura de datos en modelo datawarehouse:
-	Tabla de hechos (fact table): conteniendo el level of detail deseado, también conocido como granularidad o nivel de agregación. En este caso se opta por análisis desagregados por turnos y por dimensiones específicas.
-	Dimensiones: conteniendo la información adicional de cada dimensión presente en la fact table. 
Pipeline automatizado y proceso ETL implementado y explicado en el documento del 16/06/2023. Permite tener una arquitectura óptima para análisis y que esté automatizada. En este punto del datawarehouse las tablas ya están presentes y automatizadas para el análisis que se desea hacer. Por cada tipo de análisis y KPI se han de generar fact tables nuevas.
Se pueden observar 2 formas de proceder a partir del datawarehouse:
-	Se desea procesar el cubo OLAP para utilizarlo como fuente de datos. Debido limitaciones temporales con esta opción se está explorado la segunda opción hasta poder continuar.
-	En la segunda opción se hace una conexión directa al datawarehouse, el cual ya tiene la estructura óptima para realizar analítica de datos. Las opciones de conexión en vivo son mediante procedimientos o a tablas. La opción de Extract aún se desconoce si está disponible en DevExpressBI. En Tableau está disponible y permite realizar extractos programados de la base de datos para preprocesarlos y poder operar con ellos de forma más eficiente que en una conexión en vivo. 
Para la segunda opción se plantea la duda de si el rendimiento es mayor estableciendo la fuente de datos como una query según procedimiento almacenado con parámetros dinámicos o si la conexión se realiza a tablas directamente y se dispone de ese mismo filtro para el filtrado dinámico en las vistas.

Análisis de rendimiento.
Ya que devexpress no tiene las herramientas para analizar este rendimiento, se ha utilizado Tableau para simular el mismo escenario; dashboard cuya fuente de datos es un procedimiento almacenado frente a mismo dashboard cuya fuente de datos son las tablas del datawarehouse. 
Se analiza la comparativa del rendimiento de conexiones. 
El dashboard es el mismo para ambos tipos de conexiones. De esta forma la comparativa es relevante. El modelo de análisis se basa en medir el tiempo que tarda el dashboard en cargar y desplegar los datos (simulación real para el consumo del usuario) con procedimiento almacenado vs conexión a tablas. 

Método de conexión 	Dificultad del dashboard  / queries	Tiempo de carga de dashboards (s)	Retraso por conexión inicial (s)
Directa	1	1.16	Despreciable
Procedimiento	1	1.02	Despreciable
Directa	2	7.46	Despreciable
Procedimiento	2	8.36	64
Directa	3	16.87	Despreciable
Procedimiento	3	26.41	173

(Fuentes de los datos en anexo)
A priori se puede observar que la conexión directa a tablas es más rápida que mediante procedimiento almacenado. 
Tras analizar el plan de ejecución, planteo una explicación a esto bajo la siguiente hipótesis. Al configurar la conexión mediante procedimientos almacenados, los dashboards y sus interacciones ejecutan queries con SQL anidadas. A priori uno podría pensar que el procedimiento almacenado devolvería un set de datos que se utiliza posteriormente el motor de la plataforma de BI mejorando la eficiencia, pero la realidad es que la conexión sigue siendo en tiempo real y por tanto se ha de volver a lanzar una query contra la base de datos, que al contener consultas anidadas supone una mayor carga produciendo un efecto adverso. La demostración se puede observar en las siguientes imágenes:






-	Conexión directa:
 

-	A SQL customizada
 
-	A procedimiento almacenado
 

Cabe destacar que se está investigando actualmente otros modos propuestos por DevExpress como el modo servidor o la posibilidad de utilizar extracts con el objetivo de encontrar la opción de mayor rendimiento. 
El objetivo de este análisis es entender el funcionamiento interno de los motores de BI para poder implantar la solución que más nos beneficie. 
Inconvenientes encontrados sobre procedimientos almacenados:
Delay upfront de la carga de la fuente de datos entera. Con la conexión a la base de datos mediante procedimiento almacenado, Tableau crea una tabla temporal. Con la conexión a tablas se consiguen los metadatos de manera más eficiente. (Se está analizando si la metodología es la misma con DevExpress). 
Independientemente de haber ejecutado el procedimiento almacenado, la conexión es en vivo, por lo que cada interacción con un dashboard fuerza una ejecución de ese procedimiento almacenado en la base de datos añadiendo los parámetros específicos de los dashboards. Esto implica que las tablas devueltas por el procedimiento almacenado ejecutado inicialmente no quedan precargadas para que las vistas las utilicen más eficientemente. De hecho, el procedimiento almacenado crea una tabla temporal en la base de datos, que es a la cual accede por cada interacción con los dashboards. 
Ventajas encontradas para procedimientos almacenados:
Pese a tener que estudiarse más detenidamente los tiempos de retraso de la conexión inicial que serían lo más limitante actualmente, si se establece un rango sensato en el filtro de parámetros dinámicos del procedimiento almacenado, la interacción es más rápida que con una conexión directa a tablas. 

Siguientes pasos:
Se está preparando una conexión para el dashboard de DevExpress mediante procedimiento almacenado y conexión a tablas con el mismo rango de filtrado para comparar experiencia de usuario. 
Se propone desplegar esto en un entorno real con ATLAS y un equipo con mejores recursos para evaluar las posibilidades. 
Cuando se pueda procesar el cubo OLAP se utilizará este como fuente de datos. Habrá que idear la forma de mantener esa conexión actualizada y el cubo OLAP preprocesado con los últimos datos. 


---


Existen varios modos de conexión a fuentes de datos. 
-	Conexión directa a BDD
-	Conexión mediante procedimiento almacenado
-	Conexión a un cubo OLAP
-	Conexión a un extracto
A demás en conexiones a BDD se permite la conexión en vivo (modo servidor) o en modo cliente para recuperar los datos y realizar las operaciones en el cliente (donde se encuentre DevExpress).
Modo de conexión	Tiempo de carga (s)	Tiempo de interacción (s)
A tablas (modo servidor) (junio 2023)	31.22 	24.9
A tablas (modo cliente) (junio 2023)	10.4	Despr
Proc almacenado (junio 2023)	10.01	Despr
A tablas (modo cliente) (desde 2021)	104	Despr
Proc almacenado (desde 2021)	104	Despr
A tablas (modo cliente) (desde 2019)	379	Despr
Proc almacenado (desde 2019)	105	Despr
Proc almacenado (desde 2013)	>600	Despr

La opción de conexión a BDD en vivo o modo servidor queda descartada por tiempos de interacción. 
La opción de conexión a BDD en modo cliente queda descartada por tener un modo funcional similar al procedimiento almacenado, siendo este último más eficiente en el caso de DevExpress.
La opción de procedimiento almacenado presenta un bajo rendimiento para cargas importantes (múltiples variables, o un largo periodo de tiempo que conlleva más tuplas de datos). 
Teniendo en cuenta que la estructura de los datos en origen ya está optimizada para su uso en BI u OLAP (fact tables y dimensiones), se ha de definir una directiva en cuanto a definir cuadros de mandos:
-	No dejar al cliente un libre uso de las fechas, y definir cuadros de mandos que de partida muestren información interesante para ellos. 
o	Por ejemplo, últimos X años, comparativas anuales etc. 
o	Si aun así los dashboards que solicitan suponen una carga de computación alta (muchos años, variables…), se plantea el uso de “extracts” (más adelante)
-	Si dejamos al cliente libre uso de fechas se han de utilizar como fuentes de datos conexiones a extractos o cubos OLAP.  

Los extracts permiten extraer los datos de una fuente de datos para que la carga de los dashboards sea más rápida. Se almacenan en local y tienen asociada una fuente de datos origen. El problema: según mi experiencia realizando pruebas los extracts no funcionan correctamente y dan problemas. Además, DevExpress no tiene la característica de refrescos incrementales de las fuentes de datos o extracts lo que implicaría que para tener datos actualizados se tendría que recargar completamente el extracto y manualmente, lo cual no es factible.   

Tiempo de extracción para un extract con datos desde 2020 hasta 30/06/2023: 5 minutos 20 segundos.

Cubos OLAP:
Para conectarse a un cubo OLAP se ha de establecer una conexión con la base de datos SSAS. El modo de acceso es únicamente mediante Windows authentication, por lo que en caso de generar dashboards cuya fuente de datos sea un cubo OLAP en producción, se ha de asegurar que el usuario de Windows que está ejecutando Atlas debe ser un usuario del directorio activo. 


---


Herramientas 
Existen multitud de herramientas de business intelligence (BI) en el mercado. En el siguiente cuadrante de Gartner, utilizado como referente en investigación de mercado para la comparación entre empresas, se pueden encontrar las siguientes entidades:
 
Los principales líderes diferenciados del resto son Microsoft (PowerBi) y Salesforce (Tableau). En el presente documento se informa de la arquitectura de diseño para un proyecto de business intelligence en términos generales, apoyándose en las metodologías y practicas tanto de PowerBi como de Tableau, ya que estas poseen una extensa documentación. 
DevExpress vs PowerBi vs Tableau
Se ha investigado también las herramientas proporcionadas por DevExpress, que en este caso serían las Business Intelligence Dashboards, ya que en DBSoft se trabaja con este paquete. Estas herramientas están orientadas a ser utilizadas para incorporar componentes de business intelligence en aplicaciones nativas o web. Es decir, su filosofía difiere en que PowerBi o Tableau son plataformas desarrolladas y enfocadas a que el usuario desarrolle directamente métricas de business intelligence para ser consumido posteriormente en su entorno, mientras que DevExpress otorga herramientas de código que son embebidas en aplicaciones para desarrollar un entorno de business intelligence. Esto implica que PowerBi y Tableau son herramientas “out of the box” orientadas a que el desarrollador cree dashboards de business intelligence para ser consumidos por el usuario final, quien podrá analizar los datos para tomar decisiones de negocio; mientras que DevExpress BI Dashboards son herramientas orientadas a que un primer desarrollador mediante código cree una aplicación de business intelligence para ser consumida por un segundo desarrollador de BI, quien podrá construir en ella esos dashboards. No obstante, ambas herramientas Tableau y PowerBi permiten embeber los dashboards desarrollados en su entorno, en tu aplicación nativa o web a través de sus APIs dedicadas. Ejemplo:
 
Aplicación propia (no Tableau Cloud)
En palabras simples DevExpress se sitúa en una capa más baja desde el punto de vista de arquitectura y código, teniendo que crear el propio entorno de business intelligence y proporcionando un mayor control, a diferencia de PowerBi o Tableau, que entregan este entorno para centrarse en el diseño de KPIS, dashboards y métricas. 
DevExpress no posee un entorno cloud donde se puedan publicar los dashboards, sino que se ha de hostear en la propia infraestructura de DBSoft, creando una aplicación que publique estos dashboards, y desarrollando la lógica de conexiones con bases de datos. 
La documentación disponible para crear elementos de business intelligence con DevExprtess, es significativamente más escasa que para PowerBi o Tableau.
Arquitectura de entornos de BI para Tableau y PowerBi
En una arquitectura de BI hay como mínimo 2 entornos. Por un lado, el entorno de creación (designer) donde se configuran las conexiones a las fuentes de datos, desarrollan métricas y gestiona el esqueleto del proyecto. Por otro lado, el entorno de visualización (viewer) donde se publican las fuentes de datos y los libros de trabajo (UI con dashboards interactivos) y donde se consume el producto final (estructurado en proyectos donde se puede colaborar entre usuarios, visualizar las fuentes de datos originales etc). 
Notas: 
El entorno de visualización también es gestionado por un administrador. 
El producto final también puede ser consumido desde el entorno de creación, pero pierde el propósito de distribuir el business intelligence a más usuarios.



Ejemplo en Tableau:
           

Izquierda Tableau Desktop (entorno creación). Derecha Tableau Cloud (entorno visualización).
Lógica de conexiones
La configuración necesaria para que se pueda desarrollar un proyecto de business intelligence es la siguiente:
Se ha de preparar una fuente de datos con la información deseada; esto pueden ser tablas o vistas recuperadas de una base de datos, ficheros Excel, cubos OLAP, APIS…
Desde el entorno de creación de dashboards en la herramienta de BI se realiza una conexión a la fuente de datos para poder trabajar con un “dataset” (PowerBi) o “data source” (Tableau). El tipo conexión a la base de datos puede ser en “live connection” o generando un “extract”. 
-	“Live connection” implica que la herramienta ejecute queries cada vez que el usuario realiza una acción sobre el dashboard, lo cual permite que los datos estén constantemente actualizados, pero puede suponer problemas de rendimiento. 
-	“Extract connection” implica que la herramienta realiza una copia del set de datos en memoria para trabajar con ellos de forma más eficiente. Al trabajar con extractos se ha de configurar un refresco del extracto para mantener los datos actualizados (la configuración de la conexión a la fuente de datos se mantiene). 

 
Una vez realizada la conexión, se trabaja con la fuente de datos para elaborar los dashboards de forma intuitiva (drag and drop) y pudiendo realizar calculos y funciones complejas, así como utilizar funcionalidades pre-procesadas por el motor interno de los datos como sumas, agregaciones, jerarquias, árboles…
Desde el entorno de creación se publica la fuente de datos al cloud service (Tableau Cloud o PowerBi Service), y con ella viajan las configuraciones de conexión a la fuente de datos original. Si la fuente de datos original es “on-premise” se ha de establecer un puente entre la nube y la fuente de datos en la red privada. Para ello se dispone de Tableau Bridge o PowerBi Gateways, las cuales gestionan la configuración de la conexión y la seguridad, pudiendo programar refrescos de la copia de los datos y manteniendo los datos originales en origen. 

  
Tableau vs PowerBi conexiones cloud -> on-premise data.
Se puede observar que su funcionamiento es similar.
Una vez publicada la fuente de datos y configurados los puentes para el refresco, los dashboards publicados se mantendrán siempre actualizados con los últimos datos disponibles. Es además buena practica al publicar la fuente de datos que se trabaje con esta fuente desde el propio entorno de desarrollo (cambiando la conexión por tanto de entorno_desarrollo -> fuente_datos_original a entorno_desarrollo -> fuente_datos_publicada).

Preprocesamiento de datos: cubos OLAP vs trabajo con sets de datos acotados 
Independientemente de la herramienta escogida, es común que se presenten problemas de rendimiento al analizar tablas con mayor nivel de granularidad, ya que estas contienen un mayor número de registros. En estos casos, cada registro contiene datos específicos de cada dimensión. Por ejemplo, en caso de DBSoft, cada análisis clínico se guarda junto con múltiples variables; el laboratorio, fecha, paciente… conformando una tabla con un elevado número de registros. Por tanto, al realizar directamente una query con un agregado, filtro etc, la consulta es lenta e ineficiente. Por esta razón se necesita hacer un preprocesamiento de datos. Las técnicas de preprocesamiento de datos pueden ser varias, por ejemplo y entre otras:
-	Data reduction: implica hacer subsets de los datos para reducir el número de registros finales. Por ejemplo, reducir la unidad de anális de la tabla a solo contener análisis clínicos de un año en concreto. 
o	Ventajas: Tablas menos pobladas y más rápidas cuando se conoce exactamente la finalidad final de la visualización. 
o	Desventajas: Se pierde granularidad al tener que reducir el filtro de al menos una dimensión, y se disminuye la posibilidad de interactividad y filtrado por parte del usuario final.
-	Data transformation: implica transformar los datos en su estructura o las tablas. Por ejemplo, pasar una dimensión de variable categórica a varias dimensiones cada una representando una nueva columna (pivot de la tabla).
o	Ventajas: Puede reducir el tiempo de carga o estructurar el dataset reduciendo los registros.
o	Desventaja: Si se estructura la información de diferente manera puede llegar a desnormalizarse y dificultar su análisis.
-	Cubos OLAP:
Es un objeto multidimensional generado a partir de una tabla de análisis y distintas tablas de dimensiones de las cuales se ha realizado una pre-agregación y jerarquización de los datos en su procesamiento. El objetivo es mostrar cálculos extensos de los datos en función de la unidad de análisis escogida por el usuario y permitiendo cambiar el nivel de granularidad. 
o	Ventaja: Están optimizados para realizar queries de manera más eficiente, ya que, al generar el cubo, se realizan pre-agregaciones y cálculos entre las dimensiones que permiten posteriormente visualizar la unidad de análisis utilizando estas dimensiones como filtros de forma eficiente y rápida.  
o	Desventaja: pueden ser más complejos de mantener o de configurar, ya que antes de poder visualizar los datos, se ha de saber la estructura que ha de tener el cubo para luego hacer una correcta representación. Por tanto reduce la escalabilidad cuando se tengan que realizar visualizaciones de distinto tipo. Disminuye la capacidad de filtrado y manipulación de campos para realizar nuevas funciones de agregado según convenga en la herramienta de BI. Es decir, se ha de suministrar la unidad de calculo final, en vez de, a libre elección diseñar las medidas desde la herramienta de BI (en caso de utilizar un dataset completo). 
Por tanto al trabajar con sets de datos en una herramienta de BI se ha de tomar la decisión de si se quiere trabajar con “granular data” (mayor numero de registros y flexibilidad) o con “pre-aggregated data” (sets de datos agregados con sum() count() etc).
Ejemplos de los 2 escenarios:
-	Datos en OLAP cubes: Para generar el cubo OLAP se tiene que conocer exactamente las medidas finales que se van a usar en la visualización; por ejemplo, para finalmente visualizar el recuento de análisis clínicos por centro, el centro con el menor número de análisis en una fecha concreta… Para ello se decide, de la tabla de análisis (fact table) cuales son las columnas que se necesitan (dimensiones), y por ende se seleccionan las tablas referenciadas por estas dimensiones, (dimension tables). Se realiza un procesamiento del cubo en el agente proveedor de OLAP, por ejemplo, SQL Server Analysis Services y después se utiliza este cubo como fuente de datos. Se conecta la herramienta de BI al cubo y se construyen los dashboards. Esto permite buena organización de jerarquías entre datos para el análisis, pero al incluir nuevos datos en las tablas los cubos han de procesarse de nuevo y refrescar la conexión al cubo desde la herramienta de BI.

-	Datos granulados sin pre-agregar: La herramienta de BI se conecta directamente a la fuente de datos o se realiza un extracto de la información. Este extracto también se ha de refrescar cuando nuevos datos entran en las tablas originales. Lógicamente lo más eficiente en esta conexión es filtrar de la fuente de datos original la mayor cantidad de datos posibles que no se vayan a utilizar en las visualizaciones. Las herramientas como Tableau o PowerBi al realizar el extracto realizan una agregación en memoria y optimización de la fuente de datos para que a la hora de diseñar el dashboard con el drag and drop, las agregaciones de datos ya estén preprocesadas y sean eficientes. Tableau tiene un motor de datos en memoria diseñado especialmente para la rápida ingesta de datos y procesamiento de queries analíticas llamado Hyper. 

Comparación de las 2 opciones:
Para utilizar un cubo que este actualizado, el cubo tiene que reprocesarse cada vez que entren nuevos datos en las tablas originales, y el extracto generado mediante la conexión desde la herramienta de BI tiene que refrescarse. Por otro lado, si no se usan cubos lo único que hay que refrescar es el extracto mediante la conexión, ya que las herramientas de BI posteriormente hacen el trabajo de agregación y jerarquización en el background con sus motores internos (de la misma forma que hizo el cubo en su preprocesamiento). Esto implica que singularmente, el refresco del extracto conectado a un cubo es más rápido que el refresco de un extracto conectado al set de datos acotados, pero para poder conectarse a un cubo actualizado se ha de haber reprocesado el cubo, por lo que la sumatoria de los 2 tiempos de procesamiento podría acabar siendo mayor que el refresco al set de datos acotados. Finalmente, es complicado determinar que método es más eficiente sin recurrir a la práctica, sin embargo, la utilización de cubos conlleva más pasos manuales.
Recomendaciones:
Realizar pruebas con ambos entornos. 
-	Procesamiento de datos:
o	Utilizando una tabla de análisis y las tablas de las dimensiones, realizar una conexión desde Tableau y construir alguna métrica simple. Programar un extracto y medir tiempos de refresco. 
o	Por otro lado, construir un cubo OLAP de la misma forma (con la tabla de análisis y de dimensiones) y procesarlo. Seguidamente establecer una conexión desde Tableau al cubo y seguir los mismos pasos que anteriormente. 
-	Comparación de herramientas:
o	Realizar las mismas pruebas con DevExpress.




Tabla de equivalencias:


---

El proyecto de Cuadros de mando nace de la necesidad de obtener información de toda la actividad generada en los laboratorios del grupo compañia_z. 
Cada día, desde DBSoft recogemos una amplia gama de datos de todos los centros del grupo, desde analíticas y pruebas realizadas, hasta los tiempos de realización entre otros aspectos clave de la actividad. Posteriormente, gracias a nuestras soluciones de Business Intelligence conseguimos transformar estos datos en información valiosa para el grupo.
El presente proyecto, ya en funcionamiento, está en constante expansión y desarrollo con el objetivo satisfacer las necesidades actuales y futuras de nuestros clientes. Además, en DBSoft nos esforzamos por evolucionar con los desafíos en constante cambio del entorno empresarial.
Con la implementación de nuestra solución, el grupo ahora dispone de herramientas sofisticadas con las que analizar eventos relevantes y tomar mejores decisiones estratégicas fundamentadas.

2.	Cuadros de Mandos

A continuación, se desglosan las principales funcionalidades y opciones de cada uno de los Cuadros de mandos elaborados. 
Debido a la naturaleza de esta solución de Business Intelligence, se informa al lector de que el presente documento abarca únicamente las finalidades principales y no la completa utilidad de los cuadros, ya que su uso es extenso y variado. 
La interacción y el dinamismo de los cuadros, que no pueden ser representados en papel pero si experimentarse mediante el uso de estos, son el núcleo del aporte de valor a la organización.

2.1.	Cuadro de tiempos de respuesta de analíticas

Este cuadro ofrece información del tiempo de respuesta de las analíticas. El tiempo de respuesta se define como el tiempo desde que entra una petición hasta que se finaliza el análisis. De este dato se muestran 4 KPIS, su media, mediana, percentil 75 y percentil 90, con el objetivo de estudiar la eficiencia de trabajo de los laboratorios del grupo.

 

Características y funcionalidades principales

-	Se visualizan estos 4 KPIS tanto para el grupo completo de Quirón, como para los distintos territorios o centros. De esta forma se puede analizar para cualquier KPI:
o	El rendimiento de un territorio determinado con respecto a la media del grupo entero.
o	El rendimiento de un centro determinado con respecto a la media del grupo entero.
o	Comparaciones entre distintos territorios o distintos centros de un mismo territorio.
-	Evolutivo temporal de los 4 KPIS en los meses del periodo para estudiar la evolución mes a mes, tanto de los territorios como de los centros. 
-	Opciones de filtrar por horquilla temporal, tipo de paciente, turno y actividad (laboratorio productivo, referencia o actividad total)

2.2.	Cuadro de tiempos de respuesta de pruebas concretas

Este cuadro ofrece información del tiempo de respuesta para pruebas concretas escogidas por el usuario. Siguiendo la misma filosofía y características que en el cuadro descrito anteriormente (2.1), el usuario puede visualizar los 4KPIS para una prueba en concreto en vez de para una analítica. 
Es decir, el usuario podrá analizar la media, mediana o percentiles 75 y 90 de pruebas tales como la glucosa, troponinai … entre otras.

 


Características y funcionalidades principales

Este cuadro abarca la misma funcionalidad y características que el cuadro 2.1 con el añadido de la selección de pruebas concretas.

2.3.	Cuadro de actividad de laboratorios

Este cuadro ofrece información del número de analíticas, determinaciones solicitadas, realizadas y en referencia, con el objetivo de estudiar el volumen de actividad de los laboratorios del grupo.


 


Características y funcionalidades principales


-	La parte izquierda del cuadro (izquierda de la barra azul) ofrece información del rendimiento del año actual vs el año anterior. Se puede observar este rendimiento a nivel de grupo completo de Quirón, o profundizar a los distintos territorios y centros.
-	La parte de la derecha ofrece información general en la horquilla de tiempo seleccionada. En los filtros se selecciona si se desea ver información para analíticas o determinaciones de cualquier tipo. En consecuencia, el cuadro ofrece información del volumen total de lo seleccionado, el reparto según el tipo de paciente, el turno, el territorio o el centro en concreto.
-	Se puede analizar cómo ha variado el volumen de actividad mes a mes según el turno.
-	Se puede analizar del reparto de la actividad según el tipo de paciente para territorios o centros concretos.
-	Se puede comparar el volumen de actividad entre territorios o centros de un mismo territorio.
2.4.	Cuadro de procedencia de análisis

Este cuadro ofrece información del tráfico de analíticas o determinaciones entre centros y territorios, permitiendo analizar entre otras cosas cuantos análisis ha enviado un centro a otro o una combinación de centros a otros, así como territorios.


 


Características y funcionalidades principales

-	Se muestran KPIS a nivel de grupo completo de compañia_z de envíos entre centros (parte superior derecha).
-	Se puede analizar el reparto según el turno en destino (en que porcentaje de mañana tarde o noche llegan los análisis que se reciben de otros centros).
-	Se puede analizar mediante tabulación cruzada envíos y recepciones de analíticas según el centro de origen y destino con la tabla de la parte central del cuadro.
-	Se puede analizar la evolución temporal mes a mes de cómo han sido esos envíos entre centros. 












2.5.	Cuadro de volumen de actividad por pruebas 

Este cuadro ofrece información del número de pruebas que realiza el grupo, diferenciando según el tipo de prueba, con el objetivo de estudiar el volumen de actividad sobre pruebas concretas de los distintos laboratorios del grupo.

 

Características y funcionalidades principales

-	Ofrece información a nivel general (grupo) del número de determinaciones según el tipo de prueba, así como su evolutivo y picos de mayor y menor actividad.
-	La parte inferior izquierda del cuadro contiene información relativa a territorios y la derecha a laboratorios. 
-	Se puede analizar la actividad mensual por cada territorio y por cada laboratorio, así como picos y fluctuaciones.
-	Se puede analizar el reparto de actividad por laboratorio dentro de un territorio común (por ejemplo, dentro de los públicos de Madrid, que laboratorio realiza más glucosas, en que proporción y como se distribuyen en el tiempo).


---



1.	Ámbito:
Este documento abarca tanto la documentación, como la metodología necesaria para la realización de una integración completa entre 2 laboratorios, dentro del ámbito de anatomía patológica. Esta integración contempla varios circuitos, como son el de recepción de solicitud (con o sin resultados ya observados por el emisor) (compañia_cl - compañia_at), recepción de tubos y generación del caso (compañia_at), envío de resultados (compañia_at - compañia_cl), petición de material extra (compañia_at - compañia_cl) y recepción de material extra (compañia_cl - compañia_at). Esto hace que, pese a que todas las integraciones difieran en aspectos concretos, pueda servir de ayuda al afrontar nuevos desarrollos. Con este documento se pretende: 
-	Aportar valor al área de integraciones teniendo guías de referencia estructuradas.
-	Escalabilidad en el desarrollo de negocio mejorando la adaptación de gente nueva en el equipo de desarrollo.
-	Agilizar la gestión de proyectos, uniendo el área funcional con el área técnica.
-	Impulsar la eficiencia y productividad al afrontar nuevos desarrollos.
2.	Contexto: 
Los centros integrados son compañia_at (gestionado por DbSoft /Atlas) y compañia_cl (gestionado por Dedalus / PatWin). El contexto de la integración es el siguiente: compañia_cl tiene que realizar estudios de anatomía patológica para los cuales no tiene suficiente capacidad, por ello externaliza parte del trabajo y lo deriva a compañia_at, quienes se encargarán de realizar el estudio completo si el estudio aun no ha comenzado en compañia_cl, o complementarlo en caso de que ciertas pruebas ya hayan sido realizadas, en cuyo caso estas se recibirán como dato de entrada en la preanalítica. El envío de resultados ha de contener todos los datos relevantes, incluidos, si los hubiese, los recibidos en preanalítica. Para poder realizar cualquier integración, es necesario seguir la documentación pactada que la describe. Esta documentación se encuentra en el anexo de este documento y deberá usarse como guía de referencia.
3.	Conceptos:
Para entender los conceptos de anatomía patológica en profundidad, lo más conveniente es realizar una investigación y contactar con expertos dentro de la compañía, ya que la terminología puede ser muy extensa. No obstante, los conceptos básicos necesarios para entender una integración de este estilo son los siguientes: 
-	Estudio / derivación / solicitud / petición: Se refiere a cada caso individual en el que trabaja el centro. Este estudio es el documento / mensaje completo y contiene toda la información acerca del paciente, el médico, los patólogos, las pruebas a realizar, las muestras…
-	Muestras: Son los botes que contienen el elemento físico que se va a analizar. Para entenderlo podría ser por ejemplo un trozo de un pulmón.
-	Bloques: Son particiones que se hacen sobre las muestras. Es decir, el trozo de pulmón podrían dividirlo en varios bloques.
-	Laminas: De nuevo son particiones de un bloque en concreto, cortados de forma delgada y a las que se les aplica una serie de técnicas. Estas técnicas pueden ser por ejemplo técnicas de tinción, las cuales sirven al patólogo para diagnosticar resultados.
-	Tipo de caso / perfil: Se trata del tipo de estudio que se le hace a una muestra. Puede ser por ejemplo una biopsia, una citología…
-	Pruebas: Son las distintas pruebas que se realizan a una muestra. En compañia_at, las pruebas se dividen en macro (Macr), micro (Micr), diagnostico (Diag), tipo de muestra (TMues)…
4.	Flujo de operaciones y lógica 

El proceso de integración completo se puede simplificar en 3 partes fundamentales. La recepción y preanalítica, la generación del caso, y el envío de resultados. En el caso de esta integración hay dos circuitos más, correspondientes a la petición y recepción de láminas adicionales. El siguiente modelo de procesos de integración, representa el flujo de operaciones pertinente.

  

4.1 Recepción y preanalítica
 
4.2 Generación del caso
 
4.3 Petición de lámina

 
4.4 Envío de resultados
 


Todos los procedimientos de esta integración están comentados a nivel de código para facilitar la comprensión de cada paso. Por esa razón, las siguientes explicaciones no abarcan explicaciones detalladas, sino que describen el proceso funcional. Para entender los detalles se recomienda seguir el código con sus correspondientes comentarios. 

4.1 Recepción y preanalítica 

Los procedimientos correspondientes a esta parte de la integración son los siguientes (ordenados por orden de ejecución):
-	compañia_cl_MensajeHL7InsertaMensajeCompleto
-	Importaciones_Procesado_compañia_cl
o	Importaciones_BuscarEnRegistro
o	Imprtaciones_ParseaHL7
o	Importaciones_BuscarPruebaOGrupo

En primer lugar, se recibe el mensaje a través del Mirth, en el cual se han de configurar los canales necesarios con la IP y el puerto haciendo de listener. 
Desde el Mirth se invoca al procedimiento compañia_cl_MensajeHL7InsertaMensajeCompleto al cual se le pasa el mensaje completo. Este procedimiento hace inserts en tablas claves de la base de datos, como descrito anteriormente. Finalmente se invoca a Importaciones_Procesado_compañia_cl.
En Importaciones_Procesado_compañia_cl primero se comprueba de que tipo de mensaje se trata ya que pueden enviar por este canal tanto derivaciones, como ACK, cancelaciones, actualizaciones o respuestas a peticiones de láminas. Dependiendo de que caso se trate, se gestiona de una forma u otra. 
En caso de ser una respuesta a una lámina solicitada, se ha de actualizar la tabla Preanalitica_AP_Peiticiones y AP_Peticiones para indicar si la técnica ha sido aceptada o no , y en caso de que si, grabar el ID asignado por compañia_cl. 
En caso de ser una cancelación se ha de comprobar que no se haya dado de alta el caso y se esté trabajando ya en él, ya que bajo estas circunstancias no sería posible cancelar la petición. 
Si se trata de una derivación se han de extraer todos los datos necesarios para completar las tablas clave de la preanalítica. Estas extracciones de datos se hacen usando tablas temporales en las que se pueden estructurar los datos de la forma correcta antes de insertarlos en sus correspondientes tablas. Ejemplo concreto de esta integración: para poder gestionar las muestras bloques y laminas, primero se han de identificar los tramos en los que viene la información principal de cada elemento, en este caso en los SPM. Con estos datos se puede hacer una tabla padre que contiene las cabeceras y que se referencian entre ellos por orden de jerarquía, por ejemplo, un bloque cuelga de su muestra correspondiente y una lámina cuelga de su bloque correspondiente. A su vez se ha de extraer la información de los OBX, los cuales contienen información más específica de cada elemento. De la misma manera se encuentra la forma de ligar cada OBX a su correspondiente elemento a través de una tabla hija. Este es uno de los varios ejemplos de la lógica que hay que diseñar para transformar los datos y gestionarlos correctamente. 

A parte de recoger información de los elementos principales, es necesario también identificar el tipo de caso del que se trata y generar las pruebas correspondientes. Esto se hace a través del tipo de muestra, la cual mediante el mapeo correspondiente y el procedimiento Importaciones_BuscarPruebaOGrupo va a determinar el tipo de perfil (e.g. BIOP,CITV…), y que posteriormente generará una serie de pruebas (e.g. BIOPDiag, BIOPMacr, BIOPMicr…).
El procedimiento acaba una vez se haya introducido todo lo necesario en todas las tablas de preanalítica, lo que permite dejar la derivación lista para una vez se reciban los botes físicos, generar el caso en producción. Las tablas relevantes de esta integración y un pequeño resumen se muestran más adelante.

4.2 Generación del caso

Los procedimientos correspondientes a esta parte de la integración son los siguientes (ordenados por orden de ejecución):
-	compañia_cl_RecepcionTubos
o	Valde_LaboratorioDeReferencia

Para la generación del caso es necesario montar el procedimiento de recepción de tubos. Este se terminará ejecutando cuando se escanee una referencia desde el laboratorio al haber recibido los botes físicamente. Este procedimiento recibe esta referencia y el número de petición del HIS entre otros datos, con los cuales se hacen las comprobaciones necesarias para evitar asignar referencias repetidas o dar de alta un caso ya en producción. A continuación, se actualiza la referencia en preanalítica y se ejecuta el procedimiento Valde_LaboratorioDeReferencia, que gracias a la referencia se encarga de recoger de la preanalítica todos los datos necesarios para generar el caso. Este procedimiento creará los numeradores pero sin embargo no crea ni bloques ni cristales, por lo que hay que crearlos manualmente. Además se han de vincular correctamente las estructuras de preanalítica con las de producción para tener referenciados los identificadores que utilizan en compañia_cl vs los que utilizan en compañia_at para referirse a un mismo elemento (ya sea una muestra, un bloque o una lámina). 

4.3 Petición de lámina

Los procedimientos correspondientes a esta parte de la integración son los siguientes (ordenados por orden de ejecución):
-	compañia_cl_Peticion_Tecnica

Nótese que este procedimiento se lanza desde el trigger Insert_Ap_Peticiones_Particular, en el cual se ha configurado que se identifique si la petición insertada corresponde a un caso de compañia_cl, y si el bloque sobre el que se hace estaba en preanalítica. Cuando estos dos casos se cumplen, se puede realizar la petición y por tanto se llama al procedimiento. Nótese también (visible en el modelo de procesos) que cada acción es repetida para cada inserción de lámina nueva en un bucle, ya que pueden insertarse varias a la vez desde la aplicación. 
El procedimiento recupera los datos necesarios para generar un mensaje y lo introduce en la tabla MensajeHL7 con el analizador correspondiente (27) para que posteriormente se realice el envío.
4.3 Envío de resultados

Los procedimientos correspondientes a esta parte de la integración son los siguientes (ordenados por orden de ejecución):
-	Valde_Envia_Resultados_compañia_cl
o	Valde_NotificaResultados_compañia_cl
El primer procedimiento se ejecuta mediante una tarea programada que ha de ser configurada. Esta tarea programada ejecuta el primer procedimiento cada cierto tiempo. El procedimiento recoge los casos (códigos de control C_Control) que han sido emitidos, pero no enviados todavía y los introduce en una tabla temporal que usa el segundo procedimiento. Este segundo procedimiento genera un mensaje para cada C_Control mediante un bucle.
Para enviar de vuelta los resultados es importante adherirse a la documentación ya que muchos de los identificadores que se utilizan en compañia_at difieren de los que se usan en compañia_cl, por lo que se han de mapear de vuelta y generar las tramas correspondientes y en el orden indicado. Para extraer valores de los resultados se utilizan las vistas preparadas para ello:

-	VIND_AP_SrvCliCodificacion_Todas_Base
-	VIND_AP_SrvCliCodificacion
-	VIND_AP_SrvCliCodificacion_Base
-	VIND_AP_SrvCliComentario
-	VIND_AP_SrvCliComentario_Base
Una vez montado el mensaje, este se introduce en la tabla mensajehl7 con el analizador correspondiente (28)
Nota: La tabla MensajeHL7 es consultada desde el Mirth continuamente para enviar resultados o peticiones de técnicas cuando es necesario. Esto lo hace ejecutando un procedimiento de la base de datos cada cierto tiempo (ParticularidadesCentros_RecuperaResultadosCasiopea). Este procedimiento identifica en la tabla MensajeHL7 los mensajes que no tienen aun fecha de procesado, y mediante el analizador indicado, se devuelve el mensaje específico al Mirth parar que se envíe.

Mapeos
En algunos casos, como es en el de esta integración se han de realizar una serie de mapeos entre valores de un laboratorio y otro. Para ello, el cliente en este caso facilitó un listado de sus códigos, que tuvieron que ser correlacionados con los de compañia_at, para posteriormente cargarlos en las tablas correspondientes en base de datos. En el caso de esta integración se tuvieron que gestionar los siguientes mapeos:
-	Mapeo en ap_analizadores_pruebas de técnicas compañia_cl -> técnicas en compañia_at 
o	(e.g HEE_EXT)->(E.G HEE)
-	Mapeo en importaciones_pruebas de tipo de muestra compañia_cl -> generación de caso en compañia_at: 
o	(e.g. 1100)-> (e.g BIOP)
-	Mapeo en integracion_mapeos de tipo de muestra compañia_cl ->  tipo de muestra en compañia_at: 
o	(e.g. 1100)->(e.g 1010101)
-	Mapeo en integracion_mapeos de tipo de prueba compañia_cl ->  tipo de prueba en compañia_at: 
o	(e.g. DIAGNOSTICO)->(e.g Diag)
-	Carga de SNOMED: carga en RESCODI de todos los códigos ausentes.
5.	 Tablas y descripción 

Algunas de las tablas principales comunes a cualquier integracion pueden encontrase en la imagen inferior:

 

Y algunas de las tablas principales de esta integración específica, y su correspondencia con tablas comunes:

 

El contenido de algunas de las tablas fundamentales de la integración:
-	MensajeHl7: Cada entrada corresponde a un único mensaje hl7 individual, identificado con el analizador para distinguir de que se trata (e.g. 26 corresponde a los mensajes que deriva compañia_cl a compañia_at, 27 son peticiones de lámina desde compañia_at a compañia_cl, 28 son envío de resultados desde compañia_at a compañia_cl).
-	MensajeHl7Detalle: Cada entrada es una trama individual del mensaje, todas vinculadas por FK (CA_MensajeHL7) a mensajehl7 (C_MensajeHL7).
-	compañia_cl_Peticion: Cada entrada corresponde a una derivación. En esta tabla se puede recoger cualquier información útil de la petición.
-	SrvCli: Cada entrada corresponde a un caso (PK: C_Control). Esta es la tabla más importante en producción ya que contiene los casos sobre los que se trabaja. 
-	PruCli: Cada entrada corresponde a una prueba individual del caso. Todas las pruebas están vinculadas a un C_Control. 
-	Prueba: Cada entrada corresponde a un tipo de prueba de referencia en compañia_at.
-	Comentario: Cada entrada corresponde a una prueba individual, para la cual se necesitaba hacer una descripción más extensa.
-	PruCli_Numerador: Cada entrada corresponde a la vinculación entre una prueba y su numerador correspondiente (el numerador identifica al número de la muestra).
-	Preanalitica_Clientes: Cada entrada corresponde a un cliente individual en preanalítica 
-	Preanalitica_Pruebas: Cada entrada corresponde a una prueba individual, todas vinculadas por FK (CA_Preanalitica) a Preanalitica_Clientes (C_Preanalitica).
-	Pendiente_Resultado: Cada entrada corresponde a una prueba individual que ya venía con resultados en la preanalítica.
-	Preanalitica_Ap_Muestra: Cada entrada corresponde a una muestra individual en preanalítica.Cada muestra se vincula con un caso en preanalítica: por FK (CA_Preanalitica) a Preanalitica_Clientes (C_Preanalitica).
-	Preanalitica_Ap_Bloque: Cada entrada corresponde a un bloque individual en preanalítica. Cada bloque se vincula a una muestra en preanalítica: por FK (CA_Preanalitica_Muestra) a Preanalitica_Ap_Muestra (C_Preanalitica_Muestra).
-	Preanalitica_Ap_Peticiones: Cada entrada corresponde a una técnica individual en preanalítica. Cada técnica / cristal se vincula a un bloque en preanalítica: por FK (CA_Preanalitica_Bloque) a Preanalitica_Ap_Bloque (C_Preanalitica_Bloque)
-	Importaciones_Pruebas: Cada entrada es un mapeo del código de la muestra al tipo de perfil de caso generado (e.g. muestra con id: 1214 genera una BIOP*)
-	Integracion_Mapeos: Cada entrada es un mapeo entre 2 valores y puede ser usada para mapear tipos de muestra, nombres de pruebas… (e.g. MACRO (compañia_cl) -> Dmacr (compañia_at))

6.	Metodología de trabajo

La metodología de trabajo se basa en establecer una comunicación fluida entre los integrantes del proyecto, que permita unir el área funcional con el área técnica. De esta manera se reducen los errores en tiempo de desarrollo y se agiliza la puesta en marcha. Por otra parte, será igual de importante establecer caneles de comunicación con los clientes para canalizar el desarrollo, y siempre estar en línea con los objetivos de ambas partes. 
Es importante cuando se dispone de documentación, estudiarla y resaltar cualquier duda o error, ya que en proyectos de este estilo es común que ciertos aspectos hayan quedado sin resolver a priori, o cambien durante el desarrollo. Se recomienda también solicitar mensajes de prueba al cliente para trabajar con datos concretos y poder hacer testing continuo. 
Por último, es también importante documentar el código para su futura comprensión y facilitar la colaboración entre el equipo. 



---

Esta es una propuesta escrita por mi:

El presente documento informa de una actualización del proyecto a realizar entre las partes, Jorge Domínguez-Sol (desarrollador) y compañia_X-compañia_y. El desarrollador plantea un cambio en el desarrollo del proyecto para adaptarse a las necesidades del compañia_X-compañia_y, en cuanto a optimizar tiempos de desarrollo, costes de implementación y mantenimiento futuro.
Para ello, tras investigar varias opciones, se plantea una nueva solución que conlleva la simplificación del proyecto. El proyecto cambiará para pasar de ser una aplicación propietaria, a una solución más estandarizada, reduciendo la dependencia de código propio y utilizando herramientas de mercado ya desarrolladas (SaaS). Por tanto el nuevo proyecto consistirá en que el desarrollador prestará su servicio para diseñar e implementar la base de datos, el módulo de preprocesamiento para procesar los archivos de entrada de compañia_y, y configurar las herramientas SaaS e integrarlas con la solución buscada, diseñando los algoritmos de las métricas e implementándolas para su correcta visualización en Tableau.
La simplificación del proyecto implica numerosas ventajas sobre la solución inicial planteada:
	Ahorro de tiempo: La nueva solución permite reducir la ejecución del proyecto en 8 semanas permitiendo la entrega del mismo antes del 31/12/2023 según solicitaba el compañia_X-compañia_y. (Bajo la hipótesis de que se comience el proyecto a comienzos del mes de mayo). 
	Ahorro de costes: Se reducirá el coste final del proyecto en 10.000 €. A demás se aplica esta reducción sobre la reducción ya hablada el día 17/04/2022. 
	Menor total cost of ownership  y coste de mantenimiento: Menor coste de servidores, licencias y labor de mantenimiento de código y de hosting. 
	Mayor facilidad de uso y acceso: Con la nueva solución se podrá ir incrementando el número de usuarios para visualizar los dashboards y métricas, en base a lo que se vaya necesitando ampliando la licencia del SaaS. 
	Propiedad intelectual: Al cambiar de una aplicación propietaria a una solución estandarizada y uso de licencias SaaS, el compañia_X-compañia_y podrá mantener la integridad de la propiedad intelectual. En este sentido, la base de datos y el módulo de procesamiento desarrollados pertenecerán completamente al compañia_X-compañia_y. De la misma forma, las licencias del SaaS mantenidas por el compañia_X-compañia_y para poder acceder a la herramienta de visualización de métricas serán propiedad del compañia_X-compañia_y (usuarios de administración o consulta). El desarrollador aportará sus servicios para diseñar, gestionar e implementar todo lo necesario. 
	Documentación y soporte: Se elimina la dependencia del conocimiento del código propio de la aplicación, ya que se pasa a utilizar herramientas estándares y conocidas en el mundo IT, sobre las cuales existe documentación y soporte. 
	Simplificación hosting: Se simplifica el hosting de la aplicación de métricas, quedando gestionado completamente por la solución SaaS propuesta. 
	Autenticación y seguridad: Se elimina la necesidad de implementar métodos de autenticación y seguridad extras, ya que esto lo gestiona también el SaaS. 
Esta solución conlleva más trabajo para el desarrollador en la fase de gestión del SaaS pero también reduce carga de trabajo del desarrollo de la aplicación propia, por lo que simplifica el proyecto y planea un escenario win-win tanto para el compañia_X-compañia_y como para el desarrollador. 

Fases del proyecto

Las nuevas fases actualizadas del proyecto son las siguientes.
	Configuración de la base de datos (7 semanas)
	Conocimiento de la estructura /arquitectura base de datos. 
	Trabajo conjunto con personal del compañia_X.
	Necesidades, conocimiento de: 
	Tablas: Tipos de datos albergados, significado de los campos
	Procedimientos almacenados
	Triggers
	Tareas programadas
	Revisión de arquitectura actual para evaluar posibles cambios o mejoras 
	Se ha de hacer analizando las métricas
	Diseño de la base de datos en MySQL
	Volcado de base de datos con ficheros antiguos 
	Testing: extracción de datos con consultas manuales. compañia_X está presente para la comparación con extracciones anteriores 

	Módulo de preprocesamiento (5 semanas)
	Algoritmo de lectura de ficheros 
	2 algoritmos diferentes: compañia_y manda los archivos de manera distinta
	(A futuro se ha de intentar pactar con compañia_y el envío de datos en formato estándar y consistente)
	Testing: Carga en base de datos mediante ejecución de los algoritmos. compañia_X está presente para verificar que la carga es correcta 

	Diseño de algoritmos de las métricas y representación gráfica (7 semanas)
	Para cada métrica se implementa el código, y se diseña y despliega la representación gráfica.
	Testing: Se hará el testing 1 por 1 para verificar que la salida de datos es la esperada. compañia_X está presente para alinear objetivos en la visualización de las métricas




	Integración del módulo de procesamiento en el backend API (5 semanas)
	Configuraciones internas y funcionalidades relacionadas con backend y algoritmo de lectura de ficheros.
	Testing: No será necesario que compañia_X esté presente, pero podrá estarlo si así lo desea.

	Testing (2 semanas)
	Gracias a la metodología agile, el testing de las fases es continuo por lo que se estima que el testing final sea 

Total implantación: 26 semanas 

Elementos del proyecto

Módulo de preprocesamiento:
Abarcará la lógica necesaria para procesar los datos que facilita compañia_y al sindicato, de tal forma que puedan ser introducidos en la base de datos. Este módulo se construirá de tal forma que, si en un futuro compañia_y decidiese cambiar el formato de entrega de los datos, se puedan realizar los cambios necesarios para adaptarse a este nuevo formato y que el resto de la aplicación y arquitectura de base de datos no se vean afectados. Esto proporciona escalabilidad a la solución, haciéndola además más flexible y reduciendo riesgos derivados de la dependencia de terceros.

Sistema de gestión de base de datos:
Se realizará el montaje de una base de datos relacional, diseñando la estructura y los modelos entidad relación, junto con los procedimientos almacenados necesarios para gestionar los datos. Este apartado contempla el almacenamiento y gestión de los datos, para disponer de una fuente de información actualizada y configurada para establecer las conexiones necesarias con la herramienta de visualización de métricas.  

Análisis descriptivo, “dashboards” y métricas:
Se diseñará e implementarán métricas y dashboards mediante la herramienta SaaS que permitan al compañia_X-compañia_y analizar los datos. La siguiente imagen muestra una maqueta de ejemplo (nótese que esto es simplemente un ejemplo elaborado por el diseñador que no tiene por qué coincidir con el módulo final).
 
Ilustración 1. Maqueta del módulo de visualización

Tecnologías:
Las tecnologías descritas son susceptibles a cambios bajo criterio del desarrollador.
	Motor de gestión de base de datos: MySQL
	Módulo de preprocesamiento: Programado en Java y utilizando si fuera necesario Spark, streams y otras técnicas de functional programming.
	Metricas, dashboards y visualización de datos: Tableau.
	Control de versiones: GIT.
	Control de dependencias y configuraciones de proyecto: Maven.

Modelo de trabajo y ámbito de funcionamiento:

El desarrollador prestará sus servicios para implementar las tecnologías descritas, entregando finalmente la base de datos, el módulo de preprocesamiento y los dashboards de Tableau configurados y listos para ser visualizados desde la herramienta. La metodología de trabajo se basará en un modelo Agile. Gracias a este modelo de trabajo, el desarrollador podrá ir realizando entregas parciales que añadan valor al cliente, buscando un entorno colaborativo, en el que el cliente se  se compromete a facilitar toda la información necesaria para completar exitosamente el proyecto. Esto permitirá un testing continuo para comprobar que el desarrollo sigue en línea con los objetivos del proyecto. 
Será fundamental la comunicación entre el área técnica y área funcional, para la cual se establecerán los canales de comunicación oportunos acordados entre cliente y desarrollador. 
De acuerdo con lo hablado en la reunión el día 17/04/2023 , el compañia_X-compañia_y pondrá recursos para la ayuda en la implementación del proyecto. Los recursos mencionados son estudiantes de matemáticas que podrán ayudar en la elaboración de los algoritmos, y personal interno para ayudar al desarrollador a entender el significado de los códigos, programaciones de vuelos y términos desconocidos. El compañia_X-compañia_y se compromete a trabajar conjuntamente con el desarrollador cuando este lo necesite, para alinear objetivos e implementar correctamente la solución. Tras la reunión citada anteriormente, el compañia_X-compañia_y también alega dar prioridad al desarrollador de este proyecto para futuros desarrollos y mantenimiento.

Propiedad intelectual y licencias

En la nueva solución propuesta, el desarrollador presta sus servicios para configurar los elementos necesarios para la disposición de las métricas. Por tanto el compañia_X-compañia_y mantiene toda la propiedad intelectual, que consiste en ser propietario de la base de datos, el modulo de preprocesamiento y las licencias de la herramienta Tableau, dentro de la cual se configurarán todas las métricas, dashboards y usuarios para acceder a ellas.  
El compañia_X-compañia_y será responsable del mantenimiento de las licencias necesarias para mantener el software operativo, así como del hardware necesario para su funcionamiento. 
La inclusión de nuevas métricas, KPIs, dashboards y funcionalidades de la aplicación se consideran desarrollos futuros (ver mantenimiento en aspecto económico).

Aspecto económico y mantenimiento

Tras la reunión mantenida el 17/04/2023, se redujo el monto total del coste del proyecto de X € a X €. Además en beneficio del compañia_X-compañia_y se ha aumentado el número de métricas para un total de 15-20, para las cuales se ha acordado la posibilidad de revisar y ajustar el coste dependiendo de la dificultad y tiempo de desarrollo de implementarlas. Además, esta actualización del proyecto conlleva una reducción de X € adicionales sobre esta primera disminución. El coste final del proyecto:

Prestaciones	Número de métricas	Monto total
Todos los servicios citados	15-20	X €

Quedan excluidos de estos costes, todos los costes secundarios que se puedan originar, los cuales se facturaran a parte y siempre con previa autorización del compañia_X-compañia_y.
Costes de mantenimiento:
Los costes de mantenimiento contemplan únicamente el pago de licencias de Tableau, ya que el motor de gestión de base de datos MySQL es de código abierto y el módulo de preprocesamiento se desarrollará  en Java, también de código abierto. 
El coste de las licencias de Tableau es el siguiente:
 
Se ha de necesitar como mínimo una licencia de creador para poder desarrollar , implementar e integrar las métricas (840 $/(año*licencia)). Adicionalmente se pueden añadir usuarios para visualizar estas métricas con sus propias cuentas desde un buscador web accediendo a la plataforma (180 $/(año*licencia)).
Ejemplo práctico: 
El compañia_X-compañia_y contrata 1 licencia de creator para poder desarrollar métricas (e.g. cuenta de Jorge) y 3 licencias de viewer (e.g. cuentas de persona_s, persona_k y persona_w). Esto implica que el compañia_X-compañia_y es propietario de 4 cuentas diferentes que puede usar para acceder a la plataforma y desarrollar metricas (en caso de creator) o visualizar e interactuar con ellas (con cualquiera de las 4 cuentas). 
Este ejemplo supondría un coste anual de 1.380 €.

El coste para mantenimiento o desarrollos futuros correspondiente al desarrollador podrá ajustarse en función de las necesidades del compañia_X-compañia_y, pudiendo escoger entre 2 modelos; facturación por horas en función de la demanda, o cuota mensual para mayor disponibilidad. Ya que aún se desconoce el volumen de trabajo futuro que el compañia_X-compañia_y pueda necesitar, el desarrollador recomienda que en el futuro se comience con la facturación por horas para no generar costes adicionales. En caso de necesitarse una cuota mensual, se podrá cambiar la manera de pago de manera flexible, es decir la elección no es definitiva (siempre con mutuo acuerdo).
Esto cubriría la configuración de la herramienta para características adicionales, desarrollos de nuevas métricas, arreglo de errores … 
El precio de estos servicios será 50 €/hora. Se ofrecerá al compañia_X-compañia_y una oferta de reducción del precio al coger bloques de 8 horas, resultando en un total de X€/hora.
Notas a nivel informativo 
Coste de hosting:
El hosting en la nube de la base de datos no se contempla en este proyecto, ya que se realizará el despliegue de esta en local puesto que no es necesario para la solución planteada. Aun así sería posible en un futuro migrar la base de datos a la nube, y por petición del compañia_X-compañia_y se han investigado los costes del hosting. Existen múltiples compañías que permiten realizar esto y el coste varía en función de diferentes variables. Por ejemplo Azure database for MySQL de Microsoft, tiene un free plan de 12 meses y luego se paga en modo pay as you go, dependiendo tanto del tamaño de la base de datos y la cantidad de espacio que se necesite como de la capacidad de computación, CPUS y RAM. Existen cientos de opciones para estos servicios a parte de Microsoft, por ejemplo Amazon RDS o Google Cloud SQL. El coste de los servicios no es trivial ni estándar ya que depende de la necesidad de cada cliente por lo que en caso de que en un futuro se quisiese migrar la base de datos a la nube se debería realizar un estudio. La mayoría de servicios gestionados de bases de datos empiezan en el entorno de 130 € / mes, pero como mencionado anteriormente hay muchas variables que pueden hacer que este precio varíe. Un punto positivo de estos servicios es que permiten la escalabilidad vertical sin afectar a la base de datos, pudiendo así aumentar los recursos de los servidores. 

Los servicios que el desarrollador lleva a cabo en este proyecto son los siguientes:
	Desarrollo: 

	Investigación, diseño e implementación 
	Módulo de preprocesamiento
	Modelos relacionales, arquitectura y diseño de base de datos 
	Gestión del motor de base de datos
	Integración de tecnologías y conexiones (Tableau, MySQL, modulo preprocesamiento)
	Ingeniería de datos y diseño de métricas 
	Diseño e implementación de algoritmos 
	Diseño e implementación de dashboards
	Configuración de Tableau
	Proceso de testing 

	Consultoría: Contempla los costes derivados del servicio de consultoría que ofrezca el desarrollador al cliente y que engloban aspectos como: guía en el desarrollo y la implementación, gestión y dirección del proyecto, uso de tecnologías…


---

Estos son algunos posts escritos por mi:


Emprendimiento, riesgo y dinero.

¿Que es emprender? ¿Tener una idea brillante, un producto disruptivo, ofrecer un servicio…?

No hay una única respuesta, pero si un resultado claro, el aprendizaje y la experiencia. 
No te cierres a una única opción, ¡explóralas todas! La fórmula depende de cada uno, y encontrarla forma parte del camino.

Trabaja con empresas y con sus equipos, aprende de ellos, entiende las necesidades de un cliente y resuelve sus problemas implementando soluciones. Con esto ganarás experiencia y dinero. Además formarás relaciones claves y abrirás la puerta a grandes oportunidades. Bajo mi visión, esto que acabo de decir es de lo que va el mundo de los negocios.

Te harás muy bueno en algo y te enseñará a negociar, vender y gestionar tus finanzas. Posiblemente también tengas la oportunidad de dirigir equipos, formar a gente o subcontratar servicios, lo que te brindará habilidades sociales clave. Además conocerás aspectos legales, mercantiles y fiscales.

Entonces, está claro ¿no? Quizá no tanto… 

En mi opinión el mayor debate entre las formas de emprender está en la escalabilidad de un negocio, donde se juntan el riesgo y el dinero. Lo que acabo de contar más arriba nace de ofrecer servicios a empresas, que dentro de todo lo bueno que aporta, tiene una limitación, tu tiempo. 

Hablemos entonces de otros modelos de negocio en donde el crecimiento futuro no está estrechamente limitado por tu tiempo, por ejemplo crear una startup o un producto. 

Aquí vas a aprender a analizar el mercado y la competencia, el desarrollo de negocio... Vas a tener que tocar todos los pilares y hacer de todo, lo cual no es posible cuando eres especialista en algo.

Porque aunque des servicios profesionales a nivel estratégico, a la hora de tener un producto, lo más probable es que inicialmente tengas que realizar también tareas a nivel operacional (programar etc, depende de tu sector). 

Vas a ser dueño de una solución a la que, en mayor medida que en la consultoría o servicios profesionales, se adaptan tus clientes a tí, en vez de a la inversa. 

Ah pues suena incluso mejor ¿no?
Espera...

Ten en cuenta que tendrás que invertir tu tiempo para crear tú tu propio producto, sin cobrar y con el riesgo de que las cosas no vayan como esperabas. 

Es posible que nunca obtengas un beneficio económico a cambio, de hecho el 90% de las startups fracasan.

¿Y como lo harías sin haber trabajado con empresas en un mercado con entornos reales en producción? ¿O sin entender las necesidades, los nichos e incluso las dinámicas de trabajo? A lo mejor entonces te identificas mejor con el primer camino...

Encontrar la fórmula es parte del camino y no hay una respuesta única , ¡explora, atrévete y aprende!

---

Educación financiera y mentalidad positiva.

Si nunca te has educado financieramente, ¡es momento de empezar! 

Ya sea leyendo libros, artículos, viendo vídeos..., lo que sea, pero con el objetivo de entender como funciona el dinero. Además por lo que yo he podido experimentar, formarte en esto, no solo va a ayudarte económicamente, también va a hacer que aprendas sobre psicología aplicable a varios ámbitos. 

Si tienes curiosidad por como funciona la mente humana, el comportamiento de las personas, los hábitos y las perspectivas de cada uno en este mundo, estoy seguro que será un tema que te interese.

Mucha gente ve el dinero como un tema tabú, y en mi opinión no debería serlo, hay mucho detrás de la psicología financiera.

Si quieres empezar te recomiendo estos 3 de los libros más básicos que hay y que a mí me han parecido agradables de leer. Y si ya sabes del tema, aún así no dejes de leer "Secretos de la mente millonaria"; ya que no solo habla del dinero, sino de tener una visión del mundo positiva, cultivar tu mente y prosperar como persona.

Secretos de la mente millonaria
Padre rico padre pobre 
El hombre más rico de babilonia


---

Fin de semana de emprendimiento y startups.

Hace poco tuve la suerte de acudir al Techstars Startup Weekend de Ávila.
En un inicio no sabía muy bien lo que me iba a encontrar; quería conectar con emprendedores, empresarios, inversores y gente de la que aprender. 

A parte de poder hacer todo esto, al llegar me encontré con que se nos proponía el reto de validar una solución que hiciese frente a un problema real para pitchearla ante jurado en 54 horas. Con el fantástico equipo que formé logramos la victoria, abriendonos puertas al Startup Olé Accelerator aquí en España. 

Este evento te aporta otra visión de los negocios y te enseña varias cosas que no se aprenden en otros sitios. 
Caminas de la mano y aprendes de gente exitosa en los negocios, fundadores de empresas valoradas en cientos de millones de €, business angels e incluso mentores de cosas tan importantes como la psicología o la sociología en este sector.

Me gustaría agradeceros personalmente todo lo que he aprendido de vosotros y los ratos que hemos compartido, en especial a ___ ___ ___; estoy aplicando todo ello en mi emprendimiento.

Espero que nos volvamos a ver pronto. 

---


Emocionado de poderos hablar por primera vez de un proyecto que ha marcado mi trayectoria profesional y que he creado e implementado durante 2023-2024. 
Combinándolo con el resto de proyectos de consultoría tecnológica que llevo a cabo con otros clientes, durante 18 meses he llevado a cabo un importante proyecto de digitalización del compañia_X en España, mediante la creación de una solución de software completa "End-to-end" . Gracias a ella se han automatizado múltiples procesos que han permitido la integración masiva de datos y explotar la inteligencia de negocio mediante la ingeniería y analítica de datos. 
Ha sido un proyecto intenso y lleno de retos, en el que he aplicado todos mis conocimientos para partiendo de 0, diseñar, planificar, desarrollar y desplegar la solución. 
El resultado han sido varias plataformas, entre ellas una aplicación de usuario nativa desarrollada en Python, una base de datos operacional en PostgreSQL, un datawarehouse con tareas automatizadas y calculo de algoritmos , y un portal web de Tableau donde mi cliente final analiza una gran cantidad de métricas de negocio y dashboards interactivos.
En este proyecto he podido aplicar múltiples aptitudes, no solo de consultoría y desarrollo de software, sino también comerciales, financieras, de desarrollo de negocio, organizativas, formativas y un largo etc.
Me gustaría incluir en el post a persona_u  , a quien en su día propuse que colaborase conmigo para que me ayudase con varias partes del proyecto, y a quien estoy tremendamente agradecido por ser un gran profesional.
Además persona_u y yo hemos comenzado una nueva etapa de emprendimiento como socios, que pronto compartiremos con mucha ilusión con todos vosotros.

---



