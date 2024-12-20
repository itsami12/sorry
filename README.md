
<html>
<head>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
        }
        
        .question {
            font-size: 24px;
            margin-bottom: 20px;
        }
        
        .buttons {
            display: flex;
            gap: 20px;
        }
        
        button {
            padding: 10px 20px;
            font-size: 18px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            transition: transform 0.3s;
        }
        
        #yesBtn, #modalYesBtn {
            background-color: #4CAF50;
            color: white;
        }
        
        #yesBtn:hover, #modalYesBtn:hover {
            background-color: #45a049;
            transform: scale(1.1);
        }
        
        #neverBtn {
            background-color: #f44336;
            color: white;
        }
        
        #neverBtn:hover {
            transform: translate(
                calc(100px * var(--random-x)),
                calc(100px * var(--random-y))
            );
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 30px 40px;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(0,0,0,0.3);
            z-index: 1000;
            text-align: center;
            animation: bounce 0.5s;
        }
        
        @keyframes bounce {
            0% { transform: translate(-50%, -50%) scale(0.3); }
            50% { transform: translate(-50%, -50%) scale(1.1); }
            70% { transform: translate(-50%, -50%) scale(0.9); }
            100% { transform: translate(-50%, -50%) scale(1); }
        }
        
        .modal h2 {
            font-size: 28px;
            margin: 10px 0;
            color: #333;
        }
        
        .modal .emoji {
            font-size: 50px;
            margin: 15px 0;
            animation: shake 0.5s infinite;
        }
        
        .modal button {
            margin-top: 20px;
        }
        
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        
        .overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 999;
        }
        
        .result-container {
            display: none;
            text-align: center;
            padding: 20px;
        }
        
        .result-container h2 {
            color: #333;
            margin-bottom: 20px;
        }
        
        .result-container img {
            max-width: 300px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0,0,0,0.2);
        }
    </style>
</head>
<body>
    <div class="question">Will you forgive me?</div>
    
    <div class="buttons">
        <button id="yesBtn">Yes</button>
        <button id="neverBtn">Never</button>
    </div>
    
    <div class="result-container" id="yesResult">
        <h2>Thank you for forgiving me! ❤️</h2>
        <img src="https://media.tenor.com/images/3e1ff44c90e52ff1defe6b5dbaf225ca/tenor.gif%22%20alt=%22HABIBTI%22%20id=%22my-gif" alt="Thank You GIF" id="thankYouGif">
    </div>
    
    <div class="overlay" id="overlay"></div>
    <div class="modal" id="modal">
        <div class="emoji">🥺</div>
        <h2>Think again please</h2>
        <div class="emoji">😢</div>
        <button id="modalYesBtn" style="animation: pulse 1s infinite">Yes</button>
    </div>

    <script>
        const neverBtn = document.getElementById('neverBtn');
        const yesBtn = document.getElementById('yesBtn');
        const modalYesBtn = document.getElementById('modalYesBtn');
        const modal = document.getElementById('modal');
        const overlay = document.getElementById('overlay');
        const yesResult = document.getElementById('yesResult');
        let modalInterval;
        
        // Make the "Never" button run away
        neverBtn.addEventListener('mouseover', () => {
            neverBtn.style.setProperty('--random-x', Math.random() * 2 - 1);
            neverBtn.style.setProperty('--random-y', Math.random() * 2 - 1);
        });
        
        // Show modal when clicking "Never" and start loop
        neverBtn.addEventListener('click', () => {
            showModalLoop();
        });
        
        function showModalLoop() {
            modal.style.display = 'block';
            overlay.style.display = 'block';
            
            // Clear any existing interval
            clearInterval(modalInterval);
            
            // Set up new interval to show modal repeatedly
            modalInterval = setInterval(() => {
                modal.style.display = 'none';
                setTimeout(() => {
                    modal.style.display = 'block';
                }, 300);
            }, 2000);
        }
        
        function showSuccess() {
            clearInterval(modalInterval);
            modal.style.display = 'none';
            overlay.style.display = 'none';
            document.querySelector('.buttons').style.display = 'none';
            document.querySelector('.question').style.display = 'none';
            yesResult.style.display = 'block';
        }
        
        // Show success message and gif when clicking either Yes button
        yesBtn.addEventListener('click', showSuccess);
        modalYesBtn.addEventListener('click', showSuccess);
        
        // Prevent closing modal by clicking overlay
        overlay.addEventListener('click', (e) => {
            e.preventDefault();
            showModalLoop();
        });
    </script>
</body>
</html>
