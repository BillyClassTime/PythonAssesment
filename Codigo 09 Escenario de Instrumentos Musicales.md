## Escenario de Instrumentos Musicales: Código 09

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central es la comercialización de instrumentosmusicales:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las instrumentos musicales.

Las instrumentos musicales que se comercializan son trompetas, pianos y violines, pero próximamente se añadirán mas variedades a la comercialización según como vayan siendo cerrados acuerdos con diferentes fabricantes y lutieres. 

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases

```
Instrumentos Musicales: Trompeta, Piano y Violín
```

``` python
from abc import ABC, abstractmethod

class InstrumentosMusicales(ABC):
    def __init__(self, nombre, precio):
        self.nombre = nombre
        self.precio = precio

    @abstractmethod
    def descripcion(self):
        pass

class Trompeta(InstrumentosMusicales):
    def __init__(self, nombre, precio, tipo_trompeta):
        super().__init__(nombre, precio)
        self.tipo_trompeta = tipo_trompeta

    def descripcion(self):
        print(f"La trompeta {self.nombre} es del tipo {self.tipo_trompeta}. Su precio es {self.precio}.")

class Piano(InstrumentosMusicales):
    def __init__(self, nombre, precio, marca):
        super().__init__(nombre, precio)
        self.marca = marca

    def descripcion(self):
        print(f"El piano {self.nombre} es de la marca {self.marca}. Su precio es {self.precio}.")

class Violin(InstrumentosMusicales):
    def __init__(self, nombre, precio, tipo_violin):
        super().__init__(nombre, precio)
        self.tipo_violin = tipo_violin

    def descripcion(self):
        print(f"El violín {self.nombre} es del tipo {self.tipo_violin}. Su precio es {self.precio}.")
```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def instrumentosmusicales():
    return render_template("start_instrumentosmusicales.html")

@app.route("/instrumentosmusicales", methods=['POST'])
def mostrar_instrumentosmusicales():
 # Obtener la instrumentoMusical seleccionada por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de instrumentos musicales con el instrumento musical seleccionado
 return render_template("instrumentosmusicales.html", instrumentoMusical=instrumentoMusical_ingresado)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--instrumentosmusicales.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la instrumentoMusical</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de instrumentosmusicales</legend>
        <div class="form-group row">
            {% if instrumentoMusical %}
            <p><strong>Nombre:</strong> {{ instrumentoMusical.nombre }}</p>
            <p><strong>Precio:</strong> {{ instrumentoMusical.precio }}</p>
            {% if (instrumentoMusical.Nombre == "trompeta") %}
            <p><strong>Tipo trompeta:</strong> {{ instrumentoMusical.tipo_trompeta }}</p>
            {% elif (instrumentoMusical.Nombre== "piano") %}
            <p><strong>Marca:</strong> {{ instrumentoMusical.Marca }}</p>
            {% elif (instrumentoMusical.Nombre == "violín") %}
            <p><strong>Tipo violín:</strong> {{ instrumentoMusical.tipo_violin }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ instrumentoMusical.descripcion() }}</p>
            {% else %}
            <p>La instrumentoMusical seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas instrumentosmusicales</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_instrumentosmusicales.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de instrumentosmusicales</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/instrumentosmusicales">
    <legend>Información de instrumentosmusicales</legend>
    <fieldset  class="d-grid" >
      <label for="instrumentoMusical">Selecciona una instrumentoMusical:</label>
      <select id="instrumentoMusical" name="instrumentoMusical" class="col-form-label col-form-label-sm">
        <option value="trompeta">Trompeta</option>
        <option value="piano">Piano</option>
        <option value="violín">Violín</option>
      </select>
      <label for="precio" class="col-form-label col-form-label-sm">Precio:</label>
      <input type="number" id="precio" name="precio" >
      <div id="atributos">
        <label for="tipo_trompeta" class="col-form-label col-form-label-sm">Tipo trompeta:</label>
        <input type="text" id="tipo_trompeta" name="tipo_trompeta" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const instrumentosmusicaleselect = document.getElementById("instrumentoMusical");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const instrumentoMusical = instrumentosmusicaleselect.value;
      atributosDiv.innerHTML = "";

      if (instrumentoMusical === "trompeta") {
        atributosDiv.innerHTML += `
            <label for="tipo_trompeta" class="col-form-label col-form-label-sm">Tipo trompeta:</label>
        <input type="text" id="tipo_trompeta" name="tipo_trompeta" >
          `;
      } else if (instrumentoMusical === "piano") {
        atributosDiv.innerHTML += `
            <label for="marca" class="col-form-label col-form-label-sm">Marca:</label>
            <input type="text" id="marca" name="marca">
          `;
      } else if (instrumentoMusical === "violín") {
        atributosDiv.innerHTML += `
            <label for="tipo_violin" class="col-form-label col-form-label-sm">Tipo de Violín:</label>
            <input type="text" id="tipo_violin" name="tipo_violin">
          `;
      }
    }
    instrumentosmusicaleselect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



