<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Pilot Pre-Flight Walk Around</title>
  <style>
    /* Global & Reset Styles */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      overflow: hidden;
      background: black;
    }

    /* Video Background */
    #video-background {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
      z-index: -1;
    }

    /* Top Bar (Home screen) */
    .top-buttons {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      padding: 10px 20px;
      background: rgba(80, 80, 80, 0.7);
      backdrop-filter: blur(5px);
      border-bottom: 1px solid rgba(255, 255, 255, 0.2);
      display: flex;
      justify-content: space-between;
      align-items: center;
      z-index: 10;
    }

    /* Modern Button Styles */
    .button {
      background: rgba(50, 50, 50, 0.8);
      color: #fff;
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 16px;
      transition: background 0.3s, transform 0.2s;
    }
    .button:hover {
      background: rgba(50, 50, 50, 1);
      transform: translateY(-2px);
    }

    /* Home Button (visible when checklist is active) */
    #home-btn {
      position: fixed;
      top: 10px;
      left: 10px;
      z-index: 30;
      display: none;
      background: rgba(50, 50, 50, 0.8);
      color: #fff;
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 16px;
      transition: background 0.3s, transform 0.2s;
    }
    #home-btn:hover {
      background: rgba(50, 50, 50, 1);
      transform: translateY(-2px);
    }

    /* Main UI Container (Search Interface) */
    .container {
      position: relative;
      width: 90%;
      max-width: 400px;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      z-index: 10;
    }

    /* Bottom Section: Search & Previously Used */
    .bottom-content {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      width: 90%;
      text-align: center;
      z-index: 10;
    }
    .search-box {
      width: 100%;
      padding: 12px 16px;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      outline: none;
      background: rgba(50, 50, 50, 0.8);
      color: #fff;
      transition: background 0.3s;
    }
    .search-box::placeholder {
      color: #ddd;
    }
    #search-results {
      margin-top: 8px;
      max-height: 150px;
      overflow-y: auto;
    }
    .result-item {
      padding: 12px 16px;
      margin: 4px 0;
      background: rgba(30, 30, 30, 0.9);
      color: #fff;
      border-radius: 6px;
      cursor: pointer;
      transition: background 0.3s;
    }
    .result-item:hover {
      background: rgba(50, 50, 50, 0.9);
    }
    .previously-used {
      margin-top: 15px;
      background: rgba(50, 50, 50, 0.8);
      color: #fff;
      padding: 12px 20px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
      transition: background 0.3s, transform 0.2s;
      width: 100%;
    }
    .previously-used:hover {
      background: rgba(50, 50, 50, 1);
      transform: translateY(-2px);
    }
    #prev-dropdown {
      background: rgba(30, 30, 30, 0.9);
      border-radius: 6px;
      margin-top: 5px;
      max-height: 150px;
      overflow-y: auto;
      display: none;
      text-align: left;
    }
    .prev-item {
      padding: 12px 16px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);
      cursor: pointer;
      transition: background 0.3s;
      color: #fff;
    }
    .prev-item:last-child {
      border-bottom: none;
    }
    .prev-item:hover {
      background: rgba(50, 50, 50, 0.9);
    }

    /* Checklist Panel */
    .checklist-panel {
      position: fixed;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%) translateY(100%);
      width: 90%;
      max-width: 400px;
      max-height: 60%;
      background: rgba(0, 0, 0, 0.85);
      color: #fff;
      border-radius: 10px 10px 0 0;
      z-index: 20;
      transition: transform 0.3s ease-out;
      display: flex;
      flex-direction: column;
    }
    .checklist-panel.open {
      transform: translateX(-50%) translateY(0);
    }
    /* Revised header with three sections: left (plane name), center (timer), right (Done button) */
    .checklist-header {
      padding: 15px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.2);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .header-left h2 {
      font-size: 20px;
    }
    .header-center {
      font-size: 18px;
      color: #fff;
    }
    .checklist-items {
      overflow-y: auto;
      padding: 15px;
      /* Show roughly three items at a time */
      max-height: 200px;
    }
    .checklist-items ul {
      list-style: none;
    }
    .checklist-items li {
      display: flex;
      align-items: center;
      margin-bottom: 10px;
      font-size: 18px;
      background: rgba(50, 50, 50, 0.8);
      padding: 10px;
      border-radius: 6px;
    }
    .checklist-items li input[type="checkbox"] {
      margin-right: 10px;
      transform: scale(1.2);
    }

    /* Review Panel (Confirm Stage) – checkboxes remain active */
    .review-panel {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) scale(0.8);
      width: 90%;
      max-width: 400px;
      background: rgba(0, 0, 0, 0.9);
      color: #fff;
      border-radius: 10px;
      z-index: 40;
      padding: 20px;
      display: none;
      transition: transform 0.3s ease-out, opacity 0.3s ease-out;
      opacity: 0;
    }
    .review-panel.open {
      display: block;
      transform: translate(-50%, -50%) scale(1);
      opacity: 1;
    }
    .review-panel h2 {
      margin-bottom: 10px;
      text-align: center;
    }
    .review-panel ul {
      list-style: none;
      max-height: 300px;
      overflow-y: auto;
      margin-bottom: 20px;
    }
    .review-panel li {
      display: flex;
      align-items: center;
      margin-bottom: 10px;
      background: rgba(50, 50, 50, 0.8);
      padding: 10px;
      border-radius: 6px;
      font-size: 18px;
    }
    .review-panel li input[type="checkbox"] {
      margin-right: 10px;
      transform: scale(1.2);
    }

    /* Reports Modal (My Info) */
    .modal {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0, 0, 0, 0.8);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 50;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.3s;
    }
    .modal.open {
      opacity: 1;
      pointer-events: auto;
    }
    .modal-content {
      background: #222;
      padding: 20px;
      border-radius: 8px;
      width: 90%;
      max-width: 500px;
      max-height: 80%;
      overflow-y: auto;
    }
    .modal-content h2 {
      margin-bottom: 10px;
      color: #fff;
    }
    .modal-content ul {
      list-style: none;
      padding: 0;
    }
    .modal-content li {
      padding: 8px;
      border-bottom: 1px solid #444;
      color: #fff;
    }
  </style>
</head>
<body>
  <!-- Camera Background -->
  <video id="video-background" autoplay playsinline></video>

  <!-- Home Button (shown when checklist is active) -->
  <button id="home-btn" class="button">🏠 Home</button>

  <!-- Main UI Container (Search Interface) -->
  <div class="container" id="main-ui">
    <!-- Top Bar with Translucent Background -->
    <div class="top-buttons">
      <button id="my-info-btn" class="button">📄 My Info</button>
      <button class="button">⚙️ Settings</button>
    </div>

    <!-- Bottom Section: Search & Previously Used -->
    <div class="bottom-content">
      <input type="text" id="search-box" class="search-box" placeholder="Search Planes" />
      <div id="search-results"></div>
      <button class="previously-used" id="prev-used-btn">Previously Used</button>
      <div id="prev-dropdown"></div>
    </div>
  </div>

  <!-- Checklist Panel -->
  <div class="checklist-panel" id="checklist-panel">
    <div class="checklist-header">
      <div class="header-left"><h2 id="plane-name">Plane Name</h2></div>
      <div class="header-center"><span id="timer">00:00</span></div>
      <div class="header-right"><button id="done-btn" class="button">Done</button></div>
    </div>
    <div class="checklist-items">
      <ul id="checklist"></ul>
    </div>
  </div>

  <!-- Review Panel (Confirm Stage) -->
  <div class="review-panel" id="review-panel">
    <h2 id="review-plane-name">Review Checklist</h2>
    <ul id="review-checklist"></ul>
    <button id="confirm-btn" class="button">Confirm</button>
  </div>

  <!-- Reports Modal (My Info) -->
  <div id="reports-modal" class="modal">
    <div class="modal-content">
      <h2>Reports</h2>
      <ul id="reports-list"></ul>
      <button id="close-reports" class="button">Close</button>
    </div>
  </div>

  <script>
    // ================= Global Variables =================
    let currentChecklist = [];
    let timerInterval = null;
    let startTime = null;
    let elapsedTime = 0;
    let reports = [];
    const genericChecklist = [
      "Walk around fuselage",
      "Inspect engines",
      "Check control surfaces",
      "Examine landing gear",
      "Review instruments",
      "Test lights and signals"
    ];
    const availablePlanes = [
      "Boeing 737",
      "Airbus A320",
      "Cessna 172",
      "Beechcraft King Air",
      "Embraer E-Jet",
      "Boeing 747",
      "Airbus A380"
    ];

    // =============== Timer Functions ===============
    function formatTime(seconds) {
      let mins = Math.floor(seconds / 60);
      let secs = seconds % 60;
      return (mins < 10 ? "0" + mins : mins) + ":" + (secs < 10 ? "0" + secs : secs);
    }
    function startTimer() {
      startTime = Date.now();
      timerInterval = setInterval(updateTimer, 1000);
    }
    function updateTimer() {
      elapsedTime = Math.floor((Date.now() - startTime) / 1000);
      document.getElementById("timer").textContent = formatTime(elapsedTime);
    }
    function stopTimer() {
      clearInterval(timerInterval);
      timerInterval = null;
    }

    // ============== Search & Previously Used ==============
    const searchBox = document.getElementById("search-box");
    const searchResults = document.getElementById("search-results");
    const prevUsedBtn = document.getElementById("prev-used-btn");
    const prevDropdown = document.getElementById("prev-dropdown");
    let lastSearchedPlanes = [];

    searchBox.addEventListener("input", function () {
      const query = this.value.trim().toLowerCase();
      searchResults.innerHTML = "";
      if (query === "") return;
      const filtered = availablePlanes.filter((plane) =>
        plane.toLowerCase().includes(query)
      );
      filtered.forEach((plane) => {
        const div = document.createElement("div");
        div.className = "result-item";
        div.textContent = plane;
        div.addEventListener("click", () => {
          showChecklist(plane);
          searchBox.value = "";
          searchResults.innerHTML = "";
        });
        searchResults.appendChild(div);
      });
    });

    prevUsedBtn.addEventListener("click", function () {
      if (prevDropdown.style.display === "block") {
        prevDropdown.style.display = "none";
      } else {
        updatePrevDropdown();
        prevDropdown.style.display = "block";
      }
    });

    function updatePrevDropdown() {
      prevDropdown.innerHTML = "";
      lastSearchedPlanes.slice().reverse().forEach((plane) => {
        const div = document.createElement("div");
        div.className = "prev-item";
        div.textContent = plane;
        div.addEventListener("click", () => {
          showChecklist(plane);
          prevDropdown.style.display = "none";
        });
        prevDropdown.appendChild(div);
      });
    }

    // ============== Checklist Functions ==============
    function showChecklist(plane) {
      // Update "Previously Used" list
      if (!lastSearchedPlanes.includes(plane)) {
        lastSearchedPlanes.push(plane);
        if (lastSearchedPlanes.length > 3) {
          lastSearchedPlanes.shift();
        }
      } else {
        lastSearchedPlanes = lastSearchedPlanes.filter((p) => p !== plane);
        lastSearchedPlanes.push(plane);
      }
      // Set plane name and initialize checklist data
      document.getElementById("plane-name").textContent = plane;
      currentChecklist = genericChecklist.map((item, idx) => {
        return { index: idx, text: item, checked: false, time: null };
      });
      // Populate checklist panel
      const checklistUl = document.getElementById("checklist");
      checklistUl.innerHTML = "";
      currentChecklist.forEach((item, idx) => {
        const li = document.createElement("li");
        const checkbox = document.createElement("input");
        checkbox.type = "checkbox";
        checkbox.setAttribute("data-index", idx);
        const label = document.createElement("label");
        label.textContent = item.text;
        li.appendChild(checkbox);
        li.appendChild(label);
        checklistUl.appendChild(li);
        checkbox.addEventListener("change", function () {
          let i = this.getAttribute("data-index");
          currentChecklist[i].checked = this.checked;
          if (this.checked) {
            currentChecklist[i].time = elapsedTime;
          } else {
            currentChecklist[i].time = null;
          }
        });
      });
      // Hide main UI, show home button and checklist panel, then start timer
      document.getElementById("main-ui").style.display = "none";
      document.getElementById("home-btn").style.display = "block";
      document.getElementById("checklist-panel").classList.add("open");
      elapsedTime = 0;
      document.getElementById("timer").textContent = "00:00";
      startTimer();
    }

    document.getElementById("done-btn").addEventListener("click", function () {
      // Transition to review panel (confirm stage)
      renderReviewPanel();
      document.getElementById("checklist-panel").classList.remove("open");
      document.getElementById("review-panel").classList.add("open");
    });

    function renderReviewPanel() {
      const reviewChecklistUl = document.getElementById("review-checklist");
      reviewChecklistUl.innerHTML = "";
      // Sort so that unchecked items come first
      let sortedChecklist = currentChecklist.slice().sort((a, b) => {
        return (a.checked === b.checked) ? 0 : a.checked ? 1 : -1;
      });
      sortedChecklist.forEach(item => {
        const li = document.createElement("li");
        const checkbox = document.createElement("input");
        checkbox.type = "checkbox";
        checkbox.checked = item.checked;
        checkbox.setAttribute("data-index", item.index);
        const label = document.createElement("label");
        label.textContent =
          item.text + (item.checked && item.time !== null ? " (" + formatTime(item.time) + ")" : "");
        li.appendChild(checkbox);
        li.appendChild(label);
        reviewChecklistUl.appendChild(li);
        checkbox.addEventListener("change", function () {
          let idx = this.getAttribute("data-index");
          currentChecklist[idx].checked = this.checked;
          if (this.checked) {
            currentChecklist[idx].time = elapsedTime;
          } else {
            currentChecklist[idx].time = null;
          }
          renderReviewPanel(); // re-render to update sorting and times
        });
      });
      document.getElementById("review-plane-name").textContent =
        "Review Checklist for " + document.getElementById("plane-name").textContent;
    }

    document.getElementById("confirm-btn").addEventListener("click", function () {
      stopTimer();
      // Generate report with final checklist state
      let report = {
        plane: document.getElementById("plane-name").textContent,
        totalTime: formatTime(elapsedTime),
        items: currentChecklist.map(item => {
          return {
            text: item.text,
            checked: item.checked,
            time: item.time !== null ? formatTime(item.time) : "Not checked"
          };
        }),
        date: new Date().toLocaleString()
      };
      reports.push(report);
      // Hide review panel and return to home screen
      document.getElementById("review-panel").classList.remove("open");
      document.getElementById("checklist-panel").classList.remove("open");
      document.getElementById("main-ui").style.display = "flex";
      document.getElementById("home-btn").style.display = "none";
    });

    // Home button (cancel checklist) returns to main screen
    document.getElementById("home-btn").addEventListener("click", function () {
      stopTimer();
      document.getElementById("checklist-panel").classList.remove("open");
      document.getElementById("review-panel").classList.remove("open");
      document.getElementById("main-ui").style.display = "flex";
      document.getElementById("home-btn").style.display = "none";
    });

    // ============== Reports Modal (My Info) ==============
    document.getElementById("my-info-btn").addEventListener("click", function (e) {
      e.stopPropagation();
      populateReports();
      document.getElementById("reports-modal").classList.add("open");
    });
    document.getElementById("close-reports").addEventListener("click", function () {
      document.getElementById("reports-modal").classList.remove("open");
    });
    function populateReports() {
      const reportsList = document.getElementById("reports-list");
      reportsList.innerHTML = "";
      reports.forEach((report, idx) => {
        const li = document.createElement("li");
        li.innerHTML =
          "<strong>" +
          report.plane +
          "</strong> - " +
          report.date +
          " (Total Time: " +
          report.totalTime +
          ")";
        const ul = document.createElement("ul");
        report.items.forEach(item => {
          const itemLi = document.createElement("li");
          itemLi.textContent = item.text + ": " + item.time;
          ul.appendChild(itemLi);
        });
        li.appendChild(ul);
        reportsList.appendChild(li);
      });
    }

    // Hide Previously Used dropdown if clicking outside
    document.addEventListener("click", function (event) {
      if (!prevUsedBtn.contains(event.target) && !prevDropdown.contains(event.target)) {
        prevDropdown.style.display = "none";
      }
    });

    // ============== Start Camera ==============
    async function startCamera() {
      try {
        const stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: "environment" } });
        document.getElementById("video-background").srcObject = stream;
      } catch (error) {
        console.error("Error accessing camera:", error);
      }
    }
    startCamera();
  </script>
</body>
</html>
