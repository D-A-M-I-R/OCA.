
<html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />
<title>🦆 La Oca Inclusiva - El Total de los Sentidos 🦆</title>
<style>
    /* Estilos iguales al anterior para cuerpo, tablero, fichas, ... */
    :root {
        --primary: #2c3e50;
        --accent: #e67e22;
        --light: #ecf0f1;
        --board-bg: #fdfefe;
        --tile-bg: #d6eaf8;
        --active-bg: #f1c40f;
        --pawn-size: 1.8rem;
    }
    body {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background: linear-gradient(135deg, var(--primary), #34495e);
        color: #333;
        margin: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        min-height: 100vh;
        padding: 0 10px 20px;
    }
    h1 {
        color: var(--light);
        text-align: center;
        font-size: 2.2rem;
        margin: 20px 0 5px;
        text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    }
    .player-setup {
        background: rgba(255,255,255,0.1);
        padding: 15px;
        border-radius: 15px;
        margin-bottom: 15px;
        text-align: center;
        width: 100%;
        max-width: 450px;
    }
    .player-setup input {
        padding: 10px;
        margin: 5px 8px 10px 8px;
        border: none;
        border-radius: 5px;
        font-size: 1rem;
        width: 90%;
        max-width: 200px;
        box-sizing: border-box;
    }
    .player-setup label {
        color: var(--light);
        font-weight: bold;
        display: block;
        margin: 10px 0 5px;
    }
    .player-setup button {
        padding: 12px 25px;
        background: var(--accent);
        color: white;
        border: none;
        border-radius: 10px;
        cursor: pointer;
        font-size: 1.1rem;
        margin-top: 10px;
        width: 100%;
        max-width: 300px;
    }
    .game-container {
        display: grid;
        grid-template-columns: repeat(7, 1fr);
        gap: 8px;
        max-width: 800px;
        width: 100%;
        padding: 15px;
        background: var(--board-bg);
        border-radius: 15px;
        box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        position: relative;
    }
    .tile {
        aspect-ratio: 1;
        background-color: var(--tile-bg);
        border-radius: 10px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        position: relative;
        border: 3px solid #bdc3c7;
        font-weight: bold;
        font-size: 1rem;
        transition: transform 0.2s;
        padding: 2px;
        word-wrap: break-word;
    }
    .tile span.icon {
        font-size: 1.8rem;
        margin-bottom: 4px;
    }
    .tile.active {
        background-color: var(--active-bg);
        border-color: #d35400;
        transform: scale(1.05);
        box-shadow: 0 0 15px var(--active-bg);
        z-index: 10;
    }
    .player-token {
        font-size: var(--pawn-size);
        position: absolute;
        bottom: 4px;
        left: 4px;
        width: 24px;
        height: 24px;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-weight: bold;
        animation: bounce 1s infinite;
        z-index: 20;
        color: white;
        text-shadow: 1px 1px 2px black;
        user-select: none;
    }
    @keyframes bounce {
        0%, 100% { transform: translateY(0); }
        50% { transform: translateY(-3px); }
    }
    .pawn-red { color: #e74c3c; }
    .pawn-blue { color: #2980b9; }
    .pawn-green { color: #27ae60; }
    .pawn-yellow { color: #f39c12; }
    .pawn-purple { color: #8e44ad; }
    .controls {
        margin-top: 15px;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 12px;
        background: rgba(255,255,255,0.1);
        padding: 18px 25px;
        border-radius: 15px;
        min-width: 280px;
        max-width: 500px;
    }
    #gameCodeDisplay {
        color: var(--light);
        font-size: 1.2rem;
        margin: 10px 0;
        font-weight: bold;
        user-select: all;
    }
    .current-player {
        color: var(--light);
        font-size: 1.3rem;
        font-weight: bold;
        padding: 10px;
        border-radius: 10px;
        background: rgba(241,196,15,0.3);
        width: 100%;
        text-align: center;
    }
    button#diceBtn {
        font-size: 1.5rem;
        padding: 12px 35px;
        background-color: var(--accent);
        color: white;
        border: none;
        border-radius: 50px;
        cursor: pointer;
        box-shadow: 0 5px 0 #d35400;
        transition: all 0.1s;
        width: 100%;
        max-width: 300px;
    }
    button#diceBtn:active {
        transform: translateY(5px);
        box-shadow: none;
    }
    button#diceBtn:disabled {
        background-color: #95a5a6;
        cursor: not-allowed;
        box-shadow: none;
    }
    #status {
        color: var(--light);
        font-size: 1.1rem;
        font-weight: bold;
        text-align: center;
        width: 100%;
    }
    .players-info {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        justify-content: center;
        width: 100%;
    }
    .player-info {
        padding: 8px 12px;
        border-radius: 20px;
        color: white;
        font-weight: bold;
        font-size: 0.9rem;
        white-space: nowrap;
    }
    .modal-overlay {
        position: fixed;
        top: 0; left: 0; right: 0; bottom: 0;
        background: rgba(0,0,0,0.8);
        display: none;
        justify-content: center;
        align-items: center;
        z-index: 1000;
        padding: 15px;
    }
    .modal {
        background: white;
        padding: 25px 30px;
        border-radius: 20px;
        text-align: center;
        max-width: 480px;
        width: 100%;
        border: 5px solid var(--accent);
        box-sizing: border-box;
    }
    .modal h2 { 
        color: var(--accent); 
        margin-bottom: 15px; 
        font-size: 1.6rem;
    }
    .modal p { 
        font-size: 1.4rem; 
        margin-bottom: 22px;
        line-height: 1.4;
    }
    .options-grid {
        display: grid;
        gap: 10px;
    }
    .option-btn {
        background: var(--primary);
        color: white;
        padding: 14px 0;
        border: none;
        border-radius: 10px;
        font-size: 1.15rem;
        cursor: pointer;
        font-weight: 600;
    }
    .option-btn:hover { background: #34495e; }
    @media (max-width: 800px) {
        .game-container { grid-template-columns: repeat(5, 1fr); }
        h1 { font-size: 1.9rem; }
        .tile { font-size: 0.95rem; }
    }
    @media (max-width: 500px) {
        .game-container { grid-template-columns: repeat(4, 1fr); }
        .player-setup input { width: 100%; max-width: none; margin: 6px 0; }
        .player-setup div { display: flex; flex-direction: column; align-items: center; }
        button#diceBtn { max-width: 100%; }
    }
</style>
</head>
<body>
<h1>🦆 La Oca Inclusiva - El Total de los Sentidos 🦆</h1>

<div class="player-setup" id="playerSetup">
    <label for="gameCodeInput">Código de Juego (5 caracteres):</label>
    <input type="text" id="gameCodeInput" maxlength="5" placeholder="Escriba el código aquí" />
    <label>Ingrese nombre de jugadores (máx 5):</label>
    <input type="text" id="player1Name" placeholder="Jugador 1" maxlength="12" />
    <input type="text" id="player2Name" placeholder="Jugador 2" maxlength="12" />
    <input type="text" id="player3Name" placeholder="Jugador 3 (opcional)" maxlength="12" />
    <input type="text" id="player4Name" placeholder="Jugador 4 (opcional)" maxlength="12" />
    <input type="text" id="player5Name" placeholder="Jugador 5 (opcional)" maxlength="12" />
    <button onclick="tryStartGame()">🚀 Entrar al Juego</button>
    <div id="generatedCode" style="margin-top: 10px; color: var(--light); font-weight: bold;"></div>
</div>

<div class="game-container" id="board" style="display:none;"></div>

<div class="controls" id="controls" style="display:none;">
    <div class="current-player" id="currentPlayer"></div>
    <div class="players-info" id="playersInfo"></div>
    <button id="diceBtn" onclick="rollDice()">🎲 Tirar el Dado</button>
    <div id="status"></div>
</div>

<!-- Modal Mensajes -->
<div id="messageModal" class="modal-overlay" role="dialog" aria-modal="true">
    <div class="modal">
        <h2 id="msgTitle"></h2>
        <p id="msgText"></p>
        <button class="option-btn" onclick="closeMessage()">✅ Continuar</button>
    </div>
</div>

<!-- Modal Preguntas -->
<div id="questionModal" class="modal-overlay" role="dialog" aria-modal="true">
    <div class="modal">
        <h2>❓ ¡Pregunta / Acertijo!</h2>
        <p id="questionText">¿Pregunta?</p>
        <div class="options-grid" id="optionsContainer"></div>
    </div>
</div>

<script>
    const totalTiles = 50;
    let players = [];
    let currentPlayerIndex = 0;
    let isMoving = false;
    let gameCode = '';

    const chessPawnCodes = ['♙', '♟', '♘', '♞', '♗'];
    const playerColors = ['#e74c3c', '#2980b9', '#27ae60', '#f39c12', '#8e44ad'];

    // Definimos nuevas penalizaciones y 4 acertijos (tipo preguntas pero con lógica)
    const specialTiles = {
        6: { type: 'rojo', action: '🔥 ROJO FUEGO: ¡TODOS aplaudan fuerte o griten FUEGO!' },
        18: { type: 'azul', action: '💧 AZUL AGUA: ¡TODOS movimientos suaves con brazos + sonido SHHH!' },
        32: { type: 'amarillo', action: '🌪️ AMARILLO AIRE: ¡TODOS SILENCIO ABSOLUTO y ESTATUAS!' },
        44: { type: 'verde', action: '🌍 VERDE TIERRA: ¡TODOS golpeen suelo/muslos rítmicamente!' },

        14: { type: 'pregunta' },
        23: { type: 'pregunta' },
        25: { type: 'acertijo' },          // Acertijo 1
        29: { type: 'penalizacion', text: '¡Marea! Retrocede 5 casillas', jumpTo: 24 },
        31: { type: 'acertijo' },          // Acertijo 2
        37: { type: 'pregunta' },
        39: { type: 'penalizacion', text: '¡Tormenta! Pierdes 1 turno', turns: 1 },
        41: { type: 'retroceso', text: '¡CALLEJÓN! Vuelve a 37', jumpTo: 37 },
        42: { type: 'penalizacion', text: '¡Enfermedad! Vuelve al inicio', jumpTo: 1 },
        43: { type: 'acertijo' },          // Acertijo 3
        45: { type: 'pregunta' },
        47: { type: 'penalizacion', text: '¡Derrumbe! Pierdes 2 turnos', turns: 2 },
        48: { type: 'penalizacion', text: '¡Rayo! Retrocede 8 casillas', jumpTo: 40 },
        49: { type: 'retroceso', text: '¡Casi! Vuelve a 45', jumpTo: 45 },
        50: { type: 'meta', text: '🎉 ¡GANASTE! Todos los sentidos activados' }
    };

    // 🔴 **MAS PREGUNTAS AÑADIDAS (20+ TOTAL)**
    const questions = [
        { q: "¿Qué sentido usas para ver?", options: ["Vista 👁️", "Oído 👂", "Olfato 👃"], correct: 0 },
        { q: "¿Qué sentido para escuchar?", options: ["Vista", "Oído 👂", "Tacto"], correct: 1 },
        { q: "¿Qué sentido para oler?", options: ["Gusto", "Olfato 👃", "Vista"], correct: 1 },
        { q: "¿Qué sentido para tocar?", options: ["Oído", "Vista", "Tacto ✋"], correct: 2 },
        { q: "¿Qué sentido para sabores?", options: ["Olfato", "Gusto 👅", "Tacto"], correct: 1 },
        { q: "¿Cuántos sentidos tenemos?", options: ["3", "5", "7"], correct: 1 },
        { q: "¿Qué color es el fuego?", options: ["Azul", "Rojo 🔥", "Verde"], correct: 1 },
        { q: "¿Qué hacemos en círculo?", options: ["Correr solos", "Mirarnos 👥", "Dormir"], correct: 1 },
        
        // 🆕 NUEVAS PREGUNTAS AÑADIDAS:
        { q: "¿Qué sentido detecta el calor?", options: ["Vista", "Tacto 🔥", "Olfato"], correct: 1 },
        { q: "¿Qué sentido usas para leer?", options: ["Oído", "Vista 📖", "Gusto"], correct: 1 },
        { q: "¿Qué sentido para bailar?", options: ["Vista", "Oído 🎶", "Olfato"], correct: 1 },
        { q: "¿Qué sentido para cocinar?", options: ["Vista", "Olfato 👃", "Tacto"], correct: 1 },
        { q: "¿Qué sentido para pintar?", options: ["Oído", "Vista 🎨", "Gusto"], correct: 1 },
        { q: "¿Qué sentido para abrazar?", options: ["Vista", "Tacto 🤗", "Olfato"], correct: 1 },
        { q: "¿Qué sentido para cantar?", options: ["Vista", "Oído 🎤", "Tacto"], correct: 1 },
        { q: "¿Qué sentido para comer picante?", options: ["Olfato", "Gusto 🌶️", "Vista"], correct: 1 },
        { q: "¿Qué sentido para correr?", options: ["Vista 🏃", "Gusto", "Olfato"], correct: 0 },
        { q: "¿Qué sentido para oler lluvia?", options: ["Vista", "Oído", "Olfato ☔"], correct: 2 },
        { q: "¿Qué sentido para escribir?", options: ["Tacto ✍️", "Oído", "Gusto"], correct: 0 },
        { q: "¿Qué sentido para ver colores?", options: ["Oído", "Vista 🌈", "Olfato"], correct: 1 },
        { q: "¿Qué sentido para sentir viento?", options: ["Vista", "Tacto 🌬️", "Gusto"], correct: 1 }
    ];

    const riddles = [
        {
            q: "Acertijo: ¿Qué pesa más, un kilo de plumas o un kilo de hierro?",
            options: ["Plumas", "Hierro", "Pesan igual ⚖️"], correct: 2
        },
        {
            q: "Acertijo: Si me nombras desaparezco, ¿qué soy?",
            options: ["El silencio 🤫", "El viento 🌬️", "El tiempo ⏳"], correct: 0
        },
        {
            q: "Acertijo: ¿Qué tiene agujeros pero puede retener agua?",
            options: ["Una esponja 🧽", "Un cubo 🪣", "Una toalla 🛁"], correct: 0
        },
        {
            q: "Acertijo: En un lago hay un lirio que se duplica cada día, y tarda 48 días en cubrirlo entero, ¿Cuánto tarda en cubrir la mitad?",
            options: ["24 días", "47 días 📅", "1 día"], correct: 1
        }
    ];

    function generateGameCode(length = 5) {
        const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZ123456789';
        let res = '';
        for (let i=0; i < length; i++) {
            res += chars.charAt(Math.floor(Math.random()*chars.length));
        }
        return res;
    }

    function tryStartGame() {
        const inputCode = document.getElementById('gameCodeInput').value.trim().toUpperCase();
        if(inputCode !== gameCode){
            alert('Código incorrecto. Por favor, ingresa el código correcto.');
            return;
        }
        startGame();
    }

    function startGame(){
        let names = [];
        for(let i=1; i <=5; i++){
            const val = document.getElementById('player'+i+'Name').value.trim();
            if(val) names.push(val);
        }
        if(names.length < 2){
            alert('Ingresa al menos dos jugadores para empezar.');
            return;
        }
        if(names.length > 5){
            alert('Máximo 5 jugadores permitidos.');
            return;
        }
        players = names.map((name, idx) => ({
            name,
            pos: 1,
            color: playerColors[idx],
            emoji: chessPawnCodes[idx]
        }));
        document.getElementById('playerSetup').style.display = 'none';
        document.getElementById('board').style.display = 'grid';
        document.getElementById('controls').style.display = 'flex';

        createBoard();
        updatePlayersInfo();
        updateCurrentPlayer();
    }

    function createBoard(){
        const board = document.getElementById('board');
        board.innerHTML = '';
        for(let i=1; i <= totalTiles; i++){
            const tile = document.createElement('div');
            tile.className = 'tile';
            tile.id = 'tile-'+i;
            let icon = '';
            if(specialTiles[i]){
                const type = specialTiles[i].type;
                if(type==='rojo') icon='🔥';
                else if(type==='azul') icon='💧';
                else if(type==='amarillo') icon='🌪️';
                else if(type==='verde') icon='🌍';
                else if(type==='pregunta') icon='❓';
                else if(type==='retroceso') icon='↩️';
                else if(type==='penalizacion') icon='⛓️';
                else if(type==='meta') icon='🏆';
                else if(type==='acertijo') icon='🧩';
            }
            tile.innerHTML = `<span class="icon">${icon}</span>${i}`;
            board.appendChild(tile);
        }
        updatePlayerVisuals();
    }
    
    function updatePlayerVisuals(){
        document.querySelectorAll('.tile').forEach(tile=>{
            tile.querySelectorAll('.player-token').forEach(t=>t.remove());
        });
        players.forEach(p=>{
            const tile = document.getElementById('tile-'+Math.min(p.pos,totalTiles));
            if(tile){
                const token=document.createElement('div');
                token.className='player-token';
                token.style.color = p.color;
                token.textContent=p.emoji;
                tile.appendChild(token);
            }
        });
        updateStatus();
    }

    function updateStatus(){
        const current = players[currentPlayerIndex];
        document.getElementById('status').innerText = `${current.emoji} ${current.name}: Casilla ${current.pos}`;
    }

    function updateCurrentPlayer(){
        const current = players[currentPlayerIndex];
        document.getElementById('currentPlayer').innerHTML = 
            `👤 Turno de: <strong style="color:${current.color}">${current.name}</strong> ${current.emoji}`;
    }

    function updatePlayersInfo(){
        const info=document.getElementById('playersInfo');
        info.innerHTML = players.map(p=>
            `<div class="player-info" style="background:${p.color}">${p.emoji} ${p.name}: ${p.pos}</div>`).join('');
    }

    function rollDice(){
        if(isMoving) return;
        isMoving=true;
        const diceBtn=document.getElementById('diceBtn');
        diceBtn.disabled=true;
        let rolls=0;
        const interval=setInterval(()=>{
            const roll=Math.floor(Math.random()*6)+1;
            diceBtn.innerText=roll;
            rolls++;
            if(rolls>12) {
                clearInterval(interval);
                diceBtn.innerText='🎲 Tirar el Dado';
                diceBtn.disabled=false;
                finalizeMove(roll,currentPlayerIndex);
                isMoving=false;
            }
        },80);
    }

    function finalizeMove(steps,playerIndex){
        const player=players[playerIndex];
        let next=player.pos+steps;
        if(next > totalTiles) next=totalTiles-(next-totalTiles);
        player.pos=next;
        updatePlayerVisuals();
        updatePlayersInfo();
        
        const tileData=specialTiles[player.pos];
        if(tileData){
            checkTile(playerIndex);
        }
        else{
            endTurn();
        }
    }

    function checkTile(playerIndex){
        const player=players[playerIndex];
        const tileData=specialTiles[player.pos];
        if(['rojo','azul','amarillo','verde'].includes(tileData.type)){
            showMessage(`🎨 ${tileData.type.toUpperCase()}`, 
                tileData.action + '<br><strong>¡Pulsa para continuar! Todos hacen la acción.</strong>',
                () => endTurn()
            );
        }
        else if(tileData.type==='pregunta') {
            launchQuestion(playerIndex);
        }
        else if(tileData.type==='acertijo') {
            launchRiddle(playerIndex);
        }
        else if(tileData.type==='penalizacion') {
            showMessage('⛓️ PENALIZACIÓN', tileData.text, () => {
                if(tileData.turns){
                    // Simular pérdida turnos (se avanza manualmente pero aquí no bloquea turno)
                }
                player.pos=tileData.jumpTo || player.pos;
                updatePlayerVisuals();
                updatePlayersInfo();
                endTurn();
            });
        }
        else if(tileData.type==='retroceso'){
            showMessage('↩️ RETROCESO', tileData.text, () => {
                player.pos=tileData.jumpTo;
                updatePlayerVisuals();
                updatePlayersInfo();
                endTurn();
            });
        }
        else if(tileData.type==='meta'){
            showMessage('🏆 ¡VICTORIA!', tileData.text, endTurn);
        }
    }

    function launchQuestion(playerIndex){
        const modal=document.getElementById('questionModal');
        const qText=document.getElementById('questionText');
        const optsContainer=document.getElementById('optionsContainer');
        const q=questions[Math.floor(Math.random()*questions.length)];
        qText.innerText=q.q;
        optsContainer.innerHTML='';
        q.options.forEach((opt,i)=>{
            const btn=document.createElement('button');
            btn.className='option-btn';
            btn.innerText=opt;
            btn.onclick=()=>checkAnswer(i===q.correct,playerIndex);
            optsContainer.appendChild(btn);
        });
        modal.style.display='flex';
    }

    function launchRiddle(playerIndex){
        const modal=document.getElementById('questionModal');
        const qText=document.getElementById('questionText');
        const optsContainer=document.getElementById('optionsContainer');
        const r=riddles[Math.floor(Math.random()*riddles.length)];
        qText.innerText=r.q;
        optsContainer.innerHTML='';
        r.options.forEach((opt,i)=>{
            const btn=document.createElement('button');
            btn.className='option-btn';
            btn.innerText=opt;
            btn.onclick=()=>checkAnswer(i===r.correct,playerIndex);
            optsContainer.appendChild(btn);
        });
        modal.style.display='flex';
    }

    function checkAnswer(isCorrect,playerIndex){
        document.getElementById('questionModal').style.display='none';
        const player=players[playerIndex];
        if(isCorrect){
            if(player.pos<totalTiles) player.pos++;
            showMessage('✅ ¡CORRECTO!', '¡Avanzas 1 casilla extra!', endTurn);
        }
        else{
            showMessage('❌ Incorrecta', 'Te quedas aquí.', endTurn);
        }
        updatePlayerVisuals();
        updatePlayersInfo();
    }

    function showMessage(title,text,callback){
        const modal=document.getElementById('messageModal');
        document.getElementById('msgTitle').innerText=title;
        document.getElementById('msgText').innerHTML=text;
        modal._callback=callback;
        modal.style.display='flex';
    }
    function closeMessage(){
        const modal=document.getElementById('messageModal');
        modal.style.display='none';
        if(modal._callback){
            modal._callback();
            modal._callback=null;
        }
    }
    function endTurn(){
        currentPlayerIndex=(currentPlayerIndex+1)%players.length;
        updateCurrentPlayer();
        updatePlayerVisuals();
    }

    function generateAndShowCode(){
        gameCode=generateGameCode();
        document.getElementById('generatedCode').innerText=`Código de juego: ${gameCode} (Escríbelo para unirte)`;
    }

    window.onload=()=>{
        generateAndShowCode();
    }

    document.addEventListener('keydown', e=>{
        if(e.key==='Enter' && !document.querySelector('.modal-overlay[style*="flex"]')) {
            rollDice();
        }
    });
</script>
</body>
</html>
