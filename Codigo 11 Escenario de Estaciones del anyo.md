## Escenario de Bebidas: Código 11

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central es la comercialización de estaciones del año:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las estaciones del año.

Las estaciones que se revisarán son primavera, verano, otoño, después si todo funciona bien se añadirá la última estación el invierno.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases.

```
Estaciones del año: primavera, verano, otoño.
```

``` python
from abc import ABC, abstractmethod

class Estaciones(ABC):
    def __init__(self, nombre, temperatura_media):
        self.nombre = nombre
        self.temperatura_media = temperatura_media

    @abstractmethod
    def descripcion(self):
        pass

class Primavera(Estaciones):
    def __init__(self, nombre, temperatura_media, flores):
        super().__init__(nombre, temperatura_media)
        self.flores = flores

    def descripcion(self):
        return f"La {self.nombre} es una estación con una temperatura media de {self.temperatura_media} grados y en la que florecen {self.flores}"

class Verano(Estaciones):
    def __init__(self, nombre, temperatura_media, actividades):
        super().__init__(nombre, temperatura_media)
        self.actividades = actividades

    def descripcion(self):
        return f"El {self.nombre} es una estación con una temperatura media de {self.temperatura_media} grados y en el que se realizan actividades como {self.actividades}"

class Otonyo(Estaciones):
    def __init__(self, nombre, temperatura_media, colores):
        super().__init__(nombre, temperatura_media)
        self.colores = colores

    def descripcion(self):
        return f"El {self.nombre} es una estación con una temperatura media de {self.temperatura_media} grados y en el que predominan los colores {self.colores}"
```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def estacions():
    return render_template("start_estaciones.html")

@app.route("/estaciones", methods=['POST'])
def mostrar_estacions():
 # Obtener la estacion seleccionada por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de estaciones con la estacion seleccionada
 return render_template("estacions.html", estacion=estacion_ingresada)

if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--estaciones.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la estacion</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de estacions</legend>
        <div class="form-group row">
            {% if estacion %}
            <p><strong>Nombre:</strong> {{ estacion.nombre }}</p>
            <p><strong>Temperatura Media:</strong> {{ estacion.temperatura_media }}</p>
            {% if (estacion.Nombre == "primavera") %}
            <p><strong>Flores:</strong> {{ estacion.flores }}</p>
            {% elif (estacion.Nombre== "verano") %}
            <p><strong>Actividades:</strong> {{ estacion.actividades }}</p>
            {% elif (estacion.Nombre == "otoño") %}
            <p><strong>Colores:</strong> {{ estacion.colores }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ estacion.descripcion() }}</p>
            {% else %}
            <p>La estacion seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas estacions</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_estaciones.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de estacions</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/estaciones">
    <legend>Información de estacions</legend>
    <fieldset  class="d-grid" >
      <label for="estacion">Selecciona una estacion:</label>
      <select id="estacion" name="estacion" class="col-form-label col-form-label-sm">
        <option value="primavera">Primavera</option>
        <option value="verano">Verano</option>
        <option value="otoño">Otoño</option>
      </select>
      <label for="temparatura_media" class="col-form-label col-form-label-sm">Temperatura Media:</label>
      <input type="number" id="temperatura_media" name="temperatura_media" >
      <div id="atributos">
        <label for="flores" class="col-form-label col-form-label-sm">Flores:</label>
        <input type="text" id="flores" name="flores" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const estacionSelect = document.getElementById("estacion");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const estacion = estacionSelect.value;
      atributosDiv.innerHTML = "";

      if (estacion === "primavera") {
        atributosDiv.innerHTML += `
        <label for="flores" class="col-form-label col-form-label-sm">Flores:</label>
        <input type="text" id="flores" name="flores" >
          `;
      } else if (estacion === "verano") {
        atributosDiv.innerHTML += `
            <label for="actividades" class="col-form-label col-form-label-sm">Actividades:</label>
            <input type="text" id="actividades" name="actividades">
          `;
      } else if (estacion === "otoño") {
        atributosDiv.innerHTML += `
            <label for="colores" class="col-form-label col-form-label-sm">Colores:</label>
            <input type="text" id="colores" name="colores">
          `;
      }
    }
    estacionSelect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



