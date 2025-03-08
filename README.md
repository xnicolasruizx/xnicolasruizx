<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mini Sitio COMBA I+D</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .container { max-width: 800px; margin: auto; }
        .card { border: 1px solid #ddd; padding: 10px; margin: 10px 0; cursor: pointer; }
        .hidden { display: none; }
    </style>
    <script>
        function showGroupInfo(name, director, areas, members, description) {
            document.getElementById('groupName').innerText = name;
            document.getElementById('groupDirector').innerText = director;
            document.getElementById('groupAreas').innerText = areas;
            document.getElementById('groupMembers').innerText = members;
            document.getElementById('groupDescription').innerText = description;
            document.getElementById('groupInfo').classList.remove('hidden');
        }

        function addActivity() {
            let type = document.getElementById('activityType').value;
            let date = document.getElementById('activityDate').value;
            let time = document.getElementById('activityTime').value;
            let summary = document.getElementById('activitySummary').value;
            let limit = document.getElementById('activityLimit').value;
            
            let newActivity = document.createElement('li');
            newActivity.textContent = `${type} - ${date} - ${time} - ${summary} (Límite: ${limit})`;
            document.getElementById('activityList').appendChild(newActivity);
        }
    </script>
</head>
<body>
    <div class="container">
        <h1>Grupos de Investigación</h1>
        <div class="card" onclick="showGroupInfo('Grupo GIEIAM', 'PhD. Diana Paola Bernal Suarez', 'Gestión y control de la contaminación ambiental. Instrumentación, automatización y sistemas inteligentes. Logística, operaciones, productividad y gestión de proyectos.', 'PhD. Josnel Martínez Garcés, Harold Andrés Payán Salcedo', 'Descripción adicional para el Grupo GIEIAM.')">
            <h2>Grupo GIEIAM</h2>
        </div>
        <div class="card" onclick="showGroupInfo('Grupo COMBA I+D', 'PhD. Diana Paola Bernal Suarez', 'Gestión y control de la contaminación ambiental. Instrumentación, automatización y sistemas inteligentes. Logística, operaciones, productividad y gestión de proyectos.', 'Andrés Payán Salcedo, Mg. Iván Andrés González Vargas', 'GIFEM Grupo de Investigación en Física, Estadística y Matemáticas.')">
            <h2>Grupo COMBA I+D</h2>
        </div>

        <div id="groupInfo" class="hidden">
            <h2 id="groupName"></h2>
            <p><strong>Director:</strong> <span id="groupDirector"></span></p>
            <p><strong>Áreas de Trabajo:</strong> <span id="groupAreas"></span></p>
            <p><strong>Miembros:</strong> <span id="groupMembers"></span></p>
            <p><strong>Descripción Adicional:</strong> <span id="groupDescription"></span></p>
        </div>

        <h2>Registrar Actividad en Semillero</h2>
        <input type="text" id="activityType" placeholder="Tipo de actividad">
        <input type="date" id="activityDate">
        <input type="time" id="activityTime">
        <input type="number" id="activityLimit" placeholder="Límite de asistentes">
        <input type="text" id="activitySummary" placeholder="Resumen">
        <button onclick="addActivity()">Agregar Actividad</button>

        <h2>Actividades Registradas</h2>
        <ul id="activityList"></ul>
    </div>
</body>
</html>
