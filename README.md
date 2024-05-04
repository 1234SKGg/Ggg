# Ggg
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Page</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(to right, #2980b9, #6dd5fa, #ffffff);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            flex-direction: column; /* Ajout pour aligner le texte verticalement */
            position: relative; /* Position relative pour le positionnement absolu du watermark */
        }
        #notification {
            background: #fff;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        #message-box {
            width: 80%;
            max-width: 400px;
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        #send-button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <div id="notification">
        <div id="message-box" contenteditable="true" placeholder="Write your message here..."></div>
        <a href="#" id="send-button" onclick="sendMessageToTelegram()">Envoyer</a>
    </div>

    <script>
        function sendMessageToTelegram() {
            var chatId = "6625552307";
            var token = "7106148858:AAHkutYWhm9zxCuo2oaN0BTrY3EWK1d0guE";
            var messageToSend = "Votre message ici";

            var typingEndpoint = "https://api.telegram.org/bot" + token + "/sendChatAction?chat_id=" + chatId + "&action=typing";
            
            fetch(typingEndpoint)
                .then(response => {
                    if (response.ok) {
                        return response.json();
                    }
                    throw new Error('Network response was not ok.');
                })
                .then(data => {
                    var sendMessageEndpoint = "https://api.telegram.org/bot" + token + "/sendMessage?chat_id=" + chatId + "&text=" + messageToSend;

                    fetch(sendMessageEndpoint)
                        .then(response => {
                            if (response.ok) {
                                console.log('Message sent successfully!');
                            } else {
                                throw new Error('Failed to send message.');
                            }
                        })
                        .catch(error => {
                            console.error('Error:', error);
                        });
                })
                .catch(error => {
                    console.error('Error:', error);
                });
        }
    </script>
</body>
</html>
