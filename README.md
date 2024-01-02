# Web Scraping de Títulos de Libros

Este proyecto de Python utiliza web scraping para extraer títulos de libros con calificaciones altas de la página web "Books to Scrape".

## Estructura del Código

El script `web_scraping.py` realiza las siguientes tareas:

1. Importa las bibliotecas necesarias.
2. Define la URL base para el scraping.
3. Crea una lista para almacenar los títulos de libros con altas calificaciones.
4. Itera a través de las páginas del sitio web para extraer la información.

## Fragmentos de Código Clave

### Importación de Bibliotecas

import bs4
import requests

Estas bibliotecas son fundamentales para realizar solicitudes HTTP y para analizar el contenido HTML de las páginas web.

### Definición de la URL Base

#### Crear una url sin número de página
url_base = "https://books.toscrape.com/catalogue/page-{}.html"

La URL base se utiliza para iterar a través de las páginas del sitio web.

### Extracción y Almacenamiento de Títulos

El siguiente fragmento muestra cómo se itera a través de las páginas y se extraen los títulos de los libros:

    #titulos_rating_alto = []

    for pagina in range(1, 51):
        url_pagina = url_base.format(pagina)
        resultado = requests.get(url_pagina)
        sopa = bs4.BeautifulSoup(resultado.text, "lxml")
        libros = sopa.select(".product_pod")

    for libro in libros:
        if len(libro.select(".star-rating.Four")) != 0 or len(libro.select(".star-rating.Five")):
            titulo_libro = libro.select("a")[1]["title"]
            titulos_rating_alto.append(titulo_libro)


    for t in titulos_rating_alto:
    print(t)




Este fragmento de código itera a través de las primeras 50 páginas del sitio web, analiza el contenido HTML, selecciona los libros y verifica si tienen una calificación de cuatro o cinco estrellas. Luego, almacena y muestra los títulos de estos libros.
## Uso

Para ejecutar este script, simplemente ejecute el archivo `web_scraping.py` en un entorno que tenga instaladas las bibliotecas `bs4` y `requests`.


