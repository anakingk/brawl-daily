# Brawl Daily

Eine winzige PWA mit genau einer Aufgabe: Icon auf dem Android-Homescreen antippen, Knopf drücken, offizieller Supercell Store ist offen. Kein Login, keine Datenbank, kein Backend.

**Ziel-Adresse:** `https://store.supercell.com/brawlstars` — der offizielle Supercell Store für Brawl Stars. Das Tagesgeschenk gibt es dort nach Anmeldung mit der Supercell ID, Reset ist um 00:00 UTC.

---

## Dateien

```
brawl-daily/
├── index.html              ← die komplette App (HTML + CSS + JS in einer Datei)
├── manifest.webmanifest    ← macht sie auf Android installierbar
├── sw.js                   ← Service Worker, startet offline und sofort
├── favicon.ico
├── README.md
└── icons/
    ├── icon-192.png
    ├── icon-512.png
    ├── icon-maskable-192.png    ← für Androids runde/quadratische Icon-Masken
    ├── icon-maskable-512.png
    ├── apple-touch-icon.png     ← 180×180 für iPhone
    ├── favicon-32.png
    └── favicon-64.png
```

---

## Auf GitHub Pages stellen

Ohne Terminal, komplett im Browser:

1. Auf [github.com](https://github.com) einloggen → **New repository**
2. Name: `brawl-daily`, Sichtbarkeit **Public** (Pages braucht das im Gratis-Tarif), kein README anhaken → **Create repository**
3. Auf der leeren Repo-Seite: **uploading an existing file**
4. Den **Inhalt** des Ordners `brawl-daily` hochladen — also `index.html`, `manifest.webmanifest`, `sw.js`, `favicon.ico` und den Ordner `icons` (Ordner kann man per Drag-and-Drop mit reinziehen). Wichtig: nicht den Ordner `brawl-daily` selbst hochladen, sonst liegt alles eine Ebene zu tief.
5. **Commit changes**
6. **Settings** → links **Pages** → unter *Source* **Deploy from a branch**, Branch `main`, Ordner `/ (root)` → **Save**
7. Eine bis zwei Minuten warten, dann steht die Adresse oben auf der Pages-Seite:
   `https://DEIN-NAME.github.io/brawl-daily/`

Mit Git im Terminal geht es genauso:

```bash
cd brawl-daily
git init
git add .
git commit -m "Brawl Daily"
git branch -M main
git remote add origin https://github.com/DEIN-NAME/brawl-daily.git
git push -u origin main
```

Danach trotzdem einmal Schritt 6 in den Settings erledigen.

---

## Aufs Handy holen

Auf dem Android-Handy:

1. Die Pages-Adresse in **Chrome** öffnen (nicht Samsung Internet, da läuft die Installation anders)
2. Menü **⋮** → **Zum Startbildschirm hinzufügen** oder **App installieren**
3. Bestätigen — der Stern liegt danach als Icon zwischen den anderen Apps

Beim Antippen startet sie ohne Adressleiste, wie eine normale App. Nach dem ersten Start funktioniert sie auch ohne Netz, der Store-Link braucht natürlich Internet.

Auf dem iPhone: Safari → Teilen-Symbol → **Zum Home-Bildschirm**.

---

## Später anpassen

**Andere Ziel-Adresse** (falls Supercell umzieht): in `index.html` ganz unten im Script-Block

```js
const DAILY_REWARD_URL = "https://store.supercell.com/brawlstars";
```

**Übergang schneller oder langsamer:** `TRANSITION_MS` direkt darunter, aktuell 850 ms.

**Nach jeder Änderung** in `sw.js` die Zeile `const VERSION = "brawl-daily-v1"` hochzählen (`v2`, `v3` …). Sonst hält der Service Worker die alte Version fest und auf dem Handy ändert sich nichts.

---

## Was die App bewusst nicht tut

- Sie fragt nie nach Supercell-Login, Passwort oder Account-Daten. Die Anmeldung passiert ausschließlich bei Supercell selbst.
- Sie weiß nicht, ob das Geschenk wirklich abgeholt wurde. Der Punkt oben merkt sich nur lokal im Browser, ob heute schon auf den Knopf getippt wurde — reine Gedächtnisstütze, keine Verbindung zum Spielaccount.
- Sie sammelt nichts, sendet nichts, hat kein Tracking.
- Sie ist kein Produkt von Supercell. Das Icon ist ein eigener Stern, kein Brawl-Stars-Logo.
