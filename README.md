<!DOCTYPE html>
<html>
<head>
  <title>WellTrack BMI - SJSLNSHS</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Poppins', Arial, sans-serif;
      background: linear-gradient(to right, #ff9ec4, #c792ea);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
      padding: 20px;
    }

    .card {
      background: rgba(255,255,255,0.95);
      padding: 30px 40px;
      border-radius: 20px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.2);
      text-align: center;
      width: 90%;
      max-width: 900px;
      border: 2px solid #000;
      animation: fadeIn 0.6s ease-in-out;
      max-height: 90vh;
      overflow-y: auto;
      position: relative;
    }

    /* FRONT PAGE FIX */
    #frontPage {
      padding: 100px 40px 30px 40px;
    }

    #frontPage h1 {
      font-size: 28px; 
      margin-bottom: 8px;
    }

    #frontPage h2 {
      font-size: 20px; 
      margin-bottom: 20px;
    }

    h1 { color: hotpink; font-size: 32px; margin-bottom: 10px; text-shadow: 1px 1px 2px #00000070; }
    h2 { color: #c792ea; font-size: 24px; margin-bottom: 20px; text-shadow: 1px 1px 2px #00000050; }

    input {
      width: 90%;
      max-width: 400px;
      padding: 12px;
      margin: 10px 0;
      border-radius: 10px;
      border: 1px solid #ccc;
      background-color: #ffe6f5;
      font-size: 16px;
      box-sizing: border-box;
    }

    .password-container {
      position: relative;
      width: 90%;
      max-width: 400px;
      margin: 10px auto;
    }

    .password-container input {
      width: 100%;
      padding: 12px 40px 12px 12px;
      border-radius: 10px;
      border: 1px solid #ccc;
      background-color: #ffe6f5;
      font-size: 16px;
      box-sizing: border-box;
    }

    .toggle-eye {
      position: absolute;
      right: 12px;
      top: 50%;
      transform: translateY(-50%);
      cursor: pointer;
      font-size: 18px;
      color: #5e00ff;
      user-select: none;
    }

    .toggle-eye:hover { color: #ff5ca1; }

    button {
      padding: 12px 25px;
      border-radius: 12px;
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

    .logo-left, .logo-right {
      width: 60px;
      height: 60px;
      border-radius: 10px;
      position: absolute;
      top: 15px;
    }

    .logo-left { left: 15px; }
    .logo-right { right: 15px; }

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

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 15px;
      font-size: 14px;
    }

    th, td {
      border: 1px solid #ccc;
      padding: 8px;
      text-align: center;
    }

    th { background-color: hotpink; color: white; }

    td button {
      padding: 4px 8px;
      font-size: 12px;
      margin: 2px;
    }

    #searchInput, #searchInputAdmin {
      width: 95%;
      max-width: 450px;
      padding: 10px;
      margin-bottom: 15px;
      border-radius: 8px;
      border: 1px solid #ccc;
    }

    @media (max-width: 768px) {
      .card { width: 95%; padding: 20px 25px; }
      input, .password-container { width: 95%; }
      table th, table td { font-size: 12px; padding: 6px; }
      h1 { font-size: 26px; }
      h2 { font-size: 20px; }
    }
  </style>
</head>

<body>
<!-- FRONT PAGE -->
<div id="frontPage" class="card">
  <img src="https://upload.wikimedia.org/wikipedia/en/c/c3/BMI_Logo_blue_spark.svg" class="logo-left">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIIgIbE3prBazJq_qX0sFnyRAEi7oWAZyfBp7ujJBIRw&s=10" class="logo-right">
  <h1>Welcome to the WellTrack BMI</h1>
  <h2>SJSLNSHS</h2>
  <button onclick="startApp()">Login / Sign Up</button>
  <button onclick="viewDashboard()">View Dashboard</button>
</div>

<!-- LOGIN -->
<div id="loginPage" class="card" style="display:none;">
  <h2>Login</h2>
  <input type="text" id="loginUser" placeholder="Surname-Section">
  <div class="password-container">
    <input type="password" id="loginPass" placeholder="Password">
    <span class="toggle-eye" onclick="togglePassword('loginPass')">&#128065;</span>
  </div>
  <button onclick="login()">Login</button>
  <p class="link" onclick="showSignup()">Create Account</p>
</div>

<!-- SIGNUP -->
<div id="signupPage" class="card" style="display:none;">
  <h2>Sign Up</h2>
  <input type="text" id="signupUser" placeholder="Surname-Section">
  <div class="password-container">
    <input type="password" id="signupPass" placeholder="Password">
    <span class="toggle-eye" onclick="togglePassword('signupPass')">&#128065;</span>
  </div>
  <button onclick="signup()">Sign Up</button>
  <p class="link" onclick="showLogin()">Back to Login</p>
</div>

<!-- BMI CALCULATOR -->
<div id="bmiPage" class="card" style="display:none;">
  <img src="https://upload.wikimedia.org/wikipedia/en/c/c3/BMI_Logo_blue_spark.svg" class="logo-left">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIIgIbE3prBazJq_qX0sFnyRAEi7oWAZyfBp7ujJBIRw&s=10" class="logo-right">

  <h1>WellTrack BMI</h1>
  <p>Welcome, <strong id="displayUser"></strong></p>

  <input type="number" id="height" placeholder="Height (cm)">
  <input type="number" id="weight" placeholder="Weight (kg)">

  <button onclick="calculateBMI()">Calculate</button>
  <button id="adminBtn" onclick="showAdmin()" style="display:none;">Admin Dashboard</button>
  <button onclick="logout()">Logout</button>
  <button onclick="backToFront()">Back</button>

  <h3 id="result"></h3>
</div>

<!-- USER DASHBOARD -->
<div id="dashboardPage" class="card" style="display:none;">
  <img src="https://upload.wikimedia.org/wikipedia/en/c/c3/BMI_Logo_blue_spark.svg" class="logo-left">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIIgIbE3prBazJq_qX0sFnyRAEi7oWAZyfBp7ujJBIRw&s=10" class="logo-right">

  <h2>BMI Dashboard</h2>
  <input type="text" id="searchInput" placeholder="Search by surname" onkeyup="searchRecordsDashboard()">

  <table>
    <thead>
      <tr>
        <th>#</th>
        <th>Surname</th>
        <th>Section</th>
        <th>Height (cm)</th>
        <th>Weight (kg)</th>
        <th>BMI</th>
        <th>Category</th>
      </tr>
    </thead>
    <tbody id="dashboardTableBody"></tbody>
  </table>

  <button onclick="backToFront()">Back</button>
</div>

<!-- ADMIN DASHBOARD -->
<div id="adminPage" class="card" style="display:none;">
  <img src="https://upload.wikimedia.org/wikipedia/en/c/c3/BMI_Logo_blue_spark.svg" class="logo-left">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIIgIbE3prBazJq_qX0sFnyRAEi7oWAZyfBp7ujJBIRw&s=10" class="logo-right">

  <h2>Admin Dashboard</h2>
  <input type="text" id="searchInputAdmin" placeholder="Search by surname" onkeyup="searchRecordsAdmin()">

  <table>
    <thead>
      <tr>
        <th>#</th>
        <th>Surname</th>
        <th>Section</th>
        <th>Height (cm)</th>
        <th>Weight (kg)</th>
        <th>BMI</th>
        <th>Category</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody id="adminTableBody"></tbody>
  </table>

  <button onclick="backToBMI()">Back</button>
</div>

<script>
let users = JSON.parse(localStorage.getItem("users")) || { "admin":"admin123" };
let bmiRecords = JSON.parse(localStorage.getItem("bmiRecords")) || [];
let currentUser = "";
let isAdmin = false;

function startApp(){ frontPage.style.display="none"; loginPage.style.display="block"; }
function showSignup(){ loginPage.style.display="none"; signupPage.style.display="block"; }
function showLogin(){ signupPage.style.display="none"; loginPage.style.display="block"; }

function togglePassword(id){
  const input = document.getElementById(id);
  input.type = input.type==="password" ? "text" : "password";
}

function signup(){
  let user = signupUser.value.trim();
  let pass = signupPass.value.trim();
  if(!user || !pass){ alert("Fill all fields."); return; }
  if(users[user]){ alert("Username exists."); return; }
  users[user] = pass;
  localStorage.setItem("users", JSON.stringify(users));
  alert("Account created!");
  showLogin();
}

function login(){
  let user = loginUser.value.trim();
  let pass = loginPass.value.trim();
  if(users[user] && users[user] === pass){
    currentUser = user;
    isAdmin = (user==="admin");
    displayUser.innerText = user;
    loginPage.style.display="none";
    bmiPage.style.display="block";
    adminBtn.style.display = isAdmin ? "inline-block" : "none";
  } else{ alert("Invalid login."); }
}

function calculateBMI(){
  let hVal = parseFloat(height.value);
  let wVal = parseFloat(weight.value);
  let h = hVal/100;
  if(!hVal||!wVal){ result.innerHTML="Enter valid height & weight"; return; }
  let bmi = wVal/(h*h);
  let category="";
  if(bmi<18.5) category="Underweight";
  else if(bmi<24.9) category="Normal";
  else if(bmi<29.9) category="Overweight";
  else category="Obese";

  let parts = currentUser.split("-");
  let surname = parts[0] || "";
  let section = parts[1] || "";

  bmiRecords.push({
    user: currentUser,
    surname: surname,
    section: section,
    height: hVal,
    weight: wVal,
    bmi: bmi.toFixed(2),
    category: category
  });

  localStorage.setItem("bmiRecords", JSON.stringify(bmiRecords));
  result.innerHTML = `Your BMI is ${bmi.toFixed(2)} (${category})`;
}

function viewDashboard(){
  frontPage.style.display="none";
  dashboardPage.style.display="block";
  loadDashboardRecords();
}

function loadDashboardRecords(){
  const tbody = document.getElementById("dashboardTableBody");
  tbody.innerHTML="";
  bmiRecords.forEach((r,i)=>{
    const tr = document.createElement("tr");
    tr.innerHTML = `
      <td>${i+1}</td>
      <td>${r.surname}</td>
      <td>${r.section}</td>
      <td>${r.height}</td>
      <td>${r.weight}</td>
      <td>${r.bmi}</td>
      <td>${r.category}</td>
    `;
    tbody.appendChild(tr);
  });
}

function searchRecordsDashboard(){
  const val = searchInput.value.toLowerCase();
  const trs = dashboardTableBody.querySelectorAll("tr");
  trs.forEach(tr=>{
    let user = tr.cells[1].textContent.toLowerCase();
    tr.style.display = user.includes(val) ? "" : "none";
  });
}

// Admin
function showAdmin(){
  if(!isAdmin) return;
  bmiPage.style.display="none";
  adminPage.style.display="block";
  loadAdminRecords();
}

function loadAdminRecords(){
  const tbody = document.getElementById("adminTableBody");
  tbody.innerHTML="";
  bmiRecords.forEach((r,i)=>{
    const tr = document.createElement("tr");
    tr.innerHTML=`
      <td>${i+1}</td>
      <td>${r.surname}</td>
      <td>${r.section}</td>
      <td>${r.height}</td>
      <td>${r.weight}</td>
      <td>${r.bmi}</td>
      <td>${r.category}</td>
      <td>
        <button onclick="updateRecord(${i})">Update</button>
        <button onclick="deleteRecord(${i})">Delete</button>
      </td>
    `;
    tbody.appendChild(tr);
  });
}

function searchRecordsAdmin(){
  const val = searchInputAdmin.value.toLowerCase();
  const trs = adminTableBody.querySelectorAll("tr");
  trs.forEach(tr=>{
    let user = tr.cells[1].textContent.toLowerCase();
    tr.style.display = user.includes(val) ? "" : "none";
  });
}

function updateRecord(index){
  const newBMI = prompt("Enter new BMI:", bmiRecords[index].bmi);
  if(newBMI){
    bmiRecords[index].bmi = parseFloat(newBMI).toFixed(2);
    bmiRecords[index].category="";
    let bmiVal = parseFloat(newBMI);
    if(bmiVal<18.5) bmiRecords[index].category="Underweight";
    else if(bmiVal<24.9) bmiRecords[index].category="Normal";
    else if(bmiVal<29.9) bmiRecords[index].category="Overweight";
    else bmiRecords[index].category="Obese";
    localStorage.setItem("bmiRecords", JSON.stringify(bmiRecords));
    loadAdminRecords();
  }
}

function deleteRecord(index){
  if(confirm("Delete this record?")){
    bmiRecords.splice(index,1);
    localStorage.setItem("bmiRecords", JSON.stringify(bmiRecords));
    loadAdminRecords();
  }
}

function backToBMI(){ adminPage.style.display="none"; bmiPage.style.display="block"; }
function backToFront(){ bmiPage.style.display="none"; dashboardPage.style.display="none"; frontPage.style.display="block"; }
function logout(){ bmiPage.style.display="none"; adminPage.style.display="none"; loginPage.style.display="block"; currentUser=""; isAdmin=false; }
</script>
</body>
</html>      display: flex;
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
