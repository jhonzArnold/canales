<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cuadrícula de Canales</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            min-height: 100vh;
            background-color: #f0f0f0;
            margin: 0;
        }

        .login-container {
            text-align: center;
            background-color: #fff;
            padding: 20px;
            border: 1px solid #ddd;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            width: 90%;
        }

        .login-container input {
            padding: 10px;
            margin: 10px 0;
            font-size: 16px;
            width: 100%;
            border: 1px solid #ddd;
        }

        .login-container button {
            padding: 10px 20px;
            background-color: #007BFF;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
        }

        .login-container button:hover {
            background-color: #0056b3;
        }

        .grid-container {
            display: none;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
            max-width: 1000px;
            width: 90%;
            margin-top: 20px;
        }

        .grid-item {
            background-color: #ffffff;
            padding: 10px;
            border: 1px solid #ddd;
            text-align: center;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .grid-item img {
            width: 100%;
            height: 150px;
            object-fit: cover;
        }

        .grid-item button {
            margin-top: 10px;
            padding: 10px 20px;
            background-color: #007BFF;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 16px;
        }

        .grid-item button:hover {
            background-color: #0056b3;
        }

        #video-player-container {
            display: none;
            position: relative;
            width: 100%;
            height: 300px;
        }

        #video-player {
            width: 100%;
            height: 100%;
            border: 0;
        }

        .channel-list {
            position: absolute;
            top: 0;
            right: 0;
            background-color: rgba(255, 255, 255, 0.9);
            width: 200px;
            padding: 10px;
            display: block;
        }

        .channel-list h3 {
            margin: 0 0 10px 0;
        }

        .channel-list button {
            display: block;
            width: 100%;
            margin-bottom: 10px;
            background-color: #007BFF;
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
        }

        .channel-list button:hover {
            background-color: #0056b3;
        }

        /* Media Queries para pantallas más grandes */
        @media (min-width: 768px) {
            .grid-container {
                grid-template-columns: repeat(3, 1fr);
            }

            #video-player-container {
                height: 400px;
            }
        }

        @media (min-width: 1024px) {
            .grid-container {
                grid-template-columns: repeat(4, 1fr);
            }

            #video-player-container {
                height: 500px;
            }
        }
    </style>
    <script>
        function login() {
            const id = document.getElementById("id").value;
            const password = document.getElementById("password").value;

            if (id === "jhon" && password === "frio123") {
                document.querySelector('.login-container').style.display = 'none';
                document.querySelector('.grid-container').style.display = 'grid';
            } else {
                alert("ID o contraseña incorrectos. Intenta de nuevo.");
            }
        }

        function loadVideo(url) {
            var videoPlayerContainer = document.getElementById('video-player-container');
            var iframe = document.getElementById('video-player');

            // Establece la URL del video con reproducción automática
            iframe.src = url + "&autoplay=1";

            // Mostrar el reproductor
            videoPlayerContainer.style.display = 'block';

            // Esperar a que el iframe se cargue
            iframe.onload = function() {
                try {
                    var playerWindow = iframe.contentWindow;
                    if (playerWindow && playerWindow.document) {
                        var video = playerWindow.document.querySelector('video');
                        if (video) {
                            video.volume = 1.0; // Subir el volumen al 100%
                            video.play(); // Reproducir automáticamente
                        }
                    }
                } catch (error) {
                    console.error('Error al ajustar el volumen del video:', error);
                }

                requestFullScreen(videoPlayerContainer);
            };
        }

        // Función para solicitar pantalla completa
        function requestFullScreen(element) {
            if (element.requestFullscreen) {
                element.requestFullscreen();
            } else if (element.mozRequestFullScreen) { // Firefox
                element.mozRequestFullScreen();
            } else if (element.webkitRequestFullscreen) { // Chrome, Safari, Opera
                element.webkitRequestFullscreen();
            } else if (element.msRequestFullscreen) { // IE/Edge
                element.msRequestFullscreen();
            }

            // Cambiar a orientación horizontal para dispositivos móviles
            if (screen.orientation && screen.orientation.lock) {
                screen.orientation.lock('landscape').catch(function(error) {
                    console.error('Error en el bloqueo de orientación:', error);
                });
            }
        }
    </script>
</head>
<body>
    <!-- Formulario de login -->
    <div class="login-container">
        <h2>Iniciar Sesión</h2>
        <input type="text" id="id" placeholder="ID de usuario">
        <input type="password" id="password" placeholder="Contraseña">
        <button onclick="login()">Ingresar</button>
    </div>

    <!-- Cuadrícula de canales -->
    <div class="grid-container">
        <!-- Imagen 1 -->
        <div class="grid-item">
            <img src="descarga.jfif" alt="Imagen 1">
            <button onclick="loadVideo('https://geo.dailymotion.com/player.html?video=x7x4dgx')">Ver canal</button>
        </div>
        <!-- Imagen 2 -->
        <div class="grid-item">
            <img src="aa.jfif" alt="Imagen 2">
            <button onclick="loadVideo('https://betzta.com/canales.php?stream=america')">Ver canal</button>
        </div>
        <!-- Imagen 3 -->
        <div class="grid-item">
            <img src="dd.jfif" alt="Imagen 3">
            <button onclick="loadVideo('https://atvenvivo.com/hls.php-93.html?get=Ly9qaXJlaC0yLWhscy12aWRlby11cy1pc3AuZHBzLmxpdmUvaGxzLXZpZGVvLzU2N2ZmZGUzZmEzMTlmYWRmMzQxOWVmZGEyNTYxOTQ1NjIzMWRmZWEvbGF0aW5hL2xhdGluYS5zbWlsL3BsYXlsaXN0Lm0zdTg/ZHBzc2lkPWIyNjg1MzMxMjAxNjZiZmYyYmJjNjMzNyZzaWQ9YmE1dDFsMXhiMjUzODA5MTY3MjY2YmZmMmJkOTk0OWUmbmR2Yz0w')">Ver canal</button>
        </div>
    </div>

    <!-- Reproductor de video -->
    <div id="video-player-container">
        <iframe id="video-player" sandbox="allow-same-origin allow-scripts allow-autoplay" frameborder="0" allowfullscreen></iframe>

        <!-- Lista de otros canales para cambiar -->
        <div class="channel-list">
            <h3>Canales</h3>
            <button onclick="loadVideo('https://geo.dailymotion.com/player.html?video=x7x4dgx')">Canal 1</button>
            <button onclick="loadVideo('https://betzta.com/canales.php?stream=america')">Canal 2</button>
            <button onclick="loadVideo('https://atvenvivo.com/hls.php-93.html?get=Ly9qaXJlaC0yLWhscy12aWRlby11cy1pc3AuZHBzLmxpdmUvaGxzLXZpZGVvLzU2N2ZmZGUzZmEzMTlmYWRmMzQxOWVmZGEyNTYxOTQ1NjIzMWRmZWEvbGF0aW5hL2xhdGluYS5zbWlsL3BsYXlsaXN0Lm0zdTg/ZHBzc2lkPWIyNjg1MzMxMjAxNjZiZmYyYmJjNjMzNyZzaWQ9YmE1dDFsMXhiMjUzODA5MTY3MjY2YmZmMmJkOTk0OWUmbmR2Yz0w')">Canal 3</button>
        </div>
    </div>
</body>
</html>


