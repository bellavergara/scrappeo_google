# Google Careers Scraper

Este script en Python realiza scraping en el sitio web de Google Careers para obtener información sobre las vacantes de empleo. El código utiliza las bibliotecas `requests`, `BeautifulSoup` para analizar el HTML de las páginas web, y `json` para manipular datos en formato JSON.

## Estructura de Datos

### Clases Pydantic

El script define varias clases Pydantic para modelar diferentes aspectos de una oferta de trabajo, como habilidades, aptitudes, herramientas, idiomas, beneficios y la propia oferta de trabajo.

```python
class Skill(BaseModel):
    # ...

class Aptitude(BaseModel):
    # ...

class Tool(BaseModel):
    # ...

class Language(BaseModel):
    # ...

class Benefit(BaseModel):
    # ...

class JobPost(BaseModel):
    # ...
```

### Configuración Adicional

Se utiliza la configuración `Extra.ignore` en la clase `JobPost` para ignorar campos adicionales que no están definidos en el modelo.

## Funciones Principales

### `scrape_vacancy_urls()`

```python
def scrape_vacancy_urls():
    # ...
    # Función para obtener URLs de vacantes desde la página de Google Careers
    # Devuelve una lista de diccionarios con nombres y enlaces de vacantes
    # ...
```

### `scrape_vacancy_details(request_url)`

```python
def scrape_vacancy_details(request_url):
    # ...
    # Función para extraer información detallada de cada vacante
    # Devuelve un diccionario con la información extraída
    # ...
```

### `save_to_json(data, filename)`

```python
def save_to_json(data, filename):
    # ...
    # Función para guardar datos en formato JSON en un archivo
    # ...
```

### Ejecución Principal

```python
url_vacantes = scrape_vacancy_urls()
save_to_json(url_vacantes, 'data/url_vacantes.json')
print("Vacantes guardadas en url_vacantes.json")

detalles = []

with open('data/url_vacantes.json', 'r') as archivo:
    vacantes = json.load(archivo)

# Iterar sobre la lista de diccionarios en el archivo JSON
for vacante in vacantes:
    # Obtener la URL de cada trabajo
    url = vacante['link']
    informacion_vacantes= scrape_vacancy_details(url)
    
    detalles.append(informacion_vacantes)

save_to_json(detalles, 'data/informacion_vacantes.json')
print("Vacantes guardadas en informacion_vacantes.json")
```

