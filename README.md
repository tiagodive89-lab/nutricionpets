# nutricionpets
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VetNutri - Formulador Profesional de Dietas para Mascotas</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts (Inter) -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght=300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- FontAwesome para iconos de veterinaria y mascotas -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col">

    <!-- Encabezado Principal -->
    <header class="bg-teal-700 text-white shadow-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 flex flex-col sm:flex-row justify-between items-center">
            <div class="flex items-center space-x-3 mb-2 sm:mb-0">
                <span class="bg-white text-teal-700 p-2.5 rounded-full text-xl font-bold flex items-center justify-center shadow-inner">
                    <i class="fa-solid fa-paw"></i>
                </span>
                <div>
                    <h1 class="text-2xl font-extrabold tracking-tight">VetNutri <span class="text-teal-200 font-light text-lg">Pro</span></h1>
                    <p class="text-xs text-teal-100">Formulador de Dietas Naturales según FEDIAF, NRC, Tablas Brasileñas e ICBF</p>
                </div>
            </div>
            <div class="flex space-x-2 text-sm bg-teal-800/50 p-1.5 rounded-lg border border-teal-600">
                <span class="px-2 py-1 bg-teal-600 rounded text-white font-medium shadow-sm">
                    <i class="fa-solid fa-book-open mr-1"></i> Fórmulas Validadas
                </span>
                <span class="px-2 py-1 text-teal-200">
                    <i class="fa-solid fa-brain mr-1"></i> Soporte IA Gemini
                </span>
            </div>
        </div>
    </header>

    <!-- Contenido Principal -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
            
            <!-- COLUMNA IZQUIERDA: Paciente y Requerimientos (4 cols) -->
            <section class="lg:col-span-5 space-y-6">
                <!-- Tarjeta de Datos del Paciente -->
                <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
                    <div class="flex items-center justify-between border-b border-slate-100 pb-4 mb-4">
                        <h2 class="text-lg font-bold text-slate-900 flex items-center gap-2">
                            <i class="fa-solid fa-address-card text-teal-600"></i>
                            1. Perfil del Paciente
                        </h2>
                        <span class="text-xs bg-slate-100 text-slate-600 px-2 py-1 rounded-full font-medium">Fisiología</span>
                    </div>

                    <form id="petForm" class="space-y-4">
                        <!-- Nombre y Especie -->
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-xs font-semibold text-slate-500 uppercase tracking-wider mb-1">Nombre</label>
                                <input type="text" id="petName" value="Max" class="w-full rounded-xl border border-slate-300 px-3 py-2 text-sm focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-500 uppercase tracking-wider mb-1">Especie</label>
                                <select id="petSpecies" class="w-full rounded-xl border border-slate-300 px-3 py-2 text-sm focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition" onchange="updatePhysiologicalStates()">
                                    <option value="perro">🐶 Perro</option>
                                    <option value="gato">🐱 Gato</option>
                                </select>
                            </div>
                        </div>

                        <!-- Peso y Estándar de Fórmulas -->
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-xs font-semibold text-slate-500 uppercase tracking-wider mb-1">Peso (kg)</label>
                                <div class="relative">
                                    <input type="number" id="petWeight" value="10" step="0.1" min="0.1" class="w-full rounded-xl border border-slate-300 pl-3 pr-8 py-2 text-sm focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition">
                                    <span class="absolute right-3 top-1/2 -translate-y-1/2 text-slate-400 text-xs font-semibold">kg</span>
                                </div>
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-500 uppercase tracking-wider mb-1">Guía Científica</label>
                                <select id="energyStandard" class="w-full rounded-xl border border-slate-300 px-3 py-2 text-sm focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition">
                                    <option value="fediaf">FEDIAF (Europa)</option>
                                    <option value="nrc">NRC (Estados Unidos)</option>
                                </select>
                            </div>
                        </div>

                        <!-- Estado Fisiológico (Se actualiza dinámicamente) -->
                        <div>
                            <label class="block text-xs font-semibold text-slate-500 uppercase tracking-wider mb-1">Condición Fisiológica</label>
                            <select id="physiologicalState" class="w-full rounded-xl border border-slate-300 px-3 py-2 text-sm focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition" onchange="calculateEnergyRequirement()"></select>
                            <p id="stateDescription" class="text-xs text-slate-500 mt-1 italic"></p>
                        </div>
                    </form>
                </div>

                <!-- Tarjeta de Requerimientos Energéticos y Nutricionales Calculados -->
                <div class="bg-gradient-to-br from-teal-50 to-emerald-50 rounded-2xl shadow-sm border border-teal-100 p-6">
                    <div class="flex items-center justify-between border-b border-teal-100 pb-4 mb-4">
                        <h3 class="text-lg font-bold text-teal-900 flex items-center gap-2">
                            <i class="fa-solid fa-calculator text-teal-700"></i>
                            2. Meta Nutricional Diaria
                        </h3>
                        <span class="bg-teal-100 text-teal-800 text-xs px-2.5 py-0.5 rounded-full font-bold uppercase" id="calcSource">FEDIAF / NRC</span>
                    </div>

                    <div class="space-y-4">
                        <!-- RER y DER -->
                        <div class="grid grid-cols-2 gap-4">
                            <div class="bg-white/80 backdrop-blur rounded-xl p-3 border border-teal-100">
                                <span class="text-[10px] uppercase tracking-wider font-semibold text-slate-500">RER (Reposo)</span>
                                <div class="text-lg font-extrabold text-teal-800" id="rerVal">0 <span class="text-xs font-normal text-slate-500">kcal</span></div>
                                <p class="text-[10px] text-slate-400 mt-0.5">70 × (Peso)<sup>0.75</sup></p>
                            </div>
                            <div class="bg-white/80 backdrop-blur rounded-xl p-3 border border-emerald-200 shadow-sm">
                                <span class="text-[10px] uppercase tracking-wider font-semibold text-emerald-700 font-bold">DER (Energía Diaria)</span>
                                <div class="text-xl font-black text-emerald-800" id="derVal">0 <span class="text-xs font-normal text-slate-500">kcal</span></div>
                                <p class="text-[10px] text-emerald-600/80 mt-0.5" id="derFormulaUsed">Requerimiento de ración</p>
                            </div>
                        </div>

                        <!-- Límites de Nutrientes Mínimos Sugeridos -->
                        <div class="bg-white rounded-xl p-4 border border-slate-100 space-y-2 text-xs">
                            <div class="text-slate-500 font-semibold uppercase tracking-wider text-[10px] border-b pb-1 mb-2">Requerimientos Mínimos (por cada 1000 kcal ME)</div>
                            
                            <div class="flex justify-between">
                                <span class="text-slate-600">Proteína Mínima:</span>
                                <span class="font-bold text-slate-800" id="reqProtein">-- g</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-slate-600">Grasa Mínima:</span>
                                <span class="font-bold text-slate-800" id="reqFat">-- g</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-slate-600">Calcio Mínimo:</span>
                                <span class="font-bold text-slate-800" id="reqCalcium">-- g</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-slate-600">Fósforo Mínimo:</span>
                                <span class="font-bold text-slate-800" id="reqPhosphorus">-- g</span>
                            </div>
                            <div class="flex justify-between border-t pt-1.5 mt-1">
                                <span class="text-slate-600 font-medium">Relación Ca:P Optima:</span>
                                <span class="font-bold text-amber-700 bg-amber-50 px-2 rounded">1.1 : 1 a 1.8 : 1</span>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- COLUMNA DERECHA: Formulador Interactivo de Dieta (7 cols) -->
            <section class="lg:col-span-7 space-y-6">
                <!-- Tarjeta Formuladora Principal -->
                <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
                    <div class="flex flex-col sm:flex-row justify-between sm:items-center border-b border-slate-100 pb-4 mb-4 gap-2">
                        <div>
                            <h2 class="text-lg font-bold text-slate-900 flex items-center gap-2">
                                <i class="fa-solid fa-utensils text-teal-600"></i>
                                3. Formulador de Dieta Receta Natural
                            </h2>
                            <p class="text-xs text-slate-500">Agrega ingredientes y ajusta sus porciones en gramos para balancear la mezcla.</p>
                        </div>
                        <div class="flex gap-2">
                            <button type="button" onclick="suggestRecipeWithAI()" class="text-xs bg-indigo-600 hover:bg-indigo-700 text-white px-3 py-1.5 rounded-lg font-semibold transition flex items-center gap-1 shadow-sm">
                                <i class="fa-solid fa-wand-magic-sparkles"></i> ✨ Sugerir Receta con IA
                            </button>
                            <button type="button" onclick="resetFormulator()" class="text-xs text-rose-600 hover:bg-rose-50 px-2.5 py-1.5 rounded-lg border border-rose-200 transition font-medium">
                                <i class="fa-solid fa-trash mr-1"></i> Reiniciar
                            </button>
                        </div>
                    </div>

                    <!-- Mensaje de Sugerencia de Receta IA en caso de carga -->
                    <div id="aiSuggestionLoader" class="hidden bg-indigo-50 border border-indigo-200 text-indigo-900 rounded-xl p-4 mb-4 flex items-center gap-3 animate-pulse">
                        <i class="fa-solid fa-robot text-2xl text-indigo-600 animate-spin"></i>
                        <div class="text-xs">
                            <p class="font-bold">Calculando fórmula ideal...</p>
                            <p class="text-indigo-700">Analizando aporte de aminoácidos, lípidos y relación Ca:P balanceada con base en las tablas seleccionadas.</p>
                        </div>
                    </div>

                    <!-- Panel de Explicación de Receta Propuesta -->
                    <div id="recipeExplanationPanel" class="hidden bg-amber-50 border border-amber-200 text-slate-700 rounded-xl p-4 mb-4 text-xs space-y-2 relative">
                        <button onclick="hideExplanationPanel()" class="absolute top-2 right-2 text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-sm"></i></button>
                        <h4 class="font-bold text-amber-900 flex items-center gap-1">
                            <i class="fa-solid fa-circle-info text-amber-700"></i>
                            Estrategia de la Receta Balanceada Sugerida:
                        </h4>
                        <p id="recipeExplanationText" class="italic leading-relaxed"></p>
                    </div>

                    <!-- Agregar Ingrediente -->
                    <div class="bg-slate-50 rounded-xl p-4 border border-slate-200 mb-6">
                        <span class="block text-xs font-semibold text-slate-500 uppercase tracking-wider mb-2">Añadir Nuevo Ingrediente (Tablas Brasileñas / ICBF Colombia)</span>
                        <div class="grid grid-cols-1 md:grid-cols-12 gap-3 items-end">
                            <div class="md:col-span-6">
                                <select id="ingredientSelector" class="w-full rounded-xl border border-slate-300 px-3 py-2 text-sm focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition">
                                    <!-- Se llena dinámicamente en JavaScript -->
                                </select>
                            </div>
                            <div class="md:col-span-3">
                                <div class="relative">
                                    <input type="number" id="ingredientAmount" placeholder="Cant." min="1" class="w-full rounded-xl border border-slate-300 pl-3 pr-8 py-2 text-sm focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition">
                                    <span class="absolute right-3 top-1/2 -translate-y-1/2 text-slate-400 text-xs font-semibold">g</span>
                                </div>
                            </div>
                            <div class="md:col-span-3">
                                <button type="button" onclick="addSelectedIngredient()" class="w-full bg-teal-600 hover:bg-teal-700 text-white font-semibold py-2 px-4 rounded-xl text-sm shadow transition duration-200 flex items-center justify-center gap-1.5">
                                    <i class="fa-solid fa-plus"></i> Añadir
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Lista de ingredientes añadidos -->
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="border-b border-slate-200 text-slate-400 text-[10px] uppercase font-bold tracking-wider">
                                    <th class="pb-2 w-2/5">Ingrediente</th>
                                    <th class="pb-2 text-center">Base Datos</th>
                                    <th class="pb-2 text-right">Cant. (g)</th>
                                    <th class="pb-2 text-right">Energía (kcal)</th>
                                    <th class="pb-2 text-right">Pro (g)</th>
                                    <th class="pb-2 text-right">Gra (g)</th>
                                    <th class="pb-2 text-center">Acciones</th>
                                </tr>
                            </thead>
                            <tbody id="recipeTableBody" class="divide-y divide-slate-100 text-sm">
                                <!-- Se llena dinámicamente -->
                                <tr id="emptyTableMessage">
                                    <td colspan="7" class="py-8 text-center text-slate-400">
                                        <div class="flex flex-col items-center justify-center space-y-2">
                                            <i class="fa-solid fa-bowl-food text-3xl text-slate-300 animate-pulse"></i>
                                            <p>No has añadido ingredientes a la ración de hoy.</p>
                                        </div>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- Reporte Nutricional & Balance de Dieta -->
                <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
                    <div class="flex items-center justify-between border-b border-slate-100 pb-4 mb-4">
                        <h2 class="text-lg font-bold text-slate-900 flex items-center gap-2">
                            <i class="fa-solid fa-chart-pie text-teal-600"></i>
                            4. Diagnóstico Nutricional de la Receta
                        </h2>
                        <span class="text-xs text-slate-500 font-semibold" id="recipeTotalGrams">0g formulados</span>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <!-- Lado Izquierdo: Resumen de totales energéticos y Ca:P -->
                        <div class="space-y-4">
                            <!-- Energía aportada vs Meta -->
                            <div class="bg-slate-50 rounded-xl p-4 border border-slate-100">
                                <div class="flex justify-between items-center mb-1">
                                    <span class="text-xs font-semibold text-slate-500 uppercase tracking-wider">Energía Metabolizable Total</span>
                                    <span class="text-xs font-medium text-slate-600" id="energyRatioLabel">0 / 0 kcal</span>
                                </div>
                                <div class="flex items-baseline space-x-1.5 mb-2">
                                    <span class="text-2xl font-black text-teal-800" id="recipeTotalCalories">0</span>
                                    <span class="text-xs text-slate-500">kcal de EM aportados</span>
                                </div>
                                <div class="w-full bg-slate-200 rounded-full h-2.5 overflow-hidden">
                                    <div id="energyProgressBar" class="bg-teal-600 h-2.5 rounded-full transition-all duration-300" style="width: 0%"></div>
                                </div>
                            </div>

                            <!-- Relación Calcio : Fósforo -->
                            <div class="bg-slate-50 rounded-xl p-4 border border-slate-100">
                                <div class="flex justify-between items-center mb-1">
                                    <span class="text-xs font-semibold text-slate-500 uppercase tracking-wider">Relación Calcio : Fósforo (Ca:P)</span>
                                    <span class="text-xs font-bold text-emerald-700 bg-emerald-50 px-1.5 py-0.5 rounded" id="caPRatioBadge">Ca:P --</span>
                                </div>
                                <div class="grid grid-cols-2 gap-2 text-xs mt-2">
                                    <div class="bg-white rounded p-2 text-center border">
                                        <div class="text-slate-400 text-[9px] uppercase font-bold">Calcio</div>
                                        <div class="font-bold text-slate-700" id="totalCalcium">0 mg</div>
                                    </div>
                                    <div class="bg-white rounded p-2 text-center border">
                                        <div class="text-slate-400 text-[9px] uppercase font-bold">Fósforo</div>
                                        <div class="font-bold text-slate-700" id="totalPhosphorus">0 mg</div>
                                    </div>
                                </div>
                                <p class="text-[10px] text-slate-400 mt-2 text-center italic">Meta segura: entre 1.1:1 y 1.8:1 para evitar descalcificación u osteodistrofia.</p>
                            </div>
                        </div>

                        <!-- Lado Derecho: Barras de cumplimiento por cada 1000 kcal -->
                        <div class="space-y-4">
                            <span class="text-xs font-semibold text-slate-500 uppercase tracking-wider block">Nutrientes por cada 1000 kcal de Receta</span>
                            
                            <!-- Proteína -->
                            <div>
                                <div class="flex justify-between text-xs mb-1">
                                    <span class="font-medium text-slate-700">Proteínas (g / 1000 kcal)</span>
                                    <span class="font-bold text-slate-800" id="recipeProteinRatio">0 / 0 g</span>
                                </div>
                                <div class="w-full bg-slate-200 rounded-full h-2">
                                    <div id="proteinProgressBar" class="bg-indigo-600 h-2 rounded-full transition-all duration-300" style="width: 0%"></div>
                                </div>
                            </div>

                            <!-- Grasa -->
                            <div>
                                <div class="flex justify-between text-xs mb-1">
                                    <span class="font-medium text-slate-700">Grasas (g / 1000 kcal)</span>
                                    <span class="font-bold text-slate-800" id="recipeFatRatio">0 / 0 g</span>
                                </div>
                                <div class="w-full bg-slate-200 rounded-full h-2">
                                    <div id="fatProgressBar" class="bg-amber-500 h-2 rounded-full transition-all duration-300" style="width: 0%"></div>
                                </div>
                            </div>

                            <!-- Calcio -->
                            <div>
                                <div class="flex justify-between text-xs mb-1">
                                    <span class="font-medium text-slate-700">Calcio (g / 1000 kcal)</span>
                                    <span class="font-bold text-slate-800" id="recipeCalciumRatio">0 / 0 g</span>
                                </div>
                                <div class="w-full bg-slate-200 rounded-full h-2">
                                    <div id="calciumProgressBar" class="bg-sky-500 h-2 rounded-full transition-all duration-300" style="width: 0%"></div>
                                </div>
                            </div>

                            <!-- Fósforo -->
                            <div>
                                <div class="flex justify-between text-xs mb-1">
                                    <span class="font-medium text-slate-700">Fósforo (g / 1000 kcal)</span>
                                    <span class="font-bold text-slate-800" id="recipePhosphorusRatio">0 / 0 g</span>
                                </div>
                                <div class="w-full bg-slate-200 rounded-full h-2">
                                    <div id="phosphorusProgressBar" class="bg-purple-500 h-2 rounded-full transition-all duration-300" style="width: 0%"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Bloque de Consulta y Auditoría de la Receta con Gemini IA -->
                <div class="bg-slate-900 text-slate-100 rounded-2xl shadow-lg border border-slate-800 p-6 relative overflow-hidden">
                    <!-- Decoración brillante en fondo -->
                    <div class="absolute -right-16 -bottom-16 w-44 h-44 bg-teal-500/10 rounded-full blur-2xl"></div>

                    <div class="flex flex-col sm:flex-row justify-between sm:items-center border-b border-slate-800 pb-4 mb-4 gap-2">
                        <div>
                            <h3 class="text-base font-bold text-white flex items-center gap-2">
                                <i class="fa-solid fa-microchip-ai text-teal-400"></i>
                                Auditor Nutricional - Asistente IA Veterinaria
                            </h3>
                            <p class="text-xs text-slate-400">Envía la receta calculada al modelo Gemini para una auditoría experta y sugerencias de corrección.</p>
                        </div>
                        <button type="button" onclick="consultGeminiNutri()" class="bg-teal-500 hover:bg-teal-400 text-slate-950 font-bold py-2 px-4 rounded-xl text-xs transition shadow-md flex items-center justify-center gap-1.5 self-start">
                            <i class="fa-solid fa-stethoscope"></i> Analizar Receta con IA
                        </button>
                    </div>

                    <!-- Cuadro de Respuesta IA -->
                    <div class="bg-slate-950/80 rounded-xl p-4 border border-slate-800 min-h-[140px] flex flex-col justify-between">
                        <div id="aiResponseContainer" class="text-xs text-slate-300 leading-relaxed space-y-2 whitespace-pre-wrap">
                            Haz clic en el botón "Analizar Receta con IA" para que Gemini procese la composición energética, evalúe la relación Ca:P de tu ración, e identifique posibles suplementaciones necesarias basadas en las pautas oficiales de FEDIAF/NRC.
                        </div>
                        
                        <div class="flex justify-between items-center mt-4 pt-3 border-t border-slate-800/60 text-[10px] text-slate-500">
                            <span>Impulsado por Gemini Pro Veterinario</span>
                            <span>Sin cargo adicional</span>
                        </div>
                    </div>
                </div>

            </section>
        </div>
    </main>

    <!-- Pie de página -->
    <footer class="bg-slate-900 text-slate-400 border-t border-slate-800 py-6 mt-12">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs space-y-2">
            <p><strong>Disclaimer Clínico:</strong> Esta herramienta sirve para asistir en la formulación de raciones pero no reemplaza el criterio médico-veterinario de un especialista diplomado. Valide siempre sus raciones.</p>
            <p>&copy; 2026 VetNutri Pro. Fórmulas de DER/MER basadas en NRC (2006) y FEDIAF Guidelines. Ingredientes compilados de Tablas Brasileñas (Rostagno et al.) y Base de Datos ICBF Colombia.</p>
        </div>
    </footer>

    <script>
        // BASE DE DATOS DE INGREDIENTES COMBINADA: Tablas Brasileñas y Tablas de Composición de Alimentos ICBF (Colombia)
        // Valores definidos en base húmeda (por cada 100 gramos de alimento fresco/cocido)
        const ingredientDatabase = [
            // Carnes, Aves, Pescados y Vísceras (ICBF / Brasileñas)
            { id: "pechuga_pollo_icbf", name: "[ICBF] Pechuga de pollo cocida (sin piel)", source: "ICBF", energy: 151, protein: 28.1, fat: 3.6, calcium: 15, phosphorus: 228, moisture: 67.2 },
            { id: "muslo_pollo_icbf", name: "[ICBF] Carne de muslo de pollo cocido", source: "ICBF", energy: 185, protein: 24.3, fat: 9.1, calcium: 14, phosphorus: 195, moisture: 65.5 },
            { id: "carne_res_magra_icbf", name: "[ICBF] Pulpa de res cocida (baja grasa)", source: "ICBF", energy: 201, protein: 26.5, fat: 9.8, calcium: 12, phosphorus: 210, moisture: 62.1 },
            { id: "higado_pollo_icbf", name: "[ICBF] Hígado de pollo cocido", source: "ICBF", energy: 139, protein: 21.8, fat: 4.8, calcium: 15, phosphorus: 240, moisture: 71.4 },
            { id: "higado_res_brasileña", name: "[Brasileña] Hígado de res cocido", source: "Tablas Brasileñas", energy: 165, protein: 24.5, fat: 5.3, calcium: 10, phosphorus: 340, moisture: 68.0 },
            { id: "huevo_entero_icbf", name: "[ICBF] Huevo de gallina entero cocido", source: "ICBF", energy: 155, protein: 12.6, fat: 10.6, calcium: 50, phosphorus: 178, moisture: 75.1 },
            { id: "filete_merluza_icbf", name: "[ICBF] Filete de merluza cocido", source: "ICBF", energy: 87, protein: 18.2, fat: 1.1, calcium: 28, phosphorus: 190, moisture: 79.5 },
            { id: "lomo_cerdo_icbf", name: "[ICBF] Lomo de cerdo cocido", source: "ICBF", energy: 198, protein: 28.5, fat: 8.6, calcium: 10, phosphorus: 220, moisture: 61.8 },
            
            // Fuentes de Carbohidratos (ICBF / Brasileñas)
            { id: "arroz_blanco_icbf", name: "[ICBF] Arroz blanco pulido cocido", source: "ICBF", energy: 130, protein: 2.7, fat: 0.3, calcium: 10, phosphorus: 43, moisture: 68.2 },
            { id: "camote_cocido_icbf", name: "[ICBF] Camote o batata dulce cocida", source: "ICBF", energy: 102, protein: 1.6, fat: 0.2, calcium: 30, phosphorus: 49, moisture: 74.5 },
            { id: "avena_cocida_icbf", name: "[ICBF] Avena en hojuelas cocida", source: "ICBF", energy: 62, protein: 2.3, fat: 1.0, calcium: 15, phosphorus: 52, moisture: 84.1 },
            { id: "papa_cocida_icbf", name: "[ICBF] Papa blanca común cocida sin piel", source: "ICBF", energy: 86, protein: 1.7, fat: 0.1, calcium: 8, phosphorus: 44, moisture: 79.8 },

            // Vegetales, Verduras y Frutas (ICBF / Brasileñas)
            { id: "calabaza_ahuyama_icbf", name: "[ICBF] Ahuyama / Calabaza cocida", source: "ICBF", energy: 26, protein: 1.0, fat: 0.1, calcium: 21, phosphorus: 44, moisture: 91.5 },
            { id: "zanahoria_icbf", name: "[ICBF] Zanahoria fresca hervida", source: "ICBF", energy: 35, protein: 0.8, fat: 0.2, calcium: 33, phosphorus: 35, moisture: 89.2 },
            { id: "espinaca_icbf", name: "[ICBF] Espinacas hervidas", source: "ICBF", energy: 23, protein: 3.0, fat: 0.3, calcium: 99, phosphorus: 49, moisture: 91.2 },
            { id: "manzana_sin_semilla_icbf", name: "[ICBF] Manzana roja sin semillas", source: "ICBF", energy: 52, protein: 0.3, fat: 0.2, calcium: 6, phosphorus: 11, moisture: 85.6 },
            
            // Aceites y Suplementos Minerales (Fórmulas Brasileñas y Balanceadores)
            { id: "aceite_girasol_icbf", name: "[ICBF] Aceite de Girasol (ácido linoleico)", source: "ICBF", energy: 884, protein: 0, fat: 100.0, calcium: 0, phosphorus: 0, moisture: 0.1 },
            { id: "aceite_salmón_brasileña", name: "[Brasileña] Aceite de Salmón (Omega 3 DHA/EPA)", source: "Tablas Brasileñas", energy: 900, protein: 0, fat: 100.0, calcium: 0, phosphorus: 0, moisture: 0.1 },
            { id: "carbonato_calcio_brasileña", name: "[Suplemento] Carbonato de Calcio puro", source: "Tablas Brasileñas", energy: 0, protein: 0, fat: 0, calcium: 40000, phosphorus: 0, moisture: 0.5 },
            { id: "fosfato_dicalcico_brasileña", name: "[Suplemento] Fosfato dicálcico", source: "Tablas Brasileñas", energy: 0, protein: 0, fat: 0, calcium: 24000, phosphorus: 18000, moisture: 0.5 },
            { id: "yogur_entero_icbf", name: "[ICBF] Yogur entero natural sin azúcar", source: "ICBF", energy: 61, protein: 3.5, fat: 3.2, calcium: 120, phosphorus: 95, moisture: 87.9 }
        ];

        // Definiciones de factores de energía según la condición fisiológica (FEDIAF/NRC)
        // Perros: RER = 70 * Peso^0.75. DER = RER * factor
        const dogPhysiologicalStates = [
            { id: "dog_adult_neutered", name: "Adulto Castrado / Sedentario", factor: 1.4, desc: "Fórmula FEDIAF: 95 * Peso^0.75 (Adulto castrado con actividad normal a baja)" },
            { id: "dog_adult_intact", name: "Adulto Entero / Activo Ligero", factor: 1.6, desc: "Fórmula FEDIAF: 110 * Peso^0.75 (Adulto entero o activo moderado)" },
            { id: "dog_active", name: "Activo / Perro de Trabajo", factor: 2.0, desc: "Fórmula NRC/FEDIAF: 140 * Peso^0.75 (Trabajo, deporte o alta actividad)" },
            { id: "dog_obese", name: "Propenso a la Obesidad / Pérdida Peso", factor: 1.0, desc: "Fórmula FEDIAF de reducción: 70 * Peso^0.75 (Mantener balance calórico controlado)" },
            { id: "dog_senior", name: "Geriátrico / Senior", factor: 1.2, desc: "Fórmula NRC: 85 * Peso^0.75 (Menor demanda metabólica por edad)" },
            { id: "dog_puppy_early", name: "Cachorro Lactante o Crecimiento Temprano (<50% peso)", factor: 3.0, desc: "Fórmula NRC/FEDIAF: 3.0 * RER (Crecimiento intenso inicial)" },
            { id: "dog_puppy_late", name: "Cachorro en Crecimiento Tardío (50-80% peso)", factor: 2.5, desc: "Fórmula NRC: 2.5 * RER (Crecimiento sostenido de talla mediana/grande)" },
            { id: "dog_gestation", name: "Gestación (Último tercio)", factor: 2.0, desc: "Fórmula FEDIAF: 130 * Peso^0.75 aprox. (Mayor requerimiento energético por fetos)" },
            { id: "dog_lactation", name: "Lactancia Activa (Lactando camada promedio)", factor: 4.0, desc: "Fórmula NRC: Hasta 4.0 a 6.0 * RER dependiendo del número de cachorros" }
        ];

        // Gatos: RER = 70 * Peso^0.75 (Estándar clínico). DER = RER * factor
        const catPhysiologicalStates = [
            { id: "cat_adult_neutered", name: "Adulto Castrado / Interior", factor: 1.2, desc: "Recomendado FEDIAF para gatos de casa con baja actividad" },
            { id: "cat_adult_intact", name: "Adulto Entero / Activo", factor: 1.4, desc: "Requerimiento estándar para gatos libres o activos enteros" },
            { id: "cat_obese", name: "Obeso Prone / Pérdida de Peso", factor: 0.8, desc: "Restricción controlada recomendada por la NRC" },
            { id: "cat_senior", name: "Geriátrico / Senior", factor: 1.1, desc: "Gatos mayores con tasa metabólica moderadamente reducida" },
            { id: "cat_kitten_growth", name: "Gatito en Crecimiento (Kitten)", factor: 2.5, desc: "Fórmula de crecimiento rápido sugerido por la NRC" },
            { id: "cat_gestation", name: "Gestación Felina", factor: 1.6, desc: "Gestación del felino doméstico (Ganancia de peso lineal)" },
            { id: "cat_lactation", name: "Lactancia Felina", factor: 3.0, desc: "Gata lactante con alta demanda energética por producción láctea" }
        ];

        // Variables de Estado de la Aplicación
        let currentRecipe = []; // Almacena los ingredientes en la fórmula actual: { ingredientId, grams }

        window.onload = function() {
            // Cargar selector de ingredientes
            populateIngredientSelector();
            // Cargar condiciones fisiológicas por defecto (perros)
            updatePhysiologicalStates();
            // Calcular requerimientos iniciales
            calculateEnergyRequirement();

            // Vincular re-cálculo automático ante cambios del perfil
            document.getElementById('petWeight').addEventListener('input', calculateEnergyRequirement);
            document.getElementById('petSpecies').addEventListener('change', calculateEnergyRequirement);
            document.getElementById('energyStandard').addEventListener('change', calculateEnergyRequirement);
        };

        function populateIngredientSelector() {
            const selector = document.getElementById('ingredientSelector');
            selector.innerHTML = '';
            
            // Ordenar alfabéticamente
            const sortedIngredients = [...ingredientDatabase].sort((a, b) => a.name.localeCompare(b.name));
            
            // Añadir placeholder inicial
            const defaultOpt = document.createElement('option');
            defaultOpt.value = "";
            defaultOpt.textContent = "-- Seleccione un ingrediente para agregar --";
            selector.appendChild(defaultOpt);

            sortedIngredients.forEach(ing => {
                const opt = document.createElement('option');
                opt.value = ing.id;
                opt.textContent = `${ing.name} (Humedad: ${ing.moisture}%)`;
                selector.appendChild(opt);
            });
        }

        function updatePhysiologicalStates() {
            const species = document.getElementById('petSpecies').value;
            const stateSelector = document.getElementById('physiologicalState');
            stateSelector.innerHTML = '';

            const states = (species === "perro") ? dogPhysiologicalStates : catPhysiologicalStates;

            states.forEach(state => {
                const opt = document.createElement('option');
                opt.value = state.id;
                opt.textContent = state.name;
                stateSelector.appendChild(opt);
            });

            // Forzar disparo de cálculo
            calculateEnergyRequirement();
        }

        function calculateEnergyRequirement() {
            const weight = parseFloat(document.getElementById('petWeight').value);
            const species = document.getElementById('petSpecies').value;
            const standard = document.getElementById('energyStandard').value;
            const stateId = document.getElementById('physiologicalState').value;

            if (isNaN(weight) || weight <= 0) {
                return;
            }

            // 1. Calcular RER (Resting Energy Requirement)
            // Fórmula universal clínica de la NRC y FEDIAF para mamíferos domésticos: 70 * Weight^0.75
            const rer = 70 * Math.pow(weight, 0.75);
            document.getElementById('rerVal').innerHTML = `${Math.round(rer)} <span class="text-xs font-normal text-slate-500">kcal</span>`;

            // 2. Obtener el factor multiplicativo del estado fisiológico seleccionado
            const states = (species === "perro") ? dogPhysiologicalStates : catPhysiologicalStates;
            const selectedState = states.find(s => s.id === stateId);
            if (!selectedState) return;

            document.getElementById('stateDescription').textContent = selectedState.desc;

            // 3. Calcular DER (Daily Energy Requirement)
            let der = rer * selectedState.factor;
            document.getElementById('derVal').innerHTML = `${Math.round(der)} <span class="text-xs font-normal text-slate-500">kcal</span>`;
            document.getElementById('derFormulaUsed').textContent = `Fórmula: ${selectedState.factor} × RER (según guía ${standard.toUpperCase()})`;

            // 4. Calcular Requerimientos de Nutrientes Clave (por cada 1000 kcal ME)
            // Según la FEDIAF Guideline y NRC, para adultos sanos vs cachorros/crecimiento:
            let isGrowthOrRepro = stateId.includes("puppy") || stateId.includes("kitten") || stateId.includes("gestation") || stateId.includes("lactation");
            
            let reqs = {
                protein: 0,
                fat: 0,
                calcium: 0,
                phosphorus: 0
            };

            if (species === "perro") {
                if (isGrowthOrRepro) {
                    // Crecimiento y Reproducción canina
                    reqs.protein = 56.3; // g / 1000 kcal
                    reqs.fat = 21.3;     // g / 1000 kcal
                    reqs.calcium = 2.5;   // g / 1000 kcal
                    reqs.phosphorus = 2.0; // g / 1000 kcal
                } else {
                    // Mantenimiento de perro adulto
                    reqs.protein = 45.0; // g / 1000 kcal
                    reqs.fat = 13.8;     // g / 1000 kcal
                    reqs.calcium = 1.25;  // g / 1000 kcal
                    reqs.phosphorus = 1.0; // g / 1000 kcal
                }
            } else {
                // Especie: Gato
                if (isGrowthOrRepro) {
                    // Crecimiento y Reproducción felina
                    reqs.protein = 70.0;
                    reqs.fat = 22.5;
                    reqs.calcium = 2.5;
                    reqs.phosphorus = 2.0;
                } else {
                    // Mantenimiento de gato adulto (altamente proteicos y grasos)
                    reqs.protein = 62.5;
                    reqs.fat = 22.5;
                    reqs.calcium = 1.48;
                    reqs.phosphorus = 1.25;
                }
            }

            // Renderizar los objetivos mínimos calculados
            document.getElementById('reqProtein').textContent = `${reqs.protein.toFixed(1)} g`;
            document.getElementById('reqFat').textContent = `${reqs.fat.toFixed(1)} g`;
            document.getElementById('reqCalcium').textContent = `${reqs.calcium.toFixed(2)} g`;
            document.getElementById('reqPhosphorus').textContent = `${reqs.phosphorus.toFixed(2)} g`;

            // Guardar en data temporal para comparaciones
            window.targetRequirements = reqs;
            window.targetDER = der;

            // Actualizar la vista del diagnóstico nutricional inmediatamente
            updateRecipeAnalysis();
        }

        function addSelectedIngredient() {
            const selector = document.getElementById('ingredientSelector');
            const amountInput = document.getElementById('ingredientAmount');

            const ingredientId = selector.value;
            const grams = parseFloat(amountInput.value);

            if (!ingredientId) {
                showToast("Por favor selecciona un ingrediente de la base de datos.");
                return;
            }
            if (isNaN(grams) || grams <= 0) {
                showToast("Ingresa una cantidad válida de gramos.");
                return;
            }

            const baseIngredient = ingredientDatabase.find(ing => ing.id === ingredientId);
            if (!baseIngredient) return;

            // Verificar si ya existe en la receta para sumarle la porción
            const existingIndex = currentRecipe.findIndex(item => item.ingredientId === ingredientId);
            
            if (existingIndex >= 0) {
                currentRecipe[existingIndex].grams += grams;
            } else {
                currentRecipe.push({
                    ingredientId: ingredientId,
                    grams: grams
                });
            }

            // Limpiar inputs
            amountInput.value = '';
            selector.value = '';

            // Actualizar interfaz
            renderRecipeTable();
            updateRecipeAnalysis();
        }

        function removeIngredient(id) {
            currentRecipe = currentRecipe.filter(item => item.ingredientId !== id);
            renderRecipeTable();
            updateRecipeAnalysis();
        }

        function updateIngredientGrams(id, newGrams) {
            const index = currentRecipe.findIndex(item => item.ingredientId === id);
            if (index >= 0 && newGrams > 0) {
                currentRecipe[index].grams = parseFloat(newGrams);
                updateRecipeAnalysis();
            }
        }

        function resetFormulator() {
            currentRecipe = [];
            document.getElementById('recipeExplanationPanel').classList.add('hidden');
            renderRecipeTable();
            updateRecipeAnalysis();
        }

        function renderRecipeTable() {
            const tbody = document.getElementById('recipeTableBody');
            const emptyMsg = document.getElementById('emptyTableMessage');

            // Limpiar filas creadas dinámicamente
            const rows = tbody.querySelectorAll('.recipe-row');
            rows.forEach(r => r.remove());

            if (currentRecipe.length === 0) {
                emptyMsg.classList.remove('hidden');
                return;
            }

            emptyMsg.classList.add('hidden');

            currentRecipe.forEach(item => {
                const ing = ingredientDatabase.find(i => i.id === item.ingredientId);
                const row = document.createElement('tr');
                row.className = "recipe-row hover:bg-slate-50 transition border-b border-slate-100";

                // Cálculos específicos para el gramaje aportado (valores nutricionales están por 100g)
                const factor = item.grams / 100;
                const kcalAportados = Math.round(ing.energy * factor);
                const protAportada = (ing.protein * factor).toFixed(1);
                const fatAportada = (ing.fat * factor).toFixed(1);

                row.innerHTML = `
                    <td class="py-3 font-semibold text-slate-800">${ing.name}</td>
                    <td class="py-3 text-center"><span class="text-xs bg-slate-100 px-2 py-0.5 rounded text-slate-600 font-medium">${ing.source}</span></td>
                    <td class="py-3 text-right">
                        <input type="number" value="${item.grams}" min="1" onchange="updateIngredientGrams('${item.ingredientId}', this.value)" class="w-16 text-right border rounded px-1 py-0.5 focus:ring-1 focus:ring-teal-500">
                    </td>
                    <td class="py-3 text-right font-medium text-slate-900">${kcalAportados} kcal</td>
                    <td class="py-3 text-right text-slate-600">${protAportada}g</td>
                    <td class="py-3 text-right text-slate-600">${fatAportada}g</td>
                    <td class="py-3 text-center">
                        <button onclick="removeIngredient('${item.ingredientId}')" class="text-rose-500 hover:text-rose-700 p-1">
                            <i class="fa-solid fa-circle-minus"></i>
                        </button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function updateRecipeAnalysis() {
            let totalGrams = 0;
            let totalKcal = 0;
            let totalProtein = 0; // g
            let totalFat = 0;     // g
            let totalCalcium = 0; // mg
            let totalPhosphorus = 0; // mg

            currentRecipe.forEach(item => {
                const ing = ingredientDatabase.find(i => i.id === item.ingredientId);
                if (!ing) return;
                const factor = item.grams / 100;

                totalGrams += item.grams;
                totalKcal += ing.energy * factor;
                totalProtein += ing.protein * factor;
                totalFat += ing.fat * factor;
                totalCalcium += ing.calcium * factor;
                totalPhosphorus += ing.phosphorus * factor;
            });

            // Renderizar totales de cabecera
            document.getElementById('recipeTotalGrams').textContent = `${Math.round(totalGrams)}g formulados`;
            document.getElementById('recipeTotalCalories').textContent = Math.round(totalKcal);

            const targetDER = window.targetDER || 1;
            const energyPercent = Math.min((totalKcal / targetDER) * 100, 100);
            document.getElementById('energyProgressBar').style.width = `${energyPercent}%`;
            document.getElementById('energyRatioLabel').textContent = `${Math.round(totalKcal)} / ${Math.round(targetDER)} kcal`;

            // Calcular relación Ca:P (Calcio mg vs Fósforo mg)
            document.getElementById('totalCalcium').textContent = `${Math.round(totalCalcium)} mg`;
            document.getElementById('totalPhosphorus').textContent = `${Math.round(totalPhosphorus)} mg`;

            const caPBadge = document.getElementById('caPRatioBadge');
            if (totalPhosphorus > 0) {
                const ratio = totalCalcium / totalPhosphorus;
                caPBadge.textContent = `Ca:P ${ratio.toFixed(2)} : 1`;
                if (ratio >= 1.1 && ratio <= 1.8) {
                    caPBadge.className = "text-xs font-bold text-emerald-800 bg-emerald-100 px-2 py-0.5 rounded-full";
                } else {
                    caPBadge.className = "text-xs font-bold text-rose-800 bg-rose-100 px-2 py-0.5 rounded-full";
                }
            } else {
                caPBadge.textContent = "Ca:P N/A";
                caPBadge.className = "text-xs font-bold text-slate-500 bg-slate-100 px-2 py-0.5 rounded-full";
            }

            // Normalización para los requerimientos en base a 1000 kcal ME
            // Esto permite verificar si el alimento es nutritivamente completo sin importar cuánta cantidad coma
            const targets = window.targetRequirements;
            if (!targets) return;

            const calcNormalizationFactor = totalKcal > 0 ? (1000 / totalKcal) : 0;
            const normalizedProtein = totalProtein * calcNormalizationFactor;
            const normalizedFat = totalFat * calcNormalizationFactor;
            // Ojo: Calcio y fósforo en el formulador están en mg, la recomendación de NRC/FEDIAF está expresada en g (1g = 1000mg)
            const normalizedCalcium = (totalCalcium / 1000) * calcNormalizationFactor;
            const normalizedPhosphorus = (totalPhosphorus / 1000) * calcNormalizationFactor;

            // Actualizar barras de progreso de nutrientes por 1000 kcal
            updateNutrientBar('proteinProgressBar', 'recipeProteinRatio', normalizedProtein, targets.protein, 'g');
            updateNutrientBar('fatProgressBar', 'recipeFatRatio', normalizedFat, targets.fat, 'g');
            updateNutrientBar('calciumProgressBar', 'recipeCalciumRatio', normalizedCalcium, targets.calcium, 'g');
            updateNutrientBar('phosphorusProgressBar', 'recipePhosphorusRatio', normalizedPhosphorus, targets.phosphorus, 'g');
        }

        function updateNutrientBar(barId, labelId, current, target, unit) {
            const bar = document.getElementById(barId);
            const label = document.getElementById(labelId);
            
            label.textContent = `${current.toFixed(1)} / ${target.toFixed(1)} ${unit}`;
            
            const percent = Math.min((current / target) * 100, 100);
            bar.style.width = `${percent}%`;

            // Si está muy bajo (ej. < 80%), poner en rojo/amarillo
            if (percent < 80) {
                bar.className = "bg-rose-500 h-2 rounded-full transition-all duration-300";
            } else if (percent >= 80 && percent < 100) {
                bar.className = "bg-amber-500 h-2 rounded-full transition-all duration-300";
            } else {
                bar.className = "bg-emerald-600 h-2 rounded-full transition-all duration-300";
            }
        }

        function showToast(msg) {
            const toast = document.createElement('div');
            toast.className = "fixed bottom-5 right-5 bg-slate-900 text-white px-4 py-3 rounded-xl shadow-2xl text-xs font-semibold flex items-center gap-2 z-50 animate-bounce";
            toast.innerHTML = `<i class="fa-solid fa-circle-info text-teal-400"></i> ${msg}`;
            document.body.appendChild(toast);
            setTimeout(() => toast.remove(), 4000);
        }

        function hideExplanationPanel() {
            document.getElementById('recipeExplanationPanel').classList.add('hidden');
        }

        // FUNCIÓN NUEVA: Sugerir Receta Balanceada con Gemini IA
        async function suggestRecipeWithAI() {
            const loader = document.getElementById('aiSuggestionLoader');
            const explanationPanel = document.getElementById('recipeExplanationPanel');
            const explanationText = document.getElementById('recipeExplanationText');
            
            // Mostrar animador de carga
            loader.classList.remove('hidden');
            explanationPanel.classList.add('hidden');

            const species = document.getElementById('petSpecies').value;
            const weight = parseFloat(document.getElementById('petWeight').value);
            const stateId = document.getElementById('physiologicalState').value;
            const stateText = document.getElementById('physiologicalState').options[document.getElementById('physiologicalState').selectedIndex].text;
            const targetDER = window.targetDER || 400; // Meta calórica

            const targets = window.targetRequirements || { protein: 45, fat: 13, calcium: 1.25, phosphorus: 1 };

            // Pasar la base de datos de ingredientes disponible para que Gemini la use estrictamente
            const availableIngredientsStr = ingredientDatabase.map(ing => 
                `ID: "${ing.id}", Nombre: "${ing.name}", Energía por 100g: ${ing.energy} kcal, Proteína por 100g: ${ing.protein}g, Grasa por 100g: ${ing.fat}g, Calcio por 100g: ${ing.calcium}mg, Fósforo por 100g: ${ing.phosphorus}mg`
            ).join('\n');

            const systemPrompt = `Eres un algoritmo y asistente veterinario especializado en nutrición de precisión para caninos y felinos. Tu meta es formular una dieta óptima usando la base de datos de alimentos proporcionada.`;
            
            const prompt = `
            Elige ingredientes y calcula la cantidad exacta en gramos para estructurar una ración diaria balanceada para un paciente:
            - Especie: ${species}
            - Peso: ${weight} kg
            - Condición Fisiológica: ${stateText}
            - Energía Diaria Meta (DER): ${Math.round(targetDER)} kcal. El total de calorías de los ingredientes propuestos debe estar entre el 95% y el 105% de este valor (${Math.round(targetDER)} kcal).
            - Requerimientos mínimos por cada 1000 kcal de receta final:
                * Proteínas: ${targets.protein}g
                * Grasas: ${targets.fat}g
                * Calcio: ${targets.calcium}g (Equivale a ${targets.calcium * 1000}mg)
                * Fósforo: ${targets.phosphorus}g (Equivale a ${targets.phosphorus * 1000}mg)
            
            REGLAS IMPORTANTES DE EQUILIBRIO:
            1. Relación Calcio:Fósforo (Ca:P): Debe ser balanceada, idealmente entre 1.1:1 y 1.7:1. Usa obligatoriamente suplementos minerales disponibles si la carne u otros aportan demasiado fósforo sin calcio (por ejemplo "carbonato_calcio_brasileña" o "fosfato_dicalcico_brasileña").
            2. Usa porciones lógicas (por ejemplo, carnes principales entre 50g-300g, carbohidratos de 30g-200g, verduras en menor medida, aceites en pequeñas porciones de 2g a 15g, y suplementos minerales en porciones muy finas de 0.5g a 4g para no sobredosificar).
            3. No inventes ingredientes. Usa exclusivamente los IDs del listado de abajo.

            LISTADO DE INGREDIENTES DISPONIBLES EN BASE DE DATOS:
            ${availableIngredientsStr}

            Devuelve el resultado en formato JSON estructurado que cumpla con este esquema exacto:
            {
                "recipe": [
                    { "ingredientId": "id_del_ingrediente_1", "grams": cantidad_en_gramos_numero },
                    { "ingredientId": "id_del_ingrediente_2", "grams": cantidad_en_gramos_numero }
                ],
                "explicacion": "Una explicación clínica breve en español, explicando por qué esta combinación es perfecta para un ${species} en su etapa de ${stateText}."
            }
            `;

            const apiKey = "";
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;

            const payload = {
                contents: [{ parts: [{ text: prompt }] }],
                systemInstruction: {
                    parts: [{ text: systemPrompt }]
                },
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            recipe: {
                                type: "ARRAY",
                                items: {
                                    type: "OBJECT",
                                    properties: {
                                        ingredientId: { type: "STRING" },
                                        grams: { type: "NUMBER" }
                                    },
                                    required: ["ingredientId", "grams"]
                                }
                            },
                            explicacion: { type: "STRING" }
                        },
                        required: ["recipe", "explicacion"]
                    }
                }
            };

            // Intentar fetch con backoff simple
            let retries = 3;
            let delay = 1000;

            async function performFetch() {
                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (!response.ok) {
                        if (response.status === 429 && retries > 0) {
                            retries--;
                            setTimeout(performFetch, delay);
                            delay *= 2;
                            return;
                        }
                        throw new Error(`Error HTTP: ${response.status}`);
                    }

                    const result = await response.json();
                    const jsonText = result.candidates?.[0]?.content?.parts?.[0]?.text;

                    if (jsonText) {
                        const parsedData = JSON.parse(jsonText);
                        
                        if (parsedData && parsedData.recipe && parsedData.recipe.length > 0) {
                            // Limpiar y aplicar la receta sugerida
                            currentRecipe = parsedData.recipe.map(item => ({
                                ingredientId: item.ingredientId,
                                grams: Math.round(item.grams * 10) / 10 // Redondear a 1 decimal
                            }));

                            // Filtrar por si acaso el modelo inventó IDs
                            currentRecipe = currentRecipe.filter(item => ingredientDatabase.some(ing => ing.id === item.ingredientId));

                            // Renderizar y procesar la UI
                            renderRecipeTable();
                            updateRecipeAnalysis();

                            // Mostrar cuadro explicativo
                            explanationText.textContent = parsedData.explicacion;
                            explanationPanel.classList.remove('hidden');

                            showToast("¡Receta balanceada generada con éxito!");
                        } else {
                            showToast("Hubo un error al estructurar la receta por IA.");
                        }
                    }

                } catch (error) {
                    console.error("Error al sugerir receta con Gemini:", error);
                    showToast("No se pudo obtener la sugerencia. Verifica la conexión.");
                } finally {
                    loader.classList.add('hidden');
                }
            }

            await performFetch();
        }

        // CONSULTA DE AUDITORÍA GENERAL (CONVERSACIONAL)
        async function consultGeminiNutri() {
            const aiContainer = document.getElementById('aiResponseContainer');
            
            // Validaciones iniciales
            if (currentRecipe.length === 0) {
                showToast("Agrega al menos un ingrediente a la ración para poder analizarla.");
                return;
            }

            aiContainer.innerHTML = `
                <div class="flex items-center justify-center space-x-2 py-8">
                    <i class="fa-solid fa-circle-notch animate-spin text-teal-400 text-2xl"></i>
                    <span class="text-teal-400 font-bold">Gemini está analizando la ración y cruzando datos con FEDIAF / NRC...</span>
                </div>
            `;

            // Construir metadatos de la receta para el modelo
            const species = document.getElementById('petSpecies').value;
            const weight = document.getElementById('petWeight').value;
            const standard = document.getElementById('energyStandard').value;
            const stateText = document.getElementById('physiologicalState').options[document.getElementById('physiologicalState').selectedIndex].text;
            
            const reqProtein = document.getElementById('reqProtein').textContent;
            const reqFat = document.getElementById('reqFat').textContent;
            const reqCalcium = document.getElementById('reqCalcium').textContent;
            const reqPhosphorus = document.getElementById('reqPhosphorus').textContent;

            // Compilar los ingredientes de la receta actual
            let ingredientesText = "";
            currentRecipe.forEach(item => {
                const ing = ingredientDatabase.find(i => i.id === item.ingredientId);
                if (!ing) return;
                ingredientesText += `- ${ing.name}: ${item.grams}g (Aporta: ${Math.round(ing.energy * (item.grams/100))} kcal, ${(ing.protein * (item.grams/100)).toFixed(1)}g Proteína, ${(ing.fat * (item.grams/100)).toFixed(1)}g Grasa, ${Math.round(ing.calcium * (item.grams/100))}mg Calcio, ${Math.round(ing.phosphorus * (item.grams/100))}mg Fósforo)\n`;
            });

            const prompt = `
            Actúa como un Nutricionista Veterinario Clínico certificado.
            Audita la siguiente ración natural casera propuesta para un paciente:
            
            DATOS DEL PACIENTE:
            - Especie: ${species}
            - Peso: ${weight} kg
            - Estado Fisiológico: ${stateText}
            - Guía de Referencia: ${standard.toUpperCase()}
            - Energía Diaria Meta (DER): ${document.getElementById('derVal').textContent}
            - Requerimientos Mínimos sugeridos por 1000 kcal ME:
              * Proteína Mínima: ${reqProtein}
              * Grasa Mínima: ${reqFat}
              * Calcio Mínimo: ${reqCalcium}
              * Fósforo Mínimo: ${reqPhosphorus}

            INGREDIENTES FORMULADOS EN LA RECETA:
            ${ingredientesText}

            TOTALES OBTENIDOS EN LA RECETA:
            - Calorías Totales: ${document.getElementById('recipeTotalCalories').textContent} kcal
            - Calcio Total: ${document.getElementById('totalCalcium').textContent}
            - Fósforo Total: ${document.getElementById('totalPhosphorus').textContent}
            - Relación Ca:P Obtenida: ${document.getElementById('caPRatioBadge').textContent}

            INSTRUCCIONES DE AUDITORÍA:
            1. Analiza si la energía aportada cubre adecuadamente el requerimiento energético diario (DER).
            2. Evalúa críticamente si la ración cumple con los mínimos de proteínas y grasas.
            3. Analiza detalladamente la relación Calcio:Fósforo (Ca:P). Si la relación está fuera del rango ideal (1.1:1 a 1.8:1), indica cómo corregirlo utilizando carbonato de calcio, fosfato dicálcico u otros ingredientes de la lista.
            4. Menciona qué micronutrientes cruciales (como Vitaminas del complejo B, Zinc, Cobre, Vitamina E, o Taurina en caso de gatos) podrían estar en déficit en esta combinación de ingredientes frescos de la tabla brasileña/ICBF y recomienda suplementos generales.
            5. Mantén un tono sumamente clínico, profesional y pedagógico en español, organizado en secciones claras.
            `;

            const systemPrompt = "Eres un Asistente Clínico Experto en Nutrición Veterinaria (especialidad caninos y felinos). Te riges estrictamente por los parámetros de la FEDIAF (Guía nutricional de Europa) y la NRC (Consejo Nacional de Investigación de EEUU).";

            // Endpoint del modelo asignado de Gemini
            const apiKey = ""; // Deja vacío para usar en runtime del Canvas
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;

            const payload = {
                contents: [{ parts: [{ text: prompt }] }],
                systemInstruction: {
                    parts: [{ text: systemPrompt }]
                }
            };

            // Implementar Fetch con backoff exponencial básico para tolerar saturaciones de API
            let retries = 3;
            let delay = 1000;

            async function performFetch() {
                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (!response.ok) {
                        if (response.status === 429 && retries > 0) {
                            retries--;
                            setTimeout(performFetch, delay);
                            delay *= 2; // Incrementar retardo exponencialmente
                            return;
                        }
                        throw new Error(`Error HTTP: ${response.status}`);
                    }

                    const result = await response.json();
                    const candidateText = result.candidates?.[0]?.content?.parts?.[0]?.text;

                    if (candidateText) {
                        // Procesar y mostrar la respuesta exitosamente formateada
                        aiContainer.innerHTML = formatMarkdownToHTML(candidateText);
                    } else {
                        aiContainer.innerHTML = "La respuesta del modelo no pudo ser interpretada correctamente. Por favor, reintenta.";
                    }

                } catch (error) {
                    console.error("Error al consultar Gemini:", error);
                    aiContainer.innerHTML = "Ocurrió un error al contactar al auditor nutricional de Gemini. Por favor, verifica tu conexión o vuelve a formular.";
                }
            }

            // Iniciar llamada
            await performFetch();
        }

        // Formateador simple de markdown básico para la vista de respuesta de IA
        function formatMarkdownToHTML(text) {
            let html = text
                .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>')
                .replace(/\*(.*?)\*/g, '<em>$1</em>')
                .replace(/### (.*?)\n/g, '<h4 class="text-sm font-bold text-teal-300 mt-3 mb-1 uppercase tracking-wider">$1</h4>')
                .replace(/## (.*?)\n/g, '<h3 class="text-base font-black text-white border-b border-slate-800 pb-1 mt-4 mb-2">$1</h3>')
                .replace(/- (.*?)\n/g, '<li class="ml-4 list-disc">$1</li>')
                .replace(/\n\n/g, '<p class="mb-3"></p>');
            return html;
        }
    </script>
</body>
</html>
