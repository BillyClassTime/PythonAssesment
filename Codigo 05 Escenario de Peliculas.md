## Escenario de Películas: Código 05

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central es la comercialización de películas:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las películas.

Las películas que se comercializan son acción, comedia y drama, pero próximamente se añadirán mas variedades a la comercialización según como vayan siendo cerrados acuerdos diferentes productoras.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de Clases

```
Películas: acción, comedia, drama.
```

``` python
from abc import ABC, abstractmethod

class Pelicula(ABC):
    def __init__(self, nombre, anyo):
        self.nombre = nombre
        self.anyo = anyo

    @abstractmethod
    def descripcion(self):
        pass

class Accion(Pelicula):
    def __init__(self, nombre, anyo, protagonista):
        super().__init__(nombre, anyo)
        self.protagonista = protagonista

    def descripcion(self):
        print(f"La película de acción '{self.nombre}', estrenada en {self.anyo}, cuenta con el protagonismo de {self.protagonista}. Es una película emocionante y llena de acción.")

class Comedia(Pelicula):
    def __init__(self, nombre, anyo, director):
        super().__init__(nombre, anyo)
        self.director = director

    def descripcion(self):
        print(f"La comedia '{self.nombre}', estrenada en {self.anyo}, fue dirigida por {self.director}. Es una película divertida y con un buen sentido del humor.")

class Drama(Pelicula):
    def __init__(self, nombre, anyo, tema):
        super().__init__(nombre, anyo)
        self.tema = tema

    def descripcion(self):
        print(f"La película dramática '{self.nombre}', estrenada en {self.anyo}, trata el tema de {self.tema}. Es una película emotiva y profunda.")
```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def películas():
    return render_template("start_películas.html")

@app.route("/películas", methods=['POST'])
def mostrar_películas():
 # Obtener la película seleccionada por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de películas con la película seleccionada
 return render_template("películas.html", película=película_ingresada)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--películas.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la película</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de películas</legend>
        <div class="form-group row">
            {% if película %}
            <p><strong>Nombre:</strong> {{ película.nombre }}</p>
            <p><strong>Año:</strong> {{ película.anyo }}</p>
            {% if (película.Nombre == "Acción") %}
            <p><strong>Protagonista:</strong> {{ película.protagonista }}</p>
            {% elif (película.Nombre== "Comédia") %}
            <p><strong>Director:</strong> {{ película.director }}</p>
            {% elif (película.Nombre == "Drama") %}
            <p><strong>Dulzor:</strong> {{ película.tema }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ película.descripcion() }}</p>
            {% else %}
            <p>La película seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas películas</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_películas.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de películas</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/películas">
    <legend>Información de películas</legend>
    <fieldset  class="d-grid" >
      <label for="película">Selecciona una película:</label>
      <select id="película" name="película" class="col-form-label col-form-label-sm">
        <option value="Acción">Acción</option>
        <option value="Comédia">Comédia</option>
        <option value="Drama">Drama</option>
      </select>
      <label for="anyo" class="col-form-label col-form-label-sm">Año:</label>
      <input type="number" id="anyo" name="anyo" >
      <div id="atributos">
        <label for="protagonista" class="col-form-label col-form-label-sm">Protagonista:</label>
        <input type="text" id="protagonista" name="protagonista" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const películaselect = document.getElementById("película");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const película = películaselect.value;
      atributosDiv.innerHTML = "";

      if (película === "Acción") {
        atributosDiv.innerHTML += `
         <label for="protagonista" class="col-form-label col-form-label-sm">Protagonista:</label>
        <input type="text" id="protagonista" name="protagonista" >
          `;
      } else if (película === "Comédia") {
        atributosDiv.innerHTML += `
            <label for="director" class="col-form-label col-form-label-sm">Director:</label>
            <input type="text" id="director" name="director">
          `;
      } else if (película === "Drama") {
        atributosDiv.innerHTML += `
            <label for="tema" class="col-form-label col-form-label-sm">Tema:</label>
            <input type="text" id="tema" name="tema">
          `;
      }
    }
    películaselect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



