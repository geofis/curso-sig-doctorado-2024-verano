Curso introductorio a los Sistemas de Información Geográfica (SIG)
================
José Martínez

Versión HTML (más legible e interactiva),
[aquí](https://geofis.github.io/curso-sig-doctorado-2024-verano/README.html)

# Presentaciones de diapositivas incluidas en este repo:

- [Introducción a los SIG y herramientas de
  programación](https://geofis.github.io/curso-sig-doctorado-2024-verano/media/intro-sig-herramientas-programacion.html)

- [Puntos de muestreo, herramientas de
  programación](https://geofis.github.io/curso-sig-doctorado-2024-verano/media/puntos-de-muestreo-herramientas-programacion.html)

# Fecha

- Días: 1 al 4 de julio, 2024
- Horario: 2 a 4.30 pm
- Lugar: aula FC-101

``` r
library(leaflet)
leaflet() %>%
  addProviderTiles(providers$Esri.WorldImagery, options = providerTileOptions(maxZoom = 21)) %>%
  leaflet::addMiniMap(width = 100, height = 100) %>%
  setView(lng = -69.91673, lat = 18.45952, zoom = 18) %>%
  addMarkers(lng = -69.91673, lat = 18.45952, popup = "FC-101", ) %>%
  leafem::addMouseCoordinates()
```

<div class="leaflet html-widget html-fill-item" id="htmlwidget-f565555ecaa566430a09" style="width:50%;height:384px;"></div>
<script type="application/json" data-for="htmlwidget-f565555ecaa566430a09">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addProviderTiles","args":["Esri.WorldImagery",null,null,{"errorTileUrl":"","noWrap":false,"detectRetina":false,"maxZoom":21}]},{"method":"addMiniMap","args":[null,null,"bottomright",100,100,19,19,-5,false,false,false,false,false,false,{"color":"#ff7800","weight":1,"clickable":false},{"color":"#000000","weight":1,"clickable":false,"opacity":0,"fillOpacity":0},{"hideText":"Hide MiniMap","showText":"Show MiniMap"},[]]},{"method":"addMarkers","args":[18.45952,-69.91673,null,null,null,{"interactive":true,"draggable":false,"keyboard":true,"title":"","alt":"","zIndexOffset":0,"opacity":1,"riseOnHover":false,"riseOffset":250},"FC-101",null,null,null,null,{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null]}],"setView":[[18.45952,-69.91673],18,[]],"limits":{"lat":[18.45952,18.45952],"lng":[-69.91673,-69.91673]}},"evals":[],"jsHooks":{"render":[{"code":"function(el, x, data) {\n  return (\n      function(el, x, data) {\n      // get the leaflet map\n      var map = this; //HTMLWidgets.find('#' + el.id);\n      // we need a new div element because we have to handle\n      // the mouseover output separately\n      // debugger;\n      function addElement () {\n      // generate new div Element\n      var newDiv = $(document.createElement('div'));\n      // append at end of leaflet htmlwidget container\n      $(el).append(newDiv);\n      //provide ID and style\n      newDiv.addClass('lnlt');\n      newDiv.css({\n      'position': 'relative',\n      'bottomleft':  '0px',\n      'background-color': 'rgba(255, 255, 255, 0.7)',\n      'box-shadow': '0 0 2px #bbb',\n      'background-clip': 'padding-box',\n      'margin': '0',\n      'padding-left': '5px',\n      'color': '#333',\n      'font': '9px/1.5 \"Helvetica Neue\", Arial, Helvetica, sans-serif',\n      'z-index': '700',\n      });\n      return newDiv;\n      }\n\n\n      // check for already existing lnlt class to not duplicate\n      var lnlt = $(el).find('.lnlt');\n\n      if(!lnlt.length) {\n      lnlt = addElement();\n\n      // grab the special div we generated in the beginning\n      // and put the mousmove output there\n\n      map.on('mousemove', function (e) {\n      if (e.originalEvent.ctrlKey) {\n      if (document.querySelector('.lnlt') === null) lnlt = addElement();\n      lnlt.text(\n                           ' lon: ' + (e.latlng.lng).toFixed(5) +\n                           ' | lat: ' + (e.latlng.lat).toFixed(5) +\n                           ' | zoom: ' + map.getZoom() +\n                           ' | x: ' + L.CRS.EPSG3857.project(e.latlng).x.toFixed(0) +\n                           ' | y: ' + L.CRS.EPSG3857.project(e.latlng).y.toFixed(0) +\n                           ' | epsg: 3857 ' +\n                           ' | proj4: +proj=merc +a=6378137 +b=6378137 +lat_ts=0.0 +lon_0=0.0 +x_0=0.0 +y_0=0 +k=1.0 +units=m +nadgrids=@null +no_defs ');\n      } else {\n      if (document.querySelector('.lnlt') === null) lnlt = addElement();\n      lnlt.text(\n                      ' lon: ' + (e.latlng.lng).toFixed(5) +\n                      ' | lat: ' + (e.latlng.lat).toFixed(5) +\n                      ' | zoom: ' + map.getZoom() + ' ');\n      }\n      });\n\n      // remove the lnlt div when mouse leaves map\n      map.on('mouseout', function (e) {\n      var strip = document.querySelector('.lnlt');\n      if( strip !==null) strip.remove();\n      });\n\n      };\n\n      //$(el).keypress(67, function(e) {\n      map.on('preclick', function(e) {\n      if (e.originalEvent.ctrlKey) {\n      if (document.querySelector('.lnlt') === null) lnlt = addElement();\n      lnlt.text(\n                      ' lon: ' + (e.latlng.lng).toFixed(5) +\n                      ' | lat: ' + (e.latlng.lat).toFixed(5) +\n                      ' | zoom: ' + map.getZoom() + ' ');\n      var txt = document.querySelector('.lnlt').textContent;\n      console.log(txt);\n      //txt.innerText.focus();\n      //txt.select();\n      setClipboardText('\"' + txt + '\"');\n      }\n      });\n\n      }\n      ).call(this.getMap(), el, x, data);\n}","data":null}]}}</script>

# Programa

## Día 1: Introducción a los SIG y herramientas de programación

### Primera sesión (1 hora)

- Introducción a los Sistemas de Información Geográfica (SIG)
- Historia y evolución de los SIG
- Aplicaciones de los SIG en diversas disciplinas
- Ejercicio práctico:
  - Interfaz gráfica de QGIS
  - Cargar una fuente ráster
  - Cargar una fuente vectorial

### Segunda sesión (1.5 horas)

- Introducción a R y RStudio (cuaderno RMarkdown)
- Introducción a Python y Jupyter (cuaderno Jupyter)
- Ejercicio práctico:
  - Iniciar en la cuenta del servidor RStudio
  - Configuración de cuadernos reproducibles
  - Cuaderno reproducible
  - \[Tutorial 1(<https://geofis.shinyapps.io/tutorial1/>)

## Día 2: Puntos de muestreo

### Primera sesión (1 hora)

- Conceptos y técnicas para la creación de puntos de muestreo
- Herramientas para la visualización de puntos de muestreo

### Segunda sesión (1.5 horas)

- Ejercicio práctico: Creación y visualización de puntos de muestreo
- Discusión y análisis de resultados

## Día 3: Fuentes de imágenes satelitales orientado al análisis de uso de suelo

### Primera sesión (1 hora)

- Introducción a las imágenes satelitales
- Proveedores y tipos de imágenes satelitales

### Segunda sesión (1.5 horas)

- Técnicas de interpretación de imágenes satelitales
- Ejercicio práctico: Uso de Google Earth Engine para análisis de uso de
  suelo

## Día 4: Mapeo de áreas de sensibilidad ambiental y conclusiones

### Primera sesión (1 hora)

- Identificación y mapeo de áreas de sensibilidad ambiental
- Herramientas y técnicas de análisis espacial

### Segunda sesión (1.5 horas)

- Ejercicio práctico: análisis estadísticos y mapeo de áreas de
  sensibilidad ambiental con R y RStudio
- Discusión y retroalimentación
- ¿Para qué podrían usarse los servicios opcionales (ver abajo)?
- Conclusiones y próximos pasos en el aprendizaje de SIG

## Recursos y Herramientas

- **Software:**
  - Para instalar: QGIS (versión 3.x).
  - Provistos por mí, pero adelante si los quieres instalar: R en
    RStudio y Python en cuadernos Jupyter.
- **Servicios:**
  - Google Earth Engine, casi imprescindible.
  - ChatGPT
  - (opcional) Copernicus Data Space Ecosystem o Sentinel Hub
  - (opcional) Google Colab
  - (opcional) GitHub
  - (opcional) Overleaf. Obtén una cuenta en Overleaf para crear
    documentos avanzados
  - (opcional) Zotero Desktop y cuenta en Zotero. Te podría ayudar a
    manejar citas y referencias. Existen otros servicios, como Scite y
    CiteDrive
- **Datos:** Imágenes satelitales (por ejemplo, Landsat, Sentinel),
  bases de datos geográficos disponibles públicamente. Orientaré dónde
  obtener estas fuentes, pero últimamente recomiendo apuntar primero al
  Google Earth Engine.
- **Lecturas:** Las que deseen traer; son bienvenidos artículos
  introductorios y tutoriales en línea sobre QGIS, R y Python para
  geociencias, y Google Earth Engine.

# Referencias destacadas

Bivand, R. S., Pebesma, E., & Gómez-Rubio, V. (2013). Applied Spatial
Data Analysis with R. Springer New York.
<https://doi.org/10.1007/978-1-4614-7618-4>

Olaya, V. (2020). Sistemas de Información Geográfica.
<https://volaya.github.io/libro-sig/>

Lovelace, R., Nowosad, J., & Muenchow, J. (2019). Geocomputation with R.
Chapman and Hall/CRC. <https://r.geocompx.org/>

Dorman, M., Graser A., Nowosad, J. & Lovelace, R. (2019). Geocomputation
with Python. Chapman and Hall/CRC. <https://py.geocompx.org/>
