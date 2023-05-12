## Escenario de Equipamiento deportivo: Código 02

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central es la comercialización de Equipamiento:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las Equipamiento.

Las Equipamiento que se comercializan son de Futbol, Baketballs y Rugby, pero próximamente se añadirán mas variedades a la comercialización según como vayan siendo cerrados acuerdos con las federaciones y clubes deportivos más próximos.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases

```
Equipamiento Deportivo: EquipamientoFutbol, EquipamientoBaketball, EquipamientoRugby.
```

``` python
from abc import ABC, abstractmethod

class EquipamientoDeportivo(ABC):
    def __init__(self, nombre, precio):
        self.nombre = nombre
        self.precio = precio
    
    @abstractmethod
    def descripcion(self):
        pass

class EquipamientoFutbol(EquipamientoDeportivo):
    def __init__(self, nombre, precio, talla):
        super().__init__(nombre, precio)
        self.talla = talla
    
    def descripcion(self):
        return f"{self.nombre} talla {self.talla} para futbol, precio: {self.precio}"

class EquipamientoBasketball(EquipamientoDeportivo):
    def __init__(self, nombre, precio, talla, material):
        super().__init__(nombre, precio)
        self.talla = talla
        self.material = material
    
    def descripcion(self):
        return f"{self.nombre} talla {self.talla} para basketball, hecho de {self.material}, precio: {self.precio}"

class EquipamientoRugby(EquipamientoDeportivo):
    def __init__(self, nombre, precio, peso):
        super().__init__(nombre, precio)
        self.peso = peso
    
    def descripcion(self):
        return f"{self.nombre} con peso de {self.peso} para rugby, precio: {self.precio}"

```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def Equipamiento():
    return render_template("start_Equipamiento.html")

@app.route("/Equipamiento", methods=['POST'])
def mostrar_Equipamiento():
 # Obtener el equipamiento seleccionado por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de Equipamiento con la equipamiento seleccionado
 return render_template("Equipamiento.html", equipamiento=Equipamiento_ingresado)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--Equipamiento.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información del Equipamiento</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de Equipamiento</legend>
        <div class="form-group row">
            {% if Equipamiento %}
            <p><strong>Nombre:</strong> {{ Equipamiento.nombre }}</p>
            <p><strong>Precio:</strong> {{ Equipamiento.precio }}</p>
            {% if (Equipamiento.Nombre == "Futbol") %}
            <p><strong>Talla:</strong> {{ Equipamiento.talla }}</p>
            {% elif (Equipamiento.Nombre== "Baketball") %}
            <p><strong>Talla:</strong> {{ Equipamiento.talla }}</p>
            <p><strong>Material:</strong> {{ Equipamiento.material }}</p>
            {% elif (Equipamiento.Nombre == "Rugby") %}
            <p><strong>Peso:</strong> {{ Equipamiento.peso }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ Equipamiento.descripcion() }}</p>
            {% else %}
            <p>La Equipamiento seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas Equipamiento</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_Equipamiento.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de Equipamiento</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/Equipamiento">
    <legend>Información de Equipamiento</legend>
    <fieldset  class="d-grid" >
      <label for="Equipamiento">Seleccione un Equipamiento:</label>
      <select id="Equipamiento" name="Equipamiento" class="col-form-label col-form-label-sm">
        <option value="Futbol">Equipamiento de Futbol</option>
        <option value="Baketball">Equipamiento de Baketball</option>
        <option value="Rugby">Equipamiento de Rugby</option>
      </select>
      <label for="precio" class="col-form-label col-form-label-sm">Precio:</label>
      <input type="number" id="precio" name="precio" >
      <div id="atributos">
        <label for="talla" class="col-form-label col-form-label-sm">Talla:</label>
        <input type="text" id="talla" name="talla" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const Equipamientoelect = document.getElementById("Equipamiento");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const Equipamiento = Equipamientoelect.value;
      atributosDiv.innerHTML = "";

      if (Equipamiento === "Futbol") {
        atributosDiv.innerHTML += `
            <label for="talla" class="col-form-label col-form-label-sm">Talla:</label>
            <input type="text" id="talla" name="talla">
          `;
      } else if (Equipamiento === "Baketball") {
        atributosDiv.innerHTML += `
            <label for="talla" class="col-form-label col-form-label-sm">Talla:</label>
            <input type="text" id="talla" name="talla">
            <label for="material" class="col-form-label col-form-label-sm">Material:</label>
            <input type="text" id="material" name="material">
          `;
      } else if (Equipamiento === "Rugby") {
        atributosDiv.innerHTML += `
            <label for="peso" class="col-form-label col-form-label-sm">Peso:</label>
            <input type="text" id="peso" name="peso">
          `;
      }
    }
    Equipamientoelect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



