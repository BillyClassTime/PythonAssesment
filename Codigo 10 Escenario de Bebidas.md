## Escenario de Bebidas: Código 10

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central es la comercialización de Bebidas:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las Bebidas.

Las Bebidas que se comercializan son Cervezas, Refrescos y tes, pero próximamente se añadirán mas variedades a la comercialización para incluir zumos y lácteos. 

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases.

```
Bebidas: cerveza, refresco, té.
```

``` python
from abc import ABC, abstractmethod

class Bebidas(ABC):
    def __init__(self, nombre, precio):
        self.nombre = nombre
        self.precio = precio

    @abstractmethod
    def descripcion(self):
        pass

class Cerveza(Bebidas):
    def __init__(self, nombre, precio, tipo_cerveza):
        super().__init__(nombre, precio)
        self.tipo_cerveza = tipo_cerveza

    def descripcion(self):
        print(f"La cerveza {self.nombre} es del tipo {self.tipo_cerveza}. Su precio es {self.precio}.")

class Refresco(Bebidas):
    def __init__(self, nombre, precio, sabor):
        super().__init__(nombre, precio)
        self.sabor = sabor

    def descripcion(self):
        print(f"El refresco {self.nombre} es de sabor {self.sabor}. Su precio es {self.precio}.")

class Te(Bebidas):
    def __init__(self, nombre, precio, variedad):
        super().__init__(nombre, precio)
        self.variedad = variedad

    def descripcion(self):
        print(f"El té {self.nombre} es de la variedad {self.variedad}. Su precio es {self.precio}.")
```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def Bebidas():
    return render_template("start_Bebidas.html")

@app.route("/Bebidas", methods=['POST'])
def mostrar_Bebidas():
 # Obtener la Bebida seleccionada por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de Bebidas con la Bebida seleccionada
 return render_template("Bebidas.html", Bebida=Bebida_ingresada)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--Bebidas.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la Bebida</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de Bebidas</legend>
        <div class="form-group row">
            {% if Bebida %}
            <p><strong>Nombre:</strong> {{ Bebida.nombre }}</p>
            <p><strong>precio:</strong> {{ Bebida.precio }}</p>
            {% if (Bebida.Nombre == "Cerveza") %}
            <p><strong>tipo_cerveza:</strong> {{ Bebida.tipo_cerveza }}</p>
            {% elif (Bebida.Nombre== "Refresco") %}
            <p><strong>Sabor:</strong> {{ Bebida.sabor }}</p>
            {% elif (Bebida.Nombre == "te") %}
            <p><strong>Variedad:</strong> {{ Bebida.variedad }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ Bebida.descripcion() }}</p>
            {% else %}
            <p>La Bebida seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas Bebidas</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_Bebidas.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de Bebidas</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/Bebidas">
    <legend>Información de Bebidas</legend>
    <fieldset  class="d-grid" >
      <label for="Bebida">Selecciona una Bebida:</label>
      <select id="Bebida" name="Bebida" class="col-form-label col-form-label-sm">
        <option value="Cerveza">Cerveza</option>
        <option value="Refresco">Refresco</option>
        <option value="te">Té</option>
      </select>
      <label for="Precio" class="col-form-label col-form-label-sm">Precio:</label>
      <input type="number" id="precio" name="precio" >
      <div id="atributos">
        <label for="tipo_cerveza" class="col-form-label col-form-label-sm">Tipo Cerveza:</label>
        <input type="text" id="tipo_cerveza" name="tipo_cerveza" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const BebidaSelect = document.getElementById("Bebida");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const Bebida = BebidaSelect.value;
      atributosDiv.innerHTML = "";

      if (Bebida === "Cerveza") {
        atributosDiv.innerHTML += `
  <label for="tipo_cerveza" class="col-form-label col-form-label-sm">Tipo Cerveza:</label>
        <input type="text" id="tipo_cerveza" name="tipo_cerveza" >
          `;
      } else if (Bebida === "Refresco") {
        atributosDiv.innerHTML += `
            <label for="sabor" class="col-form-label col-form-label-sm">Sabor:</label>
            <input type="text" id="sabor" name="sabor">
          `;
      } else if (Bebida === "te") {
        atributosDiv.innerHTML += `
            <label for="variedad" class="col-form-label col-form-label-sm">Variedad:</label>
            <input type="text" id="variedad" name="variedad">
          `;
      }
    }
    BebidaSelect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



