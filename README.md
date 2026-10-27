<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Campus Navigator</title>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:Arial,sans-serif}
body{background:#f4f7fb;color:#222}
button{cursor:pointer;border:0}
button:disabled{opacity:.5;cursor:not-allowed}

/* LOGIN */
.login{min-height:100vh;display:flex;align-items:center;justify-content:center;
background:linear-gradient(135deg,#2563eb,#7c3aed);padding:20px}
.login-box{width:850px;max-width:100%;background:white;border-radius:20px;
overflow:hidden;display:flex;box-shadow:0 20px 50px #0005}
.login-image{width:50%;padding:45px;color:white;background:
linear-gradient(#2563ebcc,#7c3aedcc),
url("https://images.unsplash.com/photo-1564981797816-1043664bf78d") center/cover}
.login-image h1{margin-top:100px;font-size:38px}
.login-image p{margin-top:15px;line-height:1.7}
.login-form{width:50%;padding:45px}
.logo{font-size:25px;font-weight:bold;color:#2563eb;margin-bottom:30px}
.login-form h2{margin-bottom:10px}
.login-form p{color:#777;margin-bottom:20px}
.input{margin:15px 0}
.input label{display:block;font-weight:bold;margin-bottom:7px}
.input input{width:100%;padding:13px;border:1px solid #ddd;border-radius:8px}
.login-btn,.action{padding:11px 15px;background:#2563eb;color:white;border-radius:8px}
.login-btn{width:100%;padding:14px;font-size:16px}
.demo{margin-top:20px;padding:12px;background:#eef4ff;border-radius:8px;font-size:13px}

/* APPLICATION */
.app{display:none}
.sidebar{width:240px;height:100vh;position:fixed;left:0;top:0;
background:white;padding:25px 15px;box-shadow:2px 0 10px #ddd;z-index:5;overflow:auto}
.brand{font-size:22px;font-weight:bold;color:#2563eb;padding:0 10px 25px}
.menu button{width:100%;background:none;padding:13px;text-align:left;
border-radius:8px;margin:3px 0;font-size:14px}
.menu button:hover,.menu button.active{background:#2563eb;color:white}
.main{margin-left:240px;padding:20px}
.topbar{background:white;padding:15px 20px;border-radius:12px;
display:flex;justify-content:space-between;align-items:center;gap:12px;
margin-bottom:20px;flex-wrap:wrap}
.search{padding:10px;border:1px solid #ddd;border-radius:8px;width:220px}
.user{display:flex;align-items:center;gap:10px}
.avatar{width:42px;height:42px;border-radius:50%;background:#2563eb;color:white;
display:flex;justify-content:center;align-items:center;font-weight:bold}
.page{display:none}
.page.active{display:block}
.welcome{padding:30px;border-radius:15px;color:white;
background:linear-gradient(100deg,#2563eb,#7c3aed);margin-bottom:20px}
.welcome h1{margin-bottom:10px}
.cards{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:15px;margin-bottom:20px}
.card,.location,.event,.college-search-panel{background:white;padding:20px;
border-radius:12px;box-shadow:0 2px 10px #ddd;margin-bottom:12px}
.card h2{color:#2563eb;margin-top:8px}
.card p{margin:8px 0}
.location-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:18px}
.location-icon{font-size:38px;margin-bottom:10px}
.location p{color:#666;margin:10px 0;line-height:1.5}
.favorite{float:right;background:none;font-size:23px}
.event span{color:#2563eb;font-weight:bold}
.event h3{margin:10px 0}
table{width:100%;border-collapse:collapse;background:white}
th,td{padding:13px;text-align:left;border-bottom:1px solid #eee}
th{background:#eef3ff}

/* CAMPUS MAP */
.map-container{background:white;padding:20px;border-radius:15px;box-shadow:0 2px 10px #ddd}
.map{height:500px;background:#dcebd8;position:relative;overflow:hidden;
border-radius:12px;border:5px solid #cbd5c0;margin-top:15px}
.road{position:absolute;background:#ddd;border:2px solid #aaa}
.road1{width:100%;height:50px;top:44%}
.road2{width:50px;height:100%;left:50%}
.building{position:absolute;padding:12px;background:white;border:2px solid #2563eb;
border-radius:8px;text-align:center;cursor:pointer;box-shadow:0 3px 8px #999}
.building:hover{transform:scale(1.05);background:#eef4ff}
.pin{font-size:23px}
.b1{top:8%;left:8%}.b2{top:10%;right:8%}
.b3{bottom:10%;left:8%}.b4{bottom:10%;right:8%}
.b5{top:38%;left:35%}.b6{bottom:5%;left:43%}.b7{top:23%;left:65%}

/* COLLEGE FINDER */
.college-search-row{display:flex;gap:10px;flex-wrap:wrap;margin:15px 0}
.college-search-row input{flex:1;min-width:220px;padding:13px;border:1px solid #ddd;border-radius:8px}
.college-results{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:15px;margin-top:18px}
.college-result{background:white;padding:18px;border:1px solid #e5e7eb;border-radius:12px;overflow-wrap:anywhere}
.college-result h3{margin-bottom:10px;color:#2563eb}
.college-result p{color:#555;line-height:1.5;margin:8px 0}
.status-message{padding:12px;border-radius:8px;background:#eef4ff;margin:12px 0;line-height:1.5}
.college-map{width:100%;height:350px;border:0;border-radius:12px;margin-top:15px}
.section-title{margin-bottom:15px}
.dark{background:#151923;color:white}
.dark .sidebar,.dark .topbar,.dark .card,.dark .location,
.dark .event,.dark .map-container,.dark .college-search-panel,
.dark .college-result{background:#202530;color:white}
.dark .building{background:#303642;color:white}
.dark .location p,.dark .college-result p{color:#ddd}

@media(max-width:950px){
 .cards{grid-template-columns:repeat(2,minmax(0,1fr))}
 .login-image{display:none}.login-form{width:100%}
}
@media(max-width:650px){
 .sidebar{width:65px;padding:15px 6px}
 .brand{font-size:0;padding:10px 8px 20px}
 .brand:first-letter{font-size:24px}
 .menu button{font-size:0;padding:13px 8px}
 .menu button:first-letter{font-size:19px}
 .main{margin-left:65px;padding:10px}
 .cards{grid-template-columns:1fr}
 .search{width:145px}
 .map{height:420px}
 .building{font-size:11px;padding:7px}
 .topbar{padding:12px}
 .college-search-row input{min-width:100%}
}
</style>
</head>

<body>

<!-- LOGIN PAGE -->
<div class="login" id="loginPage">
 <div class="login-box">
  <div class="login-image">
   <h2>🗺️ Campus Navigator</h2>
   <h1>Explore Your Campus</h1>
   <p>Find classrooms, departments, library, canteen, parking, events and emergency facilities quickly from one smart platform.</p>
  </div>

  <div class="login-form">
   <div class="logo">🗺️ CampusNav</div>
   <h2>Welcome Back 👋</h2>
   <p>Login to explore your campus.</p>

   <div class="input">
    <label for="email">Email</label>
    <input id="email" type="email" placeholder="Enter email">
   </div>

   <div class="input">
    <label for="password">Password</label>
    <input id="password" type="password" placeholder="Enter password">
   </div>

   <button class="login-btn" onclick="login()">Login</button>

   <div class="demo">
    <b>Demo Credentials</b><br><br>
    Email: student@gmail.com<br>
    Password: 12345
   </div>
  </div>
 </div>
</div>

<!-- MAIN APPLICATION -->
<div class="app" id="app">

 <aside class="sidebar">
  <div class="brand">🗺️ CampusNav</div>
  <div class="menu">
   <button class="active" onclick="openPage('dashboard',this)">🏠 Dashboard</button>
   <button onclick="openPage('mapPage',this)">🗺️ Campus Map</button>
   <button onclick="openPage('collegeFinder',this)">🌐 Find Colleges</button>
   <button onclick="openPage('locations',this)">📍 Locations</button>
   <button onclick="openPage('departments',this)">🏫 Departments</button>
   <button onclick="openPage('events',this)">📅 Events</button>
   <button onclick="openPage('favorites',this)">⭐ Favorites</button>
   <button onclick="openPage('emergency',this)">🚨 Emergency</button>
   <button onclick="openPage('profile',this)">👤 Profile</button>
   <button onclick="darkMode()">🌙 Dark Mode</button>
   <button onclick="logout()">🚪 Logout</button>
  </div>
 </aside>

 <main class="main">
  <div class="topbar">
   <h3 id="pageTitle">Campus Dashboard</h3>
   <input class="search" placeholder="🔎 Search campus..."
          oninput="searchCampus(this.value)">
   <div class="user">
    <div><b>Rithika</b><br><small>Student</small></div>
    <div class="avatar">R</div>
   </div>
  </div>

  <!-- DASHBOARD -->
  <section class="page active" id="dashboard">
   <div class="welcome">
    <h1>Welcome to Campus Navigator! 👋</h1>
    <p>Find everything around your campus quickly and easily.</p>
   </div>

   <div class="cards">
    <div class="card"><p>🏫 Buildings</p><h2>24</h2><small>Campus buildings</small></div>
    <div class="card"><p>📍 Locations</p><h2>86</h2><small>Registered locations</small></div>
    <div class="card"><p>📅 Events</p><h2>12</h2><small>Upcoming events</small></div>
    <div class="card"><p>⭐ Favorites</p><h2 id="favoriteCount">0</h2><small>Your saved places</small></div>
   </div>

   <div class="cards">
    <div class="card">
     <h3>⚡ Quick Navigation</h3><br>
     <button class="action" onclick="navigate('Library')">📚 Library</button><br><br>
     <button class="action" onclick="navigate('Canteen')">🍔 Canteen</button><br><br>
     <button class="action" onclick="navigate('Main Block')">🏫 Main Block</button>
    </div>

    <div class="card">
     <h3>🧭 Recent Searches</h3>
     <div id="recentList"><p style="margin-top:15px">No recent searches yet.</p></div>
    </div>

    <div class="card">
     <h3>📢 Announcements</h3>
     <p style="margin-top:15px">New CSE block opened</p>
     <p>Annual fest registration open</p>
     <p>Check the Events section for details.</p>
    </div>

    <div class="card">
     <h3>🚨 Emergency</h3>
     <p style="margin:15px 0">Need emergency assistance?</p>
     <button class="action" onclick="openPageById('emergency')">Emergency Contacts</button>
    </div>
   </div>
  </section>

  <!-- CAMPUS MAP -->
  <section class="page" id="mapPage">
   <h2 class="section-title">🗺️ Interactive Campus Map</h2>
   <div class="map-container">
    <p>Click any building to view information.</p>
    <div class="map">
     <div class="road road1"></div>
     <div class="road road2"></div>
     <button class="building b1" onclick="locationInfo('Main Block')"><div class="pin">🏫</div>Main Block</button>
     <button class="building b2" onclick="locationInfo('Library')"><div class="pin">📚</div>Library</button>
     <button class="building b3" onclick="locationInfo('Canteen')"><div class="pin">🍔</div>Canteen</button>
     <button class="building b4" onclick="locationInfo('Sports Complex')"><div class="pin">🏀</div>Sports</button>
     <button class="building b5" onclick="locationInfo('CSE Department')"><div class="pin">💻</div>CSE</button>
     <button class="building b6" onclick="locationInfo('Seminar Hall')"><div class="pin">🎤</div>Seminar Hall</button>
     <button class="building b7" onclick="locationInfo('Parking')"><div class="pin">🚗</div>Parking</button>
    </div>
    <p style="margin-top:12px;color:#777">Note: This is a sample campus layout, not a verified geographical map.</p>
   </div>
  </section>

  <!-- MULTI-COLLEGE FINDER -->
  <section class="page" id="collegeFinder">
   <h2 class="section-title">🌐 Find Colleges Anywhere</h2>
   <p>Search for colleges by name, city or state. Select a result to view its address on the map and open directions.</p>

   <div class="college-search-panel">
    <h3>🔎 Search Colleges</h3>
    <div class="college-search-row">
     <input id="collegeQuery" placeholder="Example: engineering colleges in Vijayawada"
            onkeydown="if(event.key==='Enter')searchColleges()">
     <button class="action" onclick="searchColleges()">Search</button>
     <button class="action" onclick="useCollegeExample()">Try Example</button>
    </div>
    <div class="status-message" id="collegeStatus">
     Enter a college name and city/state. Internet access is required.
    </div>
    <div class="college-results" id="collegeResults"></div>
   </div>

   <div class="college-search-panel">
    <h3>📍 Selected College Location</h3>
    <p id="selectedCollegeAddress" style="margin-top:10px">Choose a search result to show its address and map.</p>
    <iframe id="collegeMap" class="college-map" title="Selected college map"
     loading="lazy" src="https://www.openstreetmap.org/export/embed.html?bbox=80.5%2C16.4%2C80.8%2C16.6&amp;layer=mapnik"></iframe>
    <div style="margin-top:14px">
     <button class="action" id="directionsButton" onclick="openCollegeDirections()" disabled>🧭 Get Directions</button>
     <button class="action" onclick="openCollegeMapWebsite()">Open Full Map</button>
    </div>
   </div>
  </section>

  <!-- LOCATIONS -->
  <section class="page" id="locations">
   <h2 class="section-title">📍 Campus Locations</h2>
   <div class="location-grid" id="locationGrid">

    <div class="location" data-search="library central library books">
     <button class="favorite" onclick="toggleFavorite(this,'Library')">♡</button>
     <div class="location-icon">📚</div><h3>Central Library</h3>
     <p>Books, journals and digital resources.</p>
     <button class="action" onclick="navigate('Central Library')">🧭 Navigate</button>
    </div>

    <div class="location" data-search="cse department computer science">
     <button class="favorite" onclick="toggleFavorite(this,'CSE Department')">♡</button>
     <div class="location-icon">💻</div><h3>CSE Department</h3>
     <p>Computer Science Engineering block.</p>
     <button class="action" onclick="navigate('CSE Department')">🧭 Navigate</button>
    </div>

    <div class="location" data-search="canteen food refreshments">
     <button class="favorite" onclick="toggleFavorite(this,'Canteen')">♡</button>
     <div class="location-icon">🍔</div><h3>College Canteen</h3>
     <p>Food court and refreshments.</p>
     <button class="action" onclick="navigate('Canteen')">🧭 Navigate</button>
    </div>

    <div class="location" data-search="sports complex ground">
     <button class="favorite" onclick="toggleFavorite(this,'Sports Complex')">♡</button>
     <div class="location-icon">🏀</div><h3>Sports Complex</h3>
     <p>Indoor and outdoor sports facilities.</p>
     <button class="action" onclick="navigate('Sports Complex')">🧭 Navigate</button>
    </div>

    <div class="location" data-search="medical center hospital first aid">
     <button class="favorite" onclick="toggleFavorite(this,'Medical Center')">♡</button>
     <div class="location-icon">🏥</div><h3>Medical Center</h3>
     <p>First aid and basic medical support.</p>
     <button class="action" onclick="navigate('Medical Center')">🧭 Navigate</button>
    </div>

    <div class="location" data-search="parking vehicles">
     <button class="favorite" onclick="toggleFavorite(this,'Parking')">♡</button>
     <div class="location-icon">🚗</div><h3>Parking Area</h3>
     <p>Student and faculty parking.</p>
     <button class="action" onclick="navigate('Parking')">🧭 Navigate</button>
    </div>

    <div class="location" data-search="seminar hall auditorium">
     <button class="favorite" onclick="toggleFavorite(this,'Seminar Hall')">♡</button>
     <div class="location-icon">🎤</div><h3>Seminar Hall</h3>
     <p>Seminars, meetings and presentations.</p>
     <button class="action" onclick="navigate('Seminar Hall')">🧭 Navigate</button>
    </div>

    <div class="location" data-search="main block administration office">
     <button class="favorite" onclick="toggleFavorite(this,'Main Block')">♡</button>
     <div class="location-icon">🏫</div><h3>Main Block</h3>
     <p>Administration and academic offices.</p>
     <button class="action" onclick="navigate('Main Block')">🧭 Navigate</button>
    </div>
   </div>
  </section>

  <!-- DEPARTMENTS -->
  <section class="page" id="departments">
   <h2 class="section-title">🏫 Departments</h2>
   <div class="location-grid">
    <div class="location"><div class="location-icon">💻</div><h3>CSE</h3><p>Computer Science Engineering</p><button class="action" onclick="locationInfo('CSE Department')">View Location</button></div>
    <div class="location"><div class="location-icon">📊</div><h3>CSE - Data Science</h3><p>Data analytics, AI and machine learning.</p><button class="action" onclick="locationInfo('CSE Data Science Department')">View Location</button></div>
    <div class="location"><div class="location-icon">⚡</div><h3>ECE</h3><p>Electronics and Communication</p><button class="action" onclick="locationInfo('ECE Department')">View Location</button></div>
    <div class="location"><div class="location-icon">⚙️</div><h3>Mechanical</h3><p>Mechanical Engineering</p><button class="action" onclick="locationInfo('Mechanical Department')">View Location</button></div>
    <div class="location"><div class="location-icon">🏗️</div><h3>Civil</h3><p>Civil Engineering</p><button class="action" onclick="locationInfo('Civil Department')">View Location</button></div>
   </div>
  </section>

  <!-- EVENTS -->
  <section class="page" id="events">
   <h2 class="section-title">📅 Campus Events</h2>
   <div class="event"><span>August 15</span><h3>🎉 Independence Day Celebration</h3><p>Main Auditorium • 9:00 AM</p></div>
   <div class="event"><span>August 18</span><h3>💻 Hackathon 2026</h3><p>Innovation Lab • 10:00 AM</p></div>
   <div class="event"><span>August 22</span><h3>🎤 Tech Symposium</h3><p>Seminar Hall • 11:00 AM</p></div>
   <div class="event"><span>August 25</span><h3>🏆 Annual Sports Meet</h3><p>Sports Ground • 8:00 AM</p></div>
   <p style="color:#777;margin-top:10px">Sample events for demonstration. Check your college notice board for actual dates.</p>
  </section>

  <!-- FAVORITES -->
  <section class="page" id="favorites">
   <h2 class="section-title">⭐ Favorite Locations</h2>
   <div class="card"><p>Your favorite locations will appear here.</p><br><div id="favoriteList">No favorites added yet.</div></div>
  </section>

  <!-- EMERGENCY -->
  <section class="page" id="emergency">
   <h2 class="section-title">🚨 Emergency Information</h2>
   <div class="cards">
    <div class="card"><h3>🚑 Medical Center</h3><p>Campus Health Center</p><br><button class="action" onclick="alert('Please use the verified campus medical contact number.')">📞 Contact Info</button></div>
    <div class="card"><h3>🚓 Security</h3><p>Campus Security Office</p><br><button class="action" onclick="alert('Please use the verified campus security contact number.')">📞 Contact Info</button></div>
    <div class="card"><h3>🔥 Fire Emergency</h3><p>Emergency Response Team</p><br><button class="action" onclick="alert('For an actual emergency in India, call 112.')">📞 Emergency Info</button></div>
    <div class="card"><h3>🆘 Help Desk</h3><p>Campus Help Center</p><br><button class="action" onclick="alert('Please contact your college help desk directly.')">📞 Contact Info</button></div>
   </div>
   <p>For a real emergency in India, call 112. Replace sample campus contacts with verified phone numbers.</p>
  </section>

  <!-- PROFILE -->
  <section class="page" id="profile">
   <h2 class="section-title">👤 My Profile</h2>
   <div class="card">
    <h2>Rithika Nalluri</h2><br>
    <p><b>Email:</b> student@gmail.com</p>
    <p style="margin-top:10px"><b>Role:</b> Student</p>
    <p style="margin-top:10px"><b>Department:</b> CSE - Data Science</p>
    <p style="margin-top:10px"><b>Year:</b> 3rd Year</p>
    <p style="margin-top:10px"><b>Campus:</b> Main Campus</p>
   </div>
  </section>

 </main>
</div>

<script>
/* LOGIN */
function login(){
 const email=document.getElementById("email").value.trim();
 const password=document.getElementById("password").value;

 if(email==="student@gmail.com" && password==="12345"){
  document.getElementById("loginPage").style.display="none";
  document.getElementById("app").style.display="block";
 }else{
  alert("Invalid login details.\n\nEmail: student@gmail.com\nPassword: 12345");
 }
}

document.getElementById("password").addEventListener("keydown",function(e){
 if(e.key==="Enter") login();
});

/* PAGE NAVIGATION */
const pageNames={
 dashboard:"Campus Dashboard",
 mapPage:"Interactive Campus Map",
 collegeFinder:"Find Colleges",
 locations:"Campus Locations",
 departments:"Departments",
 events:"Campus Events",
 favorites:"Favorite Locations",
 emergency:"Emergency Information",
 profile:"My Profile"
};

function openPage(id,button){
 document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
 const page=document.getElementById(id);
 if(page) page.classList.add("active");

 document.querySelectorAll(".menu button").forEach(b=>b.classList.remove("active"));
 if(button) button.classList.add("active");

 document.getElementById("pageTitle").textContent=pageNames[id]||"Campus Navigator";
}

function openPageById(id){
 const button=[...document.querySelectorAll(".menu button")]
  .find(b=>b.getAttribute("onclick")?.includes("'"+id+"'"));
 openPage(id,button);
}

/* CAMPUS LOCATION INFORMATION */
function locationInfo(place){
 alert("📍 "+place+"\n\nThis is a sample campus location.\nUse Navigate to search for directions.");
}

/* GOOGLE MAPS DIRECTIONS */
function navigate(place){
 const destination=encodeURIComponent(place+" college campus");
 window.open("https://www.google.com/maps/dir/?api=1&destination="+destination,"_blank","noopener");
}

/* RECENT SEARCHES */
let recentSearches=[];

function addRecent(place){
 recentSearches=[place,...recentSearches.filter(x=>x!==place)].slice(0,5);
 document.getElementById("recentList").innerHTML=recentSearches
  .map(x=>"<p style='margin-top:12px'>📍 "+escapeHTML(x)+"</p>").join("");
}

function searchCampus(value){
 if(value.trim().length<2) return;

 const query=value.trim().toLowerCase();
 const locations=[...document.querySelectorAll(".location[data-search]")];
 locations.forEach(item=>{
  item.style.display=item.dataset.search.includes(query)?"block":"none";
 });

 if(value.trim().length>=3) addRecent(value.trim());
}

/* FAVORITES */
let favorites=[];

function toggleFavorite(button,place){
 if(favorites.includes(place)){
  favorites=favorites.filter(x=>x!==place);
  button.innerHTML="♡";
  button.style.color="";
 }else{
  favorites.push(place);
  button.innerHTML="♥";
  button.style.color="red";
 }
 updateFavorites();
}

function updateFavorites(){
 document.getElementById("favoriteCount").textContent=favorites.length;
 const list=document.getElementById("favoriteList");

 if(favorites.length===0){
  list.textContent="No favorites added yet.";
  return;
 }

 list.innerHTML=favorites.map(place=>
  "<p style='padding:8px 0'>⭐ "+escapeHTML(place)+
  " <button class='action' onclick=\"navigate('"+place.replace(/'/g,"\\'")+"')\">Navigate</button></p>"
 ).join("");
}

/* COLLEGE SEARCH */
let selectedCollege=null;

function useCollegeExample(){
 document.getElementById("collegeQuery").value=
  "Dhanekula Institute of Engineering and Technology, Andhra Pradesh, India";
 searchColleges();
}

async function searchColleges(){
 const query=document.getElementById("collegeQuery").value.trim();
 const status=document.getElementById("collegeStatus");
 const results=document.getElementById("collegeResults");
 const directions=document.getElementById("directionsButton");

 if(!query){
  status.textContent="Please enter a college name, city or state.";
  results.innerHTML="";
  return;
 }

 status.textContent="Searching for matching places...";
 results.innerHTML="";
 selectedCollege=null;
 directions.disabled=true;

 try{
  const url="https://nominatim.openstreetmap.org/search?format=jsonv2&addressdetails=1&limit=8&q="+encodeURIComponent(query);
  const response=await fetch(url,{headers:{"Accept":"application/json"}});
  if(!response.ok) throw new Error("Search service unavailable");

  const places=await response.json();

  if(!places.length){
   status.textContent="No matching places found. Try adding the city and state.";
   return;
  }

  status.textContent="Found "+places.length+" possible result(s). Verify the address before travelling.";

  places.forEach((place,index)=>{
   const card=document.createElement("div");
   card.className="college-result";

   const title=document.createElement("h3");
   title.textContent=place.name||("Search result "+(index+1));

   const address=document.createElement("p");
   address.textContent=place.display_name||"Address not available.";

   const choose=document.createElement("button");
   choose.className="action";
   choose.textContent="View Address & Map";
   choose.addEventListener("click",()=>selectCollege(place));

   card.append(title,address,choose);
   results.appendChild(card);
  });
 }catch(error){
  status.textContent="Could not search. Check your internet connection and try again.";
 }
}

function selectCollege(place){
 selectedCollege=place;
 const lat=Number(place.lat);
 const lon=Number(place.lon);
 const delta=0.01;

 const bbox=[lon-delta,lat-delta,lon+delta,lat+delta].join("%2C");

 document.getElementById("selectedCollegeAddress").textContent=
  (place.name||"Selected place")+" — "+(place.display_name||"Address unavailable");

 document.getElementById("collegeMap").src=
  "https://www.openstreetmap.org/export/embed.html?bbox="+bbox+
  "&layer=mapnik&marker="+encodeURIComponent(lat+","+lon);

 document.getElementById("directionsButton").disabled=false;
}

function openCollegeDirections(){
 if(!selectedCollege) return;
 const destination=selectedCollege.lat+","+selectedCollege.lon;
 window.open("https://www.google.com/maps/dir/?api=1&destination="+
  encodeURIComponent(destination),"_blank","noopener");
}

function openCollegeMapWebsite(){
 if(selectedCollege){
  const lat=encodeURIComponent(selectedCollege.lat);
  const lon=encodeURIComponent(selectedCollege.lon);
  window.open("https://www.openstreetmap.org/?mlat="+lat+"&mlon="+lon+
   "#map=16/"+lat+"/"+lon,"_blank","noopener");
 }else{
  window.open("https://www.openstreetmap.org","_blank","noopener");
 }
}

/* DARK MODE */
function darkMode(){
 document.body.classList.toggle("dark");
}

/* LOGOUT */
function logout(){
 if(confirm("Logout from Campus Navigator?")){
  document.getElementById("app").style.display="none";
  document.getElementById("loginPage").style.display="flex";
  document.getElementById("email").value="";
  document.getElementById("password").value="";
 }
}

/* SAFE DISPLAY OF USER SEARCH TEXT */
function escapeHTML(value){
 return String(value).replace(/[&<>"']/g,function(char){
  return {"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[char];
 });
}
</script>

</body>
</html>
