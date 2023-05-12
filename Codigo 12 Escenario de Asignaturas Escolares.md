## Escenario de Asignaturas Escolares: Código 12

Usted ha sido contratado para trabajar como `python developer` en un centro educativo local de su ciudad.

Las actividades principales se centrarán en la gestión de los temas académicos.

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las asignaturas.

Las asignaturas que se gestionarán serán matemáticas, ciencias y historias, pero próximamente se añadirán mas asignaturas a medida que se cierren acuerdos con los demás docentes. 

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases

```
Asignaturas escolares: matemáticas, ciencias, historia.
```

``` python
from abc import ABC, abstractmethod

class Asignaturas(ABC):
    def __init__(self, nombre, profesor, creditos):
        self.nombre = nombre
        self.profesor = profesor

    @abstractmethod
    def descripcion(self):
        pass

class Matematicas(Asignaturas):
    def __init__(self, nombre, profesor, creditos, nivel):
        super().__init__(nombre, profesor, creditos)
        self.nivel = nivel

    def descripcion(self):
        return f"{self.nombre} es una asignatura de nivel {self.nivel}, impartida por el profesor {self.profesor} y otorga {self.creditos} créditos."

class Ciencias(Asignaturas):
    def __init__(self, nombre, profesor, creditos, laboratorio):
        super().__init__(nombre, profesor, creditos)
        self.laboratorio = laboratorio

    def descripcion(self):
        if self.laboratorio:
            return f"{self.nombre} es una asignatura con laboratorio, impartida por el profesor {self.profesor} y otorga {self.creditos} créditos."
        else:
            return f"{self.nombre} es una asignatura teórica, impartida por el profesor {self.profesor} y otorga {self.creditos} créditos."

class Historia(Asignaturas):
    def __init__(self, nombre, profesor, creditos, epoca):
        super().__init__(nombre, profesor, creditos)
        self.epoca = epoca

    def descripcion(self):
        return f"{self.nombre} es una asignatura que estudia la época {self.epoca}, impartida por el profesor {self.profesor} y otorga {self.creditos} créditos."
```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def asignaturas():
    return render_template("start_asignaturas.html")

@app.route("/asignaturas", methods=['POST'])
def mostrar_asignaturas():
 # Obtener la asignatura seleccionada por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de asignaturas con la asignatura seleccionada
 return render_template("asignaturas.html", asignatura=asignatura_ingresada)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--asignaturas.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la asignatura</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de asignaturas</legend>
        <div class="form-group row">
            {% if asignatura %}
            <p><strong>Nombre:</strong> {{ asignatura.nombre }}</p>
            <p><strong>Profesor:</strong> {{ asignatura.profesor }}</p>
            {% if (asignatura.Nombre == "matemáticas") %}
            <p><strong>Nivel:</strong> {{ asignatura.nivel }}</p>
            {% elif (asignatura.Nombre== "ciencia") %}
            <p><strong>Laboratorio:</strong> {{ asignatura.laboratorio }}</p>
            {% elif (asignatura.Nombre == "historia") %}
            <p><strong>Época:</strong> {{ asignatura.epoca }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ asignatura.descripcion() }}</p>
            {% else %}
            <p>La asignatura seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas asignaturas</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_asignaturas.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de asignaturas</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/asignaturas">
    <legend>Información de asignaturas</legend>
    <fieldset  class="d-grid" >
      <label for="asignatura">Selecciona una asignatura:</label>
      <select id="asignatura" name="asignatura" class="col-form-label col-form-label-sm">
        <option value="matemáticas">Matemáticas</option>
        <option value="ciencias">Ciencia</option>
        <option value="historia">Historia</option>
      </select>
      <label for="profesor" class="col-form-label col-form-label-sm">profesor:</label>
      <input type="text" id="procesor" name="profesor" >
      <div id="atributos">
        <label for="nivel" class="col-form-label col-form-label-sm">nivel:</label>
        <input type="text" id="nivel" name="nivel" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const asignaturaSelect = document.getElementById("asignatura");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const asignatura = asignaturaSelect.value;
      atributosDiv.innerHTML = "";

      if (asignatura === "matemática") {
        atributosDiv.innerHTML += `
        <label for="nivel" class="col-form-label col-form-label-sm">nivel:</label>
        <input type="text" id="nivel" name="nivel" >
          `;
      } else if (asignatura === "ciencia") {
        atributosDiv.innerHTML += `
            <label for="laboratorio" class="col-form-label col-form-label-sm">Laboratorio:</label>
            <input type="text" id="laboratorio" name="laboratorio">
          `;
      } else if (asignatura === "historia") {
        atributosDiv.innerHTML += `
            <label for="epoca" class="col-form-label col-form-label-sm">Epoca:</label>
            <input type="text" id="epoca" name="epoca">
          `;
      }
    }
    asignaturaSelect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



