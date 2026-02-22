<!DOCTYPE html>
<html>
<head>
  <title>SJSLNSHS BMI Calculator</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  
  <!-- Google Font -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
  
  <!-- Firebase SDKs -->
  <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-auth-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-firestore-compat.js"></script>

  <style>
    body {
      font-family: 'Poppins', Arial, sans-serif;
      background: linear-gradient(to right, #ff9ec4, #c792ea);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .card {
      background: rgba(255,255,255,0.95);
      padding: 30px 25px;
      border-radius: 20px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.2);
      text-align: center;
      width: 420px;
      border: 2px solid #000;
      animation: fadeIn 0.6s ease-in-out;
      max-height: 90vh;
      overflow-y: auto;
      position: relative;
    }

    h1 {
      color: hotpink;
      font-size: 28px;
      margin-bottom: 10px;
      text-shadow: 1px 1px 2px #00000070;
    }

    h2 {
      color: #c792ea;
      font-size: 22px;
      margin-bottom: 20px;
      text-shadow: 1px 1px 2px #00000050;
    }

    input {
      width: 90%;
      padding: 12px;
      margin: 10px 0;
      border-radius: 10px;
      border: 2px solid #000;
      background-color: #ffe6f5;
      font-size: 16px;
      outline: none;
      box-sizing: border-box;
    }

    input:focus {
      border-color: hotpink;
    }

    button {
      padding: 10px 20px;
      border: none;
      border-radius: 10px;
      background-color: hotpink;
      color: white;
      font-size: 16px;
      font-weight: 600;
      cursor: pointer;
      margin: 6px;
      transition: 0.3s;
      box-shadow: 2px 2px 5px rgba(0,0,0,0.3);
    }

    button:hover {
      background-color: #ff5ca1;
      transform: translateY(-2px) scale(1.05);
      box-shadow: 3px 3px 8px rgba(0,0,0,0.4);
    }

    .link {
      color: #5e00ff;
      cursor: pointer;
      font-size: 14px;
      text-decoration: underline;
    }

    .box {
      margin-top: 15px;
      text-align: left;
      font-size: 14px;
      border-top: 1px solid #ccc;
      padding-top: 10px;
      max-height: 150px;
      overflow-y: auto;
    }

    .logo-left, .logo-right {
      width: 50px;
      height: 50px;
      border-radius: 10px;
      position: absolute;
      top: 15px;
    }

    .logo-left { left: 15px; }
    .logo-right { right: 15px; }

    .password-container {
      position: relative;
      width: 90%;
      margin: 10px auto;
    }

    .password-container input {
      width: 100%;
      padding: 12px 40px 12px 12px; /* right padding for eye */
    }

    .password-container .toggle-eye {
      position: absolute;
      right: 10px;
      top: 50%;
      transform: translateY(-50%);
      cursor: pointer;
      font-size: 18px;
      color: #555;
      user-select: none;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(15px); }
      to { opacity: 1; transform: translateY(0); }
    }

    #result {
      margin-top: 15px;
      font-size: 18px;
      font-weight: 600;
      color: #2f2f2f;
      text-shadow: 1px 1px 2px #ffadd5;
    }
  </style>
</head>

<body>

<!-- FRONT PAGE -->
<div id="frontPage" class="card">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSgCmMYnyp4dZMYv24Fyu2RvNxaEWrYAaUz5kHwhywFCA&s=10" class="logo-left">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIIgIbE3prBazJq_qX0sFnyRAEi7oWAZyfBp7ujJBIRw&s=10" class="logo-right">
  <h1>Welcome to the WellTrack BMI</h1>
  <h2>SJSLNSHS</h2>
  <button onclick="startApp()">Start</button>
</div>

<!-- LOGIN -->
<div id="loginPage" class="card" style="display:none;">
  <h2>Login</h2>
  <input type="text" id="loginUser" placeholder="Username">
  <div class="password-container">
    <input type="password" id="loginPass" placeholder="Password">
    <span class="toggle-eye" onclick="togglePassword('loginPass')" id="loginEye">&#128065;</span>
  </div>
  <button onclick="login()">Login</button>
  <p class="link" onclick="showSignup()">Create Account</p>
</div>

<!-- SIGNUP -->
<div id="signupPage" class="card" style="display:none;">
  <h2>Sign Up</h2>
  <input type="text" id="signupUser" placeholder="Username">
  <div class="password-container">
    <input type="password" id="signupPass" placeholder="Password">
    <span class="toggle-eye" onclick="togglePassword('signupPass')" id="signupEye">&#128065;</span>
  </div>
  <button onclick="signup()">Sign Up</button>
  <p class="link" onclick="showLogin()">Back to Login</p>
</div>

<!-- BMI PAGE -->
<div id="bmiPage" class="card" style="display:none;">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSgCmMYnyp4dZMYv24Fyu2RvNxaEWrYAaUz5kHwhywFCA&s=10" class="logo-left">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIIgIbE3prBazJq_qX0sFnyRAEi7oWAZyfBp7ujJBIRw&s=10" class="logo-right">
  <h1>BMI Calculator</h1>
  <p>Welcome, <strong id="displayUser"></strong></p>
  <input type="number" id="height" placeholder="Height (cm)">
  <input type="number" id="weight" placeholder="Weight (kg)">
  <button onclick="calculateBMI()">Calculate</button>
  <button id="adminBtn" onclick="showAdmin()">Admin Dashboard</button>
  <button onclick="logout()">Logout</button>
  <button onclick="backToFront()">Back</button>
  <h3 id="result"></h3>
</div>

<!-- ADMIN DASHBOARD -->
<div id="adminPage" class="card" style="display:none;">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSgCmMYnyp4dZMYv24Fyu2RvNxaEWrYAaUz5kHwhywFCA&s=10" class="logo-left">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIIgIbE3prBazJq_qX0sFnyRAEi7oWAZyfBp7ujJBIRw&s=10" class="logo-right">
  <h2>Admin Dashboard</h2>
  <div class="box">
    <strong>Registered Users:</strong>
    <ul id="userList"></ul>
  </div>
  <div class="box">
    <strong>BMI Records (with Date & Time):</strong>
    <ul id="recordList"></ul>
  </div>
  <button onclick="backToBMI()">Back</button>
</div>

<script>
  // Firebase config
  const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
  };
  firebase.initializeApp(firebaseConfig);
  const auth = firebase.auth();
  const db = firebase.firestore();

  let currentUser = "";
  let isAdmin = false;

  function startApp(){ frontPage.style.display="none"; loginPage.style.display="block"; }

  function togglePassword(id){
    const field = document.getElementById(id);
    const eye = id === 'loginPass' ? document.getElementById('loginEye') : document.getElementById('signupEye');
    if(field.type === "password"){
      field.type = "text";
      eye.innerHTML = "&#128068;"; // closed eye
    } else {
      field.type = "password";
      eye.innerHTML = "&#128065;"; // open eye
    }
  }

  function signup(){
    const user = signupUser.value.trim();
    const pass = signupPass.value.trim();
    if(!user || !pass){ alert("Fill all fields."); return; }

    auth.createUserWithEmailAndPassword(user+"@sjslnshs.com", pass)
        .then(() => { alert("Account created!"); showLogin(); })
        .catch(err => alert(err.message));
  }

  function login(){
    const user = loginUser.value.trim();
    const pass = loginPass.value.trim();
    auth.signInWithEmailAndPassword(user+"@sjslnshs.com", pass)
        .then(() => {
            currentUser = user;
            displayUser.innerText = user;
            isAdmin = (user.toLowerCase() === "admin");
            loginPage.style.display="none";
            bmiPage.style.display="block";
            adminBtn.style.display = isAdmin ? "inline-block" : "none";
        })
        .catch(err => alert(err.message));
  }

  function calculateBMI(){
    const h = parseFloat(height.value)/100;
    const w = parseFloat(weight.value);
    if(!h || !w){ result.innerHTML = "Enter height and weight."; return; }

    const bmi = (w/(h*h)).toFixed(2);
    const category = bmi < 18.5 ? "Underweight" :
                     bmi < 24.9 ? "Normal" :
                     bmi < 29.9 ? "Overweight" : "Obese";

    const dateTime = new Date().toLocaleString();
    db.collection("bmiRecords").add({
      user: currentUser,
      bmi,
      category,
      date: dateTime
    });

    result.innerHTML = `Your BMI is ${bmi} (${category})`;
  }

  function showAdmin(){
    if(!isAdmin) return;
    bmiPage.style.display="none";
    adminPage.style.display="block";
    loadAdminData();
  }

  function loadAdminData(){
    userList.innerHTML = "";
    recordList.innerHTML = "";

    db.collection("bmiRecords").get().then(snapshot => {
      let usersSet = new Set();
      snapshot.forEach(doc => {
        const data = doc.data();
        usersSet.add(data.user);
        let li = document.createElement("li");
        li.textContent = `${data.user} | ${data.bmi} (${data.category}) | ${data.date}`;
        recordList.appendChild(li);
      });

      usersSet.forEach(u=>{
        let li = document.createElement("li");
        li.textContent = u;
        userList.appendChild(li);
      });
    });
  }

  function backToBMI(){ adminPage.style.display="none"; bmiPage.style.display="block"; }
  function backToFront(){ bmiPage.style.display="none"; frontPage.style.display="block"; }
  function logout(){ bmiPage.style.display="none"; adminPage.style.display="none"; loginPage.style.display="block"; currentUser=""; isAdmin=false; }
  function showSignup(){ loginPage.style.display="none"; signupPage.style.display="block"; }
  function showLogin(){ signupPage.style.display="none"; loginPage.style.display="block"; }
</script>

</body>
</html>
