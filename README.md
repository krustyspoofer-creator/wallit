# wallit
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tanky Wallit Chat</title>
  <style>
    body { background: #0f0f0f; color: #00ff99; font-family: monospace; padding: 2em; }
    .container { max-width: 800px; margin: auto; }
    h1 { color: #00ffff; }
    #chatBox { background: #111; padding: 1em; border: 1px solid #00ff99; height: 400px; overflow-y: scroll; }
    .msg { margin: 0.5em 0; }
    .user { color: #00ff99; }
    .ai { color: #ff00ff; }
    input, button { width: 100%; padding: 0.5em; margin-top: 1em; font-size: 1em; }
  </style>
</head>
<body>
  <div class="container">
    <h1>🧠 Tanky Wallit Chat</h1>
    <div id="chatBox"></div>
    <input type="text" id="userInput" placeholder="Type your message..." />
    <button onclick="sendMessage()">Send</button>
  </div>

  <script>
    const chatBox = document.getElementById('chatBox');

    function appendMessage(sender, text) {
      const msg = document.createElement('div');
      msg.className = 'msg ' + sender;
      msg.innerText = (sender === 'user' ? '🧍 Joseph: ' : '🤖 Tanky: ') + text;
      chatBox.appendChild(msg);
      chatBox.scrollTop = chatBox.scrollHeight;
    }

    async function sendMessage() {
      const input = document.getElementById('userInput');
      const text = input.value.trim();
      if (!text) return;
      appendMessage('user', text);
      input.value = '';

      const res = await fetch('/chat', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ message: text })
      });
      const reply = await res.text();
      appendMessage('ai', reply);
    }
  </script>
</body>
</html>
