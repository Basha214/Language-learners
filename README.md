# Language-learners
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Learn English with AI</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            text-align: center;
        }

        header {
            background-color: #007bff;
            color: white;
            padding: 20px 0;
            margin-bottom: 20px;
        }

        nav {
            margin-bottom: 20px;
        }

        nav a {
            margin: 0 15px;
            color: #007bff;
            text-decoration: none;
            font-weight: bold;
        }

        nav a:hover {
            text-decoration: underline;
        }

        .content {
            margin: 20px;
        }

        .lesson {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }

        .quiz {
            background-color: #fff9c4;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }

        .quiz button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }

        .quiz button:hover {
            background-color: #0056b3;
        }

        #chatbot {
            margin-top: 20px;
            padding: 20px;
            background-color: #e9ecef;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }

        #messages {
            height: 200px;
            overflow-y: scroll;
            border: 1px solid #ccc;
            padding: 10px;
            background-color: white;
        }

        #user-input {
            margin-top: 10px;
        }

        #user-input input {
            width: 80%;
            padding: 10px;
            font-size: 16px;
        }

        #user-input button {
            padding: 10px;
            font-size: 16px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #language-selector {
            margin-top: 20px;
        }

        #translation {
            margin-top: 20px;
            padding: 10px;
            background-color: #d1ecf1;
            border-radius: 5px;
            display: none;
        }
    </style>
</head>
<body>

    <header>
        <h1>Learn English with AI</h1>
        <p>Interactive English learning with AI and translation support!</p>
    </header>

    <nav>
        <a href="#vocabulary">Vocabulary</a>
        <a href="#grammar">Grammar</a>
        <a href="#quiz">Quiz</a>
    </nav>

    <div class="content">

        <!-- Vocabulary Section -->
        <section id="vocabulary" class="lesson">
            <h2>Vocabulary Building</h2>
            <p>Learn new words every day!</p>
            <p><strong>Word:</strong> Serendipity</p>
            <p><strong>Meaning:</strong> Finding something good without looking for it.</p>
        </section>

        <!-- Grammar Section -->
        <section id="grammar" class="lesson">
            <h2>Grammar Lessons</h2>
            <p>Understand the basics of English grammar.</p>
            <p><strong>Topic:</strong> Present Simple Tense</p>
            <p><strong>Rule:</strong> Use the base form of the verb for habits, general truths, and routines. Add 's' or 'es' for he/she/it.</p>
            <p><strong>Example:</strong> She walks to school every day.</p>
        </section>

        <!-- Quiz Section -->
        <section id="quiz" class="quiz">
            <h2>Quiz Time</h2>
            <p>Test your knowledge with this quick quiz!</p>
            <p><strong>Question:</strong> What is the past tense of "go"?</p>
            <button onclick="checkAnswer()">Submit</button>
            <p id="result"></p>
        </section>

        <!-- Chatbot Section -->
        <section id="chatbot">
            <h2>AI Language Assistant</h2>
            <div id="messages"></div>
            <div id="user-input">
                <input type="text" id="message" placeholder="Ask something...">
                <button onclick="sendMessage()">Send</button>
            </div>
        </section>

        <!-- Language Translation Section -->
        <section id="language-selector">
            <h2>Translate Content</h2>
            <select id="language" onchange="translateContent()">
                <option value="en">English</option>
                <option value="hi">Hindi</option>
                <option value="ur">Urdu</option>
            </select>
            <div id="translation"></div>
        </section>

    </div>

    <script>
        // Basic Chatbot Functionality
        const messagesDiv = document.getElementById("messages");

        function sendMessage() {
            const userMessage = document.getElementById("message").value;
            if (userMessage.trim() === "") return;

            const userMessageDiv = document.createElement("div");
            userMessageDiv.textContent = "You: " + userMessage;
            messagesDiv.appendChild(userMessageDiv);

            // Mock AI response
            const botResponseDiv = document.createElement("div");
            botResponseDiv.textContent = "Bot: " + getBotResponse(userMessage);
            messagesDiv.appendChild(botResponseDiv);

            messagesDiv.scrollTop = messagesDiv.scrollHeight;
            document.getElementById("message").value = "";
        }

        function getBotResponse(message) {
            // Simple responses, can be replaced with an AI API call
            if (message.toLowerCase().includes("hello")) {
                return "Hello! How can I assist you with your English learning today?";
            } else if (message.toLowerCase().includes("grammar")) {
                return "Would you like to learn about tenses, articles, or something else?";
            } else {
                return "I'm here to help! Please ask a question about vocabulary, grammar, or anything else.";
            }
        }

        // Simple Quiz Functionality
        function checkAnswer() {
            let answer = prompt("Enter your answer:");
            if (answer.toLowerCase() === "went") {
                document.getElementById("result").innerText = "Correct! Well done!";
            } else {
                document.getElementById("result").innerText = "Incorrect. The correct answer is 'went'.";
            }
        }

        // Language Translation Functionality
        async function translateContent() {
            const language = document.getElementById("language").value;
            const translationDiv = document.getElementById("translation");

            const textToTranslate = `
                Learn English with AI: Interactive English learning with AI and translation support!
                Vocabulary Building: Learn new words every day!
                Word: Serendipity - Finding something good without looking for it.
                Grammar Lessons: Understand the basics of English grammar.
                Present Simple Tense: Use the base form of the verb for habits, general truths, and routines. Add 's' or 'es' for he/she/it.
            `;

            const translatedText = await translateText(textToTranslate, language);
            translationDiv.textContent = translatedText;
            translationDiv.style.display = "block";
        }

        async function translateText(text, targetLanguage) {
            // Example using a free translation API like Google Translate API
            const apiKey = 'YOUR_API_KEY'; // Replace with your API key
            const url = `https://translation.googleapis.com/language/translate/v2?key=${apiKey}`;

            const response = await fetch(url, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                    q: text,
                    target: targetLanguage
                })
            });

            const data = await response.json();
            return data.data.translations[0].translatedText;
        }
    </script>

</body>
</html>
