<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Snapchat - Disappearing Messages</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      height: 100vh;
      display: flex;
      flex-direction: column;
    }

    /* Login Screen */
    .login-screen {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      padding: 20px;
    }

    .login-box {
      background: white;
      padding: 40px;
      border-radius: 20px;
      box-shadow: 0 20px 60px rgba(0,0,0,0.3);
      text-align: center;
      max-width: 400px;
      width: 100%;
    }

    .login-box .emoji {
      font-size: 80px;
      margin-bottom: 20px;
    }

    .login-box h1 {
      font-size: 32px;
      color: #333;
      margin-bottom: 10px;
    }

    .login-box p {
      color: #666;
      margin-bottom: 30px;
    }

    .login-box input {
      width: 100%;
      padding: 15px;
      border: 2px solid #ddd;
      border-radius: 25px;
      font-size: 16px;
      margin-bottom: 20px;
      outline: none;
    }

    .login-box input:focus {
      border-color: #667eea;
    }

    .login-box button {
      width: 100%;
      padding: 15px;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      border: none;
      border-radius: 25px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      transition: opacity 0.3s;
    }

    .login-box button:hover {
      opacity: 0.9;
    }

    /* Main App */
    .app-screen {
      display: none;
      flex-direction: column;
      height: 100vh;
    }

    .header {
      background: white;
      padding: 15px 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    .header h1 {
      font-size: 24px;
      color: #667eea;
    }

    .header-buttons button {
      background: #f3f4f6;
      border: none;
      padding: 10px;
      margin-left: 10px;
      border-radius: 50%;
      cursor: pointer;
      font-size: 20px;
      transition: background 0.3s;
    }

    .header-buttons button:hover {
      background: #e5e7eb;
    }

    .chat-container {
      flex: 1;
      display: flex;
      background: white;
      overflow: hidden;
    }

    /* Friends List */
    .friends-list {
      width: 300px;
      border-right: 1px solid #e5e7eb;
      overflow-y: auto;
    }

    .friends-header {
      padding: 20px;
      border-bottom: 1px solid #e5e7eb;
      font-weight: bold;
      color: #333;
    }

    .friend-item {
      padding: 20px;
      border-bottom: 1px solid #e5e7eb;
      cursor: pointer;
      transition: background 0.3s;
      display: flex;
      align-items: center;
      gap: 15px;
    }

    .friend-item:hover {
      background: #f9fafb;
    }

    .friend-item.active {
      background: #ede9fe;
    }

    .friend-avatar {
      font-size: 32px;
    }

    .friend-info h3 {
      font-size: 16px;
      margin-bottom: 5px;
    }

    .friend-info p {
      font-size: 14px;
      color: #666;
    }

    /* Chat Area */
    .chat-area {
      flex: 1;
      display: flex;
      flex-direction: column;
    }

    .chat-header {
      padding: 20px;
      border-bottom: 1px solid #e5e7eb;
      display: flex;
      align-items: center;
      gap: 15px;
    }

    .messages-container {
      flex: 1;
      padding: 20px;
      overflow-y: auto;
      background: #f9fafb;
    }

    .message {
      margin-bottom: 15px;
      display: flex;
    }

    .message.sent {
      justify-content: flex-end;
    }

    .message-bubble {
      max-width: 60%;
      padding: 12px 18px;
      border-radius: 20px;
      position: relative;
    }

    .message.sent .message-bubble {
      background: #667eea;
      color: white;
    }

    .message.received .message-bubble {
      background: white;
      color: #333;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }

    .message-photo {
      max-width: 100%;
      border-radius: 10px;
      margin-bottom: 8px;
    }

    .message-time {
      font-size: 11px;
      margin-top: 5px;
      opacity: 0.8;
    }

    /* Input Area */
    .input-area {
      padding: 20px;
      border-top: 1px solid #e5e7eb;
      background: white;
    }

    .photo-preview {
      margin-bottom: 15px;
      position: relative;
      display: inline-block;
    }

    .photo-preview img {
      height: 100px;
      border-radius: 10px;
    }

    .photo-preview button {
      position: absolute;
      top: -10px;
      right: -10px;
      background: #ef4444;
      color: white;
      border: none;
      border-radius: 50%;
      width: 25px;
      height: 25px;
      cursor: pointer;
      font-size: 14px;
    }

    .input-controls {
      display: flex;
      gap: 10px;
    }

    .input-controls button {
      background: #ede9fe;
      color: #667eea;
      border: none;
      padding: 12px;
      border-radius: 50%;
      cursor: pointer;
      font-size: 18px;
      transition: background 0.3s;
    }

    .input-controls button:hover {
      background: #ddd6fe;
    }

    .input-controls input {
      flex: 1;
      padding: 12px 20px;
      border: 2px solid #e5e7eb;
      border-radius: 25px;
      font-size: 16px;
      outline: none;
    }

    .input-controls input:focus {
      border-color: #667eea;
    }

    .input-controls .send-btn {
      background: #667eea;
      color: white;
    }

    .input-controls .send-btn:hover {
      background: #5568d3;
    }

    /* Camera Screen */
    .camera-screen {
      display: none;
      background: black;
      height: 100vh;
      flex-direction: column;
    }

    .camera-view {
      flex: 1;
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    #cameraVideo, #capturedImage {
      max-width: 100%;
      max-height: 100%;
    }

    .camera-controls {
      padding: 30px;
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 30px;
    }

    .capture-btn {
      width: 70px;
      height: 70px;
      background: white;
      border: 4px solid #ccc;
      border-radius: 50%;
      cursor: pointer;
    }

    .camera-action-btn {
      padding: 12px 24px;
      border: none;
      border-radius: 25px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      transition: opacity 0.3s;
    }

    .camera-action-btn:hover {
      opacity: 0.8;
    }

    .retake-btn {
      background: #4b5563;
      color: white;
    }

    .use-photo-btn {
      background: #667eea;
      color: white;
    }

    .close-camera {
      position: absolute;
      top: 20px;
      left: 20px;
      background: rgba(0,0,0,0.5);
      color: white;
      border: none;
      padding: 10px;
      border-radius: 50%;
      cursor: pointer;
      font-size: 24px;
      width: 45px;
      height: 45px;
    }

    .start-camera-btn {
      padding: 15px 30px;
      background: white;
      color: #667eea;
      border: none;
      border-radius: 25px;
      font-size: 18px;
      font-weight: bold;
      cursor: pointer;
    }

    .empty-state {
      flex: 1;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      color: #666;
    }

    .empty-state .icon {
      font-size: 64px;
      margin-bottom: 20px;
      opacity: 0.5;
    }

    .hidden {
      display: none !important;
    }
  </style>
</head>
<body>
  <!-- Login Screen -->
  <div id="loginScreen" class="login-screen">
    <div class="login-box">
      <div class="emoji">👻</div>
      <h1>Snapchat</h1>
      <p>Messages that disappear</p>
      <input type="email" id="emailInput" placeholder="Enter your email">
      <button onclick="login()">Sign In</button>
    </div>
  </div>

  <!-- Main App Screen -->
  <div id="appScreen" class="app-screen">
    <div class="header">
      <h1>👻 Snapchat</h1>
      <div class="header-buttons">
        <button onclick="openCamera()">📷</button>
        <button>👤</button>
      </div>
    </div>

    <div class="chat-container">
      <!-- Friends List -->
      <div class="friends-list">
        <div class="friends-header">👥 Friends</div>
        <div class="friend-item" onclick="selectFriend('friend1', 'Alex Chen', '👤')">
          <div class="friend-avatar">👤</div>
          <div class="friend-info">
            <h3>Alex Chen</h3>
            <p>Tap to chat</p>
          </div>
        </div>
        <div class="friend-item" onclick="selectFriend('friend2', 'Sam Rivera', '👤')">
          <div class="friend-avatar">👤</div>
          <div class="friend-info">
            <h3>Sam Rivera</h3>
            <p>Tap to chat</p>
          </div>
        </div>
      </div>

      <!-- Chat Area -->
      <div class="chat-area" id="chatArea">
        <div class="empty-state">
          <div class="icon">👥</div>
          <p>Select a friend to start chatting</p>
        </div>
      </div>
    </div>
  </div>

  <!-- Camera Screen -->
  <div id="cameraScreen" class="camera-screen">
    <div class="camera-view">
      <button class="close-camera" onclick="closeCamera()">✕</button>
      <video id="cameraVideo" autoplay playsinline class="hidden"></video>
      <img id="capturedImage" class="hidden">
      <button id="startCameraBtn" class="start-camera-btn" onclick="startCamera()">Start Camera</button>
    </div>
    <div class="camera-controls">
      <button id="captureBtn" class="capture-btn hidden" onclick="capturePhoto()"></button>
      <button id="retakeBtn" class="camera-action-btn retake-btn hidden" onclick="retakePhoto()">Retake</button>
      <button id="usePhotoBtn" class="camera-action-btn use-photo-btn hidden" onclick="usePhoto()">Use Photo</button>
    </div>
  </div>

  <canvas id="canvas" style="display: none;"></canvas>

<script>
    var currentUser = null;
    var selectedFriend = null;
    var messages = [];
    var cameraStream = null;
    var capturedPhotoData = null;

    function login() {
      var email = document.getElementById('emailInput').value;
      if (email) {
        currentUser = { id: 'user1', email: email, name: email.split('@')[0] };
        document.getElementById('loginScreen').style.display = 'none';
        document.getElementById('appScreen').style.display = 'flex';
      }
    }

    function selectFriend(id, name, avatar) {
      selectedFriend = { id: id, name: name, avatar: avatar };
      
      var items = document.querySelectorAll('.friend-item');
      for (var i = 0; i < items.length; i++) {
        items[i].classList.remove('active');
      }
      if (window.event && window.event.target) {
        var target = window.event.target.closest('.friend-item');
        if (target) target.classList.add('active');
      }
      
      var chatHTML = '<div class="chat-header">' +
          '<div class="friend-avatar">' + avatar + '</div>' +
          '<h2>' + name + '</h2>' +
        '</div>' +
        '<div class="messages-container" id="messagesContainer"></div>' +
        '<div class="input-area">' +
          '<div id="photoPreview"></div>' +
          '<div class="input-controls">' +
            '<button onclick="openCamera()">📷</button>' +
            '<input type="text" id="messageInput" placeholder="Type a message..." onkeypress="handleKeyPress(event)">' +
            '<button class="send-btn" onclick="sendMessage()">➤</button>' +
          '</div>' +
        '</div>';
      
      document.getElementById('chatArea').innerHTML = chatHTML;
      renderMessages();
    }

    function sendMessage() {
      if (!selectedFriend) return;
      
      var messageInput = document.getElementById('messageInput');
      var text = messageInput.value.trim();
      
      if (!text && !capturedPhotoData) return;
      
      var message = {
        id: Date.now(),
        sender: currentUser.id,
        recipient: selectedFriend.id,
        text: text,
        photo: capturedPhotoData,
        timestamp: Date.now(),
        expiresAt: Date.now() + 10000
      };
      
      messages.push(message);
      messageInput.value = '';
      capturedPhotoData = null;
      document.getElementById('photoPreview').innerHTML = '';
      
      renderMessages();
    }

    function renderMessages() {
      if (!selectedFriend) return;
      
      var container = document.getElementById('messagesContainer');
      if (!container) return;
      
      var now = Date.now();
      var chatMessages = [];
      for (var i = 0; i < messages.length; i++) {
        var m = messages[i];
        if (((m.sender === currentUser.id && m.recipient === selectedFriend.id) ||
             (m.sender === selectedFriend.id && m.recipient === currentUser.id)) &&
            m.expiresAt > now) {
          chatMessages.push(m);
        }
      }
      
      var html = '';
      for (var j = 0; j < chatMessages.length; j++) {
        var msg = chatMessages[j];
        var isSent = msg.sender === currentUser.id;
        var timeLeft = Math.max(0, Math.floor((msg.expiresAt - now) / 1000));
        
        html += '<div class="message ' + (isSent ? 'sent' : 'received') + '">' +
          '<div class="message-bubble">' +
            (msg.photo ? '<img src="' + msg.photo + '" class="message-photo">' : '') +
            (msg.text ? '<div>' + msg.text + '</div>' : '') +
            '<div class="message-time">⏱️ Disappears in ' + timeLeft + 's</div>' +
          '</div>' +
        '</div>';
      }
      
      container.innerHTML = html;
      container.scrollTop = container.scrollHeight;
    }

    function handleKeyPress(event) {
      if (event.key === 'Enter') {
        sendMessage();
      }
    }

    function openCamera() {
      document.getElementById('appScreen').style.display = 'none';
      document.getElementById('cameraScreen').style.display = 'flex';
    }

    function closeCamera() {
      stopCamera();
      document.getElementById('cameraScreen').style.display = 'none';
      document.getElementById('appScreen').style.display = 'flex';
    }

    function startCamera() {
      navigator.mediaDevices.getUserMedia({ video: true })
        .then(function(stream) {
          cameraStream = stream;
          var video = document.getElementById('cameraVideo');
          video.srcObject = stream;
          
          document.getElementById('startCameraBtn').classList.add('hidden');
          document.getElementById('cameraVideo').classList.remove('hidden');
          document.getElementById('captureBtn').classList.remove('hidden');
        })
        .catch(function(err) {
          alert('Camera access denied or not available');
        });
    }

    function stopCamera() {
      if (cameraStream) {
        var tracks = cameraStream.getTracks();
        for (var i = 0; i < tracks.length; i++) {
          tracks[i].stop();
        }
        cameraStream = null;
      }
      document.getElementById('cameraVideo').classList.add('hidden');
      document.getElementById('capturedImage').classList.add('hidden');
      document.getElementById('captureBtn').classList.add('hidden');
      document.getElementById('retakeBtn').classList.add('hidden');
      document.getElementById('usePhotoBtn').classList.add('hidden');
      document.getElementById('startCameraBtn').classList.remove('hidden');
    }

    function capturePhoto() {
      var video = document.getElementById('cameraVideo');
      var canvas = document.getElementById('canvas');
      var context = canvas.getContext('2d');
      
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      context.drawImage(video, 0, 0);
      
      capturedPhotoData = canvas.toDataURL('image/jpeg');
      
      var img = document.getElementById('capturedImage');
      img.src = capturedPhotoData;
      img.classList.remove('hidden');
      
      video.classList.add('hidden');
      document.getElementById('captureBtn').classList.add('hidden');
      document.getElementById('retakeBtn').classList.remove('hidden');
      document.getElementById('usePhotoBtn').classList.remove('hidden');
      
      stopCamera();
    }

    function retakePhoto() {
      capturedPhotoData = null;
      document.getElementById('capturedImage').classList.add('hidden');
      document.getElementById('retakeBtn').classList.add('hidden');
      document.getElementById('usePhotoBtn').classList.add('hidden');
      startCamera();
    }

    function usePhoto() {
      if (capturedPhotoData) {
        var photoHTML = '<div class="photo-preview">' +
            '<img src="' + capturedPhotoData + '">' +
            '<button onclick="removePhoto()">✕</button>' +
          '</div>';
        document.getElementById('photoPreview').innerHTML = photoHTML;
      }
      closeCamera();
    }

    function removePhoto() {
      capturedPhotoData = null;
      document.getElementById('photoPreview').innerHTML = '';
    }

    setInterval(function() {
      var now = Date.now();
      var filteredMessages = [];
      for (var i = 0; i < messages.length; i++) {
        if (messages[i].expiresAt > now) {
          filteredMessages.push(messages[i]);
        }
      }
      messages = filteredMessages;
      renderMessages();
    }, 1000);
  </script>
</body>
</html>
