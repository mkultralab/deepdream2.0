# deepdream2.0.html
geopolitics intel

<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PIP-BOY 2000 - AIRBORNE GLOBAL ATLAS</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Courier+Prime:ital,wght@0,400;0,700;1,400;1,700&display=swap');

        :root {
            --pip-amber: #ffb000;
            --pip-amber-dim: #996a00;
            --pip-bg: #120a00;
            --pip-crt-glare: rgba(255, 176, 0, 0.03);
            --vector-land: rgba(255, 176, 0, 0.06);
            --alert-drone: #ff3c00;
            --alert-jet: #00d2ff;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Courier Prime', monospace;
            user-select: none;
        }

        body {
            background-color: #050300;
            color: var(--pip-amber);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            padding: 20px;
        }

        /* Pip-Boy 2000 Hardware Frame */
        .pipboy-housing {
            width: 100%;
            max-width: 1500px;
            height: 95vh;
            background: linear-gradient(135deg, #2c2a25 0%, #1a1916 100%);
            border: 12px solid #3a3731;
            border-radius: 40px;
            box-shadow: inset 0 0 40px rgba(0,0,0,0.9), 0 25px 50px rgba(0,0,0,0.8);
            position: relative;
            padding: 25px;
            display: flex;
            flex-direction: column;
        }

        /* CRT Screen Simulation Overlay */
        .crt-screen {
            flex: 1;
            background-color: var(--pip-bg);
            border: 6px solid var(--pip-amber-dim);
            border-radius: 20px;
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            box-shadow: inset 0 0 60px rgba(0,0,0,1);
        }

        .crt-screen::before {
            content: " ";
            display: block;
            position: absolute;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 10, 0, 0) 50%, rgba(0, 0, 0, 0.4) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
            z-index: 10;
            background-size: 100% 4px, 6px 100%;
            pointer-events: none;
        }

        .crt-screen::after {
            content: "";
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: radial-gradient(circle, var(--pip-crt-glare) 0%, rgba(0,0,0,0) 80%);
            pointer-events: none;
            z-index: 11;
        }

        /* Top Status Header */
        .pip-header {
            border-bottom: 2px dashed var(--pip-amber);
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: bold;
            letter-spacing: 2px;
            background: rgba(255, 176, 0, 0.02);
        }

        .scanline-anim {
            animation: scanline 8s linear infinite;
            background: linear-gradient(to bottom, rgba(255,176,0,0) 0%, rgba(255,176,0,0.1) 10%, rgba(255,176,0,0) 11%);
            position: absolute;
            width: 100%;
            height: 100%;
            z-index: 5;
            pointer-events: none;
        }

        @keyframes scanline {
            0% { transform: translateY(-100%); }
            100% { transform: translateY(100%); }
        }

        /* Main Content Layout */
        .system-interface {
            display: flex;
            flex: 1;
            height: calc(100% - 45px);
            position: relative;
        }

        /* Left Side: Map Framework */
        .map-container {
            flex: 6.2;
            position: relative;
            border-right: 2px dashed var(--pip-amber-dim);
            background: radial-gradient(circle at center, #1b0f00 0%, #0c0700 100%);
        }

        #mapCanvas {
            width: 100%;
            height: 100%;
            display: block;
            cursor: crosshair;
        }

        /* Right Side: Data Intel Feed Window & System Specs */
        .intel-sidebar {
            flex: 3.8;
            display: flex;
            flex-direction: column;
            background: rgba(10, 5, 0, 0.6);
            height: 100%;
            overflow: hidden;
        }

        .intel-header {
            background: var(--pip-amber-dim);
            color: var(--pip-bg);
            padding: 8px;
            font-weight: bold;
            font-size: 0.9rem;
            letter-spacing: 1px;
            display: flex;
            justify-content: space-between;
        }

        .news-feed {
            flex: 1;
            overflow-y: auto;
            padding: 10px;
            border-bottom: 2px dashed var(--pip-amber-dim);
        }

        /* Hardware Documentation Section */
        .hardware-docs {
            height: 160px;
            padding: 12px;
            background: rgba(20, 12, 0, 0.8);
            font-size: 0.75rem;
            line-height: 1.4;
            overflow-y: auto;
        }

        .docs-title {
            font-weight: bold;
            text-transform: uppercase;
            border-bottom: 1px solid var(--pip-amber);
            margin-bottom: 6px;
            padding-bottom: 2px;
            letter-spacing: 1px;
        }

        /* Custom Scrollbar */
        .news-feed::-webkit-scrollbar, .hardware-docs::-webkit-scrollbar {
            width: 6px;
        }
        .news-feed::-webkit-scrollbar-track, .hardware-docs::-webkit-scrollbar-track {
            background: var(--pip-bg);
        }
        .news-feed::-webkit-scrollbar-thumb, .hardware-docs::-webkit-scrollbar-thumb {
            background: var(--pip-amber-dim);
        }

        .news-item {
            border: 1px solid var(--pip-amber-dim);
            padding: 10px;
            margin-bottom: 12px;
            background: rgba(255, 176, 0, 0.02);
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .news-item:hover {
            background: rgba(255, 176, 0, 0.1);
            border-color: var(--pip-amber);
            box-shadow: 0 0 10px rgba(255,176,0,0.3);
        }

        .news-time {
            font-size: 0.75rem;
            color: var(--pip-amber-dim);
            margin-bottom: 4px;
            display: flex;
            justify-content: space-between;
        }

        .news-title {
            font-size: 0.85rem;
            font-weight: bold;
            line-height: 1.3;
            margin-bottom: 6px;
        }

        .news-summary {
            font-size: 0.75rem;
            color: rgba(255, 176, 0, 0.8);
            margin-bottom: 8px;
        }

        .news-link {
            display: inline-block;
            font-size: 0.75rem;
            color: var(--pip-bg);
            background-color: var(--pip-amber);
            padding: 3px 8px;
            text-decoration: none;
            font-weight: bold;
            border: 1px solid transparent;
            user-select: auto; /* Permite interação direta */
        }

        .news-link:hover {
            background-color: #ffffff;
            color: #000000;
            box-shadow: 0 0 8px #ffffff;
        }

        /* Overlay UI HUD Controls */
        .hud-overlay {
            position: absolute;
            bottom: 15px;
            left: 15px;
            background: rgba(18, 10, 0, 0.85);
            border: 1px solid var(--pip-amber);
            padding: 10px;
            font-size: 0.8rem;
            pointer-events: none;
            z-index: 20;
        }

        .hud-line {
            margin-bottom: 4px;
        }

        .target-selector {
            position: absolute;
            top: 15px;
            left: 15px;
            z-index: 20;
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
            max-width: 80%;
        }

        .pip-btn {
            background: transparent;
            border: 1px solid var(--pip-amber);
            color: var(--pip-amber);
            padding: 6px 12px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.75rem;
        }

        .pip-btn.active, .pip-btn:hover {
            background: var(--pip-amber);
            color: var(--pip-bg);
            box-shadow: 0 0 8px var(--pip-amber);
        }

        .glitch-text {
            text-shadow: 0 0 4px var(--pip-amber);
        }
    </style>
</head>
<body>

<div class="pipboy-housing">
    <div class="crt-screen">
        <div class="scanline-anim"></div>
        
        <div class="pip-header">
            <span class="glitch-text">PIP-BOY 2000 PLUS</span>
            <span>MAP-ATLAS v5.10 [INTEGRAÇÃO MULTI-VETOR]</span>
            <span id="live-timestamp">09 JUN 2026 23:31:00</span>
        </div>

        <div class="system-interface">
            
            <div class="map-container">
                <div class="target-selector">
                    <button class="pip-btn active" id="btn-global" onclick="switchView('global')">GLOBAL GRID</button>
                    <button class="pip-btn" id="btn-ukr" onclick="switchView('ukraine')">TEATRO: UCRÂNIA</button>
                    <button class="pip-btn" id="btn-pal" onclick="switchView('palestine')">TEATRO: PALESTINA</button>
                    <button class="pip-btn" id="btn-irn" onclick="switchView('iran')">TEATRO: IRÃ / GOLFO</button>
                </div>
                
                <canvas id="mapCanvas"></canvas>

                <div class="hud-overlay">
                    <div class="hud-line"><span style="color:#00d2ff;">●</span> COMUNICAÇÕES SIGINT: INTERCEPTANDO</div>
                    <div class="hud-line">MÓDULO: GEOPOLÍTICA &amp; ATAQUES CIBERNÉTICOS</div>
                    <div class="hud-line" id="coordinates-hud">LAT: --.---- | LON: --.----</div>
                </div>
            </div>

            <div class="intel-sidebar">
                <div class="intel-header">
                    <span>WIRE DATA FEED [CONFLITOS MUNDIAIS]</span>
                    <span id="alert-counter">0 ALERTA(S)</span>
                </div>
                <div class="news-feed" id="newsFeed">
                    </div>

                <div class="hardware-docs">
                    <div class="docs-title">■ ARQUITETURA HARDWARE: PIP-BOY 2000</div>
                    <p style="margin-bottom: 6px;">
                        Módulo de inteligência geopolítica ampliado. Coleta fluxos de capitais sancionados, exploits de redes SCADA e infraestruturas táticas comprometidas.
                    </p>
                    <p style="font-weight: bold; color: #ffb000; margin-bottom: 2px;">VETORES IDENTIFICADOS:</p>
                    <ul style="padding-left: 12px; margin-bottom: 4px;">
                        <li><span style="color: #ff3c00;">● VETOR KINETIC (VERMELHO):</span> Impactos físicos, drones ou ataques locais.</li>
                        <li><span style="color: #00d2ff;">● VETOR CYBER/FIN (AZUL):</span> Operações Hacking, Sanções de Guerra ou Guerra Eletrônica.</li>
                    </ul>
                </div>
            </div>

        </div>
    </div>
</div>

<script>
    // Banco de Dados Expandido e Categorizado (Junho 2026)
    const intelDatabase = [
        {
            title: "CIBERGUERRA: INVASÃO EM SISTEMA SCADA DE ENERGIA",
            time: "09 JUN 2026 | 02:15 AM",
            source: "Wired / Cyber Defense",
            summary: "Ataque cibernético sofisticado de negação de serviço distribuído (DDoS) e malware industrial comprometeu subestação secundária no norte da Ucrânia.",
            url: "https://www.wired.com/",
            theater: "ukraine",
            lat: 50.4501, lon: 30.5234,
            type: "HACKER / CYBER",
            motive: "Piscando devido ao surto de tráfego malicioso e desativação remota de relés de proteção de energia por agentes estatais.",
            color: "#00d2ff"
        },
        {
            title: "GEOPOLÍTICA: REUNIÃO DE EMERGÊNCIA SOBRE ROTAS DO MAR NEGRO",
            time: "09 JUN 2026 | 04:50 PM",
            source: "Reuters",
            summary: "Diplomatas negociam de emergência novos corredores de exportação agrícola sob ameaça de bloqueios de minas marítimas autônomas.",
            url: "https://www.reuters.com/",
            theater: "ukraine",
            lat: 46.4825, lon: 30.7233,
            type: "GEOPOLÍTICA",
            motive: "Piscando devido a movimentações de frotas navais e remapeamento estratégico de restrições de tráfego marítimo.",
            color: "#00d2ff"
        },
        {
            title: "FINANÇAS DE GUERRA: RASTREAMENTO DE CRIPTOATIVOS DO TERROR",
            time: "09 JUN 2026 | 08:12 PM",
            source: "Bloomberg / OFAC",
            summary: "Agências ocidentais congelam carteiras digitais movimentando milhões em stablecoins destinadas ao financiamento logístico de milícias locais.",
            url: "https://www.bloomberg.com/",
            theater: "palestine",
            lat: 31.5000, lon: 34.4667,
            type: "GUERRA FINANCEIRA",
            motive: "Piscando para sinalizar a interceptação e o bloqueio de fluxos de capital descentralizados operados em redes blockchain clandestinas.",
            color: "#00d2ff"
        },
        {
            title: "ATAQUE DE DRONE EM LINHA DE TRANSMISSÃO EM ORYOL",
            time: "09 JUN 2026 | 08:28 AM",
            source: "Atlantic Council",
            summary: "Ataque cinético hostil via drone de alta velocidade visando infraestrutura de energia regional. Grade elétrica severamente avariada.",
            url: "https://www.atlanticcouncil.org/",
            theater: "ukraine",
            lat: 52.9651, lon: 36.0685,
            type: "DRONE HOSTIL",
            motive: "Piscando devido ao registro de impacto cinético recente contra infraestrutura de distribuição energética.",
            color: "#ff3c00"
        },
        {
            title: "SABOTAGEM HACKER CONTRA INFRAESTRUTURA DE ÁGUA",
            time: "08 JUN 2026 | 10:44 AM",
            source: "Mandiant Intel",
            summary: "Grupo hacker alinhado a um estado rival infiltrou-se via credenciais fracas em um CLP (Controlador Lógico Programável) de tratamento de água.",
            url: "https://www.mandiant.com/",
            theater: "iran",
            lat: 35.6892, lon: 51.3890,
            type: "HACKER / CYBER",
            motive: "Piscando por conta da alteração de parâmetros químicos detectada pelos sensores automatizados da planta industrial.",
            color: "#00d2ff"
        },
        {
            title: "TERRORISMO GLOBAL: CÉLULA OPERACIONAL DETECTADA NO GOLFO",
            time: "08 JUN 2026 | 11:15 PM",
            source: "CTC Sentinel",
            summary: "Operação antiterrorismo intercepta comunicações codificadas planejando ataques coordenados contra refinarias de petróleo costeiras.",
            url: "https://ctc.westpoint.edu/",
            theater: "iran",
            lat: 27.1833, lon: 56.2667,
            type: "TERRORISMO GLOBAL",
            motive: "Piscando devido ao alerta de inteligência humana e varreduras SIGINT interceptando frequências de rádio VHF não autorizadas.",
            color: "#ff3c00"
        },
        {
            title: "SUPRESSÃO ELETRÔNICA EW RESTRITA EM GAZA CENTRAL",
            time: "08 JUN 2026 | 11:10 PM",
            source: "OSINT Intel",
            summary: "Sistemas de guerra eletrônica operando em saturação máxima, derrubando redes de navegação civil comercial (GPS spoofing).",
            url: "https://www.osintcombative.com/",
            theater: "palestine",
            lat: 31.4200, lon: 34.3800,
            type: "SUPRESSÃO EW",
            motive: "Piscando devido à anomalia de sinal eletromagnético de alta frequência bloqueando canais GNSS/GPS.",
            color: "#00d2ff"
        },
        {
            title: "FINANÇAS: NOVAS SANÇÕES DO G7 IMPACTAM MERCADO DE COMBUTÍVEIS",
            time: "07 JUN 2026 | 01:22 PM",
            source: "Financial Times",
            summary: "Tetos de preços de energia mais rígidos provocam liquidações e redirecionamento de petroleiros fantasmas no mercado financeiro global.",
            url: "https://www.ft.com/",
            theater: "global",
            lat: 51.5074, lon: -0.1278,
            type: "GUERRA FINANCEIRA",
            motive: "Piscando devido a ordens imediatas de desinvestimento e bloqueios cambiais internacionais originados em bolsas ocidentais.",
            color: "#00d2ff"
        },
        {
            title: "CENTCOM REPELE DRONES KAMIKAZE NO ESTREITO",
            time: "07 JUN 2026 | 12:26 PM",
            source: "The Peninsula Qatar",
            summary: "Sistemas navais defensivos acionados no Golfo de Omã para neutralizar alvos aéreos direcionados a navios.",
            url: "https://m.thepeninsulaqatar.com/",
            theater: "iran",
            lat: 25.7570, lon: 57.9140,
            type: "DRONE HOSTIL",
            motive: "Piscando devido ao acionamento de cortina de fogo defensiva contra enxame kamikaze de curto alcance.",
            color: "#ff3c00"
        }
    ];

    // Desenho simplificado de massas de terra
    const worldCoasts = [
        [{lat: 70, lon: -160}, {lat: 60, lon: -100}, {lat: 50, lon: -50}, {lat: 25, lon: -80}, {lat: 8, lon: -80}, {lat: -5, lon: -80}, {lat: -10, lon: -40}, {lat: -50, lon: -70}],
        [{lat: 65, lon: -10}, {lat: 60, lon: 25}, {lat: 55, lon: 30}, {lat: 45, lon: 30}, {lat: 42, lon: 28}, {lat: 40, lon: 35}, {lat: 31, lon: 34}, {lat: 28, lon: 33}, {lat: 15, lon: 40}, {lat: 12, lon: 43}, {lat: 25, lon: 60}, {lat: 30, lon: 50}, {lat: 38, lon: 45}, {lat: 45, lon: 50}, {lat: 60, lon: 60}, {lat: 60, lon: 120}]
    ];

    const canvas = document.getElementById('mapCanvas');
    const ctx = canvas.getContext('2d');
    let currentTheater = 'global';
    let pulseFrame = 0;
    let mousePos = { x: -1000, y: -1000 };

    function resizeCanvas() {
        const rect = canvas.parentElement.getBoundingClientRect();
        canvas.width = rect.width;
        canvas.height = rect.height;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    canvas.addEventListener('mousemove', (e) => {
        const rect = canvas.getBoundingClientRect();
        mousePos.x = e.clientX - rect.left;
        mousePos.y = e.clientY - rect.top;
    });

    canvas.addEventListener('mouseleave', () => {
        mousePos = { x: -1000, y: -1000 };
    });

    // Renderização do Feed com tratamento de isolamento de clique
    function renderNewsFeed() {
        const newsFeedContainer = document.getElementById('newsFeed');
        newsFeedContainer.innerHTML = '';
        
        const filteredData = intelDatabase.filter(item => currentTheater === 'global' || item.theater === currentTheater);
        document.getElementById('alert-counter').innerText = `${filteredData.length} ALERTA(S) RECENTES`;

        filteredData.forEach((item) => {
            const block = document.createElement('div');
            block.className = 'news-item';
            // O clique no bloco foca o mapa
            block.setAttribute('onclick', `focusPoint(${item.lat}, ${item.lon}, '${item.theater}')`);
            
            block.innerHTML = `
                <div class="news-time"><span>${item.time}</span><span style="color:${item.color}">${item.type}</span></div>
                <div class="news-title">${item.title}</div>
                <div class="news-summary">${item.summary}</div>
                <a href="${item.url}" target="_blank" class="news-link" onclick="event.stopPropagation();">FONTE: ${item.source} ↗</a>
            `;
            newsFeedContainer.appendChild(block);
        });
    }

    function switchView(viewName) {
        currentTheater = viewName;
        document.querySelectorAll('.pip-btn').forEach(b => b.classList.remove('active'));
        if(viewName === 'global') document.getElementById('btn-global').classList.add('active');
        if(viewName === 'ukraine') document.getElementById('btn-ukr').classList.add('active');
        if(viewName === 'palestine') document.getElementById('btn-pal').classList.add('active');
        if(viewName === 'iran') document.getElementById('btn-irn').classList.add('active');
        renderNewsFeed();
    }

    function focusPoint(lat, lon, theater) {
        if(currentTheater !== theater) {
            switchView(theater);
        }
        document.getElementById('coordinates-hud').innerText = `FOCO TÁTICO -> LAT: ${lat.toFixed(4)} | LON: ${lon.toFixed(4)}`;
    }

    // Engine de Renderização Gráfica do Vetor do Radar
    function drawMap() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        pulseFrame += 0.04;

        const dimAmber = '#2b1a00';

        let mapCenterLat, mapCenterLon, mapScale;
        if (currentTheater === 'global') {
            mapCenterLat = 38.0; mapCenterLon = 25.0; mapScale = 2.4;
        } else if (currentTheater === 'ukraine') {
            mapCenterLat = 49.5; mapCenterLon = 34.5; mapScale = 18;
        } else if (currentTheater === 'palestine') {
            mapCenterLat = 31.60; mapCenterLon = 34.80; mapScale = 65;
        } else if (currentTheater === 'iran') {
            mapCenterLat = 30.0; mapCenterLon = 54.0; mapScale = 14;
        }

        function toXY(lat, lon) {
            const x = canvas.width / 2 + (lon - mapCenterLon) * mapScale * (canvas.width / 360);
            const y = canvas.height / 2 - (lat - mapCenterLat) * mapScale * (canvas.height / 180);
            return { x, y };
        }

        // Desenho da Grade Analógica CRT
        ctx.strokeStyle = dimAmber;
        ctx.lineWidth = 0.5;
        const gridGap = 40;
        for (let i = 0; i < canvas.width; i += gridGap) {
            ctx.beginPath(); ctx.moveTo(i, 0); ctx.lineTo(i, canvas.height); ctx.stroke();
        }
        for (let j = 0; j < canvas.height; j += gridGap) {
            ctx.beginPath(); ctx.moveTo(0, j); ctx.lineTo(canvas.width, j); ctx.stroke();
        }

        // Desenho dos contornos de terra
        ctx.fillStyle = "rgba(255, 176, 0, 0.015)";
        ctx.strokeStyle = "rgba(255, 176, 0, 0.12)";
        ctx.lineWidth = 1.2;

        worldCoasts.forEach(contour => {
            ctx.beginPath();
            contour.forEach((pt, idx) => {
                let coords = toXY(pt.lat, pt.lon);
                if (idx === 0) ctx.moveTo(coords.x, coords.y);
                else ctx.lineTo(coords.x, coords.y);
            });
            if(contour.length > 2) ctx.stroke();
        });

        let currentHoverTarget = null;

        // Processador de Alvos
        intelDatabase.forEach(item => {
            if (currentTheater !== 'global' && item.theater !== currentTheater) return;

            let pos = toXY(item.lat, item.lon);
            let pulseRadius = 3 + Math.abs(Math.sin(pulseFrame * 2.2) * 15);
            let alpha = 1 - (pulseRadius / 18);

            // Desenhar Pulso de Emissão de Rádio
            ctx.strokeStyle = item.color;
            ctx.globalAlpha = alpha > 0 ? alpha : 0;
            ctx.lineWidth = 1;
            ctx.beginPath(); ctx.arc(pos.x, pos.y, pulseRadius, 0, 2 * Math.PI); ctx.stroke();
            ctx.globalAlpha = 1.0;

            // Ponto Central do Vetor
            ctx.fillStyle = item.color;
            ctx.beginPath(); ctx.arc(pos.x, pos.y, 4, 0, 2 * Math.PI); ctx.fill();

            // Retículo Estático do Alvo
            ctx.strokeStyle = "rgba(255, 176, 0, 0.2)";
            ctx.lineWidth = 0.5;
            ctx.beginPath(); ctx.moveTo(pos.x - 10, pos.y); ctx.lineTo(pos.x + 10, pos.y); ctx.stroke();
            ctx.beginPath(); ctx.moveTo(pos.x, pos.y - 10); ctx.lineTo(pos.x, pos.y + 10); ctx.stroke();

            // Detecção Hoover do Cursor do Mouse
            let dist = Math.hypot(mousePos.x - pos.x, mousePos.y - pos.y);
            if (dist < 14) {
                currentHoverTarget = { item, pos };
            }
        });

        // Janela de Dados Flutuante (On-Canvas Tooltip)
        if (currentHoverTarget) {
            const { item, pos } = currentHoverTarget;
            document.getElementById('coordinates-hud').innerText = `CAPTURA MOUSE -> LAT: ${item.lat.toFixed(4)} | LON: ${item.lon.toFixed(4)}`;

            let boxW = 310; let boxH = 110;
            let boxX = pos.x + 15; let boxY = pos.y - 35;

            if (boxX + boxW > canvas.width) boxX = pos.x - boxW - 15;
            if (boxY + boxH > canvas.height) boxY = canvas.height - boxH - 15;
            if (boxY < 0) boxY = 15;

            ctx.fillStyle = "rgba(12, 6, 0, 0.98)";
            ctx.strokeStyle = item.color;
            ctx.lineWidth = 1.5;
            ctx.fillRect(boxX, boxY, boxW, boxH);
            ctx.strokeRect(boxX, boxY, boxW, boxH);

            ctx.fillStyle = item.color;
            ctx.font = "bold 10px 'Courier Prime'";
            ctx.fillText(`▲ TIPO: ${item.type}`, boxX + 10, boxY + 16);
            
            ctx.strokeStyle = "rgba(255, 176, 0, 0.25)";
            ctx.beginPath(); ctx.moveTo(boxX, boxY + 22); ctx.lineTo(boxX + boxW, boxY + 22); ctx.stroke();

            ctx.fillStyle = "#ffb000";
            ctx.font = "9px 'Courier Prime'";
            
            let textY = boxY + 36;
            let words = item.motive.split(' ');
            let line = '';
            let maxWidth = boxW - 20;

            for(let n = 0; n < words.length; n++) {
                let testLine = line + words[n] + ' ';
                if (ctx.measureText(testLine).width > maxWidth && n > 0) {
                    ctx.fillText(line, boxX + 10, textY);
                    line = words[n] + ' ';
                    textY += 12;
                } else { line = testLine; }
            }
            ctx.fillText(line, boxX + 10, textY);

            ctx.fillStyle = "rgba(255, 176, 0, 0.5)";
            ctx.font = "italic 8px 'Courier Prime'";
            ctx.fillText(`CANAIS DE INTELIGÊNCIA COM ANOMALIA ATIVA`, boxX + 10, boxY + boxH - 8);
        }

        requestAnimationFrame(drawMap);
    }

    // Atualização em Tempo Real do Relógio UTC
    setInterval(() => {
        const d = new Date();
        document.getElementById('live-timestamp').innerText = d.toUTCString().replace('GMT','UTC').toUpperCase();
    }, 1000);

    // Boot inicial
    renderNewsFeed();
    drawMap();
</script>

</body>
</html>
