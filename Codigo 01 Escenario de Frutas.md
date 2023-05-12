## Escenario de Frutas: Código 01

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central es la comercialización de frutas:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las frutas.

Las frutas que se comercializan son Manzanas, Bananas y Naranjas, pero próximamente se añadirán mas variedades a la comercialización según como vayan siendo cerrados acuerdos con los cultivadores más próximos.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases

```
Frutas: manzana, banana, naranja.
```

``` python
from abc import ABC, abstractmethod

class Fruta(ABC):
    def __init__(self, nombre, cantidad):
        self.nombre = nombre
        self.cantidad = cantidad

    @abstractmethod
    def descripcion(self):
        pass

class Manzana(Fruta):
    def __init__(self, nombre, cantidad, variedad):
        super().__init__(nombre, cantidad)
        self.variedad = variedad
    def descripcion(self):
        return f"{self.nombre} es una manzana de variedad {self.variedad} Tiene un sabor dulce y es ideal para comer fresca o para hacer zumo."
    
class Banana(Fruta):
    def __init__(self, nombre, cantidad, madurez):
        super().__init__(nombre, cantidad)
        self.madurez = madurez
    def descripcion(self):
        return f"Esta es una banana de madurez {self.madurez}"  

class Naranja(Fruta):
    def __init__(self, nombre, cantidad, dulzor):
        super().__init__(nombre, cantidad)
        self.dulzor = dulzor
    def descripcion(self):
        return f"Esta es una naranja de dulzor {self.dulzor}"     

```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def frutas():
    return render_template("start_frutas.html")

@app.route("/frutas", methods=['POST'])
def mostrar_frutas():
 # Obtener la fruta seleccionada por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de frutas con la fruta seleccionada
 return render_template("frutas.html", fruta=fruta_ingresada)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--frutas.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la Fruta</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de frutas</legend>
        <div class="form-group row">
            {% if fruta %}
            <p><strong>Nombre:</strong> {{ fruta.nombre }}</p>
            <p><strong>Cantidad:</strong> {{ fruta.cantidad }}</p>
            {% if (fruta.Nombre == "Manzana") %}
            <p><strong>Variedad:</strong> {{ fruta.variedad }}</p>
            {% elif (fruta.Nombre== "Banana") %}
            <p><strong>Madurez:</strong> {{ fruta.madurez }}</p>
            {% elif (fruta.Nombre == "Naranja") %}
            <p><strong>Dulzor:</strong> {{ fruta.dulzor }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ fruta.descripcion() }}</p>
            {% else %}
            <p>La fruta seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas frutas</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_frutas.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de frutas</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/frutas">
    <legend>Información de frutas</legend>
    <fieldset  class="d-grid" >
      <label for="fruta">Selecciona una fruta:</label>
      <select id="fruta" name="fruta" class="col-form-label col-form-label-sm">
        <option value="Manzana">Manzana</option>
        <option value="Banana">Banana</option>
        <option value="Naranja">Naranja</option>
      </select>
      <label for="cantidad" class="col-form-label col-form-label-sm">Cantidad:</label>
      <input type="number" id="cantidad" name="cantidad" >
      <div id="atributos">
        <label for="variedad" class="col-form-label col-form-label-sm">Variedad:</label>
        <input type="text" id="variedad" name="variedad" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const frutaSelect = document.getElementById("fruta");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const fruta = frutaSelect.value;
      atributosDiv.innerHTML = "";

      if (fruta === "Manzana") {
        atributosDiv.innerHTML += `
            <label for="variedad" class="col-form-label col-form-label-sm">Variedad:</label>
            <input type="text" id="variedad" name="variedad">
          `;
      } else if (fruta === "Banana") {
        atributosDiv.innerHTML += `
            <label for="madurez" class="col-form-label col-form-label-sm">Madurez:</label>
            <input type="text" id="madurez" name="madurez">
          `;
      } else if (fruta === "Naranja") {
        atributosDiv.innerHTML += `
            <label for="dulzor" class="col-form-label col-form-label-sm">Dulzor:</label>
            <input type="text" id="dulzor" name="dulzor">
          `;
      }
    }
    frutaSelect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



