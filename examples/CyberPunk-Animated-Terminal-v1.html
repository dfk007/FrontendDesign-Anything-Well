<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Development Checklist</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;700&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
  <style>
    :root {
      --neon-green:       #00ff41;
      --neon-cyan:        #00d9ff;
      --neon-pink:        #ff00ff;
      --dark-bg:          #0a0e1a;
      --darker-bg:        #050810;
      --terminal-bg:      #0d1117;
      --border-glow:      rgba(0, 255, 65, 0.3);
      --text-bright:      #ffffff;
      --text-dim:         #8b949e;
      --warning-red:      #ff4757;
      --success-green:    #2ed573;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }
    html, body { scroll-behavior: smooth; overflow-x: hidden; }

    body {
      background: var(--dark-bg);
      font-family: 'Fira Code', monospace;
      font-size: 0.95rem;
      line-height: 1.7;
      color: var(--text-dim);
      position: relative;
      z-index: 2;
    }

    body::before {
      content: '';
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background-image:
        linear-gradient(rgba(0, 255, 65, 0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0, 255, 65, 0.03) 1px, transparent 1px);
      background-size: 50px 50px;
      animation: gridScroll 20s linear infinite;
      pointer-events: none;
      z-index: -1;
    }

    @keyframes gridScroll {
      0%   { transform: translateY(0); }
      100% { transform: translateY(50px); }
    }

    @keyframes slideDown {
      from { transform: translateY(-100%); opacity: 0; }
      to   { transform: translateY(0); opacity: 1; }
    }

    @keyframes glow {
      from { text-shadow: 0 0 10px var(--neon-cyan), 0 0 20px var(--neon-cyan); }
      to   { text-shadow: 0 0 20px var(--neon-cyan), 0 0 40px var(--neon-cyan), 0 0 60px rgba(0, 217, 255, 0.8); }
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    @keyframes borderScan {
      0%   { transform: translateX(-100%); }
      100% { transform: translateX(100%); }
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50%      { transform: scale(1.05); }
    }

    ::-webkit-scrollbar { width: 12px; height: 12px; }
    ::-webkit-scrollbar-track { background: var(--darker-bg); }
    ::-webkit-scrollbar-thumb {
      background: var(--neon-green);
      border-radius: 6px;
      box-shadow: 0 0 10px var(--neon-green);
    }
    ::-webkit-scrollbar-thumb:hover { background: var(--neon-cyan); }

    header {
      background: linear-gradient(135deg, var(--darker-bg) 0%, var(--terminal-bg) 100%);
      border-bottom: 2px solid var(--neon-green);
      box-shadow: 0 4px 20px rgba(0, 255, 65, 0.2);
      padding: 2rem;
      text-align: center;
      position: sticky;
      top: 0;
      z-index: 100;
      animation: slideDown 0.6s ease-out;
    }

    header h1 {
      font-family: 'Orbitron', sans-serif;
      font-size: 2.8rem;
      font-weight: 900;
      text-transform: uppercase;
      letter-spacing: 4px;
      color: var(--neon-cyan);
      animation: glow 2s ease-in-out infinite alternate;
      line-height: 1.1;
    }

    .subtitle {
      color: var(--text-dim);
      font-size: 0.95rem;
      letter-spacing: 2px;
      margin-top: 0.5rem;
    }

    .subtitle span {
      color: var(--neon-green);
      font-weight: 700;
    }

    .container {
      max-width: 1400px;
      margin: 0 auto;
      padding: 2rem;
    }

    .meta-bar {
      display: flex;
      flex-wrap: wrap;
      gap: 0;
      margin: 2rem 0;
      border: 1px solid var(--border-glow);
      border-radius: 8px;
      overflow: hidden;
    }

    .meta-cell {
      flex: 1;
      min-width: 140px;
      padding: 1rem 1.25rem;
      border-right: 1px solid var(--border-glow);
      background: linear-gradient(135deg, var(--terminal-bg) 0%, var(--darker-bg) 100%);
      position: relative;
      overflow: hidden;
    }

    .meta-cell::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 3px;
      background: linear-gradient(90deg, var(--neon-green), var(--neon-cyan), var(--neon-pink));
      animation: borderScan 3s linear infinite;
    }

    .meta-cell:last-child { border-right: none; }

    .meta-cell .label {
      text-transform: uppercase;
      color: var(--text-dim);
      font-size: 0.65rem;
      letter-spacing: 1px;
      display: block;
      margin-bottom: 0.35rem;
    }

    .meta-cell .val {
      font-family: 'Orbitron', sans-serif;
      font-size: 1.6rem;
      font-weight: 700;
      color: var(--neon-green);
      text-shadow: 0 0 10px rgba(0, 255, 65, 0.5);
    }

    .layout {
      display: grid;
      grid-template-columns: 200px 1fr;
      gap: 2.5rem;
    }

    .sidebar {
      position: sticky;
      top: 8rem;
      align-self: start;
    }

    .sidebar-heading {
      font-family: 'Orbitron', sans-serif;
      font-size: 0.75rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 2px;
      color: var(--neon-cyan);
      margin-bottom: 1rem;
    }

    .sidebar-nav-item {
      padding: 0.6rem 0.75rem;
      margin-bottom: 0.5rem;
      font-family: 'Fira Code', monospace;
      font-size: 0.85rem;
      font-weight: 500;
      text-transform: uppercase;
      letter-spacing: 1px;
      cursor: pointer;
      transition: all 0.3s ease;
      border-left: 3px solid transparent;
      color: var(--text-dim);
    }

    .sidebar-nav-item::before {
      content: '> ';
      color: var(--neon-green);
      opacity: 0;
      transition: opacity 0.3s ease;
    }

    .sidebar-nav-item:hover {
      color: var(--neon-cyan);
      border-left-color: var(--neon-cyan);
      box-shadow: 0 0 10px rgba(0, 217, 255, 0.2);
      background: rgba(0, 217, 255, 0.05);
    }

    .sidebar-nav-item:hover::before { opacity: 1; }

    .sidebar-nav-item.active {
      border-left-color: var(--neon-green);
      color: var(--neon-green);
      background: rgba(0, 255, 65, 0.08);
      box-shadow: 0 0 15px rgba(0, 255, 65, 0.2);
    }

    .sidebar-nav-item.active::before { opacity: 1; }

    .sidebar-section {
      margin-top: 2rem;
    }

    .sidebar-section-title {
      font-family: 'Fira Code', monospace;
      font-size: 0.65rem;
      color: var(--text-dim);
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-bottom: 0.75rem;
    }

    .status-indicator {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      margin-bottom: 0.5rem;
    }

    .status-dot {
      width: 12px;
      height: 12px;
      border-radius: 50%;
      border: 1px solid var(--border-glow);
    }

    .status-dot.pending { background: var(--neon-pink); box-shadow: 0 0 6px rgba(255, 0, 255, 0.5); }
    .status-dot.complete { background: var(--success-green); box-shadow: 0 0 6px rgba(46, 213, 115, 0.5); }

    .status-indicator span {
      font-size: 0.7rem;
      color: var(--text-dim);
    }

    .card {
      background: linear-gradient(135deg, var(--terminal-bg) 0%, var(--darker-bg) 100%);
      border: 1px solid var(--border-glow);
      border-radius: 8px;
      padding: 2rem;
      position: relative;
      overflow: hidden;
    }

    .card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 3px;
      background: linear-gradient(90deg, var(--neon-green), var(--neon-cyan), var(--neon-pink));
      animation: borderScan 3s linear infinite;
    }

    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid var(--border-glow);
      padding-bottom: 1rem;
      margin-bottom: 1.5rem;
    }

    .card-header h2 {
      font-family: 'Orbitron', sans-serif;
      font-size: 1.8rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 2px;
      color: var(--neon-cyan);
    }

    .stats-display {
      background: rgba(0, 0, 0, 0.5);
      border: 1px solid var(--border-glow);
      border-radius: 4px;
      padding: 0.5rem 1rem;
      font-family: 'Fira Code', monospace;
      font-size: 0.75rem;
      color: var(--neon-green);
      letter-spacing: 1px;
    }

    .checklist {
      list-style: none;
      margin-left: 0;
    }

    .checklist li {
      padding: 0.75rem 0 0.75rem 2rem;
      position: relative;
      border-bottom: 1px solid rgba(0, 255, 65, 0.08);
      transition: all 0.3s ease;
      animation: fadeIn 0.5s forwards;
      opacity: 0;
    }

    .checklist li::before {
      content: '✕';
      position: absolute;
      left: 0;
      top: 0.75rem;
      color: var(--neon-pink);
      font-family: 'Fira Code', monospace;
      font-weight: 700;
      font-size: 0.9rem;
    }

    .checklist li:hover {
      background: rgba(0, 255, 65, 0.03);
      box-shadow: inset 0 0 20px rgba(0, 255, 65, 0.03);
    }

    .checklist li.done {
      opacity: 0.7;
    }

    .checklist li.done::before {
      content: '✓';
      color: var(--success-green);
      text-shadow: 0 0 8px rgba(46, 213, 115, 0.5);
    }

    .checklist li.done label {
      text-decoration: line-through;
      color: var(--text-dim);
    }

    .checklist input[type="checkbox"] {
      position: absolute;
      left: -9999px;
    }

    .checklist label {
      cursor: pointer;
      display: inline-block;
      font-size: 0.95rem;
      color: var(--neon-green);
      transition: color 0.3s ease;
    }

    .checklist label:hover {
      color: var(--neon-cyan);
      text-shadow: 0 0 8px rgba(0, 217, 255, 0.3);
    }

    .checklist input[type="checkbox"]:checked ~ label {
      color: var(--text-dim);
    }

    .badge {
      display: inline-block;
      padding: 0.3rem 0.8rem;
      border-radius: 20px;
      font-size: 0.75rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-left: 0.75rem;
      font-family: 'Fira Code', monospace;
    }

    .badge-pending {
      background: rgba(255, 0, 255, 0.2);
      color: var(--neon-pink);
      border: 1px solid var(--neon-pink);
    }

    .badge-done {
      background: rgba(46, 213, 115, 0.2);
      color: var(--success-green);
      border: 1px solid var(--success-green);
    }

    .add-task-card {
      margin-top: 2rem;
      background: linear-gradient(135deg, var(--terminal-bg) 0%, var(--darker-bg) 100%);
      border: 1px solid var(--border-glow);
      border-radius: 8px;
      padding: 1.5rem;
      position: relative;
      overflow: hidden;
    }

    .add-task-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 3px;
      background: linear-gradient(90deg, var(--neon-green), var(--neon-cyan), var(--neon-pink));
      animation: borderScan 3s linear infinite;
    }

    .add-task-header {
      border-bottom: 1px solid var(--border-glow);
      padding-bottom: 1rem;
      margin-bottom: 1rem;
    }

    .add-task-header h3 {
      font-family: 'Fira Code', monospace;
      font-size: 1.3rem;
      font-weight: 700;
      color: var(--neon-green);
    }

    .add-task-form {
      display: flex;
      gap: 1rem;
      align-items: center;
    }

    .add-task-form input[type="text"] {
      flex: 1;
      padding: 0.75rem 1rem;
      background: #000;
      border: 1px solid var(--border-glow);
      border-radius: 4px;
      font-family: 'Fira Code', monospace;
      font-size: 0.95rem;
      color: var(--neon-green);
      box-shadow: inset 0 0 10px rgba(0, 255, 65, 0.05);
      transition: all 0.3s ease;
    }

    .add-task-form input[type="text"]::placeholder {
      color: var(--text-dim);
      opacity: 0.6;
    }

    .add-task-form input[type="text"]:focus {
      outline: none;
      border-color: var(--neon-green);
      box-shadow: 0 0 15px rgba(0, 255, 65, 0.3), inset 0 0 10px rgba(0, 255, 65, 0.05);
    }

    .btn-primary {
      padding: 0.75rem 1.5rem;
      background: linear-gradient(135deg, rgba(0, 255, 65, 0.2) 0%, rgba(0, 217, 255, 0.2) 100%);
      color: var(--neon-green);
      border: 1px solid var(--neon-green);
      border-radius: 4px;
      font-family: 'Fira Code', monospace;
      font-size: 0.85rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 1px;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 0 10px rgba(0, 255, 65, 0.2);
    }

    .btn-primary:hover {
      background: linear-gradient(135deg, rgba(0, 255, 65, 0.3) 0%, rgba(0, 217, 255, 0.3) 100%);
      box-shadow: 0 0 20px rgba(0, 255, 65, 0.4);
      color: var(--text-bright);
    }

    .btn-primary:active {
      transform: scale(0.97);
    }

    .task-message {
      margin-top: 0.75rem;
      font-size: 0.85rem;
      font-family: 'Fira Code', monospace;
      height: 1.2rem;
    }

    .task-message.success { color: var(--success-green); text-shadow: 0 0 8px rgba(46, 213, 115, 0.4); }
    .task-message.error { color: var(--warning-red); text-shadow: 0 0 8px rgba(255, 71, 87, 0.4); }

    .terminal {
      background: #000;
      border: 2px solid var(--neon-green);
      border-radius: 6px;
      padding: 1.5rem;
      margin: 1.5rem 0;
      font-family: 'Fira Code', monospace;
      font-size: 0.9rem;
      overflow-x: auto;
      box-shadow:
        0 0 20px rgba(0, 255, 65, 0.2),
        inset 0 0 30px rgba(0, 255, 65, 0.05);
      position: relative;
    }

    .terminal::before {
      content: '● ● ●';
      position: absolute;
      top: -25px; left: 10px;
      color: var(--text-dim);
      font-size: 1.2rem;
      letter-spacing: 8px;
    }

    .terminal pre {
      margin: 0;
      color: var(--neon-green);
      white-space: pre-wrap;
      word-wrap: break-word;
    }

    .terminal .prompt  { color: var(--neon-cyan); font-weight: 700; }
    .terminal .comment  { color: #6a737d; font-style: italic; }
    .terminal .output   { color: var(--success-green); }
    .terminal .warning  { color: var(--warning-red); }

    footer {
      text-align: center;
      padding: 3rem 2rem;
      margin-top: 4rem;
      border-top: 2px solid var(--border-glow);
      color: var(--text-dim);
      font-size: 0.9rem;
    }

    footer a {
      color: var(--neon-cyan);
      text-decoration: none;
      transition: color 0.3s ease;
    }

    footer a:hover {
      color: var(--neon-green);
      text-shadow: 0 0 10px var(--neon-green);
    }

    .footer-brand {
      font-family: 'Orbitron', sans-serif;
      font-weight: 700;
      color: var(--neon-green);
      text-shadow: 0 0 10px rgba(0, 255, 65, 0.4);
    }

    @media (max-width: 768px) {
      header h1 { font-size: 2rem; }
      .layout { grid-template-columns: 1fr; }
      .sidebar { position: static; margin-bottom: 1.5rem; }
      .meta-cell { border-bottom: 1px solid var(--border-glow); }
      .card { padding: 1.5rem; }
      .add-task-form { flex-direction: column; }
      .add-task-form input[type="text"] { width: 100%; }
    }

    .block:nth-child(1) { animation-delay: 0.05s; }
    .block:nth-child(2) { animation-delay: 0.15s; }
    .block:nth-child(3) { animation-delay: 0.25s; }
    .block:nth-child(4) { animation-delay: 0.35s; }
    .block:nth-child(5) { animation-delay: 0.45s; }
    .block:nth-child(6) { animation-delay: 0.55s; }
    .block:nth-child(7) { animation-delay: 0.65s; }
    .block:nth-child(8) { animation-delay: 0.75s; }
  </style>
</head>
<body>
  <header>
    <h1>Task Management System</h1>
    <p class="subtitle">// Development Checklist <span>v2026.06</span></p>
  </header>

  <div class="container">
    <div class="meta-bar">
      <div class="meta-cell">
        <div class="label">Total Tasks</div>
        <div class="val" id="total-count">5</div>
      </div>
      <div class="meta-cell">
        <div class="label">Completed</div>
        <div class="val" id="completed-count">1</div>
      </div>
      <div class="meta-cell">
        <div class="label">Progress</div>
        <div class="val" id="progress-percent">20%</div>
      </div>
      <div class="meta-cell">
        <div class="label">Last Updated</div>
        <div class="val" id="last-updated" style="font-size:1rem;">Jun 15, 2026</div>
      </div>
    </div>

    <div class="layout">
      <aside class="sidebar">
        <div class="sidebar-heading">Navigation</div>
        <div class="sidebar-nav-item active">Dashboard</div>
        <div class="sidebar-nav-item">Tasks</div>
        <div class="sidebar-nav-item">Progress</div>

        <div class="sidebar-section">
          <div class="sidebar-section-title">Status Codes</div>
          <div class="status-indicator">
            <div class="status-dot pending"></div>
            <span>Pending</span>
          </div>
          <div class="status-indicator">
            <div class="status-dot complete"></div>
            <span>Complete</span>
          </div>
        </div>

        <div class="sidebar-section">
          <div style="background:#000; border:2px solid var(--neon-green); border-radius:6px; padding:1rem; box-shadow: 0 0 20px rgba(0,255,65,0.2), inset 0 0 30px rgba(0,255,65,0.05); position:relative; margin-top:1rem;">
            <div style="position:absolute; top:-25px; left:10px; color:var(--text-dim); font-size:1.2rem; letter-spacing:8px;">● ● ●</div>
            <pre style="margin:0; color:var(--neon-green); white-space:pre-wrap; font-family:'Fira Code',monospace; font-size:0.75rem; line-height:1.6;"><span class="prompt">$</span> sys.status
<span class="output">● system online</span>
<span class="comment">// uptime: 100%</span></pre>
          </div>
        </div>
      </aside>

      <main>
        <div class="card">
          <div class="card-header">
            <h2>Task List</h2>
            <div class="stats-display">
              <span id="stats-text">1 of 5 tasks completed</span>
            </div>
          </div>

          <ul class="checklist" id="taskList">
          </ul>

          <div class="add-task-card">
            <div class="add-task-header">
              <h3>+ Add New Task</h3>
            </div>
            <div class="add-task-form">
              <input type="text" id="newTaskInput" placeholder="Enter new task...">
              <button class="btn-primary" id="addTaskBtn">Add Task</button>
            </div>
            <div class="task-message" id="addTaskMessage"></div>
          </div>
        </div>
      </main>
    </div>

    <footer>
      <p><span class="footer-brand">Ai-Point-of-Sale-Software</span> &mdash; Cyberpunk Task System &copy; 2026</p>
    </footer>
  </div>

  <script>
    const tasks = [
      { name: "Task 1: Fix Logout on Frontend Refresh", done: true },
      { name: "Task 2: Fix RBAC — Admin Role Gets Full Access", done: false },
      { name: "Task 3: Add RBAC Role Definitions (Manager & Cashier)", done: false },
      { name: "Task 4: Fix Product Not Appearing After Creation", done: false },
      { name: "Task 6: Fix Product Creation IntegrityError — Handle DB Constraint Violations in API", done: false },
      { name: "Task 5: Final Integration Verification", done: false },
    ];

    const saved = localStorage.getItem("todo-checklist-state");
    if (saved) {
      const parsed = JSON.parse(saved);
      tasks.forEach((t, i) => { if (parsed[i] !== undefined) t.done = parsed[i]; });
    }

    function updateStats() {
      const doneCount = tasks.filter(t => t.done).length;
      const totalCount = tasks.length;
      const progressPercent = Math.round((doneCount / totalCount) * 100);

      document.getElementById("stats-text").textContent = `${doneCount} of ${totalCount} tasks completed`;
      document.getElementById("completed-count").textContent = doneCount;
      document.getElementById("progress-percent").textContent = `${progressPercent}%`;
      document.getElementById("total-count").textContent = totalCount;
    }

    function render() {
      const list = document.getElementById("taskList");
      list.innerHTML = "";

      tasks.forEach((task, i) => {
        const li = document.createElement("li");
        li.className = "block";
        if (task.done) li.classList.add("done");

        li.innerHTML = `
          <input type="checkbox" id="task${i}" ${task.done ? "checked" : ""}>
          <label for="task${i}">${task.name}</label>
          <span class="badge ${task.done ? 'badge-done' : 'badge-pending'}">${task.done ? 'Complete' : 'Pending'}</span>
        `;

        li.querySelector("input").addEventListener("change", () => {
          tasks[i].done = !tasks[i].done;
          localStorage.setItem("todo-checklist-state", JSON.stringify(tasks.map(t => t.done)));
          render();
          updateStats();
        });

        list.appendChild(li);
      });

      const newTaskInput = document.getElementById("newTaskInput");
      if (newTaskInput) {
        newTaskInput.value = "";
      }
    }

    const addTaskBtn = document.getElementById("addTaskBtn");
    const newTaskInput = document.getElementById("newTaskInput");
    const addTaskMessage = document.getElementById("addTaskMessage");

    if (addTaskBtn && newTaskInput) {
      addTaskBtn.addEventListener("click", function() {
        const taskText = newTaskInput.value.trim();

        if (taskText === "") {
          addTaskMessage.textContent = "Please enter a task name";
          addTaskMessage.className = "task-message error";
          return;
        }

        const newTask = { name: taskText, done: false };
        tasks.push(newTask);

        localStorage.setItem("todo-checklist-state", JSON.stringify(tasks.map(t => t.done)));

        render();
        updateStats();

        addTaskMessage.textContent = "Task added successfully!";
        addTaskMessage.className = "task-message success";

        newTaskInput.value = "";
        setTimeout(() => {
          addTaskMessage.textContent = "";
          addTaskMessage.className = "task-message";
        }, 3000);
      });

      if (newTaskInput) {
        newTaskInput.addEventListener("keypress", function(e) {
          if (e.key === "Enter") {
            addTaskBtn.click();
          }
        });
      }
    }

    updateStats();
    render();
  </script>
</body>
</html>
