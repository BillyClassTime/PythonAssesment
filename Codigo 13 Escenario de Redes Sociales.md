## Escenario de Redes Sociales: Código 13

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

La actividad principal se encuentra al rededor de las Redes Sociales:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las redes sociales.

Las redes  sociales que se gestionarán son Facebook, Twitter y Instagram, pero próximamente se añadirán otras redes sociales, conforme vaya creciendo el proyecto.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases

```
Redes sociales: Facebook, Twitter, Instagram.
```

``` python
from abc import ABC, abstractmethod

class RedesSociales(ABC):
    def __init__(self, nombre, url, usuarios):
        self.nombre = nombre
        self.url = url

        @abstractmethod
    def descripcion(self):
        pass

class Facebook(RedesSociales):
    def __init__(self, nombre, url, usuarios, grupos):
        super().__init__(nombre, url, usuarios)
        self.grupos = grupos

    def descripcion(self):
        return f"{self.nombre} es una red social con {self.usuarios} usuarios, que se encuentra en {self.url}. Además, cuenta con {self.grupos} grupos."

class Twitter(RedesSociales):
    def __init__(self, nombre, url, usuarios, hashtags):
        super().__init__(nombre, url, usuarios)
        self.hashtags = hashtags

    def descripcion(self):
        return f"{self.nombre} es una red social con {self.usuarios} usuarios, que se encuentra en {self.url}. Además, cuenta con los hashtags {self.hashtags}."

class Instagram(RedesSociales):
    def __init__(self, nombre, url, usuarios, filtros):
        super().__init__(nombre, url, usuarios)
        self.filtros = filtros

    def descripcion(self):
        return f"{self.nombre} es una red social con {self.usuarios} usuarios, que se encuentra en {self.url}. Además, cuenta con los filtros {self.filtros}."
```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def redSocials():
    return render_template("start_redessociales.html")

@app.route("/redsocial", methods=['POST'])
def mostrar_redSocials():
 # Obtener la red social seleccionada por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de redes sociales con la red social seleccionada
 return render_template("redsocial.html", redSocial=redSocial_ingresada)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--redsocial.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la red social</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de la red social</legend>
        <div class="form-group row">
            {% if redSocial %}
            <p><strong>Nombre:</strong> {{ redSocial.nombre }}</p>
            <p><strong>url:</strong> {{ redSocial.url }}</p>
            {% if (redSocial.Nombre == "facebook") %}
            <p><strong>grupos:</strong> {{ redSocial.grupos }}</p>
            {% elif (redSocial.Nombre== "Twitter") %}
            <p><strong>hashtags:</strong> {{ redSocial.hashtags }}</p>
            {% elif (redSocial.Nombre == "Instagram") %}
            <p><strong>filtros:</strong> {{ redSocial.filtros }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ redSocial.descripcion() }}</p>
            {% else %}
            <p>La redSocial seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas redSocials</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_redessociales.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de redSocials</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/redsocial">
    <legend>Información de redSocials</legend>
    <fieldset  class="d-grid" >
      <label for="redSocial">Selecciona una red social:</label>
      <select id="redSocial" name="redSocial" class="col-form-label col-form-label-sm">
        <option value="facebook">Facebook</option>
        <option value="Twitter">Twitter</option>
        <option value="Instagram">Instagram</option>
      </select>
      <label for="url" class="col-form-label col-form-label-sm">Url:</label>
      <input type="text" id="url" name="url" >
      <div id="atributos">
        <label for="grupos" class="col-form-label col-form-label-sm">Grupos:</label>
        <input type="text" id="grupos" name="grupos" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const redSocialSelect = document.getElementById("redSocial");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const redSocial = redSocialSelect.value;
      atributosDiv.innerHTML = "";

      if (redSocial === "facebook") {
        atributosDiv.innerHTML += `
        <label for="grupos" class="col-form-label col-form-label-sm">Grupos:</label>
        <input type="text" id="grupos" name="grupos" >
          `;
      } else if (redSocial === "Twitter") {
        atributosDiv.innerHTML += `
            <label for="hashtags" class="col-form-label col-form-label-sm">Hash Tags:</label>
            <input type="text" id="hashtags" name="hashtags">
          `;
      } else if (redSocial === "Instagram") {
        atributosDiv.innerHTML += `
            <label for="filtros" class="col-form-label col-form-label-sm">filtros:</label>
            <input type="text" id="filtros" name="filtros">
          `;
      }
    }
    redSocialSelect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



