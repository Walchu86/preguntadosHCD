<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Juego de Preguntas</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f8ff;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        .container {
            text-align: center;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 10px;
            background-color: white;
        }

        h1 {
            color: #333;
        }

        .question {
            font-size: 1.2em;
            margin-bottom: 20px;
        }

        .options {
            display: flex;
            flex-direction: column;
        }

        .options button {
            margin: 10px 0;
            padding: 10px;
            font-size: 1em;
            cursor: pointer;
            border-radius: 5px;
            border: 1px solid #ddd;
        }

        .options button:hover {
            background-color: #f0f0f0;
        }

        #result {
            margin-top: 20px;
            font-size: 1.5em;
        }

    </style>
</head>
<body>
    <div class="container">
        <h1>Juego de Preguntas sobre Corrientes</h1>
        <div class="question" id="question">Aquí irá la pregunta</div>
        <div class="options">
            <button onclick="checkAnswer(0)" id="option0">Opción 1</button>
            <button onclick="checkAnswer(1)" id="option1">Opción 2</button>
            <button onclick="checkAnswer(2)" id="option2">Opción 3</button>
        </div>
        <div id="result"></div>
    </div>

    <script>
        const preguntas = [
            {
                pregunta: "¿Cuál es el río que bordea Corrientes Capital?",
                opciones: ["Río Paraná", "Río Uruguay", "Río Paraguay"],
                correcta: 0
            },
            {
                pregunta: "¿En qué año se fundó Corrientes Capital?",
                opciones: ["1588", "1733", "1600"],
                correcta: 0
            },
            {
                pregunta: "¿Cuál es la flor provincial de Corrientes?",
                opciones: ["Flor de Ceibo", "Flor de Lapacho", "Flor de Jazmín"],
                correcta: 0
            },
            {
                pregunta: "¿Qué animal es típico de la fauna de los Esteros del Iberá?",
                opciones: ["Yacaré", "León", "Oso"],
                correcta: 0
            },
            {
                pregunta: "¿Qué mito es popular en Corrientes Capital?",
                opciones: ["El Pombero", "La Llorona", "El Cadejo"],
                correcta: 0
            }
        ];

        let preguntaActual = 0;
        let correctasSeguidas = 0;
        let incorrectasSeguidas = 0;

        function cargarPregunta() {
            const pregunta = preguntas[preguntaActual];
            document.getElementById('question').innerText = pregunta.pregunta;
            document.getElementById('option0').innerText = pregunta.opciones[0];
            document.getElementById('option1').innerText = pregunta.opciones[1];
            document.getElementById('option2').innerText = pregunta.opciones[2];
            document.getElementById('result').innerText = "";
        }

        function checkAnswer(opcion) {
            const pregunta = preguntas[preguntaActual];
            if (opcion === pregunta.correcta) {
                correctasSeguidas++;
                incorrectasSeguidas = 0;
                document.getElementById('result').innerText = "¡Correcto!";
            } else {
                incorrectasSeguidas++;
                correctasSeguidas = 0;
                document.getElementById('result').innerText = "Incorrecto";
            }

            if (correctasSeguidas === 5) {
                alert("¡Felicidades! Ganaste el juego.");
                resetGame();
            } else if (incorrectasSeguidas === 3) {
                alert("Perdiste el juego. Mejor suerte la próxima vez.");
                resetGame();
            } else {
                preguntaActual = (preguntaActual + 1) % preguntas.length;
                cargarPregunta();
            }
        }

        function resetGame() {
            correctasSeguidas = 0;
            incorrectasSeguidas = 0;
            preguntaActual = 0;
            cargarPregunta();
        }

        window.onload = cargarPregunta;
    </script>
</body>
</html>
