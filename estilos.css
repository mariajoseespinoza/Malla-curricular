<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Malla Curricular | Terapia Ocupacional</title>
    <!-- Carga de Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        /* Configuración de color base según la paleta solicitada */
        :root {
            --color-dark-bg: #1A1A1A; /* Negro Oscuro */
            --color-card-bg: #2C2C2C; /* Gris Oscuro para Tarjetas */
            --color-gold: #FFD700; /* Dorado */
            --color-gold-light: #FFEB8C; /* Dorado más claro para texto */
            --color-rose: #602A4A; /* Rosado Oscuro/Bloqueado */
            --color-rose-pastel: #FADADD; /* Rosado Pastel/Texto principal */
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--color-dark-bg);
            color: var(--color-rose-pastel);
            padding: 20px;
        }

        /* Estilos personalizados para los ramos */
        .ramo-card {
            background-color: var(--color-card-bg);
            cursor: pointer;
            transition: all 0.2s ease-in-out;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
            border: 2px solid transparent;
            min-height: 100px;
        }
        
        /* Estado NO APROBADO (por defecto) */
        .ramo-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 10px rgba(0, 0, 0, 0.4);
            border-color: var(--color-rose);
        }

        /* Estado APROBADO */
        .aprobado {
            background-color: var(--color-gold);
            color: var(--color-dark-bg);
            text-decoration: line-through;
            opacity: 0.85;
            pointer-events: none; /* No se puede volver a hacer clic */
            transform: scale(0.98);
        }
        .aprobado .title {
            font-weight: 700;
        }

        /* Estado BLOQUEADO (Requisitos no cumplidos) */
        .bloqueado {
            background-color: var(--color-rose);
            color: var(--color-rose-pastel);
            opacity: 0.5;
            cursor: not-allowed;
            border-style: dashed;
        }
        .bloqueado:hover {
             border-color: var(--color-rose-pastel);
             transform: none; /* Desactiva el lift en hover */
        }

        /* Estilo para el contenedor de la malla (columnas responsivas) */
        #curriculum-grid {
            display: grid;
            grid-template-columns: repeat(2, minmax(0, 1fr)); /* 2 columnas por defecto */
            gap: 20px;
        }
        /* Media query para tabletas y escritorios (más de 768px) */
        @media (min-width: 768px) {
            #curriculum-grid {
                grid-template-columns: repeat(5, minmax(0, 1fr)); /* 5 columnas en desktop/tablet */
            }
        }
        /* Media query para pantallas extra grandes (más de 1280px) */
        @media (min-width: 1280px) {
            #curriculum-grid {
                grid-template-columns: repeat(10, minmax(0, 1fr)); /* 10 columnas en pantallas grandes */
            }
        }

        /* Estilo para la notificación/modal de requisitos */
        #notification-box {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: var(--color-card-bg);
            border: 3px solid var(--color-gold);
            z-index: 100;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.8);
            max-width: 90%;
            display: none; /* Inicialmente oculto */
        }
        
        .semester-title {
            color: var(--color-gold-light);
            font-size: 1.25rem;
            font-weight: 700;
            margin-bottom: 10px;
            padding: 5px 0;
            border-bottom: 2px solid var(--color-rose);
        }
    </style>
</head>
<body class="p-4 md:p-8">

    <!-- Encabezado -->
    <header class="text-center mb-10">
        <h1 class="text-4xl md:text-5xl font-extrabold text-white mb-2">
            Malla Curricular Interactiva
        </h1>
        <p class="text-lg md:text-xl font-light text-rose-pastel">Terapia Ocupacional - Sigue tu progreso</p>
    </header>

    <!-- Contenedor de Notificaciones (Bloqueado) -->
    <div id="notification-box" class="p-6 rounded-lg">
        <h3 class="text-xl font-bold mb-3 text-red-400">¡Ramo Bloqueado!</h3>
        <p id="notification-message" class="text-base text-white mb-4"></p>
        <button onclick="document.getElementById('notification-box').style.display = 'none';"
                class="w-full py-2 bg-rose-500 hover:bg-rose-600 text-white font-semibold rounded-md transition duration-150">
            Entendido
        </button>
    </div>

    <!-- Contenedor Principal de la Malla -->
    <div id="curriculum-grid">
        <!-- Los semestres se renderizarán aquí -->
    </div>

    <!-- Pie de página o Controles -->
    <footer class="text-center mt-10 p-4 border-t border-rose-900">
        <button onclick="resetCurriculum();"
                class="px-6 py-2 bg-gray-600 hover:bg-gray-700 text-rose-pastel font-semibold rounded-full transition duration-150 shadow-lg">
            Reiniciar Malla
        </button>
        <p class="mt-4 text-sm text-gray-500">Haz clic en un ramo para marcarlo como aprobado.</p>
    </footer>

    <!-- Bloque de Script JS -->
    <script>
        // --- 1. Definición de la Malla Curricular con Requisitos ---
        // Estructura: {[nombre del ramo]: {semestre: N, requisitos: ['Ramo A', 'Ramo B']}}
        const curriculumData = {
            // Semestre 1
            'morfología basica': { semestre: 1, requisitos: [] },
            'biología celular': { semestre: 1, requisitos: [] },
            'introducción a la terapia ocupacional': { semestre: 1, requisitos: [] },
            'destrezas y actividades terapéuticas': { semestre: 1, requisitos: [] },
            'psicología aplicada a la salud': { semestre: 1, requisitos: [] },
            'Antropología': { semestre: 1, requisitos: [] },
            
            // Semestre 2
            'morfología aplicada a la Terapia Ocupacional': { semestre: 2, requisitos: ['morfología basica'] },
            'integrado a la fisiología y fisiopatologia 1': { semestre: 2, requisitos: ['biología celular'] },
            'fundamentos de la terapia ocupacional': { semestre: 2, requisitos: ['introducción a la terapia ocupacional'] },
            'Destrezas y actividades terapéuticas ll': { semestre: 2, requisitos: ['destrezas y actividades terapéuticas'] },
            'teorías de la psicología y curso de vida': { semestre: 2, requisitos: ['psicología aplicada a la salud'] },

            // Semestre 3
            'Salud Digital': { semestre: 3, requisitos: [] },
            'integrado a la fisiología y fisiopatologia 2': { semestre: 3, requisitos: ['integrado a la fisiología y fisiopatologia 1'] },
            'Marcos de Referencia y Modelos de Intervención en Terapia Ocupacional I': { semestre: 3, requisitos: ['fundamentos de la terapia ocupacional'] },
