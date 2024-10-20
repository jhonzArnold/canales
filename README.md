<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cuadrícula de Canales</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
        }

        /* Contenedor de Login */
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            min-height: 100vh;
            background-color: #f0f0f0;
        }

        .login-container.hidden {
            display: none;
        }

        .login-box {
            text-align: center;
            background-color: #fff;
            padding: 20px 30px;
            border: 1px solid #ddd;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            max-width: 400px;
            width: 100%;
        }

        .login-box h2 {
            margin-bottom: 20px;
        }

        .login-box input {
            padding: 10px;
            margin: 10px 0;
            font-size: 16px;
            width: 100%;
            border: 1px solid #ddd;
            border-radius: 4px;
        }

        .login-box button {
            padding: 10px 20px;
            background-color: #007BFF;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
            border-radius: 4px;
        }

        .login-box button:hover {
            background-color: #0056b3;
        }

        /* Contenedor Principal */
        .main-container {
            display: none;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .main-container.active {
            display: block;
        }

        .main-container h2, .main-container h3 {
            text-align: center;
            margin-bottom: 20px;
        }

        /* Grid de Canales */
        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 20px;
        }

        .grid-item {
            background-color: #ffffff;
            padding: 10px;
            border: 1px solid #ddd;
            text-align: center;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }

        .grid-item img {
            width: 100%;
            height: auto;
            max-height: 100px;
            object-fit: cover;
            border-radius: 4px;
        }

        .grid-item h4 {
            margin: 10px 0 0 0;
            font-size: 14px;
        }

        .grid-item button {
            margin-top: 10px;
            padding: 8px 16px;
            background-color: #007BFF;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 14px;
            border-radius: 4px;
            width: 100%;
        }

        .grid-item button:hover {
            background-color: #0056b3;
        }

        /* Contenedor del Reproductor de Video */
        #video-player-container {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 90vw;
            height: 50vh;
            background-color: #000;
            border: 2px solid #007BFF;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
            display: none;
            z-index: 1000;
        }

        #video-player-container.active {
            display: block;
        }

        #video-player {
            width: 100%;
            height: 100%;
            border: 0;
            border-radius: 8px;
        }

        .close-button, .show-channels-button {
            position: absolute;
            top: 10px;
            background-color: rgba(255, 0, 0, 0.7);
            border: none;
            color: white;
            padding: 8px 12px;
            cursor: pointer;
            border-radius: 50%;
            font-size: 16px;
            z-index: 1001;
        }

        .close-button {
            right: 10px;
        }

        .show-channels-button {
            right: 50px;
            background-color: rgba(0, 123, 255, 0.7);
        }

        .close-button:hover, .show-channels-button:hover {
            background-color: rgba(255, 0, 0, 0.9);
        }

        .show-channels-button:hover {
            background-color: rgba(0, 123, 255, 0.9);
        }

        /* Lista de Canales flotante dentro del reproductor */
        .channel-list {
            position: absolute;
            top: 10%;
            left: 10px;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 8px;
            padding: 10px;
            z-index: 1002;
            display: none;
            width: 200px;
            max-height: 80%;
            overflow-y: auto;
        }

        .channel-list.active {
            display: block;
        }

        .channel-list button {
            display: block;
            margin-bottom: 10px;
            background-color: #007BFF;
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
            width: 100%;
            border-radius: 4px;
        }

        .channel-list button:hover {
            background-color: #0056b3;
        }

        /* Media Queries para Responsividad */
        @media (min-width: 768px) {
            .grid-item img {
                max-height: 150px;
            }

            #video-player-container {
                width: 70vw;
                height: 60vh;
            }
        }

        @media (min-width: 1024px) {
            .grid-item img {
                max-height: 200px;
            }

            #video-player-container {
                width: 60vw;
                height: 70vh;
            }
        }
    </style>
    <script>
        // Función de Login
        function login() {
            const id = document.getElementById("id").value;
            const password = document.getElementById("password").value;

            if (id === "jhon" && password === "frio123") {
                document.querySelector('.login-container').classList.add('hidden');
                document.querySelector('.main-container').classList.add('active');
            } else {
                alert("ID o contraseña incorrectos. Intenta de nuevo.");
            }
        }

        // Función para Cargar Video
        function loadVideo(url) {
            var videoPlayerContainer = document.getElementById('video-player-container');
            var iframe = document.getElementById('video-player');

            // Establece la URL del video con reproducción automática
            iframe.src = url;

            // Mostrar el reproductor
            videoPlayerContainer.classList.add('active');

            // Solicitar orientación horizontal (no siempre posible)
            if (screen.orientation && screen.orientation.lock) {
                screen.orientation.lock('landscape').catch(function(error) {
                    console.error('Error al bloquear la orientación:', error);
                });
            }

            // Entrar en fullscreen
            enterFullScreen(videoPlayerContainer);
        }

        // Función para Cerrar el Video
        function closeVideo() {
            var videoPlayerContainer = document.getElementById('video-player-container');
            var iframe = document.getElementById('video-player');

            // Ocultar el reproductor
            videoPlayerContainer.classList.remove('active');

            // Detener el video
            iframe.src = "";

            // Salir de fullscreen
            if (document.fullscreenElement) {
                document.exitFullscreen().catch(err => {
                    console.error('Error al salir de fullscreen:', err);
                });
            }

            // Desbloquear orientación
            if (screen.orientation && screen.orientation.unlock) {
                screen.orientation.unlock().catch(function(error) {
                    console.error('Error al desbloquear la orientación:', error);
                });
            }
        }

        // Función para mostrar la lista de canales en el reproductor
        function toggleChannelList() {
            var channelList = document.querySelector('.channel-list');
            channelList.classList.toggle('active');
        }

        // Función para Entrar en Fullscreen
        function enterFullScreen(element) {
            if (element.requestFullscreen) {
                element.requestFullscreen();
            } else if (element.mozRequestFullScreen) { // Firefox
                element.mozRequestFullScreen();
            } else if (element.webkitRequestFullscreen) { // Chrome, Safari, Opera
                element.webkitRequestFullscreen();
            } else if (element.msRequestFullscreen) { // IE/Edge
                element.msRequestFullscreen();
            }
        }
    </script>
</head>
<body>
    <!-- Formulario de Login -->
    <div class="login-container">
        <div class="login-box">
            <h2>Iniciar Sesión</h2>
            <input type="text" id="id" placeholder="ID de usuario">
            <input type="password" id="password" placeholder="Contraseña">
            <button onclick="login()">Ingresar</button>
        </div>
    </div>

    <!-- Contenedor Principal Después del Login -->
    <div class="main-container">
        <div class="content-container">
            <!-- Sección de Canales -->
            <div class="channels-section">
                <h2>Canales</h2>
                <div class="grid-container">
                    <!-- Canal 1 -->
                    <div class="grid-item">
                        <img src="descarga.jfif" alt="Willax">
                        <h4>Willax</h4>
                        <button onclick="loadVideo('https://geo.dailymotion.com/player.html?video=x7x4dgx')">Ver canal</button>
                    </div>
                    <!-- Canal 2 -->
                    <div class="grid-item">
                        <img src="gol.jpg" alt="Gol Perú">
                        <h4>Gol Perú</h4>
                        <button onclick="loadVideo('https://betzta.com/canales.php?stream=golperu')">Ver canal</button>
                    </div>
                    <!-- Canal 3 -->
                    <div class="grid-item">
                        <img src="dd.jfif" alt="Latina">
                        <h4>Latina</h4>
                        <button onclick="loadVideo('https://atvenvivo.com/hls.php-93.html?get=Ly9qaXJlaC0yLWhscy12aWRlby11cy1pc3AuZHBzLmxpdmUvaGxzLXZpZGVvLzU2N2ZmZGUzZmEzMTlmYWRmMzQxOWVmZGEyNTYxOTQ1NjIzMWRmZWEvbGF0aW5hL2xhdGluYS5zbWlsL3BsYXlsaXN0Lm0zdTg/ZHBzc2lkPWIyNjg1MzMxMjAxNjZiZmYyYmJjNjMzNyZzaWQ9YmE1dDFsMXhiMjUzODA5MTY3MjY2YmZmMmJkOTk0OWUmbmR2Yz0w')">Ver canal</button>
                    </div>
                </div>
            </div>

            <!-- Sección de Películas -->
            <div class="movies-section">
                <h3>Películas</h3>
                <div class="grid-container">
                    <div class="grid-item">
                        <img src="garf.jpg" alt="Garfield">
                        <h4>Garfield</h4>
                        <button onclick="loadVideo('https://nuuuppp.pro/watch/7kz7jIHYMkPnCGUQ5OVCQ3jz3s7kz70Y8cv7kz7kU4p45xzpNojXZmI?h=')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="win.jpg" alt="winnie pooh 2">
                        <h4>winnie pooh 2</h4>
                        <button onclick="loadVideo('https://tmdbcdn.lat/watch_video.php?v=aEpFdVRUcDdpcSsyaVZSLzJPaXZKS01UQTFla1lRTzdKaHFLS3E0VThuQi92V2s0SEpMRWZZL0RqNkk4VGZZUA%3D%3D#iss=MjgwMzphM2UwOjE5MTM6YzBmOTphMWNkOjUyNDA6YWU4ZjoyOWM5')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="terr.jpg" alt="Terriefer 3">
                        <h4>Terriefer 3</h4>
                        <button onclick="loadVideo('https://tmdbcdn.lat/watch_video.php?v=aldOTm5vMzFwcTZuaEV3ZUZ3WVhRMWtDU2JOdk9CVHQ0eUJqbjFmL1pvaXl3U2NpU3I0ci9CR1NPZlR0dFgvWA%3D%3D#iss=MjgwMzphM2UwOjE5MTM6YzBmOTphMWNkOjUyNDA6YWU4ZjoyOWM5')">Ver película</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Reproductor de Video (Ventana Grande) -->
    <div id="video-player-container">
        <button class="close-button" onclick="closeVideo()">✖</button>
        <button class="show-channels-button" onclick="toggleChannelList()">📺</button>
        <iframe id="video-player" frameborder="0" allowfullscreen></iframe>

        <!-- Lista de Canales dentro del reproductor -->
        <div class="channel-list">
            <button onclick="loadVideo('https://geo.dailymotion.com/player.html?video=x7x4dgx')">Willax</button>
            <button onclick="loadVideo('https://betzta.com/canales.php?stream=golperu')">Gol Perú</button>
            <button onclick="loadVideo('https://atvenvivo.com/hls.php-93.html?get=Ly9qaXJlaC0yLWhscy12aWRlby11cy1pc3AuZHBzLmxpdmUvaGxzLXZpZGVvLzU2N2ZmZGUzZmEzMTlmYWRmMzQxOWVmZGEyNTYxOTQ1NjIzMWRmZWEvbGF0aW5hL2xhdGluYS5zbWlsL3BsYXlsaXN0Lm0zdTg/ZHBzc2lkPWIyNjg1MzMxMjAxNjZiZmYyYmJjNjMzNyZzaWQ9YmE1dDFsMXhiMjUzODA5MTY3MjY2YmZmMmJkOTk0OWUmbmR2Yz0w')">Latina</button>
        </div>
    </div>
</body>
</html>
