<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rutina Arnold Split - Antony</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@700&display=swap" rel="stylesheet"> <!-- Añadido -->
  <style>
    body {
      font-family: 'Poppins', sans-serif; /* Cambiado */
      margin: 0;
      padding: 0;
      transition: background-color 0.3s, color 0.3s;
      background-color: #f8f8f8;
      color: #333;
      position: relative;
    }
    /* Modo Oscuro */
    body.dark-mode {
      background-color: #333;
      color: #f8f8f8;
    }
    h1 {
      text-align: center;
      margin-top: 30px;
      color: inherit;
    }
    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      background-color: #fff;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      transition: background-color 0.3s, box-shadow 0.3s;
    }
    /* Modo Oscuro */
    .container.dark-mode {
      background-color: #444;
      box-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
    }
    table {
      width: 100%;
      color: inherit;
      border-collapse: collapse;
    }
    th, td {
      padding: 8px;
      border-bottom: 1px solid #ddd;
    }
    th {
      text-align: left;
      color: inherit;
    }
    .form-group {
      margin-bottom: 15px;
    }
    label {
      font-weight: bold;
      color: inherit;
    }
    input[type="text"] {
      width: 100%;
      padding: 8px;
      border-radius: 4px;
      border: 1px solid #ccc;
      color: inherit;
      background-color: #fff;
    }
    button {
      padding: 10px 20px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      transition: background-color 0.3s;
      margin-top: 10px; /* Añadido */
    }
    button:hover {
      background-color: #45a049;
    }
    .rutinaBox {
      border: 1px solid #ddd;
      padding: 15px;
      margin-top: 20px;
      border-radius: 8px;
      background-color: #f8f8f8;
      position: relative; /* Añadido */
    }
    /* Modo Oscuro */
    .rutinaBox.dark-mode {
      background-color: #666;
      border-color: #888;
    }
    .rutinaBox h2 {
      margin-top: 0;
      margin-bottom: 10px;
      font-size: 20px;
      color: inherit;
    }
    .rutinaEntry {
      margin-bottom: 8px;
      color: inherit;
    }
    a {
      color: #007bff;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
    .green-bg {
      background-color: #aaffaa;
    }
    .red-bg {
      background-color: #ffaaaa;
    }
    /* Líneas de Separación */
    .separator {
      border-top: 1px solid #ccc;
      margin-top: 20px;
      margin-bottom: 20px;
    }
    .edit-button {
      position: absolute;
      top: 10px;
      right: 10px;
    }
    /* Estilo para resaltar la palabra "rutina" */
    .highlight {
      font-weight: bold;
      text-decoration: underline;
    }
  </style>
</head>
<body class="light-mode">
  <h1>Rutina Arnold Split - Antony</h1>
  <div class="container">
    <h2 style="color: inherit;">Agrega tu rutina aquí</h2>
    <table>
      <tr>
        <th style="color: inherit;">Día:</th>
        <td><input type="text" id="dia" name="dia" required></td>
      </tr>
      <tr>
        <th style="color: inherit;">Rutina:</th>
        <td><input type="text" id="rutina" name="rutina" required></td>
      </tr>
      <tr>
        <th style="color: inherit;">Ejercicio:</th>
        <td><input type="text" id="ejercicio" name="ejercicio" required></td>
      </tr>
      <tr>
        <th style="color: inherit;">Series:</th>
        <td><input type="text" id="series" name="series" required></td>
      </tr>
      <tr>
        <th style="color: inherit;">Descansos:</th>
        <td><input type="text" id="descansos" name="descansos" required></td>
      </tr>
      <tr>
        <th style="color: inherit;">Video Demostración:</th>
        <td><input type="text" id="video" name="video" placeholder="https://www.youtube.com/watch?v=... o https://www.tiktok.com/@usuario/video/..."></td>
      </tr>
    </table>
    <button onclick="agregarRutina()">Agregar Rutina</button> <!-- Modificado -->
    <!-- Línea de Separación -->
    <div class="separator"></div>
    <!-- Cuadros de Rutinas -->
    <div id="rutinasContainer"></div>
  </div>
  
  <script>
    function agregarRutina() {
      var dia = document.getElementById("dia").value;
      var rutina = document.getElementById("rutina").value;
      var ejercicio = document.getElementById("ejercicio").value;
      var series = document.getElementById("series").value;
      var descansos = document.getElementById("descansos").value;
      var video = document.getElementById("video").value;
      
      var rutinasContainer = document.getElementById("rutinasContainer");
      var diaBox = document.getElementById(dia.toLowerCase());
      
      if (!diaBox) {
        diaBox = document.createElement("div");
        diaBox.id = dia.toLowerCase();
        diaBox.classList.add("rutinaBox");
        if (dia.toLowerCase() === obtenerDiaActual()) {
          diaBox.classList.add("green-bg");
        } else {
          diaBox.classList.add("red-bg");
        }
        diaBox.innerHTML = `<h2>${dia}<button class="edit-button" onclick="editarRutina('${dia.toLowerCase()}')">Editar</button></h2>`; // Modificado
        rutinasContainer.appendChild(diaBox);
      }
      
      var rutinaEntry = document.createElement("div");
      rutinaEntry.classList.add("rutinaEntry");
      rutinaEntry.innerHTML = `<strong>Rutina:</strong> ${resaltarPalabra(rutina, "rutina")}<br>
                                <strong>Ejercicio:</strong> ${ejercicio}<br>
                                <strong>Series:</strong> ${series}<br>
                                <strong>Descansos:</strong> ${descansos}<br>
                                <a href="${video}" target="_blank">Ver Video</a>`;
      diaBox.appendChild(rutinaEntry);
      
      document.getElementById("dia").value = "";
      document.getElementById("rutina").value = "";
      document.getElementById("ejercicio").value = "";
      document.getElementById("series").value = "";
      document.getElementById("descansos").value = "";
      document.getElementById("video").value = "";
    }

    function resaltarPalabra(texto, palabra) {
      var expresionRegular = new RegExp('\\b' + palabra + '\\b', 'gi');
      return texto.replace(expresionRegular, '<span class="highlight">' + palabra + '</span>');
    }

    function obtenerDiaActual() {
      var diasSemana = ["domingo", "lunes", "martes", "miércoles", "jueves", "viernes", "sábado"];
      var fechaActual = new Date();
      var diaActual = diasSemana[fechaActual.getDay()];
      var diaBox = document.getElementById(diaActual.toLowerCase());
      if (diaBox) {
        window.scrollTo(0, diaBox.offsetTop);
      }
      return diaActual;
    }

    function editarRutina(dia) { // Agregado
      var diaBox = document.getElementById(dia);
      var rutinaEntry = diaBox.querySelector('.rutinaEntry');
      var textoRutina = rutinaEntry.innerHTML;
      var partesRutina = textoRutina.split('<br>');
      var rutina = partesRutina[0].split('</strong>')[1].trim();
      var ejercicio = partesRutina[1].split('</strong>')[1].trim();
      var series = partesRutina[2].split('</strong>')[1].trim();
      var descansos = partesRutina[3].split('</strong>')[1].trim();
      var video = partesRutina[4].split('"')[1].trim();
      
      document.getElementById("dia").value = dia.charAt(0).toUpperCase() + dia.slice(1);
      document.getElementById("rutina").value = rutina;
      document.getElementById("ejercicio").value = ejercicio;
      document.getElementById("series").value = series;
      document.getElementById("descansos").value = descansos;
      document.getElementById("video").value = video;
      
      diaBox.removeChild(rutinaEntry);
    }

    // Función para cambiar entre modo claro y oscuro
    function toggleDarkMode() {
      var body = document.body;
      body.classList.toggle("dark-mode");
      var container = document.querySelector('.container');
      container.classList.toggle("dark-mode");
      var rutinaBoxes = document.querySelectorAll('.rutinaBox');
      rutinaBoxes.forEach(function(box) {
        box.classList.toggle("dark-mode");
      });
    }

    obtenerDiaActual(); // Llamada a la función al cargar la página para redirigir automáticamente
  </script>
</body>
</html>
