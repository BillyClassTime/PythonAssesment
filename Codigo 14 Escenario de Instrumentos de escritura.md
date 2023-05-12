## Escenario de Instrumentos de escritura: Código 14

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central en la comercialización de instrumentos de escritura:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de las instrumentos.

Las instrumentos que se comercializan son bolígrafos, lápices y rotuladores, pero próximamente se añadirán mas variedades a la comercialización según como vayan siendo cerrados acuerdos con diversos fabricantes.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

```
Instrumentos de escritura: Bolígrafo, Lapiz y Rotulador.
```

``` python
from abc import ABC, abstractmethod

class InstrumentoEscritura(ABC):
    def __init__(self, marca, modelo, color, tinta):
        self.marca = marca
        self.modelo = modelo
        self.color = color
        self.tinta = tinta

    @abstractmethod
    def escribir(self, texto):
        pass

class Boligrafo(InstrumentoEscritura):
    def __init__(self, marca, modelo, color, tinta, punta):
        super().__init__(marca, modelo, color, tinta)
        self.punta = punta

    def escribir(self, texto):
        return f"Escribiendo con un bolígrafo {self.color} de {self.marca} modelo {self.modelo} con punta de {self.punta}mm y tinta {self.tinta}: {texto}"

class Lapiz(InstrumentoEscritura):
    def __init__(self, marca, modelo, color, dureza):
        super().__init__(marca, modelo, color, None)
        self.dureza = dureza

    def escribir(self, texto):
        return f"Escribiendo con un lápiz {self.color} de {self.marca} modelo {self.modelo} con dureza {self.dureza}: {texto}"

class Rotulador(InstrumentoEscritura):
    def __init__(self, marca, modelo, color, punta):
        super().__init__(marca, modelo, color, None)
        self.punta = punta

    def escribir(self, texto):
        return f"Escribiendo con un rotulador {self.color} de {self.marca} modelo {self.modelo} con punta de {self.punta}mm: {texto}"

```

####  Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def instrumentos():
    return render_template("start_instrumentos.html")

@app.route("/instrumentos", methods=['POST'])
def mostrar_instrumentos():
 # Obtener el instrumento seleccionado por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de instrumentos con el instrumento seleccionado
 return render_template("instrumentos.html", instrumento=instrumento_ingresado)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--instrumentos.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de instrumentos de escritura</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de instrumentos</legend>
        <div class="form-group row">
            {% if instrumento %}
            <p><strong>Nombre:</strong> {{ instrumento.nombre }}</p>
            <p><strong>Marca:</strong> {{ instrumento.marca }}</p>
            <p><strong>Color:</strong> {{ instrumento.color }}</p>
            <p><strong>Tinta:</strong> {{ instrumento.tinta }}</p>
            {% if (instrumento.Nombre == "boligrafo") %}
            <p><strong>punta:</strong> {{ instrumento.punta }}</p>
            {% elif (instrumento.Nombre== "lápiz") %}
            <p><strong>Dureza:</strong> {{ instrumento.dureza }}</p>
            {% elif (instrumento.Nombre == "rotulador") %}
            <p><strong>Punta:</strong> {{ instrumento.punta }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ instrumento.escribir() }}</p>
            {% else %}
            <p>La instrumento seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas instrumentos</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_instrumentos.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de instrumentos de escritura</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/instrumentos">
    <legend>Información de instrumentos de escritura</legend>
    <fieldset  class="d-grid" >
      <label for="instrumento">Selecciona una instrumento:</label>
      <select id="instrumento" name="instrumento" class="col-form-label col-form-label-sm">
        <option value="boligrafo">Boligrafo</option>
        <option value="lápiz">Lápiz</option>
        <option value="rotulador">Rotulador</option>
      </select>
      <label for="marca" class="col-form-label col-form-label-sm">Marca:</label>
      <input type="text" id="marca" name="marca" >
      <label for="color" class="col-form-label col-form-label-sm">Color:</label>
      <input type="text" id="color" name="color" >     
      <label for="tinta" class="col-form-label col-form-label-sm">Tinta:</label>
      <input type="text" id="tinta" name="tinta" >        
      <div id="atributos">
        <label for="punta" class="col-form-label col-form-label-sm">Punta:</label>
        <input type="text" id="punta" name="punta" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const instrumentoSelect = document.getElementById("instrumento");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const instrumento = instrumentoSelect.value;
      atributosDiv.innerHTML = "";

      if (instrumento === "boligrafo") {
        atributosDiv.innerHTML += `
        <label for="punta" class="col-form-label col-form-label-sm">Punta:</label>
        <input type="text" id="punta" name="punta" >
          `;
      } else if (instrumento === "lápiz") {
        atributosDiv.innerHTML += `
            <label for="dureza" class="col-form-label col-form-label-sm">Dureza:</label>
            <input type="text" id="dureza" name="dureza">
          `;
      } else if (instrumento === "rotulador") {
        atributosDiv.innerHTML += `
            <label for="punta" class="col-form-label col-form-label-sm">Punta:</label>
            <input type="text" id="punta" name="punta">
          `;
      }
    }
    instrumentoSelect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



