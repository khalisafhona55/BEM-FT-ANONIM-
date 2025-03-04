<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BEM FT Anonim Chat</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }
        textarea {
            width: 80%;
            height: 100px;
            margin-bottom: 10px;
        }
        button {
            padding: 10px;
            background-color: blue;
            color: white;
            border: none;
            cursor: pointer;
        }
        #messages {
            margin-top: 20px;
            text-align: left;
            width: 80%;
            margin-left: auto;
            margin-right: auto;
        }
        .message-box {
            padding: 10px;
            border: 1px solid #ddd;
            margin-bottom: 10px;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
    </style>
</head>
<body>
    <h2>Kirim Pesan Anonim ke BEM FT</h2>
    <textarea id="message" placeholder="Tulis pesanmu di sini ^^..."></textarea><br>
    <button onclick="sendMessage()">Kirim</button>

    <h3>Pesan yang Masuk:</h3>
    <div id="messages"></div>

    <script type="module">
        // Import Firebase
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, push, onChildAdded } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // Konfigurasi Firebase 
        const firebaseConfig = {
            // For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: "AIzaSyC_Dk7hcd_vUV77nAjjpgOBZPvFbrmlhk8",
  authDomain: "bem-ft-anonim.firebaseapp.com",
  projectId: "bem-ft-anonim",
  storageBucket: "bem-ft-anonim.firebasestorage.app",
  messagingSenderId: "73952916555",
  appId: "1:73952916555:web:878cb746c154b2bbc309ce",
  measurementId: "G-5PP1LY3WR4"
};
        };

        // Inisialisasi Firebase
        const app = initializeApp(firebaseConfig);
        const database = getDatabase(app);

        // Fungsi kirim pesan
        window.sendMessage = function() {
            const message = document.getElementById("message").value;
            if (message.trim() === "") return alert("Pesan tidak boleh kosong!");

            push(ref(database, "messages"), { text: message })
                .then(() => {
                    document.getElementById("message").value = "";
                })
                .catch(error => console.error("Error:", error));
        };

        // Fungsi tampilkan pesan secara real-time
        const messagesDiv = document.getElementById("messages");
        onChildAdded(ref(database, "messages"), (snapshot) => {
            const data = snapshot.val();
            const messageElement = document.createElement("div");
            messageElement.classList.add("message-box");
            messageElement.textContent = data.text;
            messagesDiv.prepend(messageElement);
        });
    </script>
</body>
</html>
