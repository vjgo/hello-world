<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Global Geography Quiz</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    keyframes: {
                        shake: {
                            '0%, 100%': { transform: 'translateX(0)' },
                            '25%': { transform: 'translateX(-5px)' },
                            '75%': { transform: 'translateX(5px)' }
                        }
                    },
                    animation: {
                        shake: 'shake 0.3s ease-in-out'
                    },
                    dropShadow: {
                        'all-sides': '0 0 25px rgba(0, 0, 0, 0.4)' // Custom thick shadow for the main flag
                    }
                }
            }
        }
    </script>
    <style>
        .safe-padding {
            padding-top: env(safe-area-inset-top, 24px);
            padding-bottom: env(safe-area-inset-bottom, 24px);
            padding-left: env(safe-area-inset-left, 24px);
            padding-right: env(safe-area-inset-right, 24px);
        }
        .no-scrollbar::-webkit-scrollbar {
            display: none !important;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
        img {
            image-rendering: -webkit-optimize-contrast;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen safe-padding flex flex-col antialiased">

    <header class="max-w-5xl mx-auto w-full pt-6 pb-6 px-4">
        <!-- Top row: Logo, Nav, and Compact Metrics -->
        <div class="flex flex-col lg:flex-row justify-between items-center gap-4 w-full">
            
            <!-- Logo -->
            <a href="javascript:location.reload()" class="text-xl font-black text-slate-800 tracking-tighter flex items-center gap-2 shrink-0 hover:opacity-80 transition-opacity cursor-pointer">
                <svg width="28" height="28" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <polygon points="3,7 9,4 9,17 3,20" fill="#EF4444"/>
                    <polygon points="9,4 15,7 15,20 9,17" fill="#FBBF24"/>
                    <polygon points="15,7 21,4 21,17 15,20" fill="#3B82F6"/>
                </svg>
                GeoQuiz
            </a>
            
            <!-- Navigation Tabs -->
            <nav class="flex items-center justify-center overflow-x-auto no-scrollbar w-full lg:w-auto bg-white p-1 rounded-full shadow-sm border border-slate-200 shrink-0 select-none touch-manipulation" id="region-tabs">
                <!-- Tabs injected by JS -->
            </nav>

            <!-- Compact Metrics Dashboard -->
            <div class="flex items-center justify-center gap-3 md:gap-4 bg-white px-4 py-1.5 rounded-full shadow-sm border border-slate-200 shrink-0 w-full lg:w-auto">
                <div class="flex items-center gap-1.5">
                    <span class="text-slate-400 font-semibold uppercase tracking-wider text-[10px]">Correct</span>
                    <span class="font-bold text-[#3182ce] text-base" id="metric-correct">0</span>
                </div>
                <div class="w-px h-4 bg-slate-200"></div>
                <div class="flex items-center gap-1.5">
                    <span class="text-slate-400 font-semibold uppercase tracking-wider text-[10px]">Visited</span>
                    <span class="font-bold text-[#3182ce] text-base" id="metric-visited">0</span>
                </div>
                <div class="w-px h-4 bg-slate-200"></div>
                <div class="flex items-center gap-1.5">
                    <span class="text-slate-400 font-semibold uppercase tracking-wider text-[10px]">Deck</span>
                    <span class="font-bold text-[#3182ce] text-base" id="metric-deck">0</span>
                </div>
            </div>
        </div>
    </header>

    <main class="max-w-5xl mx-auto w-full flex-grow flex flex-col items-center justify-start pb-8 px-4 relative gap-6 md:gap-8">
        
        <!-- Flag Display (Top Half) - Border removed, custom shadow applied to image -->
        <div class="w-full max-w-2xl h-[180px] sm:h-[240px] md:h-[300px] relative flex items-center justify-center p-4 md:p-8 shrink-0 mt-4 group">
            <div id="flag-loader" class="absolute inset-0 flex items-center justify-center animate-pulse">
                <span class="text-slate-400 font-medium tracking-wide text-xs md:text-sm uppercase">Loading...</span>
            </div>
            <!-- Flag image with all-sides drop shadow and smooth hover scaling -->
            <img id="flag-image" src="" alt="Country Flag" class="w-full h-full object-contain hidden drop-shadow-all-sides group-hover:scale-105 transition-all duration-300 ease-out will-change-transform">
        </div>

        <!-- 2px Horizontal Line Separator -->
        <div class="w-full max-w-[320px] sm:max-w-md mx-auto h-[2px] bg-slate-200 rounded-full shrink-0"></div>

        <!-- Options Board (Bottom Half - D-Pad Plus Layout) -->
        <div class="grid grid-cols-3 grid-rows-3 gap-2 md:gap-3 w-full max-w-[320px] sm:max-w-md mx-auto shrink-0 mb-auto">
            
            <!-- Up Option -->
            <button id="btn-up" class="col-start-2 row-start-1 w-full h-full min-h-[70px] md:min-h-[90px] bg-white rounded-2xl shadow-sm border-2 border-slate-200 p-2 flex flex-col items-center justify-center gap-1 hover:border-blue-400 hover:bg-blue-50 transition-all duration-150 focus:outline-none focus:ring-4 focus:ring-blue-100 group active:scale-95">
                <span class="name-label font-bold text-slate-700 text-xs md:text-sm leading-tight text-center break-words line-clamp-2"></span>
                <span class="prefix-label text-[9px] md:text-[10px] text-slate-400 opacity-70 font-bold tracking-widest uppercase group-hover:text-blue-500 transition-colors flex items-center gap-1">Up <kbd class="font-sans hidden sm:inline font-black border border-slate-200 rounded px-1 group-hover:border-blue-300">↑</kbd></span>
            </button>

            <!-- Left Option -->
            <button id="btn-left" class="col-start-1 row-start-2 w-full h-full min-h-[70px] md:min-h-[90px] bg-white rounded-2xl shadow-sm border-2 border-slate-200 p-2 flex flex-col items-center justify-center gap-1 hover:border-blue-400 hover:bg-blue-50 transition-all duration-150 focus:outline-none focus:ring-4 focus:ring-blue-100 group active:scale-95">
                <span class="name-label font-bold text-slate-700 text-xs md:text-sm leading-tight text-center break-words line-clamp-2"></span>
                <span class="prefix-label text-[9px] md:text-[10px] text-slate-400 opacity-70 font-bold tracking-widest uppercase group-hover:text-blue-500 transition-colors flex items-center gap-1"><kbd class="font-sans hidden sm:inline font-black border border-slate-200 rounded px-1 group-hover:border-blue-300">←</kbd> Left</span>
            </button>

            <!-- Right Option -->
            <button id="btn-right" class="col-start-3 row-start-2 w-full h-full min-h-[70px] md:min-h-[90px] bg-white rounded-2xl shadow-sm border-2 border-slate-200 p-2 flex flex-col items-center justify-center gap-1 hover:border-blue-400 hover:bg-blue-50 transition-all duration-150 focus:outline-none focus:ring-4 focus:ring-blue-100 group active:scale-95">
                <span class="name-label font-bold text-slate-700 text-xs md:text-sm leading-tight text-center break-words line-clamp-2"></span>
                <span class="prefix-label text-[9px] md:text-[10px] text-slate-400 opacity-70 font-bold tracking-widest uppercase group-hover:text-blue-500 transition-colors flex items-center gap-1">Right <kbd class="font-sans hidden sm:inline font-black border border-slate-200 rounded px-1 group-hover:border-blue-300">→</kbd></span>
            </button>

            <!-- Down Option -->
            <button id="btn-down" class="col-start-2 row-start-3 w-full h-full min-h-[70px] md:min-h-[90px] bg-white rounded-2xl shadow-sm border-2 border-slate-200 p-2 flex flex-col items-center justify-center gap-1 hover:border-blue-400 hover:bg-blue-50 transition-all duration-150 focus:outline-none focus:ring-4 focus:ring-blue-100 group active:scale-95">
                <span class="name-label font-bold text-slate-700 text-xs md:text-sm leading-tight text-center break-words line-clamp-2"></span>
                <span class="prefix-label text-[9px] md:text-[10px] text-slate-400 opacity-70 font-bold tracking-widest uppercase group-hover:text-blue-500 transition-colors flex items-center gap-1">Down <kbd class="font-sans hidden sm:inline font-black border border-slate-200 rounded px-1 group-hover:border-blue-300">↓</kbd></span>
            </button>

        </div>
    </main>

    <!-- Post-Answer Overlay / Modal -->
    <div id="result-overlay" class="fixed inset-0 z-[70] hidden items-center justify-center p-4 md:p-8">
        <!-- Animated Backdrop (Click to dismiss to next question) -->
        <div id="overlay-backdrop" class="absolute inset-0 bg-slate-900/60 backdrop-blur-md opacity-0 transition-opacity duration-150 cursor-pointer" onclick="handleBackdropClick()"></div>
        
        <!-- Modal Content (Bento Design) -->
        <div id="overlay-content" class="bg-white rounded-[2.5rem] shadow-2xl w-full max-w-6xl max-h-[95vh] overflow-y-auto transform scale-95 opacity-0 transition-all duration-150 relative z-10 flex flex-col lg:flex-row gap-6 p-6 md:p-8 no-scrollbar">

            <!-- Bento Stats -->
            <div class="flex-1 w-full lg:w-[55%] flex flex-col gap-5 pt-4 md:pt-0">
                <div class="flex items-center gap-4 flex-wrap pr-4">
                    <h2 class="text-3xl md:text-4xl font-black text-slate-800 tracking-tight" id="fs-country-name">Country Name</h2>
                    <!-- Inline flag with 3px subtle drop shadow for white flag visibility -->
                    <img id="fs-flag" src="" alt="Flag" class="h-8 md:h-10 object-contain drop-shadow-[0_0_3px_rgba(0,0,0,0.3)]">
                </div>
                
                <div class="grid grid-cols-2 sm:grid-cols-3 gap-3 md:gap-4">
                    <div class="bg-slate-50 p-3 md:p-4 rounded-2xl border border-slate-100">
                        <p class="text-[9px] md:text-[10px] text-slate-400 font-bold uppercase tracking-wider mb-1">Capital(s)</p>
                        <p class="text-sm md:text-base font-bold text-slate-700 leading-tight truncate" id="fs-capital">-</p>
                    </div>
                    <div class="bg-slate-50 p-3 md:p-4 rounded-2xl border border-slate-100">
                        <p class="text-[9px] md:text-[10px] text-slate-400 font-bold uppercase tracking-wider mb-1">Continent</p>
                        <p class="text-sm md:text-base font-bold text-slate-700 leading-tight truncate" id="fs-continent">-</p>
                    </div>
                    <div class="bg-slate-50 p-3 md:p-4 rounded-2xl border border-slate-100 col-span-2 sm:col-span-1">
                        <p class="text-[9px] md:text-[10px] text-slate-400 font-bold uppercase tracking-wider mb-1">Coastline</p>
                        <p class="text-sm md:text-base font-bold text-slate-700 leading-tight truncate" id="fs-coastline">-</p>
                    </div>

                    <div class="bg-slate-50 p-3 md:p-4 rounded-2xl border border-slate-100 col-span-2 sm:col-span-3">
                        <p class="text-[9px] md:text-[10px] text-slate-400 font-bold uppercase tracking-wider mb-1">Population</p>
                        <p class="text-sm md:text-base font-bold text-slate-700 leading-tight" id="fs-population">-</p>
                    </div>
                    
                    <div class="bg-slate-50 p-3 md:p-4 rounded-2xl border border-slate-100 col-span-2 sm:col-span-3">
                        <p class="text-[9px] md:text-[10px] text-slate-400 font-bold uppercase tracking-wider mb-1">Area</p>
                        <p class="text-sm md:text-base font-bold text-slate-700 leading-tight" id="fs-area">-</p>
                    </div>

                    <div class="bg-slate-50 p-3 md:p-4 rounded-2xl border border-slate-100 col-span-2 sm:col-span-3">
                        <p class="text-[9px] md:text-[10px] text-slate-400 font-bold uppercase tracking-wider mb-1">Language</p>
                        <p class="text-sm md:text-base font-bold text-slate-700 leading-tight" id="fs-language">-</p>
                    </div>

                    <div class="bg-slate-50 p-3 md:p-4 rounded-2xl border border-slate-100 col-span-2 sm:col-span-3">
                        <p class="text-[9px] md:text-[10px] text-slate-400 font-bold uppercase tracking-wider mb-1">Religion</p>
                        <p class="text-sm md:text-base font-bold text-slate-700 leading-tight" id="fs-religion">-</p>
                    </div>

                    <!-- Economics Row -->
                    <div class="bg-slate-50 p-3 md:p-4 rounded-2xl border border-slate-100">
                        <p class="text-[9px] md:text-[10px] text-slate-400 font-bold uppercase tracking-wider mb-1">GDP (Nominal)</p>
                        <p class="text-sm md:text-base font-bold text-slate-700 leading-tight truncate" id="fs-gdp">-</p>
                    </div>
                    <div class="bg-slate-50 p-3 md:p-4 rounded-2xl border border-slate-100">
                        <p class="text-[9px] md:text-[10px] text-slate-400 font-bold uppercase tracking-wider mb-1">GDP Per Capita</p>
                        <p class="text-sm md:text-base font-bold text-slate-700 leading-tight truncate" id="fs-gdp-pc">-</p>
                    </div>
                    <div class="bg-slate-50 p-3 md:p-4 rounded-2xl border border-slate-100 col-span-2 sm:col-span-1">
                        <p class="text-[9px] md:text-[10px] text-slate-400 font-bold uppercase tracking-wider mb-1">GDP PPP Per Capita</p>
                        <p class="text-sm md:text-base font-bold text-slate-700 leading-tight truncate" id="fs-gdp-ppp">-</p>
                    </div>
                </div>
            </div>

            <!-- Map Container -->
            <div class="w-full lg:w-[45%] shrink-0 bg-white rounded-[2rem] shadow-sm border border-slate-200 p-2.5 h-[240px] lg:h-auto min-h-[350px] relative overflow-hidden mt-2 lg:mt-0">
                <div class="absolute inset-0 bg-slate-100 animate-pulse rounded-[1.5rem] m-2.5 z-0"></div>
                <iframe id="map-iframe" class="w-full h-full border-0 rounded-[1.5rem] absolute inset-0 z-10 bg-white" title="Google Maps" loading="lazy"></iframe>
            </div>
        </div>
    </div>

    <!-- Gallery Overlay / Modal (Triggered by double click) -->
    <div id="gallery-overlay" class="fixed inset-0 z-[60] hidden items-center justify-center p-4 md:p-8">
        <!-- Animated Backdrop -->
        <div id="gallery-backdrop" class="absolute inset-0 bg-slate-900/60 backdrop-blur-md opacity-0 transition-opacity duration-150 cursor-pointer" onclick="closeGallery()"></div>
        
        <!-- Gallery Content -->
        <div id="gallery-content" class="bg-slate-50 rounded-[2.5rem] shadow-2xl w-full max-w-6xl h-[90vh] flex flex-col transform scale-95 opacity-0 transition-all duration-150 relative z-10 overflow-hidden">
            
            <!-- Header -->
            <div class="px-6 md:px-8 py-5 border-b border-slate-200 bg-white flex flex-col sm:flex-row items-center justify-between gap-4 shrink-0">
                <div class="flex items-center gap-3">
                    <h2 class="text-2xl md:text-3xl font-black text-slate-800 tracking-tight" id="gallery-title">Region Gallery</h2>
                    <span class="bg-blue-100 text-blue-700 px-2 py-0.5 rounded text-xs font-bold uppercase tracking-wider" id="gallery-count">0</span>
                </div>
                
                <!-- Controls Wrapper -->
                <div class="flex items-stretch gap-4 md:gap-6 w-full sm:w-auto justify-end">
                    <!-- Sort Controls -->
                    <div class="flex items-center bg-slate-100 rounded-xl p-1 gap-1 border border-slate-200 flex-wrap justify-center">
                        <button onclick="sortGallery('name-asc')" id="sort-name-asc" class="flex items-center gap-1 px-3 py-2 rounded-lg hover:bg-white hover:shadow-sm text-slate-500 transition-all font-bold text-xs" title="Sort A-Z">
                            A-Z <svg class="w-3 h-3" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M19 14l-7 7m0 0l-7-7m7 7V3" /></svg>
                        </button>
                        <button onclick="sortGallery('name-desc')" id="sort-name-desc" class="flex items-center gap-1 px-3 py-2 rounded-lg hover:bg-white hover:shadow-sm text-slate-500 transition-all font-bold text-xs" title="Sort Z-A">
                            Z-A <svg class="w-3 h-3" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 10l7-7m0 0l7 7m-7-7v18" /></svg>
                        </button>
                        <div class="w-px h-5 bg-slate-300 mx-1"></div>
                        <button onclick="sortGallery('pop-desc')" id="sort-pop-desc" class="flex items-center gap-1.5 px-3 py-2 rounded-lg hover:bg-white hover:shadow-sm text-slate-500 transition-all font-bold text-xs" title="Sort Population Highest to Lowest">
                            <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path><circle cx="9" cy="7" r="4"></circle><path d="M23 21v-2a4 4 0 0 0-3-3.87"></path><path d="M16 3.13a4 4 0 0 1 0 7.75"></path></svg>
                            <svg class="w-3 h-3" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M19 14l-7 7m0 0l-7-7m7 7V3" /></svg>
                        </button>
                        <button onclick="sortGallery('pop-asc')" id="sort-pop-asc" class="flex items-center gap-1.5 px-3 py-2 rounded-lg hover:bg-white hover:shadow-sm text-slate-500 transition-all font-bold text-xs" title="Sort Population Lowest to Highest">
                            <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path><circle cx="9" cy="7" r="4"></circle><path d="M23 21v-2a4 4 0 0 0-3-3.87"></path><path d="M16 3.13a4 4 0 0 1 0 7.75"></path></svg>
                            <svg class="w-3 h-3" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 10l7-7m0 0l7 7m-7-7v18" /></svg>
                        </button>
                    </div>

                    <!-- Close Gallery Button -->
                    <button onclick="closeGallery()" class="bg-red-50 hover:bg-red-100 text-red-500 border border-red-200 px-4 rounded-xl flex items-center justify-center font-black transition-colors shadow-sm text-xl min-h-[44px]" title="Close Gallery">
                        &times;
                    </button>
                </div>
            </div>

            <!-- Scrollable Grid (Added pt-6 and pb-32 to prevent any clipping at top/bottom) -->
            <div id="gallery-grid" class="flex-1 overflow-y-auto p-4 md:p-8 pt-6 pb-32 grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4 md:gap-6 relative">
                <!-- Flags will be injected here -->
            </div>
        </div>
    </div>

    <script>
        // Highly compressed 195-country dataset for maximum performance
        const rawData = [
            ["Afghanistan","af","Kabul","Asia","Asia","Pashto 50,Dari 40","Islam 99.7",652230,40218234,0,14,350,1500,33.93,67.70],
            ["Albania","al","Tirana","Europe","Europe","Albanian 98","Islam 58,Christianity 17",28748,2832439,362,18,6400,17000,41.15,20.16],
            ["Algeria","dz","Algiers","Africa","Africa","Arabic 80,Berber 20","Islam 99",2381741,44700000,998,163,3700,13000,28.03,1.65],
            ["Andorra","ad","Andorra la Vella","Europe","Europe","Catalan 38,Spanish 35,Portuguese 15","Christianity 89",468,79034,0,3,40000,53000,42.50,1.52],
            ["Angola","ao","Luanda","Africa","Africa","Portuguese 71,Umbundu 23,Kikongo 8","Christianity 93,Traditional 5",1246700,34503774,1600,74,2100,6800,-11.20,17.87],
            ["Antigua and Barbuda","ag","St. John's","Americas","North America","English 95","Christianity 93",442,98728,153,1,16000,21000,17.06,-61.79],
            ["Argentina","ar","Buenos Aires","Americas","South America","Spanish 90","Christianity 79,Unaffiliated 19",2780400,45376763,4989,632,13600,26000,-38.41,-63.61],
            ["Armenia","am","Yerevan","Asia","Asia","Armenian 97","Christianity 97",29743,2968128,0,19,6500,16000,40.06,45.03],
            ["Australia","au","Canberra","Oceania","Oceania","English 72,Mandarin 2.7","Christianity 43,Unaffiliated 38",7692024,25687041,25760,1700,62000,62000,-25.27,133.77],
            ["Austria","at","Vienna","Europe","Europe","German 88,Turkish 2","Christianity 68,Unaffiliated 22,Islam 8",83871,8932664,0,471,52000,59000,47.51,14.55],
            ["Azerbaijan","az","Baku","Asia","Asia","Azerbaijani 92,Russian 1","Islam 97",86600,10139177,713,54,5300,15000,40.14,47.57],
            ["Bahamas","bs","Nassau","Americas","North America","English 90","Christianity 95",13943,393248,3542,11,28000,34000,25.03,-77.39],
            ["Bahrain","bh","Manama","Asia","Asia","Arabic 50,English 20","Islam 70,Christianity 14,Hinduism 9",760,1701583,161,38,22000,53000,25.93,50.63],
            ["Bangladesh","bd","Dhaka","Asia","Asia","Bengali 98","Islam 91,Hinduism 8",148460,166303498,580,416,2500,6800,23.68,90.35],
            ["Barbados","bb","Bridgetown","Americas","North America","English 95","Christianity 75",430,287025,97,4,17000,18000,13.19,-59.54],
            ["Belarus","by","Minsk","Europe","Europe","Russian 70,Belarusian 23","Christianity 58,Unaffiliated 41",207600,9442862,0,68,7300,21000,53.70,27.95],
            ["Belgium","be","Brussels","Europe","Europe","Dutch 59,French 40,German 1","Christianity 60,Unaffiliated 31,Islam 5",30528,11589616,66,599,51000,58000,50.50,4.46],
            ["Belize","bz","Belmopan","Americas","North America","English 62,Spanish 56,Creole 44","Christianity 73,Unaffiliated 15",22966,397621,386,1,4900,6500,17.18,-88.49],
            ["Benin","bj","Porto-Novo","Africa","Africa","French 35,Fon 24,Yoruba 8","Christianity 48,Islam 27,Traditional 11",112622,12123200,121,17,1400,3600,9.30,2.31],
            ["Bhutan","bt","Thimphu","Asia","Asia","Dzongkha 24,Nepali 22,Tshangla 8","Buddhism 75,Hinduism 22",38394,771612,0,2,3200,12000,27.51,90.43],
            ["Bolivia","bo","Sucre,La Paz","Americas","South America","Spanish 60,Quechua 21,Aymara 14","Christianity 92",1098581,11673029,0,40,3500,9000,-16.29,-63.58],
            ["Bosnia and Herzegovina","ba","Sarajevo","Europe","Europe","Bosnian 52,Serbian 30,Croatian 14","Islam 51,Christianity 46",51197,3280815,20,20,6000,15000,43.91,17.67],
            ["Botswana","bw","Gaborone","Africa","Africa","Setswana 77,English 2","Christianity 79,Unaffiliated 15",581730,2351625,0,17,7300,18000,-22.32,24.68],
            ["Brazil","br","Brasilia","Americas","South America","Portuguese 98","Christianity 88,Unaffiliated 8",8515767,212559409,7491,2081,10400,17800,-14.23,-51.92],
            ["Brunei","bn","Bandar Seri Begawan","Asia","Asia","Malay 65,English 15,Chinese 10","Islam 80,Christianity 7,Buddhism 7",5765,437483,161,14,32000,65000,4.53,114.72],
            ["Bulgaria","bg","Sofia","Europe","Europe","Bulgarian 76,Turkish 8,Romani 4","Christianity 61,Unaffiliated 9,Islam 7",110994,6927328,354,80,12000,27000,42.73,25.48],
            ["Burkina Faso","bf","Ouagadougou","Africa","Africa","French 10,Mooré 50","Islam 63,Christianity 30,Traditional 7",274200,20903278,0,17,850,2300,12.23,-1.56],
            ["Burundi","bi","Gitega","Africa","Africa","Kirundi 97,French 10","Christianity 86,Traditional 11,Islam 2",27834,11890781,0,3,270,750,-3.37,29.91],
            ["Cabo Verde","cv","Praia","Africa","Africa","Portuguese 10,Kabuverdianu 90","Christianity 85",4033,555988,965,2,3600,7400,16.00,-24.01],
            ["Cambodia","kh","Phnom Penh","Asia","Asia","Khmer 96","Buddhism 97,Islam 2",181035,16718971,443,26,1600,4600,12.56,104.99],
            ["Cameroon","cm","Yaounde","Africa","Africa","French 80,English 20","Christianity 70,Islam 20,Traditional 9",475442,26545864,402,44,1600,3800,3.84,11.50],
            ["Canada","ca","Ottawa","Americas","North America","English 75,French 21","Christianity 53,Unaffiliated 34,Islam 5",9984670,38005238,202080,2117,53000,59000,56.13,-106.34],
            ["Central African Republic","cf","Bangui","Africa","Africa","Sango 90,French 20","Christianity 89,Islam 9",622984,4829764,0,2,490,1000,6.61,20.93],
            ["Chad","td","N'Djamena","Africa","Africa","Arabic 10,French 10,Sara 20","Islam 52,Christianity 44,Traditional 4",1284000,16425859,0,11,700,1600,15.45,18.73],
            ["Chile","cl","Santiago","Americas","South America","Spanish 99","Christianity 68,Unaffiliated 25",756102,19116209,6435,317,16000,27000,-35.67,-71.54],
            ["China","cn","Beijing","Asia","Asia","Mandarin 71,Wu 8,Min 4","Unaffiliated 52,Buddhism 18,Folk 21",9596961,1439323774,14500,17730,12500,18900,35.86,104.19],
            ["Colombia","co","Bogota","Americas","South America","Spanish 99","Christianity 92",1141748,50882884,3208,343,6700,16000,4.57,-74.29],
            ["Comoros","km","Moroni","Africa","Africa","Comorian 97,French 30,Arabic 10","Islam 98",2235,869595,340,1,1400,3200,-11.87,43.87],
            ["Congo (Brazzaville)","cg","Brazzaville","Africa","Africa","French 30,Kituba 50,Lingala 13","Christianity 88,Traditional 5,Islam 2",342000,5518092,169,13,2200,4000,-0.22,15.82],
            ["Congo (Kinshasa)","cd","Kinshasa","Africa","Africa","French 47,Lingala 30,Swahili 10","Christianity 95,Islam 1",2344858,89561404,37,58,600,1100,-4.03,21.75],
            ["Costa Rica","cr","San Jose","Americas","North America","Spanish 99","Christianity 76,Unaffiliated 19",51100,5094114,1290,68,13000,23000,9.74,-83.75],
            ["Côte d'Ivoire","ci","Yamoussoukro,Abidjan","Africa","Africa","French 30,Baoulé 15,Dioula 10","Islam 43,Christianity 40",322463,28160542,515,73,2600,6300,7.54,-5.55],
            ["Croatia","hr","Zagreb","Europe","Europe","Croatian 95","Christianity 91,Unaffiliated 6",56594,4105267,5835,71,17000,34000,45.10,15.20],
            ["Cuba","cu","Havana","Americas","North America","Spanish 100","Christianity 59,Unaffiliated 23,Folk 17",109884,11326616,3735,107,9500,12000,21.52,-77.78],
            ["Cyprus","cy","Nicosia","Europe","Europe","Greek 80,Turkish 20","Christianity 73,Islam 25",9251,1207361,648,28,29000,45000,35.12,33.42],
            ["Czechia","cz","Prague","Europe","Europe","Czech 95","Unaffiliated 78,Christianity 11",78865,10708982,0,290,27000,47000,49.81,15.47],
            ["Denmark","dk","Copenhagen","Europe","Europe","Danish 98","Christianity 74,Unaffiliated 19,Islam 5",42933,5831404,7314,398,68000,64000,56.26,9.50],
            ["Djibouti","dj","Djibouti","Africa","Africa","Somali 50,Afar 30,French 10,Arabic 10","Islam 94,Christianity 6",23200,988002,314,3,3400,5800,11.82,42.59],
            ["Dominica","dm","Roseau","Americas","North America","English 95,French Patois 80","Christianity 88",751,71991,148,0.6,8300,12000,15.41,-61.37],
            ["Dominican Republic","do","Santo Domingo","Americas","North America","Spanish 98","Christianity 69,Unaffiliated 28",48671,10847904,1288,112,10000,21000,18.73,-70.16],
            ["Ecuador","ec","Quito","Americas","South America","Spanish 93,Quechua 4","Christianity 92",283561,17643060,2237,115,6400,12000,-1.83,-78.18],
            ["Egypt","eg","Cairo","Africa","Africa","Arabic 99","Islam 90,Christianity 10",1002450,102334403,2450,398,3600,16000,26.82,30.80],
            ["El Salvador","sv","San Salvador","Americas","North America","Spanish 99","Christianity 84,Unaffiliated 15",21041,6486201,307,32,4900,10000,13.79,-88.89],
            ["Equatorial Guinea","gq","Malabo","Africa","Africa","Spanish 67,French 10,Fang 10","Christianity 88,Traditional 5",28051,1402985,296,16,11000,18000,1.65,10.26],
            ["Eritrea","er","Asmara","Africa","Africa","Tigrinya 50,Arabic 10,English 5","Christianity 63,Islam 36",117600,3546427,2234,2,640,1600,15.17,39.78],
            ["Estonia","ee","Tallinn","Europe","Europe","Estonian 68,Russian 29","Unaffiliated 60,Christianity 28",45228,1326535,3794,37,28000,43000,58.59,25.01],
            ["Eswatini","sz","Mbabane,Lobamba","Africa","Africa","Swati 95,English 20","Christianity 90,Traditional 8",17364,1160164,0,4,4000,10000,-26.52,31.46],
            ["Ethiopia","et","Addis Ababa","Africa","Africa","Oromo 33,Amharic 29,Somali 6","Christianity 67,Islam 31",1104300,114963583,0,126,1000,3200,9.14,40.48],
            ["Fiji","fj","Suva","Oceania","Oceania","English 95,Fijian 54,Hindi 37","Christianity 64,Hinduism 27,Islam 6",18274,896444,1129,5,5300,12000,-17.71,178.06],
            ["Finland","fi","Helsinki","Europe","Europe","Finnish 86,Swedish 5","Christianity 68,Unaffiliated 30",338145,5540720,1250,297,53000,55000,61.92,25.74],
            ["France","fr","Paris","Europe","Europe","French 100","Christianity 47,Unaffiliated 40,Islam 5",551695,65273512,4853,2923,44000,55000,46.22,2.21],
            ["Gabon","ga","Libreville","Africa","Africa","French 80,Fang 32","Christianity 76,Islam 11,Traditional 6",267668,2225728,885,21,9000,16000,-0.80,11.60],
            ["Gambia","gm","Banjul","Africa","Africa","English 10,Mandinka 38,Fula 21","Islam 96,Christianity 3",11300,2416664,80,2,800,2300,13.44,-15.31],
            ["Georgia","ge","Tbilisi","Asia","Asia","Georgian 87,Azerbaijani 6,Armenian 4","Christianity 88,Islam 10",69700,3989167,310,24,6600,17000,42.31,43.35],
            ["Germany","de","Berlin","Europe","Europe","German 95","Christianity 54,Unaffiliated 40,Islam 6",357022,83783945,2389,4429,52000,63000,51.16,10.45],
            ["Ghana","gh","Accra","Africa","Africa","Asante 16,Ewe 14,English 10","Christianity 71,Islam 19,Traditional 3",238533,31072945,539,72,2300,6100,7.94,-1.02],
            ["Greece","gr","Athens","Europe","Europe","Greek 99","Christianity 90,Unaffiliated 4",131957,10423054,13676,214,20000,33000,39.07,21.82],
            ["Grenada","gd","St. George's","Americas","North America","English 95","Christianity 89",344,112519,121,1,10000,15000,12.11,-61.67],
            ["Guatemala","gt","Guatemala City","Americas","North America","Spanish 69,Maya 29","Christianity 87,Unaffiliated 11",108889,17915567,400,95,5000,9500,15.78,-90.23],
            ["Guinea","gn","Conakry","Africa","Africa","French 15,Pular 33,Maninka 30","Islam 89,Christianity 6,Traditional 4",245857,13132792,320,21,1500,2900,9.94,-9.69],
            ["Guinea-Bissau","gw","Bissau","Africa","Africa","Portuguese 11,Kriol 44","Islam 46,Traditional 30,Christianity 18",36125,1967998,350,1,800,2000,11.80,-15.18],
            ["Guyana","gy","Georgetown","Americas","South America","English 95,Guyanese Creole 90","Christianity 64,Hinduism 24,Islam 6",214969,786559,459,14,18000,24000,4.86,-58.93],
            ["Haiti","ht","Port-au-Prince","Americas","North America","French 10,Haitian Creole 95","Christianity 86,Voodoo 2",27750,11402533,1771,20,1800,3100,18.97,-72.28],
            ["Honduras","hn","Tegucigalpa","Americas","North America","Spanish 98","Christianity 87,Unaffiliated 10",112492,9904608,820,31,3000,6200,15.19,-86.24],
            ["Hungary","hu","Budapest","Europe","Europe","Hungarian 99","Christianity 52,Unaffiliated 20",93028,9660351,0,178,18000,37000,47.16,19.50],
            ["Iceland","is","Reykjavik","Europe","Europe","Icelandic 97,English 90","Christianity 73,Unaffiliated 21",103000,341250,4970,27,73000,60000,64.96,-19.02],
            ["India","in","New Delhi","Asia","Asia","Hindi 43,Bengali 8,Marathi 6,English 0.5","Hinduism 79,Islam 14,Christianity 2",3287263,1380004385,7516,3549,2500,8300,20.59,78.96],
            ["Indonesia","id","Jakarta","Asia","Asia","Indonesian 94,Javanese 30","Islam 87,Protestantism 7,Catholicism 2",1904569,273523621,54716,1371,4900,15000,-0.78,113.92],
            ["Iran","ir","Tehran","Asia","Asia","Persian 53,Azerbaijani 16,Kurdish 10","Islam 99",1648195,83992953,2440,388,4600,16000,32.42,53.68],
            ["Iraq","iq","Baghdad","Asia","Asia","Arabic 79,Kurdish 21","Islam 95,Christianity 1",438317,40222503,58,264,5900,11000,33.22,43.67],
            ["Ireland","ie","Dublin","Europe","Europe","English 99,Irish 39","Christianity 78,Unaffiliated 14",70273,4937796,1448,529,106000,124000,53.41,-8.24],
            ["Israel","il","Jerusalem","Asia","Asia","Hebrew 74,Arabic 20","Judaism 73,Islam 18,Christianity 2",22072,8655541,273,522,54000,43000,31.04,34.85],
            ["Italy","it","Rome","Europe","Europe","Italian 97","Christianity 80,Unaffiliated 15,Islam 4",301340,60461828,7600,2186,37000,50000,41.87,12.56],
            ["Jamaica","jm","Kingston","Americas","North America","English 95,Patois 90","Christianity 68,Unaffiliated 21",10991,2961161,1022,17,5800,11000,18.10,-77.29],
            ["Japan","jp","Tokyo","Asia","Asia","Japanese 99","Shinto 70,Buddhism 69,Christianity 1",377975,126476461,29751,4231,33000,45000,36.20,138.25],
            ["Jordan","jo","Amman","Asia","Asia","Arabic 98","Islam 97,Christianity 2",89342,10203140,26,47,4600,11000,31.24,36.51],
            ["Kazakhstan","kz","Astana","Asia","Asia","Kazakh 65,Russian 21","Islam 70,Christianity 26",2724900,18776707,0,220,11000,28000,48.01,66.92],
            ["Kenya","ke","Nairobi","Africa","Africa","Swahili 70,English 20,Kikuyu 17","Christianity 85,Islam 11",580367,53771300,536,112,2000,5700,-0.02,37.90],
            ["Kiribati","ki","Tarawa","Oceania","Oceania","English 100,Gilbertese 95","Christianity 96",811,119446,1143,0.2,1600,2300,-3.37,-168.73],
            ["Kuwait","kw","Kuwait City","Asia","Asia","Arabic 90,English 10","Islam 74,Christianity 18,Hinduism 6",17818,4270563,499,184,38000,51000,29.31,47.48],
            ["Kyrgyzstan","kg","Bishkek","Asia","Asia","Kyrgyz 71,Russian 9,Uzbek 14","Islam 90,Christianity 7",199951,6524191,0,10,1600,5500,41.20,74.76],
            ["Laos","la","Vientiane","Asia","Asia","Lao 65,French 10","Buddhism 64,Traditional 31",236800,7275556,0,15,2000,8500,19.85,102.49],
            ["Latvia","lv","Riga","Europe","Europe","Latvian 62,Russian 37","Christianity 60,Unaffiliated 35",64589,1901548,498,41,21000,35000,56.87,24.60],
            ["Lebanon","lb","Beirut","Asia","Asia","Arabic 95,French 20","Islam 61,Christianity 33",10400,6825442,225,23,3500,7500,33.85,35.86],
            ["Lesotho","ls","Maseru","Africa","Africa","Sesotho 90,English 10","Christianity 90,Traditional 10",30355,2142252,0,2,1000,2800,-29.61,28.23],
            ["Liberia","lr","Monrovia","Africa","Africa","English 20,Kpelle 20","Christianity 85,Islam 12,Traditional 1",111369,5057677,579,4,700,1600,6.42,-9.42],
            ["Libya","ly","Tripoli","Africa","Africa","Arabic 95,Berber 5","Islam 97",1759540,6871287,1770,45,6700,15000,26.33,17.22],
            ["Liechtenstein","li","Vaduz","Europe","Europe","German 94","Christianity 80,Unaffiliated 10,Islam 5",160,38137,0,6,180000,98000,47.16,9.55],
            ["Lithuania","lt","Vilnius","Europe","Europe","Lithuanian 82,Russian 8,Polish 5","Christianity 79,Unaffiliated 15",65300,2722289,90,70,25000,42000,55.16,23.88],
            ["Luxembourg","lu","Luxembourg City","Europe","Europe","Luxembourgish 70,French 55,German 30","Christianity 69,Unaffiliated 26",2586,625978,0,82,125000,131000,49.81,6.12],
            ["Madagascar","mg","Antananarivo","Africa","Africa","Malagasy 98,French 20","Christianity 85,Traditional 10,Islam 3",587041,27691019,4828,15,500,1700,-18.76,46.86],
            ["Malawi","mw","Lilongwe","Africa","Africa","Chichewa 57,English 10,Chinyanja 12","Christianity 77,Islam 14",118484,19129955,0,13,600,1600,-13.25,34.30],
            ["Malaysia","my","Kuala Lumpur","Asia","Asia","Malay 60,English 40,Mandarin 20","Islam 61,Buddhism 19,Christianity 9",330803,32365998,4675,406,12000,31000,4.21,101.97],
            ["Maldives","mv","Malé","Asia","Asia","Dhivehi 98,English 20","Islam 100",298,540542,644,5,10000,23000,3.20,73.22],
            ["Mali","ml","Bamako","Africa","Africa","Bambara 46,French 20,Peul 9","Islam 95,Christianity 2,Traditional 2",1240192,20250834,0,19,850,2400,17.57,-3.99],
            ["Malta","mt","Valletta","Europe","Europe","Maltese 90,English 88","Christianity 88,Unaffiliated 7",316,441539,196,17,33000,49000,35.93,14.37],
            ["Marshall Islands","mh","Majuro","Oceania","Oceania","Marshallese 98,English 80","Christianity 90",181,59194,370,0.2,4000,3900,7.13,171.18],
            ["Mauritania","mr","Nouakchott","Africa","Africa","Arabic 80,French 10","Islam 99",1030700,4649660,754,10,2100,5700,21.00,-10.94],
            ["Mauritius","mu","Port Louis","Africa","Africa","Creole 86,Bhojpuri 5,French 4","Hinduism 48,Christianity 32,Islam 17",2040,1271768,177,11,8800,23000,-20.34,57.55],
            ["Mexico","mx","Mexico City","Americas","North America","Spanish 93,Nahuatl 1","Christianity 89,Unaffiliated 10",1964375,128932753,9330,1663,12000,22000,23.63,-102.55],
            ["Micronesia","fm","Palikir","Oceania","Oceania","English 90,Chuukese 45,Pohnpeian 25","Christianity 95",702,115021,6112,0.4,3500,3600,7.42,150.55],
            ["Moldova","md","Chisinau","Europe","Europe","Romanian 80,Russian 16,Ukrainian 2","Christianity 92,Unaffiliated 6",33846,2640459,0,14,5600,15000,47.41,28.36],
            ["Monaco","mc","Monaco","Europe","Europe","French 99,Italian 20,English 10","Christianity 82,Unaffiliated 15",2,39244,4,7,190000,115000,43.73,7.42],
            ["Mongolia","mn","Ulaanbaatar","Asia","Asia","Mongolian 90,Kazakh 5","Buddhism 53,Unaffiliated 38,Islam 3",1564110,3278292,0,15,4500,13000,46.86,103.84],
            ["Montenegro","me","Podgorica","Europe","Europe","Montenegrin 42,Serbian 42,Bosnian 5","Christianity 75,Islam 19,Unaffiliated 3",13812,628062,293,6,9000,22000,42.70,19.37],
            ["Morocco","ma","Rabat","Africa","Africa","Arabic 90,Berber 26,French 33","Islam 99",446550,36910558,1835,142,3900,9000,31.79,-7.09],
            ["Mozambique","mz","Maputo","Africa","Africa","Portuguese 47,Makhuwa 26,Tsonga 11","Christianity 59,Islam 18,Unaffiliated 13",801590,31255435,2470,19,600,1300,-18.66,35.52],
            ["Myanmar","mm","Naypyidaw","Asia","Asia","Burmese 68,Shan 9,Karen 7","Buddhism 87,Christianity 6,Islam 4",676578,54409794,1930,65,1200,5000,21.91,95.95],
            ["Namibia","na","Windhoek","Africa","Africa","Oshiwambo 49,Khoekhoe 11,Afrikaans 10","Christianity 90,Traditional 10",824292,2540916,1572,12,5000,10000,-22.95,18.49],
            ["Nauru","nr","Yaren","Oceania","Oceania","Nauruan 95,English 66","Christianity 95",21,10834,30,0.1,12000,11000,-0.52,166.93],
            ["Nepal","np","Kathmandu","Asia","Asia","Nepali 44,Maithili 11,Bhojpuri 6","Hinduism 81,Buddhism 9,Islam 4",147181,29136808,0,40,1300,4300,28.39,84.12],
            ["Netherlands","nl","Amsterdam","Europe","Europe","Dutch 98,Frisian 2","Unaffiliated 50,Christianity 43,Islam 5",41543,17134873,451,1013,57000,62000,52.13,5.29],
            ["New Zealand","nz","Wellington","Oceania","Oceania","English 95,Māori 4,Samoan 2","Unaffiliated 48,Christianity 37,Hinduism 2",268021,4822233,15134,247,47000,50000,-40.90,174.88],
            ["Nicaragua","ni","Managua","Americas","North America","Spanish 95,Miskito 2","Christianity 85,Unaffiliated 12",130373,6624554,910,15,2200,6000,12.86,-85.20],
            ["Niger","ne","Niamey","Africa","Africa","French 10,Hausa 53,Zarma 21","Islam 99",1267000,24206636,0,15,500,1300,17.60,8.08],
            ["Nigeria","ng","Abuja","Africa","Africa","English 60,Hausa 25,Yoruba 21","Islam 50,Christianity 48,Traditional 1",923768,206139587,853,390,1600,5800,9.08,8.67],
            ["North Korea","kp","Pyongyang","Asia","Asia","Korean 99","Unaffiliated 71,Traditional 16,Buddhism 11",120538,25778815,2495,18,700,1700,40.33,127.51],
            ["North Macedonia","mk","Skopje","Europe","Europe","Macedonian 66,Albanian 25","Christianity 65,Islam 33",25713,2083380,0,13,6700,18000,41.60,21.74],
            ["Norway","no","Oslo","Europe","Europe","Norwegian 95,Sami 1","Christianity 74,Unaffiliated 19,Islam 3",323802,5421242,25148,482,90000,68000,60.47,8.46],
            ["Oman","om","Muscat","Asia","Asia","Arabic 85,English 20","Islam 85,Christianity 6,Hinduism 5",309500,5106622,2092,88,17000,32000,21.47,55.97],
            ["Pakistan","pk","Islamabad","Asia","Asia","Punjabi 48,Sindhi 11,Saraiki 10,Urdu 8","Islam 96,Hinduism 2,Christianity 1",881912,220892331,1046,376,1600,5800,30.37,69.34],
            ["Palau","pw","Ngerulmud","Oceania","Oceania","Palauan 65,English 90","Christianity 92",459,18092,1519,0.2,13000,15000,7.51,134.58],
            ["Palestine","ps","Jerusalem,Ramallah","Asia","Asia","Arabic 95","Islam 93,Christianity 6",6020,5101416,40,18,3500,6000,31.95,35.23],
            ["Panama","pa","Panama City","Americas","North America","Spanish 93","Christianity 90,Unaffiliated 5",75417,4314768,2490,76,17000,36000,8.53,-80.78],
            ["Papua New Guinea","pg","Port Moresby","Oceania","Oceania","Tok Pisin 75,English 1,Hiri Motu 1","Christianity 95,Indigenous 3",462840,8947027,5152,31,3100,4200,-6.31,143.95],
            ["Paraguay","py","Asuncion","Americas","South America","Spanish 87,Guarani 90","Christianity 96,Unaffiliated 2",406752,7132530,0,41,5600,14000,-23.44,-58.44],
            ["Peru","pe","Lima","Americas","South America","Spanish 82,Quechua 13,Aymara 1","Christianity 94,Unaffiliated 4",1285216,32971846,2414,243,7200,13000,-9.19,-75.01],
            ["Philippines","ph","Manila","Asia","Asia","Tagalog 28,Cebuano 13,Ilocano 9,English 50","Christianity 92,Islam 5",300000,109581078,36289,404,3600,9000,12.87,121.77],
            ["Poland","pl","Warsaw","Europe","Europe","Polish 98","Christianity 87,Unaffiliated 12",312696,37846605,440,688,18000,37000,51.91,19.14],
            ["Portugal","pt","Lisbon","Europe","Europe","Portuguese 99","Christianity 84,Unaffiliated 14",92090,10196707,1793,253,24000,36000,39.39,-8.22],
            ["Qatar","qa","Doha","Asia","Asia","Arabic 60,English 80","Islam 65,Hinduism 15,Christianity 13",11586,2881060,563,220,76000,104000,25.35,51.18],
            ["Romania","ro","Bucharest","Europe","Europe","Romanian 85,Hungarian 6","Christianity 98,Unaffiliated 1",238391,19237691,225,301,15000,34000,45.94,24.96],
            ["Russia","ru","Moscow","Europe","Europe","Russian 85,Tatar 3,Chechen 1","Christianity 71,Unaffiliated 15,Islam 10",17098242,145912022,37653,2240,15000,32000,61.52,105.31],
            ["Rwanda","rw","Kigali","Africa","Africa","Kinyarwanda 93,French 5,English 5","Christianity 93,Islam 2",26338,12952209,0,13,900,2400,-1.94,29.87],
            ["Saint Kitts and Nevis","kn","Basseterre","Americas","North America","English 95","Christianity 94",261,53192,135,1,19000,28000,17.35,-62.78],
            ["Saint Lucia","lc","Castries","Americas","North America","English 95,French Creole 90","Christianity 90",616,183629,158,2,11000,16000,13.90,-60.97],
            ["Saint Vincent and the Grenadines","vc","Kingstown","Americas","North America","English 95,Vincentian Creole 90","Christianity 89,Hinduism 3",389,110947,84,0.9,8500,14000,13.25,-61.22],
            ["Samoa","ws","Apia","Oceania","Oceania","Samoan 91,English 9","Christianity 98",2842,198410,403,0.8,4100,6400,-13.75,-172.10],
            ["San Marino","sm","San Marino","Europe","Europe","Italian 98","Christianity 97,Unaffiliated 2",61,33938,0,1,50000,62000,43.94,12.45],
            ["Sao Tome and Principe","st","Sao Tome","Africa","Africa","Portuguese 98,Forro 36","Christianity 82,Unaffiliated 15",1001,219159,209,0.5,2300,4300,0.18,6.61],
            ["Saudi Arabia","sa","Riyadh","Asia","Asia","Arabic 100","Islam 93,Christianity 4",2149690,34813867,2640,1067,30000,59000,23.88,45.07],
            ["Senegal","sn","Dakar","Africa","Africa","French 20,Wolof 43,Pular 24","Islam 96,Christianity 3",196722,16743930,531,27,1500,3700,14.49,-14.45],
            ["Serbia","rs","Belgrade","Europe","Europe","Serbian 88,Hungarian 3","Christianity 92,Islam 3,Unaffiliated 3",77474,8737371,0,63,9000,20000,44.01,21.00],
            ["Seychelles","sc","Victoria","Africa","Africa","Seychellois Creole 89,English 5,French 1","Christianity 89,Hinduism 2",452,98340,491,1.5,15000,30000,-4.67,55.49],
            ["Sierra Leone","sl","Freetown","Africa","Africa","English 10,Mende 30,Temne 30","Islam 78,Christianity 21",71740,7976985,402,4,480,1800,8.46,-11.77],
            ["Singapore","sg","Singapore","Asia","Asia","English 36,Mandarin 34,Malay 10","Buddhism 31,Christianity 18,Islam 15",719,5850342,193,396,72000,116000,1.35,103.81],
            ["Slovakia","sk","Bratislava","Europe","Europe","Slovak 80,Hungarian 8,Romani 1","Christianity 73,Unaffiliated 23",49035,5459642,0,115,21000,34000,48.66,19.69],
            ["Slovenia","si","Ljubljana","Europe","Europe","Slovenian 91,Serbo-Croatian 4","Christianity 74,Unaffiliated 18",20273,2078932,46,62,29000,42000,46.15,14.99],
            ["Solomon Islands","sb","Honiara","Oceania","Oceania","Pijin 95,English 2","Christianity 96",28896,686878,5313,1.5,2300,2600,-9.64,160.15],
            ["Somalia","so","Mogadishu","Africa","Africa","Somali 95,Arabic 5","Islam 99",637657,15893219,3025,8,480,1200,5.15,46.19],
            ["South Africa","za","Pretoria,Cape Town,Bloemfontein","Africa","Africa","Zulu 24,Xhosa 16,Afrikaans 13","Christianity 86,Traditional 5,Islam 2",1221037,59308690,2798,377,6100,16100,-30.55,22.93],
            ["South Korea","kr","Seoul","Asia","Asia","Korean 99","Unaffiliated 56,Christianity 27,Buddhism 15",100210,51269185,2413,1712,34000,48000,35.90,127.76],
            ["South Sudan","ss","Juba","Africa","Africa","English 10,Dinka 35,Nuer 15","Christianity 60,Traditional 32,Islam 6",644329,11193729,0,12,1100,1300,6.87,31.30],
            ["Spain","es","Madrid","Europe","Europe","Spanish 99,Catalan 16,Galician 6","Christianity 58,Unaffiliated 37",505992,46754783,4964,1580,33000,46000,40.46,-3.74],
            ["Sri Lanka","lk","Colombo","Asia","Asia","Sinhala 74,Tamil 18","Buddhism 70,Hinduism 12,Islam 9",65610,21413249,1340,84,3800,13000,7.87,80.77],
            ["Sudan","sd","Khartoum","Africa","Africa","Arabic 80,English 10","Islam 97,Christianity 3",1886068,43849269,853,34,750,4200,12.86,30.21],
            ["Suriname","sr","Paramaribo","Americas","South America","Dutch 60,Sranan Tongo 95,Hindi 20","Christianity 48,Hinduism 22,Islam 13",163820,586634,386,3,5800,17000,3.91,-56.02],
            ["Sweden","se","Stockholm","Europe","Europe","Swedish 95,Arabic 2","Christianity 59,Unaffiliated 31,Islam 8",450295,10099270,3218,585,55000,56000,60.12,18.64],
            ["Switzerland","ch","Bern","Europe","Europe","German 62,French 22,Italian 8","Christianity 67,Unaffiliated 25,Islam 5",41284,8654622,0,807,92000,75000,46.81,8.22],
            ["Syria","sy","Damascus","Asia","Asia","Arabic 90,Kurdish 8","Islam 87,Christianity 10",185180,17500657,193,21,1200,2900,34.80,38.99],
            ["Tajikistan","tj","Dushanbe","Asia","Asia","Tajik 84,Uzbek 11,Russian 3","Islam 98",143100,9537642,0,8,850,3800,38.86,71.27],
            ["Tanzania","tz","Dodoma","Africa","Africa","Swahili 95,English 10","Christianity 61,Islam 35,Traditional 2",947300,59734213,1424,67,1100,2800,-6.36,34.88],
            ["Thailand","th","Bangkok","Asia","Asia","Thai 90","Buddhism 94,Islam 5,Christianity 1",513120,69799978,3219,536,7500,19000,15.87,100.99],
            ["Timor-Leste","tl","Dili","Asia","Oceania","Tetum 90,Portuguese 5,Indonesian 10","Christianity 99,Islam 0.3",14874,1318442,706,2,1400,3300,-8.87,125.72],
            ["Togo","tg","Lome","Africa","Africa","French 39,Ewe 32,Kabiyé 14","Christianity 48,Traditional 33,Islam 14",56785,8278737,56,9,970,2500,8.61,0.82],
            ["Tonga","to","Nuku'alofa","Oceania","Oceania","Tongan 95,English 80","Christianity 98",747,105697,419,0.5,5000,6600,-21.17,-175.20],
            ["Trinidad and Tobago","tt","Port of Spain","Americas","North America","English 98,Creole 90","Christianity 63,Hinduism 18,Islam 5",5128,1399491,362,25,17000,26000,10.69,-61.22],
            ["Tunisia","tn","Tunis","Africa","Africa","Arabic 98,French 60","Islam 99",163610,11818618,1148,46,3900,10000,33.88,9.53],
            ["Turkey","tr","Ankara","Asia","Asia","Turkish 85,Kurdish 11","Islam 99",783562,84339067,7200,815,9500,30000,38.96,35.24],
            ["Turkmenistan","tm","Ashgabat","Asia","Asia","Turkmen 72,Russian 12,Uzbek 9","Islam 93,Christianity 6",488100,6031187,0,45,7600,16000,38.96,59.55],
            ["Tuvalu","tv","Funafuti","Oceania","Oceania","Tuvaluan 95,English 80","Christianity 97",26,11792,24,0.06,5300,4300,-7.10,177.64],
            ["Uganda","ug","Kampala","Africa","Africa","English 20,Luganda 16,Swahili 10","Christianity 84,Islam 14",241038,45741000,0,37,800,2500,1.37,32.29],
            ["Ukraine","ua","Kyiv","Europe","Europe","Ukrainian 67,Russian 29","Christianity 87,Unaffiliated 11",603500,43733759,2782,155,3700,14000,48.37,31.16],
            ["United Arab Emirates","ae","Abu Dhabi","Asia","Asia","Arabic 80,English 90,Hindi 15","Islam 76,Christianity 9,Hinduism 6",83600,9890400,1318,507,51000,74000,23.42,53.84],
            ["United Kingdom","gb","London","Europe","Europe","English 98,Welsh 1","Christianity 46,Unaffiliated 37,Islam 6",242900,67886004,12429,3332,48000,54000,55.37,-3.43],
            ["United States","us","Washington, D.C.","Americas","North America","English 78,Spanish 13","Christianity 63,Unaffiliated 29,Judaism 2",9833517,331002647,19924,26949,80000,80000,37.09,-95.71],
            ["Uruguay","uy","Montevideo","Americas","South America","Spanish 99","Christianity 57,Unaffiliated 41",176215,3473727,660,59,17000,23000,-32.52,-55.76],
            ["Uzbekistan","uz","Tashkent","Asia","Asia","Uzbek 74,Russian 14,Tajik 4","Islam 93,Christianity 4",447400,34232050,0,60,1700,7700,41.37,64.58],
            ["Vanuatu","vu","Port Vila","Oceania","Oceania","Bislama 90,English 80,French 20","Christianity 93,Traditional 4",12189,307150,2528,0.9,3100,2800,-15.37,166.95],
            ["Vatican City","va","Vatican City","Europe","Europe","Italian 100,Latin 10","Christianity 100",0.49,825,0,0.02,21000,21000,41.90,12.45],
            ["Venezuela","ve","Caracas","Americas","South America","Spanish 98,Wayuu 1","Christianity 96,Unaffiliated 2",916445,28435943,2800,48,1700,5100,6.42,-66.58],
            ["Vietnam","vn","Hanoi","Asia","Asia","Vietnamese 85,English 20","Unaffiliated 73,Buddhism 12,Christianity 8",331212,97338583,3444,366,3700,11000,14.05,108.27],
            ["Yemen","ye","Sanaa","Asia","Asia","Arabic 99","Islam 99",527968,29825968,1906,20,700,2000,15.55,48.51],
            ["Zambia","zm","Lusaka","Africa","Africa","English 10,Bemba 33,Nyanja 14","Christianity 95,Traditional 2",752618,18383956,0,21,1100,3400,-13.13,27.84],
            ["Zimbabwe","zw","Harare","Africa","Africa","Shona 70,Ndebele 20,English 5","Christianity 84,Traditional 10",390757,14862927,0,25,1700,2400,-19.01,29.15]
        ];

        // Parse dataset into object format
        const allCountries = rawData.map(row => {
            const [name, iso, capStr, region, continent, langStr, relStr, area, pop, coastline, gdp, gdp_pc, gdp_ppp_pc, lat, lng] = row;
            
            const parseList = (str) => {
                if (!str || str === "N/A") return [];
                return str.split(',').map(s => {
                    const parts = s.trim().split(' ');
                    const p = parseFloat(parts.pop());
                    return { n: parts.join(' '), p: isNaN(p) ? 0 : p };
                });
            };

            return {
                name,
                iso,
                capitals: capStr.split(','),
                region,
                continent,
                languages: parseList(langStr),
                religions: parseList(relStr),
                area, pop, coastline, gdp, gdp_pc, gdp_ppp_pc, lat, lng
            };
        });

        const regions = ["All World", "Asia", "Europe", "Americas", "Africa", "Oceania"];

        // App State
        let currentRegion = 'All World';
        let activeDeck = [...allCountries];
        let currentQuestion = null;
        let correctSet = new Set();
        let visitedSet = new Set();
        
        let buttonsDisabled = false;
        let isProcessingAnswer = false; // Prevents double click logic
        let isOverlayOpen = false;
        let isGalleryOpen = false; // Tracks if gallery modal is actively open
        let isFactSheetFromGallery = false; // Track if we opened fact sheet from the gallery
        let isTransitioning = false;

        // Gallery State
        let currentGalleryRegion = null;
        let gallerySortMode = 'name-asc';
        let galleryFocusedIndex = -1; // Keyboard focus tracker
        const directionButtons = [
            { key: 'ArrowUp', el: null },    // index 0
            { key: 'ArrowDown', el: null },  // index 1
            { key: 'ArrowLeft', el: null },  // index 2
            { key: 'ArrowRight', el: null }  // index 3
        ];

        const DOM = {
            tabs: document.getElementById('region-tabs'),
            metricCorrect: document.getElementById('metric-correct'),
            metricVisited: document.getElementById('metric-visited'),
            metricDeck: document.getElementById('metric-deck'),
            flagImage: document.getElementById('flag-image'),
            flagLoader: document.getElementById('flag-loader'),
            
            overlay: document.getElementById('result-overlay'),
            overlayBackdrop: document.getElementById('overlay-backdrop'),
            overlayContent: document.getElementById('overlay-content'),
            
            fsCountryName: document.getElementById('fs-country-name'),
            fsFlag: document.getElementById('fs-flag'),
            fsCapital: document.getElementById('fs-capital'),
            fsContinent: document.getElementById('fs-continent'),
            fsCoastline: document.getElementById('fs-coastline'),
            fsPopulation: document.getElementById('fs-population'),
            fsArea: document.getElementById('fs-area'),
            fsLanguage: document.getElementById('fs-language'),
            fsReligion: document.getElementById('fs-religion'),
            fsGdp: document.getElementById('fs-gdp'),
            fsGdpPc: document.getElementById('fs-gdp-pc'),
            fsGdpPpp: document.getElementById('fs-gdp-ppp'),
            mapIframe: document.getElementById('map-iframe'),
        };

        function init() {
            directionButtons[0].el = document.getElementById('btn-up');
            directionButtons[1].el = document.getElementById('btn-down');
            directionButtons[2].el = document.getElementById('btn-left');
            directionButtons[3].el = document.getElementById('btn-right');

            DOM.metricDeck.innerText = activeDeck.length;

            initTabs();
            generateQuestion();
            setupKeyboardListeners();
        }

        // Initialize Tabs - using a custom click counter for reliable touch triple clicks
        function initTabs() {
            DOM.tabs.innerHTML = '';
            
            const clickCounts = {};
            const clickTimers = {};

            regions.forEach(region => {
                const btn = document.createElement('button');
                btn.innerText = region;
                btn.dataset.region = region;
                
                // Custom double-click logic (handles rapid taps flawlessly on mobile & desktop)
                btn.addEventListener('click', (e) => {
                    e.preventDefault(); // Prevent accidental zoom on mobile
                    
                    if (!clickCounts[region]) clickCounts[region] = 0;
                    clickCounts[region]++;

                    if (clickCounts[region] === 1) {
                        // Action for single click: Update instantly for snappy UI
                        filterRegion(region);

                        // Set a window for subsequent clicks
                        clickTimers[region] = setTimeout(() => {
                            clickCounts[region] = 0; // reset after timeout
                        }, 400); // 400ms is a generous window for 2 rapid taps
                    } 
                    else if (clickCounts[region] === 2) {
                        // Action for double click
                        clearTimeout(clickTimers[region]);
                        clickCounts[region] = 0;
                        openGallery(region);
                    }
                });
                
                DOM.tabs.appendChild(btn);
            });
            updateTabsState();
        }

        function updateTabsState() {
            Array.from(DOM.tabs.children).forEach(btn => {
                const region = btn.dataset.region;
                btn.className = `px-3 py-1 md:py-1.5 text-[11px] md:text-xs rounded-full font-bold whitespace-nowrap transition-all focus:outline-none ${region === currentRegion ? 'bg-[#3182ce] text-white shadow-sm' : 'bg-transparent text-slate-500 hover:text-slate-800 hover:bg-slate-50'}`;
            });
        }

        function filterRegion(region) {
            if (currentRegion === region) return; // Prevent rebuilding if same
            
            currentRegion = region;
            if (region === 'All World') {
                activeDeck = [...allCountries];
            } else {
                activeDeck = allCountries.filter(c => c.region === region);
            }
            updateTabsState();
            DOM.metricDeck.innerText = activeDeck.length;
            generateQuestion();
        }

        function handleBackdropClick() {
            if (isFactSheetFromGallery) {
                // If opened from gallery, just dismiss this overlay without generating a new question
                isFactSheetFromGallery = false;
                isOverlayOpen = false;
                DOM.overlayBackdrop.classList.remove('opacity-100');
                DOM.overlayContent.classList.remove('scale-100', 'opacity-100');
                DOM.overlayContent.classList.add('scale-95', 'opacity-0');
                setTimeout(() => {
                    if(!isOverlayOpen) DOM.overlay.classList.remove('flex');
                    DOM.overlay.classList.add('hidden');
                }, 150);
            } else {
                // Regular gameplay dismiss
                generateQuestion();
            }
        }

        function generateQuestion() {
            if (activeDeck.length === 0 || isTransitioning) return;
            isTransitioning = true;
            buttonsDisabled = true;
            isProcessingAnswer = false; 
            
            // Dismiss Modal
            isOverlayOpen = false;
            DOM.overlayBackdrop.classList.remove('opacity-100');
            DOM.overlayContent.classList.remove('scale-100', 'opacity-100');
            DOM.overlayContent.classList.add('scale-95', 'opacity-0');
            
            setTimeout(() => {
                if(!isOverlayOpen) DOM.overlay.classList.remove('flex');
                DOM.overlay.classList.add('hidden');
                isTransitioning = false;
            }, 150);

            // Reset Button Styling
            directionButtons.forEach(btnObj => {
                const el = btnObj.el;
                const label = el.querySelector('.name-label');
                const prefix = el.querySelector('.prefix-label');

                el.classList.remove('bg-[#10b981]', 'border-[#10b981]', 'bg-[#ef4444]', 'border-[#ef4444]', 'scale-105', 'shadow-md', 'z-20', 'animate-shake', 'opacity-40', 'cursor-default');
                el.classList.add('bg-white', 'border-slate-200', 'hover:border-blue-400', 'hover:bg-blue-50', 'active:scale-95', 'cursor-pointer', 'group');
                
                label.classList.remove('text-white');
                label.classList.add('text-slate-700');
                
                prefix.classList.remove('text-white', 'text-white/80');
                prefix.classList.add('text-slate-400', 'opacity-70');
            });

            // Generate options logic
            const correctCountry = activeDeck[Math.floor(Math.random() * activeDeck.length)];
            let options = [correctCountry];
            
            while (options.length < 4) {
                const distractor = allCountries[Math.floor(Math.random() * allCountries.length)];
                if (!options.find(o => o.iso === distractor.iso)) {
                    options.push(distractor);
                }
            }

            options.sort(() => Math.random() - 0.5);
            
            currentQuestion = {
                correct: correctCountry,
                options: options
            };

            renderQuestion();
        }

        function renderQuestion() {
            DOM.flagImage.classList.add('hidden');
            DOM.flagLoader.classList.remove('hidden');
            
            DOM.flagImage.onload = () => {
                DOM.flagLoader.classList.add('hidden');
                DOM.flagImage.classList.remove('hidden');
                buttonsDisabled = false;
            };
            DOM.flagImage.src = `https://flagcdn.com/w320/${currentQuestion.correct.iso}.png`;

            directionButtons.forEach((btnObj, index) => {
                const option = currentQuestion.options[index];
                btnObj.el.querySelector('.name-label').innerText = option.name;
                btnObj.el.onclick = () => handleAnswer(option, index);
            });
        }

        function handleAnswer(selectedOption, selectedIndex) {
            if (buttonsDisabled || isTransitioning || isProcessingAnswer) return;
            isProcessingAnswer = true;
            buttonsDisabled = true;
            
            visitedSet.add(currentQuestion.correct.iso);
            const isCorrect = selectedOption.iso === currentQuestion.correct.iso;

            // Animate buttons based on guess
            directionButtons.forEach((btnObj, index) => {
                const option = currentQuestion.options[index];
                const isThisCorrect = option.iso === currentQuestion.correct.iso;
                const el = btnObj.el;
                const label = el.querySelector('.name-label');
                const prefix = el.querySelector('.prefix-label');
                
                el.classList.remove('hover:border-blue-400', 'hover:bg-blue-50', 'active:scale-95', 'cursor-pointer', 'group');
                el.classList.add('cursor-default');

                if (isThisCorrect) {
                    el.classList.remove('bg-white', 'border-slate-200');
                    el.classList.add('bg-[#10b981]', 'border-[#10b981]', 'scale-105', 'shadow-md', 'z-20');
                    label.classList.remove('text-slate-700');
                    label.classList.add('text-white');
                    prefix.classList.remove('text-slate-400', 'opacity-70');
                    prefix.classList.add('text-white/80');
                    if(isCorrect) correctSet.add(currentQuestion.correct.iso);
                } else if (index === selectedIndex) {
                    el.classList.remove('bg-white', 'border-slate-200');
                    el.classList.add('bg-[#ef4444]', 'border-[#ef4444]', 'animate-shake', 'z-20');
                    label.classList.remove('text-slate-700');
                    label.classList.add('text-white');
                    prefix.classList.remove('text-slate-400', 'opacity-70');
                    prefix.classList.add('text-white/80');
                } else {
                    el.classList.add('opacity-40');
                }
            });

            DOM.metricCorrect.innerText = correctSet.size;
            DOM.metricVisited.innerText = visitedSet.size;
            
            setTimeout(() => showFactSheet(currentQuestion.correct), 300);
        }

        function formatPop(pop) {
            let western = pop >= 1e9 ? (pop / 1e9).toFixed(2) + " bn" : (pop >= 1e6 ? (pop / 1e6).toFixed(2) + " mn" : pop.toLocaleString());
            let indian = pop >= 1e7 ? (pop / 1e7).toFixed(2) + " crores" : (pop >= 1e5 ? (pop / 1e5).toFixed(2) + " lakhs" : pop.toLocaleString());
            return `${western} | ${indian}`;
        }
        function formatPopShort(pop) {
            let western = pop >= 1e9 ? (pop / 1e9).toFixed(2) + "B" : (pop >= 1e6 ? (pop / 1e6).toFixed(1) + "M" : (pop >= 1e3 ? (pop / 1e3).toFixed(1) + "K" : pop.toLocaleString()));
            let indian = pop >= 1e7 ? (pop / 1e7).toFixed(2) + "C" : (pop >= 1e5 ? (pop / 1e5).toFixed(2) + "L" : (pop >= 1e3 ? (pop / 1e3).toFixed(1) + "K" : pop.toLocaleString()));
            return `${western} | ${indian}`;
        }

        function formatArea(areaSqKm) {
            const acres = areaSqKm * 247.105;
            let acresStr = acres >= 1e9 ? (acres / 1e9).toFixed(2) + " bn acres" : (acres >= 1e6 ? (acres / 1e6).toFixed(2) + " mn acres" : Math.round(acres).toLocaleString() + " acres");
            return `${areaSqKm.toLocaleString()} sq km | ${acresStr}`;
        }

        function formatListWithPercentages(list) {
            if (!list || list.length === 0) return 'N/A';
            return list
                .filter(item => item.p >= 1)
                .sort((a, b) => b.p - a.p)
                .slice(0, 3)
                .map(item => `${item.n} (${item.p}%)`)
                .join(', ') || 'N/A';
        }

        function formatBillionUsd(billions) {
            if (billions >= 1000) return `$${(billions / 1000).toFixed(2)} Trillion`;
            return `$${billions.toLocaleString()} Billion`;
        }

        function showFactSheet(country) {
            DOM.fsCountryName.innerText = country.name;
            DOM.fsFlag.src = `https://flagcdn.com/w80/${country.iso}.png`;
            DOM.fsCapital.innerText = country.capitals ? country.capitals.join(', ') : 'N/A';
            DOM.fsContinent.innerText = country.continent;
            DOM.fsCoastline.innerText = country.coastline ? `${country.coastline.toLocaleString()} km` : 'N/A';
            
            DOM.fsPopulation.innerText = formatPop(country.pop);
            DOM.fsArea.innerText = formatArea(country.area);
            DOM.fsLanguage.innerText = formatListWithPercentages(country.languages);
            DOM.fsReligion.innerText = formatListWithPercentages(country.religions);
            
            DOM.fsGdp.innerText = country.gdp ? formatBillionUsd(country.gdp) : 'N/A';
            DOM.fsGdpPc.innerText = country.gdp_pc ? `$${country.gdp_pc.toLocaleString()}` : 'N/A';
            DOM.fsGdpPpp.innerText = country.gdp_ppp_pc ? `$${country.gdp_ppp_pc.toLocaleString()}` : 'N/A';

            DOM.mapIframe.src = `https://maps.google.com/maps?q=${country.lat},${country.lng}&hl=en&z=5&output=embed`;

            isOverlayOpen = true;
            DOM.overlay.classList.remove('hidden');
            DOM.overlay.classList.add('flex');
            
            void DOM.overlay.offsetWidth; 
            
            DOM.overlayBackdrop.classList.add('opacity-100');
            DOM.overlayContent.classList.remove('scale-95', 'opacity-0');
            DOM.overlayContent.classList.add('scale-100', 'opacity-100');
        }

        // --- Region Gallery Logic ---

        function openGallery(region) {
            currentGalleryRegion = region;
            isGalleryOpen = true;
            galleryFocusedIndex = -1; // Reset keyboard focus
            document.getElementById('gallery-title').innerText = region === 'All World' ? 'Global Flags' : `${region} Flags`;
            
            const overlay = document.getElementById('gallery-overlay');
            const backdrop = document.getElementById('gallery-backdrop');
            const content = document.getElementById('gallery-content');
            
            overlay.classList.remove('hidden');
            overlay.classList.add('flex');
            
            void overlay.offsetWidth;
            
            backdrop.classList.add('opacity-100');
            content.classList.remove('scale-95', 'opacity-0');
            content.classList.add('scale-100', 'opacity-100');
            
            sortGallery('name-asc');
        }

        function closeGallery() {
            isGalleryOpen = false;
            const overlay = document.getElementById('gallery-overlay');
            const backdrop = document.getElementById('gallery-backdrop');
            const content = document.getElementById('gallery-content');
            
            backdrop.classList.remove('opacity-100');
            content.classList.remove('scale-100', 'opacity-100');
            content.classList.add('scale-95', 'opacity-0');
            
            setTimeout(() => {
                overlay.classList.remove('flex');
                overlay.classList.add('hidden');
            }, 150);
        }

        function sortGallery(mode) {
            gallerySortMode = mode;
            
            // Toggle highlight styles on the UI buttons
            ['name-asc', 'name-desc', 'pop-asc', 'pop-desc'].forEach(m => {
                const btn = document.getElementById(`sort-${m}`);
                if(m === mode) {
                    btn.classList.add('bg-white', 'shadow-sm', 'text-[#3182ce]');
                    btn.classList.remove('text-slate-500');
                } else {
                    btn.classList.remove('bg-white', 'shadow-sm', 'text-[#3182ce]');
                    btn.classList.add('text-slate-500');
                }
            });

            renderGallery();
        }

        function renderGallery() {
            const grid = document.getElementById('gallery-grid');
            grid.innerHTML = ''; 
            galleryFocusedIndex = -1; // Reset focus on rerender
            
            // Filter by Region
            let countries = currentGalleryRegion === 'All World' 
                ? [...allCountries] 
                : allCountries.filter(c => c.region === currentGalleryRegion);

            document.getElementById('gallery-count').innerText = countries.length;

            // Apply selected sorting algorithm
            countries.sort((a, b) => {
                if (gallerySortMode === 'name-asc') return a.name.localeCompare(b.name);
                if (gallerySortMode === 'name-desc') return b.name.localeCompare(a.name);
                if (gallerySortMode === 'pop-asc') return a.pop - b.pop;
                if (gallerySortMode === 'pop-desc') return b.pop - a.pop;
                return 0;
            });

            // Paint DOM elements
            countries.forEach((country, index) => {
                // Changed background to bg-slate-100 to strike a balance between grey and white
                const card = document.createElement('div');
                card.className = "bg-slate-100 p-3 md:p-4 rounded-2xl shadow-sm border border-slate-200 flex flex-col items-center gap-3 hover:shadow-md hover:border-slate-300 transition-all cursor-pointer";
                
                // Allow opening the Fact Sheet straight from the gallery
                card.onclick = () => {
                    galleryFocusedIndex = index; // Update focus purely for visual return
                    updateGalleryFocus(document.querySelectorAll('#gallery-grid > div'));
                    isFactSheetFromGallery = true;
                    showFactSheet(country);
                };
                
                // Added a subtle drop shadow to the image so white flags remain visible
                card.innerHTML = `
                    <div class="w-full aspect-[4/3] bg-transparent rounded-lg flex items-center justify-center overflow-hidden relative">
                        <img src="https://flagcdn.com/w160/${country.iso}.png" loading="lazy" alt="${country.name}" class="w-full h-full object-contain drop-shadow-[0_0_2px_rgba(0,0,0,0.15)]">
                    </div>
                    <div class="w-full text-center">
                        <p class="font-bold text-slate-700 text-xs sm:text-sm truncate w-full" title="${country.name}">${country.name}</p>
                        ${gallerySortMode.includes('pop') ? `<p class="text-[10px] text-[#3182ce] font-bold mt-1 uppercase tracking-wider">${formatPopShort(country.pop)}</p>` : ''}
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        // Helper to update the visual focus state of the grid items
        function updateGalleryFocus(cards) {
            cards.forEach((c, i) => {
                if (i === galleryFocusedIndex) {
                    c.classList.add('ring-4', 'ring-[#3182ce]', 'ring-offset-2', 'border-[#3182ce]');
                    // Adjusted to match the new lighter border standard
                    c.classList.remove('border-slate-200');
                    // 'nearest' combined with the pt-6 pb-32 on the container guarantees it brings the top/bottom items fully into view smoothly
                    c.scrollIntoView({ block: 'nearest', behavior: 'smooth' });
                } else {
                    c.classList.remove('ring-4', 'ring-[#3182ce]', 'ring-offset-2', 'border-[#3182ce]');
                    // Adjusted to match the new lighter border standard
                    c.classList.add('border-slate-200');
                }
            });
        }

        // Global Keyboard Routing
        function setupKeyboardListeners() {
            document.addEventListener('keydown', (e) => {
                // 1. If Fact Sheet Overlay is open (highest priority)
                if (isOverlayOpen && !isTransitioning) {
                    if (['ArrowUp', 'ArrowDown', 'ArrowLeft', 'ArrowRight', 'Enter', ' ', 'Escape'].includes(e.key)) {
                        e.preventDefault();
                        handleBackdropClick(); // This intelligently handles returning to gallery vs returning to game
                    }
                } 
                // 2. If Gallery Overlay is open
                else if (isGalleryOpen) {
                    const cards = document.querySelectorAll('#gallery-grid > div');
                    if (!cards.length) return;
                    
                    // Safely calculate column count based on active Tailwind breakpoints 
                    const vw = window.innerWidth;
                    let colCount = 2; // default grid-cols-2
                    if (vw >= 1024) colCount = 5; // lg:grid-cols-5
                    else if (vw >= 768) colCount = 4; // md:grid-cols-4
                    else if (vw >= 640) colCount = 3; // sm:grid-cols-3
                    
                    if (['ArrowRight', 'ArrowLeft', 'ArrowDown', 'ArrowUp'].includes(e.key)) {
                        e.preventDefault();
                        
                        if (galleryFocusedIndex === -1) {
                            galleryFocusedIndex = 0; // Initialize focus on first keystroke
                        } else {
                            if (e.key === 'ArrowRight') galleryFocusedIndex++;
                            else if (e.key === 'ArrowLeft') galleryFocusedIndex--;
                            else if (e.key === 'ArrowDown') galleryFocusedIndex += colCount;
                            else if (e.key === 'ArrowUp') galleryFocusedIndex -= colCount;
                        }
                        
                        // Clamp focus bounds
                        if (galleryFocusedIndex < 0) galleryFocusedIndex = 0;
                        if (galleryFocusedIndex >= cards.length) galleryFocusedIndex = cards.length - 1;
                        
                        updateGalleryFocus(cards);
                    } 
                    else if (e.key === 'Enter' || e.key === ' ') {
                        e.preventDefault();
                        if (galleryFocusedIndex >= 0 && galleryFocusedIndex < cards.length) {
                            cards[galleryFocusedIndex].click();
                        }
                    } 
                    else if (e.key === 'Escape') {
                        e.preventDefault();
                        closeGallery();
                    }
                }
                // 3. If game is active
                else if (!buttonsDisabled && !isTransitioning && currentQuestion) {
                    const keyMap = {
                        'ArrowUp': 0,
                        'ArrowDown': 1,
                        'ArrowLeft': 2,
                        'ArrowRight': 3
                    };
                    if (e.key in keyMap) {
                        e.preventDefault();
                        const index = keyMap[e.key];
                        handleAnswer(currentQuestion.options[index], index);
                    }
                }
            });
        }

        // Boot Application
        init();
    </script>
</body>
</html>
