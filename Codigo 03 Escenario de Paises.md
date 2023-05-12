## Escenario de Países: Código 03

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central es el estudio económico de países de la OECD.

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de la información económica de los países basado en estudios de diversos sectores.

Las países que iniciales que se incorporarán al estudio son México, España y Japón, pero próximamente se añadirán mas países conforme vayan llegando los resultado de los estudios  económicos.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases

```
Países: México, España, Japón.
```

``` python
from abc import ABC, abstractmethod

class Pais(ABC):
    def __init__(self, nombre, capital):
        self.nombre = nombre
        self.capital = capital

    @abstractmethod
    def descripcion(self):
        pass

class Mexico(Pais):
    def __init__(self, nombre, capital, idioma):
        super().__init__(nombre, capital)
        self.idioma = idioma

    def descripcion(self):
        print(f"México es un país de América del Norte, cuya capital es {self.capital} y su idioma oficial es el {self.idioma}.")

class Japon(Pais):
    def __init__(self, nombre, capital, moneda):
        super().__init__(nombre, capital)
        self.moneda = moneda

    def descripcion(self):
        print(f"Japón es un país de Asia, cuya capital es {self.capital} y su moneda oficial es el {self.moneda}.")

class Espana(Pais):
    def __init__(self, nombre, capital, region):
        super().__init__(nombre, capital)
        self.region = region

    def descripcion(self):
        print(f"España es un país de Europa, cuya capital es {self.capital} y se encuentra en la región de {self.region}.")
```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def Paises():
    return render_template("start_Paises.html")

@app.route("/Paises", methods=['POST'])
def mostrar_Paises():
 # Obtener la Pais seleccionado por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de Paises con el Pais seleccionado
 return render_template("Paises.html", Pais=Pais_ingresado)

if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--Paises.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información del Pais</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de Paises</legend>
        <div class="form-group row">
            {% if Pais %}
            <p><strong>Nombre:</strong> {{ Pais.nombre }}</p>
            <p><strong>Capital:</strong> {{ Pais.capital }}</p>
            {% if (Pais.Nombre == "Mexico") %}
            <p><strong>Idioma:</strong> {{ Pais.idioma }}</p>
            {% elif (Pais.Nombre == "Japón") %}
            <p><strong>Mondeda:</strong> {{ Pais.moneda }}</p>
            {% elif (Pais.Nombre == "España") %}
            <p><strong>Región:</strong> {{ Pais.region }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ Pais.descripcion() }}</p>
            {% else %}
            <p>La Pais seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas Paises</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_Paises.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de Paises</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/Paises">
    <legend>Información de Paises</legend>
    <fieldset  class="d-grid" >
      <label for="Pais">Selecciona una País:</label>
      <select id="Pais" name="Pais" class="col-form-label col-form-label-sm">
        <option value="México">México</option>
        <option value="Japón">Japón</option>
        <option value="España">España</option>
      </select>
      <label for="capital" class="col-form-label col-form-label-sm">Capital:</label>
      <input type="text" id="capital" name="capital" >
      <div id="atributos">
		 <label for="idioma" class="col-form-label col-form-label-sm">Idioma:</label>
      	 <input type="text" id="idioma" name="idioma" >      
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const Paiseselect = document.getElementById("Pais");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const Pais = Paiseselect.value;
      atributosDiv.innerHTML = "";

      if (Pais === "México") {
        atributosDiv.innerHTML += `
		 <label for="idioma" class="col-form-label col-form-label-sm">Idioma:</label>
      	 <input type="text" id="idioma" name="idioma" > 
          `;
      } else if (Pais === "Japón") {
        atributosDiv.innerHTML += `
            <label for="moneda" class="col-form-label col-form-label-sm">Moneda:</label>
            <input type="text" id="moneda" name="moneda">
          `;
      } else if (Pais === "España") {
        atributosDiv.innerHTML += `
            <label for="region" class="col-form-label col-form-label-sm">Región:</label>
            <input type="text" id="region" name="region">
          `;
      }
    }
    Paiseselect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



