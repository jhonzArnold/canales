<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TrotamundoTv</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            overflow-x: hidden; /* Prevent horizontal scrolling */
        }
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            min-height: 100vh;
            background-image: url('https://img.global.news.samsung.com/mx/wp-content/uploads/2022/08/MX_TV_Mockup_03-1.jpg');
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
        }
        .login-container.hidden {
            display: none;
        }
        .login-box {
            text-align: center;
            background-color: rgba(0, 0, 0, 0.8);
            padding: 20px 30px;
            border-radius: 8px;
            max-width: 400px;
            width: 100%;
            color: white;
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
            background-color: #000;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
            border-radius: 4px;
        }
        .login-box button:hover {
            background-color: #333;
        }
        .main-container {
            display: none;
            padding: 0;
            width: 100%;
            color: white;
            position: relative;
        }
        .main-container.active {
            display: block;
        }
        /* Header */
        .header {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 10px 0;
            background-color: #000;
            color: white;
            width: 100%;
        }
        .header h1 {
            margin: 0;
            margin-bottom: 10px;
            text-align: center;
        }
        .header .button-container {
            display: flex;
            justify-content: center;
            gap: 10px; /* Space between buttons */
        }
        .header button {
            background-color: #000;
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
            font-size: 16px;
            border-radius: 4px;
        }
        .header button:hover {
            background-color: rgba(255, 255, 255, 0.2);
        }
        /* Cerrar Sesión Button in Header */
        .header .logout-button {
            background-color: #dc3545; /* Red color for Logout */
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
            font-size: 16px;
            border-radius: 4px;
        }
        .header .logout-button:hover {
            background-color: #c82333; /* Darker red on hover */
        }
        /* Image Carousel */
        .carousel {
            position: relative;
            overflow: hidden;
            width: 100%;
            height: 50vh;
            margin: 0 auto;
        }
        .carousel img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none;
        }
        .carousel img.active {
            display: block;
        }
        /* Information Section */
        .info-section {
            background-color: rgba(255, 255, 255, 0.9); /* Semi-transparent white background */
            padding: 15px;
            border-radius: 8px;
            width: 100%; /* Full width */
            box-sizing: border-box;
            position: fixed;
            bottom: 0; /* Fixed to the bottom */
            left: 0; /* Align to the left */
            right: 0; /* Align to the right */
            display: flex; /* Changed to flex */
            align-items: center; /* Center vertically */
            justify-content: center; /* Center horizontally */
            gap: 10px; /* Space between text and icon */
            color: black; /* Text color */
        }
        .info-section h3 {
            margin: 10px 0;
            font-weight: bold;
            color: black;
        }
        .info-section p {
            color: black; /* Ensure text is black */
            opacity: 0;
            transition: opacity 1s;
        }
        /* WhatsApp Icon */
        .whatsapp-icon {
            width: 40px;
            height: 40px;
            background-color: #25D366;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            z-index: 1000; /* Ensure it's above other elements */
        }
        .whatsapp-icon img {
            width: 60%;
        }
        /* Grid for Channels and Movies */
        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 20px;
            width: 100%;
            padding: 20px;
            box-sizing: border-box;
        }
        .grid-item {
            background-color: #000;
            padding: 10px;
            border-radius: 8px;
            color: white;
            text-align: center;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
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
            background-color: #000;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 14px;
            border-radius: 4px;
            width: 100%;
        }
        .grid-item button:hover {
            background-color: #333;
        }
        /* Video Player Container */
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
            color: white;
            padding: 8px;
            cursor: pointer;
            border-radius: 50%;
            font-size: 16px;
            z-index: 1001;
        }
        .close-button { 
            right: 10px; 
            background-color: rgba(255, 0, 0, 0.7); 
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
        /* Floating Channel List inside Video Player */
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
            background-color: #000;
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
            width: 100%;
            border-radius: 4px;
        }
        .channel-list button:hover {
            background-color: #333;
        }
        /* Media Queries for Responsiveness */
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
        let currentImageIndex = 0;
        let images = [];
        let infoIndex = 0;
        const infoTexts = [
            "🌟 👀 las peliculas de estreno a un no se ven en full HD",
            "📺 Cualquier mejora escribeme ➔",
            "💡 Parches Alternativos , para cualquier equipo ➔",
        ];
        // Login Function
        function login() {
            const id = document.getElementById("id").value;
            const password = document.getElementById("password").value;
            if (id === "jhon" && password === "frio123") {
                document.querySelector('.login-container').classList.add('hidden');
                document.querySelector('.main-container').classList.add('active');
                startCarousel(); // Start carousel
            } else {
                alert("ID o contraseña incorrectos. Intenta de nuevo.");
            }
        }
        // Logout Function
        function logout() {
            document.querySelector('.main-container').classList.remove('active');
            document.querySelector('.login-container').classList.remove('hidden');
            document.getElementById("id").value = ''; // Clear ID field
            document.getElementById("password").value = ''; // Clear password field
        }
        // Start Image Carousel
        function startCarousel() {
            images = document.querySelectorAll('.carousel img');
            images[currentImageIndex].classList.add('active');
            setInterval(() => {
                images[currentImageIndex].classList.remove('active');
                currentImageIndex = (currentImageIndex + 1) % images.length;
                images[currentImageIndex].classList.add('active');
            }, 3000); // Change every 3 seconds
        }
        // Show Next Info Text
        function showNextInfo() {
            const infoSection = document.querySelector('.info-section p');
            infoSection.textContent = infoTexts[infoIndex];
            infoIndex = (infoIndex + 1) % infoTexts.length;
            infoSection.style.opacity = 1; // Show text
            // Hide text after 3 seconds
            setTimeout(() => {
                infoSection.style.opacity = 0; // Fade out text
                setTimeout(showNextInfo, 1000); // Wait 1 second before showing next text
            }, 3000); // Display each text for 3 seconds
        }
        // Show Sections Function
        function showSection(section) {
            document.querySelector('.home-section').style.display = 'none';
            document.querySelector('.channels-section').style.display = 'none';
            document.querySelector('.movies-section').style.display = 'none';
            if (section === 'home') {
                document.querySelector('.home-section').style.display = 'block';
            } else if (section === 'channels') {
                document.querySelector('.channels-section').style.display = 'block';
            } else if (section === 'movies') {
                document.querySelector('.movies-section').style.display = 'block';
            }
        }
        // Load Video Function
        function loadVideo(url) {
            var videoPlayerContainer = document.getElementById('video-player-container');
            var iframe = document.getElementById('video-player');
            // Set video URL
            iframe.src = url;
            // Show player
            videoPlayerContainer.classList.add('active');
            // Enter fullscreen
            enterFullScreen(videoPlayerContainer);
        }
        // Close Video Function
        function closeVideo() {
            var videoPlayerContainer = document.getElementById('video-player-container');
            var iframe = document.getElementById('video-player');
            // Hide player
            videoPlayerContainer.classList.remove('active');
            // Stop video
            iframe.src = "";
        }
        // Enter Fullscreen Function
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
        // Toggle Channel List Function
        function toggleChannelList() {
            var channelList = document.querySelector('.channel-list');
            channelList.classList.toggle('active');
        }
        // Initialize Info Rotation on Page Load
        window.onload = function() {
            showNextInfo(); // Start info rotation
        };
    </script>
</head>
<body>
    <!-- Login Form -->
    <div class="login-container">
        <div class="login-box">
            <h2>Iniciar Sesión</h2>
            <input type="text" id="id" placeholder="ID de usuario">
            <input type="password" id="password" placeholder="Contraseña">
            <button onclick="login()">Ingresar</button>
        </div>
    </div>
    <!-- Main Container After Login -->
    <div class="main-container">
        <div class="header">
            <h1>TrotamundoTv</h1>
            <div class="button-container">
                <button onclick="showSection('home')">Inicio</button>
                <button onclick="showSection('channels')">TV Online</button>
                <button onclick="showSection('movies')">Películas</button>
                <button class="logout-button" onclick="logout()">Cerrar Sesión</button>
            </div>
        </div>
        <div class="content-container">
            <!-- Home Section with Carousel -->
            <div class="home-section" style="display: block;">
                <div class="carousel">
                    <img src="hs.jpg" alt="Imagen 1" class="active">
                    <img src="lia.jfif" alt="Imagen 2">
                    <img src="canaa.jpg" alt="Imagen 3">
                </div>
            </div>
            <div class="channels-section" style="display: none;">
                <h2>Canales</h2>
                <div class="grid-container">
                    <div class="grid-item">
                        <img src="descarga.jfif" alt="Willax">
                        <h4>Willax</h4>
                        <button onclick="loadVideo('https://geo.dailymotion.com/player.html?video=x7x4dgx')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="dd.jfif" alt="Latina">
                        <h4>Latina</h4>
                        <button onclick="loadVideo('https://atvenvivo.com/hls.php-93.html?get=Ly9qaXJlaC0yLWhscy12aWRlby11cy1pc3AuZHBzLmxpdmUvaGxzLXZpZGVvLzU2N2ZmZGUzZmEzMTlmYWRmMzQxOWVmZGEyNTYxOTQ1NjIzMWRmZWEvbGF0aW5hL2xhdGluYS5zbWlsL3BsYXlsaXN0Lm0zdTg/ZHBzc2lkPWIyNjg1MzMxMjAxNjZiZmYyYmJjNjMzNyZzaWQ9YmE1dDFsMXhiMjUzODA5MTY3MjY2YmZmMmJkOTk0OWUmbmR2Yz0w')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="pana.jpg" alt="panamericana">
                        <h4>panamericana</h4>
                        <button onclick="loadVideo('https://cdnhd.iblups.com/hls/ptv5.m3u8')">Ver canal</button>
                    </div>
                     <div class="grid-item">
                        <img src="aa.jfif" alt="America">
                        <h4>America</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/americatv.html')">Ver canal</button>
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
                    <div class="grid-item">
                        <img src="Direct Sport.png" alt="Direct Sport1">
                        <h4>Direct Sport1</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://micanaldeportivo.com/directvsports.php')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="Direct Sport.png" alt="Direct Sport2">
                        <h4>Direct Sport2</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/directvsports.html')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="Liga.png" alt="Ligamax1">
                        <h4>Ligamax1</h4>
                        <button onclick="loadVideo('https://la10hd.com/tv/liga1max.html')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="Liga.png" alt="Ligamax1.1">
                        <h4>Ligamax1.1</h4>
                        <button onclick="loadVideo('https://gol12.com/vivo/canales.php?stream=l1max')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="atv.jfif" alt="atv">
                        <h4>atv</h4>
                        <button onclick="loadVideo('https://atvenvivo.com/hls.php-89.html?get=Ly9hbGJhLXBlLWF0di1hdHYuc3RyZWFtLm1lZGlhdGlxdWVzdHJlYW0uY29tL2luZGV4Lm0zdTg=')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="ki.png" alt="discovery kids">
                        <h4>discovery kids</h4>
                        <button onclick="loadVideo('https://tvlibreonline.net/html/clarovideo.html?r=DISKIDS')">Ver canal</button>
                    </div>
                     <div class="grid-item">
                        <img src="kk.webp" alt="cartton network">
                        <h4>cartton network</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/cartoonnetwork.html')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="ees.png" alt="star chanel">
                        <h4>star chanel</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/starchannel.html')">Ver canal</button>
                    </div>
                     <div class="grid-item">
                        <img src="tt.png" alt="tnt hd">
                        <h4>tnt hd</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/tnt.html')">Ver canal</button>
                    </div>
                     <div class="grid-item">
                        <img src="pla.png" alt="animad plane">
                        <h4>animad plane</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/animalplanet.html')">Ver canal</button>
                    </div>
                     <div class="grid-item">
                        <img src="his.jfif" alt="histoty chanel">
                        <h4>histoty chanel</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/history.html')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="ju.jfif" alt="Disney Junior">
                        <h4>Disney Junior</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/disneyjr.html')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="caa.png" alt="Cartoonito">
                        <h4>Cartoonito</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/cartoonito.html')">Ver canal</button>
                    </div>
                    <div class="grid-item">
                        <img src="se.png" alt="TNT Series">
                        <h4>TNT Series</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/tntseries.html')">Ver canal</button>
                    </div>
                     <div class="grid-item">
                        <img src="qq.png" alt="National Geographic">
                        <h4>National Geographic</h4>
                        <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/natgeo.html')">Ver canal</button>
                    </div>
                </div>
            </div>
            <div class="movies-section" style="display: none;">
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
                        <img src="Back to Black.jfif" alt="Back to Black">
                        <h4>Back to Black</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-2se7c04s9ia5.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="Aquaman y el reino perdido.jfif" alt="Aquaman y el reino perdido">
                        <h4>Aquaman y el reino perdido</h4>
                        <button onclick="loadVideo('https://asnwish.com/e/rcubldghkke8')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="Kung Fu Panda 4.jfif" alt="Kung Fu Panda 4">
                        <h4>Kung Fu Panda 4</h4>
                        <button onclick="loadVideo('https://jodwish.com/e/vs3upr0nt6bs')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="Oppenheimer.jfif" alt="Oppenheimer">
                        <h4>Oppenheimer</h4>
                        <button onclick="loadVideo('https://asnwish.com/e/yfeizpk9bu1k')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="Saw X.jfif" alt="Saw X">
                        <h4>Saw X</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-q8m15ez359pl.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="docto.jfif" alt="Doctor Strange en el multiverso de la locura">
                        <h4>Doctor Strange en el multiverso de la locura</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-rm2n3u8wfz1k.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="gua.jfif" alt="Guasón">
                        <h4>Guasón</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-u32uvhrvale8.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="yoa.jfif" alt="Yo antes de ti">
                        <h4>Yo antes de ti</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-i6ogeh2w5hah.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="leon.jfif" alt="El Rey León">
                        <h4>El Rey León</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-c3ftopv5nqel.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="gat.jfif" alt="Gato con Botas: El último deseo">
                        <h4>Gato con Botas: El último deseo</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-rvp3i5twjgoa.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="yo.jfif" alt="John Wick 4">
                        <h4>John Wick 4</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-dqw9finfbw93.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="me1.jfif" alt="Megalodón1">
                        <h4>Megalodón1</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-vt1all8l1gty.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="me2.jfif" alt="Megalodón2">
                        <h4>Megalodón2</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-cb8o0xtaig7d.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="al.jpeg" alt="Alien: Romulus">
                        <h4>Alien: Romulus</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-pz9stsy48d2h.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="sis.jfif" alt="Sismo magnitud 9.5">
                        <h4>Sismo magnitud 9.5</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-jjsflhutm25v.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="simi.jpg" alt="El planeta de los simios: Nuevo reino">
                        <h4>El planeta de los simios: Nuevo reino</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-ocon4alaq35r.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="civil.jfif" alt="Guerra Civil">
                        <h4>Guerra Civil</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-7jebr2qvb9tv.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="beat.jfif" alt="Beetlejuice Beetlejuice">
                        <h4>Beetlejuice Beetlejuice</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-tnmqaw2bgkqr.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="terr.jpg" alt="Terrifier 3: Payaso Siniestro">
                        <h4>Terrifier 3: Payaso Siniestro</h4>
                        <button onclick="loadVideo('https://hlswish.com/e/odvqzm85ot2z')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="tee.jfif" alt="Terrifier : Payaso Siniestro">
                        <h4>Terrifier : Payaso Siniestro</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-41v48hl5no9t.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="wii.jpg" alt="Winnie Pooh: Miel y Sangre1">
                        <h4>Winnie Pooh: Miel y Sangre1</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-kbpwgv55k2k7.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="win.jpg" alt="Winnie Pooh: Miel y Sangre2">
                        <h4>Winnie Pooh: Miel y Sangre2</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-yulefh32jjg5.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="mi1.jfif" alt="Misión de rescate 1">
                        <h4>Misión de rescate 1</h4>
                        <button onclick="loadVideo('https://upstream.to/embed-igf16a3hl2ig.html')">Ver película</button>
                    </div>
                    <div class="grid-item">
                        <img src="mi22.jfif" alt="Misión de rescate 2">
                        <h4>Misión de rescate 2</h4>
                        <button onclick="loadVideo('https://uqload.net/embed-76fvbnv9zf3n.html')">Ver película</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div id="video-player-container">
        <button class="close-button" onclick="closeVideo()">✖</button>
        <button class="show-channels-button" onclick="toggleChannelList()">📺</button>
        <iframe id="video-player" frameborder="0" allowfullscreen></iframe>
        <div class="channel-list">
            <button onclick="loadVideo('https://geo.dailymotion.com/player.html?video=x7x4dgx')">Willax</button>
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
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/latina.html')">Latina1</button>
            <button onclick="loadVideo('https://la10hd.com/tv/golperu.html')">golperu1</button>
            <button onclick="loadVideo('https://la10hd.com/tv/liga1max.html')">Ligamax1</button>
            <button onclick="loadVideo('https://gol12.com/vivo/canales.php?stream=l1max')">Ligamax1.1</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://micanaldeportivo.com/directvsports.php')">Direct Sport1</button>
            <button onclick="loadVideo('https://nebunexa.co/red/?get=https://embed.sdfgnksbounce.com/embed2/directvsports.html')">Direct Sport2</button>
        </div>
    </div>
    <!-- Information Section (At the Bottom) -->
    <div class="info-section">
        <h3>👤💻 Cualquier mejora:</h3>
        <p></p> <!-- Dynamic Paragraph -->
        <!-- WhatsApp Icon -->
        <a href="https://wa.me/51925519546" class="whatsapp-icon" target="_blank" title="Contactar por WhatsApp">
            <img src="https://upload.wikimedia.org/wikipedia/commons/5/5e/WhatsApp_icon.png" alt="WhatsApp">
        </a>
    </div>
</body>
</html>

