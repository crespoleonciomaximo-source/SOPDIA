<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Detector de IA con Porcentaje</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f9;
            color: #333;
            transition: background-color 0.3s, color 0.3s;
        }

        .container {
            max-width: 600px;
            margin: auto;
            background-color: white;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            transition: background-color 0.3s, color 0.3s;
        }

        h1 {
            text-align: center;
        }

        textarea {
            width: 100%;
            height: 150px;
            padding: 10px;
            font-size: 16px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
            transition: border-color 0.3s;
        }

        button {
            width: 100%;
            padding: 10px;
            font-size: 18px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #45a049;
        }

        .result {
            margin-top: 20px;
            text-align: center;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .ai {
            background-color: #FFDDC1;
            color: #e74c3c;
        }

        .human {
            background-color: #DFF0D8;
            color: #27ae60;
        }

        /* Estilos para el panel de personalización */
        .settings {
            margin-top: 30px;
            padding: 15px;
            background-color: #f4f4f9;
            border-radius: 5px;
        }

        .settings label {
            display: block;
            margin-bottom: 5px;
        }

        .settings input[type="color"], .settings input[type="range"] {
            width: 100%;
            margin-bottom: 15px;
        }

        .percentage {
            font-size: 20px;
            font-weight: bold;
            margin-top: 10px;
        }

    </style>
</head>
<body>

    <div class="container">
        <h1>Detector de IA con Porcentaje</h1>
        <textarea id="inputText" placeholder="Introduce el texto que quieres analizar..."></textarea>
        <button onclick="detectText()">Detectar</button>
        <div id="result" class="result"></div>
        <div id="percentage" class="percentage"></div> <!-- Mostrará el porcentaje -->
    </div>

    <!-- Panel de Personalización -->
    <div class="settings">
        <h3>Personaliza tu Página</h3>
        <label for="bgColor">Color de fondo:</label>
        <input type="color" id="bgColor" value="#f4f4f9" onchange="changeBackground()">

        <label for="textColor">Color del texto:</label>
        <input type="color" id="textColor" value="#333" onchange="changeTextColor()">

        <label for="buttonColor">Color de los botones:</label>
        <input type="color" id="buttonColor" value="#4CAF50" onchange="changeButtonColor()">
    </div>

    <script>
        function detectText() {
            const inputText = document.getElementById("inputText").value;
            const resultDiv = document.getElementById("result");
            const percentageDiv = document.getElementById("percentage");
            
            if (inputText.trim() === "") {
                resultDiv.innerHTML = "Por favor, ingresa un texto para analizar.";
                resultDiv.className = "";
                percentageDiv.innerHTML = "";
                return;
            }

            // Patrones comunes que podrían indicar un texto generado por IA
            const aiIndicators = [
                /intentaré/, /probablemente/, /no tengo emociones/, /seguramente/, /mi conocimiento es limitado/,
                /como modelo de lenguaje/, /mis respuestas se basan/, /lo que puedo decirte/, /este texto no es/,
                /si me lo permites/, /en general puedo decirte/, /como mencioné antes/, /según mi entrenamiento/
            ];

            // Contar cuántos patrones de IA coinciden
            let matches = 0;
            aiIndicators.forEach(indicator => {
                if (inputText.toLowerCase().match(indicator)) {
                    matches++;
                }
            });

            // Calcular el porcentaje de probabilidad basado en el número de coincidencias
            const totalIndicators = aiIndicators.length;
            let percentage = Math.round((matches / totalIndicators) * 100);

            // Si hay alguna coincidencia, mostrar el porcentaje de IA
            if (matches > 0) {
                resultDiv.innerHTML = "Este texto tiene alta probabilidad de ser generado por una IA.";
                resultDiv.className = "result ai";
            } else {
                resultDiv.innerHTML = "Este texto parece ser escrito por un ser humano.";
                resultDiv.className = "result human";
            }

            percentageDiv.innerHTML = `Probabilidad de IA: ${percentage}%`;

            // Si la probabilidad es 0, mostrar como 0%, si es más de 50%, podríamos decir que es más probable IA
            if (percentage > 50) {
                percentageDiv.style.color = "#e74c3c"; // Rojo para alto porcentaje de IA
            } else {
                percentageDiv.style.color = "#27ae60"; // Verde para bajo porcentaje de IA
            }
        }

        // Funciones de personalización
        function changeBackground() {
            const bgColor = document.getElementById("bgColor").value;
            document.body.style.backgroundColor = bgColor;
            document.querySelector('.container').style.backgroundColor = bgColor;
        }

        function changeTextColor() {
            const textColor = document.getElementById("textColor").value;
            document.body.style.color = textColor;
            document.querySelector('.container').style.color = textColor;
        }

        function changeButtonColor() {
            const buttonColor = document.getElementById("buttonColor").value;
            document.querySelector('button').style.backgroundColor = buttonColor;
        }
    </script>

</body>
</html>
