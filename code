<html lang="uk">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Інтерактивна SVG Карта Вигаданого Світу</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Inter', sans-serif;
    }
    
    
    .map-shape {
      transition: all 0.25s ease-in-out;
      cursor: pointer;
    }
    .map-shape:hover {
      filter: drop-shadow(0 0 8px rgba(59, 130, 246, 0.6));
      transform: scale(1.008);
      transform-origin: center;
    }
    .map-shape.active {
      fill: #3b82f6 !important;
      stroke: #93c5fd;
      stroke-width: 1.5;
    }
    
   
    .bg-grid {
      background-size: 30px 30px;
      background-image: linear-gradient(to right, rgba(255, 255, 255, 0.03) 1px, transparent 1px),
                        linear-gradient(to bottom, rgba(255, 255, 255, 0.03) 1px, transparent 1px);
    }
    
    
    #labels-layer {
      transition: opacity 0.3s ease;
    }
    .labels-hidden #labels-layer {
      opacity: 0;
      pointer-events: none;
    }

   
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #0f172a;
    }
    ::-webkit-scrollbar-thumb {
      background: #334155;
      border-radius: 4px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #475569;
    }
  </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen flex flex-col antialiased selection:bg-blue-500 selection:text-white">

  
  <header class="border-b border-slate-800 bg-slate-900/80 backdrop-blur-md sticky top-0 z-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
      <div class="flex items-center space-x-3">
        <div class="p-2 bg-blue-600/20 text-blue-400 rounded-lg border border-blue-500/30">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 20l-5.447-2.724A1 1 0 013 16.382V5.618a1 1 0 011.447-.894L9 7m0 13l6-3m-6 3V7m6 10l4.553 2.276A1 1 0 0021 18.382V7.618a1 1 0 00-.553-.894L15 4m0 13V4m0 0L9 7"></path>
          </svg>
        </div>
        <div>
          <h1 class="font-bold text-lg text-slate-100 leading-none">Aethelgard SVG Atlas</h1>
          <p class="text-xs text-slate-400 mt-1">Демонстрація геометрії із зазорами (Margin / Gap)</p>
        </div>
      </div>

      
      <div class="flex items-center space-x-4">
        
        <label class="flex items-center cursor-pointer select-none">
          <span class="text-xs font-medium text-slate-300 mr-2.5">Назви (labels-layer)</span>
          <div class="relative">
            <input type="checkbox" id="toggle-labels" class="sr-only" checked>
            <div class="block bg-slate-800 w-10 h-6 rounded-full border border-slate-700 transition"></div>
            <div class="dot absolute left-1 top-1 bg-blue-500 w-4 h-4 rounded-full transition transform translate-x-4"></div>
          </div>
        </label>

        
        <button id="btn-view-code" class="px-3 py-1.5 text-xs font-medium bg-slate-800 hover:bg-slate-700 text-slate-200 rounded-lg border border-slate-700 transition flex items-center gap-1.5">
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"></path>
          </svg>
          SVG Код
        </button>
      </div>
    </div>
  </header>

  
  <main class="flex-1 flex flex-col lg:flex-row max-w-7xl w-full mx-auto p-4 sm:p-6 lg:p-8 gap-6">
<div class="flex-1 bg-slate-900 border border-slate-800 rounded-2xl overflow-hidden flex flex-col relative shadow-2xl">
     
      <div class="p-4 border-b border-slate-800/80 bg-slate-950/40 flex items-center justify-between">
        <div class="flex items-center space-x-2 text-sm text-slate-400" id="breadcrumb">
          <span class="text-blue-400 font-medium">Світ (world-map.svg)</span>
        </div>
        
        <button id="btn-back" class="hidden px-3 py-1 text-xs font-medium bg-blue-600 hover:bg-blue-500 text-white rounded-md shadow-md transition flex items-center gap-1">
          <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18"></path>
          </svg>
          Назад до карти світу
        </button>
      </div>

     
      <div id="svg-viewport" class="flex-1 bg-grid relative flex items-center justify-center p-6 min-h-[420px] lg:min-h-[550px]">
       
      </div>

     
      <div class="px-4 py-3 border-t border-slate-800/80 bg-slate-950/50 flex flex-wrap items-center justify-between text-xs text-slate-400 gap-2">
        <div class="flex items-center space-x-4">
          <span class="flex items-center gap-1.5">
            <span class="w-2.5 h-2.5 rounded-full bg-slate-700 border border-slate-500"></span>
   
          </span>
          <span class="flex items-center gap-1.5">
            <span class="w-2.5 h-2.5 rounded-full bg-blue-500"></span>
            Вибрана область
          </span>
        </div>
        <span id="map-stats">35 Країн на полотні</span>
      </div>
    </div>

    
    <div class="w-full lg:w-96 flex flex-col gap-6">
      
      
      <div class="bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl flex flex-col">
        <div class="flex items-center justify-between border-b border-slate-800 pb-4 mb-4">
          <div>
            <span id="inspect-tag" class="text-[10px] uppercase font-bold tracking-wider text-blue-400 bg-blue-950 border border-blue-800 px-2 py-0.5 rounded">Семантика ID</span>
            <h2 id="inspect-title" class="text-xl font-bold text-slate-100 mt-1">Оберіть елемент</h2>
          </div>
          <div id="inspect-id-badge" class="font-mono text-xs text-slate-400 bg-slate-950 px-2.5 py-1 rounded border border-slate-800">
            --
          </div>
        </div>

        <div class="space-y-4 flex-1">
          <p id="inspect-desc" class="text-sm text-slate-400 leading-relaxed">
            Наведіть курсор або натисніть на будь-яку країну на карті світу, щоб переглянути її внутрішню модульну структуру та геометрію областей.
          </p>

          <div id="inspect-details" class="hidden space-y-3 pt-2">
            <div class="bg-slate-950/60 p-3 rounded-lg border border-slate-800/80 space-y-2 text-xs">
              <div class="flex justify-between">
                <span class="text-slate-500">Контур (&lt;path&gt;):</span>
                <span class="text-emerald-400 font-mono">Автономний / Закритий</span>
              </div>
              <div class="flex justify-between">
                <span class="text-slate-500">Зазор (Margin/Gap):</span>
                <span class="text-slate-300 font-mono">Фізичні координати</span>
              </div>
              <div class="flex justify-between">
                <span class="text-slate-500">Кількість областей:</span>
                <span id="region-count" class="text-blue-400 font-bold">12-35</span>
              </div>
            </div>

            <button id="btn-enter-country" class="w-full py-2.5 px-4 bg-blue-600 hover:bg-blue-500 active:bg-blue-700 text-white font-medium text-sm rounded-xl transition shadow-lg shadow-blue-600/20 flex items-center justify-center gap-2">
<span>Відкрити карту країни</span>
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
            </svg>
          </button>
        </div>
      </div>

    </div>
  </main>

  
  <div id="modal-code" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-slate-900 border border-slate-800 rounded-2xl w-full max-w-4xl max-h-[85vh] flex flex-col shadow-2xl">
      <div class="p-4 border-b border-slate-800 flex items-center justify-between">
        <h3 class="font-bold text-slate-100 flex items-center gap-2 text-sm">
          <svg class="w-4 h-4 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 9l3 3-3 3m5 0h3M5 20h14a2 2 0 002-2V6a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
          </svg>
          Чистий SVG Код Поточного Вікна
        </h3>
        <button id="btn-close-modal" class="text-slate-400 hover:text-white p-1">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
          </svg>
        </button>
      </div>
      <div class="p-4 flex-1 overflow-auto bg-slate-950 font-mono text-xs text-emerald-400 leading-relaxed">
        <pre id="svg-code-content" class="whitespace-pre-wrap break-all"></pre>
      </div>
      <div class="p-4 border-t border-slate-800 flex justify-end gap-3">
        <button id="btn-copy-code" class="px-4 py-2 bg-blue-600 hover:bg-blue-500 text-white rounded-lg text-xs font-medium transition">
          Копіювати SVG
        </button>
      </div>
    </div>
  </div>

  <!-- JavaScript App Logic -->
  <script>
    // --- MOCK MAP DATA GENERATOR FOR DEMO ---
    // Generates mathematically distinct modular SVG shapes with built-in gaps/margins
    
    const COUNTRY_NAMES = [
      "Нордгард", "Острія", "Альбіон", "Соларія", "Вердантія", 
      "Зефірія", "Драконія", "Ельдорія", "Геліос", "Аркадія"
    ];

    const REGION_PREFIXES = ["Північний", "Західний", "Центральний", "Східний", "Південний", "Верхній", "Нижній", "Прибережний"];
    const REGION_SUFFIXES = ["Район", "Округ", "Префектура", "Дол", "Предел", "Край", "Глен"];

    // App State
    let currentView = 'world'; // 'world' or 'country'
    let selectedCountryId = null;
    let selectedElement = null;

    // Helper: Create a grid polygon path string with explicit margin gaps
    function generatePathData(x, y, width, height, gap = 4) {
      // Reduce dimensions to form natural geometry gap between paths
      const gx = x + gap / 2;
      const gy = y + gap / 2;
      const gw = width - gap;
      const gh = height - gap;
      const r = 6; // rounded path edges

      return `M ${gx + r} ${gy} 
              H ${gx + gw - r} 
              Q ${gx + gw} ${gy} ${gx + gw} ${gy + r} 
              V ${gy + gh - r} 
              Q ${gx + gw} ${gy + gh} ${gx + gw - r} ${gy + gh} 
              H ${gx + r} 
              Q ${gx} ${gy + gh} ${gx} ${gy + gh - r} 
              V ${gy + r} 
              Q ${gx} ${gy} ${gx + r} ${gy} Z`;
    }

    // World Map Generator (35 Countries layout grid)
    function generateWorldMapSVG() {
      const cols = 7;
      const rows = 5;
      const itemW = 100;
      const itemH = 80;
      const gap = 8; // Margin gap requirement from specs

      let countriesSVG = '';
      let labelsSVG = '';

      let idCounter = 1;
      for (let r = 0; r < rows; r++) {
        for (let c = 0; c < cols; c++) {
          const idNum = String(idCounter).padStart(2, '0');
          const countryId = `country-${idNum}`;
          const x = c * itemW + 20;
          const y = r * itemH + 20;
// Create SVG Path with geometrical gap
          const pathD = generatePathData(x, y, itemW, itemH, gap);
          const name = COUNTRY_NAMES[(idCounter - 1) % COUNTRY_NAMES.length] + ` ${idNum}`;

          countriesSVG += `
            <path id="${countryId}" 
                  data-name="${name}" 
                  class="map-shape fill-slate-800 stroke-slate-700 hover:fill-blue-600/60 stroke-[1.5]" 
                  d="${pathD}" />`;

          // Centered Text Label
          const cx = x + itemW / 2;
          const cy = y + itemH / 2;
          labelsSVG += `
            <text x="${cx}" y="${cy}" 
                  fill="#94a3b8" 
                  font-size="10" 
                  font-weight="600"
                  text-anchor="middle" 
                  dominant-baseline="central" 
                  class="pointer-events-none font-sans select-none tracking-wider">${name}</text>`;

          idCounter++;
        }
      }

      return `
        <svg viewBox="0 0 740 440" class="w-full h-full max-h-[600px] transition-all" xmlns="http://www.w3.org/2000/svg" id="svg-root">
          <g id="countries-layer">
            ${countriesSVG}
          </g>
          <g id="labels-layer">
            ${labelsSVG}
          </g>
        </svg>
      `;
    }

    // Country Detailed Map Generator (10 - 25 Regions layout grid)
    function generateCountryMapSVG(countryId, countryName) {
      const count = 16; // 16 regions per country map
      const cols = 4;
      const rows = 4;
      const itemW = 150;
      const itemH = 100;
      const gap = 6; // Specs gap requirement

      let regionsSVG = '';
      let labelsSVG = '';

      for (let i = 0; i < count; i++) {
        const r = Math.floor(i / cols);
        const c = i % cols;
        const idNum = String(i + 1).padStart(2, '0');
        const regionId = `region-${idNum}`;
        const x = c * itemW + 30;
        const y = r * itemH + 30;

        const pathD = generatePathData(x, y, itemW, itemH, gap);
        const regName = `${REGION_PREFIXES[i % REGION_PREFIXES.length]} ${REGION_SUFFIXES[i % REGION_SUFFIXES.length]}`;

        regionsSVG += `
          <path id="${regionId}" 
                data-name="${regName}" 
                class="map-shape fill-slate-800 stroke-slate-700 hover:fill-emerald-600/60 stroke-[1.5]" 
                d="${pathD}" />`;

        const cx = x + itemW / 2;
        const cy = y + itemH / 2;
        labelsSVG += `
          <text x="${cx}" y="${cy}" 
                fill="#cbd5e1" 
                font-size="11" 
                font-weight="500"
                text-anchor="middle" 
                dominant-baseline="central" 
                class="pointer-events-none font-sans select-none">${regName}</text>`;
      }

      return `
        <svg viewBox="0 0 660 460" class="w-full h-full max-h-[600px] transition-all" xmlns="http://www.w3.org/2000/svg" id="svg-root">
          <g id="regions-layer">
            ${regionsSVG}
          </g>
          <g id="labels-layer">
            ${labelsSVG}
          </g>
        </svg>
      `;
    }

    // DOM Elements
    const viewport = document.getElementById('svg-viewport');
    const toggleLabels = document.getElementById('toggle-labels');
    const btnBack = document.getElementById('btn-back');
    const breadcrumb = document.getElementById('breadcrumb');
    const inspectTitle = document.getElementById('inspect-title');
    const inspectIdBadge = document.getElementById('inspect-id-badge');
    const inspectDesc = document.getElementById('inspect-desc');
    const inspectDetails = document.getElementById('inspect-details');
    const btnEnterCountry = document.getElementById('btn-enter-country');
    const mapStats = document.getElementById('map-stats');
    
    // Modal Elements
const modalCode = document.getElementById('modal-code');
    const btnViewCode = document.getElementById('btn-view-code');
    const btnCloseModal = document.getElementById('btn-close-modal');
    const svgCodeContent = document.getElementById('svg-code-content');
    const btnCopyCode = document.getElementById('btn-copy-code');

    // --- Render Functions ---

    function loadWorldMap() {
      currentView = 'world';
      selectedCountryId = null;
      viewport.innerHTML = generateWorldMapSVG();
      
      // Update UI Header / Breadcrumbs
      breadcrumb.innerHTML = `<span class="text-blue-400 font-medium">Загальна Карта Світу (world-map.svg)</span>`;
      btnBack.classList.add('hidden');
      mapStats.textContent = '35 Країн на полотні';

      resetInspector();
      attachShapeEvents();
      updateLabelsVisibility();
    }

    function loadCountryMap(countryId, countryName) {
      currentView = 'country';
      selectedCountryId = countryId;
      viewport.innerHTML = generateCountryMapSVG(countryId, countryName);

      // Update UI Header / Breadcrumbs
      breadcrumb.innerHTML = `
        <span class="cursor-pointer hover:underline text-slate-400" onclick="loadWorldMap()">Світ</span>
        <span class="text-slate-600">/</span>
        <span class="text-emerald-400 font-medium">${countryName} (country-${countryId.split('-')[1]}.svg)</span>
      `;
      btnBack.classList.remove('hidden');
      mapStats.textContent = '16 Автономних областей';

      resetInspector();
      attachShapeEvents();
      updateLabelsVisibility();
    }

    function resetInspector() {
      selectedElement = null;
      inspectTitle.textContent = currentView === 'world' ? 'Оберіть країну' : 'Оберіть область';
      inspectIdBadge.textContent = '--';
      inspectDesc.textContent = currentView === 'world' 
        ? 'Натисніть на будь-яку країну для відкриття її внутрішніх областей та деталей.' 
        : 'Клацніть по регіону для перегляду його параметрів геометрії.';
      inspectDetails.classList.add('hidden');
    }

    function attachShapeEvents() {
      const shapes = viewport.querySelectorAll('.map-shape');

      shapes.forEach(shape => {
        shape.addEventListener('click', (e) => {
          e.stopPropagation();

          // Reset previous active styling
          shapes.forEach(s => s.classList.remove('active'));
          
          // Set active target
          shape.classList.add('active');
          selectedElement = shape;

          // Update Inspector Panel
          const id = shape.getAttribute('id');
          const name = shape.getAttribute('data-name');
          
          inspectTitle.textContent = name;
          inspectIdBadge.textContent = id;
          inspectDesc.textContent = `Об'єкт із модульним зазором. Всі межі утворені точними координатами без фізичного контакту контурів.`;
          inspectDetails.classList.remove('hidden');

          if (currentView === 'world') {
            btnEnterCountry.classList.remove('hidden');
          } else {
            btnEnterCountry.classList.add('hidden');
          }
        });
      });
    }

    function updateLabelsVisibility() {
      const isChecked = toggleLabels.checked;
      const dot = document.querySelector('.dot');
      
      if (isChecked) {
        viewport.classList.remove('labels-hidden');
        dot.style.transform = 'translateX(1rem)';
      } else {
        viewport.classList.add('labels-hidden');
        dot.style.transform = 'translateX(0rem)';
      }
    }

    // --- Event Listeners ---

    // Toggle Label visibility switch
    toggleLabels.addEventListener('change', updateLabelsVisibility);

    // Back button click
    btnBack.addEventListener('click', loadWorldMap);

    // Enter Country Button in Inspector
    btnEnterCountry.addEventListener('click', () => {
      if (selectedElement && currentView === 'world') {
        const id = selectedElement.getAttribute('id');
        const name = selectedElement.getAttribute('data-name');
        loadCountryMap(id, name);
      }
    });
// View Code Modal
    btnViewCode.addEventListener('click', () => {
      const svgCode = viewport.innerHTML.trim();
      svgCodeContent.textContent = svgCode;
      modalCode.classList.remove('hidden');
    });

    btnCloseModal.addEventListener('click', () => {
      modalCode.classList.add('hidden');
    });

    btnCopyCode.addEventListener('click', () => {
      const code = svgCodeContent.textContent;
      
      // Fallback safe clipboard execution
      const textarea = document.createElement('textarea');
      textarea.value = code;
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand('copy');
      document.body.removeChild(textarea);

      btnCopyCode.textContent = 'Скопійовано!';
      setTimeout(() => {
        btnCopyCode.textContent = 'Копіювати SVG';
      }, 2000);
    });

    // Initialize App on Window Load
    window.onload = function() {
      loadWorldMap();
    };
  </script>
</body>
</html>