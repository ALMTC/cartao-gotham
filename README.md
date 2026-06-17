<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cartão Gotham A5</title>
    <style>
        @page {
            size: A5 landscape;
            margin: 0;
        }

        body {
            margin: 0;
            padding: 0;
            font-family: 'Impact', 'Arial Black', sans-serif;
            background: #000;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .cartao {
            width: 210mm;
            height: 148mm;
            position: relative;
            overflow: hidden;
            background: #0a0a0a;
            box-shadow: 0 0 40px rgba(255, 200, 0, 0.15);
        }

        /* Neblina */
        .neblina {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 30% 60%, rgba(50, 50, 70, 0.3) 0%, transparent 70%),
                        radial-gradient(circle at 80% 40%, rgba(40, 40, 60, 0.2) 0%, transparent 60%);
            pointer-events: none;
            z-index: 0;
        }

        /* Holofote */
        .holofote {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 120px;
            height: 100%;
            background: linear-gradient(to bottom, rgba(255, 220, 50, 0.6) 0%, transparent 90%);
            clip-path: polygon(40% 0%, 60% 0%, 100% 100%, 0% 100%);
            z-index: 1;
            opacity: 0.8;
            animation: pulsar 3s infinite alternate;
        }

        @keyframes pulsar {
            0% { opacity: 0.5; }
            100% { opacity: 0.9; }
        }

        /* Prédios (silhueta) */
        .predios {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 45%;
            z-index: 2;
            display: flex;
            align-items: flex-end;
            justify-content: space-around;
            padding: 0 5px;
        }

        .predio {
            background: #1a1a2e;
            border-radius: 2px 2px 0 0;
            box-shadow: inset 0 0 20px rgba(0,0,0,0.8);
            position: relative;
        }

        .predio::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 100%;
            background: repeating-linear-gradient(90deg, 
                rgba(255, 200, 50, 0.15) 0px, 
                rgba(255, 200, 50, 0.15) 3px,
                transparent 3px, 
                transparent 6px);
        }

        .p1 { width: 20px; height: 60%; }
        .p2 { width: 35px; height: 85%; }
        .p3 { width: 25px; height: 70%; }
        .p4 { width: 45px; height: 95%; }
        .p5 { width: 30px; height: 75%; }
        .p6 { width: 25px; height: 55%; }
        .p7 { width: 40px; height: 90%; }
        .p8 { width: 20px; height: 65%; }
        .p9 { width: 30px; height: 80%; }
        .p10 { width: 15px; height: 50%; }

        /* Luzes nos prédios */
        .luzes {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 3;
            background: repeating-linear-gradient(
                0deg,
                rgba(255, 200, 0, 0.08) 0px,
                rgba(255, 200, 0, 0.08) 2px,
                transparent 2px,
                transparent 8px
            );
            pointer-events: none;
        }

        /* Lua */
        .lua {
            position: absolute;
            top: 8%;
            right: 12%;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background: radial-gradient(circle, #f5e6b8 0%, #d4c59a 100%);
            box-shadow: 0 0 40px rgba(255, 220, 150, 0.3);
            z-index: 4;
        }

        .lua::after {
            content: '';
            position: absolute;
            top: 2px;
            left: 6px;
            width: 22px;
            height: 22px;
            border-radius: 50%;
            background: #0a0a0a;
            box-shadow: inset -2px -2px 8px rgba(0,0,0,0.5);
        }

        /* Morcegos */
        .morcego {
            position: absolute;
            color: #1a1a2e;
            font-size: 20px;
            z-index: 5;
            opacity: 0.6;
        }
        .m1 { top: 12%; left: 20%; transform: rotate(-10deg); }
        .m2 { top: 18%; left: 60%; transform: rotate(15deg) scale(0.8); }
        .m3 { top: 8%; left: 45%; transform: rotate(-20deg) scale(0.6); }
        .m4 { top: 25%; left: 15%; transform: rotate(5deg) scale(0.9); }
        .m5 { top: 30%; left: 70%; transform: rotate(-15deg) scale(0.7); }

        /* Título - CAPA */
        .titulo-capa {
            position: absolute;
            top: 18%;
            left: 50%;
            transform: translateX(-50%);
            z-index: 10;
            text-align: center;
            color: #ffd700;
            text-shadow: 0 0 20px #ffd700, 0 0 40px #ff8800, 0 0 60px #ff5500;
            font-size: 28px;
            letter-spacing: 4px;
            background: rgba(0,0,0,0.5);
            padding: 8px 20px;
            border-radius: 8px;
            border: 2px solid rgba(255, 215, 0, 0.3);
        }

        .titulo-capa span {
            display: block;
            font-size: 14px;
            color: #ccc;
            text-shadow: none;
            margin-top: 4px;
            font-family: 'Courier New', monospace;
        }

        /* INTERIOR - mensagem */
        .interior {
            display: none; /* oculto na capa */
        }

        /* Verso (página 2) */
        .pagina2 .neblina { opacity: 0.5; }
        .pagina2 .predios { opacity: 0.3; }
        .pagina2 .holofote { opacity: 0.2; }

        .mensagem {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 20;
            text-align: center;
            color: #ffd700;
            text-shadow: 0 0 15px rgba(255, 215, 0, 0.4);
            width: 85%;
            padding: 20px;
            background: rgba(0,0,0,0.6);
            border-radius: 12px;
            border: 1px solid rgba(255, 215, 0, 0.2);
            backdrop-filter: blur(2px);
        }

        .mensagem h1 {
            font-size: 22px;
            margin: 0 0 8px 0;
            color: #fff;
            text-shadow: 0 0 30px rgba(255, 255, 255, 0.2);
            letter-spacing: 2px;
        }

        .mensagem .alert {
            font-size: 18px;
            color: #ffaa00;
            font-weight: bold;
        }

        .mensagem .culpado {
            font-size: 28px;
            color: #ff5500;
            text-shadow: 0 0 30px #ff5500;
            margin: 10px 0;
            letter-spacing: 4px;
        }

        .mensagem .parabens {
            font-size: 16px;
            color: #ffd700;
            margin: 12px 0 6px 0;
        }

        .mensagem .final {
            font-size: 18px;
            color: #fff;
            text-shadow: 0 0 20px rgba(255,255,255,0.3);
            margin-top: 8px;
        }

        .mensagem .final span {
            color: #ffd700;
        }

        /* Estrelas */
        .estrelas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            pointer-events: none;
        }
        .estrela {
            position: absolute;
            width: 2px;
            height: 2px;
            background: #fff;
            border-radius: 50%;
            opacity: 0.3;
        }
        .e1 { top: 5%; left: 10%; }
        .e2 { top: 15%; left: 85%; }
        .e3 { top: 3%; left: 40%; }
        .e4 { top: 22%; left: 5%; }
        .e5 { top: 10%; left: 75%; }
        .e6 { top: 28%; left: 55%; }
        .e7 { top: 7%; left: 30%; }
        .e8 { top: 35%; left: 90%; }

        /* Impressão */
        @media print {
            body { margin: 0; padding: 0; }
            .cartao { width: 100%; height: 100%; page-break-after: always; }
            .pagina2 { page-break-after: avoid; }
        }
    </style>
</head>
<body>

    <!-- CAPA (PÁGINA 1) -->
    <div class="cartao">
        <div class="estrelas">
            <div class="estrela e1"></div><div class="estrela e2"></div>
            <div class="estrela e3"></div><div class="estrela e4"></div>
            <div class="estrela e5"></div><div class="estrela e6"></div>
            <div class="estrela e7"></div><div class="estrela e8"></div>
        </div>
        <div class="neblina"></div>
        <div class="holofote"></div>
        <div class="lua"></div>
        <div class="morcego m1">🦇</div>
        <div class="morcego m2">🦇</div>
        <div class="morcego m3">🦇</div>
        <div class="morcego m4">🦇</div>
        <div class="morcego m5">🦇</div>
        <div class="predios">
            <div class="predio p1"></div>
            <div class="predio p2"></div>
            <div class="predio p3"></div>
            <div class="predio p4"></div>
            <div class="predio p5"></div>
            <div class="predio p6"></div>
            <div class="predio p7"></div>
            <div class="predio p8"></div>
            <div class="predio p9"></div>
            <div class="predio p10"></div>
        </div>
        <div class="luzes"></div>
        <div class="titulo-capa">
            🦇 ALERTA EM GOTHAM! 🦇
            <span>Cidade sob vigilância</span>
        </div>
    </div>

    <!-- INTERIOR (PÁGINA 2) -->
    <div class="cartao pagina2">
        <div class="estrelas">
            <div class="estrela e1"></div><div class="estrela e2"></div>
            <div class="estrela e3"></div><div class="estrela e4"></div>
            <div class="estrela e5"></div><div class="estrela e6"></div>
            <div class="estrela e7"></div><div class="estrela e8"></div>
        </div>
        <div class="neblina"></div>
        <div class="holofote"></div>
        <div class="lua"></div>
        <div class="morcego m1">🦇</div>
        <div class="morcego m2">🦇</div>
        <div class="morcego m3">🦇</div>
        <div class="morcego m4">🦇</div>
        <div class="morcego m5">🦇</div>
        <div class="predios">
            <div class="predio p1"></div>
            <div class="predio p2"></div>
            <div class="predio p3"></div>
            <div class="predio p4"></div>
            <div class="predio p5"></div>
            <div class="predio p6"></div>
            <div class="predio p7"></div>
            <div class="predio p8"></div>
            <div class="predio p9"></div>
            <div class="predio p10"></div>
        </div>
        <div class="luzes"></div>

        <div class="mensagem">
            <h1>🦇 ALERTA EM GOTHAM! 🦇</h1>
            <p class="alert">Foi detectado um aumento anormal de idade.</p>
            <p>Após investigação, descobrimos o culpado:</p>
            <div class="culpado">VOCÊ!</div>
            <p class="parabens">Parabéns por subir mais um nível!</p>
            <div class="final">Feliz Aniversário, <span>Cavaleiro das Trevas!</span> 🦇🎉</div>
        </div>
    </div>

</body>
</html>
