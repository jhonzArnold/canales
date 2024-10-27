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

        /* Contenedor de Login con imagen de fondo */
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            min-height: 100vh;
            background-image: url('https://img.global.news.samsung.com/mx/wp-content/uploads/2022/08/MX_TV_Mockup_03-1.jpg'); /* Aquí va la URL de tu imagen */
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
        }

        .login-container.hidden {
            display: none;
        }

        .login-box {
            text-align: center;
            background-color: rgba(255, 255, 255, 0.9); /* Fondo semitransparente */
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

        // Función para Cargar Video sin sandbox para ciertos canales
        function loadVideo(url) {
            var videoPlayerContainer = document.getElementById('video-player-container');
            var iframe = document.getElementById('video-player');
            
            // Remover sandbox para algunos canales específicos
            if (url.includes('golperu') || url.includes('latina')|| url.includes('Venom3')) {
                iframe.removeAttribute('sandbox');
            } else {
                iframe.setAttribute('sandbox', 'allow-same-origin allow-scripts allow-autoplay');
            }

            // Establecer la URL del video con reproducción automática
            iframe.src = url;

            // Mostrar el reproductor
            videoPlayerContainer.classList.add('active');

            // Solicitar orientación horizontal
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
                        <img src="exitosa.jpg" alt="Exitosa">
                        <h4>Exitosa</h4>
                        <button onclick="loadVideo('https://atvenvivo.com/hls.php-95.html?get=Ly9sdW5hLTEtdmlkZW8ubWVkaWFzZXJ2ZXIuZGlnaXRhbC9leGl0b3NhdHZfMjMzYi00YjQ5LWE3MjYtNWEzY2IwZTMyNDNjL2luZGV4LmZtcDQubTN1OA==')">Ver canal</button>
                    </div>
                    <!-- Canal 3 -->
                    <div class="grid-item">
                        <img src="dd.jfif" alt="Latina">
                        <h4>Latina</h4>
                        <button onclick="loadVideo('https://atvenvivo.com/hls.php-93.html?get=Ly9qaXJlaC0yLWhscy12aWRlby11cy1pc3AuZHBzLmxpdmUvaGxzLXZpZGVvLzU2N2ZmZGUzZmEzMTlmYWRmMzQxOWVmZGEyNTYxOTQ1NjIzMWRmZWEvbGF0aW5hL2xhdGluYS5zbWlsL3BsYXlsaXN0Lm0zdTg/ZHBzc2lkPWIyNjg1MzMxMjAxNjZiZmYyYmJjNjMzNyZzaWQ9YmE1dDFsMXhiMjUzODA5MTY3MjY2YmZmMmJkOTk0OWUmbmR2Yz0w')">Ver canal</button>
                    </div>
                    <!-- Canal 4 -->
                    <div class="grid-item">
                        <img src="pana.jpg" alt="panamericana">
                        <h4>panamericana</h4>
                        <button onclick="loadVideo('https://cdnhd.iblups.com/hls/ptv5.m3u8')">Ver canal</button>
                    </div>
                     <!-- Canal 5 -->
                     <div class="grid-item">
                        <img src="aa.jfif" alt="America">
                        <h4>America</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/americatv.html')">Ver canal</button>
                    </div>
                    <!-- Canal 6 -->
                    <div class="grid-item">
                        <img src="gol.jpg" alt="golperu">
                        <h4>golperu</h4>
                        <button onclick="loadVideo('https://gol12.com/vivo/canales.php?stream=golperu')">Ver canal</button>
                    </div>
                    <!-- Canal 7 -->
                    <div class="grid-item">
                        <img src="atv.jfif" alt="atv">
                        <h4>atv</h4>
                        <button onclick="loadVideo('https://atvenvivo.com/hls.php-89.html?get=Ly9hbGJhLXBlLWF0di1hdHYuc3RyZWFtLm1lZGlhdGlxdWVzdHJlYW0uY29tL2luZGV4Lm0zdTg=')">Ver canal</button>
                    </div>
                    <!-- Canal 8 -->
                    <div class="grid-item">
                        <img src="ki.png" alt="discovery kids">
                        <h4>discovery kids</h4>
                        <button onclick="loadVideo('https://tvlibreonline.net/html/clarovideo.html?r=DISKIDS')">Ver canal</button>
                    </div>
                     <!-- Canal 9 -->
                     <div class="grid-item">
                        <img src="dee.png" alt="disney chanel">
                        <h4>disney chanel</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/disneychannel.html')">Ver canal</button>
                    </div>
                     <!-- Canal 10 -->
                     <div class="grid-item">
                        <img src="kk.webp" alt="cartton network">
                        <h4>cartton network</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/cartoonnetwork.html')">Ver canal</button>
                    </div>
                    <!-- Canal 11 -->
                    <div class="grid-item">
                        <img src="ees.png" alt="star chanel">
                        <h4>star chanel</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/starchannel.html')">Ver canal</button>
                    </div>
                     <!-- Canal 12 -->
                     <div class="grid-item">
                        <img src="tt.png" alt="tnt hd">
                        <h4>tnt hd</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/tnt.html')">Ver canal</button>
                    </div>
                     <!-- Canal 13 -->
                     <div class="grid-item">
                        <img src="pla.png" alt="animad plane">
                        <h4>animad plane</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/animalplanet.html')">Ver canal</button>
                    </div>
                     <!-- Canal 14 -->
                     <div class="grid-item">
                        <img src="his.jfif" alt="histoty chanel">
                        <h4>histoty chanel</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/history.html')">Ver canal</button>
                    </div>
                    <!-- Canal 15 -->
                    <div class="grid-item">
                        <img src="ju.jfif" alt="Disney Junior">
                        <h4>Disney Junior</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/disneyjr.html')">Ver canal</button>
                    </div>
                    <!-- Canal 16 -->
                    <div class="grid-item">
                        <img src="caa.png" alt="Cartoonito">
                        <h4>Cartoonito</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/cartoonito.html')">Ver canal</button>
                    </div>
                    <!-- Canal 17 -->
                    <div class="grid-item">
                        <img src="se.png" alt="TNT Series">
                        <h4>TNT Series</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/tntseries.html')">Ver canal</button>
                    </div>
                     <!-- Canal 18 -->
                     <div class="grid-item">
                        <img src="tet.png" alt="Telemundo">
                        <h4>Telemundo</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/telemundopuertorico.html')">Ver canal</button>
                    </div>
                     <!-- Canal 19 -->
                     <div class="grid-item">
                        <img src="qq.png" alt="National Geographic">
                        <h4>National Geographic</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/natgeo.html')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="gol.jpg" alt="golperu1">
                        <h4>golperu1</h4>
                        <button onclick="loadVideo('https://la10hd.com/tv/golperu.html')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="gol.jpg" alt="golperu">
                        <h4>golperu</h4>
                        <button onclick="loadVideo('https://gol12.com/vivo/canales.php?stream=golperu')">Ver canal</button>
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
                        <img src="Venom3.jfif" alt="Venom3">
                        <h4>Venom3</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-8j3csupwsnty.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="win.jpg" alt="winnie pooh 2">
                        <h4>winnie pooh 2</h4>
                        <button onclick="loadVideo('https://vidhidepro.com/v/p6zkbptnjokx')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="al.jpeg" alt="Alien: Romulus">
                        <h4>Alien: Romulus</h4>
                        <button onclick="loadVideo('https://vidhidepro.com/v/xhzx133jvb6t')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="simi.jpg" alt="El planeta de los simios: Nuevo reino">
                        <h4>El planeta de los simios: Nuevo reino</h4>
                        <button onclick="loadVideo('https://vidhidepro.com/v/xh1s090mn2wp')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="god.jpeg" alt="Godzilla y Kong: El nuevo imperio">
                        <h4>Godzilla y Kong: El nuevo imperio</h4>
                        <button onclick="loadVideo('https://swdyu.com/e/lxxfbxny2vsb')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="dea.jpg" alt="Deadpool & Wolverine">
                        <h4>Deadpool & Wolverine</h4>
                        <button onclick="loadVideo('https://vidhidepro.com/v/5jlv210gxoid')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="bad.jpg" alt="Bad Boys: Hasta la muerte">
                        <h4>Bad Boys: Hasta la muerte</h4>
                        <button onclick="loadVideo('https://vidhidepro.com/v/wy2w7lkpk98c')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="cho.jpg" alt="Chabuca">
                        <h4>Chabuca</h4>
                        <button onclick="loadVideo('https://cdnplaypro.com/e/ap4r4jtogkl3')">Ver película</button>
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
            <button onclick="loadVideo('https://atvenvivo.com/hls.php-95.html?get=Ly9sdW5hLTEtdmlkZW8ubWVkaWFzZXJ2ZXIuZGlnaXRhbC9leGl0b3NhdHZfMjMzYi00YjQ5LWE3MjYtNWEzY2IwZTMyNDNjL2luZGV4LmZtcDQubTN1OA==')">Exitosa</button>
            <button onclick="loadVideo('https://cdnhd.iblups.com/hls/ptv5.m3u8')">panamericana</button>
            <button onclick="loadVideo('https://atvenvivo.com/hls.php-93.html?get=Ly9qaXJlaC0yLWhscy12aWRlby11cy1pc3AuZHBzLmxpdmUvaGxzLXZpZGVvLzU2N2ZmZGUzZmEzMTlmYWRmMzQxOWVmZGEyNTYxOTQ1NjIzMWRmZWEvbGF0aW5hL2xhdGluYS5zbWlsL3BsYXlsaXN0Lm0zdTg/ZHBzc2lkPWIyNjg1MzMxMjAxNjZiZmYyYmJjNjMzNyZzaWQ9YmE1dDFsMXhiMjUzODA5MTY3MjY2YmZmMmJkOTk0OWUmbmR2Yz0w')">Latina</button>
            <button onclick="loadVideo('https://gol12.com/vivo/canales.php?stream=golperu')">golperu</button>
            <button onclick="loadVideo('https://atvenvivo.com/hls.php-89.html?get=Ly9hbGJhLXBlLWF0di1hdHYuc3RyZWFtLm1lZGlhdGlxdWVzdHJlYW0uY29tL2luZGV4Lm0zdTg=')">atv</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/americatv.html')">America</button>
            <button onclick="loadVideo('https://tvlibreonline.net/html/clarovideo.html?r=DISKIDS')">discovery kids</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/disneychannel.html')">disney chanel</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/cartoonnetwork.html')">cartton network</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/starchannel.html')">star chanel</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/tnt.html')">tnt hd</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/animalplanet.html')">animad plane</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/history.html')">histoty chanel</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/disneyjr.html')">Disney Junior</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/cartoonito.html')">Cartoonito</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/tntseries.html')">TNT Series</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/telemundopuertorico.html')">Telemundo</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/natgeo.html')">National Geographic</button>
            <button onclick="loadVideo('https://la10hd.com/tv/golperu.html'')">Golperu1</button>
            <button onclick="loadVideo('https://gol12.com/vivo/canales.php?stream=golperu')">Golperu2</button>

        </div>
    </div>
</body>
</html>

