# World-clock-app
Aplicación moderna de reloj mundial con javascrpit,html ycss.world-clock-app<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />

  <title>Reloj Mundial</title>

  <link rel="stylesheet" href="styles.css" />
</head>

<body>
  <main class="contenedor">
    <h1>Reloj mundial</h1>

    <section class="controles">
      <label for="tz-input">Añadir zona horaria:</label>
      <input id="tz-input" list="tz-list" placeholder="Ej: Europe/Madrid">
      <datalist id="tz-list"></datalist>

      <button id="add-btn">Añadir</button>

      <div class="opciones">
        <label>
          <input type="checkbox" id="show-date" checked>
          Mostrar fecha
        </label>

        <label>
          <input type="checkbox" id="hour12">
          Formato 12 horas
        </label>

        <button id="reset-defaults">Restablecer por defecto</button>
      </div>
    </section>

    <section id="clocks" class="clock-grid" aria-live="polite"></section>

    <footer>
      <p>Hecho con Intl.DateTimeFormat • Las zonas se guardan localmente</p>
    </footer>
  </main>

  <script src="script.js"></script>
</body>
</html><!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="theme-color" content="#000000" />
  <title>Reloj Mundial</title>

  <!-- Hoja de estilos -->
  <link rel="stylesheet" href="styles.css" />
</head>

<body>
  <main class="contenedor">
    <header>
      <h1>Reloj mundial</h1>
      <p class="lead">Añade zonas horarias y visualiza la hora local en cada una.</p>
    </header>

    <section class="controles" aria-label="Controles principales">
      <label for="tz-input">Añadir zona horaria:</label>
      <input id="tz-input" list="tz-list" placeholder="Ej: Europe/Madrid" />
      <datalist id="tz-list"></datalist>

      <button id="add-btn" class="control-btn">Añadir</button>

      <div class="opciones" aria-hidden="false">
        <label class="option-label">
          <input type="checkbox" id="show-date" checked>
          Mostrar fecha
        </label>

        <label class="option-label">
          <input type="checkbox" id="hour12">
          Formato 12 horas
        </label>

        <button id="reset-defaults" class="control-btn">Restablecer por defecto</button>
      </div>
    </section>

    <section id="clocks" class="clock-grid" aria-live="polite" aria-label="Relojes por zona"></section>

    <footer>
      <p>Hecho con <code>Intl.DateTimeFormat</code> • Las zonas seleccionadas se guardan localmente</p>
    </footer>
  </main>

  <script src="script.js" defer></script>
</body>
</html>:root{
  --bg: #0f1724;
  --card: #0b1220;
  --accent: #06b6d4;
  --muted: #94a3b8;
  --text: #e6eef8;
  --radius: 12px;
  --max-width: 980px;
  --font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
}

* { box-sizing: border-box; }
html, body { height: 100%; }
body {
  margin: 0;
  background: linear-gradient(180deg, var(--bg), #031028 120%);
  color: var(--text);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 24px;
  font-family: var(--font-family);
}

.contenedor{
  max-width: var(--max-width);
  margin: 0 auto;
}

h1{
  margin: 0 0 18px 0;
  font-weight: 600;
  letter-spacing: 0.2px;
}

.lead {
  margin-top: 6px;
  color: var(--muted);
  font-size: 14px;
}

.controles{
  display: flex;
  gap: 12px;
  align-items: center;
  flex-wrap: wrap;
  margin-bottom: 18px;
}

.controles input[type="text"],
.controles input[list]{
  padding: 8px 10px;
  border-radius: 8px;
  border: 1px solid rgba(255,255,255,0.06);
  background: rgba(255,255,255,0.02);
  color: var(--text);
  min-width: 220px;
  outline: none;
}

.control-btn{
  background: var(--accent);
  border: none;
  color: #031025;
  padding: 8px 12px;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 600;
}

.opciones {
  margin-left: auto;
  display: flex;
  gap: 12px;
  align-items: center;
}

.option-label {
  color: var(--muted);
  font-size: 14px;
  display: flex;
  gap: 6px;
  align-items: center;
}

.clock-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 14px;
  margin-top: 12px;
}

.clock-card{
  background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
  border-radius: var(--radius);
  padding: 14px;
  border: 1px solid rgba(255,255,255,0.03);
  display: flex;
  flex-direction: column;
  gap: 8px;
  min-height: 110px;
}

.clock-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 8px;
}

.tz-name {
  font-weight: 700;
  font-size: 15px;
}

.remove-btn {
  background: transparent;
  border: 1px solid rgba(255,255,255,0.06);
  color: var(--muted);
  padding: 6px 8px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 13px;
}

.time {
  font-size: 28px;
  font-weight: 700;
  letter-spacing: 0.6px;
}

.date {
  color: var(--muted);
  font-size: 13px;
}

.small {
  font-size: 12px;
  color: var(--muted);
}

footer {
  margin-top: 22px;
  color: var(--muted);
  font-size: 13px;
}// script.js - Reloj Mundial
(function () {
  const tzInput = document.getElementById('tz-input');
  const tzList = document.getElementById('tz-list');
  const addBtn = document.getElementById('add-btn');
  const clocksEl = document.getElementById('clocks');
  const showDateCheckbox = document.getElementById('show-date');
  const hour12Checkbox = document.getElementById('hour12');
  const resetBtn = document.getElementById('reset-defaults');

  const STORAGE_KEY = 'world_clock_zones_v1';

  // Util: obtener lista de zonas horarias (con fallback)
  function getTimeZones() {
    if (typeof Intl.supportedValuesOf === 'function') {
      try {
        return Intl.supportedValuesOf('timeZone');
      } catch (e) {
        // continuar al fallback
      }
    }
    // Fallback: lista corta y útil
    return [
      'UTC',
      'Europe/Madrid',
      'Europe/London',
      'America/New_York',
      'America/Los_Angeles',
      'America/Mexico_City',
      'Asia/Tokyo',
      'Asia/Shanghai',
      'Australia/Sydney'
    ];
  }

  // Estado
  const state = {
    zones: loadZones(),
    settings: {
      showDate: loadSetting('showDate', true),
      hour12: loadSetting('hour12', false)
    }
  };

  // Inicializa datalist con zonas
  const allTZ = getTimeZones();
  allTZ.forEach(tz => {
    const opt = document.createElement('option');
    opt.value = tz;
    tzList.appendChild(opt);
  });

  // Renders
  function renderClocks() {
    clocksEl.innerHTML = '';
    state.zones.forEach(tz => {
      const card = document.createElement('article');
      card.className = 'clock-card';
      card.dataset.tz = tz;

      const head = document.createElement('div');
      head.className = 'clock-head';

      const name = document.createElement('div');
      name.className = 'tz-name';
      name.textContent = tz;

      const removeBtn = document.createElement('button');
      removeBtn.className = 'remove-btn';
      removeBtn.type = 'button';
      removeBtn.textContent = 'Eliminar';
      removeBtn.addEventListener('click', () => {
        removeZone(tz);
      });

      head.appendChild(name);
      head.appendChild(removeBtn);

      const time = document.createElement('div');
      time.className = 'time';
      time.textContent = '';

      const date = document.createElement('div');
      date.className = 'date';
      date.textContent = '';

      card.appendChild(head);
      card.appendChild(time);
      if (state.settings.showDate) card.appendChild(date);

      clocksEl.appendChild(card);
    });

    updateTimes(); // render inicial
  }

  // Actualiza todos los tiempos (cada segundo)
  function updateTimes() {
    const cards = Array.from(document.querySelectorAll('.clock-card'));
    cards.forEach(card => {
      const tz = card.dataset.tz;
      const timeEl = card.querySelector('.time');
      const dateEl = card.querySelector('.date');

      try {
        const now = new Date();
        const opts = {
          hour: 'numeric',
          minute: '2-digit',
          second: '2-digit',
          hour12: !!state.settings.hour12,
          timeZone: tz
        };

        const timeStr = new Intl.DateTimeFormat(undefined, opts).format(now);
        timeEl.textContent = timeStr;

        if (state.settings.showDate && dateEl) {
          const dateOpts = {
            year: 'numeric',
            month: 'short',
            day: 'numeric',
            timeZone: tz
          };
          dateEl.textContent = new Intl.DateTimeFormat(undefined, dateOpts).format(now);
        }
      } catch (e) {
        timeEl.textContent = '—';
        if (dateEl) dateEl.textContent = '';
        console.warn('Error formateando zona', tz, e);
      }
    });
  }

  // Add/remove
  function addZone(tz) {
    if (!tz) return;
    if (!state.zones.includes(tz)) {
      state.zones.push(tz);
      saveZones();
      renderClocks();
    } else {
      // opcional: feedback
      flashInput('Ya añadido');
    }
  }

  function removeZone(tz) {
    state.zones = state.zones.filter(z => z !== tz);
    saveZones();
    renderClocks();
  }

  // Persistence
  function saveZones() {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(state.zones));
  }

  function loadZones() {
    try {
      const raw = localStorage.getItem(STORAGE_KEY);
      if (raw) return JSON.parse(raw);
    } catch (e) { /* ignore */ }
    // Default zones iniciales
    return ['UTC', 'Europe/Madrid', 'America/Mexico_City'];
  }

  function saveSetting(key, val) {
    localStorage.setItem(`wc_${key}`, JSON.stringify(val));
  }

  function loadSetting(key, def) {
    try {
      const r = localStorage.getItem(`wc_${key}`);
      return r === null ? def : JSON.parse(r);
    } catch (e) {
      return def;
    }
  }

  // small UI helpers
  function flashInput(message) {
    const prev = tzInput.placeholder;
    tzInput.placeholder = message;
    setTimeout(() => tzInput.placeholder = prev, 1200);
  }

  // Reset a valores por defecto
  function resetDefaults() {
    state.zones = ['UTC', 'Europe/Madrid', 'America/Mexico_City'];
    state.settings.showDate = true;
    state.settings.hour12 = false;
    saveZones();
    saveSetting('showDate', state.settings.showDate);
    saveSetting('hour12', state.settings.hour12);
    // Actualiza checkboxes y re-render
    showDateCheckbox.checked = state.settings.showDate;
    hour12Checkbox.checked = state.settings.hour12;
    renderClocks();
  }

  // Listeners
  addBtn.addEventListener('click', () => {
    const tz = tzInput.value.trim();
    if (tz) addZone(tz);
    tzInput.value = '';
  });

  tzInput.addEventListener('keydown', e => {
    if (e.key === 'Enter') {
      addBtn.click();
    }
  });

  showDateCheckbox.addEventListener('change', (e) => {
    state.settings.showDate = e.target.checked;
    saveSetting('showDate', state.settings.showDate);
    renderClocks();
  });

  hour12Checkbox.addEventListener('change', (e) => {
    state.settings.hour12 = e.target.checked;
    saveSetting('hour12', state.settings.hour12);
    renderClocks();
  });

  resetBtn.addEventListener('click', resetDefaults);

  // Inicialización
  renderClocks();
  // Actualiza cada segundo
  setInterval(updateTimes, 1000);
})();{
  "name": "reponsil-world-clock",
  "version": "1.0.0",
  "description": "Reloj mundial - demo",
  "private": true,
  "scripts": {
    "start": "serve . -s -l 5000",
    "check:html": "npx html-validate \"index.html\"",
    "check:css": "npx stylelint \"**/*.css\" --allow-empty-input",
    "ci": "npm run check:html && npm run check:css"
  },
  "devDependencies": {
    "html-validate": "^8.0.0",
    "stylelint": "^15.0.0",
    "serve": "^14.0.1"
  }
}name: CI - Reponsil

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  checks:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install dependencies
        run: npm ci

      - name: Run HTML & CSS checks
        run: npm run ci#!/usr/bin/env bash
# run.sh - start local static server for testing
set -e
if ! command -v npx >/dev/null 2>&1; then
  echo "npx no encontrado. Instala node/npx."
  exit 1
fi
npx serve . -s -l 5000npm install
npm run cichmod +x run.sh
./run.sh<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>World Clock App</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: #0e0e0e;
            color: #ffffff;
            margin: 0;
            padding: 20px;
            text-align: center;
        }

        h1 {
            margin-bottom: 30px;
        }

        .clock-container {
            display: flex;
            flex-direction: column;
            gap: 15px;
            max-width: 400px;
            margin: auto;
        }

        .clock {
            background: #1c1c1c;
            padding: 15px;
            border-radius: 10px;
            font-size: 1.3rem;
            box-shadow: 0 0 10px #000;
        }
    </style>
</head>
<body>

    <h1>World Clock</h1>

    <div class="clock-container">
        <div class="clock" id="mx">México: --:--:--</div>
        <div class="clock" id="ny">New York: --:--:--</div>
        <div class="clock" id="uk">Londres: --:--:--</div>
        <div class="clock" id="jp">Japón: --:--:--</div>
    </div>

    <script>
        function updateClocks() {
            const zones = {
                mx: "America/Mexico_City",
                ny: "America/New_York",
                uk: "Europe/London",
                jp: "Asia/Tokyo",
            };

            for (const id in zones) {
                const time = new Date().toLocaleTimeString("es-MX", {
                    timeZone: zones[id],
                });
                document.getElementById(id).textContent =
                    document.getElementById(id).textContent.split(":")[0] + ": " + time;
            }
        }

        setInterval(updateClocks, 1000);
        updateClocks();
    </script>

</body>
</html>feat(ui): fix and optimize index.html for World Clock App

- Cleaned HTML structure
- Improved responsive layout
- Fixed JavaScript timezone logic
- Added consistent styling
- Removed deprecated or unused elementsdiff --git a/index.html b/index.html
index 8f23a1d..c2b7fa0 100644
--- a/index.html
+++ b/index.html
@@ -1,32 +1,89 @@
-<html>
-<body>
-<h1>World Clock</h1>
-<div id="clock1"></div>
-<script>
-// old buggy code
-var x = new Date();
-document.getElementById("clock1").innerHTML = x;
-</script>
-</body>
-</html>
+<!DOCTYPE html>
+<html lang="en">
+<head>
+    <meta charset="UTF-8" />
+    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
+    <title>World Clock App</title>
+
+    <style>
+        body {
+            font-family: Arial, sans-serif;
+            background: #0e0e0e;
+            color: #ffffff;
+            margin: 0;
+            padding: 20px;
+            text-align: center;
+        }
+
+        h1 {
+            margin-bottom: 30px;
+        }
+
+        .clock-container {
+            display: flex;
+            flex-direction: column;
+            gap: 15px;
+            max-width: 400px;
+            margin: auto;
+        }
+
+        .clock {
+            background: #1c1c1c;
+            padding: 15px;
+            border-radius: 10px;
+            font-size: 1.3rem;
+            box-shadow: 0 0 10px #000;
+        }
+    </style>
+</head>
+<body>
+
+    <h1>World Clock</h1>
+
+    <div class="clock-container">
+        <div class="clock" id="mx">México: --:--:--</div>
+        <div class="clock" id="ny">New York: --:--:--</div>
+        <div class="clock" id="uk">Londres: --:--:--</div>
+        <div class="clock" id="jp">Japón: --:--:--</div>
+    </div>
+
+    <script>
+        function updateClocks() {
+            const zones = {
+                mx: "America/Mexico_City",
+                ny: "America/New_York",
+                uk: "Europe/London",
+                jp: "Asia/Tokyo",
+            };
+
+            for (const id in zones) {
+                const time = new Date().toLocaleTimeString("es-MX", {
+                    timeZone: zones[id],
+                });
+                document.getElementById(id).textContent =
+                    document.getElementById(id).textContent.split(":")[0] +
+                    ": " +
+                    time;
+            }
+        }
+
+        setInterval(updateClocks, 1000);
+        updateClocks();
+    </script>
+
+</body>
+</html>world-clock-app/
├─ src/
│  ├─ index.html
│  ├─ style.css
│  └─ app.js
│
├─ .github/
│   └─ workflows/
│       └─ ci.yml
│
├─ .gitignore
├─ LICENSE
├─ README.md
└─ package.json<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>World Clock App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <h1>🌎 World Clock</h1>

    <div class="clock-container">
        <div class="clock" id="mx">México: --:--:--</div>
        <div class="clock" id="ny">Nueva York: --:--:--</div>
        <div class="clock" id="uk">Londres: --:--:--</div>
        <div class="clock" id="jp">Tokio: --:--:--</div>
    </div>

    <script src="app.js"></script>
</body>
</html>body {
    background: #0e0e0e;
    color: white;
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 20px;
    text-align: center;
}

h1 {
    margin-bottom: 30px;
}

.clock-container {
    display: flex;
    flex-direction: column;
    gap: 15px;
    max-width: 400px;
    margin: auto;
}

.clock {
    background: #1c1c1c;
    padding: 16px;
    border-radius: 10px;
    font-size: 1.3rem;
    box-shadow: 0 0 10px black;
}function updateClocks() {
    const zones = {
        mx: "America/Mexico_City",
        ny: "America/New_York",
        uk: "Europe/London",
        jp: "Asia/Tokyo",
    };

    for (const id in zones) {
        const time = new Date().toLocaleTimeString("es-MX", {
            timeZone: zones[id],
        });

        document.getElementById(id).textContent =
            document.getElementById(id).textContent.split(":")[0] + ": " + time;
    }
}

setInterval(updateClocks, 1000);
updateClocks();name: CI

on:
  push:
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Run HTML Validator
        uses: Cyb3r-Jak3/html5validator-action@v3

      - name: Run JS Lint
        uses: actions/setup-node@v4
        with:
          node-version: 18
    node_modules/
dist/
*.log  - run: npm install eslintMIT License

Copyright (c) 2025

Permission is hereby granted, free of charge...# 🌎 World Clock App

Una aplicación simple, moderna y responsive que muestra la hora en diferentes zonas del mundo.

## ✨ Características

- ⏱️ Actualización automática cada segundo  
- 🌍 Relojes para México, Nueva York, Londres y Tokio  
- 📱 Totalmente responsive  
- ⚡ Carga rápida (HTML + CSS + JS puro)  
- 🔧 CI/CD con GitHub Actions  

---

## 📂 Estructura del proyecto---

## 🚀 Demo

*(Puedes activar GitHub Pages en `/settings/pages`)*

---

## 📦 Instalación---

## 🛠️ Uso

Solo abre:---

## 🤝 Contribuciones

¡Pull requests bienvenidos!

---

## 📝 Licencia

MIT License.{
  "name": "world-clock-app",
  "version": "1.0.0",
  "description": "Simple world clock application",
  "scripts": {
    "lint": "eslint src/**/*.js"
  }
}https://chatgpt.com/s/t_69253274ba2081918b366ee30881dbfccd /sdcard/Downloadunzip world-clock-app.zip -d world-clock-appcd world-clock-appgit init
git add .
git commit -m "Initial release: World Clock App"git remote add origin https://github.com/TU_USUARIO/world-clock-app.gitgit branch -M main
git push -u origin maingit branch -M main
git push -u origin main
      - run: npx eslint src/**/*.js
