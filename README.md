<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Worldwide chat</title>
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

    .error-message {
      color: #ef4444;
      font-size: 14px;
      margin-bottom: 15px;
      display: none;
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

    .header-info {
      display: flex;
      align-items: center;
      gap: 15px;
    }

    .current-user {
      color: #666;
      font-size: 14px;
    }

    .header-buttons button {
      background: #f3f4f6;
      border: none;
      padding: 10px 15px;
      margin-left: 10px;
      border-radius: 20px;
      cursor: pointer;
      font-size: 14px;
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

    /* Users List */
    .friends-list {
      width: 300px;
      border-right: 1px solid #e5e7eb;
      overflow-y: auto;
      display: flex;
      flex-direction: column;
    }

    .friends-header {
      padding: 20px;
      border-bottom: 1px solid #e5e7eb;
      font-weight: bold;
      color: #333;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .add-user-btn {
      background: #667eea;
      color: white;
      border: none;
      padding: 8px 15px;
      border-radius: 15px;
      cursor: pointer;
      font-size: 14px;
    }

    .add-user-btn:hover {
      background: #5568d3;
    }

    .friend-item {
      padding: 20px;
      border-bottom: 1px solid #e5e7eb;
      cursor: pointer;
      transition: background 0.3s;
      display: flex;
      align-items: center;
      gap: 15px;
      position: relative;
    }

    .friend-item:hover {
      background: #f9fafb;
    }

    .friend-item.active {
      background: #ede9fe;
    }

    .friend-avatar {
      font-size: 32px;
      width: 40px;
      height: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .friend-info {
      flex: 1;
    }

    .friend-info h3 {
      font-size: 16px;
      margin-bottom: 5px;
    }

    .friend-info p {
      font-size: 14px;
      color: #666;
    }

    .edit-name-btn {
      background: #f3f4f6;
      border: none;
      padding: 5px 10px;
      border-radius: 10px;
      cursor: pointer;
      font-size: 12px;
    }

    .edit-name-btn:hover {
      background: #e5e7eb;
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

    .message-text {
      word-wrap: break-word;
    }

    .message-time {
      font-size: 11px;
      margin-top: 5px;
      opacity: 0.8;
    }

    .message-sender {
      font-weight: bold;
      font-size: 12px;
      margin-bottom: 5px;
    }

    /* Input Area */
    .input-area {
      padding: 20px;
      border-top: 1px solid #e5e7eb;
      background: white;
    }

    .input-controls {
      display: flex;
      gap: 10px;
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

    .input-controls button {
      background: #667eea;
      color: white;
      border: none;
      padding: 12px 24px;
      border-radius: 25px;
      cursor: pointer;
      font-size: 16px;
      transition: background 0.3s;
    }

    .input-controls button:hover {
      background: #5568d3;
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

    /* Modal */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      z-index: 1000;
      align-items: center;
      justify-content: center;
    }

    .modal-content {
      background: white;
      padding: 30px;
      border-radius: 20px;
      max-width: 400px;
      width: 90%;
    }

    .modal-content h2 {
      margin-bottom: 20px;
      color: #333;
    }

    .modal-content input {
      width: 100%;
      padding: 12px;
      border: 2px solid #ddd;
      border-radius: 15px;
      font-size: 14px;
      margin-bottom: 15px;
      outline: none;
    }

    .modal-content input:focus {
      border-color: #667eea;
    }

    .modal-buttons {
      display: flex;
      gap: 10px;
      justify-content: flex-end;
    }

    .modal-buttons button {
      padding: 10px 20px;
      border: none;
      border-radius: 15px;
      cursor: pointer;
      font-size: 14px;
    }

    .modal-buttons .cancel-btn {
      background: #f3f4f6;
      color: #333;
    }

    .modal-buttons .save-btn {
      background: #667eea;
      color: white;
    }

    .hidden {
      display: none !important;
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- Login Screen -->
    <div class="login-screen" id="loginScreen">
      <div class="login-box">
        <div class="emoji">💬</div>
        <h1>Worldwide chat</h1>
        <p>Connect and chat with friends</p>
        <div class="error-message" id="errorMessage"></div>
        <input type="email" id="emailInput" placeholder="Email (@gmail.com or @icloud.com)" />
        <input type="password" id="passwordInput" placeholder="Password" />
        <input type="password" id="confirmPasswordInput" placeholder="Confirm Password" />
        <button onclick="login()">Sign In</button>
      </div>
    </div>

    <!-- Main App -->
    <div class="app-screen" id="appScreen">
      <div class="header">
        <h1>💬 Discussion Board</h1>
        <div class="header-info">
          <span class="current-user" id="currentUserName"></span>
          <div class="header-buttons">
            <button onclick="logout()">Logout</button>
          </div>
        </div>
      </div>

      <div class="chat-container">
        <!-- Users List -->
        <div class="friends-list">
          <div class="friends-header">
            👥 Users
            <button class="add-user-btn" onclick="openAddUserModal()">+ Add</button>
          </div>
          <div id="usersList"></div>
        </div>

        <!-- Chat Area -->
        <div class="chat-area" id="chatArea">
          <div class="empty-state">
            <div class="icon">👥</div>
            <p>Select a user to start chatting</p>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Add User Modal -->
  <div class="modal" id="addUserModal">
    <div class="modal-content">
      <h2>Add New User</h2>
      <input type="text" id="newUserName" placeholder="Name" />
      <input type="email" id="newUserEmail" placeholder="Email" />
      <div class="modal-buttons">
        <button class="cancel-btn" onclick="closeAddUserModal()">Cancel</button>
        <button class="save-btn" onclick="addNewUser()">Add User</button>
      </div>
    </div>
  </div>

  <!-- Edit Name Modal -->
  <div class="modal" id="editNameModal">
    <div class="modal-content">
      <h2>Edit Name</h2>
      <input type="text" id="editUserName" placeholder="New Name" />
      <div class="modal-buttons">
        <button class="cancel-btn" onclick="closeEditNameModal()">Cancel</button>
        <button class="save-btn" onclick="saveUserName()">Save</button>
      </div>
    </div>
  </div>

  <script>
    var currentUser = null;
    var selectedFriend = null;
    var messages = [];
    var editingUserId = null;

    // Initial users
    var users = [
      { id: 'user1', name: 'Alex Chen', email: 'alex.chen@gmail.com', avatar: '👤' },
      { id: 'user2', name: 'Sam Rivera', email: 'sam.rivera@icloud.com', avatar: '👤' },
      { id: 'user3', name: 'Jordan Kim', email: 'jordan.kim@gmail.com', avatar: '👤' },
      { id: 'user4', name: 'Taylor Brooks', email: 'taylor.brooks@icloud.com', avatar: '👤' },
      { id: 'user5', name: 'Morgan Lee', email: 'morgan.lee@gmail.com', avatar: '👤' },
      { id: 'user6', name: 'Casey Martinez', email: 'casey.m@icloud.com', avatar: '👤' },
      { id: 'user7', name: 'Riley Johnson', email: 'riley.j@gmail.com', avatar: '👤' },
      { id: 'user8', name: 'Avery Smith', email: 'avery.smith@icloud.com', avatar: '👤' },
      { id: 'user9', name: 'Dakota Williams', email: 'dakota.w@gmail.com', avatar: '👤' },
      { id: 'user10', name: 'Quinn Davis', email: 'quinn.davis@icloud.com', avatar: '👤' }
    ];

    function showError(message) {
      var errorEl = document.getElementById('errorMessage');
      errorEl.textContent = message;
      errorEl.style.display = 'block';
    }

    function hideError() {
      document.getElementById('errorMessage').style.display = 'none';
    }

    function login() {
      hideError();
      
      var email = document.getElementById('emailInput').value.trim();
      var password = document.getElementById('passwordInput').value;
      var confirmPassword = document.getElementById('confirmPasswordInput').value;

      // Validate email ends with @gmail.com or @icloud.com
      if (!email.endsWith('@gmail.com') && !email.endsWith('@icloud.com')) {
        showError('Email must end with @gmail.com or @icloud.com');
        return;
      }

      // Validate password fields
      if (!password) {
        showError('Please enter a password');
        return;
      }

      if (password !== confirmPassword) {
        showError('Passwords do not match');
        return;
      }

      if (password.length < 6) {
        showError('Password must be at least 6 characters');
        return;
      }

      // Create current user
      currentUser = {
        id: 'currentUser',
        email: email,
        name: email.split('@')[0]
      };

      document.getElementById('currentUserName').textContent = currentUser.name;
      document.getElementById('loginScreen').style.display = 'none';
      document.getElementById('appScreen').style.display = 'flex';
      
      renderUsersList();
    }

    function logout() {
      currentUser = null;
      selectedFriend = null;
      messages = [];
      
      document.getElementById('emailInput').value = '';
      document.getElementById('passwordInput').value = '';
      document.getElementById('confirmPasswordInput').value = '';
      
      document.getElementById('loginScreen').style.display = 'flex';
      document.getElementById('appScreen').style.display = 'none';
    }

    function renderUsersList() {
      var html = '';
      for (var i = 0; i < users.length; i++) {
        var user = users[i];
        html += '<div class="friend-item" onclick="selectFriend(\'' + user.id + '\')">' +
                '<div class="friend-avatar">' + user.avatar + '</div>' +
                '<div class="friend-info">' +
                '<h3>' + user.name + '</h3>' +
                '<p>' + user.email + '</p>' +
                '</div>' +
                '<button class="edit-name-btn" onclick="event.stopPropagation(); openEditNameModal(\'' + user.id + '\')">✏️</button>' +
                '</div>';
      }
      document.getElementById('usersList').innerHTML = html;
    }

    function selectFriend(id) {
      for (var i = 0; i < users.length; i++) {
        if (users[i].id === id) {
          selectedFriend = users[i];
          break;
        }
      }

      var items = document.querySelectorAll('.friend-item');
      for (var j = 0; j < items.length; j++) {
        items[j].classList.remove('active');
      }

      if (event && event.currentTarget) {
        event.currentTarget.classList.add('active');
      }

      var chatHTML = '<div class="chat-header">' +
                    '<div class="friend-avatar">' + selectedFriend.avatar + '</div>' +
                    '<div class="friend-info">' +
                    '<h3>' + selectedFriend.name + '</h3>' +
                    '</div>' +
                    '</div>' +
                    '<div class="messages-container" id="messagesContainer"></div>' +
                    '<div class="input-area">' +
                    '<div class="input-controls">' +
                    '<input type="text" id="messageInput" placeholder="Type a message..." onkeypress="handleKeyPress(event)" />' +
                    '<button onclick="sendMessage()">Send</button>' +
                    '</div>' +
                    '</div>';

      document.getElementById('chatArea').innerHTML = chatHTML;
      renderMessages();
    }

    function sendMessage() {
      if (!selectedFriend) return;

      var messageInput = document.getElementById('messageInput');
      var text = messageInput.value.trim();
      
      if (!text) return;

      var message = {
        id: Date.now(),
        sender: currentUser.id,
        senderName: currentUser.name,
        recipient: selectedFriend.id,
        text: text,
        timestamp: Date.now()
      };

      messages.push(message);
      messageInput.value = '';
      renderMessages();
    }

    function renderMessages() {
      if (!selectedFriend) return;

      var container = document.getElementById('messagesContainer');
      if (!container) return;

      var chatMessages = [];
      for (var i = 0; i < messages.length; i++) {
        var m = messages[i];
        if ((m.sender === currentUser.id && m.recipient === selectedFriend.id) ||
            (m.sender === selectedFriend.id && m.recipient === currentUser.id)) {
          chatMessages.push(m);
        }
      }

      var html = '';
      for (var j = 0; j < chatMessages.length; j++) {
        var msg = chatMessages[j];
        var isSent = msg.sender === currentUser.id;
        var date = new Date(msg.timestamp);
        var timeStr = date.getHours() + ':' + (date.getMinutes() < 10 ? '0' : '') + date.getMinutes();

        html += '<div class="message ' + (isSent ? 'sent' : 'received') + '">' +
                '<div class="message-bubble">' +
                (!isSent ? '<div class="message-sender">' + msg.senderName + '</div>' : '') +
                '<div class="message-text">' + msg.text + '</div>' +
                '<div class="message-time">' + timeStr + '</div>' +
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

    function openAddUserModal() {
      document.getElementById('addUserModal').style.display = 'flex';
      document.getElementById('newUserName').value = '';
      document.getElementById('newUserEmail').value = '';
    }

    function closeAddUserModal() {
      document.getElementById('addUserModal').style.display = 'none';
    }

    function addNewUser() {
      var name = document.getElementById('newUserName').value.trim();
      var email = document.getElementById('newUserEmail').value.trim();

      if (!name || !email) {
        alert('Please enter both name and email');
        return;
      }

      if (!email.endsWith('@gmail.com') && !email.endsWith('@icloud.com')) {
        alert('Email must end with @gmail.com or @icloud.com');
        return;
      }

      var newUser = {
        id: 'user' + Date.now(),
        name: name,
        email: email,
        avatar: '👤'
      };

      users.push(newUser);
      renderUsersList();
      closeAddUserModal();
    }

    function openEditNameModal(userId) {
      editingUserId = userId;
      var user = null;
      for (var i = 0; i < users.length; i++) {
        if (users[i].id === userId) {
          user = users[i];
          break;
        }
      }

      if (user) {
        document.getElementById('editUserName').value = user.name;
        document.getElementById('editNameModal').style.display = 'flex';
      }
    }

    function closeEditNameModal() {
      document.getElementById('editNameModal').style.display = 'none';
      editingUserId = null;
    }

    function saveUserName() {
      var newName = document.getElementById('editUserName').value.trim();
      
      if (!newName) {
        alert('Please enter a name');
        return;
      }

      for (var i = 0; i < users.length; i++) {
        if (users[i].id === editingUserId) {
          users[i].name = newName;
          
          // Update messages with old name
          for (var j = 0; j < messages.length; j++) {
            if (messages[j].sender === editingUserId) {
              messages[j].senderName = newName;
            }
          }
          
          break;
        }
      }

      renderUsersList();
      
      if (selectedFriend && selectedFriend.id === editingUserId) {
        selectedFriend.name = newName;
        selectFriend(editingUserId);
      }
      
      closeEditNameModal();
    }
  </script>
</body>
</html>
