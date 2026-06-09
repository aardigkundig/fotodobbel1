<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Afbeeldingen Dobbelsteen</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 20px;
            background-color: #f5f5f5;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #333;
        }
        .dice-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 10px;
            margin: 20px 0;
        }
        .dice-image {
            width: 100px;
            height: 100px;
            border-radius: 8px;
            object-fit: cover;
            transition: transform 0.3s;
        }
        .dice-image.shake {
            animation: shake 0.5s;
        }
        @keyframes shake {
            0% { transform: rotate(0deg); }
            25% { transform: rotate(10deg); }
            50% { transform: rotate(-10deg); }
            75% { transform: rotate(10deg); }
            100% { transform: rotate(0deg); }
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px;
        }
        button:hover {
            background-color: #45a049;
        }
        input {
            margin: 10px;
            padding: 8px;
            width: 300px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Afbeeldingen Dobbelsteen</h1>
        <p>Klik op "Gooi" om willekeurige afbeeldingen te tonen.</p>

        <div class="dice-container" id="diceContainer">
            <!-- Afbeeldingen worden hier dynamisch toegevoegd -->
        </div>

        <button onclick="rollDice()">Gooi</button>

        <h3>Afbeeldingen beheer</h3>
        <input type="text" id="imageUrlInput" placeholder="Voer afbeeldings-URL in">
        <button onclick="addImage()">Voeg afbeelding toe</button>
        <button onclick="removeLastImage()">Verwijder laatste afbeelding</button>
    </div>

    <script>
        // Lijst met afbeeldings-URLs (vervang deze door je eigen URLs)
        let images = [
            "https://via.placeholder.com/100?text=Afbeelding+1",
            "https://via.placeholder.com/100?text=Afbeelding+2",
            "https://via.placeholder.com/100?text=Afbeelding+3",
            "https://via.placeholder.com/100?text=Afbeelding+4",
            "https://via.placeholder.com/100?text=Afbeelding+5",
            "https://via.placeholder.com/100?text=Afbeelding+6"
        ];

        // Aantal afbeeldingen dat getoond wordt per worp
        const diceCount = 3;

        // Functie om de dobbelsteen te "gooien"
        function rollDice() {
            const diceContainer = document.getElementById("diceContainer");
            diceContainer.innerHTML = "";

            // Voeg de shake-animatie toe
            diceContainer.classList.add("shake");
            setTimeout(() => {
                diceContainer.classList.remove("shake");
            }, 500);

            // Kies willekeurige afbeeldingen
            for (let i = 0; i < diceCount; i++) {
                const randomIndex = Math.floor(Math.random() * images.length);
                const img = document.createElement("img");
                img.src = images[randomIndex];
                img.className = "dice-image";
                diceContainer.appendChild(img);
            }
        }

        // Functie om een afbeelding toe te voegen
        function addImage() {
            const urlInput = document.getElementById("imageUrlInput");
            const newUrl = urlInput.value.trim();
            if (newUrl) {
                images.push(newUrl);
                urlInput.value = "";
                alert("Afbeelding toegevoegd!");
            } else {
                alert("Voer een geldige URL in.");
            }
        }

        // Functie om de laatste afbeelding te verwijderen
        function removeLastImage() {
            if (images.length > 0) {
                images.pop();
                alert("Laatste afbeelding verwijderd!");
            } else {
                alert("Er zijn geen afbeeldingen om te verwijderen.");
            }
        }

        // Toon de eerste set afbeeldingen bij het laden
        window.onload = rollDice;
    </script>
</body>
</html>
