<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Melodigma · El Misterio de la Escuela Armonía | Estel</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Tipografías Infantiles y de Cuento Musical -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&family=Nunito:wght@400;600;700;800&family=Playfair+Display:ital,wght@0,700;1,600&display=swap" rel="stylesheet" />

  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            crema: '#FDF6EC',
            cremaCard: '#FFFDF9',
            pergamino: '#D8C3A5',
            madera: '#5C3A21',
            maderaSuave: '#8B5A2B',
            lupa: '#4CAF50',
            lupaOscuro: '#388E3C',
            dorado: '#FFD54F',
            doradoOscuro: '#FBC02D',
            celeste: '#4DD0E1',
            coral: '#F48FB1',
            terracota: '#BF5B2B'
          },
          fontFamily: {
            display: ['Fredoka', 'cursive', 'sans-serif'],
            body: ['Nunito', 'sans-serif'],
            serif: ['Playfair Display', 'serif']
          },
          boxShadow: {
            card: '0 8px 20px -4px rgba(92, 58, 33, 0.12)',
            btn: '0 4px 0px rgba(92, 58, 33, 0.25)'
          }
        }
      }
    };
  </script>

  <style>
    body {
      background-color: #FDF6EC;
      background-image:
        radial-gradient(circle at 12% 18%, rgba(77, 208, 225, 0.14) 0px, transparent 140px),
        radial-gradient(circle at 88% 12%, rgba(255, 213, 79, 0.18) 0px, transparent 160px),
        radial-gradient(circle at 82% 85%, rgba(244, 143, 177, 0.14) 0px, transparent 160px),
        radial-gradient(circle at 18% 82%, rgba(76, 175, 80, 0.10) 0px, transparent 150px);
      color: #5C3A21;
      font-family: 'Nunito', sans-serif;
    }

    h1, h2, h3, h4, .font-display {
      font-family: 'Fredoka', cursive, sans-serif;
    }

    @keyframes floatNote {
      0%, 100% { transform: translateY(0px) rotate(-3deg); }
      50% { transform: translateY(-7px) rotate(3deg); }
    }
    .animate-float {
      animation: floatNote 3.5s ease-in-out infinite;
    }

    @keyframes popIn {
      0% { transform: scale(0.95); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }
    .animate-pop {
      animation: popIn 0.28s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
    }

    /* Papel de carta de la directora */
    .letter-paper {
      background: linear-gradient(180deg, #FFFDF7 0%, #FAF0DC 100%);
      border: 3px solid #D8C3A5;
      box-shadow: 0 10px 25px rgba(92, 58, 33, 0.12), inset 0 0 30px rgba(216, 195, 165, 0.25);
    }

    /* Cartel estilo portada 'El Misterio de la Escuela Armonía' */
    .storybook-plaque {
      background: #FFFBF0;
      border: 4px solid #C8A97E;
      box-shadow: 0 6px 0 #C8A97E, 0 12px 24px rgba(92, 58, 33, 0.15);
    }

    /* Scrollbar sutil */
    ::-webkit-scrollbar {
      width: 8px;
      height: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #FDF6EC;
    }
    ::-webkit-scrollbar-thumb {
      background: #D8C3A5;
      border-radius: 9999px;
    }
  </style>
</head>
<body class="min-h-screen flex flex-col overflow-x-hidden selection:bg-dorado selection:text-madera">

  <!-- NOTIFICACIÓN FLOTANTE (TOAST) -->
  <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 max-w-sm pointer-events-none"></div>

  <!-- CABECERA / BARRA DE NAVEGACIÓN PRINCIPAL -->
  <header class="sticky top-0 z-40 bg-[#FFFDF9]/95 backdrop-blur-md border-b-4 border-pergamino shadow-sm">
    <div class="max-w-7xl mx-auto px-3 sm:px-6 py-2.5 flex flex-wrap items-center justify-between gap-3">

      <!-- Logos Flotantes Transparentes: Melodigma (Juego) y Estel (Productora) -->
      <div class="flex items-center gap-3 sm:gap-4">
        <button onclick="switchSection('inicio')" class="flex items-center gap-2.5 group focus:outline-none text-left" title="Ir al inicio de Melodigma">
          <div id="header-logo-melodigma" class="w-32 sm:w-36 h-12 flex items-center justify-center transition-transform group-hover:scale-105"></div>
        </button>

        <div class="hidden md:flex items-center gap-2 pl-3 border-l-2 border-pergamino/60">
          <span class="text-[11px] font-bold uppercase tracking-wider text-maderaSuave">Una producción de</span>
          <div id="header-logo-estel" class="w-20 h-11 flex items-center justify-center"></div>
        </div>
      </div>

      <!-- Menú de Navegación Principal -->
      <nav class="flex flex-wrap items-center gap-1.5 sm:gap-2" aria-label="Navegación principal">
        <button onclick="switchSection('inicio')" id="nav-inicio" class="nav-btn px-3.5 py-2 rounded-2xl font-display font-semibold text-sm sm:text-base transition flex items-center gap-1.5 bg-lupa text-white shadow-btn">
          <span>🏫</span> <span>Inicio</span>
        </button>
        <button onclick="switchSection('juego')" id="nav-juego" class="nav-btn px-3.5 py-2 rounded-2xl font-display font-semibold text-sm sm:text-base transition flex items-center gap-1.5 bg-[#FFF3DF] text-madera hover:bg-dorado/60">
          <span>🎲</span> <span>Juega al Cluedo</span>
        </button>
        <button onclick="switchSection('avatar')" id="nav-avatar" class="nav-btn px-3.5 py-2 rounded-2xl font-display font-semibold text-sm sm:text-base transition flex items-center gap-1.5 bg-[#FFF3DF] text-madera hover:bg-dorado/60">
          <span>🎨</span> <span>Crea tu Avatar</span>
        </button>
        <button onclick="switchSection('transmedia')" id="nav-transmedia" class="nav-btn px-3.5 py-2 rounded-2xl font-display font-semibold text-sm sm:text-base transition flex items-center gap-1.5 bg-[#FFF3DF] text-madera hover:bg-dorado/60">
          <span>✨</span> <span>Universo Transmedia</span>
        </button>
      </nav>
    </div>
  </header>

  <!-- CONTENIDO PRINCIPAL -->
  <main class="flex-grow max-w-7xl w-full mx-auto px-3 sm:px-6 py-6 sm:py-8 space-y-10">

    <!-- ===================================================================== -->
    <!-- SECCIÓN 1: INICIO (PORTADA, CARTA DIRECTORA Y LOS 6 SOSPECHOSOS)      -->
    <!-- ===================================================================== -->
    <section id="sec-inicio" class="space-y-10 animate-pop">

      <!-- HERO DE CUENTO INSPIRADO EN LA PORTADA DE LA ESCUELA ARMONÍA -->
      <div class="relative rounded-3xl bg-gradient-to-br from-[#FFF9EB] via-[#FCEBD2] to-[#F5E0C3] border-4 border-pergamino p-6 sm:p-10 shadow-card overflow-hidden">
        <!-- Notas musicales decorativas flotantes -->
        <span class="hidden sm:block absolute top-5 left-8 text-3xl text-terracota/40 animate-float">♪</span>
        <span class="hidden sm:block absolute top-8 right-12 text-4xl text-celeste/60 animate-float" style="animation-delay: 0.8s">♫</span>
        <span class="hidden sm:block absolute bottom-6 left-1/2 text-3xl text-lupa/40 animate-float" style="animation-delay: 1.4s">♩</span>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-center relative z-10">
          <!-- Texto y Placa Titular -->
          <div class="lg:col-span-7 space-y-5">
            <div class="inline-flex items-center gap-2 bg-white/90 border-2 border-dorado px-4 py-1.5 rounded-full shadow-sm">
              <span class="text-lg">🔍</span>
              <span class="font-display font-bold text-xs sm:text-sm text-madera uppercase tracking-wide">
                Juego de Deducción Musical · 7 a 12 años
              </span>
            </div>

            <div class="storybook-plaque rounded-3xl px-6 py-5 max-w-xl">
              <h1 class="text-3xl sm:text-5xl font-bold text-madera leading-tight text-center">
                EL MISTERIO
                <span class="block text-lg sm:text-xl font-serif italic text-maderaSuave my-1">— de la —</span>
                ESCUELA ARMONÍA
              </h1>
            </div>

            <p class="text-base sm:text-lg text-madera/90 leading-relaxed font-semibold">
              Durante los preparativos del concierto anual ha desaparecido misteriosamente el legendario violín <strong class="text-terracota">"La Aurora"</strong>. Recorre las 9 estancias de la escuela, interroga a los sospechosos internacionales, escucha pistas sonoras y descubre qué se esconde dentro del <strong>Sobre Secreto</strong>.
            </p>

            <div class="flex flex-wrap gap-3 pt-1">
              <button onclick="switchSection('juego')" class="px-6 py-3.5 rounded-2xl bg-lupa hover:bg-lupaOscuro text-white font-display font-bold text-lg shadow-btn transition transform hover:-translate-y-0.5 flex items-center gap-2">
                <span>🕵️‍♀️</span> ¡Jugar al Cluedo Musical!
              </button>
              <button onclick="switchSection('avatar')" class="px-6 py-3.5 rounded-2xl bg-dorado hover:bg-amber-400 text-madera font-display font-bold text-lg shadow-btn transition transform hover:-translate-y-0.5 flex items-center gap-2">
                <span>🎨</span> Crear mi Detective
              </button>
              <button onclick="playMelody('aurora')" class="px-4 py-3.5 rounded-2xl bg-white hover:bg-celeste/20 text-madera border-2 border-celeste font-display font-semibold text-base transition flex items-center gap-2">
                <span>🎻</span> Melodía "La Aurora"
              </button>
            </div>
          </div>

          <!-- Ilustración vectorial de la Escuela Armonía, libros, lupa y el Violín La Aurora -->
          <div class="lg:col-span-5 flex flex-col items-center">
            <div class="w-full max-w-md text-center">
              <svg viewBox="0 0 380 250" class="w-full h-auto drop-shadow-md overflow-visible">
                <!-- Círculos pastel estilo portada -->
                <circle cx="85" cy="60" r="45" fill="#4DD0E1" opacity="0.25" />
                <circle cx="295" cy="65" r="48" fill="#F48FB1" opacity="0.25" />
                <circle cx="190" cy="48" r="40" fill="#FFD54F" opacity="0.30" />

                <!-- Césped y camino -->
                <ellipse cx="190" cy="212" rx="165" ry="26" fill="#8BC34A" />
                <path d="M170 192 Q195 215 155 236 L225 236 Q205 215 210 192 Z" fill="#F3D9B1" />

                <!-- Torres laterales de la Escuela Armonía -->
                <rect x="78" y="96" width="38" height="96" rx="3" fill="#E8C670" stroke="#795548" stroke-width="2.5" />
                <path d="M74 96 A23 23 0 0 1 120 96 Z" fill="#90A4AE" stroke="#546E7A" stroke-width="2.5" />
                <rect x="264" y="96" width="38" height="96" rx="3" fill="#E8C670" stroke="#795548" stroke-width="2.5" />
                <path d="M260 96 A23 23 0 0 1 306 96 Z" fill="#90A4AE" stroke="#546E7A" stroke-width="2.5" />

                <!-- Cuerpo principal de la Escuela -->
                <rect x="116" y="106" width="148" height="86" fill="#F6DC8C" stroke="#795548" stroke-width="2.5" />
                <polygon points="108,106 190,62 272,106" fill="#E5BE5E" stroke="#795548" stroke-width="2.5" />
                <circle cx="190" cy="87" r="10" fill="#FFF8EB" stroke="#795548" stroke-width="2" />

                <!-- Ventanas azules -->
                <rect x="136" y="122" width="18" height="22" rx="2" fill="#29B6F6" stroke="#5D4037" stroke-width="2" />
                <rect x="181" y="122" width="18" height="22" rx="2" fill="#29B6F6" stroke="#5D4037" stroke-width="2" />
                <rect x="226" y="122" width="18" height="22" rx="2" fill="#29B6F6" stroke="#5D4037" stroke-width="2" />

                <!-- Puerta principal -->
                <path d="M174 192 L174 162 A16 16 0 0 1 206 162 L206 192 Z" fill="#263238" stroke="#5D4037" stroke-width="2.5" />

                <!-- Pila de libros musicales (izquierda) -->
                <g transform="translate(22, 168)">
                  <rect x="0" y="34" width="66" height="14" rx="4" fill="#F06292" stroke="#5C3A21" stroke-width="2" />
                  <rect x="4" y="21" width="64" height="13" rx="4" fill="#3F51B5" stroke="#5C3A21" stroke-width="2" />
                  <rect x="2" y="8" width="66" height="13" rx="4" fill="#FF7043" stroke="#5C3A21" stroke-width="2" />
                  <rect x="10" y="-4" width="60" height="12" rx="4" fill="#FFD54F" stroke="#5C3A21" stroke-width="2" />
                </g>

                <!-- Lupa gigante (arriba derecha) -->
                <g transform="translate(312, 42) rotate(-35)">
                  <rect x="-5" y="24" width="10" height="32" rx="4" fill="#A1887F" stroke="#4E342E" stroke-width="2.5" />
                  <circle cx="0" cy="0" r="24" fill="#B2EBF2" stroke="#E69D45" stroke-width="6" />
                  <path d="M-11 -9 A15 15 0 0 1 4 -14" fill="none" stroke="#FFFFFF" stroke-width="3" stroke-linecap="round" />
                </g>

                <!-- Violín La Aurora en primer plano (derecha) -->
                <g transform="translate(310, 178) rotate(22)">
                  <ellipse cx="0" cy="24" rx="22" ry="26" fill="#BF5B2B" stroke="#4E342E" stroke-width="2.5" />
                  <ellipse cx="0" cy="-4" rx="16" ry="20" fill="#BF5B2B" stroke="#4E342E" stroke-width="2.5" />
                  <rect x="-4" y="-56" width="8" height="52" fill="#4E342E" />
                  <circle cx="0" cy="-60" r="6" fill="#8D5524" stroke="#4E342E" stroke-width="2" />
                  <line x1="-2" y1="-52" x2="-2" y2="34" stroke="#FFD54F" stroke-width="1.3" />
                  <line x1="2" y1="-52" x2="2" y2="34" stroke="#FFD54F" stroke-width="1.3" />
                </g>
              </svg>
              <!-- Logos flotantes transparentes debajo de la ilustración -->
              <div class="flex items-center justify-center gap-4 -mt-2">
                <div id="hero-logo-melodigma" class="w-32 h-11"></div>
                <div id="hero-logo-estel" class="w-20 h-11"></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- CARTA DE LA DIRECTORA DOÑA BEATRIZ VALCÁRCEL -->
      <div class="letter-paper rounded-3xl p-6 sm:p-8 relative">
        <div class="flex flex-col md:flex-row gap-6 items-start">
          <div class="flex-shrink-0 mx-auto md:mx-0 text-center">
            <!-- Retrato flotante transparente sin fondo -->
            <div id="director-letter-portrait" class="w-32 h-40 flex items-center justify-center drop-shadow-md"></div>
            <span class="inline-block mt-1 text-xs font-extrabold bg-rose-100 text-rose-800 px-3 py-1 rounded-full border border-rose-200">
              Directora · 62 años
            </span>
          </div>
          <div class="space-y-3 text-madera">
            <div class="flex flex-wrap items-center justify-between gap-2 border-b-2 border-pergamino/60 pb-2">
              <h2 class="text-2xl sm:text-3xl font-bold text-madera flex items-center gap-2">
                <span>📜</span> Una carta de la directora
              </h2>
              <span class="text-xs font-bold uppercase tracking-wider text-maderaSuave">Archivo Confidencial · Escuela Armonía</span>
            </div>
            <p class="font-serif italic text-lg text-maderaSuave">"Queridos detectives,</p>
            <p class="text-sm sm:text-base leading-relaxed">
              Soy <strong>Doña Beatriz Valcárcel</strong>, directora de la Escuela de Música Armonía. Durante muchos años, nuestra escuela ha sido un lugar lleno de música, aprendizaje y talento. Por sus pasillos han pasado cientos de alumnos y profesores.
            </p>
            <p class="text-sm sm:text-base leading-relaxed">
              Sin embargo, últimamente han ocurrido cosas bastante extrañas. Algunos comportamientos me hacen sospechar que no todo el mundo está siendo tan sincero como parece... Por eso, he decidido confiaros una misión muy especial: investigar lo que está sucediendo en nuestra escuela y descubrir la verdad.
            </p>
            <p class="text-sm sm:text-base leading-relaxed font-bold text-terracota">
              No os dejéis engañar por las apariencias, aquí todos tienen algo que contar. ¡Que comience la investigación!"
            </p>
            <p class="font-serif italic font-bold text-right text-madera pt-1">— Doña Beatriz Valcárcel</p>
          </div>
        </div>
      </div>

      <!-- LOS 6 SOSPECHOSOS ACTUALIZADOS (ILUSTRACIONES FLOTANTES TRANSPARENTES SIN FONDO) -->
      <div class="space-y-4">
        <div class="flex flex-wrap items-end justify-between gap-3">
          <div>
            <span class="text-xs font-extrabold uppercase tracking-wider text-lupaOscuro bg-green-100 px-3 py-1 rounded-full">Reparto Internacional Oficial</span>
            <h2 class="text-2xl sm:text-3xl font-bold text-madera mt-1">Conoce a los 6 Sospechosos de Armonía</h2>
          </div>
          <p class="text-sm text-maderaSuave font-semibold">
            ✨ Haz clic en <strong>"Personalizar estilo"</strong> para editar cualquier personaje en el creador.
          </p>
        </div>

        <div id="characters-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
          <!-- Renderizado dinámicamente en JS -->
        </div>
      </div>

      <!-- LAS 9 ESTANCIAS DE LA ESCUELA ARMONÍA -->
      <div class="space-y-4">
        <div>
          <span class="text-xs font-extrabold uppercase tracking-wider text-cyan-800 bg-cyan-100 px-3 py-1 rounded-full">El Tablero de Investigación</span>
          <h2 class="text-2xl sm:text-3xl font-bold text-madera mt-1">Explora las 9 Estancias de la Escuela Armonía</h2>
        </div>
        <div id="rooms-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
          <!-- Renderizado dinámicamente en JS -->
        </div>
      </div>
    </section>

    <!-- ===================================================================== -->
    <!-- SECCIÓN 2: JUEGO CLUEDO ONLINE INTERACTIVO                            -->
    <!-- ===================================================================== -->
    <section id="sec-juego" class="hidden space-y-6 animate-pop">

      <!-- Cabecera del Juego -->
      <div class="bg-white rounded-3xl p-5 border-4 border-pergamino shadow-card flex flex-wrap items-center justify-between gap-4">
        <div>
          <h2 class="text-2xl sm:text-3xl font-bold text-madera flex items-center gap-2">
            <span>🎲</span> Melodigma Online: El Robo en la Escuela Armonía
          </h2>
          <p class="text-sm text-maderaSuave font-semibold">
            Muévete por el tablero, entra en las estancias, formula hipótesis y descubre qué hay en el <strong>Sobre Secreto</strong>.
          </p>
        </div>
        <div class="flex flex-wrap items-center gap-2">
          <button onclick="openNewGameModal()" class="px-4 py-2.5 rounded-2xl bg-dorado hover:bg-amber-400 text-madera font-display font-bold text-sm shadow-btn transition">
            🔄 Nueva Partida
          </button>
          <button onclick="openAccusationModal()" id="btn-accuse" class="px-4 py-2.5 rounded-2xl bg-rose-500 hover:bg-rose-600 text-white font-display font-bold text-sm shadow-btn transition">
            ✉️ ¡Acusación Final!
          </button>
        </div>
      </div>

      <!-- Panel de Selección de Personaje para Empezar -->
      <div id="game-setup-panel" class="bg-white rounded-3xl p-6 sm:p-8 border-4 border-lupa shadow-card space-y-6">
        <div class="text-center max-w-2xl mx-auto space-y-2">
          <span class="inline-block bg-green-100 text-lupaOscuro font-extrabold text-xs px-3 py-1 rounded-full uppercase">Preparación del Caso</span>
          <h3 class="text-2xl sm:text-3xl font-bold text-madera">Elige tu Detective para Investigar</h3>
          <p class="text-sm text-maderaSuave font-semibold">
            Se guardarán 3 cartas al azar en el <strong>Sobre Secreto</strong> (Culpable, Instrumento robado y Escondite) y las demás se repartirán entre los 4 detectives en partida.
          </p>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 max-w-2xl mx-auto">
          <label class="flex items-center gap-3 p-3.5 rounded-2xl border-2 border-dorado bg-amber-50/70 cursor-pointer">
            <input type="radio" name="gameMode" value="aurora" checked class="w-5 h-5 accent-lupa" />
            <div>
              <p class="font-display font-bold text-madera">🎻 Caso Principal: El Violín "La Aurora"</p>
              <p class="text-xs text-maderaSuave">Investiga el robo del violín histórico y los instrumentos implicados.</p>
            </div>
          </label>
          <label class="flex items-center gap-3 p-3.5 rounded-2xl border-2 border-celeste bg-cyan-50/60 cursor-pointer">
            <input type="radio" name="gameMode" value="clasico" class="w-5 h-5 accent-lupa" />
            <div>
              <p class="font-display font-bold text-madera">🎼 Modo Clásico: Todos los Instrumentos</p>
              <p class="text-xs text-maderaSuave">Cualquiera de los 7 instrumentos de la escuela puede haber desaparecido.</p>
            </div>
          </label>
        </div>

        <div id="setup-character-choices" class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-6 gap-4">
          <!-- Se rellena con los 6 detectives y el avatar personalizado si existe -->
        </div>
      </div>

      <!-- ÁREA PRINCIPAL DEL JUEGO ACTIVO -->
      <div id="game-active-area" class="hidden grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">

        <!-- COLUMNA IZQUIERDA: TABLERO DE LA ESCUELA ARMONÍA (7 cols) -->
        <div class="lg:col-span-7 space-y-4">
          <div class="bg-white rounded-3xl p-4 sm:p-5 border-4 border-pergamino shadow-card">
            <!-- Barra de estado de turno -->
            <div class="flex flex-wrap items-center justify-between gap-3 mb-4 pb-3 border-b-2 border-pergamino">
              <div class="flex items-center gap-3">
                <div id="turn-avatar-badge" class="w-11 h-11 rounded-2xl flex items-center justify-center font-display font-bold text-white text-lg shadow"></div>
                <div>
                  <p class="text-xs font-extrabold uppercase text-maderaSuave">Turno Actual</p>
                  <p id="turn-player-name" class="font-display font-bold text-lg text-madera">Luana Pereira (Tú)</p>
                </div>
              </div>

              <div class="flex items-center gap-2">
                <div id="dice-display" class="flex items-center gap-1.5 bg-crema px-3 py-1.5 rounded-2xl border-2 border-pergamino font-display font-bold text-lg text-madera">
                  <span>🎲</span> <span id="dice-values">-</span>
                </div>
                <button id="btn-roll-dice" onclick="rollDice()" class="px-4 py-2.5 rounded-2xl bg-lupa hover:bg-lupaOscuro text-white font-display font-bold text-sm shadow-btn transition">
                  🎲 Tirar Dados
                </button>
                <button id="btn-end-turn" onclick="endPlayerTurn()" class="hidden px-4 py-2.5 rounded-2xl bg-madera hover:bg-maderaSuave text-white font-display font-bold text-sm shadow-btn transition">
                  ⏭️ Pasar Turno
                </button>
              </div>
            </div>

            <!-- Instrucción dinámica de movimiento -->
            <div id="game-instruction-banner" class="mb-3 px-4 py-2.5 rounded-2xl bg-amber-50 border-2 border-dorado text-xs sm:text-sm font-bold text-madera flex items-center justify-between gap-2">
              <span id="instruction-text">Pulsa "Tirar Dados" para empezar a moverte por la Escuela Armonía.</span>
              <span id="steps-remaining-badge" class="hidden px-2.5 py-0.5 rounded-full bg-lupa text-white text-xs font-extrabold whitespace-nowrap"></span>
            </div>

            <!-- TABLERO INTERACTIVO 11x11 -->
            <div class="w-full overflow-x-auto pb-1">
              <div id="cluedo-board-grid" class="grid grid-cols-11 gap-1 min-w-[330px] max-w-[560px] mx-auto bg-[#E9D8BE] p-2 rounded-2xl border-4 border-madera shadow-inner select-none">
                <!-- Celdas renderizadas por JS -->
              </div>
            </div>

            <!-- Leyenda rápida del tablero -->
            <div class="mt-3 flex flex-wrap items-center justify-center gap-4 text-xs font-bold text-maderaSuave">
              <span class="flex items-center gap-1"><span class="w-3.5 h-3.5 rounded bg-emerald-200 border border-emerald-600 inline-block"></span> Casilla accesible</span>
              <span class="flex items-center gap-1"><span class="w-3.5 h-3.5 rounded bg-amber-300 border border-amber-700 inline-block"></span> ❓ Carta de Ayuda</span>
              <span class="flex items-center gap-1"><span class="w-3.5 h-3.5 rounded bg-madera inline-block"></span> 🚪 Puerta de Estancia</span>
            </div>
          </div>

          <!-- REGISTRO DE INVESTIGACIÓN (BITÁCORA EN VIVO) -->
          <div class="bg-white rounded-3xl p-4 sm:p-5 border-4 border-pergamino shadow-card">
            <h4 class="font-display font-bold text-base text-madera mb-2 flex items-center gap-2">
              <span>🗞️</span> Crónica de la Investigación
            </h4>
            <div id="game-log-list" class="h-36 overflow-y-auto space-y-1.5 pr-1 text-xs sm:text-sm">
              <!-- Mensajes de partida -->
            </div>
          </div>
        </div>

        <!-- COLUMNA DERECHA: CARTAS DEL JUGADOR Y HOJA DE INVESTIGACIÓN (5 cols) -->
        <div class="lg:col-span-5 space-y-4">

          <!-- Mis Cartas en Mano + Cartas de Ayuda -->
          <div class="bg-white rounded-3xl p-4 sm:p-5 border-4 border-pergamino shadow-card space-y-3">
            <div class="flex items-center justify-between">
              <h4 class="font-display font-bold text-lg text-madera flex items-center gap-2">
                <span>🃏</span> Tus Cartas Secretas
              </h4>
              <span class="text-xs font-bold text-maderaSuave bg-crema px-2.5 py-1 rounded-full border border-pergamino">Descartadas automáticamente</span>
            </div>
            <div id="player-hand-cards" class="grid grid-cols-2 sm:grid-cols-3 gap-2">
              <!-- Cartas repartidas al jugador -->
            </div>

            <!-- Cartas de Ayuda obtenidas -->
            <div id="player-help-cards-box" class="hidden pt-2 border-t-2 border-pergamino">
              <p class="text-xs font-extrabold uppercase text-amber-800 mb-1.5">✨ Tus Cartas de Ayuda:</p>
              <div id="player-help-cards" class="space-y-1.5"></div>
            </div>
          </div>

          <!-- HOJA DE INVESTIGACIÓN INTERACTIVA -->
          <div class="letter-paper rounded-3xl p-4 sm:p-5 space-y-3">
            <div class="flex items-center justify-between border-b-2 border-pergamino pb-2">
              <div>
                <h4 class="font-display font-bold text-lg text-madera flex items-center gap-1.5">
                  <span>📋</span> Hoja de Detective
                </h4>
                <p class="text-[11px] text-maderaSuave font-semibold">Haz clic en cada fila para marcar: ⬜ Dudoso · ❌ Descartado · ⭐ Sospechoso</p>
              </div>
              <button onclick="openAccusationModal()" class="px-3 py-1.5 rounded-xl bg-rose-500 hover:bg-rose-600 text-white font-display font-bold text-xs shadow">
                Acusar
              </button>
            </div>

            <div id="detective-notebook" class="space-y-3 max-h-[430px] overflow-y-auto pr-1 text-xs sm:text-sm">
              <!-- Checklist generada en JS -->
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ===================================================================== -->
    <!-- SECCIÓN 3: GENERADOR DE AVATARES (EXPEDIENTES ARMONÍA - SIN FONDO)    -->
    <!-- ===================================================================== -->
    <section id="sec-avatar" class="hidden space-y-8 animate-pop">

      <div class="bg-white rounded-3xl p-6 sm:p-8 border-4 border-pergamino shadow-card">
        <div class="flex flex-wrap items-center justify-between gap-4 border-b-2 border-pergamino pb-4 mb-6">
          <div>
            <span class="text-xs font-extrabold uppercase tracking-wider text-purple-800 bg-purple-100 px-3 py-1 rounded-full">Expedientes Armonía · Espacio Fandom</span>
            <h2 class="text-2xl sm:text-3xl font-bold text-madera mt-1">Creador de Avatares Cabeza Cuadrada</h2>
            <p class="text-sm text-maderaSuave font-semibold">
              Diseña tu propio detective o parte de uno de los 6 personajes oficiales. Guárdalo como tu <strong>Perfil de Detective</strong> para jugar con él en el Cluedo o envíalo a la galería del concurso.
            </p>
          </div>
          <!-- Presets rápidos de los 6 personajes -->
          <div class="flex flex-wrap gap-1.5">
            <span class="text-xs font-bold text-maderaSuave w-full mb-0.5">Cargar plantilla de personaje:</span>
            <button onclick="applyAvatarPreset('luana')" class="px-3 py-1.5 rounded-xl bg-emerald-100 hover:bg-emerald-200 text-emerald-900 font-bold text-xs">🇧🇷 Luana</button>
            <button onclick="applyAvatarPreset('liwei')" class="px-3 py-1.5 rounded-xl bg-red-100 hover:bg-red-200 text-red-900 font-bold text-xs">🇨🇳 Li Wei</button>
            <button onclick="applyAvatarPreset('emese')" class="px-3 py-1.5 rounded-xl bg-purple-100 hover:bg-purple-200 text-purple-900 font-bold text-xs">🇭🇺 Emese</button>
            <button onclick="applyAvatarPreset('diego')" class="px-3 py-1.5 rounded-xl bg-amber-100 hover:bg-amber-200 text-amber-900 font-bold text-xs">🇧🇴 Diego</button>
            <button onclick="applyAvatarPreset('arjun')" class="px-3 py-1.5 rounded-xl bg-sky-100 hover:bg-sky-200 text-sky-900 font-bold text-xs">🇮🇳 Arjun</button>
            <button onclick="applyAvatarPreset('beatriz')" class="px-3 py-1.5 rounded-xl bg-rose-100 hover:bg-rose-200 text-rose-900 font-bold text-xs">🇪🇸 Directora</button>
          </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
          <!-- Vista Previa Flotante Sin Fondo -->
          <div class="lg:col-span-5 flex flex-col items-center space-y-4">
            <div class="w-full max-w-[300px] aspect-[3/4] flex items-center justify-center p-2 relative">
              <div id="avatar-preview-svg" class="w-full h-full flex items-center justify-center drop-shadow-md"></div>
            </div>

            <div class="w-full max-w-[340px] space-y-2.5">
              <input id="avatar-name-input" type="text" value="Detective Armonía" placeholder="Nombre de tu detective..."
                class="w-full px-4 py-2.5 rounded-2xl border-2 border-pergamino bg-crema font-display font-bold text-center text-madera focus:outline-none focus:border-lupa" />

              <button onclick="applyCustomAvatarAsProfile()" class="w-full py-3 px-5 rounded-2xl bg-lupa hover:bg-lupaOscuro text-white font-display font-bold text-base shadow-btn transition flex items-center justify-center gap-2">
                <span>🕵️‍♀️</span> Usar como mi Perfil de Detective
              </button>

              <button onclick="saveAvatarToGallery()" class="w-full py-2.5 px-5 rounded-2xl bg-dorado hover:bg-amber-400 text-madera font-display font-bold text-sm shadow-btn transition flex items-center justify-center gap-2">
                <span>🏆</span> Publicar en la Galería del Concurso
              </button>
            </div>
          </div>

          <!-- Controles de Personalización -->
          <div class="lg:col-span-7 grid grid-cols-1 sm:grid-cols-2 gap-4">
            <!-- Tono de piel -->
            <div class="bg-crema rounded-2xl p-4 border-2 border-pergamino space-y-2">
              <label class="font-display font-bold text-sm text-madera block">1. Tono de piel</label>
              <div class="flex flex-wrap gap-2" id="ctrl-skin"></div>
            </div>

            <!-- Peinado -->
            <div class="bg-crema rounded-2xl p-4 border-2 border-pergamino space-y-2">
              <label class="font-display font-bold text-sm text-madera block">2. Peinado o Gorra</label>
              <select id="ctrl-hair" onchange="updateAvatarFromControls()" class="w-full p-2.5 rounded-xl border-2 border-pergamino bg-white font-bold text-sm text-madera">
                <option value="curly">Melena ondulada (Estilo Luana)</option>
                <option value="straight">Flequillo recto liso (Estilo Li Wei)</option>
                <option value="ponytail">Coleta alta con coletero (Estilo Emese)</option>
                <option value="cap">Gorra urbana hacia atrás (Estilo Diego)</option>
                <option value="eccentric">Pelo alborotado creativo (Estilo Arjun)</option>
                <option value="bun">Moño elegante de directora (Estilo Beatriz)</option>
              </select>
            </div>

            <!-- Color de pelo -->
            <div class="bg-crema rounded-2xl p-4 border-2 border-pergamino space-y-2">
              <label class="font-display font-bold text-sm text-madera block">3. Color de cabello</label>
              <div class="flex flex-wrap gap-2" id="ctrl-haircolor"></div>
            </div>

            <!-- Expresión / Ojos -->
            <div class="bg-crema rounded-2xl p-4 border-2 border-pergamino space-y-2">
              <label class="font-display font-bold text-sm text-madera block">4. Expresión de detective</label>
              <select id="ctrl-eyes" onchange="updateAvatarFromControls()" class="w-full p-2.5 rounded-xl border-2 border-pergamino bg-white font-bold text-sm text-madera">
                <option value="happy">Sonrisa alegre (‿ ‿)</option>
                <option value="determined">Mirada investigadora (╲ ╱)</option>
                <option value="calm">Concentración serena (— —)</option>
                <option value="glasses">Gafas redondas de músico (O-O)</option>
              </select>
            </div>

            <!-- Vestuario -->
            <div class="bg-crema rounded-2xl p-4 border-2 border-pergamino space-y-2">
              <label class="font-display font-bold text-sm text-madera block">5. Vestuario de la Escuela</label>
              <select id="ctrl-outfit" onchange="updateAvatarFromControls()" class="w-full p-2.5 rounded-xl border-2 border-pergamino bg-white font-bold text-sm text-madera">
                <option value="sweater">Jersey con nota musical + Falda</option>
                <option value="uniform">Uniforme clásico Escuela Armonía</option>
                <option value="hoodie">Sudadera cómoda de ensayo</option>
                <option value="jacket">Chaqueta abierta urbana</option>
                <option value="professor">Traje de profesor con corbata</option>
                <option value="director">Conjunto de Directora con carpeta</option>
              </select>
            </div>

            <!-- Color principal de ropa -->
            <div class="bg-crema rounded-2xl p-4 border-2 border-pergamino space-y-2">
              <label class="font-display font-bold text-sm text-madera block">6. Color del vestuario</label>
              <div class="flex flex-wrap gap-2" id="ctrl-outfitcolor"></div>
            </div>

            <!-- Instrumento / Accesorio -->
            <div class="bg-crema rounded-2xl p-4 border-2 border-pergamino space-y-2 sm:col-span-2">
              <label class="font-display font-bold text-sm text-madera block">7. Instrumento o Herramienta de Detective</label>
              <div class="grid grid-cols-2 sm:grid-cols-4 gap-2" id="ctrl-item"></div>
            </div>

            <!-- Notas musicales flotantes -->
            <div class="bg-crema rounded-2xl p-4 border-2 border-pergamino sm:col-span-2 flex items-center justify-between">
              <div>
                <p class="font-display font-bold text-sm text-madera">8. Notas musicales alrededor del personaje</p>
                <p class="text-xs text-maderaSuave">Añade las líneas de movimiento y corcheas características del diseño.</p>
              </div>
              <input id="ctrl-notes" type="checkbox" checked onchange="updateAvatarFromControls()" class="w-6 h-6 accent-lupa cursor-pointer" />
            </div>
          </div>
        </div>
      </div>

      <!-- GALERÍA DEL CONCURSO FANDOM -->
      <div class="bg-white rounded-3xl p-6 sm:p-8 border-4 border-dorado shadow-card space-y-5">
        <div class="flex flex-wrap items-center justify-between gap-4">
          <div>
            <span class="text-xs font-extrabold uppercase bg-amber-100 text-amber-900 px-3 py-1 rounded-full">Concurso Oficial para Niños (7-12 años)</span>
            <h3 class="text-2xl font-bold text-madera mt-1">🏆 Galería de Detectives y Concurso de Dibujos</h3>
            <p class="text-sm text-maderaSuave font-semibold">
              ¡Crea tu personaje digitalmente o sube tu dibujo hecho a mano! El detective ganador protagonizará el próximo episodio de la webserie en YouTube Kids.
            </p>
          </div>
          <label class="px-4 py-2.5 rounded-2xl bg-celeste/30 hover:bg-celeste/50 border-2 border-celeste text-madera font-display font-bold text-sm cursor-pointer transition">
            🖍️ Subir dibujo hecho a mano
            <input type="file" accept="image/*" id="fan-drawing-upload" onchange="submitFanDrawing()" class="hidden" />
          </label>
        </div>

        <div id="avatar-gallery-grid" class="grid grid-cols-2 sm:grid-cols-4 gap-4">
          <!-- Avatares guardados por fans -->
        </div>
      </div>
    </section>

    <!-- ===================================================================== -->
    <!-- SECCIÓN 4: UNIVERSO TRANSMEDIA (EXPANSIONES DEL PROYECTO)             -->
    <!-- ===================================================================== -->
    <section id="sec-transmedia" class="hidden space-y-6 animate-pop">

      <!-- Cabecera Universo Transmedia -->
      <div class="bg-gradient-to-r from-[#E0F7FA] via-[#FFF8EB] to-[#FFF3E0] rounded-3xl p-6 sm:p-8 border-4 border-celeste shadow-card">
        <div class="flex flex-wrap items-center justify-between gap-4">
          <div class="max-w-3xl space-y-2">
            <span class="text-xs font-extrabold uppercase tracking-wider bg-celeste/30 text-cyan-950 px-3 py-1 rounded-full">Estrategia Transmedia · Productora Estel</span>
            <h2 class="text-2xl sm:text-4xl font-bold text-madera">El Universo Expandido de Melodigma</h2>
            <p class="text-sm sm:text-base text-madera/90 font-semibold">
              Explora todas las plataformas y medios donde crece la historia de la <strong>Escuela de Música Armonía</strong>: desde el juego de mesa físico hasta la webserie en YouTube Kids, el libro interactivo con códigos QR, el podcast divulgativo, la película precuela y el espacio fandom.
            </p>
          </div>
          <div id="transmedia-logos-box" class="flex items-center gap-3 p-1"></div>
        </div>

        <!-- Submenú de Pestañas Transmedia -->
        <div class="flex flex-wrap gap-2 mt-6 pt-4 border-t-2 border-madera/10">
          <button onclick="switchTransmediaTab('mesa')" id="tm-tab-mesa" class="tm-tab px-4 py-2 rounded-2xl font-display font-bold text-sm bg-madera text-white shadow">
            🎲 Juego de Mesa (Core)
          </button>
          <button onclick="switchTransmediaTab('webserie')" id="tm-tab-webserie" class="tm-tab px-4 py-2 rounded-2xl font-display font-bold text-sm bg-white text-madera hover:bg-dorado/40 border border-pergamino">
            📺 Webserie YouTube Kids
          </button>
          <button onclick="switchTransmediaTab('libro')" id="tm-tab-libro" class="tm-tab px-4 py-2 rounded-2xl font-display font-bold text-sm bg-white text-madera hover:bg-dorado/40 border border-pergamino">
            📖 Libro con QR Musicales
          </button>
          <button onclick="switchTransmediaTab('podcast')" id="tm-tab-podcast" class="tm-tab px-4 py-2 rounded-2xl font-display font-bold text-sm bg-white text-madera hover:bg-dorado/40 border border-pergamino">
            🎧 Ficción Sonora / Podcast
          </button>
          <button onclick="switchTransmediaTab('pelicula')" id="tm-tab-pelicula" class="tm-tab px-4 py-2 rounded-2xl font-display font-bold text-sm bg-white text-madera hover:bg-dorado/40 border border-pergamino">
            🎬 Película Precuela
          </button>
          <button onclick="switchTransmediaTab('fandom')" id="tm-tab-fandom" class="tm-tab px-4 py-2 rounded-2xl font-display font-bold text-sm bg-white text-madera hover:bg-dorado/40 border border-pergamino">
            🌟 Fandom y Reglas
          </button>
        </div>
      </div>

      <!-- PANEL 1: JUEGO DE MESA FÍSICO -->
      <div id="tm-panel-mesa" class="tm-panel bg-white rounded-3xl p-6 sm:p-8 border-4 border-pergamino shadow-card space-y-6">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-center">
          <div class="lg:col-span-7 space-y-3">
            <span class="text-xs font-extrabold uppercase bg-green-100 text-lupaOscuro px-3 py-1 rounded-full">Experiencia Principal · Campaña de Navidad</span>
            <h3 class="text-2xl sm:text-3xl font-bold text-madera">Juego de Mesa "Melodigma: El Misterio de la Escuela Armonía"</h3>
            <p class="text-sm sm:text-base text-madera/90 leading-relaxed">
              Diseñado para <strong>6 jugadores</strong> de entre <strong>7 y 12 años</strong> (partidas de 30 a 50 minutos). Cada partida plantea una combinación distinta oculta en el <strong>Sobre Secreto</strong>: ¿quién robó el instrumento, cuál fue y en qué estancia lo escondió?
            </p>
            <div class="grid grid-cols-2 sm:grid-cols-3 gap-2.5 pt-2 text-xs font-bold">
              <div class="bg-crema p-3 rounded-2xl border border-pergamino">🗺️ Tablero Escuela Armonía (9 salas)</div>
              <div class="bg-crema p-3 rounded-2xl border border-pergamino">♟️ 6 Fichas ilustradas por colores</div>
              <div class="bg-crema p-3 rounded-2xl border border-pergamino">🃏 6 Cartas de Sospechosos</div>
              <div class="bg-crema p-3 rounded-2xl border border-pergamino">🎻 Cartas de Instrumentos</div>
              <div class="bg-crema p-3 rounded-2xl border border-pergamino">✨ 12 Cartas de Ayuda</div>
              <div class="bg-crema p-3 rounded-2xl border border-pergamino">✉️ Sobre Secreto y Hojas</div>
            </div>
          </div>
          <div class="lg:col-span-5 bg-crema rounded-3xl p-5 border-2 border-dorado space-y-3">
            <h4 class="font-display font-bold text-lg text-madera">✨ Las 12 Cartas de Ayuda del Juego</h4>
            <ul class="text-xs space-y-1.5 text-madera/90 max-h-60 overflow-y-auto pr-1">
              <li><strong>🏃 Movimiento:</strong> ¡Atajo secreto! (+2 casillas), ¡Camino despejado! (repetir dado), ¡Pasillo libre! (entrar sin dado exacto), ¡Un paso adelante! (movimiento extra).</li>
              <li><strong>🔍 Investigación:</strong> ¡Oído atento! (preguntar instrumento), ¡Mirada de detective! (preguntar personaje), ¡Archivo secreto! (ver carta de lugar al azar), ¡Pista inesperada! (pregunta adicional).</li>
              <li><strong>⚡ Especiales:</strong> ¡Silencio en la escuela! (bloquea ayudas de un rival), ¡Suerte de principiante! (relanzar si no entras), ¡Detective astuto! (doble hipótesis), ¡Información privilegiada! (ver carta al azar).</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- PANEL 2: WEBSERIE YOUTUBE KIDS -->
      <div id="tm-panel-webserie" class="tm-panel hidden bg-white rounded-3xl p-6 sm:p-8 border-4 border-pergamino shadow-card space-y-6">
        <div class="flex flex-wrap items-center justify-between gap-4 border-b-2 border-pergamino pb-4">
          <div>
            <span class="text-xs font-extrabold uppercase bg-red-100 text-red-800 px-3 py-1 rounded-full">YouTube Kids · Episodios Especiales</span>
            <h3 class="text-2xl sm:text-3xl font-bold text-madera mt-1">Webserie: "Los Secretos de Armonía y el Armario Musical"</h3>
            <p class="text-sm text-maderaSuave font-semibold">
              Episodios breves de animación para fechas señaladas (Halloween, Navidad, Carnaval, Pascua). Un misterioso <strong>armario mágico</strong> transporta a los alumnos al país de origen de cada personaje para descubrir su cultura musical.
            </p>
          </div>
          <button onclick="playWebseriesIntro()" class="px-5 py-3 rounded-2xl bg-red-500 hover:bg-red-600 text-white font-display font-bold text-sm shadow-btn transition flex items-center gap-2">
            <span>▶️</span> Ver Cabecera / Intro Oficial
          </button>
        </div>

        <!-- Reproductor Simulado de Intro de Webserie -->
        <div id="webseries-intro-player" class="hidden rounded-3xl bg-gradient-to-br from-[#1B5E20] via-[#006064] to-[#3E2723] text-white p-6 sm:p-8 text-center space-y-4 border-4 border-dorado shadow-lg">
          <p class="text-xs uppercase tracking-widest text-dorado font-extrabold">Cabecera Oficial · Estel Presenta</p>
          <div class="flex flex-wrap items-center justify-center gap-6 py-2">
            <div class="p-1" id="intro-estel-box"></div>
            <span class="text-3xl">✨🚪🎻✨</span>
            <div class="p-1" id="intro-melodigma-box"></div>
          </div>
          <h4 class="font-display text-2xl sm:text-3xl font-bold text-dorado">"¡Abre el armario y sigue la melodía!"</h4>
          <p class="text-sm text-white/90 max-w-xl mx-auto">
            ♪ Suena la sintonía principal de <em>Los Secretos de Armonía</em>: una fusión de percusión brasileña, erhu chino, violín húngaro, zampoña boliviana, sitar indio y guitarra española.
          </p>
          <button onclick="document.getElementById('webseries-intro-player').classList.add('hidden')" class="px-4 py-1.5 rounded-xl bg-white/20 hover:bg-white/30 text-xs font-bold">
            Cerrar reproductor
          </button>
        </div>

        <!-- Carteles y Sinopsis de Episodios Especiales -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
          <div class="rounded-3xl bg-gradient-to-b from-purple-900 to-indigo-950 text-white p-5 border-4 border-amber-400 flex flex-col justify-between space-y-3">
            <div>
              <span class="text-[11px] font-extrabold uppercase bg-amber-400 text-madera px-2.5 py-0.5 rounded-full">Especial Halloween</span>
              <h4 class="font-display font-bold text-xl mt-2 text-amber-300">Ep. 1: La Danza Macabra de Budapest</h4>
              <p class="text-xs text-white/85 mt-2 leading-relaxed">
                El armario se abre en plena noche de brujas y lleva a <strong>Nagy Emese</strong> y sus amigos a Hungría, donde un violín zíngaro suena solo en un castillo antiguo.
              </p>
            </div>
            <button onclick="playMelody('hungria')" class="w-full py-2 rounded-xl bg-amber-400 text-madera font-display font-bold text-xs">🎵 Escuchar tema del episodio</button>
          </div>

          <div class="rounded-3xl bg-gradient-to-b from-red-800 to-emerald-900 text-white p-5 border-4 border-dorado flex flex-col justify-between space-y-3">
            <div>
              <span class="text-[11px] font-extrabold uppercase bg-dorado text-madera px-2.5 py-0.5 rounded-full">Especial Navidad</span>
              <h4 class="font-display font-bold text-xl mt-2 text-dorado">Ep. 2: Villancicos entre Farolillos</h4>
              <p class="text-xs text-white/85 mt-2 leading-relaxed">
                <strong>Li Wei</strong> guía al grupo a través del armario hasta un festival invernal en China para recuperar las partituras navideñas perdidas de la Escuela Armonía.
              </p>
            </div>
            <button onclick="playMelody('china')" class="w-full py-2 rounded-xl bg-dorado text-madera font-display font-bold text-xs">🎵 Escuchar tema del episodio</button>
          </div>

          <div class="rounded-3xl bg-gradient-to-b from-emerald-700 to-teal-900 text-white p-5 border-4 border-celeste flex flex-col justify-between space-y-3">
            <div>
              <span class="text-[11px] font-extrabold uppercase bg-celeste text-madera px-2.5 py-0.5 rounded-full">Especial Carnaval</span>
              <h4 class="font-display font-bold text-xl mt-2 text-celeste">Ep. 3: El Ritmo Secreto de Río y Oruro</h4>
              <p class="text-xs text-white/85 mt-2 leading-relaxed">
                <strong>Luana Pereira</strong> y <strong>Diego Quispe</strong> compiten por descubrir quién escondió los tambores y las zampoñas antes del gran desfile de Carnaval.
              </p>
            </div>
            <button onclick="playMelody('brasil')" class="w-full py-2 rounded-xl bg-celeste text-madera font-display font-bold text-xs">🎵 Escuchar tema del episodio</button>
          </div>

          <div class="rounded-3xl bg-gradient-to-b from-orange-700 to-rose-900 text-white p-5 border-4 border-coral flex flex-col justify-between space-y-3">
            <div>
              <span class="text-[11px] font-extrabold uppercase bg-coral text-madera px-2.5 py-0.5 rounded-full">Especial Pascua</span>
              <h4 class="font-display font-bold text-xl mt-2 text-coral">Ep. 4: El Misterio de los Colores de Jaipur</h4>
              <p class="text-xs text-white/85 mt-2 leading-relaxed">
                El profesor <strong>Arjun Sharma</strong> muestra cómo las escalas musicales de la India esconden la clave para abrir el cofre de primavera de Doña Beatriz.
              </p>
            </div>
            <button onclick="playMelody('india')" class="w-full py-2 rounded-xl bg-coral text-madera font-display font-bold text-xs">🎵 Escuchar tema del episodio</button>
          </div>
        </div>
      </div>

      <!-- PANEL 3: LIBRO INTERACTIVO CON CÓDIGOS QR MUSICALES -->
      <div id="tm-panel-libro" class="tm-panel hidden bg-white rounded-3xl p-6 sm:p-8 border-4 border-pergamino shadow-card space-y-6">
        <div class="flex flex-wrap items-center justify-between gap-4 border-b-2 border-pergamino pb-4">
          <div>
            <span class="text-xs font-extrabold uppercase bg-amber-100 text-amber-900 px-3 py-1 rounded-full">Ficción y Divulgación Musical</span>
            <h3 class="text-2xl sm:text-3xl font-bold text-madera mt-1">Libro: "La Vuelta al Mundo en Seis Melodías"</h3>
            <p class="text-sm text-maderaSuave font-semibold">
              Un libro ilustrado donde cada capítulo viaja al país de uno de los protagonistas. Incluye <strong>códigos QR interactivos</strong> para escuchar los instrumentos típicos de cada cultura mientras lees.
            </p>
          </div>
          <button onclick="showToast('📚 Edición física disponible en librerías y pack navideño de Estel.', 'info')" class="px-5 py-2.5 rounded-2xl bg-dorado hover:bg-amber-400 text-madera font-display font-bold text-sm shadow-btn">
            🛒 Reservar Libro Completo
          </button>
        </div>

        <!-- Vista previa interactiva de capítulos con QR sonoro -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
          <div class="letter-paper rounded-2xl p-5 flex flex-col justify-between space-y-4">
            <div class="space-y-2">
              <div class="flex items-center justify-between">
                <span class="text-xs font-extrabold bg-emerald-100 text-emerald-900 px-2.5 py-0.5 rounded-full">Capítulo 1 · Brasil 🇧🇷</span>
                <span class="text-xs font-bold text-maderaSuave">Preview Gratuito</span>
              </div>
              <h4 class="font-display font-bold text-lg text-madera">El Tambor de Luana en Bahía</h4>
              <p class="text-xs text-madera/90 leading-relaxed">
                "Cuando Luana golpeó el surdo con su baqueta de madera, todo el aula de percusión vibró como una batucada en plena plaza de Salvador..."
              </p>
            </div>
            <div class="bg-white p-3 rounded-xl border-2 border-pergamino flex items-center justify-between gap-3">
              <div class="w-12 h-12 bg-madera text-white rounded-lg flex items-center justify-center font-mono text-[10px] text-center leading-tight p-1">QR<br/>🇧🇷<br/>AUDIO</div>
              <div class="flex-grow">
                <p class="text-xs font-bold text-madera">Ritmo de Samba y Surdo</p>
                <button onclick="playMelody('brasil')" class="mt-1 px-3 py-1 rounded-lg bg-lupa text-white font-bold text-xs">▶️ Escuchar QR</button>
              </div>
            </div>
          </div>

          <div class="letter-paper rounded-2xl p-5 flex flex-col justify-between space-y-4">
            <div class="space-y-2">
              <div class="flex items-center justify-between">
                <span class="text-xs font-extrabold bg-red-100 text-red-900 px-2.5 py-0.5 rounded-full">Capítulo 2 · China 🇨🇳</span>
                <span class="text-xs font-bold text-maderaSuave">Preview Gratuito</span>
              </div>
              <h4 class="font-display font-bold text-lg text-madera">Las Dos Cuerdas de Li Wei</h4>
              <p class="text-xs text-madera/90 leading-relaxed">
                "Li Wei comparó su violonchelo con el antiguo erhu de su abuelo en Pekín: bastaba una escala pentatónica para dibujar montañas entre la niebla..."
              </p>
            </div>
            <div class="bg-white p-3 rounded-xl border-2 border-pergamino flex items-center justify-between gap-3">
              <div class="w-12 h-12 bg-madera text-white rounded-lg flex items-center justify-center font-mono text-[10px] text-center leading-tight p-1">QR<br/>🇨🇳<br/>AUDIO</div>
              <div class="flex-grow">
                <p class="text-xs font-bold text-madera">Escala Pentatónica Erhu</p>
                <button onclick="playMelody('china')" class="mt-1 px-3 py-1 rounded-lg bg-lupa text-white font-bold text-xs">▶️ Escuchar QR</button>
              </div>
            </div>
          </div>

          <div class="letter-paper rounded-2xl p-5 flex flex-col justify-between space-y-4">
            <div class="space-y-2">
              <div class="flex items-center justify-between">
                <span class="text-xs font-extrabold bg-amber-100 text-amber-900 px-2.5 py-0.5 rounded-full">Capítulo 3 · Bolivia 🇧🇴</span>
                <span class="text-xs font-bold text-maderaSuave">Preview Gratuito</span>
              </div>
              <h4 class="font-display font-bold text-lg text-madera">El Viento de los Andes de Diego</h4>
              <p class="text-xs text-madera/90 leading-relaxed">
                "Antes de tocar la trompeta, Diego Quispe aprendió a soplar la zampoña en La Paz, donde el aire de las alturas convierte cada nota en eco..."
              </p>
            </div>
            <div class="bg-white p-3 rounded-xl border-2 border-pergamino flex items-center justify-between gap-3">
              <div class="w-12 h-12 bg-madera text-white rounded-lg flex items-center justify-center font-mono text-[10px] text-center leading-tight p-1">QR<br/>🇧🇴<br/>AUDIO</div>
              <div class="flex-grow">
                <p class="text-xs font-bold text-madera">Melodía Andina de Zampoña</p>
                <button onclick="playMelody('bolivia')" class="mt-1 px-3 py-1 rounded-lg bg-lupa text-white font-bold text-xs">▶️ Escuchar QR</button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- PANEL 4: FICCIÓN SONORA / PODCAST -->
      <div id="tm-panel-podcast" class="tm-panel hidden bg-white rounded-3xl p-6 sm:p-8 border-4 border-pergamino shadow-card space-y-5">
        <div class="flex flex-col md:flex-row gap-6 items-center">
          <div class="w-40 h-40 rounded-3xl bg-gradient-to-br from-celeste to-lupa flex flex-col items-center justify-center text-white p-4 text-center shadow-lg flex-shrink-0 border-4 border-white">
            <span class="text-4xl mb-1">🎧</span>
            <p class="font-display font-bold text-base leading-tight">Ondas de Armonía</p>
            <span class="text-[10px] uppercase tracking-wider mt-1 bg-black/20 px-2 py-0.5 rounded-full">Podcast Infantil</span>
          </div>
          <div class="space-y-3 flex-grow">
            <span class="text-xs font-extrabold uppercase bg-cyan-100 text-cyan-900 px-3 py-1 rounded-full">Ficción Sonora · Vinculado al Libro</span>
            <h3 class="text-2xl sm:text-3xl font-bold text-madera">Podcast Divulgativo: "Detectives del Sonido"</h3>
            <p class="text-sm text-madera/90 leading-relaxed">
              Un viaje sonoro narrado por los alumnos de la Escuela Armonía para escuchar con los ojos cerrados. Cada episodio combina misterios auditivos con músicas tradicionales de España, Hungría, India, Bolivia, China y Brasil.
            </p>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 pt-1">
              <div class="bg-crema p-3.5 rounded-2xl border-2 border-pergamino flex items-center justify-between gap-2">
                <div>
                  <p class="font-display font-bold text-sm text-madera">🎙️ Ep. 01: ¿Qué instrumento suena en la niebla?</p>
                  <p class="text-xs text-maderaSuave">Duración: 12 min · Con Arjun Sharma</p>
                </div>
                <button onclick="playMelody('india')" class="px-3 py-2 rounded-xl bg-lupa text-white font-bold text-xs">▶️ Oír</button>
              </div>
              <div class="bg-crema p-3.5 rounded-2xl border-2 border-pergamino flex items-center justify-between gap-2">
                <div>
                  <p class="font-display font-bold text-sm text-madera">🎙️ Ep. 02: El compás secreto del flamenco</p>
                  <p class="text-xs text-maderaSuave">Duración: 14 min · Con Doña Beatriz</p>
                </div>
                <button onclick="playMelody('espana')" class="px-3 py-2 rounded-xl bg-lupa text-white font-bold text-xs">▶️ Oír</button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- PANEL 5: PELÍCULA PRECUELA -->
      <div id="tm-panel-pelicula" class="tm-panel hidden rounded-3xl bg-gradient-to-br from-[#2C1810] via-[#4A2C18] to-[#1E293B] text-white p-6 sm:p-8 border-4 border-dorado shadow-card">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-center">
          <div class="lg:col-span-5">
            <div class="rounded-3xl bg-gradient-to-b from-amber-500/20 to-black/60 border-4 border-dorado p-6 text-center space-y-4 shadow-2xl">
              <p class="text-xs uppercase tracking-widest text-dorado font-extrabold">Estel Films · Especial TV (Clan / Boing)</p>
              <div class="text-6xl py-2">🎻✨</div>
              <h4 class="font-serif italic text-3xl font-bold text-dorado leading-tight">La Desaparición de La Aurora</h4>
              <p class="text-xs text-amber-100/90">La película precuela que revela el origen de la Escuela Armonía</p>
              <div class="pt-2 border-t border-dorado/30 text-[11px] text-amber-200">
                UNA HISTORIA DE AURORA VALCÁRCEL · BANDA SONORA ORIGINAL
              </div>
            </div>
          </div>
          <div class="lg:col-span-7 space-y-4">
            <span class="text-xs font-extrabold uppercase bg-dorado text-madera px-3 py-1 rounded-full">Largometraje de Animación · Precuela Oficial</span>
            <h3 class="text-2xl sm:text-4xl font-bold text-white">El origen de la leyenda del violín "La Aurora"</h3>
            <p class="text-sm sm:text-base text-amber-50/90 leading-relaxed">
              Décadas antes de que Doña Beatriz Valcárcel dirigiera la escuela, su antepasada y fundadora <strong>Aurora Valcárcel</strong> construyó junto a lutieres de todo el mundo un violín irrepetible cuya madera guardaba el eco de seis culturas musicales.
            </p>
            <p class="text-sm text-amber-100/80 leading-relaxed">
              Cuando el violín desaparece la víspera de la inauguración oficial en 1926, una joven Beatriz tendrá que resolver su primer gran enigma musical.
            </p>
            <div class="flex flex-wrap gap-3 pt-2">
              <button onclick="playMelody('aurora')" class="px-5 py-3 rounded-2xl bg-dorado hover:bg-amber-400 text-madera font-display font-bold text-sm shadow-lg transition flex items-center gap-2">
                <span>🎬</span> Escuchar Tema Principal del Tráiler
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- PANEL 6: FANDOM Y REGLAS DEL JUEGO -->
      <div id="tm-panel-fandom" class="tm-panel hidden bg-white rounded-3xl p-6 sm:p-8 border-4 border-pergamino shadow-card space-y-6">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div class="bg-crema rounded-2xl p-5 border-2 border-pergamino space-y-3">
            <h3 class="font-display font-bold text-xl text-madera">🌟 Comunidad Fandom "Expedientes Armonía"</h3>
            <p class="text-xs sm:text-sm text-madera/90 leading-relaxed">
              Los seguidores de Melodigma pasan de espectadores a creadores (prosumidores) diseñando sus propios detectives en el <strong>Generador de Avatares</strong> y enviando sus ilustraciones a mano. El personaje ganador se integra oficialmente en la siguiente aventura de la webserie.
            </p>
            <button onclick="switchSection('avatar')" class="px-4 py-2.5 rounded-xl bg-lupa text-white font-display font-bold text-xs shadow-btn">
              🎨 Ir al Creador y Concurso Fandom
            </button>
          </div>
          <div class="bg-crema rounded-2xl p-5 border-2 border-pergamino space-y-3">
            <h3 class="font-display font-bold text-xl text-madera">📖 Resumen Rápido del Manual de Detective</h3>
            <ul class="text-xs space-y-1.5 text-madera/90">
              <li><strong>1. Preparación:</strong> Se ocultan 1 sospechoso, 1 instrumento y 1 estancia en el Sobre Secreto.</li>
              <li><strong>2. Movimiento:</strong> Tira los dados y desplázate horizontal o verticalmente por los pasillos.</li>
              <li><strong>3. Hipótesis:</strong> Al entrar en una estancia, formula una sospecha sobre esa habitación. Los rivales te enseñarán en secreto una carta si la tienen para refutarla.</li>
              <li><strong>4. Acusación Final:</strong> Cuando estés seguro, abre el Sobre Secreto. ¡Si aciertas las 3 cartas, ganas el caso!</li>
            </ul>
          </div>
        </div>
      </div>
    </section>

  </main>

  <!-- MODAL DE FORMULAR HIPÓTESIS (AL ENTRAR EN UNA HABITACIÓN) -->
  <div id="hypothesis-modal" class="hidden fixed inset-0 z-50 bg-black/60 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="bg-[#FFFDF9] rounded-3xl max-w-md w-full p-6 border-4 border-dorado shadow-2xl space-y-4 animate-pop">
      <div class="flex items-center justify-between border-b-2 border-pergamino pb-2">
        <h3 class="font-display font-bold text-xl text-madera flex items-center gap-2">
          <span>🔍</span> Formular Hipótesis
        </h3>
        <button onclick="closeHypothesisModal()" class="text-maderaSuave hover:text-madera font-bold text-lg">✕</button>
      </div>
      <p class="text-xs sm:text-sm text-madera/90">
        Has entrado en <strong id="hyp-room-name" class="text-terracota">Aula de Cuerda</strong>. Elige qué sospechoso y qué instrumento crees que están implicados en esta estancia:
      </p>

      <div class="space-y-3">
        <div>
          <label class="block text-xs font-extrabold uppercase text-maderaSuave mb-1">Sospechoso</label>
          <select id="hyp-suspect-select" class="w-full p-2.5 rounded-xl border-2 border-pergamino bg-crema font-bold text-sm text-madera"></select>
        </div>
        <div>
          <label class="block text-xs font-extrabold uppercase text-maderaSuave mb-1">Instrumento</label>
          <select id="hyp-instrument-select" class="w-full p-2.5 rounded-xl border-2 border-pergamino bg-crema font-bold text-sm text-madera"></select>
        </div>
      </div>

      <div class="flex gap-2 pt-2">
        <button onclick="submitHypothesis()" class="flex-grow py-3 rounded-2xl bg-lupa hover:bg-lupaOscuro text-white font-display font-bold text-sm shadow-btn">
          🗣️ Preguntar a los Detectives
        </button>
        <button onclick="closeHypothesisModal()" class="px-4 py-3 rounded-2xl bg-crema border-2 border-pergamino text-madera font-bold text-sm">
          Cancelar
        </button>
      </div>
    </div>
  </div>

  <!-- MODAL DE ACUSACIÓN FINAL Y SOBRE SECRETO -->
  <div id="accusation-modal" class="hidden fixed inset-0 z-50 bg-black/65 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="bg-[#FFFDF9] rounded-3xl max-w-md w-full p-6 border-4 border-rose-400 shadow-2xl space-y-4 animate-pop">
      <div class="flex items-center justify-between border-b-2 border-pergamino pb-2">
        <h3 class="font-display font-bold text-xl text-rose-700 flex items-center gap-2">
          <span>✉️</span> Acusación Final · Sobre Secreto
        </h3>
        <button onclick="closeAccusationModal()" class="text-maderaSuave hover:text-madera font-bold text-lg">✕</button>
      </div>
      <p class="text-xs sm:text-sm text-madera/90 font-semibold">
        ¡Cuidado, detective! Solo tienes una oportunidad para abrir el <strong>Sobre Secreto</strong> y comprobar si tus tres deducciones son correctas:
      </p>

      <div class="space-y-3">
        <div>
          <label class="block text-xs font-extrabold uppercase text-maderaSuave mb-1">1. ¿Quién ha robado el instrumento?</label>
          <select id="acc-suspect-select" class="w-full p-2.5 rounded-xl border-2 border-pergamino bg-crema font-bold text-sm text-madera"></select>
        </div>
        <div>
          <label class="block text-xs font-extrabold uppercase text-maderaSuave mb-1">2. ¿Qué instrumento ha desaparecido?</label>
          <select id="acc-instrument-select" class="w-full p-2.5 rounded-xl border-2 border-pergamino bg-crema font-bold text-sm text-madera"></select>
        </div>
        <div>
          <label class="block text-xs font-extrabold uppercase text-maderaSuave mb-1">3. ¿Dónde está escondido?</label>
          <select id="acc-room-select" class="w-full p-2.5 rounded-xl border-2 border-pergamino bg-crema font-bold text-sm text-madera"></select>
        </div>
      </div>

      <div class="flex gap-2 pt-2">
        <button onclick="submitFinalAccusation()" class="flex-grow py-3 rounded-2xl bg-rose-500 hover:bg-rose-600 text-white font-display font-bold text-sm shadow-btn">
          🔓 Abrir el Sobre Secreto
        </button>
        <button onclick="closeAccusationModal()" class="px-4 py-3 rounded-2xl bg-crema border-2 border-pergamino text-madera font-bold text-sm">
          Seguir investigando
        </button>
      </div>
    </div>
  </div>

  <!-- MODAL DE DESENLACE (VICTORIA O DERROTA) -->
  <div id="outcome-modal" class="hidden fixed inset-0 z-50 bg-black/70 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="bg-[#FFFDF9] rounded-3xl max-w-lg w-full p-6 sm:p-8 border-4 border-dorado shadow-2xl text-center space-y-5 animate-pop">
      <div id="outcome-emoji" class="text-6xl">🎉</div>
      <h3 id="outcome-title" class="font-display font-bold text-2xl sm:text-3xl text-madera">¡Caso Resuelto!</h3>
      <p id="outcome-message" class="text-sm sm:text-base text-madera/90 font-semibold"></p>

      <div class="bg-crema rounded-2xl p-4 border-2 border-pergamino space-y-2">
        <p class="text-xs font-extrabold uppercase tracking-wider text-maderaSuave">Contenido del Sobre Secreto</p>
        <div id="outcome-secret-cards" class="grid grid-cols-3 gap-2 text-xs font-bold"></div>
      </div>

      <button onclick="closeOutcomeModal()" class="w-full py-3 rounded-2xl bg-lupa hover:bg-lupaOscuro text-white font-display font-bold text-base shadow-btn">
        🔄 Jugar otra partida
      </button>
    </div>
  </div>

  <!-- PIE DE PÁGINA CON LOGOS TRANSPARENTES -->
  <footer class="bg-[#FFFDF9] border-t-4 border-pergamino mt-12 py-6">
    <div class="max-w-7xl mx-auto px-4 flex flex-col sm:flex-row items-center justify-between gap-4">
      <div class="flex items-center gap-4">
        <div id="footer-logo-melodigma" class="w-36 h-12"></div>
        <div id="footer-logo-estel" class="w-24 h-12"></div>
      </div>
      <div class="text-center sm:text-right text-xs text-maderaSuave space-y-1">
        <p class="font-bold text-madera">Proyecto Universitario Transmedia · "Melodigma: El Misterio de la Escuela Armonía"</p>
        <p>Producido por <strong>Estel</strong> · Universo musical e interactivo para niños de 7 a 12 años.</p>
      </div>
    </div>
  </footer>

  <!-- ===================================================================== -->
  <!-- JAVASCRIPT COMPLETO: LOGOS SVG, PERSONAJES INLINE, CLUEDO Y AVATARES  -->
  <!-- ===================================================================== -->
  <script>
    // =========================================================================
    // 1. LOGOS VECTORIALES TRANSPARENTES (MELODIGMA Y PRODUCTORA ESTEL)
    // =========================================================================
    const SVG_LOGO_MELODIGMA = `
      <svg viewBox="0 0 280 95" xmlns="http://www.w3.org/2000/svg" class="w-full h-full">
        <!-- Pentagrama ondulado -->
        <g stroke="#212121" stroke-width="1.2" fill="none" opacity="0.85">
          <path d="M42 42 Q85 65 125 32 T215 48" />
          <path d="M44 47 Q87 70 127 37 T217 53" />
          <path d="M46 52 Q89 75 129 42 T219 58" />
          <path d="M48 57 Q91 80 131 47 T221 63" />
        </g>
        <!-- Notas musicales sobre pentagrama -->
        <g fill="#111111">
          <ellipse cx="68" cy="59" rx="4.5" ry="3.2" transform="rotate(-15 68 59)" />
          <rect x="71.5" y="42" width="1.8" height="17" />
          <ellipse cx="94" cy="49" rx="4.5" ry="3.2" transform="rotate(-15 94 49)" />
          <rect x="97.5" y="33" width="1.8" height="16" />
          <polygon points="97.5,33 111,30 111,34 97.5,37" />
          <ellipse cx="107" cy="46" rx="4.5" ry="3.2" transform="rotate(-15 107 46)" />
          <rect x="110.5" y="30" width="1.8" height="16" />
          <ellipse cx="152" cy="36" rx="5.5" ry="3.8" transform="rotate(-15 152 36)" />
          <rect x="156.5" y="16" width="2" height="20" />
          <ellipse cx="176" cy="42" rx="5.5" ry="3.8" transform="rotate(-15 176 42)" />
          <rect x="180.5" y="21" width="2" height="21" />
          <polygon points="180.5,21 206,27 206,32 180.5,26" />
          <ellipse cx="201" cy="47" rx="5.5" ry="3.8" transform="rotate(-15 201 47)" />
          <rect x="205.5" y="27" width="2" height="20" />
        </g>
        <!-- Lupa Verde Melodigma -->
        <g transform="translate(8, 6)">
          <rect x="14" y="54" width="13" height="28" rx="5" transform="rotate(42 20 68)" fill="#4CAF50" />
          <circle cx="52" cy="36" r="28" fill="none" stroke="#4CAF50" stroke-width="7.5" />
          <path d="M35 23 A20 20 0 0 1 48 16" fill="none" stroke="#4CAF50" stroke-width="4.5" stroke-linecap="round" />
          <circle cx="55" cy="16" r="2.3" fill="#4CAF50" />
        </g>
        <!-- Texto Melodigma -->
        <text x="92" y="84" font-family="'Fredoka', cursive, sans-serif" font-weight="700" font-size="27" fill="#4CAF50" letter-spacing="-0.5">Melodigma</text>
      </svg>
    `;

    const SVG_LOGO_ESTEL = `
      <svg viewBox="0 0 180 105" xmlns="http://www.w3.org/2000/svg" class="w-full h-full">
        <!-- Cuadrado turquesa -->
        <rect x="64" y="34" width="76" height="62" rx="4" fill="#4DD0E1" />
        <!-- Estrella amarilla superpuesta -->
        <polygon points="48,12 60,41 91,43 67,63 75,93 48,76 21,93 29,63 5,43 36,41" fill="#FFD54F" />
        <!-- Texto Estel verde -->
        <text x="72" y="28" font-family="'Fredoka', cursive, sans-serif" font-weight="700" font-size="25" fill="#66BB6A" letter-spacing="1.5">Estel</text>
      </svg>
    `;

    // =========================================================================
    // 2. DATOS DEL PROYECTO TRANSMEDIA (6 PERSONAJES ACTUALIZADOS + ESTANCIAS)
    // =========================================================================
    const CHARACTERS = [
      {
        id: 'luana',
        name: 'Luana Pereira',
        shortName: 'Luana',
        age: '10 años',
        country: 'Brasileña 🇧🇷',
        instrument: 'Percusión / Tambor',
        traits: 'Rebelde, creativa e impulsiva',
        desc: 'Suele actuar antes de pensar. Le encanta experimentar con los ritmos de percusión y no tiene miedo de saltarse las normas cuando algo despierta su curiosidad.',
        color: '#2E7D32',
        badgeBg: 'bg-emerald-100 text-emerald-900',
        avatarConfig: {
          skin: '#C68658',
          hair: 'curly',
          hairColor: '#4E342E',
          eyes: 'determined',
          outfit: 'sweater',
          outfitColor: '#2E7D32',
          item: 'tambor',
          notes: true
        }
      },
      {
        id: 'liwei',
        name: 'Li Wei',
        shortName: 'Li Wei',
        age: '10 años',
        country: 'Chino 🇨🇳',
        instrument: 'Violonchelo',
        traits: 'Sensible, soñador y reservado',
        desc: 'Prefiere observar antes que hablar y suele pasar desapercibido, aunque su capacidad para prestar atención a los pequeños detalles resulta clave en cada caso.',
        color: '#B71C1C',
        badgeBg: 'bg-red-100 text-red-900',
        avatarConfig: {
          skin: '#F5D0B5',
          hair: 'straight',
          hairColor: '#212121',
          eyes: 'calm',
          outfit: 'jacket',
          outfitColor: '#B71C1C',
          item: 'cello',
          notes: true
        }
      },
      {
        id: 'emese',
        name: 'Nagy Emese',
        shortName: 'Emese',
        age: '11 años',
        country: 'Húngara 🇭🇺',
        instrument: 'Piano',
        traits: 'Inteligente, observadora y curiosa',
        desc: 'Le encanta resolver enigmas, descubrir patrones musicales y encontrar explicaciones lógicas a situaciones aparentemente inexplicables.',
        color: '#6A1B9A',
        badgeBg: 'bg-purple-100 text-purple-900',
        avatarConfig: {
          skin: '#F9DEC9',
          hair: 'ponytail',
          hairColor: '#D4A359',
          eyes: 'happy',
          outfit: 'uniform',
          outfitColor: '#6A1B9A',
          item: 'piano',
          notes: true
        }
      },
      {
        id: 'diego',
        name: 'Diego Quispe',
        shortName: 'Diego',
        age: '12 años',
        country: 'Boliviano 🇧🇴',
        instrument: 'Trompeta',
        traits: 'Bromista, extrovertido y travieso',
        desc: 'Siempre está buscando la manera de divertirse y gastar alguna broma. Su carácter despreocupado hace que nadie sepa cuándo habla totalmente en serio.',
        color: '#FBC02D',
        badgeBg: 'bg-amber-100 text-amber-900',
        avatarConfig: {
          skin: '#B57449',
          hair: 'cap',
          hairColor: '#212121',
          eyes: 'happy',
          outfit: 'hoodie',
          outfitColor: '#FBC02D',
          item: 'trompeta',
          notes: true
        }
      },
      {
        id: 'arjun',
        name: 'Arjun Sharma',
        shortName: 'Arjun',
        age: '42 años',
        country: 'Indio 🇮🇳',
        instrument: 'Profesor de Flauta',
        traits: 'Excéntrico, curioso e intuitivo',
        desc: 'Conoce cada pasillo, aula y leyenda de la Escuela Armonía. Su peculiar comportamiento hace que resulte difícil adivinar qué está pensando realmente.',
        color: '#1565C0',
        badgeBg: 'bg-sky-100 text-sky-900',
        avatarConfig: {
          skin: '#8D5524',
          hair: 'eccentric',
          hairColor: '#212121',
          eyes: 'glasses',
          outfit: 'professor',
          outfitColor: '#1565C0',
          item: 'flauta',
          notes: true
        }
      },
      {
        id: 'beatriz',
        name: 'Doña Beatriz Valcárcel',
        shortName: 'Directora',
        age: '62 años',
        country: 'Española 🇪🇸',
        instrument: 'Directora de la Escuela',
        traits: 'Seria, tradicional y misteriosa',
        desc: 'Lleva décadas al frente de la institución y custodia la historia del violín "La Aurora". Muy estricta con las normas, parece guardar secretos del pasado.',
        color: '#AD1457',
        badgeBg: 'bg-rose-100 text-rose-900',
        avatarConfig: {
          skin: '#F3CBB2',
          hair: 'bun',
          hairColor: '#4E342E',
          eyes: 'determined',
          outfit: 'director',
          outfitColor: '#AD1457',
          item: 'violin',
          notes: true
        }
      }
    ];

    const ROOMS = [
      { id: 'cuerda', name: 'Aula de cuerda', icon: '🎻', bg: '#FFCCBC', desc: 'Espacio dedicado al aprendizaje y ensayo de violines y violonchelos.' },
      { id: 'viento', name: 'Aula de viento', icon: '🎺', bg: '#C8E6C9', desc: 'Aquí se imparten las clases de flauta travesera, clarinete y trompeta.' },
      { id: 'percusion', name: 'Aula de percusión', icon: '🥁', bg: '#FFF9C4', desc: 'Sala llena de tambores, xilófonos y ritmos donde ensaya Luana.' },
      { id: 'piano', name: 'Aula de piano', icon: '🎹', bg: '#E1BEE7', desc: 'Una de las aulas principales con pianos de cola y partituras clásicas.' },
      { id: 'auditorio', name: 'Auditorio', icon: '🎭', bg: '#B2EBF2', desc: 'El gran escenario de la Escuela Armonía donde se celebrará el concierto anual.' },
      { id: 'biblioteca', name: 'Biblioteca musical', icon: '📚', bg: '#BBDEFB', desc: 'Estancia tranquila con libros antiguos, biografías y archivos históricos.' },
      { id: 'despacho', name: 'Despacho del director', icon: '🗝️', bg: '#FFE0B2', desc: 'El despacho privado de Doña Beatriz Valcárcel, lleno de expedientes.' },
      { id: 'almacen', name: 'Almacén de instrumentos', icon: '📦', bg: '#D7CCC8', desc: 'Lugar donde se guardan estuches, atriles e instrumentos de reserva.' },
      { id: 'danza', name: 'Sala de danza', icon: '🩰', bg: '#F8BBD0', desc: 'Habitación con espejos y barra destinada a la expresión corporal y el ritmo.' }
    ];

    const INSTRUMENTS_AURORA = [
      { id: 'violin_aurora', name: 'Violín "La Aurora"', icon: '🎻' },
      { id: 'trompeta', name: 'Trompeta', icon: '🎺' },
      { id: 'piano', name: 'Piano', icon: '🎹' },
      { id: 'violonchelo', name: 'Violonchelo', icon: '🎻' },
      { id: 'flauta', name: 'Flauta', icon: '🪈' },
      { id: 'tambor', name: 'Tambor', icon: '🥁' }
    ];

    const INSTRUMENTS_ALL = [
      ...INSTRUMENTS_AURORA,
      { id: 'guitarra', name: 'Guitarra', icon: '🎸' }
    ];

    const HELP_CARDS_DECK = [
      { title: '¡Atajo secreto!', desc: 'Avanzas +2 casillas adicionales en este movimiento.', effect: 'bonus2' },
      { title: '¡Pasillo libre!', desc: 'Entras directamente en la estancia más cercana.', effect: 'teleport' },
      { title: '¡Oído atento!', desc: 'Descubres automáticamente una carta que NO está en el sobre.', effect: 'reveal1' },
      { title: '¡Mirada de detective!', desc: 'Descartas un sospechoso inocente en tu hoja.', effect: 'revealSuspect' },
      { title: '¡Archivo secreto!', desc: 'Compruebas una estancia segura de la escuela.', effect: 'revealRoom' },
      { title: '¡Información privilegiada!', desc: 'Un testigo te muestra una de sus cartas en secreto.', effect: 'reveal1' }
    ];

    // =========================================================================
    // 3. MOTOR DE DIBUJO DE AVATARES CABEZA CUADRADA (SVG INLINE TRANSPARENTE)
    // =========================================================================
    function generateSquareCharacterSVG(cfg) {
      const outline = '#3E2723';
      let backHair = '';
      if (cfg.hair === 'curly') {
        backHair = `<path d="M118 92 Q92 130 102 175 Q106 202 128 198 L232 198 Q254 202 258 175 Q268 130 242 92 Z" fill="${cfg.hairColor}" stroke="${outline}" stroke-width="4.5" stroke-linejoin="round" />`;
      } else if (cfg.hair === 'ponytail') {
        backHair = `
          <path d="M222 85 Q272 78 266 145 Q263 172 244 178 Q252 155 240 135 Q234 112 222 106 Z" fill="${cfg.hairColor}" stroke="${outline}" stroke-width="4.5" stroke-linejoin="round" />
          <circle cx="225" cy="92" r="9" fill="${cfg.outfitColor}" stroke="${outline}" stroke-width="4" />
        `;
      } else if (cfg.hair === 'bun') {
        backHair = `<circle cx="226" cy="76" r="24" fill="${cfg.hairColor}" stroke="${outline}" stroke-width="4.5" />`;
      }

      let outfitSvg = '';
      if (cfg.outfit === 'sweater' || cfg.outfit === 'uniform') {
        const topFill = cfg.outfit === 'uniform' ? '#FFFDF7' : cfg.outfitColor;
        const chestDetail = cfg.outfit === 'sweater'
          ? `<g fill="#FFF8EB" stroke="#FFF8EB" stroke-width="3">
               <circle cx="174" cy="246" r="4.5" />
               <circle cx="188" cy="243" r="4.5" />
               <path d="M178 246 L178 226 L192 223 L192 243" fill="none" />
             </g>`
          : `<polygon points="166,204 180,222 194,204" fill="#E0F7FA" stroke="${outline}" stroke-width="3.5" stroke-linejoin="round" />`;
        outfitSvg = `
          <rect x="134" y="204" width="92" height="68" rx="12" fill="${topFill}" stroke="${outline}" stroke-width="4.5" />
          ${chestDetail}
          <polygon points="138,268 222,268 238,336 122,336" fill="${cfg.outfitColor}" stroke="${outline}" stroke-width="4.5" stroke-linejoin="round" />
          <line x1="162" y1="268" x2="156" y2="336" stroke="${outline}" stroke-width="3.5" />
          <line x1="180" y1="268" x2="180" y2="336" stroke="${outline}" stroke-width="3.5" />
          <line x1="198" y1="268" x2="204" y2="336" stroke="${outline}" stroke-width="3.5" />
        `;
      } else if (cfg.outfit === 'hoodie' || cfg.outfit === 'jacket') {
        const innerShirt = cfg.outfit === 'jacket'
          ? `<rect x="166" y="206" width="28" height="70" fill="#FFF8EB" stroke="${outline}" stroke-width="4" />`
          : '';
        outfitSvg = `
          <rect x="140" y="268" width="36" height="86" fill="#455A64" stroke="${outline}" stroke-width="4.5" />
          <rect x="184" y="268" width="36" height="86" fill="#455A64" stroke="${outline}" stroke-width="4.5" />
          <rect x="130" y="204" width="100" height="74" rx="14" fill="${cfg.outfitColor}" stroke="${outline}" stroke-width="4.5" />
          ${innerShirt}
        `;
      } else if (cfg.outfit === 'professor') {
        outfitSvg = `
          <rect x="142" y="268" width="35" height="88" fill="#D7CCC8" stroke="${outline}" stroke-width="4.5" />
          <rect x="183" y="268" width="35" height="88" fill="#D7CCC8" stroke="${outline}" stroke-width="4.5" />
          <rect x="132" y="204" width="96" height="74" rx="10" fill="${cfg.outfitColor}" stroke="${outline}" stroke-width="4.5" />
          <polygon points="164,204 180,246 196,204" fill="#FFFFFF" stroke="${outline}" stroke-width="3.5" stroke-linejoin="round" />
          <rect x="176" y="214" width="8" height="42" fill="#263238" />
        `;
      } else if (cfg.outfit === 'director') {
        outfitSvg = `
          <polygon points="142,266 218,266 234,384 126,384" fill="${cfg.outfitColor}" stroke="${outline}" stroke-width="4.5" stroke-linejoin="round" />
          <rect x="136" y="204" width="88" height="66" rx="10" fill="#FFFDF7" stroke="${outline}" stroke-width="4.5" />
          <polyline points="166,204 180,232 194,204" fill="none" stroke="${outline}" stroke-width="3.5" />
          <rect x="173" y="232" width="14" height="18" fill="#FFD54F" stroke="${outline}" stroke-width="3" />
        `;
      }

      let eyesSvg = '';
      if (cfg.eyes === 'happy') {
        eyesSvg = `
          <path d="M149 150 Q158 139 167 150" fill="none" stroke="${outline}" stroke-width="4.2" stroke-linecap="round" />
          <path d="M193 150 Q202 139 211 150" fill="none" stroke="${outline}" stroke-width="4.2" stroke-linecap="round" />
        `;
      } else if (cfg.eyes === 'determined') {
        eyesSvg = `
          <line x1="148" y1="138" x2="166" y2="148" stroke="${outline}" stroke-width="4.2" stroke-linecap="round" />
          <line x1="212" y1="138" x2="194" y2="148" stroke="${outline}" stroke-width="4.2" stroke-linecap="round" />
        `;
      } else if (cfg.eyes === 'calm') {
        eyesSvg = `
          <line x1="148" y1="145" x2="166" y2="145" stroke="${outline}" stroke-width="4.2" stroke-linecap="round" />
          <line x1="194" y1="145" x2="212" y2="145" stroke="${outline}" stroke-width="4.2" stroke-linecap="round" />
        `;
      } else if (cfg.eyes === 'glasses') {
        eyesSvg = `
          <circle cx="158" cy="145" r="14" fill="rgba(224,247,250,0.6)" stroke="${outline}" stroke-width="4" />
          <circle cx="202" cy="145" r="14" fill="rgba(224,247,250,0.6)" stroke="${outline}" stroke-width="4" />
          <line x1="172" y1="145" x2="188" y2="145" stroke="${outline}" stroke-width="4" />
        `;
      }

      let frontHair = '';
      if (cfg.hair === 'cap') {
        frontHair = `
          <path d="M126 98 A54 54 0 0 1 234 98 Z" fill="${cfg.outfitColor}" stroke="${outline}" stroke-width="4.5" stroke-linejoin="round" />
          <ellipse cx="134" cy="96" rx="36" ry="10" transform="rotate(-8 134 96)" fill="${cfg.outfitColor}" stroke="${outline}" stroke-width="4.5" />
        `;
      } else if (cfg.hair === 'straight') {
        frontHair = `<path d="M122 115 Q124 72 180 72 Q236 72 238 115 L212 106 L195 118 L180 105 L162 118 L145 106 Z" fill="${cfg.hairColor}" stroke="${outline}" stroke-width="4.5" stroke-linejoin="round" />`;
      } else if (cfg.hair === 'eccentric') {
        frontHair = `<path d="M122 112 L116 82 L142 88 L158 66 L180 84 L204 65 L220 86 L244 80 L238 112 Q180 98 122 112 Z" fill="${cfg.hairColor}" stroke="${outline}" stroke-width="4.5" stroke-linejoin="round" />`;
      } else {
        frontHair = `<path d="M122 118 Q120 74 180 74 Q240 74 238 118 Q205 108 180 96 Q155 108 122 118 Z" fill="${cfg.hairColor}" stroke="${outline}" stroke-width="4.5" stroke-linejoin="round" />`;
      }

      let itemSvg = '';
      if (cfg.item === 'violin' || cfg.item === 'cello') {
        const s = cfg.item === 'cello' ? '1.22' : '0.92';
        itemSvg = `
          <g transform="translate(262, 255) rotate(16) scale(${s})">
            <ellipse cx="0" cy="26" rx="18" ry="22" fill="#BF5B2B" stroke="${outline}" stroke-width="4" />
            <ellipse cx="0" cy="0" rx="14" ry="17" fill="#BF5B2B" stroke="${outline}" stroke-width="4" />
            <rect x="-3.5" y="-42" width="7" height="42" fill="#3E2723" />
            <line x1="-2" y1="-38" x2="-2" y2="36" stroke="#FFD54F" stroke-width="1.6" />
            <line x1="2" y1="-38" x2="2" y2="36" stroke="#FFD54F" stroke-width="1.6" />
          </g>
        `;
      } else if (cfg.item === 'tambor') {
        itemSvg = `
          <g transform="translate(265, 285)">
            <rect x="-22" y="-16" width="44" height="30" fill="#E53935" stroke="${outline}" stroke-width="4" />
            <ellipse cx="0" cy="-16" rx="22" ry="7" fill="#FFF8EB" stroke="${outline}" stroke-width="4" />
            <line x1="-18" y1="-32" x2="4" y2="-18" stroke="${outline}" stroke-width="3.5" stroke-linecap="round" />
            <line x1="18" y1="-32" x2="-4" y2="-18" stroke="${outline}" stroke-width="3.5" stroke-linecap="round" />
          </g>
        `;
      } else if (cfg.item === 'trompeta') {
        itemSvg = `
          <g transform="translate(264, 272) rotate(-25)">
            <rect x="-24" y="-4" width="38" height="8" fill="#FFD54F" stroke="${outline}" stroke-width="3.5" />
            <polygon points="14,-4 28,-14 28,14 14,4" fill="#FFD54F" stroke="${outline}" stroke-width="3.5" stroke-linejoin="round" />
          </g>
        `;
      } else if (cfg.item === 'flauta') {
        itemSvg = `
          <g transform="translate(264, 255) rotate(12)">
            <rect x="-4" y="-45" width="8" height="90" fill="#CFD8DC" stroke="${outline}" stroke-width="3.5" />
          </g>
        `;
      } else if (cfg.item === 'piano') {
        itemSvg = `
          <g transform="translate(256, 278) rotate(-8)">
            <rect x="-20" y="-24" width="40" height="48" fill="#263238" stroke="${outline}" stroke-width="3.5" />
            <rect x="-14" y="-18" width="28" height="36" fill="#FFFFFF" />
          </g>
        `;
      } else if (cfg.item === 'lupa') {
        itemSvg = `
          <g transform="translate(264, 265) rotate(-18)">
            <rect x="-4" y="16" width="8" height="26" fill="#43A047" stroke="${outline}" stroke-width="3.5" />
            <circle cx="0" cy="0" r="18" fill="rgba(224,247,250,0.8)" stroke="#43A047" stroke-width="6" />
          </g>
        `;
      }

      const notesSvg = cfg.notes ? `
        <text x="74" y="132" font-size="26" font-weight="bold" fill="${outline}">♪</text>
        <text x="266" y="120" font-size="26" font-weight="bold" fill="${outline}">♫</text>
        <line x1="84" y1="160" x2="96" y2="165" stroke="${outline}" stroke-width="3" stroke-linecap="round" />
        <line x1="264" y1="155" x2="276" y2="150" stroke="${outline}" stroke-width="3" stroke-linecap="round" />
      ` : '';

      return `
        <svg viewBox="60 45 245 380" xmlns="http://www.w3.org/2000/svg" class="w-full h-full overflow-visible">
          ${backHair}
          <!-- Piernas y zapatos -->
          <rect x="152" y="330" width="18" height="65" fill="${cfg.skin}" stroke="${outline}" stroke-width="4.5" />
          <rect x="190" y="330" width="18" height="65" fill="${cfg.skin}" stroke="${outline}" stroke-width="4.5" />
          <ellipse cx="156" cy="402" rx="20" ry="10" fill="#37474F" stroke="${outline}" stroke-width="4.5" />
          <ellipse cx="204" cy="402" rx="20" ry="10" fill="#37474F" stroke="${outline}" stroke-width="4.5" />
          <!-- Brazos -->
          <polygon points="132,212 106,278 124,286 142,232" fill="${cfg.outfitColor}" stroke="${outline}" stroke-width="4.5" stroke-linejoin="round" />
          <circle cx="114" cy="286" r="10" fill="${cfg.skin}" stroke="${outline}" stroke-width="4.5" />
          <polygon points="228,212 254,278 236,286 218,232" fill="${cfg.outfitColor}" stroke="${outline}" stroke-width="4.5" stroke-linejoin="round" />
          <circle cx="246" cy="286" r="10" fill="${cfg.skin}" stroke="${outline}" stroke-width="4.5" />
          <!-- Vestuario -->
          ${outfitSvg}
          <!-- Cuello, orejas y cabeza cuadrada -->
          <rect x="171" y="184" width="18" height="22" fill="${cfg.skin}" stroke="${outline}" stroke-width="4.5" />
          <circle cx="124" cy="146" r="11" fill="${cfg.skin}" stroke="${outline}" stroke-width="4.5" />
          <circle cx="236" cy="146" r="11" fill="${cfg.skin}" stroke="${outline}" stroke-width="4.5" />
          <rect x="126" y="94" width="108" height="94" rx="10" fill="${cfg.skin}" stroke="${outline}" stroke-width="4.5" />
          <!-- Coloretes -->
          <circle cx="145" cy="162" r="10" fill="rgba(244,143,177,0.45)" />
          <circle cx="215" cy="162" r="10" fill="rgba(244,143,177,0.45)" />
          <!-- Expresión y pelo delantero -->
          ${eyesSvg}
          ${frontHair}
          ${itemSvg}
          ${notesSvg}
        </svg>
      `;
    }

    // =========================================================================
    // 4. SÍNTESIS DE AUDIO MUSICAL (WEB AUDIO API - SIN ARCHIVOS EXTERNOS)
    // =========================================================================
    let audioCtx = null;
    function getAudioCtx() {
      if (!audioCtx) {
        const AC = window.AudioContext || window.webkitAudioContext;
        if (AC) audioCtx = new AC();
      }
      if (audioCtx && audioCtx.state === 'suspended') audioCtx.resume();
      return audioCtx;
    }

    const MELODIES = {
      aurora: [
        { f: 440, d: 0.22 }, { f: 523.25, d: 0.22 }, { f: 659.25, d: 0.28 },
        { f: 587.33, d: 0.20 }, { f: 659.25, d: 0.25 }, { f: 880, d: 0.45 }
      ],
      brasil: [
        { f: 392, d: 0.16 }, { f: 493.88, d: 0.16 }, { f: 587.33, d: 0.16 },
        { f: 659.25, d: 0.22 }, { f: 587.33, d: 0.16 }, { f: 783.99, d: 0.35 }
      ],
      china: [
        { f: 523.25, d: 0.22 }, { f: 587.33, d: 0.22 }, { f: 659.25, d: 0.22 },
        { f: 783.99, d: 0.25 }, { f: 880, d: 0.35 }, { f: 659.25, d: 0.35 }
      ],
      hungria: [
        { f: 440, d: 0.2 }, { f: 466.16, d: 0.2 }, { f: 554.37, d: 0.25 },
        { f: 587.33, d: 0.25 }, { f: 659.25, d: 0.2 }, { f: 880, d: 0.4 }
      ],
      bolivia: [
        { f: 659.25, d: 0.22 }, { f: 587.33, d: 0.22 }, { f: 493.88, d: 0.25 },
        { f: 440, d: 0.25 }, { f: 392, d: 0.22 }, { f: 329.63, d: 0.42 }
      ],
      india: [
        { f: 440, d: 0.2 }, { f: 466.16, d: 0.2 }, { f: 554.37, d: 0.2 },
        { f: 587.33, d: 0.2 }, { f: 659.25, d: 0.2 }, { f: 698.46, d: 0.25 }, { f: 880, d: 0.4 }
      ],
      espana: [
        { f: 329.63, d: 0.18 }, { f: 349.23, d: 0.18 }, { f: 415.30, d: 0.22 },
        { f: 440, d: 0.25 }, { f: 415.30, d: 0.18 }, { f: 349.23, d: 0.18 }, { f: 329.63, d: 0.4 }
      ],
      dice: [
        { f: 523.25, d: 0.08 }, { f: 659.25, d: 0.08 }, { f: 783.99, d: 0.12 }
      ],
      victory: [
        { f: 523.25, d: 0.15 }, { f: 659.25, d: 0.15 }, { f: 783.99, d: 0.15 }, { f: 1046.5, d: 0.45 }
      ]
    };

    function playMelody(key) {
      try {
        const ctx = getAudioCtx();
        if (!ctx) return;
        const notes = MELODIES[key] || MELODIES.aurora;
        let now = ctx.currentTime;
        notes.forEach(n => {
          const osc = ctx.createOscillator();
          const gain = ctx.createGain();
          osc.type = 'triangle';
          osc.frequency.setValueAtTime(n.f, now);
          gain.gain.setValueAtTime(0.14, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + n.d);
          osc.connect(gain);
          gain.connect(ctx.destination);
          osc.start(now);
          osc.stop(now + n.d + 0.02);
          now += n.d * 0.92;
        });
      } catch (e) {
        // Silencioso si el navegador bloquea audio sin gesto
      }
    }

    // =========================================================================
    // 5. NAVEGACIÓN Y TOASTS
    // =========================================================================
    function showToast(msg, type = 'info') {
      const container = document.getElementById('toast-container');
      const el = document.createElement('div');
      const colors = {
        info: 'bg-[#FFFDF9] border-celeste text-madera',
        success: 'bg-emerald-50 border-lupa text-emerald-950',
        warning: 'bg-amber-50 border-dorado text-madera'
      };
      el.className = `pointer-events-auto px-4 py-3 rounded-2xl border-4 shadow-lg font-bold text-xs sm:text-sm animate-pop ${colors[type] || colors.info}`;
      el.textContent = msg;
      container.appendChild(el);
      setTimeout(() => {
        el.style.opacity = '0';
        el.style.transition = 'opacity 0.3s';
        setTimeout(() => el.remove(), 320);
      }, 3600);
    }

    function switchSection(secId) {
      ['inicio', 'juego', 'avatar', 'transmedia'].forEach(id => {
        document.getElementById(`sec-${id}`).classList.add('hidden');
        const btn = document.getElementById(`nav-${id}`);
        btn.classList.remove('bg-lupa', 'text-white', 'shadow-btn');
        btn.classList.add('bg-[#FFF3DF]', 'text-madera');
      });
      document.getElementById(`sec-${secId}`).classList.remove('hidden');
      const activeBtn = document.getElementById(`nav-${secId}`);
      activeBtn.classList.remove('bg-[#FFF3DF]', 'text-madera');
      activeBtn.classList.add('bg-lupa', 'text-white', 'shadow-btn');
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function switchTransmediaTab(tabId) {
      ['mesa', 'webserie', 'libro', 'podcast', 'pelicula', 'fandom'].forEach(id => {
        document.getElementById(`tm-panel-${id}`).classList.add('hidden');
        const tab = document.getElementById(`tm-tab-${id}`);
        tab.classList.remove('bg-madera', 'text-white', 'shadow');
        tab.classList.add('bg-white', 'text-madera');
      });
      document.getElementById(`tm-panel-${tabId}`).classList.remove('hidden');
      const activeTab = document.getElementById(`tm-tab-${tabId}`);
      activeTab.classList.remove('bg-white', 'text-madera');
      activeTab.classList.add('bg-madera', 'text-white', 'shadow');
    }

    function playWebseriesIntro() {
      document.getElementById('webseries-intro-player').classList.remove('hidden');
      playMelody('aurora');
    }

    // =========================================================================
    // 6. RENDERIZADO DE INICIO (PERSONAJES TRANSPARENTES Y ESTANCIAS)
    // =========================================================================
    function renderInicioContent() {
      // Retrato transparente de la directora en su carta
      document.getElementById('director-letter-portrait').innerHTML =
        generateSquareCharacterSVG(CHARACTERS[5].avatarConfig);

      // Tarjetas de los 6 personajes con ilustración flotante 100% transparente
      const charGrid = document.getElementById('characters-grid');
      charGrid.innerHTML = CHARACTERS.map(ch => {
        const charSvg = generateSquareCharacterSVG(ch.avatarConfig);
        return `
          <div class="bg-white rounded-3xl p-5 border-4 border-pergamino shadow-card flex flex-col justify-between space-y-4 hover:-translate-y-1 transition">
            <div>
              <div class="flex items-center justify-between gap-2 mb-2">
                <span class="text-xs font-extrabold px-3 py-1 rounded-full ${ch.badgeBg}">${ch.country} · ${ch.age}</span>
                <span class="text-xs font-bold text-maderaSuave bg-crema px-2.5 py-1 rounded-full border border-pergamino">🎵 ${ch.instrument}</span>
              </div>

              <div class="w-full h-52 flex items-center justify-center p-1 mb-2">
                <div class="h-full w-40 flex items-center justify-center drop-shadow-md">
                  ${charSvg}
                </div>
              </div>

              <h3 class="font-display font-bold text-xl text-madera">${ch.name}</h3>
              <p class="text-xs font-extrabold text-lupaOscuro mb-1">"${ch.traits}"</p>
              <p class="text-xs text-madera/85 leading-relaxed">${ch.desc}</p>
            </div>

            <div class="pt-2 border-t border-pergamino">
              <button onclick="editCharacterInAvatar('${ch.id}')" class="w-full py-2 px-3 rounded-xl bg-lupa hover:bg-lupaOscuro text-white font-display font-bold text-xs transition flex items-center justify-center gap-1.5">
                <span>🎨</span> Personalizar estilo en el Creador
              </button>
            </div>
          </div>
        `;
      }).join('');

      // Tarjetas de las 9 estancias
      const roomsGrid = document.getElementById('rooms-grid');
      roomsGrid.innerHTML = ROOMS.map((r, idx) => `
        <div class="bg-white rounded-2xl p-4 border-2 border-pergamino shadow-sm flex items-start gap-3">
          <div class="w-12 h-12 rounded-2xl flex items-center justify-center text-2xl flex-shrink-0 border-2 border-madera/20" style="background-color: ${r.bg}">
            ${r.icon}
          </div>
          <div>
            <h4 class="font-display font-bold text-base text-madera">${idx + 1}. ${r.name}</h4>
            <p class="text-xs text-maderaSuave leading-relaxed mt-0.5">${r.desc}</p>
          </div>
        </div>
      `).join('');
    }

    function editCharacterInAvatar(charId) {
      switchSection('avatar');
      applyAvatarPreset(charId);
    }

    // =========================================================================
    // 7. JUEGO CLUEDO ONLINE (LÓGICA COMPLETA FIEL AL MANUAL)
    // =========================================================================
    const BOARD_LAYOUT = [
      ['cuerda','cuerda','cuerda','H','viento','viento','viento','H','percusion','percusion','percusion'],
      ['cuerda','cuerda','cuerda','P','viento','viento','viento','P','percusion','percusion','percusion'],
      ['cuerda','cuerda','D:cuerda','P','viento','D:viento','viento','P','percusion','D:percusion','percusion'],
      ['P','P','P','P','P','P','P','P','P','P','P'],
      ['piano','piano','piano','P','CENTER','CENTER','CENTER','P','auditorio','auditorio','auditorio'],
      ['piano','piano','D:piano','P','CENTER','CENTER','CENTER','P','D:auditorio','auditorio','auditorio'],
      ['piano','piano','piano','P','CENTER','CENTER','CENTER','P','P','P','P'],
      ['P','P','P','P','P','P','P','P','danza','danza','danza'],
      ['biblioteca','biblioteca','D:biblioteca','P','despacho','D:despacho','despacho','P','D:danza','danza','danza'],
      ['biblioteca','biblioteca','biblioteca','P','despacho','despacho','despacho','P','P','P','P'],
      ['biblioteca','biblioteca','biblioteca','P','despacho','despacho','despacho','P','almacen','D:almacen','almacen']
    ];

    const DOOR_COORDS = {
      cuerda: { r: 2, c: 2 },
      viento: { r: 2, c: 5 },
      percusion: { r: 2, c: 9 },
      piano: { r: 5, c: 2 },
      auditorio: { r: 5, c: 8 },
      biblioteca: { r: 8, c: 2 },
      despacho: { r: 8, c: 5 },
      danza: { r: 8, c: 8 },
      almacen: { r: 10, c: 9 }
    };

    const START_SPOTS = [
      { r: 3, c: 0 },
      { r: 0, c: 3 },
      { r: 0, c: 7 },
      { r: 3, c: 10 }
    ];

    let gameState = null;
    let customProfileDetective = null;

    function getAvailableDetectives() {
      return customProfileDetective ? [customProfileDetective, ...CHARACTERS] : [...CHARACTERS];
    }

    function renderGameSetupChoices() {
      const box = document.getElementById('setup-character-choices');
      const pool = getAvailableDetectives();
      box.innerHTML = pool.map(ch => {
        const charSvg = generateSquareCharacterSVG(ch.avatarConfig);
        return `
          <button onclick="startNewGame('${ch.id}')" class="bg-crema hover:bg-dorado/40 rounded-2xl p-3 border-2 ${ch.isCustom ? 'border-lupa bg-green-50/60' : 'border-pergamino'} hover:border-lupa transition flex flex-col items-center text-center group">
            <div class="h-24 w-20 flex items-center justify-center mb-2 group-hover:scale-105 transition drop-shadow-sm">
              ${charSvg}
            </div>
            <p class="font-display font-bold text-sm text-madera">${ch.shortName}</p>
            <p class="text-[11px] text-maderaSuave">${ch.instrument}</p>
          </button>
        `;
      }).join('');
    }

    function openNewGameModal() {
      renderGameSetupChoices();
      document.getElementById('game-setup-panel').classList.remove('hidden');
      document.getElementById('game-active-area').classList.add('hidden');
    }

    function startNewGame(selectedCharId) {
      const mode = document.querySelector('input[name="gameMode"]:checked')?.value || 'aurora';
      const instrumentsPool = mode === 'aurora' ? [...INSTRUMENTS_AURORA] : [...INSTRUMENTS_ALL];
      const pool = getAvailableDetectives();

      // 1. Elegir Sobre Secreto (1 sospechoso oficial, 1 instrumento, 1 habitación)
      const secretSuspect = CHARACTERS[Math.floor(Math.random() * CHARACTERS.length)];
      const secretInstrument = mode === 'aurora' && Math.random() < 0.65
        ? instrumentsPool[0]
        : instrumentsPool[Math.floor(Math.random() * instrumentsPool.length)];
      const secretRoom = ROOMS[Math.floor(Math.random() * ROOMS.length)];

      // 2. Preparar mazo restante y repartir entre 4 jugadores (1 humano + 3 IA)
      const remainingCards = [
        ...CHARACTERS.filter(c => c.id !== secretSuspect.id).map(c => ({ id: c.id, name: c.name, cat: 'Sospechoso', icon: '🕵️' })),
        ...instrumentsPool.filter(i => i.id !== secretInstrument.id).map(i => ({ id: i.id, name: i.name, cat: 'Instrumento', icon: i.icon })),
        ...ROOMS.filter(r => r.id !== secretRoom.id).map(r => ({ id: r.id, name: r.name, cat: 'Estancia', icon: r.icon }))
      ].sort(() => Math.random() - 0.5);

      const humanChar = pool.find(c => c.id === selectedCharId) || CHARACTERS[0];
      const aiChars = CHARACTERS.filter(c => c.id !== selectedCharId).sort(() => Math.random() - 0.5).slice(0, 3);

      const players = [humanChar, ...aiChars].map((ch, idx) => ({
        char: ch,
        isHuman: idx === 0,
        r: START_SPOTS[idx].r,
        c: START_SPOTS[idx].c,
        inRoom: null,
        hand: [],
        helpCards: []
      }));

      remainingCards.forEach((card, i) => {
        players[i % players.length].hand.push(card);
      });

      // 3. Notas del detective (0: dudoso, 1: descartado X, 2: sospechoso ⭐)
      const notes = {};
      [...CHARACTERS, ...instrumentsPool, ...ROOMS].forEach(item => { notes[item.id] = 0; });
      players[0].hand.forEach(c => { notes[c.id] = 1; });

      gameState = {
        mode,
        instrumentsPool,
        secret: { suspect: secretSuspect, instrument: secretInstrument, room: secretRoom },
        players,
        turnIdx: 0,
        stepsLeft: 0,
        hasRolled: false,
        hasHypothesizedThisTurn: false,
        notes,
        gameOver: false
      };

      document.getElementById('game-setup-panel').classList.add('hidden');
      document.getElementById('game-active-area').classList.remove('hidden');
      document.getElementById('game-log-list').innerHTML = '';

      addGameLog(`✉️ El Sobre Secreto ha sido sellado con 3 cartas. ¡Comienza la investigación de ${humanChar.name}!`, 'highlight');
      addGameLog(`🃏 Has recibido ${players[0].hand.length} cartas secretas y ya están marcadas con ❌ en tu Hoja de Detective.`);
      playMelody('aurora');
      updateGameUI();
    }

    function addGameLog(text, style = 'normal') {
      const list = document.getElementById('game-log-list');
      const p = document.createElement('div');
      p.className = style === 'highlight'
        ? 'p-2 rounded-xl bg-amber-50 border border-dorado text-madera font-bold'
        : style === 'clue'
          ? 'p-2 rounded-xl bg-emerald-50 border border-lupa text-emerald-950 font-bold'
          : 'p-1.5 rounded-lg bg-crema/70 text-madera/90';
      p.textContent = text;
      list.prepend(p);
    }

    function updateGameUI() {
      if (!gameState) return;
      const current = gameState.players[gameState.turnIdx];
      const badge = document.getElementById('turn-avatar-badge');
      badge.style.backgroundColor = current.char.color;
      badge.textContent = current.char.shortName.slice(0, 2).toUpperCase();
      document.getElementById('turn-player-name').textContent =
        current.isHuman ? `${current.char.name} (Tú)` : `${current.char.name} (Investigando...)`;

      const btnRoll = document.getElementById('btn-roll-dice');
      const btnEnd = document.getElementById('btn-end-turn');
      const stepsBadge = document.getElementById('steps-remaining-badge');

      if (current.isHuman && !gameState.gameOver) {
        if (!gameState.hasRolled) {
          btnRoll.classList.remove('hidden');
          btnEnd.classList.add('hidden');
          stepsBadge.classList.add('hidden');
          document.getElementById('instruction-text').textContent = 'Tu turno: pulsa "Tirar Dados" para moverte por los pasillos.';
        } else {
          btnRoll.classList.add('hidden');
          btnEnd.classList.remove('hidden');
          if (gameState.stepsLeft > 0) {
            stepsBadge.classList.remove('hidden');
            stepsBadge.textContent = `${gameState.stepsLeft} pasos`;
            document.getElementById('instruction-text').textContent = 'Haz clic en las casillas verdes o en una puerta (🚪) para entrar.';
          } else {
            stepsBadge.classList.add('hidden');
            document.getElementById('instruction-text').textContent = 'Movimiento completado. Puedes pasar turno o hacer tu Acusación Final.';
          }
        }
      } else {
        btnRoll.classList.add('hidden');
        btnEnd.classList.add('hidden');
        stepsBadge.classList.add('hidden');
      }

      renderBoardGrid();
      renderPlayerHand();
      renderDetectiveNotebook();
    }

    function rollDice() {
      if (!gameState || gameState.gameOver) return;
      const current = gameState.players[gameState.turnIdx];
      if (!current.isHuman || gameState.hasRolled) return;

      const d1 = Math.floor(Math.random() * 6) + 1;
      const d2 = Math.floor(Math.random() * 6) + 1;
      const total = d1 + d2;
      gameState.stepsLeft = total;
      gameState.hasRolled = true;
      current.inRoom = null;

      document.getElementById('dice-values').textContent = `${d1} + ${d2} = ${total}`;
      playMelody('dice');
      addGameLog(`🎲 ${current.char.shortName} tira los dados y saca un ${total} (${d1} y ${d2}).`);
      updateGameUI();
    }

    function getValidAdjacentMoves(player) {
      if (!player.isHuman || !gameState.hasRolled || gameState.stepsLeft <= 0) return [];
      const dirs = [[-1, 0], [1, 0], [0, -1], [0, 1]];
      const moves = [];
      dirs.forEach(([dr, dc]) => {
        const nr = player.r + dr;
        const nc = player.c + dc;
        if (nr >= 0 && nr < 11 && nc >= 0 && nc < 11) {
          const cell = BOARD_LAYOUT[nr][nc];
          if (cell === 'P' || cell === 'H' || cell.startsWith('D:')) {
            moves.push({ r: nr, c: nc, cell });
          }
        }
      });
      return moves;
    }

    function handleBoardCellClick(r, c) {
      if (!gameState || gameState.gameOver) return;
      const human = gameState.players[0];
      if (gameState.turnIdx !== 0 || !gameState.hasRolled || gameState.stepsLeft <= 0) return;

      const valid = getValidAdjacentMoves(human);
      const target = valid.find(m => m.r === r && m.c === c);
      if (!target) return;

      human.r = r;
      human.c = c;
      gameState.stepsLeft -= 1;

      if (target.cell === 'H') {
        const card = HELP_CARDS_DECK[Math.floor(Math.random() * HELP_CARDS_DECK.length)];
        addGameLog(`❓ ¡Casilla especial! Has robado la Carta de Ayuda "${card.title}": ${card.desc}`, 'highlight');
        applyHelpCardEffect(card);
      }

      if (target.cell.startsWith('D:')) {
        const roomId = target.cell.split(':')[1];
        const roomObj = ROOMS.find(rm => rm.id === roomId);
        human.inRoom = roomId;
        gameState.stepsLeft = 0;
        addGameLog(`🚪 Has entrado en ${roomObj.name}. ¡Puedes formular una hipótesis!`);
        updateGameUI();
        if (!gameState.hasHypothesizedThisTurn) {
          openHypothesisModal(roomObj);
        }
        return;
      }

      updateGameUI();
    }

    function applyHelpCardEffect(card) {
      const human = gameState.players[0];
      if (card.effect === 'bonus2') {
        gameState.stepsLeft += 2;
        showToast('🏃 ¡Atajo secreto! +2 pasos adicionales.', 'success');
      } else if (card.effect === 'teleport') {
        const randomRoom = ROOMS[Math.floor(Math.random() * ROOMS.length)];
        const door = DOOR_COORDS[randomRoom.id];
        human.r = door.r;
        human.c = door.c;
        human.inRoom = randomRoom.id;
        gameState.stepsLeft = 0;
        showToast(`🚪 ¡Pasillo libre! Te trasladas a ${randomRoom.name}.`, 'success');
        openHypothesisModal(randomRoom);
      } else {
        const unknownCards = gameState.players.slice(1).flatMap(p => p.hand).filter(c => gameState.notes[c.id] !== 1);
        if (unknownCards.length > 0) {
          const revealed = unknownCards[Math.floor(Math.random() * unknownCards.length)];
          gameState.notes[revealed.id] = 1;
          addGameLog(`✨ Pista obtenida: La carta "${revealed.name}" (${revealed.cat}) NO está en el Sobre Secreto.`, 'clue');
          showToast(`🔍 Pista revelada: ${revealed.name} descartado.`, 'success');
        }
      }
    }

    function renderBoardGrid() {
      const grid = document.getElementById('cluedo-board-grid');
      const human = gameState.players[0];
      const validMoves = getValidAdjacentMoves(human);

      let html = '';
      for (let r = 0; r < 11; r++) {
        for (let c = 0; c < 11; c++) {
          const code = BOARD_LAYOUT[r][c];
          const isValid = validMoves.some(m => m.r === r && m.c === c);
          const occupants = gameState.players.filter(p => p.r === r && p.c === c);

          let bgStyle = 'background-color: #F7E9D4;';
          let extraClasses = 'border border-[#D8C3A5]/70';
          let label = '';

          if (code === 'CENTER') {
            bgStyle = 'background-color: #FFF8EB;';
            extraClasses = 'border border-dorado';
            if (r === 5 && c === 5) label = '<span class="text-[9px] sm:text-[10px] font-display font-bold text-madera leading-none text-center">ARMONÍA</span>';
          } else if (code === 'H') {
            bgStyle = 'background-color: #FFE082;';
            label = '<span class="text-xs font-extrabold text-amber-900">❓</span>';
          } else if (code.startsWith('D:')) {
            const rId = code.split(':')[1];
            const rObj = ROOMS.find(rm => rm.id === rId);
            bgStyle = `background-color: ${rObj.bg};`;
            extraClasses = 'border-2 border-madera';
            label = `<span class="text-xs">${rObj.icon}</span>`;
          } else if (code !== 'P') {
            const rObj = ROOMS.find(rm => rm.id === code);
            bgStyle = `background-color: ${rObj.bg};`;
            extraClasses = 'border border-madera/20';
            if ((r === 1 && c === 1) || (r === 1 && c === 5) || (r === 1 && c === 9) ||
                (r === 4 && c === 1) || (r === 4 && c === 9) || (r === 7 && c === 9) ||
                (r === 9 && c === 1) || (r === 9 && c === 5) || (r === 10 && c === 10)) {
              label = `<span class="text-sm sm:text-base" title="${rObj.name}">${rObj.icon}</span>`;
            }
          }

          if (isValid) {
            extraClasses += ' ring-2 ring-lupa bg-emerald-200 cursor-pointer animate-pulse';
            bgStyle = 'background-color: #A5D6A7;';
          }

          const tokensHtml = occupants.map(occ => `
            <span title="${occ.char.name}" class="w-4 h-4 sm:w-5 sm:h-5 rounded-full border-2 border-white shadow text-[8px] sm:text-[9px] font-extrabold text-white flex items-center justify-center" style="background:${occ.char.color}">
              ${occ.char.shortName[0]}
            </span>
          `).join('');

          html += `
            <div onclick="handleBoardCellClick(${r}, ${c})" style="${bgStyle}" class="aspect-square rounded-md flex items-center justify-center relative ${extraClasses}">
              ${tokensHtml ? `<div class="flex flex-wrap items-center justify-center gap-0.5 z-10">${tokensHtml}</div>` : label}
            </div>
          `;
        }
      }
      grid.innerHTML = html;
    }

    function renderPlayerHand() {
      const box = document.getElementById('player-hand-cards');
      const hand = gameState.players[0].hand;
      box.innerHTML = hand.map(card => `
        <div class="bg-crema rounded-2xl p-2.5 border-2 border-pergamino text-center shadow-sm">
          <div class="text-xl mb-0.5">${card.icon}</div>
          <p class="font-display font-bold text-xs text-madera leading-tight">${card.name}</p>
          <span class="text-[10px] text-maderaSuave font-bold">${card.cat}</span>
        </div>
      `).join('');
    }

    function renderDetectiveNotebook() {
      const nb = document.getElementById('detective-notebook');
      const sections = [
        { title: '🕵️ Sospechosos (6)', items: CHARACTERS },
        { title: '🎻 Instrumentos', items: gameState.instrumentsPool },
        { title: '🏫 Estancias de Armonía (9)', items: ROOMS }
      ];

      nb.innerHTML = sections.map(sec => `
        <div>
          <p class="font-display font-bold text-xs uppercase tracking-wider text-maderaSuave mb-1">${sec.title}</p>
          <div class="space-y-1">
            ${sec.items.map(it => {
              const st = gameState.notes[it.id] || 0;
              const badge = st === 1
                ? '<span class="px-2 py-0.5 rounded bg-rose-100 text-rose-800 font-extrabold text-[11px]">❌ Descartado</span>'
                : st === 2
                  ? '<span class="px-2 py-0.5 rounded bg-amber-200 text-amber-950 font-extrabold text-[11px]">⭐ Sospechoso</span>'
                  : '<span class="px-2 py-0.5 rounded bg-white border border-pergamino text-maderaSuave text-[11px]">⬜ Dudoso</span>';
              const textStrike = st === 1 ? 'line-through opacity-55' : 'font-bold';
              return `
                <button onclick="toggleNotebookNote('${it.id}')" class="w-full flex items-center justify-between px-2.5 py-1.5 rounded-xl bg-white/85 hover:bg-dorado/25 border border-pergamino/80 text-left transition">
                  <span class="text-madera ${textStrike}">${it.name}</span>
                  ${badge}
                </button>
              `;
            }).join('')}
          </div>
        </div>
      `).join('');
    }

    function toggleNotebookNote(itemId) {
      if (!gameState) return;
      gameState.notes[itemId] = ((gameState.notes[itemId] || 0) + 1) % 3;
      renderDetectiveNotebook();
    }

    function openHypothesisModal(roomObj) {
      document.getElementById('hyp-room-name').textContent = roomObj.name;
      document.getElementById('hyp-suspect-select').innerHTML =
        CHARACTERS.map(c => `<option value="${c.id}">${c.name} (${c.country})</option>`).join('');
      document.getElementById('hyp-instrument-select').innerHTML =
        gameState.instrumentsPool.map(i => `<option value="${i.id}">${i.icon} ${i.name}</option>`).join('');
      document.getElementById('hypothesis-modal').classList.remove('hidden');
    }

    function closeHypothesisModal() {
      document.getElementById('hypothesis-modal').classList.add('hidden');
    }

    function submitHypothesis() {
      const human = gameState.players[0];
      const roomObj = ROOMS.find(r => r.id === human.inRoom);
      const susObj = CHARACTERS.find(c => c.id === document.getElementById('hyp-suspect-select').value);
      const instObj = gameState.instrumentsPool.find(i => i.id === document.getElementById('hyp-instrument-select').value);

      gameState.hasHypothesizedThisTurn = true;
      closeHypothesisModal();

      addGameLog(`🗣️ Hipótesis de ${human.char.shortName}: "Creo que ${susObj.name} robó ${instObj.name} y lo escondió en ${roomObj.name}".`, 'highlight');

      let refutedBy = null;
      let shownCard = null;
      for (let i = 1; i < gameState.players.length; i++) {
        const rival = gameState.players[i];
        const matches = rival.hand.filter(c => c.id === susObj.id || c.id === instObj.id || c.id === roomObj.id);
        if (matches.length > 0) {
          refutedBy = rival;
          shownCard = matches[Math.floor(Math.random() * matches.length)];
          break;
        }
      }

      if (refutedBy && shownCard) {
        gameState.notes[shownCard.id] = 1;
        addGameLog(`🤫 ${refutedBy.char.name} te enseña en secreto la carta "${shownCard.name}". ¡Queda descartada en tu hoja!`, 'clue');
        showToast(`🤫 ${refutedBy.char.shortName} refuta tu hipótesis con: ${shownCard.name}`, 'success');
      } else {
        addGameLog(`😮 ¡Ningún detective ha podido refutar tu hipótesis! Es una pista muy fuerte...`, 'clue');
        showToast('😮 ¡Nadie tiene ninguna de esas 3 cartas!', 'warning');
      }

      updateGameUI();
    }

    function endPlayerTurn() {
      if (!gameState || gameState.gameOver) return;
      gameState.hasRolled = false;
      gameState.hasHypothesizedThisTurn = false;
      gameState.stepsLeft = 0;

      for (let i = 1; i < gameState.players.length; i++) {
        const ai = gameState.players[i];
        const randomRoom = ROOMS[Math.floor(Math.random() * ROOMS.length)];
        const door = DOOR_COORDS[randomRoom.id];
        ai.r = door.r;
        ai.c = door.c;
        const randSus = CHARACTERS[Math.floor(Math.random() * CHARACTERS.length)];
        const randInst = gameState.instrumentsPool[Math.floor(Math.random() * gameState.instrumentsPool.length)];
        addGameLog(`🕵️ ${ai.char.shortName} entra en ${randomRoom.name} y pregunta por ${randSus.shortName} y ${randInst.name}.`);
      }

      gameState.turnIdx = 0;
      document.getElementById('dice-values').textContent = '-';
      updateGameUI();
    }

    function openAccusationModal() {
      if (!gameState) return;
      document.getElementById('acc-suspect-select').innerHTML =
        CHARACTERS.map(c => `<option value="${c.id}">${c.name}</option>`).join('');
      document.getElementById('acc-instrument-select').innerHTML =
        gameState.instrumentsPool.map(i => `<option value="${i.id}">${i.icon} ${i.name}</option>`).join('');
      document.getElementById('acc-room-select').innerHTML =
        ROOMS.map(r => `<option value="${r.id}">${r.icon} ${r.name}</option>`).join('');
      document.getElementById('accusation-modal').classList.remove('hidden');
    }

    function closeAccusationModal() {
      document.getElementById('accusation-modal').classList.add('hidden');
    }

    function submitFinalAccusation() {
      const susId = document.getElementById('acc-suspect-select').value;
      const instId = document.getElementById('acc-instrument-select').value;
      const roomId = document.getElementById('acc-room-select').value;

      closeAccusationModal();
      gameState.gameOver = true;

      const sec = gameState.secret;
      const won = susId === sec.suspect.id && instId === sec.instrument.id && roomId === sec.room.id;

      document.getElementById('outcome-emoji').textContent = won ? '🏆🎻🎉' : '✉️😅🔍';
      document.getElementById('outcome-title').textContent = won
        ? '¡Enhorabuena, Detective! Has resuelto el misterio'
        : '¡Oh, no coincidían las 3 cartas del Sobre Secreto!';
      document.getElementById('outcome-message').textContent = won
        ? `Has recuperado el instrumento antes del concierto anual de la Escuela Armonía. ¡Doña Beatriz Valcárcel te nombra Detective Honorario!`
        : `El culpable ha logrado escapar esta vez, pero ya conoces la verdad oculta en el sobre. ¡Inténtalo de nuevo!`;

      document.getElementById('outcome-secret-cards').innerHTML = `
        <div class="bg-white p-2.5 rounded-xl border border-pergamino">
          <span class="block text-lg">🕵️</span>
          <span>${sec.suspect.name}</span>
        </div>
        <div class="bg-white p-2.5 rounded-xl border border-pergamino">
          <span class="block text-lg">${sec.instrument.icon}</span>
          <span>${sec.instrument.name}</span>
        </div>
        <div class="bg-white p-2.5 rounded-xl border border-pergamino">
          <span class="block text-lg">${sec.room.icon}</span>
          <span>${sec.room.name}</span>
        </div>
      `;

      if (won) playMelody('victory');
      document.getElementById('outcome-modal').classList.remove('hidden');
    }

    function closeOutcomeModal() {
      document.getElementById('outcome-modal').classList.add('hidden');
      openNewGameModal();
    }

    // =========================================================================
    // 8. GENERADOR DE AVATARES INTERACTIVO (VISTA SIN FONDO Y PERFIL ACTIVO)
    // =========================================================================
    let currentAvatarCfg = { ...CHARACTERS[0].avatarConfig };

    const SKIN_PALETTE = ['#F9DEC9', '#F5D0B5', '#F3CBB2', '#D79E74', '#C68658', '#B57449', '#8D5524'];
    const HAIR_PALETTE = ['#212121', '#4E342E', '#795548', '#D4A359', '#C62828', '#757575', '#ECEFF1'];
    const OUTFIT_PALETTE = ['#2E7D32', '#B71C1C', '#6A1B9A', '#FBC02D', '#1565C0', '#AD1457', '#00838F'];
    const ITEM_OPTIONS = [
      { id: 'violin', label: '🎻 Violín Aurora' },
      { id: 'tambor', label: '🥁 Tambor' },
      { id: 'cello', label: '🎻 Violonchelo' },
      { id: 'piano', label: '🎼 Partitura' },
      { id: 'trompeta', label: '🎺 Trompeta' },
      { id: 'flauta', label: '🪈 Flauta' },
      { id: 'lupa', label: '🔍 Lupa Verde' }
    ];

    function initAvatarStudio() {
      document.getElementById('ctrl-skin').innerHTML = SKIN_PALETTE.map(hex =>
        `<button onclick="setAvatarProp('skin', '${hex}')" class="w-8 h-8 rounded-full border-2 border-madera/40 shadow-sm hover:scale-110 transition" style="background:${hex}"></button>`
      ).join('');

      document.getElementById('ctrl-haircolor').innerHTML = HAIR_PALETTE.map(hex =>
        `<button onclick="setAvatarProp('hairColor', '${hex}')" class="w-8 h-8 rounded-full border-2 border-madera/40 shadow-sm hover:scale-110 transition" style="background:${hex}"></button>`
      ).join('');

      document.getElementById('ctrl-outfitcolor').innerHTML = OUTFIT_PALETTE.map(hex =>
        `<button onclick="setAvatarProp('outfitColor', '${hex}')" class="w-8 h-8 rounded-full border-2 border-madera/40 shadow-sm hover:scale-110 transition" style="background:${hex}"></button>`
      ).join('');

      document.getElementById('ctrl-item').innerHTML = ITEM_OPTIONS.map(it =>
        `<button onclick="setAvatarProp('item', '${it.id}')" class="p-2 rounded-xl bg-white border-2 border-pergamino hover:border-lupa font-bold text-xs text-madera">${it.label}</button>`
      ).join('');

      renderAvatarPreview();
      renderInitialGallery();
    }

    function setAvatarProp(prop, val) {
      currentAvatarCfg[prop] = val;
      renderAvatarPreview();
    }

    function applyAvatarPreset(charId) {
      const ch = CHARACTERS.find(c => c.id === charId);
      if (!ch) return;
      currentAvatarCfg = { ...ch.avatarConfig };
      document.getElementById('avatar-name-input').value = ch.name;
      document.getElementById('ctrl-hair').value = currentAvatarCfg.hair;
      document.getElementById('ctrl-eyes').value = currentAvatarCfg.eyes;
      document.getElementById('ctrl-outfit').value = currentAvatarCfg.outfit;
      document.getElementById('ctrl-notes').checked = currentAvatarCfg.notes;
      renderAvatarPreview();
      showToast(`🎨 Plantilla cargada: ${ch.name}`, 'info');
    }

    function updateAvatarFromControls() {
      currentAvatarCfg.hair = document.getElementById('ctrl-hair').value;
      currentAvatarCfg.eyes = document.getElementById('ctrl-eyes').value;
      currentAvatarCfg.outfit = document.getElementById('ctrl-outfit').value;
      currentAvatarCfg.notes = document.getElementById('ctrl-notes').checked;
      renderAvatarPreview();
    }

    function renderAvatarPreview() {
      document.getElementById('avatar-preview-svg').innerHTML =
        generateSquareCharacterSVG(currentAvatarCfg);
    }

    function applyCustomAvatarAsProfile() {
      const name = document.getElementById('avatar-name-input').value.trim() || 'Detective Armonía';
      customProfileDetective = {
        id: 'custom_player',
        name,
        shortName: name.split(' ')[0],
        age: 'Detective',
        country: 'Escuela Armonía 🎼',
        instrument: 'Detective Invitado',
        color: currentAvatarCfg.outfitColor,
        isCustom: true,
        avatarConfig: { ...currentAvatarCfg }
      };
      renderGameSetupChoices();
      playMelody('victory');
      showToast(`🕵️‍♀️ ¡${name} guardado como tu detective! Ya puedes elegirlo en el Cluedo Online.`, 'success');
    }

    function saveAvatarToGallery() {
      const name = document.getElementById('avatar-name-input').value.trim() || 'Detective Anónimo';
      const svgMarkup = generateSquareCharacterSVG(currentAvatarCfg);

      const gallery = document.getElementById('avatar-gallery-grid');
      const card = document.createElement('div');
      card.className = 'bg-crema rounded-2xl p-3 border-2 border-dorado text-center space-y-2 animate-pop';
      card.innerHTML = `
        <div class="h-32 flex items-center justify-center p-1 drop-shadow-sm">
          <div class="h-full w-24 flex items-center justify-center">${svgMarkup}</div>
        </div>
        <p class="font-display font-bold text-xs text-madera truncate">${name}</p>
        <span class="inline-block text-[10px] font-extrabold bg-green-100 text-lupaOscuro px-2 py-0.5 rounded-full">Candidato Webserie</span>
      `;
      gallery.prepend(card);
      playMelody('victory');
      showToast(`🏆 ¡${name} publicado en la Galería del Concurso!`, 'success');
    }

    function submitFanDrawing() {
      const input = document.getElementById('fan-drawing-upload');
      if (!input.files || !input.files[0]) {
        showToast('🖍️ Selecciona primero una foto de tu dibujo hecho a mano.', 'warning');
        return;
      }
      playMelody('victory');
      showToast('🎉 ¡Dibujo recibido! Participas para protagonizar el próximo capítulo de YouTube Kids.', 'success');
      input.value = '';
    }

    function renderInitialGallery() {
      const gallery = document.getElementById('avatar-gallery-grid');
      gallery.innerHTML = CHARACTERS.slice(0, 4).map(ch => {
        const svgMarkup = generateSquareCharacterSVG(ch.avatarConfig);
        return `
          <div class="bg-crema rounded-2xl p-3 border-2 border-pergamino text-center space-y-1.5">
            <div class="h-32 flex items-center justify-center p-1 drop-shadow-sm">
              <div class="h-full w-24 flex items-center justify-center">${svgMarkup}</div>
            </div>
            <p class="font-display font-bold text-xs text-madera truncate">${ch.name}</p>
            <span class="inline-block text-[10px] font-bold text-maderaSuave">${ch.country}</span>
          </div>
        `;
      }).join('');
    }

    // =========================================================================
    // 9. INICIALIZACIÓN DE LOGOS TRANSPARENTES Y TODA LA APLICACIÓN
    // =========================================================================
    window.onload = function () {
      // Inyectar los logos transparentes directamente en cabecera, hero, intro y pie de página
      document.getElementById('header-logo-melodigma').innerHTML = SVG_LOGO_MELODIGMA;
      document.getElementById('header-logo-estel').innerHTML = SVG_LOGO_ESTEL;
      document.getElementById('hero-logo-melodigma').innerHTML = SVG_LOGO_MELODIGMA;
      document.getElementById('hero-logo-estel').innerHTML = SVG_LOGO_ESTEL;
      document.getElementById('footer-logo-melodigma').innerHTML = SVG_LOGO_MELODIGMA;
      document.getElementById('footer-logo-estel').innerHTML = SVG_LOGO_ESTEL;

      document.getElementById('transmedia-logos-box').innerHTML = `
        <div class="w-32 h-11">${SVG_LOGO_MELODIGMA}</div>
        <div class="w-20 h-11">${SVG_LOGO_ESTEL}</div>
      `;
      document.getElementById('intro-estel-box').innerHTML = `<div class="w-28 h-16">${SVG_LOGO_ESTEL}</div>`;
      document.getElementById('intro-melodigma-box').innerHTML = `<div class="w-40 h-16">${SVG_LOGO_MELODIGMA}</div>`;

      // Renderizar secciones principales
      renderInicioContent();
      renderGameSetupChoices();
      initAvatarStudio();
    };
  </script>
</body>
</html>
