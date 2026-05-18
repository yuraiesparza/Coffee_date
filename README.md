# Coffee_date
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>💕 Tienes un mensaje especial 💕</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            min-height: 100vh;
            background: linear-gradient(135deg, #ff6b9d 0%, #c44569 50%, #f8b500 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        /* Corazones flotantes */
        .floating-hearts {
            position: fixed;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .heart {
            position: absolute;
            font-size: 2rem;
            animation: floatHeart 6s ease-in-out infinite;
            opacity: 0.6;
        }

        @keyframes floatHeart {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(10deg); }
        }

        /* Pantalla inicial */
        .phone-screen {
            background: white;
            border-radius: 40px;
            padding: 20px;
            box-shadow: 0 25px 80px rgba(0,0,0,0.3);
            max-width: 380px;
            width: 90%;
            z-index: 10;
            position: relative;
        }

        .notch {
            width: 120px;
            height: 25px;
            background: #1a1a1a;
            border-radius: 20px;
            margin: 0 auto 15px;
        }

        .content {
            text-align: center;
            padding: 20px;
        }

        /* Animación del sobre */
        .envelope-container {
            position: relative;
            margin: 30px auto;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .envelope-container:hover {
            transform: scale(1.05);
        }

        .envelope {
            width: 200px;
            height: 150px;
            background: linear-gradient(145deg, #ff85a2, #ff6b9d);
            border-radius: 10px;
            position: relative;
            margin: 0 auto;
            box-shadow: 0 10px 30px rgba(255,107,157,0.4);
        }

        .envelope-flap {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 70px;
            background: linear-gradient(180deg, #ff9eb5, #ff85a2);
            clip-path: polygon(0 0, 50% 100%, 100% 0);
            transition: transform 0.5s ease;
            transform-origin: top center;
        }

        .envelope.open .envelope-flap {
            transform: rotateX(180deg);
        }

        .letter {
            position: absolute;
            width: 160px;
            height: 110px;
            background: #fff9f0;
            border-radius: 5px;
            top: 30px;
            left: 50%;
            transform: translateX(-50%);
            transition: transform 0.5s ease 0.3s;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            font-size: 2rem;
        }

        .envelope.open .letter {
            transform: translateX(-50%) translateY(-60px);
        }

        .tap-hint {
            margin-top: 20px;
            color: #ff6b9d;
            font-weight: 600;
            animation: bounce 1s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-5px); }
        }

        /* Contenido de la invitación */
        .invitation {
            display: none;
            animation: fadeIn 0.8s ease;
        }

        .invitation.show {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .invitation-header {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }

        .invitation-subtitle {
            color: #666;
            font-size: 1rem;
            margin-bottom: 25px;
        }

        .emoji-row {
            font-size: 2.5rem;
            margin: 20px 0;
        }

        .date-card {
            background: linear-gradient(135deg, #fff9f0, #ffe4ec);
            border-radius: 20px;
            padding: 25px;
            margin: 20px 0;
            border: 3px solid #ff6b9d;
        }

        .date-card h3 {
            color: #c44569;
            font-size: 1.3rem;
            margin-bottom: 15px;
        }

        .activity-item {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            margin: 15px 0;
            font-size: 1.1rem;
            color: #333;
        }

        .activity-icon {
            font-size: 2rem;
        }

        .plus-sign {
            font-size: 2rem;
            color: #ff6b9d;
            font-weight: bold;
        }

        .the-question {
            background: linear-gradient(135deg, #c44569, #ff6b9d);
            color: white;
            padding: 25px;
            border-radius: 20px;
            margin-top: 25px;
        }

        .the-question h2 {
            font-size: 1.5rem;
            margin-bottom: 10px;
        }

        .the-question p {
            font-size: 0.95rem;
            opacity: 0.9;
        }

        /* Botones de respuesta */
        .buttons-container {
            display: flex;
            gap: 15px;
            margin-top: 25px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .btn {
            padding: 15px 35px;
            border: none;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: inherit;
        }

        .btn-yes {
            background: linear-gradient(135deg, #ff6b9d, #ff85a2);
            color: white;
            box-shadow: 0 5px 20px rgba(255,107,157,0.4);
        }

        .btn-yes:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 30px rgba(255,107,157,0.6);
        }

        .btn-no {
            background: #f0f0f0;
            color: #999;
            position: relative;
        }

        .btn-no:hover {
            background: #e0e0e0;
        }

        /* Pantalla de éxito */
        .success-screen {
            display: none;
            text-align: center;
            animation: celebrate 0.8s ease;
        }

        .success-screen.show {
            display: block;
        }

        @keyframes celebrate {
            0% { transform: scale(0.5); opacity: 0; }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); opacity: 1; }
        }

        .success-emoji {
            font-size: 5rem;
            animation: wiggle 1s infinite;
        }

        @keyframes wiggle {
            0%, 100% { transform: rotate(0deg); }
            25% { transform: rotate(10deg); }
            75% { transform: rotate(-10deg); }
        }

        .success-text {
            font-size: 1.8rem;
            color: #c44569;
            margin: 20px 0;
            font-weight: 700;
        }

        .success-message {
            color: #666;
            font-size: 1rem;
            line-height: 1.6;
        }

        .countdown {
            margin-top: 20px;
            font-size: 1.2rem;
            color: #ff6b9d;
            font-weight: 600;
        }

        /* UNO Cards decorativas */
        .uno-cards {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin: 20px 0;
        }

        .uno-card {
            width: 50px;
            height: 70px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 1.2rem;
            color: white;
            box-shadow: 0 3px 10px rgba(0,0,0,0.2);
            animation: cardFloat 2s ease-in-out infinite;
        }

        .uno-card:nth-child(1) {
            background: linear-gradient(135deg, #ff0000, #cc0000);
            animation-delay: 0s;
        }
        .uno-card:nth-child(2) {
            background: linear-gradient(135deg, #00ff00, #00cc00);
            animation-delay: 0.2s;
        }
        .uno-card:nth-child(3) {
            background: linear-gradient(135deg, #0000ff, #0000cc);
            animation-delay: 0.4s;
        }
        .uno-card:nth-child(4) {
            background: linear-gradient(135deg, #ffff00, #ffcc00);
            animation-delay: 0.6s;
        }

        @keyframes cardFloat {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-10px) rotate(5deg); }
        }

        /* Café decorativo */
        .coffee-cup {
            position: relative;
            display: inline-block;
        }

        .steam {
            position: absolute;
            top: -20px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 5px;
        }

        .steam span {
            width: 8px;
            height: 20px;
            background: rgba(139, 90, 43, 0.3);
            border-radius: 50%;
            animation: steam 1.5s ease-in-out infinite;
        }

        .steam span:nth-child(2) {
            animation-delay: 0.3s;
        }

        .steam span:nth-child(3) {
            animation-delay: 0.6s;
        }

        @keyframes steam {
            0%, 100% { 
                transform: translateY(0) scale(1); 
                opacity: 0.3;
            }
            50% { 
                transform: translateY(-10px) scale(1.2); 
                opacity: 0.6;
            }
        }

        /* Cursor personalizado */
        .cursor-love {
            cursor: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='30' height='30' style='font-size:24px' viewBox='0 0 24 24'><text y='20'>💕</text></svg>"), auto;
        }

        /* Confetti */
        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            top: -10px;
            border-radius: 50%;
            animation: confettiFall 3s ease-in forwards;
            z-index: 100;
        }

        @keyframes confettiFall {
            to {
                transform: translateY(100vh) rotate(720deg);
                opacity: 0;
            }
        }

        /* Respuesta coqueta al pasar el mouse por "No" */
        .no-message {
            position: absolute;
            background: #c44569;
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.8rem;
            white-space: nowrap;
            opacity: 0;
            transition: opacity 0.3s;
            pointer-events: none;
            right: 0;
            top: -40px;
        }

        .btn-no:hover .no-message {
            opacity: 1;
        }

        /* Estilo para pantallas pequeñas */
        @media (max-width: 400px) {
            .phone-screen {
                border-radius: 25px;
                padding: 15px;
            }

            .invitation-header {
                font-size: 2rem;
            }

            .btn {
                padding: 12px 25px;
                font-size: 1rem;
            }
        }
    </style>
</head>
<body class="cursor-love">

    <!-- Corazones flotantes de fondo -->
    <div class="floating-hearts" id="hearts"></div>

    <div class="phone-screen">
        <div class="notch"></div>

        <!-- Sobre cerrado -->
        <div class="content" id="envelopeScreen">
            <div class="envelope-container" onclick="openEnvelope()">
                <div class="envelope" id="envelope">
                    <div class="envelope-flap"></div>
                    <div class="letter">💌</div>
                </div>
            </div>
            <p class="tap-hint">✨ Toca el sobre ✨</p>
        </div>

        <!-- Invitación -->
        <div class="invitation" id="invitation">
            <div class="content">
                <div class="invitation-header">🌸 ¡Hola! 🌸</div>
                <div class="invitation-subtitle">Tengo algo especial para ti... 💫</div>

                <div class="uno-cards">
                    <div class="uno-card">7</div>
                    <div class="uno-card">+2</div>
                    <div class="uno-card">4</div>
                    <div class="uno-card">+4</div>
                </div>

                <div class="date-card">
                    <h3>🎯 ¿Qué te parece si...?</h3>
                    
                    <div class="activity-item">
                        <span class="activity-icon">☕</span>
                        <span>Tomamos un café</span>
                    </div>

                    <div class="plus-sign">➕</div>

                    <div class="activity-item">
                        <span class="activity-icon">🃏</span>
                        <span>Jugamos una partida de UNO</span>
                    </div>

                    <div class="plus-sign">💕</div>

                    <div class="activity-item">
                        <span class="activity-icon">😏</span>
                        <span>Nos reímos juntos</span>
                    </div>
                </div>

                <div class="the-question">
                    <h2>¿Aceptas esta cita? 🤭</h2>
                    <p>(No puedes decir que no... ¡ya lo sabes! 😜)</p>
                </div>

                <div class="buttons-container">
                    <button class="btn btn-yes" onclick="sayYes()">
                        ¡Sí, vamos! 💕
                    </button>
                    <button class="btn btn-no">
                        Mmm... 🤔
                        <span class="no-message">¡Esa no es una opción! 😤💕</span>
                    </button>
                </div>
            </div>
        </div>

        <!-- Pantalla de éxito -->
        <div class="success-screen" id="successScreen">
            <div class="content">
                <div class="success-emoji">🎉🥳💕</div>
                <div class="success-text">¡Entonces es una cita!</div>
                <div class="success-message">
                    No puedo creer que hayas dicho que sí 🥰<br>
                    Va a ser la mejor cita, lo prometido 💫<br><br>
                    <strong>PD:</strong> Prepárate para perder en UNO... soy muy mala perdendo 😈🃏
                </div>

                <div class="uno-cards" style="margin-top: 30px;">
                    <div class="uno-card">7</div>
                    <div class="uno-card">🃏</div>
                    <div class="uno-card">+2</div>
                    <div class="uno-card">7</div>
                </div>

                <p class="countdown">¡Nos vemos pronto! ☕💕</p>
            </div>
        </div>
    </div>

    <script>
        // Crear corazones flotantes
        function createFloatingHearts() {
            const container = document.getElementById('hearts');
            const hearts = ['❤️', '💕', '💖', '💗', '☕', '🃏'];

            for (let i = 0; i < 15; i++) {
                const heart = document.create
