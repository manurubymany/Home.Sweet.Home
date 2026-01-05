<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Home.Sweet.Home — Harmonia Hub (Manu & Pedro)</title>
    <meta name="description" content="Painel simples para tarefas, compras, finanças e ideias de encontro — Harmonia Hub, por Manu & Pedro.">
    <meta name="author" content="Manu & Pedro">
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #F8FAFC; -webkit-font-smoothing: antialiased; }
        .tab-content { display: none; }
        .tab-content.active { display: block; animation: slideUp 0.3s ease-out; }
        .active-nav { border-bottom: 3px solid #6366f1; color: #6366f1; font-weight: 800; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .card-animate { transition: transform 0.2s, box-shadow 0.2s; }
        .card-animate:hover { transform: translateY(-2px); box-shadow: 0 4px 12px rgba(0,0,0,0.05); }
        footer a { color: #6366f1; font-weight: 700; text-decoration: none; }
    </style>
</head>
<body>

    <header class="bg-white border-b sticky top-0 z-50 shadow-sm">
        <div class="max-w-5xl mx-auto px-4 h-16 flex justify-between items-center">
            <div class="flex items-center gap-2">
                <div class="w-8 h-8 bg-indigo-600 rounded-lg flex items-center justify-center shadow-lg text-white font-bold">H</div>
                <span class="font-bold text-lg tracking-tight">Harmonia<span class="text-indigo-600">.</span></span>
            </div>
            <div class="flex bg-slate-100 p-1 rounded-full text-xs font-semibold">
                <button onclick="switchUser('Manu')" id="btn-Manu" class="px-4 py-1.5 rounded-full bg-white shadow-sm text-indigo-600 transition-all">Manu</button>
                <button onclick="switchUser('Pedro')" id="btn-Pedro" class="px-4 py-1.5 rounded-full text-slate-500 transition-all">Pedro</button>
            </div>
        </div>
        <nav class="max-w-5xl mx-auto px-4 flex justify-between overflow-x-auto gap-4 no-scrollbar">
            <button onclick="showMainTab('casa')" id="nav-casa" class="py-3 text-[10px] font-black uppercase tracking-widest active-nav whitespace-nowrap">🏠 Casa</button>
            <button onclick="showMainTab('dates')" id="nav-dates" class="py-3 text-[10px] font-black uppercase tracking-widest text-slate-400 whitespace-nowrap">🍷 Ideias Date</button>
            <button onclick="showMainTab('pontos')" id="nav-pontos" class="py-3 text-[10px] font-black uppercase tracking-widest text-slate-400">🏆 Pontos</button>
            <button onclick="showMainTab('financeiro')" id="nav-financeiro" class="py-3 text-[10px] font-black uppercase tracking-widest text-slate-400">💰 Financeiro</button>
            <button onclick="showMainTab('compras')" id="nav-compras" class="py-3 text-[10px] font-black uppercase tracking-widest text-slate-400">🛒 Compras</button>
        </nav>
    </header>

    <main class="max-w-5xl mx-auto p-4 py-6">
        <section id="content-casa" class="tab-content active space-y-6">
            <div class="flex justify-between items-center">
                <h2 class="text-xl font-bold text-slate-700">Tarefas de <span id="view-name">Manu</span></h2>
                <button onclick="adicionarTarefaManual()" class="bg-indigo-50 text-indigo-600 px-4 py-2 rounded-xl text-xs font-bold">+ Nova</button>
            </div>
            <div class="flex overflow-x-auto pb-2 gap-3 no-scrollbar" id="dias-container"></div>
            <div id="daily-tasks" class="grid gap-3"></div>
        </section>

        <section id="content-dates" class="tab-content space-y-6">
            <div class="flex justify-between items-center">
                <h2 class="text-xl font-bold text-slate-700">Wishlist de Dates 🕯️</h2>
                <div class="flex gap-2">
                    <button onclick="sortearDate()" class="bg-amber-100 text-amber-700 px-4 py-2 rounded-xl text-xs font-bold shadow-sm">🎲 Sortear</button>
                    <button onclick="adicionarDate()" class="bg-rose-50 text-rose-600 px-4 py-2 rounded-xl text-xs font-bold">+ Nova</button>
                </div>
            </div>
            <div id="lista-dates" class="grid grid-cols-1 md:grid-cols-2 gap-4"></div>
        </section>

        <section id="content-pontos" class="tab-content">
            <div class="bg-white p-8 rounded-[2rem] shadow-sm border border-slate-100 text-center">
                <h2 class="text-xl font-bold mb-8">Placar da Semana 🚀</h2>
                <div class="grid grid-cols-2 gap-4">
                    <div class="bg-indigo-50 p-6 rounded-3xl border-2 border-indigo-100">
                        <span class="text-3xl font-black text-indigo-600" id="pts-manu">0</span>
                        <p class="text-[10px] uppercase font-bold text-indigo-400 mt-2">Manu</p>
                    </div>
                    <div class="bg-teal-50 p-6 rounded-3xl border-2 border-teal-100">
                        <span class="text-3xl font-black text-teal-600" id="pts-pedro">0</span>
                        <p class="text-[10px] uppercase font-bold text-teal-400 mt-2">Pedro</p>
                    </div>
                </div>
                <button onclick="resetarPontos()" class="mt-8 text-[10px] text-slate-400 underline font-bold">Resetar Placar</button>
            </div>
        </section>

        <section id="content-financeiro" class="tab-content space-y-6">
            <div class="grid grid-cols-2 gap-4">
                <div class="bg-emerald-500 p-6 rounded-[2rem] text-white shadow-lg shadow-emerald-100">
                    <h3 class="text-[10px] font-bold opacity-80 uppercase">Sair Juntos</h3>
                    <p class="text-2xl font-black" id="total-sair">R$ 0,00</p>
                </div>
                <div class="bg-indigo-600 p-6 rounded-[2rem] text-white shadow-lg shadow-indigo-100">
                    <h3 class="text-[10px] font-bold opacity-80 uppercase">Dinheiro Casa</h3>
                    <p class="text-2xl font-black" id="total-casa">R$ 0,00</p>
                </div>
            </div>
            <div class="bg-white p-6 rounded-[2rem] border shadow-sm">
                <input type="number" id="fin-valor" placeholder="Valor R$" class="w-full p-4 bg-slate-50 rounded-2xl mb-3 font-bold border-none outline-none focus:ring-2 ring-indigo-500/20">
                <select id="fin-destino" class="w-full p-3 bg-slate-100 rounded-xl text-xs font-bold border-none mb-3">
                    <option value="sair">🍷 Sair Juntos</option>
                    <option value="casa">🏠 Casa</option>
                </select>
                <button onclick="adicionarTransacao()" class="w-full py-4 bg-slate-900 text-white rounded-2xl font-bold">Lançar no Caixa</button>
            </div>
        </section>

        <section id="content-compras" class="tab-content space-y-6">
            <div class="bg-white p-6 rounded-[2rem] border shadow-sm">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-xl font-bold text-slate-700">Lista de Compras 🛒</h2>
                    <button onclick="adicionarItemCompra()" class="text-xs font-bold bg-indigo-600 text-white px-3 py-1 rounded-lg">Add Item</button>
                </div>
                <div id="lista-compras-geral" class="space-y-2"></div>
            </div>
        </section>
    </main>

    <footer class="max-w-5xl mx-auto p-6 text-center text-sm text-slate-500">
        Projeto: <strong>Home.Sweet.Home</strong> — Harmonia Hub<br>
        Repositório: <a href="https://github.com/manurubymany/Home.Sweet.Home" target="_blank" rel="noopener noreferrer">github.com/manurubymany/Home.Sweet.Home</a> · Site: <a href="https://manurubymany.github.io/Home.Sweet.Home/" target="_blank" rel="noopener noreferrer">Acessar site</a>
    </footer>

    <script>
        // --- DADOS INICIAIS ---
        const initialTasks = {
            "Segunda": [{ t: "Lavar louça", p: 20, user: "Manu" }],
            "Terça": [{ t: "Limpar o fogão (15/15 dias)", p: 30, user: "Pedro" }],
            "Quarta": [
                { t: "Lavar louça", p: 20, user: "Pedro" },
                { t: "Lavar Roupas", p: 30, user: "Manu" },
                { t: "Estender Roupas", p: 15, user: "Pedro" }
            ],
            "Quinta": [{ t: "Lavar banheiro (15/15 dias)", p: 50, user: "Manu" }],
            "Sexta": [
                { t: "Lavar louça", p: 20, user: "Manu" },
                { t: "Recolher e dobrar roupa varal", p: 20, user: "Pedro" }
            ],
            "Sábado": [
                { t: "Lavar louça", p: 20, user: "Pedro" },
                { t: "Fazer comida", p: 40, user: "Manu" },
                { t: "Lavar Roupas", p: 30, user: "Pedro" },
                { t: "Estender Roupas", p: 15, user: "Manu" },
                { t: "Varrer a casa", p: 30, user: "Pedro" },
                { t: "Lavar tapetes (15/15 dias)", p: 40, user: "Manu" }
            ],
            "Domingo": [
                { t: "Fazer comida", p: 40, user: "Pedro" },
                { t: "Tirar poeira dos móveis", p: 25, user: "Manu" },
                { t: "Recolher e dobrar roupa", p: 20, user: "Manu" },
                { t: "Passar pano na casa", p: 35, user: "Pedro" },
                { t: "Limpar guarda roupa (30 dias)", p: 60, user: "Pedro" },
                { t: "Limpar geladeira (30 dias)", p: 60, user: "Manu" }
            ]
        };

        const initialShopping = [
            "🥩 1kg de acem moido", "🥩 1kg de colchão duro bife", "🍗 1kg de peito de frango",
            "🧄 Alho com Sal (Pote)", "🧅 Cebola", "🌿 Cheiro verde",
            "🍎 Maçã", "🍈 Melão", "🍉 Melancia",
            "🥕 Cenoura", "🎃 Abobora", "🌱 Quiabo", "🥒 Vagem",
            "🍚 Arroz", "🫘 Feijão", "🍝 Macarrão", "🍅 Molho", "🍲 Lentilha",
            "🌽 Milho e ervilha", "🫒 Azeitona", "🥣 Maionese", "🥛 Leite", "🥤 Coca cola"
        ];

        const initialDates = [
            { titulo: "🌭 Night dog" },
            { titulo: "🥩 Estação da Picanha" },
            { titulo: "🥟 Pastel da sogra" }
        ];

        // --- ESTADO GLOBAL ---
        let db_tarefas, db_compras, db_dates, saldos, pontos, currentUser = 'Manu', diaAtual = 'Segunda';

        function save() { localStorage.setItem('harmonia_data_final', JSON.stringify({ db_tarefas, db_compras, db_dates, saldos, pontos })); }
        
        function load() {
            const saved = localStorage.getItem('harmonia_data_final');
            if (saved) {
                const data = JSON.parse(saved);
                db_tarefas = data.db_tarefas; db_compras = data.db_compras;
                db_dates = data.db_dates; saldos = data.saldos; pontos = data.pontos;
            } else {
                db_tarefas = JSON.parse(JSON.stringify(initialTasks));
                db_compras = [...initialShopping];
                db_dates = [...initialDates];
                saldos = { sair: 0, casa: 0 };
                pontos = { Manu: 0, Pedro: 0 };
            }
        }

        // --- FUNÇÕES DE RENDERIZAÇÃO ---
        function switchUser(name) {
            currentUser = name;
            document.getElementById('view-name').innerText = name;
            document.querySelectorAll('[id^="btn-"]').forEach(b => b.classList.remove('bg-white', 'shadow-sm', 'text-indigo-600'));
            document.getElementById('btn-' + name).classList.add('bg-white', 'shadow-sm', 'text-indigo-600');
            renderTarefas();
        }

        function renderTarefas() {
            const container = document.getElementById('daily-tasks');
            const tasks = (db_tarefas[diaAtual] || []).filter(t => t.user === currentUser);
            container.innerHTML = tasks.map(t => {
                const globalIdx = db_tarefas[diaAtual].indexOf(t);
                return `
                <div class="bg-white p-4 rounded-2xl border flex items-center justify-between shadow-sm card-animate">
                    <div class="flex items-center gap-4">
                        <input type="checkbox" onchange="completarTarefa(${globalIdx})" class="w-6 h-6 rounded-full border-slate-300 text-indigo-600">
                        <div><p class="font-bold text-slate-700">${t.t}</p><span class="text-[9px] font-black text-indigo-400 uppercase">${t.p} PTS</span></div>
                    </div>
                </div>`;
            }).join('') || '<p class="text-center text-slate-400 py-6 italic text-sm">Folga hoje! ✨</p>';
        }

        function completarTarefa(idx) {
            pontos[db_tarefas[diaAtual][idx].user] += db_tarefas[diaAtual][idx].p;
            db_tarefas[diaAtual].splice(idx, 1);
            save(); updateUI(); renderTarefas();
        }

        function renderCompras() {
            document.getElementById('lista-compras-geral').innerHTML = db_compras.map((item, idx) => `
                <div class="flex items-center justify-between p-3 bg-slate-50 rounded-xl">
                    <span class="font-semibold text-slate-700 text-sm">${item}</span>
                    <button onclick="db_compras.splice(${idx},1); save(); renderCompras();" class="text-rose-400 px-2">✕</button>
                </div>`).join('');
        }

        function renderDates() {
            document.getElementById('lista-dates').innerHTML = db_dates.map((d, idx) => `
                <div class="bg-white p-4 rounded-2xl border shadow-sm relative group card-animate">
                    <button onclick="db_dates.splice(${idx}, 1); save(); renderDates();" class="absolute top-2 right-2 text-slate-300 hover:text-rose-500 opacity-0 group-hover:opacity-100 transition-opacity">✕</button>
                    <h3 class="font-bold text-slate-800">📍 ${d.titulo}</h3>
                </div>`).join('');
        }

        function updateUI() {
            document.getElementById('pts-manu').innerText = pontos.Manu;
            document.getElementById('pts-pedro').innerText = pontos.Pedro;
            document.getElementById('total-sair').innerText = saldos.sair.toLocaleString('pt-br',{style:'currency',currency:'BRL'});
            document.getElementById('total-casa').innerText = saldos.casa.toLocaleString('pt-br',{style:'currency','BRL'});
        }

        // --- SISTEMA DE NAVEGAÇÃO ---
        function showMainTab(id) {
            document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
            document.getElementById('content-' + id).classList.add('active');
            document.querySelectorAll('nav button').forEach(b => b.classList.remove('active-nav', 'text-indigo-600'));
            document.getElementById('nav-' + id).classList.add('active-nav', 'text-indigo-600');
        }

        function setDia(d) { diaAtual = d; renderDias(); renderTarefas(); }

        function renderDias() {
            const dias = ["Segunda", "Terça", "Quarta", "Quinta", "Sexta", "Sábado", "Domingo"];
            document.getElementById('dias-container').innerHTML = dias.map(d => `
                <button onclick="setDia('${d}')" class="flex-shrink-0 px-5 py-2.5 rounded-xl border ${diaAtual === d ? 'bg-indigo-600 text-white' : 'bg-white text-slate-400'} font-bold text-[10px] uppercase transition-all">
                    ${d.substring(0,3)}
                </button>`).join('');
        }

        // --- FUNÇÕES DE ADIÇÃO ---
        function adicionarTransacao() {
            const val = parseFloat(document.getElementById('fin-valor').value);
            const dest = document.getElementById('fin-destino').value;
            if(val) { saldos[dest] += val; document.getElementById('fin-valor').value = ''; save(); updateUI(); }
        }

        function adicionarItemCompra() {
            const item = prompt("O que falta?");
            if(item) { db_compras.push(item); save(); renderCompras(); }
        }

        function adicionarDate() {
            const t = prompt("Novo lugar:");
            if(t) { db_dates.push({ titulo: t }); save(); renderDates(); }
        }

        function sortearDate() {
            if(db_dates.length === 0) return alert("Adicione ideias primeiro!");
            const escolhido = db_dates[Math.floor(Math.random() * db_dates.length)];
            alert(`💖 O destino é: ${escolhido.titulo.toUpperCase()}`);
        }

        function resetarPontos() { if(confirm("Resetar placar?")) { pontos = { Manu: 0, Pedro: 0 }; save(); updateUI(); } }

        window.onload = () => { load(); renderDias(); renderTarefas(); renderCompras(); renderDates(); updateUI(); };
    </script>
</body>
</html>
