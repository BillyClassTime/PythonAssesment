## Escenario de Libros: Código 15

Usted ha sido contratado para trabajar como `python developer` en una empresa local de su ciudad.

El negocio central es la comercialización de libros:

Usted iniciará un proyecto que incluirá la elaboración de `site` en Internet para la gestión de los libros.

Las libros que se comercializan son Novelas, Ensayos y Poesías, pero próximamente se añadirán mas variedades a la comercialización según como vayan siendo cerrados acuerdos con los editoriales más próximos.

Debe crear el proyecto de iniciación para comenzar a desarrollar en las siguientes jornadas toda la aplicación.

Hoy deberá entregar el proyecto web, con la jerarquía de clases, y con el funcionamiento de la primera página web; incluyendo toda la información proporcionada en este documento. Solo añadirá lo faltante.

- Jerarquía de clases

  ```
  Libros: novela, ensayo, poesía.
  ```

  ```python
  from abc import ABC, abstractmethod
  
  class Libros(ABC):
      def init(self, clase, titulo, autor):
          self.clase = clase
          self.titulo = titulo
          self.autor = autor   
      @abstractmethod
      def descripcion(self):
          pass
  
  class Novelas(Libros):
      def init(self, clase, titulo, autor, genero):
      super().init(clase, titulo, autor)
      self.genero = genero    
      def descripcion(self):
          return f"{self.titulo} es una novela escrita por {self.autor} del género {self.genero}."
      
  class Ensayo(Libros):
      def init(self, clase, titulo, autor, tema):
      super().init(clase, titulo, autor)
      self.tema = tema
  
      def descripcion(self):
          return f"{self.titulo} es un ensayo escrito por {self.autor} sobre el tema {self.tema}."
  
  class Poesia(Libros):
      def init(self,clase, titulo, autor, estilo):
      super().init(clase, titulo, autor)
      self.estilo = estilo    
  def descripcion(self):
      return f"{self.titulo} es un libro de poesía escrito por {self.autor} en el estilo {self.estilo}."    
  ```

#### Aplicación principal

```python
from flask import Flask, request, render_template

app = Flask(__name__,template_folder='html')

@app.route("/")
def libros():
    return render_template("start_libros.html")

@app.route("/libros", methods=['POST'])
def mostrar_libros():
 # Obtener la clase de libro seleccionada por el usuario

 # Insertar el código aquí
        
 # Renderizar la página de libros con la libro seleccionado
 return render_template("libros.html", libro=libro_ingresado)


if __name__ == '__main__':
   app.run(debug=True)
```

#### Páginas Web

```html
<!--libros.html-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Información de la libro</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
    <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
    <fieldset>
        <legend>Información de libros</legend>
        <div class="form-group row">
            {% if libro %}
            <p><strong>Clase:</strong> {{ libro.clase }}</p>
            <p><strong>Título:</strong> {{ libro.título }}</p>
            {% if (libro.clase == "Novela") %}
            <p><strong>Genero:</strong> {{ libro.genero }}</p>
            {% elif (libro.clase == "Ensayo") %}
            <p><strong>Tema:</strong> {{ libro.tema }}</p>
            {% elif (libro.clase == "Poesia") %}
            <p><strong>Estilo:</strong> {{ libro.estilo }}</p>
            {% endif %}
            <p><strong>Descripcion:</strong> {{ libro.descripcion() }}</p>
            {% else %}
            <p>La libro seleccionada no fue encontrada en la lista.</p>
            {% endif %}
            <form method="get" action="/">
                <button type="submit" class="btn btn-primary">Mas libros</button>
            </form>
        </div>
    </fieldset>
</body>
</html>

<!-- start_libros.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Información de libros</title>
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  <link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}" />
</head>

<body>
  <form method="post" action="/libros">
    <legend>Información de libros</legend>
    <fieldset  class="d-grid" >
      <label for="libro">Selecciona la clase de libro:</label>
      <select id="clase" name="clase" class="col-form-label col-form-label-sm">
        <option value="Novela">Novela</option>
        <option value="Ensayo">Ensayo</option>
        <option value="Poesia">Poesía</option>
      </select>
      <label for="titulo" class="col-form-label col-form-label-sm">Título:</label>
      <input type="text" id="titulo" name="titulo" >
      <label for="autor" class="col-form-label col-form-label-sm">Autor:</label>
      <input type="text" id="autor" name="autor" >
      <div id="atributos">
        <label for="genero" class="col-form-label col-form-label-sm">Genero:</label>
        <input type="text" id="genero" name="genero" >
      </div>
    </fieldset>
    <button type="submit" class="btn btn-primary">Revisar</button>
  </form>

  <script>
    const libroselect = document.getElementById("clase");
    const atributosDiv = document.getElementById("atributos");

    function mostrarAtributos() {
      const clase = libroselect.value;
      atributosDiv.innerHTML = "";

      if (clase === "Novela") {
        atributosDiv.innerHTML += `
            <label for="genero" class="col-form-label col-form-label-sm">Genero:</label>
            <input type="text" id="genero" name="genero">
          `;
      } else if (clase === "Ensayo") {
        atributosDiv.innerHTML += `
            <label for="tema" class="col-form-label col-form-label-sm">Tema:</label>
            <input type="text" id="tema" name="tema">
          `;
      } else if (clase === "Poesia") {
        atributosDiv.innerHTML += `
            <label for="poesia" class="col-form-label col-form-label-sm">Poesía:</label>
            <input type="text" id="poesia" name="poesia">
          `;
      }
    }
    libroselect.addEventListener("change", mostrarAtributos);
  </script>
</body>

</html>
```



