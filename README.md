<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TrotamundoTv</title>
    <link href="https://vjs.zencdn.net/7.14.3/video-js.css" rel="stylesheet" />
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            background-color: #f4f4f4;
        }
        h1 {
            color: #fff;
            margin: 0;
            padding: 10px;
            text-align: center;
        }
        /* Fondo de inicio de sesión */
        .login-container {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-image: url('fondo.jpg');
            background-size: cover;
        }
        .login-box {
            text-align: center;
            background-color: rgba(0, 0, 0, 0.7);
            padding: 20px 30px;
            border-radius: 8px;
            color: white;
            max-width: 400px;
            width: 100%;
        }
        .login-box input, .login-box button {
            padding: 10px;
            font-size: 16px;
            width: 100%;
            border-radius: 4px;
        }
        .nav-container {
            background-color: #000;
            color: white;
            text-align: center;
            padding: 10px 0;
        }
        .button-container {
            display: flex;
            justify-content: center;
            gap: 20px;
        }
        /* Configuración general para eliminar espacios en blanco */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body, html {
    width: 100%;
    height: 100%;
    overflow-x: hidden;
    font-family: Arial, sans-serif;
}

/* Ajustes de la cabecera */
.nav-container {
    background-color: #000;
    color: white;
    text-align: center;
    padding: 10px 0;
    position: relative;
    z-index: 1;
}
      /* Carrusel de imágenes que ocupa toda la pantalla sin espacios */
.carousel {
    width: 100vw; /* Abarca todo el ancho de la pantalla */
    height: calc(100vh - 40px); /* Resta la altura de la cabecera */
    margin: 0; /* Sin margen */
    padding: 0; /* Sin relleno */
    overflow: hidden;
    background-color: #333;
    position: relative;
}

.carousel img {
    width: 100vw; /* Ocupa todo el ancho */
    height: 100vh; /* Asegura que cubra toda la altura */
    object-fit: cover; /* Cubre el contenedor sin distorsión */
    position: absolute;
    top: 0;
    left: 0;
    display: none;
}

.carousel img.active {
    display: block;
}


        /* Contenedor de canales y películas */
        .content-container {
            display: none;
            padding: 20px;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }
        .channel-box, .movie-box {
            background-color: #eaeaea;
            width: 150px;
            padding: 10px;
            border-radius: 8px;
            text-align: center;
        }
        .channel-box img, .movie-box img {
            width: 100%;
            border-radius: 4px;
        }
        button {
            background-color: #007bff;
            color: white;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
            width: 100%;
        }
        /* Reproductor de video en pantalla completa */
        #video-player-container,
        #iframe-player-container {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background-color: #000;
            z-index: 1000;
        }
        #video-player, #iframe-player {
            width: 100%;
            height: 100%;
        }
        /* Botones de control */
        .control-button {
            position: absolute;
            top: 10px;
            color: white;
            font-size: 24px;
            cursor: pointer;
            padding: 10px;
            border-radius: 50%;
            z-index: 1001;
        }
        .close-button {
            left: 10px;
            background-color: rgba(255, 0, 0, 0.7);
        }
        .tv-button {
            left: 60px;
            background-color: rgba(0, 123, 255, 0.7);
        }
        /* Menú de canales flotante */
        .channel-menu {
            position: fixed;
            top: 50px;
            left: 10px;
            background-color: rgba(0, 0, 0, 0.8);
            color: white;
            padding: 10px;
            border-radius: 8px;
            display: none;
            width: 200px;
            z-index: 1002;
        }
        
    </style>
</head>
<body>

    <!-- Login -->
    <div class="login-container">
        <div class="login-box">
            <h2>Iniciar Sesión</h2>
            <input type="text" id="id" placeholder="ID de usuario">
            <input type="password" id="password" placeholder="Contraseña">
            <button onclick="login()">Ingresar</button>
        </div>
    </div>

    <!-- Main content -->
    <div class="main-container" style="display:none;">
        <div class="nav-container">
            <h1>TrotamundoTv</h1>
            <div class="button-container">
                <button onclick="showSection('inicio')">Inicio</button>
                <button onclick="showSection('canales')">Canales</button>
                <button onclick="showSection('peliculas')">Películas</button>
            </div>
        </div>

        <!-- Inicio (Carrusel) -->
        <div class="content-container" id="inicio" style="display: flex;">
            <div class="carousel">
                <img src="halo.jfif" alt="Imagen 1" class="carousel-img active">
                <img src="lia.jfif" alt="Imagen 2" class="carousel-img">
                <img src="canaa.jpg" alt="Imagen 3" class="carousel-img">
            </div>
        </div>

        <!-- Canales -->
        <div class="content-container" id="canales">
            <div class="channel-box">
                <img src="atv.png" alt="ATV">
                <button onclick="reproducirM3U8('https://alba-pe-atv-atv.stream.mediatiquestream.com/index.m3u8')">ATV 1</button>
                <button onclick="reproducirIframe('https://atvenvivo.com/hls.php-89.html?get=Ly9hbGJhLXBlLWF0di1hdHYuc3RyZWFtLm1lZGlhdGlxdWVzdHJlYW0uY29tL2luZGV4Lm0zdTg=')">ATV 2</button>
                <button onclick="reproducirM3U8('https://alba-pe-atv-atv.stream.mediatiquestream.com/index.m3u8')">ATV 3</button>
            </div>
            <div class="channel-box">
                <img src="dd.jfif" alt="Latina">
                <button onclick="reproducirM3U8('https://redirector.rudo.video/hls-video/567ffde3fa319fadf3419efda25619456231dfea/latina/latina.smil/playlist.m3u8')">Latina 1</button>
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/latina.html')">Latina 2</button>
                <button onclick="reproducirM3U8('https://live-latinav2-mdstrm.secure.footprint.net/live-stream-mp/d1aden84nxx8u4/3330943a0248407faa8c6f5f5c874fa4/5ce7109c7398b977dc0744cd/index.m3u8')">Latina 3</button>
                <button onclick="reproducirIframe('https://atvenvivo.com/hls.php-93.html?get=Ly9qaXJlaC0yLWhscy12aWRlby11cy1pc3AuZHBzLmxpdmUvaGxzLXZpZGVvLzU2N2ZmZGUzZmEzMTlmYWRmMzQxOWVmZGEyNTYxOTQ1NjIzMWRmZWEvbGF0aW5hL2xhdGluYS5zbWlsL3BsYXlsaXN0Lm0zdTg/ZHBzc2lkPWIyNjg1MzMxMjAxNjZiZmYyYmJjNjMzNyZzaWQ9YmE1dDFsMXhiMjUzODA5MTY3MjY2YmZmMmJkOTk0OWUmbmR2Yz0w')">Latina 4</button>
                
            </div>
            <div class="channel-box">
                <img src="pana.jpg" alt="Panamericana">
                <button onclick="reproducirM3U8('https://cdnhd.iblups.com/hls/ptv5.m3u8')">Ver Panamericana</button>
            </div>
            <div class="channel-box">
                <img src="aa.jfif" alt="America">
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/americatv.html')">Ver America</button>
            </div>
            <div class="channel-box">
                <img src="tvperu.png" alt="Tv Peru">
                <button onclick="reproducirM3U8('https://cdnhd.iblups.com/hls/777b4d4cc0984575a7d14f6ee57dbcaf.m3u8')">Ver Tv Peru</button>
            </div>
            <div class="channel-box">
                <img src="sony.png" alt="Sony">
                <button onclick="reproducirM3U8('https://cdn.klowdtv.net/803B48A/n1.klowdtv.net/live1/cine_720p/playlist.m3u8')">Ver Sony</button>
            </div>
            <div class="channel-box">
                <img src="cosmo.png" alt="cosmo">
                <button onclick="reproducirM3U8('https://tv.mediacp.eu:19360/cosmos/cosmos.m3u8')">Ver Sony</button>
            </div>
            <div class="channel-box">
                <img src="kk.webp" alt="cartoon network">
                <button onclick="reproducirIframe('https://embed.sdfgnksbounce.com/embed/cartoonnetwork.html')">Cartoon Network 1</button>
                <button onclick="reproducirM3U8('http://181.78.105.146:2000/play/a03k/index.m3u8')">Cartoon Network 2</button>
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed/cartoonnetwork.html')">Cartoon Network 3</button>
            </div>
            <div class="channel-box">
                <img src="gol.jpg" alt="Gol Peru">
                <button onclick="reproducirM3U8('https://server.betzta.com/lb/golperu/index.m3u8?token=29c51188b2833e882b43400a19523c7d3c53ec09-aed7a084501b2286ca4594aa0063a17f-1730658382-1730647582&remote=38.')">Ver Gol Peru1</button>
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed/golperu.html')">Ver Gol Peru2</button>
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/golperu.html')">Ver Gol Peru3</button>
                
                

            
            </div>
            <div class="channel-box">
                <img src="qq.png" alt="National Geographic">
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/natgeo.html')">National Geographic</button>
            </div>
            <div class="channel-box">
                <img src="se.png" alt="TNT Series">
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/tntseries.html')">Ver canal</button>
            </div>
            <div class="channel-box">
                <img src="tet.png" alt="Telemundo">
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/telemundopuertorico.html')">Ver canal</button>
            </div>
            <div class="channel-box">
                <img src="caa.png" alt="Cartoonito">
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/cartoonito.html')">Ver canal</button>
            </div>
            <div class="channel-box">
                <img src="ju.jfif" alt="Disney Junior">
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/disneyjr.html')">Ver Disney Junior</button>
            </div>


        </div>
        </div>

        <!-- Películas -->
        <div class="content-container" id="peliculas">
            <div class="movie-box">
                <img src="garf.jpg" alt="Garfield">
                <button onclick="reproducirIframe('https://nuuuppp.pro/watch/7kz7jIHYMkPnCGUQ5OVCQ3jz3s7kz70Y8cv7kz7kU4p45xzpNojXZmI?h=')">Ver Garfield</button>
            </div>
            <div class="movie-box">
                <img src="Venom3.jfif" alt="Venom3">
                <button onclick="reproducirIframe('https://vidhidefast.com/v/lxni6eh6v7ds')">Ver Venom3</button>
            </div>
            <div class="movie-box">
                <img src="robot.jfif" alt="Robot salvaje">
                <button onclick="reproducirIframe('https://hlswish.com/e/fprszlndo9n1')">Ver Robot salvaje 1</button>
                <button onclick="reproducirIframe('https://nuuuppp.pro/watch/6fVeH9e1DDaSAJfCoOccOY7kz7jh2ojRoDxoTWfvNOSPPI?h=')">Ver Robot salvaje1.1</button>
            </div>
            <div class="movie-box">
                <img src="terr.jpg" alt="Terrifer3">
                <button onclick="reproducirIframe('https://vidsrc.xyz/embed/movie/tt27911000')">Ver Terrifer3</button>
            </div>
            <div class="movie-box">
                <img src="La Sustancia.jfif" alt="La Sustancia">
                <button onclick="reproducirIframe('https://hlswish.com/e/t82ki8yd6pyb')">Ver La Sustancia</button>
            </div>
            <div class="movie-box">
                <img src="al.jpeg" alt="Alien: Romulus">
                <button onclick="reproducirIframe('https://hlswish.com/e/xnx3im559fcl')">Ver Alien: Romulus</button>
            </div>
            <div class="movie-box">
                <img src="yoa.jfif" alt="Yo antes de ti">
                <button onclick="reproducirIframe('https://fastbrisk.com/e/mbj6m7jgue2c')">Ver Yo antes de ti</button>
            </div>
            <div class="movie-box">
                <img src="Aquaman y el reino perdido.jfif" alt="aquaman3">
                <button onclick="reproducirIframe('https://asnwish.com/e/zidnda5xvskl')">Ver aquaman3</button>
            </div>
            <div class="movie-box">
                <img src="wonka.jfif" alt="wonka">
                <button onclick="reproducirIframe('https://asnwish.com/e/1gtafknvymij')">Ver wonka</button>
            </div>
            <div class="movie-box">
                <img src="Kung Fu Panda 4.jfif" alt="kunfu panda4">
                <button onclick="reproducirIframe('https://jodwish.com/e/qfmi115yrwg8')">Ver kunfu panda4</button>
            </div>
            <div class="movie-box">
                <img src="blue beete.jfif" alt="blue beete">
                <button onclick="reproducirIframe('https://jodwish.com/e/qfmi115yrwg8')">Ver blue beete</button>
            </div>
        </div>
    </div>

    <!-- Reproductor M3U8 -->
    <div id="video-player-container">
        <span class="control-button close-button" onclick="cerrarReproductor()">✖</span>
        <span class="control-button tv-button" onclick="toggleMenu()">📺</span>
        <video id="video-player" class="video-js vjs-default-skin" controls preload="auto"></video>
    </div>

    <!-- Reproductor Iframe -->
    <div id="iframe-player-container">
        <span class="control-button close-button" onclick="cerrarIframe()">✖</span>
        <span class="control-button tv-button" onclick="toggleMenu()">📺</span>
        <iframe id="iframe-player" frameborder="0" allowfullscreen sandbox="allow-same-origin allow-scripts"></iframe>
        
    </div>

    <!-- Menú de canales flotante accesible desde ambos reproductores -->
    <div class="channel-menu" id="channel-menu">
        <button onclick="reproducirM3U8('https://alba-pe-atv-atv.stream.mediatiquestream.com/index.m3u8')">Canal ATV 1</button>
        <button onclick="reproducirIframe('https://atvenvivo.com/hls.php-89.html?get=Ly9hbGJhLXBlLWF0di1hdHYuc3RyZWFtLm1lZGlhdGlxdWVzdHJlYW0uY29tL2luZGV4Lm0zdTg=')">Canal ATV 2</button>
        <button onclick="reproducirM3U8('https://alba-pe-atv-atv.stream.mediatiquestream.com/index.m3u8')">Canal ATV 3</button>
        <button onclick="reproducirM3U8('https://redirector.rudo.video/hls-video/567ffde3fa319fadf3419efda25619456231dfea/latina/latina.smil/playlist.m3u8')">Canal Latina 1</button>
        <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/latina.html')">Canal Latina 2</button>
        <button onclick="reproducirM3U8('https://live-latinav2-mdstrm.secure.footprint.net/live-stream-mp/d1aden84nxx8u4/3330943a0248407faa8c6f5f5c874fa4/5ce7109c7398b977dc0744cd/index.m3u8')">Canal Latina 3</button>
        <button onclick="reproducirIframe('https://atvenvivo.com/hls.php-93.html?get=Ly9qaXJlaC0yLWhscy12aWRlby11cy1pc3AuZHBzLmxpdmUvaGxzLXZpZGVvLzU2N2ZmZGUzZmEzMTlmYWRmMzQxOWVmZGEyNTYxOTQ1NjIzMWRmZWEvbGF0aW5hL2xhdGluYS5zbWlsL3BsYXlsaXN0Lm0zdTg/ZHBzc2lkPWIyNjg1MzMxMjAxNjZiZmYyYmJjNjMzNyZzaWQ9YmE1dDFsMXhiMjUzODA5MTY3MjY2YmZmMmJkOTk0OWUmbmR2Yz0w')">Canal Latina 4</button>
        <button onclick="reproducirM3U8('https://cdnhd.iblups.com/hls/ptv5.m3u8')">Canal Panamericana</button>
        <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/americatv.html')">Canal America</button>
        <button onclick="reproducirM3U8('https://cdnhd.iblups.com/hls/777b4d4cc0984575a7d14f6ee57dbcaf.m3u8')">Tv Peru</button>
        <button onclick="reproducirM3U8('https://cdn.klowdtv.net/803B48A/n1.klowdtv.net/live1/cine_720p/playlist.m3u8')">Sony</button>
        <button onclick="reproducirM3U8('https://tv.mediacp.eu:19360/cosmos/cosmos.m3u8')">cosmo</button>
       
        <button onclick="reproducirIframe('https://embed.sdfgnksbounce.com/embed/cartoonnetwork.html')">Cartoon Network 1</button>
                <button onclick="reproducirM3U8('http://181.78.105.146:2000/play/a03k/index.m3u8')">Cartoon Network 2</button>
                <button onclick="reproducirIframe('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed/cartoonnetwork.html')">Cartoon Network 3</button>
        <button onclick="reproducirIframe('https://embed.sdfgnksbounce.com/embed2/golperu.html')">Gol Peru</button>
    </div>

    <script src="https://vjs.zencdn.net/7.14.3/video.min.js"></script>
    <script>
        function login() {
            const id = document.getElementById("id").value;
            const password = document.getElementById("password").value;
            if (id === "jhon" && password === "frio123") {
                document.querySelector('.login-container').style.display = 'none';
                document.querySelector('.main-container').style.display = 'block';
                startCarousel();
            } else {
                alert("ID o contraseña incorrectos.");
            }
        }

        function showSection(section) {
            document.querySelectorAll('.content-container').forEach(el => el.style.display = 'none');
            document.getElementById(section).style.display = 'flex';
        }

        function startCarousel() {
            let index = 0;
            const images = document.querySelectorAll('.carousel-img');
            setInterval(() => {
                images.forEach(img => img.classList.remove('active'));
                images[index].classList.add('active');
                index = (index + 1) % images.length;
            }, 3000);
        }

        function reproducirM3U8(enlaceM3U8) {
            cerrarIframe(); // Cerrar cualquier iframe abierto
            const player = videojs('video-player');
            player.src({ src: enlaceM3U8, type: 'application/x-mpegURL' });
            document.getElementById('video-player-container').style.display = 'block';
            document.getElementById('channel-menu').style.display = 'none';
            player.play();
        }

        function cerrarReproductor() {
            const player = videojs('video-player');
            player.pause();
            player.src({ src: '' });
            document.getElementById('video-player-container').style.display = 'none';
            document.getElementById('channel-menu').style.display = 'none';
        }

        function reproducirIframe(enlaceIframe) {
            cerrarReproductor(); // Cerrar cualquier M3U8 abierto
            document.getElementById('iframe-player').src = enlaceIframe;
            document.getElementById('iframe-player-container').style.display = 'block';
            document.getElementById('channel-menu').style.display = 'none';
        }
          
        // Bloquear anuncios y redirecciones
        bloquearAnuncios(iframe);

        function cerrarIframe() {
            document.getElementById('iframe-player').src = '';
            document.getElementById('iframe-player-container').style.display = 'none';
            document.getElementById('channel-menu').style.display = 'none';
        }

        function toggleMenu() {
            const menu = document.getElementById('channel-menu');
            menu.style.display = menu.style.display === 'none' ? 'block' : 'none';
        }
    </script>

</body>
</html>
