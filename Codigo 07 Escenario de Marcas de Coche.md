## Escenario de Marcas de Coche: Código 07

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central es la comercialización de coches:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las coches.

Las coches que se comercializan son Ford, Toyota y Honda, pero próximamente se añadirán mas variedades a la comercialización según como vayan siendo cerrados acuerdos con los diferentes fabricantes.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases

```
Marcas de coches: Ford, Toyota, Honda.
```

``` python
from abc import ABC, abstractmethod

class Coches(ABC):
    def __init__(self, fabricante, anyo, modelo):
        self.fabricante = fabricante
        self.anyo = anyo
        self.modelo = modelo

    @abstractmethod
    def descripcion(self):
        pass

class Ford(Coches):
    def __init__(self, fabricante, anyo, modelo, color):
        super().__init__(fabricante, anyo, modelo)
        self.color = color

    def descripcion(self):
        print(f"Este es un Ford {self.modelo} de color {self.color} fabricado en {self.anyo} por {self.fabricante}.")

class Toyota(Coches):
    def __init__(self, fabricante, anyo, modelo, num_puertas):
        super().__init__(fabricante, anyo, modelo)
        self.num_puertas = num_puertas

    def descripcion(self):
        print(f"Este es un Toyota {self.modelo} de {self.num_puertas} puertas fabricado en {self.anyo} por {self.fabricante}.")

class Honda(Coches):
    def __init__(self, fabricante, anyo, modelo, tipo_transmision):
        super().__init__(fabricante, anyo, modelo)
        self.tipo_transmision = tipo_transmision

    def descripcion(self):
        print(f"Este es un Honda {self.modelo} con transmisión {self.tipo_transmision} fabricado en {self.anyo} por {self.fabricante}.")
```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def coches():
    return render_template("start_coches.html")

@app.route("/coches", methods=['POST'])
def mostrar_coches():
 # Obtener el coche seleccionado por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de coches con el coche seleccionado
 return render_template("coches.html", coche=coche_ingresado)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--coches.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la coche</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de coches</legend>
        <div class="form-group row">
            {% if coche %}
            <p><strong>fabricante:</strong> {{ coche.fabricante }}</p>
            <p><strong>Año:</strong> {{ coche.anyo }}</p>
            <p><strong>Modelo:</strong> {{ coche.modelo }}</p>
            {% if (coche.fabricante == "ford") %}
            <p><strong>Color:</strong> {{ coche.color }}</p>
            {% elif (coche.fabricante == "toyota") %}
            <p><strong>Número de puertas:</strong> {{ coche.num_puertas }}</p>
            {% elif (coche.fabricante == "honda") %}
            <p><strong>tipo_transmision:</strong> {{ coche.tipo_transmision }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ coche.descripcion() }}</p>
            {% else %}
            <p>La coche seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas coches</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_coches.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de coches</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/coches">
    <legend>Información de coches</legend>
    <fieldset  class="d-grid" >
      <label for="coche">Selecciona una coche:</label>
      <select id="coche" name="coche" class="col-form-label col-form-label-sm">
        <option value="ford">Ford</option>
        <option value="toyota">Toyota</option>
        <option value="honda">Honda</option>
      </select>
      <label for="anyo" class="col-form-label col-form-label-sm">Año:</label>
      <input type="number" id="anyo" name="anyo" >
      <label for="modelo" class="col-form-label col-form-label-sm">Modelo:</label>
      <input type="text" id="modelo" name="modelo" >

      <div id="atributos">
        <label for="color" class="col-form-label col-form-label-sm">Color:</label>
        <input type="text" id="color" name="color" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const cocheselect = document.getElementById("coche");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const coche = cocheselect.value;
      atributosDiv.innerHTML = "";

      if (coche === "ford") {
        atributosDiv.innerHTML += `
        <label for="color" class="col-form-label col-form-label-sm">Color:</label>
        <input type="text" id="color" name="color" >
          `;
      } else if (coche === "toyota") {
        atributosDiv.innerHTML += `
            <label for="num_puertas" class="col-form-label col-form-label-sm">num_puertas:</label>
            <input type="text" id="num_puertas" name="num_puertas">
          `;
      } else if (coche === "honda") {
        atributosDiv.innerHTML += `
            <label for="tipo_transmision" class="col-form-label col-form-label-sm">Tipo_transmision:</label>
            <input type="text" id="tipo_transmision" name="tipo_transmisioin">
          `;
      }
    }
    cocheselect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



