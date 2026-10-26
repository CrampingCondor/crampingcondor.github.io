<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Leseverständnis-Aufgabe</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Merriweather:ital,wght@0,400;0,700;1,400&family=JetBrains+Mono:wght@500;700&display=swap');

    body {
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
      -webkit-tap-highlight-color: transparent;
    }

    .font-serif-academic {
      font-family: 'Merriweather', Georgia, serif;
    }

    .font-mono-num {
      font-family: 'JetBrains Mono', monospace;
    }

    /* Standard Push-Banner Einblend-Animation */
    @keyframes slideInPush {
      0% {
        opacity: 0;
        transform: translateY(-120%) scale(0.95);
      }
      70% {
        transform: translateY(6px) scale(1.01);
      }
      100% {
        opacity: 1;
        transform: translateY(0) scale(1);
      }
    }

    /* Standard Push-Banner Ausblend-Animation */
    @keyframes slideOutPush {
      0% {
        opacity: 1;
        transform: translateY(0) scale(1);
      }
      100% {
        opacity: 0;
        transform: translateY(-120%) scale(0.95);
      }
    }

    /* Auffällige Wackel-/Shake-Animation für die Prüfungs-Nachricht */
    @keyframes shakeIntense {
      0%, 100% { transform: translateX(0) rotate(0deg); }
      10%, 30%, 50%, 70%, 90% { transform: translateX(-7px) rotate(-1.5deg); }
      20%, 40%, 60%, 80% { transform: translateX(7px) rotate(1.5deg); }
    }

    .push-enter {
      animation: slideInPush 0.4s cubic-bezier(0.22, 1, 0.36, 1) forwards;
    }

    .push-enter-wobble {
      animation: 
        slideInPush 0.35s cubic-bezier(0.22, 1, 0.36, 1) forwards,
        shakeIntense 0.75s ease-in-out 0.35s 4;
    }

    .push-exit {
      animation: slideOutPush 0.3s cubic-bezier(0.4, 0, 1, 1) forwards;
    }
  </style>
</head>
<body class="bg-slate-100 text-slate-900 min-h-screen flex flex-col justify-between selection:bg-indigo-600 selection:text-white">

  <!-- =====================================================================
       OVERLAY CONTAINER FÜR PUSH-BENACHRICHTIGUNGEN (Top Fixed Banner)
       ===================================================================== -->
  <div id="push-container" class="fixed top-3 left-0 right-0 z-50 px-3 sm:px-4 pointer-events-none flex flex-col items-center gap-2.5 max-w-md mx-auto">
    <!-- Dynamische Push-Banner erscheinen hier -->
  </div>

  <!-- =====================================================================
       TOP HEADER BAR (Ohne Timer-Anzeige)
       ===================================================================== -->
  <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
    <div class="max-w-2xl mx-auto px-4 py-3.5 flex items-center justify-between">
      <div class="flex items-center gap-2">
        <span class="w-2.5 h-2.5 rounded-full bg-indigo-600"></span>
        <span class="text-xs font-bold uppercase tracking-wider text-slate-700">Leseverständnis-Aufgabe</span>
      </div>
      <span class="text-xs font-medium text-slate-400">Psychologisches Seminar</span>
    </div>
  </header>

  <!-- =====================================================================
       MAIN CONTENT AREA
       ===================================================================== -->
  <main class="flex-1 w-full max-w-2xl mx-auto px-4 py-6 flex flex-col justify-center">

    <!-- -------------------------------------------------------------------
         SCREEN 1: START-SCREEN (Neutral, ohne Erwähnung des Timers)
         ------------------------------------------------------------------- -->
    <section id="screen-start" class="bg-white rounded-2xl border border-slate-200 p-6 sm:p-8 shadow-sm">
      <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-indigo-50 text-indigo-700 text-xs font-semibold mb-4 border border-indigo-100">
        <span>📖 Textverständnis</span>
      </div>

      <h1 id="ui-start-title" class="text-2xl sm:text-3xl font-extrabold text-slate-900 tracking-tight mb-3">
        <!-- Wird aus CONFIG geladen -->
      </h1>

      <p id="ui-start-intro" class="text-slate-600 text-sm sm:text-base leading-relaxed mb-8">
        <!-- Wird aus CONFIG geladen -->
      </p>

      <button id="btn-open-text" class="w-full py-4 px-6 rounded-xl bg-indigo-600 hover:bg-indigo-700 active:scale-[0.99] text-white font-bold text-base shadow-md shadow-indigo-200 transition flex items-center justify-center gap-2">
        <span id="ui-start-btn">Text öffnen</span>
        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6"/></svg>
      </button>
    </section>

    <!-- -------------------------------------------------------------------
         SCREEN 2: LESE-AUFGABE + POP-UP BENACHRICHTIGUNGEN
         ------------------------------------------------------------------- -->
    <section id="screen-reading" class="hidden space-y-6">
      
      <!-- Hinweis-Banner über dem Artikel -->
      <div class="bg-amber-50 border border-amber-200/90 rounded-xl p-4 flex items-start gap-3 shadow-sm">
        <span class="text-lg leading-none mt-0.5">📌</span>
        <p id="ui-reading-hint" class="text-xs sm:text-sm font-medium text-amber-900 leading-snug">
          <!-- Wird aus CONFIG geladen -->
        </p>
      </div>

      <!-- Akademischer Artikel-Container -->
      <article class="bg-white rounded-2xl border border-slate-200 p-5 sm:p-8 shadow-sm">
        <div class="border-b border-slate-100 pb-4 mb-5">
          <div id="ui-article-meta" class="text-[11px] font-semibold uppercase tracking-wider text-slate-400 mb-1">
            <!-- Quelle -->
          </div>
          <h2 id="ui-article-title" class="text-lg sm:text-xl font-bold text-slate-900 leading-snug">
            <!-- Artikeltitel -->
          </h2>
        </div>

        <!-- Der englische Original-Abstract -->
        <div id="ui-article-paragraphs" class="font-serif-academic text-slate-800 text-[15px] sm:text-base leading-[1.85] space-y-4">
          <!-- Absätze werden aus CONFIG geladen -->
        </div>
      </article>

      <!-- Button zum Weitergehen -->
      <div class="pt-2">
        <button id="btn-to-questions" class="w-full py-4 px-6 rounded-xl bg-slate-900 hover:bg-slate-800 active:scale-[0.99] text-white font-bold text-base transition shadow-md flex items-center justify-center gap-2">
          <span id="ui-reading-next-btn">Weiter zur Aufgabe</span>
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/></svg>
        </button>
      </div>
    </section>

    <!-- -------------------------------------------------------------------
         SCREEN 3: FRAGEN (1x Freitext zum Artikel, 1x MC zur Prüfungsnote)
         ------------------------------------------------------------------- -->
    <section id="screen-questions" class="hidden bg-white rounded-2xl border border-slate-200 p-6 sm:p-8 shadow-sm space-y-7">
      <div>
        <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-indigo-50 text-indigo-700 text-xs font-bold mb-2 border border-indigo-100">
          <span>✍️ Aufgaben</span>
        </div>
        <h2 class="text-xl sm:text-2xl font-extrabold text-slate-900">
          Fragen zum Durchgang
        </h2>
      </div>

      <!-- FRAGE 1: Freitext zum Artikel-Thema -->
      <div class="space-y-2.5">
        <label for="input-freetext" id="ui-q1-label" class="block text-sm sm:text-base font-bold text-slate-900 leading-snug">
          <!-- Wird aus CONFIG geladen -->
        </label>
        <textarea 
          id="input-freetext" 
          rows="3" 
          class="w-full rounded-xl border border-slate-300 bg-slate-50/70 p-3.5 text-sm sm:text-base text-slate-900 placeholder-slate-400 focus:bg-white focus:border-indigo-600 focus:ring-2 focus:ring-indigo-500/20 outline-none transition"
          placeholder="Deine Antwort in einem Satz..."
        ></textarea>
      </div>

      <!-- FRAGE 2: Single Multiple Choice zur Prüfungs-Nachricht -->
      <div class="space-y-3 pt-4 border-t border-slate-100">
        <label id="ui-q2-label" class="block text-sm sm:text-base font-bold text-slate-900 leading-snug">
          <!-- Wird aus CONFIG geladen -->
        </label>
        <div id="ui-q2-options" class="space-y-2.5">
          <!-- Radio-Buttons werden aus CONFIG generiert -->
        </div>
      </div>

      <p id="questions-error-msg" class="hidden text-xs font-semibold text-rose-600 bg-rose-50 border border-rose-200 rounded-lg p-3">
        Bitte beantworte beide Fragen, um die Auswertung anzuzeigen.
      </p>

      <button id="btn-show-results" class="w-full py-4 px-6 rounded-xl bg-indigo-600 hover:bg-indigo-700 active:scale-[0.99] text-white font-bold text-base shadow-md transition">
        Auswertung anzeigen
      </button>
    </section>

    <!-- -------------------------------------------------------------------
         SCREEN 4: REINE AUSWERTUNG (Ohne Psychofakt-Erklärbox)
         ------------------------------------------------------------------- -->
    <section id="screen-results" class="hidden space-y-5">
      <div class="bg-white rounded-2xl border border-slate-200 p-6 sm:p-8 shadow-sm space-y-6">
        <div>
          <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-emerald-50 text-emerald-700 text-xs font-bold mb-2 border border-emerald-100">
            <span>📊 Auswertung</span>
          </div>
          <h2 class="text-2xl font-extrabold text-slate-900">
            Deine Ergebnisse
          </h2>
        </div>

        <!-- Metrik 1: Benötigte Lesezeit -->
        <div class="p-4 sm:p-5 rounded-xl bg-slate-50 border border-slate-200 flex flex-col sm:flex-row sm:items-center justify-between gap-2">
          <div>
            <span class="text-xs font-bold uppercase tracking-wider text-slate-400 block">1. Benötigte Lesezeit</span>
            <span id="res-notif-count" class="text-xs text-slate-500 mt-0.5 block">
              <!-- Anzahl eingeblendeter Nachrichten -->
            </span>
          </div>
          <div id="res-reading-time" class="text-2xl sm:text-3xl font-extrabold font-mono-num text-indigo-600">
            0,0 Sekunden
          </div>
        </div>

        <!-- Metrik 2: Deine Antwort zum Artikel-Thema -->
        <div class="p-4 sm:p-5 rounded-xl bg-slate-50 border border-slate-200 space-y-3">
          <span class="text-xs font-bold uppercase tracking-wider text-slate-400 block">
            2. Deine Antwort zum Artikel-Thema
          </span>
          <blockquote id="res-user-freetext" class="p-3.5 rounded-lg bg-white border border-slate-200 text-sm sm:text-base text-slate-800 italic">
            <!-- Eingabe des Nutzers -->
          </blockquote>
          <p id="res-reference-text" class="text-xs text-slate-500 leading-relaxed">
            <!-- Kurze neutrale Referenz aus CONFIG -->
          </p>
        </div>

        <!-- Metrik 3: Erinnerung an den Störreiz (Prüfungs-Nachricht) -->
        <div class="p-4 sm:p-5 rounded-xl bg-slate-50 border border-slate-200 space-y-3">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <span class="text-xs font-bold uppercase tracking-wider text-slate-400">
              3. Erinnerung an den Störreiz (Prüfungs-Nachricht)
            </span>
            <span id="res-mc-badge" class="px-3 py-1 rounded-full text-xs font-bold">
              <!-- Korrekt erinnert / Nicht korrekt -->
            </span>
          </div>

          <div class="text-sm text-slate-700">
            Deine Auswahl: <strong id="res-mc-selected" class="text-slate-900"></strong>
          </div>
        </div>

        <!-- Button zum Neustarten -->
        <div class="pt-2">
          <button id="btn-restart" class="w-full py-3.5 px-5 rounded-xl bg-slate-900 hover:bg-slate-800 active:scale-[0.99] text-white font-bold text-sm sm:text-base transition">
            Neu starten
          </button>
        </div>
      </div>
    </section>

  </main>

  <!-- Footer -->
  <footer class="max-w-2xl mx-auto w-full px-4 py-4 text-center text-xs text-slate-400">
    Interaktives Experiment &bull; Psychologie
  </footer>

  <!-- =====================================================================
       JAVASCRIPT & EINFACHER KONFIGURATIONSBEREICH
       ===================================================================== -->
  <script>
    /* =========================================================================
       █████████████████████████████████████████████████████████████████████████
       KONFIGURATIONSBEREICH - HIER TEXTE, ZEITEN & FRAGEN ANPASSEN
       █████████████████████████████████████████████████████████████████████████
       Du kannst alle Texte innerhalb der Anführungszeichen ("...") einfach 
       ändern. Wenn du die Datei speicherst, werden deine Änderungen sofort 
       übernommen.
       ========================================================================= */

    const CONFIG = {

      // 1. START-SCREEN (Kein Hinweis auf Zeitmessung!)
      startScreen: {
        title: "Leseverständnis-Aufgabe",
        instruction: "Bitte lies den folgenden englischsprachigen wissenschaftlichen Abstract aufmerksam durch. Im Anschluss folgt eine kurze Frage zum Inhalt.",
        buttonText: "Text öffnen"
      },

      // 2. ARTIKEL-TEXT (Original-Abstract von Simons & Chabris, 1999)
      article: {
        topHint: "Lies den Text sorgfältig durch. Klicke unten auf „Weiter zur Aufgabe“, sobald du fertig bist.",
        sourceMeta: "Simons, D. J., & Chabris, C. F. (1999) • Perception, 28(9), 1059–1074",
        title: "Gorillas in our midst: sustained inattentional blindness for dynamic events",
        nextButtonText: "Weiter zur Aufgabe",
        // Jeder Text in Anführungszeichen bildet einen Absatz:
        paragraphs: [
          "With each eye fixation, we experience a richly detailed visual world. Yet recent work on visual integration and change direction reveals that we are surprisingly unaware of the details of our environment from one view to the next: we often do not detect large changes to objects and scenes ('change blindness'). Furthermore, without attention, we may not even perceive objects ('inattentional blindness'). Taken together, these findings suggest that we perceive and remember only those objects and details that receive focused attention. In this paper, we briefly review and discuss evidence for these cognitive forms of 'blindness'. We then present a new study that builds on classic studies of divided visual attention to examine inattentional blindness for complex objects and events in dynamic scenes. Our results suggest that the likelihood of noticing an unexpected object depends on the similarity of that object to other objects in the display and on how difficult the priming monitoring task is. Interestingly, spatial proximity of the critical unattended object to attended locations does not appear to affect detection, suggesting that observers attend to objects and events, not spatial positions. We discuss the implications of these results for visual representations and awareness of our visual environment."
        ]
      },

      // 3. DIE 6 PUSH-BENACHRICHTIGUNGEN WÄHREND DES LESENS
      // delaySeconds = Nach wie vielen Sekunden erscheint die Nachricht?
      // durationSeconds = Wie lange bleibt sie sichtbar (in Sekunden)?
      // wobble = true aktiviert den starken Wackel-Effekt + rote Hervorhebung!
      notifications: [
        {
          delaySeconds: 9,
          durationSeconds: 5.5,
          icon: "⚠️",
          appName: "Eilmeldung",
          timeText: "Gerade eben",
          message: "Eiffelturm in Paris eingestürzt, drei Leute unter Schutt begraben.",
          style: "news",
          wobble: false
        },
        {
          delaySeconds: 18,
          durationSeconds: 6.5,
          icon: "🎓",
          appName: "Studierenden-Service-Center",
          timeText: "Wichtig",
          message: "Deine Note für die Prüfung „Differenzielle Psychologie und Persönlichkeitspsychologie“ muss neu berechnet werden.",
          style: "uni_alert",
          wobble: true // <-- WACKELT STARK & ROT HERVORGEHOBEN (Position 2)
        },
        {
          delaySeconds: 27,
          durationSeconds: 5.5,
          icon: "📸",
          appName: "Instagram",
          timeText: "Jetzt",
          message: "Jana hat einen neuen Post veröffentlicht. Klicke jetzt, um zu liken.",
          style: "insta",
          wobble: false
        },
        {
          delaySeconds: 36,
          durationSeconds: 5.5,
          icon: "💳",
          appName: "PayPal",
          timeText: "Gerade eben",
          message: "Zahlung von 489,00 € an MediaMarkt Online erfolgreich autorisiert.",
          style: "paypal",
          wobble: false
        },
        {
          delaySeconds: 45,
          durationSeconds: 5.5,
          icon: "💬",
          appName: "WhatsApp • Mama",
          timeText: "Jetzt",
          message: "Ruf mich bitte SOFORT zurück, wenn du das liest!!",
          style: "whatsapp",
          wobble: false
        },
        {
          delaySeconds: 54,
          durationSeconds: 5.5,
          icon: "🔋",
          appName: "Systemwarnung",
          timeText: "4% Batterie",
          message: "Akku fast leer (4%). Das Gerät schaltet sich in Kürze aus.",
          style: "battery",
          wobble: false
        }
      ],

      // 4. FRAGEN AUF SCREEN 3
      questions: {
        // Frage 1: Freitextfrage zum Artikel
        freeTextQuestion: "1. Beschreibe in einem Satz, welches Thema der Artikel behandelt:",
        freeTextPlaceholder: "Schreibe hier deinen Satz zum Thema des Artikels...",
        referenceSolution: "Referenz: Unaufmerksamkeitsblindheit (Inattentional Blindness) bei selektiver visueller Aufmerksamkeit (Gorilla-Experiment).",

        // Frage 2: Multiple-Choice-Frage zur Prüfungs-Nachricht
        mcQuestion: "2. Für welches Modul muss laut Benachrichtigung des Studierenden-Service-Centers deine Note neu berechnet werden?",
        mcOptions: [
          "Differenzielle Psychologie und Persönlichkeitspsychologie",
          "Quantitative Methoden II",
          "Sozialpsychologie"
        ],
        // Welche Option ist richtig? (0 = die erste Option, 1 = die zweite, 2 = die dritte)
        mcCorrectIndex: 0
      }

    };

    /* =========================================================================
       ENDE DES KONFIGURATIONSBEREICHS
       Ab hier folgt die technische Programmlogik.
       ========================================================================= */

    let readingStartTimestamp = 0;
    let readingDurationSec = 0;
    let activeTimeouts = [];
    let shownNotificationsCount = 0;
    let selectedMcIndex = null;

    // Dezenter Benachrichtigungston über Web Audio API (funktioniert ohne externe Audiodatei)
    const AudioCtx = window.AudioContext || window.webkitAudioContext;
    let audioCtx = null;

    function playNotificationSound(isUrgentWobble) {
      try {
        if (!audioCtx) audioCtx = new AudioCtx();
        if (audioCtx.state === 'suspended') audioCtx.resume();
        const now = audioCtx.currentTime;
        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();

        osc.type = isUrgentWobble ? 'triangle' : 'sine';
        osc.frequency.setValueAtTime(isUrgentWobble ? 920 : 840, now);
        osc.frequency.exponentialRampToValueAtTime(isUrgentWobble ? 1480 : 1220, now + 0.1);

        gain.gain.setValueAtTime(isUrgentWobble ? 0.09 : 0.05, now);
        gain.gain.exponentialRampToValueAtTime(0.0001, now + 0.25);

        osc.connect(gain);
        gain.connect(audioCtx.destination);
        osc.start(now);
        osc.stop(now + 0.25);
      } catch (e) {
        // Ignorieren, falls Browser Audio blockiert
      }
    }

    // Texte & Optionen aus CONFIG in das HTML laden
    function renderConfigToDOM() {
      // Screen 1
      document.getElementById('ui-start-title').textContent = CONFIG.startScreen.title;
      document.getElementById('ui-start-intro').textContent = CONFIG.startScreen.instruction;
      document.getElementById('ui-start-btn').textContent = CONFIG.startScreen.buttonText;

      // Screen 2
      document.getElementById('ui-reading-hint').textContent = CONFIG.article.topHint;
      document.getElementById('ui-article-meta').textContent = CONFIG.article.sourceMeta;
      document.getElementById('ui-article-title').textContent = CONFIG.article.title;
      document.getElementById('ui-reading-next-btn').textContent = CONFIG.article.nextButtonText;

      const pContainer = document.getElementById('ui-article-paragraphs');
      pContainer.innerHTML = '';
      CONFIG.article.paragraphs.forEach(text => {
        const p = document.createElement('p');
        p.textContent = text;
        pContainer.appendChild(p);
      });

      // Screen 3
      document.getElementById('ui-q1-label').textContent = CONFIG.questions.freeTextQuestion;
      const freetextEl = document.getElementById('input-freetext');
      freetextEl.placeholder = CONFIG.questions.freeTextPlaceholder;
      freetextEl.value = '';

      document.getElementById('ui-q2-label').textContent = CONFIG.questions.mcQuestion;
      const mcContainer = document.getElementById('ui-q2-options');
      mcContainer.innerHTML = '';

      CONFIG.questions.mcOptions.forEach((optText, idx) => {
        const label = document.createElement('label');
        label.className = 'flex items-start gap-3 p-3.5 rounded-xl border border-slate-200 bg-slate-50/70 hover:bg-indigo-50/50 hover:border-indigo-200 cursor-pointer transition select-none';
        label.innerHTML = `
          <input type="radio" name="mc_module_question" value="${idx}" class="mt-0.5 w-4 h-4 text-indigo-600 focus:ring-indigo-500">
          <span class="text-sm sm:text-base font-medium text-slate-800 leading-snug">${optText}</span>
        `;
        label.querySelector('input').addEventListener('change', () => {
          selectedMcIndex = idx;
          document.getElementById('questions-error-msg').classList.add('hidden');
        });
        mcContainer.appendChild(label);
      });

      // Screen 4 Referenztext
      document.getElementById('res-reference-text').textContent = CONFIG.questions.referenceSolution;
    }

    // Styling je nach Benachrichtigungstyp
    function getBannerStyle(styleType, isWobble) {
      if (isWobble || styleType === 'uni_alert') {
        return {
          wrapperBorder: 'border-2 border-red-600 ring-4 ring-red-500/30 shadow-2xl shadow-red-600/25 bg-red-50/95',
          badge: 'bg-red-600 text-white',
          iconBox: 'bg-red-600 text-white'
        };
      }
      switch (styleType) {
        case 'news':
          return {
            wrapperBorder: 'border-2 border-rose-300 shadow-2xl bg-white/95',
            badge: 'bg-rose-600 text-white',
            iconBox: 'bg-rose-100 text-rose-600'
          };
        case 'insta':
          return {
            wrapperBorder: 'border-2 border-pink-300 shadow-2xl bg-white/95',
            badge: 'bg-gradient-to-r from-fuchsia-600 via-pink-600 to-amber-500 text-white',
            iconBox: 'bg-pink-100 text-pink-600'
          };
        case 'paypal':
          return {
            wrapperBorder: 'border-2 border-sky-300 shadow-2xl bg-white/95',
            badge: 'bg-sky-700 text-white',
            iconBox: 'bg-sky-100 text-sky-700'
          };
        case 'whatsapp':
          return {
            wrapperBorder: 'border-2 border-emerald-300 shadow-2xl bg-white/95',
            badge: 'bg-emerald-600 text-white',
            iconBox: 'bg-emerald-100 text-emerald-700'
          };
        case 'battery':
        default:
          return {
            wrapperBorder: 'border-2 border-amber-300 shadow-2xl bg-white/95',
            badge: 'bg-slate-800 text-white',
            iconBox: 'bg-amber-100 text-amber-700'
          };
      }
    }

    // Einzelnes Push-Banner oben einblenden
    function showPushBanner(notif) {
      const container = document.getElementById('push-container');
      const styleCfg = getBannerStyle(notif.style, notif.wobble);

      shownNotificationsCount++;

      // Smartphone-Vibration (stärker bei der wackelnden Prüfungsnachricht)
      if (navigator.vibrate) {
        if (notif.wobble) {
          navigator.vibrate([160, 70, 160, 70, 200]);
        } else {
          navigator.vibrate([80, 40, 80]);
        }
      }
      playNotificationSound(notif.wobble);

      const banner = document.createElement('div');
      const animClass = notif.wobble ? 'push-enter-wobble' : 'push-enter';
      banner.className = `pointer-events-auto w-full backdrop-blur-md rounded-2xl p-3.5 ${styleCfg.wrapperBorder} ${animClass} transition-transform`;

      banner.innerHTML = `
        <div class="flex items-start gap-3">
          <div class="w-10 h-10 rounded-xl ${styleCfg.iconBox} flex items-center justify-center text-xl shrink-0 shadow-sm">
            ${notif.icon}
          </div>
          <div class="flex-1 min-w-0">
            <div class="flex items-center justify-between gap-2 mb-1">
              <span class="px-2 py-0.5 rounded text-[10px] font-extrabold uppercase tracking-wider ${styleCfg.badge}">
                ${notif.appName}
              </span>
              <div class="flex items-center gap-2">
                <span class="text-[11px] text-slate-500 font-medium">${notif.timeText}</span>
                <button type="button" aria-label="Schließen" class="close-banner-btn text-slate-400 hover:text-slate-700 text-sm font-bold px-1.5 py-0.5 rounded">×</button>
              </div>
            </div>
            <p class="text-xs sm:text-sm font-bold text-slate-900 leading-snug">
              ${notif.message}
            </p>
          </div>
        </div>
      `;

      let dismissed = false;
      function removeBanner() {
        if (dismissed) return;
        dismissed = true;
        banner.classList.remove('push-enter', 'push-enter-wobble');
        banner.classList.add('push-exit');
        setTimeout(() => {
          if (banner.parentNode) banner.parentNode.removeChild(banner);
        }, 300);
      }

      banner.addEventListener('click', removeBanner);

      const hideTimer = setTimeout(removeBanner, (notif.durationSeconds || 5.5) * 1000);
      activeTimeouts.push(hideTimer);

      container.appendChild(banner);
    }

    // Alle geplanten Timer bereinigen
    function clearScheduledNotifications() {
      activeTimeouts.forEach(id => clearTimeout(id));
      activeTimeouts = [];
      document.getElementById('push-container').innerHTML = '';
    }

    // Übergang: Screen 1 -> Screen 2 (Lesen + Stille Zeitmessung startet)
    function startReadingScreen() {
      shownNotificationsCount = 0;
      selectedMcIndex = null;

      document.getElementById('screen-start').classList.add('hidden');
      document.getElementById('screen-questions').classList.add('hidden');
      document.getElementById('screen-results').classList.add('hidden');
      document.getElementById('screen-reading').classList.remove('hidden');

      window.scrollTo({ top: 0, behavior: 'smooth' });

      // Stille Zeitmessung im Hintergrund starten
      readingStartTimestamp = performance.now();

      // Alle 6 Push-Nachrichten einplanen
      clearScheduledNotifications();
      CONFIG.notifications.forEach(notif => {
        const timerId = setTimeout(() => {
          showPushBanner(notif);
        }, notif.delaySeconds * 1000);
        activeTimeouts.push(timerId);
      });
    }

    // Übergang: Screen 2 -> Screen 3 (Fragen)
    function goToQuestionsScreen() {
      // Stille Zeitmessung stoppen
      const elapsedMs = performance.now() - readingStartTimestamp;
      readingDurationSec = elapsedMs / 1000;

      clearScheduledNotifications();

      document.getElementById('screen-reading').classList.add('hidden');
      document.getElementById('screen-questions').classList.remove('hidden');

      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    // Übergang: Screen 3 -> Screen 4 (Auswertung)
    function submitQuestionsAndShowResults() {
      const freetextVal = document.getElementById('input-freetext').value.trim();

      if (!freetextVal || selectedMcIndex === null) {
        document.getElementById('questions-error-msg').classList.remove('hidden');
        return;
      }

      document.getElementById('questions-error-msg').classList.add('hidden');
      document.getElementById('screen-questions').classList.add('hidden');
      document.getElementById('screen-results').classList.remove('hidden');

      window.scrollTo({ top: 0, behavior: 'smooth' });

      // Metrik 1: Lesezeit & Anzahl eingeblendeter Benachrichtigungen
      const formattedTime = readingDurationSec.toFixed(1).replace('.', ',');
      document.getElementById('res-reading-time').textContent = `${formattedTime} Sekunden`;
      document.getElementById('res-notif-count').textContent = `Während des Lesens eingeblendete Push-Nachrichten: ${shownNotificationsCount}`;

      // Metrik 2: Freitext-Antwort des Nutzers
      document.getElementById('res-user-freetext').textContent = `„${freetextVal}“`;

      // Metrik 3: Multiple-Choice-Auswertung zur Prüfungsnachricht
      const isCorrect = selectedMcIndex === CONFIG.questions.mcCorrectIndex;
      const badgeEl = document.getElementById('res-mc-badge');
      const selectedTextEl = document.getElementById('res-mc-selected');

      selectedTextEl.textContent = CONFIG.questions.mcOptions[selectedMcIndex];

      if (isCorrect) {
        badgeEl.textContent = "✓ Korrekt erinnert";
        badgeEl.className = "px-3 py-1 rounded-full text-xs font-bold bg-emerald-100 text-emerald-800 border border-emerald-200";
      } else {
        badgeEl.textContent = "✕ Nicht korrekt";
        badgeEl.className = "px-3 py-1 rounded-full text-xs font-bold bg-rose-100 text-rose-800 border border-rose-200";
      }
    }

    // Event-Listener initialisieren
    document.addEventListener('DOMContentLoaded', () => {
      renderConfigToDOM();

      document.getElementById('btn-open-text').addEventListener('click', startReadingScreen);
      document.getElementById('btn-to-questions').addEventListener('click', goToQuestionsScreen);
      document.getElementById('btn-show-results').addEventListener('click', submitQuestionsAndShowResults);

      document.getElementById('input-freetext').addEventListener('input', () => {
        document.getElementById('questions-error-msg').classList.add('hidden');
      });

      document.getElementById('btn-restart').addEventListener('click', () => {
        renderConfigToDOM();
        document.getElementById('screen-results').classList.add('hidden');
        document.getElementById('screen-start').classList.remove('hidden');
        window.scrollTo({ top: 0, behavior: 'smooth' });
      });
    });
  </script>
</body>
</html>
