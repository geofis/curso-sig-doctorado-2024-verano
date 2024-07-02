Diseño de muestreo espacial estratificado
================
<b>José-Ramón Martínez-Batlle</b> (<jmartinez19@uasd.edu.do>) <br>
Facultad de Ciencias, Universidad Autónoma de Santo Domingo (UASD) <br>
Santo Domingo, República Dominicana

<!-- README.md se genera a partir de README.Rmd. Por favor, edita ese archivo. -->

------------------------------------------------------------------------

# Generales

- **Objetivo:** En esta práctica, te familiarizarás con el software QGIS
  para realizar un diseño de muestreo espacial estratificado usando
  coberturas del suelo.

- **[Ver vídeo
  demostrativo](https://drive.google.com/file/d/1k6IotOHj6fUkyfi4rSBK6d320TY45KED/view?usp=drive_link)**

------------------------------------------------------------------------

# Ejercicio. Diseño de muestreo espacial estratificado

**Resumen:** Aprenderás a realizar un diseño de muestreo espacial
estratificado por coberturas, lanzando 30 puntos aleatoriamente
localizados sobre dos coberturas del suelo diferentes, distribuidos
proporcionalmente según el área de cada cobertura.

En esta práctica, explorararás cómo se distribuyen distintas coberturas
en tu área asignada una fuente abierta un software SIG, en este caso
QGIS.

La capa ráster de coberturas es el mapa global titulado “Land Cover
100m: version 3 Globe 2015-2019” (Buchhorn et al., s. f.). El mapa se
elaboró de forma sistemática para todos los años comprendidos en el
periodo 2015-2019, pero en esta práctica sólo usarás la fuente de 2019.
El ráster tiene una resolución espacial de 100m, y representa múltiples
coberturas del suelo clasificadas mediante algoritmos de *machine
learning*. Fue elaborado por el equipo del componente global del
Servicio de Monitoreo de Tierras de Copernicus, el cual produce
sistemáticamente mapas globales de cobertura y cambios en la cobertura
del suelo, así como estadísticas sobre la superficie cubierta por cada
cobertura. Los principales insumos usados para realizar dicho mapa,
fueron observaciones del satélite PROBA-V, organizadas en millones de
teselas (cuadros) equivalentes a Sentinel-2 de 110x110 km.

Estos son los pasos clave que debes dar para realizar un muestreo
estratificado en tu área asignada:

1.  Descarga, desde [esta ruta](media/fuentes/practica-muestreo), una
    capa vectorial. Autoasígnate una, eligiendo un número del 1 al 25, o
    haz que R la elija aleatoriamente con `sample(1:25, 1)`.
    Identifícala en función del número de estudiante que hayas elegido
    entre el 1 y el 25.

2.  Carga la capa vectorial de tu área asignada en QGIS.

3.  Descarga, [desde aquí](https://lcviewer.vito.be/download), la capa
    ráster del año 2019 correspondiente al mapa “Land Cover 100m:
    version 3 Globe 2015-2019”. Para esto, haz clic sobre el área que
    cubre nuestro país, luego elige “*Discrete classification*” dentro
    del grupo *Land Cover Classification* y finalmente presiona el botón
    “2019” para iniciar la descarg. Normalmente, obtendrás un archivo
    con el nombre
    “W080N20_PROBAV_LC100_global_v3.0.1_2019-nrt_Discrete-Classification-map_EPSG-4326.tif”.
    Ten presente que el archivo que descargarás cubre un área de mucho
    mayor tamaño que la isla Española (abarca partes de Centroamérica y
    Sudamérica); esto se debe a que el Servicio de Monitoreo de Tierras
    de Copernicus ofrece cuadros (teselas) muy grandes, de 20x20 grados
    (~2200x2150 km). Más adelante, te explico cómo recortar el ráster
    dentro de tu área asignada.

4.  Observa tu área asignada, identifica qué coberturas están presentes
    y cómo éstas se distribuyen en términos espaciales y en cuanto a
    proporciones. Usa la herramienta de “Identificación de elementos”
    (*Identify features*) para hacer clic sobre el ráster y explorar los
    valores numéricos de cada celda; dichos valores se corresponden con
    la leyenda de la tabla 4 de [este
    PDF](https://zenodo.org/records/4723921/files/CGLOPS1_PUM_LC100m-V3_I3.4.pdf?download=1).
    Para usuarios/as avanzados/as: existe un complemento llamado “*Value
    tool*” que ofrece el valor de las celdas sin necesidad de hacer clic
    sobre ellas, basta con pasar el puntero del ratón por encima del
    ráster (si te interesa, instala primero dicho complemento).

5.  Realiza el muestreo espacial estratificado en tu área asignada
    (recuerda, 30 puntos en total en toda tu área asignada). Para esto,
    primero divide tu área según el uso y la cobertura del terreno y
    luego lanza los puntos aleatorios. Carga y Procesamiento en QGIS:

5.1. Carga la capa de raster de uso y cobertura del suelo en QGIS.
Normalmente, será un archivo que descargarías en la ruta mencionada
arriba, y que tendrá por nombre algo tal que
“W080N20_PROBAV_LC100_global_v3.0.1_2019-nrt_Discrete-Classification-map_EPSG-4326.tif”.

5.2. Corta el ráster. Usando la herramienta `Clip Raster by Mask Layer`
(`Cortar Ráster por capa de máscara`) del menú `Raster>Misceléneos`,
recorta tu ráste de coberturas. Indícale que la capa de máscara es el
vectorial de tu área asignada, y que el ráster de entrada (el ráster a
recortar) es el de coberturas. Elige una ruta/nombre para el ráster de
salida (por ejemplo, `coberturas-recortado.tif`), y presiona ejecutar.

5.3. Clasificación del Raster. Para simplificar, reclasifica el ráster
de coberturas que acabas de recortar en sólo dos clases: las celdas de
bosque (con valores originalmente de 111 a 126, representadas por tonos
verdes) deberían reclasificarse a valor 1; las celdas restantes (por
ejemplo, matorral, urbano), deberían reclasificarse a valor 0. Para
esto, necesitarás revisar la tabla 4 de [este
PDF](https://zenodo.org/records/4723921/files/CGLOPS1_PUM_LC100m-V3_I3.4.pdf?download=1).
Usa la herramienta `Reclassify by table` (`Reclasificar por tabla`) en
QGIS para hacer la reclasificación. Para esto, deberás crear una tabla
de reclasificación, donde los valores que representan el bosque asuman
valor 1 y todos los restantes valores asuman valores 0. Debes observar
tanto la creación de la tabla como la forma de elegir los límites de los
umbrales. Usa [este vídeo (en
español)](https://www.youtube.com/watch?v=hT_7BI93gEg) o [este otro (en
inglés)](https://www.youtube.com/watch?v=s7KrIjvcCz0) para informarte
sobre el uso de la herramienta. Define una ruta y un nombre de salida
para el ráster reclasificado, por ejemplo,
`coberturas-reclasificado.tif`. Para usuarios/as avanzados/as: QGIS está
preparado para realizar el diseño de muestreo estratificando con más de
dos clases, en cuyo caso seguirías los mismos pasos explicados en esta
práctica, conservando las clases que sean de tu interés.

5.4. Símbolos y visualización. Cuando hayas reclasificado la capa, se
cargará automáticamente en el lienzo de QGIS si así se especificó al
momento de crearla. Modifica la simbología de la capa ráster
reclasificada, estableciendo el valor máximo a 1, para visualizar las
coberturas agrupadas rápidamente.

5.5. Convierte de ráster a vectorial (polígonos). Convierte el raster
reclasificado en una capa vectorial. Utiliza el comando
`Poligonizar "Ráster a Vectorial` (`Polygonize (Raster to Vector)`) del
menú `Ráster>Conversión`, y elige una ruta y nombre de archivo de salida
(por ejemplo, `cobertura-vectorial.gpkg`).

5.6. Del vectorial de coberturas, selecciona los polígonos con valor “1”
en el campo DN. Para esto, abre la tabla de atributos del vectorial, y
selecciona los elementos de interés. Puedes hacerlo usando el ratón y
manteniendo la tecla `Control` (`Ctrl`) del teclado presionada, pero si
son muchos elementos (polígonos), éste podría no ser un método práctico.
Puedes seleccionar también por atributos, para lo cual, abre la tabla de
atributos, y usa la herramienta
`Seleccionar elementos usando una expresión` (coloca la expresión
`"DN" = 1` y presiona `Seleccionar elementos`), o la herramienta
`Seleccionar/filtrar elementos usando un formulario` (escribe `1` en el
campo de formulario `DN` y presiona `Seleccionar elementos`).

5.7. Lanza los puntos aleatorios. Abre la herramienta
`Puntos aleatorios en los límites de la capa` del menú
`Vector>Herramientas de investigación`, en `Capa de entrada` elige el
vectorial de coberturas, marca la opción `Sólo elementos seleccionados`
y en número de puntos deberás escribir cuántos puntos aleatorios lanzar
(ver siguiente oración), no cambies la opción
`Distancia mínima entre puntos` y elige una ruta y nombre de salida para
el vectorial de puntos aleatorios (por ejemplo, `puntos-bosque.gpkg`).
El número de puntos a lanzar debe ser proporcional a la superficie que
ocupa el bosque en tu área asignada. Supón que, en tu área asignada, el
bosque ocupa el 70%. Pues bien, de 30 puntos en total que debes lanzar
en tu área asignada (número aproximado, no es estricto), lanzarás
aleatoriamente en tu área asignada, 21 (el 70%, que equivale a `30x0.7`)
deberían caer en bosque, y los restantes 9 en la otra cobertura. Puedes
calcular el área de la cobertura bosque y de la cobertura no bosque
usando la herramienta `Añadir atributos de geometría` en el menú
`Vector>Herramientas de geometría`. Sin ebargo, para mantener la
práctica lo más simple posible, realiza el cálculo de proporciones por
medio de estimación visual, para lo cual, observa los polígonos de
bosque y no bosque y estima que proporciones hay (por ejemplo, 40% y
60%, o 20% y 80%), y usa dichas proporciones para decidir cuántos puntos
lanzar dentro de cada cobertura.

5.8. Repite los pasos 5.6 y 5.7 para el área de no bosque.

5.9. Simboliza los puntos. Define una simbología común para los puntos
que corresponden a la cobertura bosque, y otra simbología, también
común, para los puntos de la cobertura no bosque, de tal suerte que los
puntos dentro de la cobertura bosque tendrán la misma simbología entre
sí, pero se diferenciarán de los puntos de la cobertura no bosque (y
viceversa). Puedes usar el color o la forma del punto, o ambas. Bonus:
si puedes, coloca etiquetas a cada punto, yendo a la pestaña `Etiquetas`
del panel `Estilo de capas`, definiendo `Etiquetas sencillas` y en
`Valor` colocando eligiendo el campo `id`. Esto hará que los puntos
tengan un rótulo único que los diferencie entre sí.

5.10. Paso final. Observa el resultado de los puntos aleatorios con la
capa vectorial de coberturas. Deberías notar que la proporcionalidad en
cuanto al área (estimada o calculada) de cada cobertura se corresponde
con la proporcionalidad de tipos puntos. El mapa de los puntos
aleatorios deberá figurar en el documento de entrega.

# Referencias

<div id="refs" class="references csl-bib-body hanging-indent"
entry-spacing="0" line-spacing="2">

<div id="ref-buchhorn" class="csl-entry">

Buchhorn, M., Smets, B., Bertels, L., Roo, B. D., Lesiv, M., Tsendbazar,
N.-E., Herold, M. y Fritz, S. (s. f.). *Copernicus Global Land Service:
Land Cover 100m: collection 3: epoch 2019: Globe*.
<https://doi.org/10.5281/ZENODO.3939050>

</div>

</div>
