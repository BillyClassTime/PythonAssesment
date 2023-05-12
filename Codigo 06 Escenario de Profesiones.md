## Escenario de Profesiones: Código 06

Usted ha sido contratado para trabajar como `python developer` en la secretaría de empleo de su localidad.

Se controlará la información de empleo por profesiones.

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de  la información de empleo de las profesiones.

Las profesiones que se gestionarán inicialmente son Ingenieros, Médicos y Abogados, pero próximamente se añadirán otra profesiones hasta cubrir todos los sectores económicos y sociales.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases

```
Profesiones: Ingeniero, Médico y Abogado.
```

``` python
from abc import ABC, abstractmethod

class Profesion(ABC):
    def __init__(self, nombre, area):
        self.nombre = nombre
        self.area = area

    @abstractmethod
    def descripcion(self):
        pass

class Ingeniero(Profesion):
    def __init__(self, nombre, area, especialidad):
        super().__init__(nombre, area)
        self.especialidad = especialidad

    def descripcion(self):
        print(f"El ingeniero {self.nombre} es especialista en {self.especialidad}, dentro del área de {self.area}.")

class Medico(Profesion):
    def __init__(self, nombre, area, especialidad):
        super().__init__(nombre, area)
        self.especialidad = especialidad

    def descripcion(self):
        print(f"El médico {self.nombre} es especialista en {self.especialidad}, dentro del área de {self.area}.")

class Abogado(Profesion):
    def __init__(self, nombre, area, especialidad):
        super().__init__(nombre, area)
        self.especialidad = especialidad

    def descripcion(self):
        print(f"El abogado {self.nombre} es especialista en {self.especialidad}, dentro del área de {self.area}.")
```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def profesiones():
    return render_template("start_profesiones.html")

@app.route("/profesiones", methods=['POST'])
def mostrar_profesiones():
 # Obtener la profesión seleccionada por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de profesiones con la profesión seleccionada
 return render_template("profesiones.html", profesión=profesión_ingresada)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--profesiones.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la profesión</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de profesiones</legend>
        <div class="form-group row">
            {% if profesión %}
            <p><strong>Nombre:</strong> {{ profesión.nombre }}</p>
            <p><strong>Area:</strong> {{ profesión.area }}</p>
            {% if (profesión.Nombre == "Ingeniero") %}
            <p><strong>Sector:</strong> {{ profesión.sector }}</p>
            {% elif (profesión.Nombre== "Médico") %}
            <p><strong>Especialidad:</strong> {{ profesión.especialidad }}</p>
            {% elif (profesión.Nombre == "Abogado") %}
            <p><strong>Rama:</strong> {{ profesión.rama }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ profesión.descripcion() }}</p>
            {% else %}
            <p>La profesión seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas profesiones</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_profesiones.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de profesiones</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/profesiones">
    <legend>Información de profesiones</legend>
    <fieldset  class="d-grid" >
      <label for="profesión">Selecciona una profesión:</label>
      <select id="profesión" name="profesión" class="col-form-label col-form-label-sm">
        <option value="Ingeniero">Ingeniero</option>
        <option value="Médico">Médico</option>
        <option value="Abogado">Abogado</option>
      </select>
      <label for="area" class="col-form-label col-form-label-sm">Area:</label>
      <input type="text" id="area" name="area" >
      <div id="atributos">
        <label for="sector" class="col-form-label col-form-label-sm">Sector:</label>
        <input type="text" id="sector" name="sector" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const profesioneselect = document.getElementById("profesión");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const profesión = profesioneselect.value;
      atributosDiv.innerHTML = "";

      if (profesión === "Ingeniero") {
        atributosDiv.innerHTML += `
        <label for="sector" class="col-form-label col-form-label-sm">Sector:</label>
        <input type="text" id="sector" name="sector" >
          `;
      } else if (profesión === "Médico") {
        atributosDiv.innerHTML += `
            <label for="especialidad" class="col-form-label col-form-label-sm">Especialidad:</label>
            <input type="text" id="especialidad" name="especialidad">
          `;
      } else if (profesión === "Abogado") {
        atributosDiv.innerHTML += `
            <label for="rama" class="col-form-label col-form-label-sm">Rama:</label>
            <input type="text" id="rama" name="rama">
          `;
      }
    }
    profesioneselect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



