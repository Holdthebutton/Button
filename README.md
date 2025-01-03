<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hold The Button</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f9;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            flex-direction: column;
            text-align: center;
        }
        h1 {
            color: #4CAF50;
            font-size: 36px;
        }
        p {
            font-size: 18px;
            color: #555;
        }
        .button-container {
            margin-bottom: 30px;
        }
        #tapButton {
            font-size: 24px;
            padding: 30px 60px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
        }
        #tapButton:hover {
            background-color: #45a049;
        }
        #tapButton:active {
            background-color: #388e3c;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            transform: translateY(4px);
        }
        .score-board {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 12px;
            width: 300px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
        }
        .score-board p {
            font-size: 20px;
            color: #333;
            margin: 10px 0;
        }
        .record {
            font-weight: bold;
            color: #2196F3;
        }
    </style>
</head>
<body>

    <h1>Hold The Button Game</h1>
    <p>Hold the button to see how long you can Hold!</p>

    <div class="button-container">
        <button id="tapButton">Hold Me!</button>
    </div>

    <div class="score-board">
        <p>Time held: <span id="currentScore">0</span> seconds</p>
        <p class="record">Personal Record: <span id="personalRecord">0</span> seconds</p>
    </div>

    <script>
        // Retrieve personal record from localStorage, or set it to 0 if not found
        let personalRecord = parseFloat(localStorage.getItem('personalRecord')) || 0;

        // Update the display of personal record immediately after loading
        document.getElementById('personalRecord').innerText = personalRecord.toFixed(2);

        let startTime = 0;
        let endTime = 0;
        let currentScore = 0;

        // Start measuring when the mouse button is pressed down
        document.getElementById("tapButton").addEventListener("mousedown", function() {
            startTime = new Date().getTime();
            document.getElementById("tapButton").innerText = "Release Me!";
        });

        // End measuring when the mouse button is released
        document.getElementById("tapButton").addEventListener("mouseup", function() {
            endTime = new Date().getTime();
            currentScore = (endTime - startTime) / 1000;  // Convert milliseconds to seconds
            document.getElementById("currentScore").innerText = currentScore.toFixed(2);

            // Check if the new score is higher than the current personal record
            if (currentScore > personalRecord) {
                personalRecord = currentScore;

                // Update the display of the personal record
                document.getElementById("personalRecord").innerText = personalRecord.toFixed(2);

                // Save the new personal record in localStorage
                localStorage.setItem('personalRecord', personalRecord);
            }

            // Reset the button text
            document.getElementById("tapButton").innerText = "Tap Me!";
        });
    </script>

</body>
</html>
