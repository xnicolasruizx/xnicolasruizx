!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grupos de Investigación y Semilleros</title>
    <style>
        body { font-family: Arial, sans-serif; }
        .container { max-width: 800px; margin: auto; padding: 20px; }
        .section { margin-bottom: 20px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Grupos de Investigación y Semilleros</h1>
        
        <div class="section">
            <h2>Listado de Grupos de Investigación</h2>
            <select id="grupos" onchange="mostrarInfoGrupo()">
                <option value="">Seleccione un grupo</option>
                <option value="gieiam">Grupo GIEIAM</option>
                <option value="comba">Grupo COMBA I+D</option>
            </select>
            <div id="infoGrupo"></div>
            <h3>Docentes del grupo</h3>
            <ul id="listaDocentesGrupo"></ul>
        </div>
        
        <div class="section">
            <h2>Registrar Docente Investigador</h2>
            <form id="formDocente">
                <input type="text" id="nombreDocente" placeholder="Nombre" required>
                <input type="text" id="formacion" placeholder="Formación Académica" required>
                <input type="text" id="horario" placeholder="Horario de Atención" required>
                <select id="grupoDocente" required>
                    <option value="">Seleccione un grupo</option>
                    <option value="gieiam">Grupo GIEIAM</option>
                    <option value="comba">Grupo COMBA I+D</option>
                </select>
                <button type="submit">Registrar</button>
            </form>
        </div>
        
        <div class="section">
            <h2>Vincular Estudiante a Semillero</h2>
            <form id="formEstudiante">
                <input type="text" id="nombreEstudiante" placeholder="Nombre" required>
                <input type="text" id="codigoEstudiante" placeholder="Código" required>
                <input type="text" id="carreraEstudiante" placeholder="Carrera" required>
                <select id="semilleroEstudiante" required>
                    <option value="">Seleccione un semillero</option>
                    <option value="comba">Semillero Comba</option>
                    <option value="informa">Semillero Informa</option>
                </select>
                <button type="submit">Vincular</button>
            </form>
        </div>
        
        <div class="section">
            <h2>Agregar Actividad a Semillero</h2>
            <form id="formActividad">
                <input type="text" id="tipoActividad" placeholder="Tipo de Actividad" required>
                <input type="date" id="fecha" required>
                <input type="time" id="hora" required>
                <input type="number" id="limite" placeholder="Límite de Asistentes" required>
                <textarea id="resumen" placeholder="Resumen de la Actividad" required></textarea>
                <button type="submit">Agregar</button>
            </form>
        </div>
        
        <div class="section">
            <h2>Listado de Actividades</h2>
            <ul id="listaActividades"></ul>
        </div>
    </div>

    <script>
        let docentes = JSON.parse(localStorage.getItem("docentes")) || [];
        let actividades = JSON.parse(localStorage.getItem("actividades")) || [];

        function mostrarInfoGrupo() {
            const grupoSeleccionado = document.getElementById("grupos").value;
            const infoGrupo = {
                gieiam: "Nombre: Grupo GIEIAM\nObjetivos: Investigación en Ingeniería Electrónica Industrial y Computación Móvil y Banda Ancha\nDirector:  PhD. Diana Paola Bernal Suarez",
                comba: "Nombre: Grupo COMBA I+D\nObjetivos: Investigación en Ingeniería Electrónica Industrial y Computación Móvil y Banda Ancha\nDirector:  PhD. Diana Paola Bernal Suarez"
            };
            document.getElementById("infoGrupo").innerText = infoGrupo[grupoSeleccionado] || "";
            mostrarDocentesGrupo(grupoSeleccionado);
        }

        function mostrarDocentesGrupo(grupo) {
            const listaDocentesGrupo = document.getElementById("listaDocentesGrupo");
            listaDocentesGrupo.innerHTML = "";
            docentes.filter(docente => docente.grupo === grupo).forEach(docente => {
                const li = document.createElement("li");
                li.textContent = `${docente.nombre} - ${docente.formacion} - Horario: ${docente.horario}`;
                listaDocentesGrupo.appendChild(li);
            });
        }

        document.getElementById("formDocente").addEventListener("submit", function(event) {
            event.preventDefault();
            const nombre = document.getElementById("nombreDocente").value;
            const formacion = document.getElementById("formacion").value;
            const horario = document.getElementById("horario").value;
            const grupo = document.getElementById("grupoDocente").value;
            
            docentes.push({ nombre, formacion, horario, grupo });
            localStorage.setItem("docentes", JSON.stringify(docentes));
            mostrarDocentesGrupo(document.getElementById("grupos").value);
        });

        document.getElementById("formActividad").addEventListener("submit", function(event) {
            event.preventDefault();
            const actividad = document.getElementById("tipoActividad").value;
            const fecha = document.getElementById("fecha").value;
            const hora = document.getElementById("hora").value;
            const limite = document.getElementById("limite").value;
            const resumen = document.getElementById("resumen").value;
            
            actividades.push({ actividad, fecha, hora, limite, resumen });
            localStorage.setItem("actividades", JSON.stringify(actividades));
            mostrarActividades();
        });

        function mostrarActividades() {
            const listaActividades = document.getElementById("listaActividades");
            listaActividades.innerHTML = "";
            actividades.forEach(act => {
                const li = document.createElement("li");
                li.textContent = `${act.actividad} - ${act.fecha} ${act.hora} - ${act.limite} asistentes - ${act.resumen}`;
                listaActividades.appendChild(li);
            });
        }

        mostrarActividades();
    </script>
</body>
</html>
