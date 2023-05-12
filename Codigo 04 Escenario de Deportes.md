## Escenario de Deportes: Código 04

Usted ha sido contratado para trabajar como `python developer` en la secretaría de deportes de su ciudad.

La actividad central es el control de los diferentes deportes.

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para el control de los deportes en su localidad.

Las deportes que iniciarán son Fútbol, Baloncesto y el Béisbol, pero próximamente se añadirán mas deportes, a medida que se vayan incorporando nueva información a la secretaría.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

```
Deportes: fútbol, baloncesto, béisbol.
```

``` python
from abc import ABC, abstractmethod

class Deportes(ABC):
    def __init__(self, nombre, jugadores):
        self.nombre = nombre
        self.jugadores = jugadores

    @abstractmethod
    def descripcion(self):
        pass

class Futbol(Deportes):
    def __init__(self, nombre, jugadores, posicion_arquero):
        super().__init__(nombre, jugadores)
        self.posicion_arquero = posicion_arquero

    def descripcion(self):
        print(f"El fútbol es un deporte de equipo con {self.jugadores} jugadores, donde el arquero se coloca en la posición {self.posicion_arquero}.")

class Baloncesto(Deportes):
    def __init__(self, nombre, jugadores, altura_aro):
        super().__init__(nombre, jugadores)
        self.altura_aro = altura_aro

    def descripcion(self):
        print(f"El baloncesto es un deporte de equipo con {self.jugadores} jugadores, donde el aro se encuentra a una altura de {self.altura_aro} metros.")

class Beisbol(Deportes):
    def __init__(self, nombre, jugadores, entrada_extra):
        super().__init__(nombre, jugadores)
        self.entrada_extra = entrada_extra

    def descripcion(self):
        print(f"El béisbol es un deporte de equipo con {self.jugadores} jugadores, donde en caso de empate se puede jugar una entrada extra, conocida como {self.entrada_extra}.")
```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def deportes():
    return render_template("start_deportes.html")

@app.route("/deportes", methods=['POST'])
def mostrar_deportes():
 # Obtener el deporte seleccionado por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de deportes con el deporte seleccionado
 return render_template("deportes.html", deporte=deporte_ingresado)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--deportes.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información del deporte</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información del deporte</legend>
        <div class="form-group row">
            {% if deporte %}
            <p><strong>Nombre:</strong> {{ deporte.nombre }}</p>
            <p><strong>Jugadores:</strong> {{ deporte.jugadores }}</p>
            {% if (deporte.Nombre == "Futbol") %}
            <p><strong>Posicion Portero:</strong> {{ deporte.posicion_portero }}</p>
            {% elif (deporte.Nombre== "Baloncesto") %}
            <p><strong>Altura aro:</strong> {{ deporte.altura_aro }}</p>
            {% elif (deporte.Nombre == "Beisbol") %}
            <p><strong>Entrada extra:</strong> {{ deporte.entrada_extra }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ deporte.descripcion() }}</p>
            {% else %}
            <p>La deporte seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas deportes</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_deportes.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de deportes</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/deportes">
    <legend>Información de deportes</legend>
    <fieldset  class="d-grid" >
      <label for="deporte">Selecciona una deporte:</label>
      <select id="deporte" name="deporte" class="col-form-label col-form-label-sm">
        <option value="Futbol">Futbol</option>
        <option value="Baloncesto">Baloncesto</option>
        <option value="Beisbol">Beisbol</option>
      </select>
      <label for="jugadores" class="col-form-label col-form-label-sm">Jugadores:</label>
      <input type="text" id="jugadores" name="jugadores" >
      <div id="atributos">
          <label for="posicion_portero" class="col-form-label col-form-label-sm">Posición portero:</label>
      <input type="text" id="posicion_portero" name="posicion_portero" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const deporteselect = document.getElementById("deporte");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const deporte = deporteselect.value;
      atributosDiv.innerHTML = "";

      if (deporte === "Futbol") {
        atributosDiv.innerHTML += `
 <label for="posicion_portero" class="col-form-label col-form-label-sm">Posición portero:</label>
      <input type="text" id="posicion_portero" name="posicion_portero" >
          `;
      } else if (deporte === "Baloncesto") {
        atributosDiv.innerHTML += `
            <label for="altura_aro" class="col-form-label col-form-label-sm">Altura aro:</label>
            <input type="text" id="altra_aro" name="altura_aro">
          `;
      } else if (deporte === "Beisbol") {
        atributosDiv.innerHTML += `
            <label for="entrada_extra" class="col-form-label col-form-label-sm">Entrada extra:</label>
            <input type="text" id="entrada_extra" name="entrada_extra">
          `;
      }
    }
    deporteselect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



