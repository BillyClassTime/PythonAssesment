## Escenario de Alimentos: Código 08

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central es la comercialización de alimentos:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las alimentos.

Las alimentos que se comercializan son pizzas, hamburguesas y sushis, pero próximamente se añadirán mas variedades a la comercialización según como vayan siendo cerrados acuerdos diferentes chefs.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases:

```
Alimentos: pizza, hamburguesa, sushi.
```

``` python
from abc import ABC, abstractmethod

class Alimentos(ABC):
    def __init__(self, nombre, precio):
        self.nombre = nombre
        self.precio = precio

    @abstractmethod
    def descripcion(self):
        pass

class Pizza(Alimentos):
    def __init__(self, nombre, precio, ingredientes):
        super().__init__(nombre, precio)
        self.ingredientes = ingredientes

    def descripcion(self):
        print(f"La pizza {self.nombre} tiene los siguientes ingredientes: {self.ingredientes}. Su precio es {self.precio}.")

class Hamburguesa(Alimentos):
    def __init__(self, nombre, precio, tipo_carne):
        super().__init__(nombre, precio)
        self.tipo_carne = tipo_carne

    def descripcion(self):
        print(f"La hamburguesa {self.nombre} está hecha con carne de {self.tipo_carne}. Su precio es {self.precio}.")

class Sushi(Alimentos):
    def __init__(self, nombre, precio, tipo_sushi):
        super().__init__(nombre, precio)
        self.tipo_sushi = tipo_sushi

    def descripcion(self):
        print(f"El sushi {self.nombre} es de tipo {self.tipo_sushi}. Su precio es {self.precio}.")
```

####  Aplicación principal

```python
efrom flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def alimentos():
    return render_template("start_alimentos.html")

@app.route("/alimentos", methods=['POST'])
def mostrar_alimentos():
 # Obtener la alimento seleccionada por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de alimentos con el alimento seleccionado
 return render_template("alimentos.html", alimento=alimento_ingresado)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--alimentos.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la alimento</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de alimentos</legend>
        <div class="form-group row">
            {% if alimento %}
            <p><strong>Nombre:</strong> {{ alimento.nombre }}</p>
            <p><strong>Precio:</strong> {{ alimento.precio }}</p>
            {% if (alimento.Nombre == "pizza") %}
            <p><strong>Ingredientes:</strong> {{ alimento.ingredientes }}</p>
            {% elif (alimento.Nombre== "hamburguesa") %}
            <p><strong>Tipo de carne:</strong> {{ alimento.tipo_carne }}</p>
            {% elif (alimento.Nombre == "sushi") %}
            <p><strong>Tipo Sushi:</strong> {{ alimento.tipo_sushi }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ alimento.descripcion() }}</p>
            {% else %}
            <p>La alimento seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas alimentos</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_alimentos.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de alimentos</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/alimentos">
    <legend>Información de alimentos</legend>
    <fieldset  class="d-grid" >
      <label for="alimento">Selecciona una alimento:</label>
      <select id="alimento" name="alimento" class="col-form-label col-form-label-sm">
        <option value="pizza">Pizza</option>
        <option value="hamburguesa">Hamburguesa</option>
        <option value="sushi">Sushi</option>
      </select>
      <label for="Precio" class="col-form-label col-form-label-sm">Precio:</label>
      <input type="number" id="precio" name="precio" >
      <div id="atributos">
        <label for="ingredientes" class="col-form-label col-form-label-sm">Ingredientes:</label>
        <input type="text" id="ingredientes" name="ingredientes" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const alimentoselect = document.getElementById("alimento");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const alimento = alimentoselect.value;
      atributosDiv.innerHTML = "";

      if (alimento === "pizza") {
        atributosDiv.innerHTML += `
        <label for="ingredientes" class="col-form-label col-form-label-sm">Ingredientes:</label>
        <input type="text" id="ingredientes" name="ingredientes" >
          `;
      } else if (alimento === "hamburguesa") {
        atributosDiv.innerHTML += `
            <label for="tipo_carne" class="col-form-label col-form-label-sm">Tipo Carne:</label>
            <input type="text" id="tipo_carne" name="tipo_carne">
          `;
      } else if (alimento === "sushi") {
        atributosDiv.innerHTML += `
            <label for="tipo_sushi" class="col-form-label col-form-label-sm">Tipo_sushi:</label>
            <input type="text" id="tipo_sushi" name="tipo_sushi">
          `;
      }
    }
    alimentoselect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



