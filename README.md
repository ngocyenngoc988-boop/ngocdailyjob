<!doctype html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Daily Job</title>
  <meta name="description" content="Daily Job - Quản lý việc cần làm, tiến độ chương trình và tài liệu" />
  <style>
    :root{
      --blue:#0ea5e9;
      --deep-blue:#0369a1;
      --accent:#ff7a00;
      --card:#ffffff;
      --muted:#667085;
      --radius:14px;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }

    *{box-sizing:border-box}
    html,body{height:100%;margin:0;background:#f0f4f8;}

    .app-wrap{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:28px}
    .container{width:100%;max-width:1000px;background:rgba(255,255,255,0.95);backdrop-filter: blur(6px);border-radius:var(--radius);box-shadow:0 8px 30px rgba(2,6,23,0.15);overflow:hidden}

    header.top{display:flex;align-items:center;justify-content:space-between;padding:22px 24px;background:rgba(3,105,161,0.08);}
    .brand{display:flex;gap:14px;align-items:center}
    .logo{width:56px;height:56px;border-radius:12px;background:var(--deep-blue);display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700;font-size:28px}
    .logo svg{width:36px;height:36px;}
    h1{margin:0;font-size:20px}
    p.sub{margin:0;color:var(--muted);font-size:13px}

    nav{display:flex;gap:10px}
    nav button{background:transparent;border:0;padding:8px 12px;border-radius:10px;font-weight:600;cursor:pointer}
    nav button.active{background:rgba(3,105,161,0.08);color:var(--deep-blue)}

    .body{display:flex;gap:24px;padding:22px}
    .main{flex:1;min-height:420px}
    .sidebar{width:280px}

    section.card{background:var(--card);border-radius:12px;padding:16px;box-shadow:0 6px 18px rgba(12,18,40,0.04);}
    .card + .card{margin-top:16px}

    .hero{display:flex;gap:18px;align-items:center}
    .hero-left{flex:1}
    .hero-right{width:180px;height:180px;border-radius:12px;background:linear-gradient(180deg,rgba(2,6,23,0.06),transparent);display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:8px;}
    .decor-icons{position:absolute;top:10px;left:10px;right:10px;bottom:10px;pointer-events:none;opacity:0.15;}

    .todo-controls{display:flex;gap:8px;margin-bottom:12px}
    .input, .small-input{padding:10px;border-radius:10px;border:1px solid #e6eef5;width:100%;}
    .btn{padding:10px 12px;border-radius:10px;border:0;background:var(--deep-blue);color:#fff;cursor:pointer}
    .btn.ghost{background:transparent;color:var(--deep-blue);border:1px solid rgba(3,105,161,0.08)}
    ul.todo-list{list-style:none;margin:0;padding:0}
    ul.todo-list li{display:flex;align-items:center;gap:12px;padding:10px;border-radius:10px;border:1px solid #f3f7fb;margin-bottom:8px}
    .todo-text{flex:1}
    .todo-text.done{text-decoration:line-through;color:#94a3b8}

    .items{display:flex;flex-direction:column;gap:10px}
    .item-row{display:flex;justify-content:space-between;gap:12px;align-items:center;padding:10px;border-radius:10px;border:1px solid #f3f7fb}
    .item-row .meta{font-size:12px;color:var(--muted)}

    .footer{padding:16px;text-align:center;font-size:13px;color:var(--muted)}

    @media (max-width:880px){.body{flex-direction:column}.sidebar{width:100%}.hero-right{display:none}}
  </style>
</head>
<body>
  <div class="app-wrap">
    <div class="container">
      <header class="top">
        <div class="brand">
          <div class="logo">
            <!-- Sách SVG -->
            <svg viewBox="0 0 64 64" fill="white" xmlns="http://www.w3.org/2000/svg">
              <path d="M8 8h48v48H8V8zm4 4v40h40V12H12zm10 6h20v4H22v-4zm0 8h20v4H22v-4zm0 8h20v4H22v-4z"/>
            </svg>
          </div>
          <div>
            <h1>Daily Job</h1>
            <p class="sub">Quản lý việc cần làm · Tiến độ · Tài liệu</p>
          </div>
        </div>
        <nav>
          <button class="nav-btn active" data-tab="home">Trang chủ</button>
          <button class="nav-btn" data-tab="todo">Việc cần làm</button>
          <button class="nav-btn" data-tab="progress">Tiến độ chương trình</button>
          <button class="nav-btn" data-tab="docs">Tài liệu</button>
        </nav>
      </header>

      <div class="body">
        <main class="main">

          <!-- HOME -->
          <section id="home" class="card tab" style="position:relative;">
            <div class="decor-icons">📚 ✏️ 🖊️ 📖 ☕ 🌿</div>
            <h2>Đếm ngược đến 01/06/2026 ⏳</h2>
            <div style="font-size:24px;font-weight:700;" id="countdown">Loading...</div>
            <div style="margin-top:12px;font-style:italic;color:var(--muted);" id="dailyQuote">Loading quote...</div>
          </section>

          <!-- TODO -->
          <section id="todo" class="card tab" style="display:none">
            <h3>Việc cần làm (To‑Do) — reset mỗi ngày</h3>
            <div class="todo-controls">
              <input id="todoInput" class="input" placeholder="Thêm việc mới..." />
              <button id="addTodoBtn" class="btn">Thêm</button>
            </div>
            <div style="margin-bottom:12px;display:flex;gap:8px">
              <button id="resetTodayBtn" class="btn ghost">Reset hôm nay</button>
              <button id="clearDoneBtn" class="btn ghost">Xoá đã hoàn thành</button>
            </div>
            <ul id="todoList" class="todo-list"></ul>
          </section>

          <!-- PROGRESS -->
          <section id="progress" class="card tab" style="display:none">
            <h3>Tiến độ chương trình (lưu dài hạn)</h3>
            <div class="items">
              <div class="item-row"><strong>Toán</strong><div id="mathList"></div></div>
              <div class="item-row"><strong>Lý</strong><div id="physicsList"></div></div>
              <div class="item-row"><strong>Hóa</strong><div id="chemList"></div></div>
              <div class="item-row"><strong>Anh</strong><div id="engList"></div></div>
            </div>
            <div style="display:flex;gap:8px;margin-top:12px">
              <input id="progInput" class="input" placeholder="Thêm tiến độ/ghi chú..." />
              <select id="subjectSelect" class="input">
                <option value="math">Toán</option>
                <option value="physics">Lý</option>
                <option value="chem">Hóa</option>
                <option value="eng">Anh</option>
              </select>
              <button id="addProgBtn" class="btn">Thêm</button>
            </div>
          </section>

          <!-- DOCS -->
          <section id="docs" class="card tab" style="display:none">
            <h3>Tài liệu (lưu dài hạn)</h3>
            <input id="docInput" class="input" placeholder="Tiêu đề tài liệu" />
            <textarea id="docContent" class="input" style="height:110px;margin-top:8px" placeholder="Nội dung hoặc link..."></textarea>
            <div style="display:flex;gap:8px;margin-top:8px">
              <button id="addDocBtn" class="btn">Thêm tài liệu</button>
              <button id="clearDocsBtn" class="btn ghost">Xoá tất cả tài liệu</button>
            </div>
            <div class="items" id="docsList" style="margin-top:12px"></div>
          </section>

        </main>
      </div>

      <div class="footer">Built with ♥ — Daily Job</div>
    </div>
  </div>

  <script>
    // Countdown
    function updateCountdown(){
      const target = new Date('2026-06-01T00:00:00');
      const now = new Date();
      const diff = target - now;
      if(diff<0){ document.getElementById('countdown').textContent='Đã đến 01/06/2026'; return; }
      const d = Math.floor(diff/1000/60/60/24);
      const h = Math.floor(diff/1000/60/60)%24;
      const m = Math.floor(diff/1000/60)%60;
      const s = Math.floor(diff/1000)%60;
      document.getElementById('countdown').textContent = `${d}d ${h}h ${m}m ${s}s`;
    }
    setInterval(updateCountdown,1000);
    updateCountdown();

    // Daily quotes
    const quotes = [
      "Many a little makes a mickle",
      "Money makes the mare go",
      "Diamond cuts diamond",
      "A stitch in time saves nine",
      "Where there's a will, there's a way"
    ];
    function updateQuote(){
      const day = new Date().getDate();
      document.getElementById('dailyQuote').textContent = quotes[day % quotes.length];
    }
    updateQuote();

    // Navigation
    const tabs = document.querySelectorAll('.nav-btn');
    tabs.forEach(btn=>{ btn.addEventListener('click',()=>{
      tabs.forEach(b=>b.classList.remove('active'));
      btn.classList.add('active');
      document.querySelectorAll('.tab').forEach(t=>t.style.display = t.id===btn.dataset.tab?'':'none');
    })});

    // TODO
    const TODO_KEY = 'dailyjob_todos_v2';
    const TODO_DATE_KEY = 'dailyjob_todos_date_v2';
    function todayISO(){ return new Date().toISOString().slice(0,10); }
    let todos = JSON.parse(localStorage.getItem(TODO_KEY)||'[]');
    if(localStorage.getItem(TODO_DATE_KEY)!==todayISO()){ todos=[]; localStorage.setItem(TODO_DATE_KEY,todayISO()); localStorage.setItem(TODO_KEY,JSON.stringify(todos)); }

    function renderTodos(){ const ul=document.getElementById('todoList'); ul.innerHTML=''; todos.forEach((t,i)=>{
      const li=document.createElement('li');
      const cb=document.createElement('input'); cb.type='checkbox'; cb.checked=t.done; cb.addEventListener('change',()=>{ todos[i].done=cb.checked; localStorage.setItem(TODO_KEY,JSON.stringify(todos)); renderTodos(); });
      const txt=document.createElement('div'); txt.className='todo-text'+(t.done?' done':''); txt.textContent=t.text;
      const del=document.createElement('button'); del.className='btn ghost'; del.textContent='X'; del.addEventListener('click',()=>{ todos.splice(i,1); localStorage.setItem(TODO_KEY,JSON.stringify(todos)); renderTodos(); });
      li.append(cb,txt,del); ul.appendChild(li);
    }); }
    document.getElementById('addTodoBtn').addEventListener('click',()=>{
      const v=document.getElementById('todoInput').value.trim(); if(!v) return;
      todos.unshift({text:v,done:false}); document.getElementById('todoInput').value=''; localStorage.setItem(TODO_KEY,JSON.stringify(todos)); renderTodos();
    });
    document.getElementById('resetTodayBtn').addEventListener('click',()=>{ if(confirm('Reset danh sách hôm nay?')){ todos=[]; localStorage.setItem(TODO_KEY,JSON.stringify(todos)); renderTodos(); }});
    renderTodos();

    // Progress with subjects
    const subjects = ['math','physics','chem','eng'];
    const PROG_KEY = 'dailyjob_progress_v2';
    let progress = JSON.parse(localStorage.getItem(PROG_KEY)||'{}');
    subjects.forEach(s=>{ if(!progress[s]) progress[s]=[]; });
    function renderProgress(){
      subjects.forEach(s=>{
        const wrap=document.getElementById(s+'List'); wrap.innerHTML='';
        progress[s].forEach((p,i)=>{
          const div=document.createElement('div'); div.textContent=p; wrap.appendChild(div);
        });
      });
    }
    document.getElementById('addProgBtn').addEventListener('click',()=>{
      const val=document.getElementById('progInput').value.trim();
      const sub=document.getElementById('subjectSelect').value;
      if(!val) return;
      progress[sub].unshift(val);
      localStorage.setItem(PROG_KEY,JSON.stringify(progress));
      document.getElementById('progInput').value=''; renderProgress();
    });
    renderProgress();

    // Docs
    const DOCS_KEY='dailyjob_docs_v2';
    let docs = JSON.parse(localStorage.getItem(DOCS_KEY)||'[]');
    function renderDocs(){ const wrap=document.getElementById('docsList'); wrap.innerHTML=''; docs.forEach((d,i)=>{
      const div=document.createElement('div'); div.className='item-row';
      div.innerHTML='<strong>'+d.title+'</strong> ('+d.date+')<div>'+d.content+'</div>';
      const del=document.createElement('button'); del.className='btn ghost'; del.textContent='X'; del.addEventListener('click',()=>{ docs.splice(i,1); localStorage.setItem(DOCS_KEY,JSON.stringify(docs)); renderDocs(); });
      div.appendChild(del); wrap.appendChild(div);
    }); }
    document.getElementById('addDocBtn').addEventListener('click',()=>{
      const title=document.getElementById('docInput').value.trim();
      const content=document.getElementById('docContent').value.trim();
      if(!title) return;
      docs.unshift({title,content,date:new Date().toLocaleString()});
      localStorage.setItem(DOCS_KEY,JSON.stringify(docs));
      document.getElementById('docInput').value=''; document.getElementById('docContent').value=''; renderDocs();
    });
    document.getElementById('clearDocsBtn').addEventListener('click',()=>{ if(confirm('Xoá tất cả tài liệu?')){ docs=[]; localStorage.setItem(DOCS_KEY,JSON.stringify(docs)); renderDocs(); }});
    renderDocs();
  </script>
</body>
</html>
