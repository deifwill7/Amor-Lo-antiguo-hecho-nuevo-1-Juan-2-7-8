# Amor-Lo-antiguo-hecho-nuevo-1-Juan-2-7-8
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Análisis Interactivo y Mapa Mental: Amor - Lo Antiguo Hecho Nuevo</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        /* --- Configuración General --- */
        :root {
            --bg-color: #121212;
            --text-color: #f0f0f0;
            --line-color: #4a4a4a;
            --line-width: 2px;
            
            /* Colores base para cada rama principal */
            --color-branch-1: 3, 169, 244;     /* Azul */
            --color-branch-2: 255, 87, 34;   /* Naranja */
            --color-branch-3: 156, 39, 176;  /* Morado */
            --color-branch-4: 231, 76, 60;   /* Rojo */
            --color-branch-5: 0, 150, 136;   /* Turquesa */
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: #000000; /* Fondo negro */
        }
        .tab-button {
            transition: all 0.3s ease;
        }
        .tab-button.active {
            color: #d946ef; /* text-fuchsia-500 */
            border-bottom-color: #d946ef;
            background-color: #1f2937; /* bg-gray-800 */
        }
        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: block;
            animation: fadeIn 0.5s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* --- Estilos Acordeón (Pestaña 1) --- */
        .accordion-item { border-bottom: 1px solid #374151; }
        .accordion-header { cursor: pointer; transition: background-color 0.3s ease; }
        .accordion-header:hover { background-color: #1f2937; }
        .accordion-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.7s ease-in-out, padding 0.7s ease-in-out;
            padding: 0 1.5rem;
            background-color: #111827;
        }
        .accordion-content.open { max-height: 5000px; padding: 1.5rem; }
        .accordion-arrow { transition: transform 0.3s ease; }
        .open .accordion-arrow { transform: rotate(90deg); }
        .content-list { list-style: none; padding-left: 0; }
        .content-list li { padding-left: 2.5rem; position: relative; margin-bottom: 1.5rem; }
        .content-list li::before {
            content: attr(data-emoji);
            position: absolute; left: 0; top: -2px; font-size: 1.5rem;
        }

        /* --- Estilos Mapa Mental (Pestaña 2) --- */
        #mapaMental {
            background-color: var(--bg-color);
            color: var(--text-color);
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            display: flex;
            justify-content: center;
            padding: 40px;
            overflow-x: auto;
            border-radius: 0.5rem;
        }
        .mindmap { display: inline-block; text-align: center; }
        .mindmap ul { padding-left: 80px; position: relative; list-style: none; margin: 0; }
        .mindmap li { margin: 20px 0; position: relative; list-style: none; }
        .mindmap .node {
            background-color: rgba(var(--branch-color, 74, 74, 74), 0.2);
            border: var(--line-width) solid rgb(var(--branch-color, 100, 100, 100));
            padding: 8px 15px; border-radius: 8px; display: inline-block;
            position: relative; z-index: 1; min-width: 150px; text-align: center;
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }
        .mindmap .node:hover { transform: scale(1.05); box-shadow: 0 0 15px rgba(var(--branch-color), 0.7); }
        .mindmap > .node { --branch-color: 224, 224, 224; font-size: 1.2em; font-weight: bold; }
        .mindmap > ul > li:nth-child(1) { --branch-color: var(--color-branch-1); }
        .mindmap > ul > li:nth-child(2) { --branch-color: var(--color-branch-2); }
        .mindmap > ul > li:nth-child(3) { --branch-color: var(--color-branch-3); }
        .mindmap > ul > li:nth-child(4) { --branch-color: var(--color-branch-4); }
        .mindmap > ul > li:nth-child(5) { --branch-color: var(--color-branch-5); }
        .mindmap ul ul .node { background-color: rgba(var(--branch-color), 0.3); }
        .mindmap ul ul ul .node { background-color: rgba(var(--branch-color), 0.4); }
        .mindmap ul ul ul ul .node { background-color: rgba(var(--branch-color), 0.5); }
        .mindmap li .node::before {
            content: ''; position: absolute; top: 50%; left: -40px;
            width: 40px; height: var(--line-width); background-color: rgb(var(--branch-color)); z-index: 0;
        }
        .mindmap li::after {
            content: ''; position: absolute; top: 0; left: -40px;
            width: var(--line-width); height: 100%; background-color: rgb(var(--branch-color)); z-index: 0;
        }
        .mindmap li:first-child::after { top: 50%; height: 50%; }
        .mindmap li:last-child::after { height: 50%; }
        .mindmap li:only-child::after { display: none; }
        .mindmap ul::before {
            content: ''; position: absolute; top: 50%; left: 0;
            width: 40px; height: var(--line-width); background-color: rgb(var(--branch-color));
            transform: translateY(-50%);
        }
        .mindmap > ul::before, .mindmap > ul > li .node::before, .mindmap > ul > li::after { display: none; }
        .mindmap .toggle {
            position: absolute; right: -25px; top: 50%; transform: translateY(-50%);
            width: 18px; height: 18px; background-color: rgba(var(--branch-color), 0.8);
            color: var(--bg-color); border-radius: 50%; font-weight: bold;
            display: flex; align-items: center; justify-content: center;
            cursor: pointer; transition: transform 0.3s ease; font-size: 14px; user-select: none;
        }
        .mindmap .collapsible.collapsed > ul { display: none; }
    </style>
</head>
<body class="text-gray-200">

    <div class="container mx-auto p-4 md:p-8 max-w-7xl">
        
        <header class="text-center mb-12">
            <h1 class="text-3xl md:text-4xl font-bold text-fuchsia-500 mb-2">Análisis y Resumen Detallado del Sermón</h1>
            <p class="text-lg text-gray-400">"Amor: Lo antiguo hecho nuevo" (1 Juan 2:7-8)</p>
        </header>
        
        <!-- Pestañas -->
        <div class="mb-8 border-b-2 border-gray-700 flex justify-center">
            <button class="tab-button active text-gray-400 py-3 px-6 border-b-2 border-transparent text-lg font-semibold" onclick="openTab(event, 'analisis')">Análisis Detallado</button>
            <button class="tab-button text-gray-400 py-3 px-6 border-b-2 border-transparent text-lg font-semibold" onclick="openTab(event, 'mapaMental')">Mapa Mental</button>
        </div>

        <!-- Contenido Pestaña 1: Análisis Detallado -->
        <div id="analisis" class="tab-content active">
            <!-- Contenido del acordeón va aquí -->
             <p class="mb-8 text-center text-gray-300">El expositor presenta el mandamiento del amor en 1 Juan 2:7-8 como una verdad fundamental que combate la mentalidad de "consumismo espiritual" prevaleciente en la cultura moderna. El sermón se estructura en dos puntos principales que desentrañan la paradoja de un mandamiento que es a la vez antiguo y nuevo, demostrando que el amor práctico por los hermanos es la prueba definitiva de una fe genuina.</p>
            <div class="bg-black border border-fuchsia-800 rounded-lg shadow-lg shadow-fuchsia-500/10">
                <div class="accordion-item">
                    <div class="accordion-header flex justify-between items-center p-6">
                        <div class="flex items-center space-x-4"><span class="text-3xl">🛒</span><h2 class="text-xl font-semibold text-fuchsia-400">Introducción: De Consumidores a Familia</h2></div>
                        <span class="accordion-arrow text-fuchsia-400 text-2xl">▶</span>
                    </div>
                    <div class="accordion-content">
                        <p class="mb-6 text-gray-300">El sermón comienza con una poderosa crítica a la mentalidad consumista que moldea la vida moderna. El predicador describe cómo, desde pedir domicilios hasta elegir series en Netflix [02:22.855], "día tras día vivimos inmersos en un universo diseñado para nosotros" [03:02.455]. El peligro surge cuando esta mentalidad se traslada a la iglesia.</p>
                        <ul class="content-list">
                            <li data-emoji="💻"><strong class="text-white">El software del consumidor en la iglesia:</strong> Se plantea la pregunta retórica: al entrar a la iglesia, "¿nosotros apagamos ese software de consumidores? ¿O entramos a la casa de Dios con la misma mentalidad con la que entramos a un centro comercial?" [03:42.455]. Esta mentalidad lleva a calificar la experiencia —la alabanza, el sermón, el café— como si se tratara de un producto, transformando "el cuerpo de Cristo, la familia de Dios en servicios espirituales que yo tengo que consumir" [04:24.155].</li>
                            <li data-emoji="🛡️"><strong class="text-white">La iglesia como un ejército, no un espectáculo:</strong> Se establece un contraste radical. La iglesia "no es un espectáculo para evaluar, es un cuerpo en el que sufrimos y nos alegramos juntos. No es principalmente un lugar para ser servidos, es un ejército en el que somos llamados a servir" [05:00.755].</li>
                            <li data-emoji="❤️"><strong class="text-white">El mandamiento contracultural:</strong> El mandamiento del amor se presenta como la antítesis del consumismo, ya que "nos exige apagar el software del yo y encender el software del nosotros, de servir. Nos obliga a dejar de preguntar qué recibo y empezar a vivir la respuesta de cómo puedo amar, cómo puedo entregarme, cómo puedo dar, cómo puedo servir" [05:22.555].</li>
                        </ul>
                    </div>
                </div>
                <div class="accordion-item">
                    <div class="accordion-header flex justify-between items-center p-6">
                        <div class="flex items-center space-x-4"><span class="text-3xl">📜</span><h2 class="text-xl font-semibold text-fuchsia-400">1. El Mandamiento Antiguo que hemos tenido desde el principio</h2></div>
                        <span class="accordion-arrow text-fuchsia-400 text-2xl">▶</span>
                    </div>
                    <div class="accordion-content">
                        <p class="mb-6 text-gray-300">El primer punto, basado en el versículo 7, establece que el mandamiento de amar no es una innovación de Juan, sino una verdad fundamental que la iglesia ha conocido desde sus inicios y que tiene sus raíces en la misma creación y en la ley del Antiguo Testamento.</p>
                        <ul class="content-list">
                            <li data-emoji="📖"><strong class="text-white">Una enseñanza fundamental desde el principio:</strong> Juan se dirige a su audiencia como "Amados" [09:47.855] para recordarles una verdad que no es nueva. El "mandamiento antiguo" es la enseñanza del amor que "han tenido desde el principio" [12:33.855], es decir, desde el momento en que escucharon el evangelio por primera vez. El expositor enfatiza que el mensaje de salvación siempre iba acompañado del llamado a unirse a una comunidad de fe para amar a otros [14:28.355]. Convertirse implicaba unirse a una iglesia local.</li>
                            <li data-emoji="🧠"><strong class="text-white">La herejía del conocimiento sin amor:</strong> Se expone el contexto de los falsos maestros (gnósticos), quienes priorizaban una "iluminación interior" y un "conocimiento superior" (`gnosis`) por encima de los "mandamientos éticos como amarse" [23:25.255]. Para ellos, el amor "era para los principiantes" [23:51.955], mientras que la élite espiritual se dedicaba a asuntos más elevados. Juan combate esta herejía al afirmar que el amor no es opcional, sino la prueba de la verdadera fe.</li>
                            <li data-emoji="📜"><strong class="text-white">Las raíces del mandamiento en el Antiguo Testamento:</strong> El predicador argumenta que el mandamiento es "antiguo" porque se remonta a la creación ("No es bueno que el hombre qué, esté solo" - Génesis 2:18 [30:02.655]) y se codifica explícitamente en la ley. Se realiza una lectura detallada de <strong>Levítico 19:9-18</strong>, mostrando cómo el amor al prójimo se manifestaba en generosidad con los pobres, honestidad en los negocios, compasión por los vulnerables y justicia imparcial, culminando en el resumen: "Amarás a tu prójimo como a ti mismo" [34:05.455].</li>
                            <li data-emoji="🤔"><strong class="text-white">Segmento de Reflexión y Aplicación:</strong> Se confronta directamente la soberbia intelectual que puede existir en la iglesia. El expositor advierte sobre aquellos que "pueden debatir horas, horas sobre la cronología del milenio, pero no pueden pasar 10 minutos sirviendo a los hermanos" [27:26.455]. La conclusión es tajante y cita el versículo 9: "El que dice que está en la luz y aborrece a su hermano, está en tinieblas... Puedes tener la cabeza llena de teología, pero si no amas a tu hermano, eres mentiroso y la verdad no está en ti" [29:10.255, 29:26.155].</li>
                        </ul>
                    </div>
                </div>
                <div class="accordion-item border-b-0">
                    <div class="accordion-header flex justify-between items-center p-6">
                        <div class="flex items-center space-x-4"><span class="text-3xl">✨</span><h2 class="text-xl font-semibold text-fuchsia-400">2. El Mandamiento Nuevo que es verdadero en Cristo y en nosotros</h2></div>
                        <span class="accordion-arrow text-fuchsia-400 text-2xl">▶</span>
                    </div>
                    <div class="accordion-content">
                        <p class="mb-6 text-gray-300">El segundo punto, basado en el versículo 8, resuelve la aparente contradicción al explicar en qué sentido el mandamiento del amor es radicalmente "nuevo". La novedad no reside en el contenido del mandato, sino en el poder para cumplirlo y en el ejemplo perfecto que lo define.</p>
                        <ul class="content-list">
                            <li data-emoji="⚡"><strong class="text-white">La novedad de un nuevo poder:</strong> Citando a Jesús en <strong>Juan 13:34</strong> ("Un mandamiento nuevo les doy: que se amen los unos a los otros" [35:55.555]), el expositor explica que la novedad radica en "un nuevo poder que va a ser dado a la iglesia, que es el Espíritu Santo morando dentro del corazón del creyente" [36:24.155]. A diferencia de los santos del Antiguo Testamento, los creyentes del Nuevo Pacto reciben una "capacidad divina impartida" para cumplir el mandato, como fue prometido en <strong>Ezequiel 36:25-27</strong> [38:58.955].</li>
                            <li data-emoji="✝️"><strong class="text-white">Verdadero en Él (Cristo):</strong> El mandamiento es "verdadero en él" [43:17.955] porque Cristo es la "manifestación suprema, plena, completa del amor" [44:07.955]. Su amor no fue teórico, sino sacrificial. El predicador enfatiza que Jesús "recibió la ira de Dios por nosotros... Él se entregó, él asumió el peor castigo que pudiera existir por gente que no lo merecía" [45:01.855, 45:22.655]. Mirar a la cruz es ver la definición del amor verdadero.</li>
                            <li data-emoji="🤝"><strong class="text-white">Verdadero en ustedes (Los Creyentes):</strong> De manera sorprendente, el mandamiento también es verdadero "en ustedes" [47:07.955]. Esto no es un llamado a imitar a Cristo por nuestras propias fuerzas. La Biblia enseña que "al estar unido a Cristo, quien es el amor verdadero, él me da el poder y él me da la capacidad y él me da la gracia para amar a personas difíciles" [47:21.355]. En virtud de nuestra unión con Cristo, su vida fluye en nosotros, capacitándonos para amar.</li>
                            <li data-emoji="💡"><strong class="text-white">Segmento de Ánimo y Exhortación:</strong> La aplicación final es un llamado urgente al arrepentimiento del "individualismo" y el "egoísmo" [41:58.355], especialmente en el contexto cultural de Bogotá [42:06.955]. El expositor advierte: "Nadie puede salir diciendo, 'Me voy a esforzar más por amar'. Si sales diciendo eso, no entendiste nada" [54:05.855]. La solución no es el esfuerzo propio, sino "ir a la cruz, donde está ese nuevo poder, para que Dios por gracia me libre de mi egoísmo y me ayude a amar a otros" [54:17.255]. Se usa el ejemplo de <strong>2 Corintios 1:3-4</strong> para mostrar que incluso el sufrimiento es una oportunidad que Dios nos da para salir de nosotros mismos y consolar a otros [56:16.355].</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Contenido Pestaña 2: Mapa Mental -->
        <div id="mapaMental" class="tab-content">
            <div class="mindmap">
                <div class="node">Amor: Mandamiento Antiguo y Nuevo</div>
                <ul>
                    <li class="collapsible">
                        <div class="node">Introducción<span class="toggle">></span></div>
                        <ul>
                            <li><div class="node">Era del Consumismo</div></li>
                            <li class="collapsible"><div class="node">Mentalidad de Consumidor en la Iglesia<span class="toggle">></span></div>
                                <ul>
                                    <li class="collapsible"><div class="node">La Iglesia no es un Producto<span class="toggle">></span></div>
                                        <ul>
                                            <li><div class="node">No es un Club</div></li>
                                            <li><div class="node">Es una Familia</div></li>
                                            <li><div class="node">No es un Espectáculo</div></li>
                                            <li><div class="node">Es un Cuerpo</div></li>
                                            <li><div class="node">No para ser Servido</div></li>
                                            <li><div class="node">Es un Ejército para Servir</div></li>
                                        </ul>
                                    </li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Mandamiento Contrario a la Cultura<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Apagar el Software del 'Yo'</div></li>
                                    <li><div class="node">Encender el Software del 'Nosotros'</div></li>
                                    <li><div class="node">Preguntar '¿Cómo puedo amar?'</div></li>
                                </ul>
                            </li>
                            <li><div class="node">ADN de la Vida Cristiana: Dar Amor</div></li>
                            <li><div class="node">Amor Perfeccionado por Cristo</div></li>
                            <li><div class="node">Amor Práctico: Prueba de Salvación</div></li>
                        </ul>
                    </li>
                    <li class="collapsible">
                        <div class="node">Propósito de la Carta de Juan<span class="toggle">></span></div>
                        <ul>
                            <li class="collapsible"><div class="node">Refutar Herejía Gnóstica/Docetismo<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Jesús no vino en carne</div></li>
                                    <li><div class="node">Carne es mala, Espíritu es bueno</div></li>
                                    <li><div class="node">Énfasis en Conocimiento Superior (Gnosis)</div></li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Dar Certeza de Salvación<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Paso de Tinieblas a Luz</div></li>
                                    <li><div class="node">Crecimiento en Amor por Hermanos</div></li>
                                    <li><div class="node">Lucha contra el Pecado</div></li>
                                    <li><div class="node">Santificación</div></li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Cuatro Cosas a Lograr<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Gozo Completo</div></li>
                                    <li><div class="node">Santificación</div></li>
                                    <li><div class="node">Comunión con Dios y la Iglesia</div></li>
                                    <li><div class="node">Enfrentar el Pecado</div></li>
                                    <li><div class="node">Discernimiento Espiritual</div></li>
                                    <li><div class="node">Certeza en la Salvación</div></li>
                                </ul>
                            </li>
                            <li><div class="node">Logrado a través de Creer, Obedecer y Amar</div></li>
                        </ul>
                    </li>
                    <li class="collapsible">
                        <div class="node">El Mandamiento Antiguo (1 Juan 2:7)<span class="toggle">></span></div>
                        <ul>
                            <li><div class="node">Tono Afectuoso y Personal de Juan</div></li>
                            <li><div class="node">No es Mandamientos (Plural) sino Un Mandamiento (Singular)</div></li>
                            <li class="collapsible"><div class="node">Desde el Principio<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Día que Oyeron el Mensaje de Salvación</div></li>
                                    <li><div class="node">Continua Enseñanza del Amor</div></li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Es la Palabra que Han Oído (Logos)<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Evangelio acompañado de Amar al Prójimo</div></li>
                                    <li><div class="node">Ejemplo de Evangelismo del Nuevo Testamento</div></li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Implicaciones de la Conversión Temprana<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Dejar Vida, Familia, Amigos</div></li>
                                    <li><div class="node">Unirse a Comunidad de Fe para Amar</div></li>
                                    <li><div class="node">No es Cristianismo Aislado</div></li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Importancia de la Iglesia Local<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">No paredes, sino Gente</div></li>
                                    <li><div class="node">Unirse para Amar, Entregarse, tener Comunión</div></li>
                                    <li><div class="node">Ejemplo del Futbolista sin Equipo</div></li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Respuesta a Acusaciones de Falsos Maestros<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">No introduce nada 'Novedoso'</div></li>
                                    <li><div class="node">Énfasis en Amor es Contracultural</div></li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Falso Conocimiento vs. Verdadero Amor<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Gnósticos: Conocimiento Espiritual Superior</div></li>
                                    <li><div class="node">Menosprecian el Amar/Servir a Otros</div></li>
                                    <li><div class="node">Verdadero Cristiano: Ama a Otros</div></li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Origen del Mandamiento Antiguo<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Creación (Génesis 2:18): Hombre no fue diseñado para estar solo</div></li>
                                    <li class="collapsible"><div class="node">Antiguo Testamento (Levítico 19:9-18): Amar al Prójimo<span class="toggle">></span></div>
                                        <ul>
                                            <li><div class="node">Ser Generoso y Proveedor</div></li>
                                            <li><div class="node">Honesto e Íntegro</div></li>
                                            <li><div class="node">Protector y Compasivo con Indefensos</div></li>
                                            <li><div class="node">Justo e Imparcial</div></li>
                                            <li><div class="node">Cuidar Reputación Ajena</div></li>
                                            <li><div class="node">Actuar Correctivamente Piadoso</div></li>
                                            <li><div class="node">No Vengarse ni Guardar Rencor</div></li>
                                        </ul>
                                    </li>
                                </ul>
                            </li>
                        </ul>
                    </li>
                    <li class="collapsible">
                        <div class="node">El Mandamiento Nuevo (1 Juan 2:8)<span class="toggle">></span></div>
                        <ul>
                            <li><div class="node">Verdadero en Él (Cristo) y en Ustedes</div></li>
                            <li class="collapsible"><div class="node">Nuevo por un Nuevo Poder<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Espíritu Santo Morando en el Creyente</div></li>
                                    <li><div class="node">Capacita para Amar al Prójimo</div></li>
                                </ul>
                            </li>
                            <li><div class="node">Nuevo Pacto (Ezequiel 36:25): Corazón de Carne</div></li>
                            <li><div class="node">Creyentes del Nuevo Testamento: Poder para Amar</div></li>
                            <li><div class="node">Ejemplo del Buen Samaritano: Jesús Encarna el Amor</div></li>
                            <li><div class="node">Iglesia: Poder Único para Crecer en Amor</div></li>
                            <li><div class="node">Arrepentimiento del Individualismo/Egoísmo</div></li>
                            <li class="collapsible"><div class="node">Amor Verdadero en Cristo<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Dios es la Fuente de Amor</div></li>
                                    <li><div class="node">Cristo Encarnó el Amor Sacrificial</div></li>
                                    <li><div class="node">Murió por Pecadores</div></li>
                                    <li><div class="node">Traspasó Prejuicios (raza, género)</div></li>
                                    <li><div class="node">Acogió Marginados, Débiles, Ricos</div></li>
                                    <li><div class="node">Amor Humilde, Personal, Restaurador</div></li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Amor Verdadero en Ustedes<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Unión con Cristo da Poder para Amar</div></li>
                                    <li><div class="node">Amar Personas Difíciles en la Iglesia</div></li>
                                    <li><div class="node">Rama Unida a la Vid (Juan 15)</div></li>
                                </ul>
                            </li>
                            <li class="collapsible"><div class="node">Las Tinieblas Van Pasando y la Luz Verdadera Alumbra<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">Dios Disipa Tinieblas en Mundo y Corazón</div></li>
                                    <li><div class="node">Cristo es la Luz Verdadera</div></li>
                                </ul>
                            </li>
                        </ul>
                    </li>
                     <li class="collapsible">
                        <div class="node">Diagnóstico de la Fe (1 Juan 2:9)<span class="toggle">></span></div>
                        <ul>
                            <li><div class="node">El que dice estar en la luz y aborrece a su hermano, está en tinieblas</div></li>
                            <li><div class="node">No importa cuánto sabes si no amas</div></li>
                            <li class="collapsible"><div class="node">Amar al Prójimo: Un Llamado al Arrepentimiento del Egoísmo<span class="toggle">></span></div>
                                <ul>
                                    <li><div class="node">No esforzarse más, sino ir a la Cruz</div></li>
                                    <li><div class="node">Unidos a Cristo hay Poder para Perdonar, Servir, Dar</div></li>
                                    <li><div class="node">Planificar Tiempo Familiar para Amar a Otros</div></li>
                                </ul>
                            </li>
                            <li><div class="node">Consuelo en el Sufrimiento (2 Corintios 1:3): Para Consolar a Otros</div></li>
                        </ul>
                    </li>
                </ul>
            </div>
        </div>

        <footer class="text-center mt-12 text-gray-500 text-sm">
            <p>Navega entre las pestañas y haz clic en cada sección para expandir el contenido.</p>
        </footer>
    </div>

    <script>
        // --- SCRIPT PARA PESTAÑAS ---
        function openTab(evt, tabName) {
            let i, tabcontent, tablinks;
            tabcontent = document.getElementsByClassName("tab-content");
            for (i = 0; i < tabcontent.length; i++) {
                tabcontent[i].style.display = "none";
                tabcontent[i].classList.remove("active");
            }
            tablinks = document.getElementsByClassName("tab-button");
            for (i = 0; i < tablinks.length; i++) {
                tablinks[i].classList.remove("active");
            }
            document.getElementById(tabName).style.display = "block";
            document.getElementById(tabName).classList.add("active");
            evt.currentTarget.classList.add("active");
        }

        // --- SCRIPT PARA ACORDEÓN ---
        document.addEventListener('DOMContentLoaded', function() {
            const accordionItems = document.querySelectorAll('.accordion-item');
            accordionItems.forEach(item => {
                const header = item.querySelector('.accordion-header');
                const content = item.querySelector('.accordion-content');
                header.addEventListener('click', () => {
                    const isOpen = content.classList.contains('open');
                    document.querySelectorAll('.accordion-content').forEach(c => {
                        if (c !== content) {
                           c.classList.remove('open');
                           c.parentElement.querySelector('.accordion-header').classList.remove('open');
                        }
                    });
                    content.classList.toggle('open');
                    header.classList.toggle('open');
                });
            });

            // --- SCRIPT PARA MAPA MENTAL ---
            const collapsibleItems = document.querySelectorAll('.mindmap li:has(ul)');
            collapsibleItems.forEach(item => {
                item.classList.add('collapsible', 'collapsed');
                const node = item.querySelector(':scope > .node');
                if (node) {
                    node.style.cursor = 'pointer';
                    node.addEventListener('click', (event) => {
                        event.stopPropagation();
                        item.classList.toggle('collapsed');
                    });
                }
            });
            const firstLevelItems = document.querySelectorAll('.mindmap > ul > li.collapsible');
            firstLevelItems.forEach(item => {
                item.classList.remove('collapsed');
            });
        });
    </script>

</body>
</html>
