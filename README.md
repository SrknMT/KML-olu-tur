<html lang="tr"><head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KML Görüntüleyici ve Profesyonel Koordinat Dönüştürücü</title>
    <!-- Tailwind CSS (Stil için) -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Leaflet CSS (Harita için) -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY=" crossorigin="">
    <!-- Leaflet JS -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js" integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo=" crossorigin=""></script>
    <!-- Proj4js (Koordinat Dönüşümü için) -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/proj4js/2.9.0/proj4.js"></script>
    
    <style>
        #map {
            height: 100%;
            width: 100%;
            z-index: 1;
        }
        .scroller::-webkit-scrollbar {
            width: 8px;
        }
        .scroller::-webkit-scrollbar-track {
            background: #f1f1f1; 
        }
        .scroller::-webkit-scrollbar-thumb {
            background: #888; 
            border-radius: 4px;
        }
        .scroller::-webkit-scrollbar-thumb:hover {
            background: #555; 
        }
    </style>
<style>*, ::before, ::after{--tw-border-spacing-x:0;--tw-border-spacing-y:0;--tw-translate-x:0;--tw-translate-y:0;--tw-rotate:0;--tw-skew-x:0;--tw-skew-y:0;--tw-scale-x:1;--tw-scale-y:1;--tw-pan-x: ;--tw-pan-y: ;--tw-pinch-zoom: ;--tw-scroll-snap-strictness:proximity;--tw-gradient-from-position: ;--tw-gradient-via-position: ;--tw-gradient-to-position: ;--tw-ordinal: ;--tw-slashed-zero: ;--tw-numeric-figure: ;--tw-numeric-spacing: ;--tw-numeric-fraction: ;--tw-ring-inset: ;--tw-ring-offset-width:0px;--tw-ring-offset-color:#fff;--tw-ring-color:rgb(59 130 246 / 0.5);--tw-ring-offset-shadow:0 0 #0000;--tw-ring-shadow:0 0 #0000;--tw-shadow:0 0 #0000;--tw-shadow-colored:0 0 #0000;--tw-blur: ;--tw-brightness: ;--tw-contrast: ;--tw-grayscale: ;--tw-hue-rotate: ;--tw-invert: ;--tw-saturate: ;--tw-sepia: ;--tw-drop-shadow: ;--tw-backdrop-blur: ;--tw-backdrop-brightness: ;--tw-backdrop-contrast: ;--tw-backdrop-grayscale: ;--tw-backdrop-hue-rotate: ;--tw-backdrop-invert: ;--tw-backdrop-opacity: ;--tw-backdrop-saturate: ;--tw-backdrop-sepia: ;--tw-contain-size: ;--tw-contain-layout: ;--tw-contain-paint: ;--tw-contain-style: }::backdrop{--tw-border-spacing-x:0;--tw-border-spacing-y:0;--tw-translate-x:0;--tw-translate-y:0;--tw-rotate:0;--tw-skew-x:0;--tw-skew-y:0;--tw-scale-x:1;--tw-scale-y:1;--tw-pan-x: ;--tw-pan-y: ;--tw-pinch-zoom: ;--tw-scroll-snap-strictness:proximity;--tw-gradient-from-position: ;--tw-gradient-via-position: ;--tw-gradient-to-position: ;--tw-ordinal: ;--tw-slashed-zero: ;--tw-numeric-figure: ;--tw-numeric-spacing: ;--tw-numeric-fraction: ;--tw-ring-inset: ;--tw-ring-offset-width:0px;--tw-ring-offset-color:#fff;--tw-ring-color:rgb(59 130 246 / 0.5);--tw-ring-offset-shadow:0 0 #0000;--tw-ring-shadow:0 0 #0000;--tw-shadow:0 0 #0000;--tw-shadow-colored:0 0 #0000;--tw-blur: ;--tw-brightness: ;--tw-contrast: ;--tw-grayscale: ;--tw-hue-rotate: ;--tw-invert: ;--tw-saturate: ;--tw-sepia: ;--tw-drop-shadow: ;--tw-backdrop-blur: ;--tw-backdrop-brightness: ;--tw-backdrop-contrast: ;--tw-backdrop-grayscale: ;--tw-backdrop-hue-rotate: ;--tw-backdrop-invert: ;--tw-backdrop-opacity: ;--tw-backdrop-saturate: ;--tw-backdrop-sepia: ;--tw-contain-size: ;--tw-contain-layout: ;--tw-contain-paint: ;--tw-contain-style: }/* ! tailwindcss v3.4.17 | MIT License | https://tailwindcss.com */*,::after,::before{box-sizing:border-box;border-width:0;border-style:solid;border-color:#e5e7eb}::after,::before{--tw-content:''}:host,html{line-height:1.5;-webkit-text-size-adjust:100%;-moz-tab-size:4;tab-size:4;font-family:ui-sans-serif, system-ui, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";font-feature-settings:normal;font-variation-settings:normal;-webkit-tap-highlight-color:transparent}body{margin:0;line-height:inherit}hr{height:0;color:inherit;border-top-width:1px}abbr:where([title]){-webkit-text-decoration:underline dotted;text-decoration:underline dotted}h1,h2,h3,h4,h5,h6{font-size:inherit;font-weight:inherit}a{color:inherit;text-decoration:inherit}b,strong{font-weight:bolder}code,kbd,pre,samp{font-family:ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;font-feature-settings:normal;font-variation-settings:normal;font-size:1em}small{font-size:80%}sub,sup{font-size:75%;line-height:0;position:relative;vertical-align:baseline}sub{bottom:-.25em}sup{top:-.5em}table{text-indent:0;border-color:inherit;border-collapse:collapse}button,input,optgroup,select,textarea{font-family:inherit;font-feature-settings:inherit;font-variation-settings:inherit;font-size:100%;font-weight:inherit;line-height:inherit;letter-spacing:inherit;color:inherit;margin:0;padding:0}button,select{text-transform:none}button,input:where([type=button]),input:where([type=reset]),input:where([type=submit]){-webkit-appearance:button;background-color:transparent;background-image:none}:-moz-focusring{outline:auto}:-moz-ui-invalid{box-shadow:none}progress{vertical-align:baseline}::-webkit-inner-spin-button,::-webkit-outer-spin-button{height:auto}[type=search]{-webkit-appearance:textfield;outline-offset:-2px}::-webkit-search-decoration{-webkit-appearance:none}::-webkit-file-upload-button{-webkit-appearance:button;font:inherit}summary{display:list-item}blockquote,dd,dl,figure,h1,h2,h3,h4,h5,h6,hr,p,pre{margin:0}fieldset{margin:0;padding:0}legend{padding:0}menu,ol,ul{list-style:none;margin:0;padding:0}dialog{padding:0}textarea{resize:vertical}input::placeholder,textarea::placeholder{opacity:1;color:#9ca3af}[role=button],button{cursor:pointer}:disabled{cursor:default}audio,canvas,embed,iframe,img,object,svg,video{display:block;vertical-align:middle}img,video{max-width:100%;height:auto}[hidden]:where(:not([hidden=until-found])){display:none}.pointer-events-none{pointer-events:none}.absolute{position:absolute}.relative{position:relative}.left-1\/2{left:50%}.top-1\/2{top:50%}.z-10{z-index:10}.z-20{z-index:20}.z-\[1000\]{z-index:1000}.mb-1{margin-bottom:0.25rem}.mb-2{margin-bottom:0.5rem}.mt-10{margin-top:2.5rem}.block{display:block}.flex{display:flex}.grid{display:grid}.hidden{display:none}.h-2\/3{height:66.666667%}.h-4{height:1rem}.h-5{height:1.25rem}.h-6{height:1.5rem}.h-screen{height:100vh}.w-4{width:1rem}.w-5{width:1.25rem}.w-6{width:1.5rem}.w-full{width:100%}.max-w-\[150px\]{max-width:150px}.flex-1{flex:1 1 0%}.shrink-0{flex-shrink:0}.-translate-x-1\/2{--tw-translate-x:-50%;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.-translate-y-1\/2{--tw-translate-y:-50%;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.transform{transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.cursor-pointer{cursor:pointer}.grid-cols-2{grid-template-columns:repeat(2, minmax(0, 1fr))}.flex-col{flex-direction:column}.items-center{align-items:center}.justify-center{justify-content:center}.justify-between{justify-content:space-between}.gap-2{gap:0.5rem}.gap-4{gap:1rem}.space-y-2 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(0.5rem * calc(1 - var(--tw-space-y-reverse)));margin-bottom:calc(0.5rem * var(--tw-space-y-reverse))}.space-y-3 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(0.75rem * calc(1 - var(--tw-space-y-reverse)));margin-bottom:calc(0.75rem * var(--tw-space-y-reverse))}.overflow-hidden{overflow:hidden}.overflow-y-auto{overflow-y:auto}.truncate{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}.rounded{border-radius:0.25rem}.rounded-full{border-radius:9999px}.rounded-lg{border-radius:0.5rem}.rounded-xl{border-radius:0.75rem}.border{border-width:1px}.border-b{border-bottom-width:1px}.border-r{border-right-width:1px}.border-t{border-top-width:1px}.border-blue-200{--tw-border-opacity:1;border-color:rgb(191 219 254 / var(--tw-border-opacity, 1))}.border-gray-100{--tw-border-opacity:1;border-color:rgb(243 244 246 / var(--tw-border-opacity, 1))}.border-gray-200{--tw-border-opacity:1;border-color:rgb(229 231 235 / var(--tw-border-opacity, 1))}.border-gray-300{--tw-border-opacity:1;border-color:rgb(209 213 219 / var(--tw-border-opacity, 1))}.bg-blue-600{--tw-bg-opacity:1;background-color:rgb(37 99 235 / var(--tw-bg-opacity, 1))}.bg-gray-100{--tw-bg-opacity:1;background-color:rgb(243 244 246 / var(--tw-bg-opacity, 1))}.bg-gray-200{--tw-bg-opacity:1;background-color:rgb(229 231 235 / var(--tw-bg-opacity, 1))}.bg-gray-50{--tw-bg-opacity:1;background-color:rgb(249 250 251 / var(--tw-bg-opacity, 1))}.bg-green-600{--tw-bg-opacity:1;background-color:rgb(22 163 74 / var(--tw-bg-opacity, 1))}.bg-slate-50{--tw-bg-opacity:1;background-color:rgb(248 250 252 / var(--tw-bg-opacity, 1))}.bg-white{--tw-bg-opacity:1;background-color:rgb(255 255 255 / var(--tw-bg-opacity, 1))}.bg-white\/90{background-color:rgb(255 255 255 / 0.9)}.p-2{padding:0.5rem}.p-3{padding:0.75rem}.p-4{padding:1rem}.p-6{padding:1.5rem}.px-2{padding-left:0.5rem;padding-right:0.5rem}.px-4{padding-left:1rem;padding-right:1rem}.py-0\.5{padding-top:0.125rem;padding-bottom:0.125rem}.py-2{padding-top:0.5rem;padding-bottom:0.5rem}.py-2\.5{padding-top:0.625rem;padding-bottom:0.625rem}.text-center{text-align:center}.font-sans{font-family:ui-sans-serif, system-ui, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji"}.text-\[10px\]{font-size:10px}.text-lg{font-size:1.125rem;line-height:1.75rem}.text-sm{font-size:0.875rem;line-height:1.25rem}.text-xs{font-size:0.75rem;line-height:1rem}.font-bold{font-weight:700}.font-medium{font-weight:500}.font-semibold{font-weight:600}.uppercase{text-transform:uppercase}.italic{font-style:italic}.leading-tight{line-height:1.25}.tracking-wider{letter-spacing:0.05em}.text-blue-600{--tw-text-opacity:1;color:rgb(37 99 235 / var(--tw-text-opacity, 1))}.text-gray-400{--tw-text-opacity:1;color:rgb(156 163 175 / var(--tw-text-opacity, 1))}.text-gray-500{--tw-text-opacity:1;color:rgb(107 114 128 / var(--tw-text-opacity, 1))}.text-gray-600{--tw-text-opacity:1;color:rgb(75 85 99 / var(--tw-text-opacity, 1))}.text-gray-700{--tw-text-opacity:1;color:rgb(55 65 81 / var(--tw-text-opacity, 1))}.text-gray-800{--tw-text-opacity:1;color:rgb(31 41 55 / var(--tw-text-opacity, 1))}.text-green-600{--tw-text-opacity:1;color:rgb(22 163 74 / var(--tw-text-opacity, 1))}.text-white{--tw-text-opacity:1;color:rgb(255 255 255 / var(--tw-text-opacity, 1))}.shadow-lg{--tw-shadow:0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 10px 15px -3px var(--tw-shadow-color), 0 4px 6px -4px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.shadow-md{--tw-shadow:0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 4px 6px -1px var(--tw-shadow-color), 0 2px 4px -2px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.shadow-sm{--tw-shadow:0 1px 2px 0 rgb(0 0 0 / 0.05);--tw-shadow-colored:0 1px 2px 0 var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.shadow-xl{--tw-shadow:0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 20px 25px -5px var(--tw-shadow-color), 0 8px 10px -6px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.outline-none{outline:2px solid transparent;outline-offset:2px}.backdrop-blur-sm{--tw-backdrop-blur:blur(4px);-webkit-backdrop-filter:var(--tw-backdrop-blur) var(--tw-backdrop-brightness) var(--tw-backdrop-contrast) var(--tw-backdrop-grayscale) var(--tw-backdrop-hue-rotate) var(--tw-backdrop-invert) var(--tw-backdrop-opacity) var(--tw-backdrop-saturate) var(--tw-backdrop-sepia);backdrop-filter:var(--tw-backdrop-blur) var(--tw-backdrop-brightness) var(--tw-backdrop-contrast) var(--tw-backdrop-grayscale) var(--tw-backdrop-hue-rotate) var(--tw-backdrop-invert) var(--tw-backdrop-opacity) var(--tw-backdrop-saturate) var(--tw-backdrop-sepia)}.transition{transition-property:color, background-color, border-color, fill, stroke, opacity, box-shadow, transform, filter, -webkit-text-decoration-color, -webkit-backdrop-filter;transition-property:color, background-color, border-color, text-decoration-color, fill, stroke, opacity, box-shadow, transform, filter, backdrop-filter;transition-property:color, background-color, border-color, text-decoration-color, fill, stroke, opacity, box-shadow, transform, filter, backdrop-filter, -webkit-text-decoration-color, -webkit-backdrop-filter;transition-timing-function:cubic-bezier(0.4, 0, 0.2, 1);transition-duration:150ms}.hover\:bg-blue-50:hover{--tw-bg-opacity:1;background-color:rgb(239 246 255 / var(--tw-bg-opacity, 1))}.hover\:bg-blue-700:hover{--tw-bg-opacity:1;background-color:rgb(29 78 216 / var(--tw-bg-opacity, 1))}.hover\:bg-gray-50:hover{--tw-bg-opacity:1;background-color:rgb(249 250 251 / var(--tw-bg-opacity, 1))}.hover\:bg-green-700:hover{--tw-bg-opacity:1;background-color:rgb(21 128 61 / var(--tw-bg-opacity, 1))}.focus\:ring-1:focus{--tw-ring-offset-shadow:var(--tw-ring-inset) 0 0 0 var(--tw-ring-offset-width) var(--tw-ring-offset-color);--tw-ring-shadow:var(--tw-ring-inset) 0 0 0 calc(1px + var(--tw-ring-offset-width)) var(--tw-ring-color);box-shadow:var(--tw-ring-offset-shadow), var(--tw-ring-shadow), var(--tw-shadow, 0 0 #0000)}.focus\:ring-blue-500:focus{--tw-ring-opacity:1;--tw-ring-color:rgb(59 130 246 / var(--tw-ring-opacity, 1))}@media (min-width: 768px){.md\:mb-0{margin-bottom:0px}.md\:h-auto{height:auto}.md\:w-\[420px\]{width:420px}.md\:flex-row{flex-direction:row}.md\:border-l{border-left-width:1px}.md\:border-t-0{border-top-width:0px}}</style></head>
<body class="bg-gray-100 h-screen flex flex-col font-sans overflow-hidden">

    <!-- Header -->
    <header class="bg-white shadow-md p-3 flex flex-col md:flex-row items-center justify-between z-10 shrink-0 border-b border-gray-200">
        <div class="flex items-center gap-2 mb-2 md:mb-0">
            <div class="bg-blue-600 text-white p-2 rounded-lg">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 20l-5.447-2.724A1 1 0 013 16.382V5.618a1 1 0 011.447-.894L9 7m0 13l6-3m-6 3V7m6 10l4.553 2.276A1 1 0 0021 18.382V7.618a1 1 0 00-.553-.894L15 7m0 13V7m0 0L9.553 4.553A1 1 0 009 3.618C9 3.618 9 7 9 7"></path>
                </svg>
            </div>
            <div>
                <h1 class="text-lg font-bold text-gray-800 leading-tight">KML Koordinat Okuyucu</h1>
                <p class="text-xs text-gray-500">WGS84 / ED50 / UTM / TM Dönüştürücü</p>
            </div>
        </div>

        <div class="flex items-center gap-4">
            <label class="flex items-center gap-2 px-4 py-2 bg-blue-600 text-white rounded-lg cursor-pointer hover:bg-blue-700 transition shadow-sm text-sm font-medium">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12"></path>
                </svg>
                <span>KML Yükle</span>
                <input type="file" id="fileInput" accept=".kml" class="hidden">
            </label>
            <span id="fileName" class="text-xs text-gray-500 italic max-w-[150px] truncate">Dosya seçilmedi</span>
        </div>
    </header>

    <!-- Main Content -->
    <main class="flex-1 flex flex-col md:flex-row overflow-hidden relative">
        
        <!-- Map Panel -->
        <div class="flex-1 relative bg-gray-200 border-r border-gray-300">
            <div id="map" class="leaflet-container leaflet-touch leaflet-retina leaflet-fade-anim leaflet-grab leaflet-touch-drag leaflet-touch-zoom" tabindex="0" style="position: relative;"><div class="leaflet-pane leaflet-map-pane" style="transform: translate3d(0px, 0px, 0px);"><div class="leaflet-pane leaflet-tile-pane"><div class="leaflet-layer " style="z-index: 1; opacity: 1;"><div class="leaflet-tile-container leaflet-zoom-animated" style="z-index: 18; transform: translate3d(0px, 0px, 0px) scale(1);"><img alt="" src="https://a.tile.openstreetmap.org/6/37/23.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(-21px, -227px, 0px); opacity: 1;"><img alt="" src="https://b.tile.openstreetmap.org/6/38/23.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(235px, -227px, 0px); opacity: 1;"><img alt="" src="https://b.tile.openstreetmap.org/6/37/24.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(-21px, 29px, 0px); opacity: 1;"><img alt="" src="https://c.tile.openstreetmap.org/6/38/24.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(235px, 29px, 0px); opacity: 1;"></div></div></div><div class="leaflet-pane leaflet-overlay-pane"></div><div class="leaflet-pane leaflet-shadow-pane"></div><div class="leaflet-pane leaflet-marker-pane"></div><div class="leaflet-pane leaflet-tooltip-pane"></div><div class="leaflet-pane leaflet-popup-pane"></div><div class="leaflet-proxy leaflet-zoom-animated" style="transform: translate3d(9687.481458px, 6206.595735px, 0px) scale(32);"></div></div><div class="leaflet-control-container"><div class="leaflet-top leaflet-left"><div class="leaflet-control-zoom leaflet-bar leaflet-control"><a class="leaflet-control-zoom-in" href="#" title="Zoom in" role="button" aria-label="Zoom in" aria-disabled="false"><span aria-hidden="true">+</span></a><a class="leaflet-control-zoom-out" href="#" title="Zoom out" role="button" aria-label="Zoom out" aria-disabled="false"><span aria-hidden="true">−</span></a></div></div><div class="leaflet-top leaflet-right"></div><div class="leaflet-bottom leaflet-left"></div><div class="leaflet-bottom leaflet-right"><div class="leaflet-control-attribution leaflet-control"><a href="https://leafletjs.com" title="A JavaScript library for interactive maps"><svg aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="12" height="8" viewBox="0 0 12 8" class="leaflet-attribution-flag"><path fill="#4C7BE1" d="M0 0h12v4H0z"></path><path fill="#FFD500" d="M0 4h12v3H0z"></path><path fill="#E0BC00" d="M0 7h12v1H0z"></path></svg> Leaflet</a> <span aria-hidden="true">|</span> © OpenStreetMap</div></div></div></div>
            <div id="map-overlay" class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-center pointer-events-none z-[1000]">
                <div class="bg-white/90 backdrop-blur-sm p-6 rounded-xl shadow-lg border border-gray-200">
                    <p class="text-gray-600 text-lg">Başlamak için bir KML dosyası yükleyin</p>
                </div>
            </div>
        </div>

        <!-- Settings & Data Panel -->
        <div class="w-full md:w-[420px] bg-white flex flex-col shadow-xl z-20 shrink-0 h-2/3 md:h-auto border-t md:border-t-0 md:border-l border-gray-300">
            
            <!-- Projeksiyon Ayarları (Gelimiş) -->
            <div class="p-4 bg-slate-50 border-b border-gray-200 space-y-3">
                <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Projeksiyon Ayarları</h3>
                
                <div class="grid grid-cols-2 gap-2">
                    <!-- Datum Seçimi -->
                    <div>
                        <label class="block text-[10px] font-semibold text-gray-600 mb-1">DATUM</label>
                        <select id="datumSelect" onchange="updateProjectionUI()" class="w-full p-2 border border-gray-300 rounded text-sm bg-white focus:ring-1 focus:ring-blue-500 outline-none">
                            <option value="WGS84">WGS84 (ITRF)</option>
                            <option value="ED50">ED50 (Türkiye)</option>
                        </select>
                    </div>

                    <!-- Sistem Seçimi -->
                    <div>
                        <label class="block text-[10px] font-semibold text-gray-600 mb-1">SİSTEM</label>
                        <select id="systemSelect" onchange="updateProjectionUI()" class="w-full p-2 border border-gray-300 rounded text-sm bg-white focus:ring-1 focus:ring-blue-500 outline-none">
                            <option value="GEO">Coğrafi (Lat/Lon)</option>
                            <option value="UTM_6">UTM (6 Derece)</option>
                            <option value="TM_3">TM (3 Derece)</option>
                        </select>
                    </div>
                </div>

                <!-- Dilim Seçimi (Dinamik) -->
                <div id="zoneContainer" class="hidden">
                    <label id="zoneLabel" class="block text-[10px] font-semibold text-gray-600 mb-1">DİLİM / DOM</label>
                    <select id="zoneSelect" onchange="refreshData()" class="w-full p-2 border border-gray-300 rounded text-sm bg-white focus:ring-1 focus:ring-blue-500 outline-none"></select>
                </div>
            </div>

            <!-- Liste Başlığı -->
            <div class="p-3 border-b border-gray-100 bg-white flex justify-between items-center shadow-sm z-10">
                <h2 class="font-semibold text-gray-700 flex items-center gap-2 text-sm">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-green-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 10h16M4 14h16M4 18h16"></path>
                    </svg>
                    Koordinat Listesi
                </h2>
                <span id="pointCount" class="text-[10px] bg-gray-100 border border-gray-200 px-2 py-0.5 rounded-full text-gray-600">0 Veri</span>
            </div>
            
            <!-- Liste Alanı -->
            <div id="coordinatesList" class="flex-1 overflow-y-auto p-4 scroller space-y-2 bg-white text-sm">
                <p class="text-xs text-gray-400 text-center mt-10">Henüz veri yüklenmedi.</p>
            </div>
            
            <!-- Alt Butonlar -->
            <div class="p-4 bg-gray-50 border-t border-gray-200 flex flex-col gap-2">
                <button onclick="downloadAsTxt()" class="w-full flex items-center justify-center gap-2 bg-green-600 hover:bg-green-700 text-white py-2.5 px-4 rounded-lg transition shadow-sm text-sm font-semibold">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4-4m0 0l-4 4m4-4v12"></path>
                    </svg>
                    TXT İndir (Seçili Format)
                </button>
                <div class="grid grid-cols-2 gap-2">
                    <button onclick="copyToClipboard('formatted')" class="text-xs text-gray-600 bg-white border border-gray-300 hover:bg-gray-50 py-2 rounded transition">
                        Seçiliyi Kopyala
                    </button>
                    <button onclick="copyToClipboard('raw')" class="text-xs text-blue-600 bg-white border border-blue-200 hover:bg-blue-50 py-2 rounded transition">
                        Ham Veriyi Kopyala
                    </button>
                </div>
            </div>
        </div>

    </main>

    <script>
        // --- PROJEKSİYON YÖNETİMİ ---

        // Türkiye için gerekli projeksiyon tanımlarını dinamik oluşturacağız.
        // ED50 -> WGS84 dönüşümü için yaklaşık 7 parametre (Türkiye Ortalaması)
        // Kaynak: Yaygın kullanılan parametreler (-87, -98, -121...)
        const ED50_PARAMS = "+ellps=intl +towgs84=-87,-98,-121,0,0,0,0 +units=m +no_defs";
        const WGS84_PARAMS = "+datum=WGS84 +no_defs";

        // HTML Elemanları
        const datumSelect = document.getElementById('datumSelect');
        const systemSelect = document.getElementById('systemSelect');
        const zoneSelect = document.getElementById('zoneSelect');
        const zoneContainer = document.getElementById('zoneContainer');
        const zoneLabel = document.getElementById('zoneLabel');

        // Sayfa yüklendiğinde arayüzü hazırla
        window.onload = function() {
            updateProjectionUI();
        };

        function updateProjectionUI() {
            const system = systemSelect.value;
            const currentZone = zoneSelect.value; // Mevcut seçimi korumaya çalış

            zoneSelect.innerHTML = ""; // Temizle

            if (system === 'GEO') {
                zoneContainer.classList.add('hidden');
            } else {
                zoneContainer.classList.remove('hidden');
                
                if (system === 'UTM_6') {
                    zoneLabel.textContent = "UTM ZON (6 DERECE)";
                    // Türkiye Zonları: 35, 36, 37, 38
                    [35, 36, 37, 38].forEach(z => {
                        let opt = document.createElement('option');
                        opt.value = z;
                        opt.text = `Zone ${z} (${(z*6)-3}° - ${(z*6)+3}°)`;
                        zoneSelect.add(opt);
                    });
                    // Varsayılan olarak Ankara (36) seçelim veya eskisini koruyalım
                    if(currentZone >= 35 && currentZone <= 38) zoneSelect.value = currentZone;
                    else zoneSelect.value = "36";

                } else if (system === 'TM_3') {
                    zoneLabel.textContent = "DİLİM ORTA MERİDYENİ (DOM - 3 DERECE)";
                    // Türkiye DOM'ları: 27, 30, 33, 36, 39, 42, 45
                    [27, 30, 33, 36, 39, 42, 45].forEach(dom => {
                        let opt = document.createElement('option');
                        opt.value = dom;
                        opt.text = `DOM ${dom} (Dilim ${dom/3}?)`; // Dilim numarası bazen DOM/3 olabiliyor ama DOM kullanımı daha yaygın.
                        zoneSelect.add(opt);
                    });
                    // Varsayılan DOM 30
                    if([27, 30, 33, 36, 39, 42, 45].includes(parseInt(currentZone))) zoneSelect.value = currentZone;
                    else zoneSelect.value = "30";
                }
            }
            refreshData();
        }

        // Seçilen ayarlara göre Proj4 string'i üret
        function getCurrentProjString() {
            const datum = datumSelect.value;
            const system = systemSelect.value;
            const zone = zoneSelect.value;

            let baseParams = (datum === 'ED50') ? ED50_PARAMS : WGS84_PARAMS;

            if (system === 'GEO') {
                // Sadece Datum farkı varsa (Lat/Lon)
                if (datum === 'ED50') return `+proj=longlat ${baseParams}`;
                return `+proj=longlat +datum=WGS84 +no_defs`; // Varsayılan
            } 
            else if (system === 'UTM_6') {
                return `+proj=utm +zone=${zone} ${baseParams}`;
            } 
            else if (system === 'TM_3') {
                // TM 3 Derece (Genelde k=1.0 alınır, UTM'deki 0.9996 yerine)
                // False Easting = 500,000
                return `+proj=tmerc +lat_0=0 +lon_0=${zone} +k=1 +x_0=500000 +y_0=0 ${baseParams}`;
            }
        }

        function refreshData() {
            if (parsedData.length > 0) updateListUI();
        }

        // --- HARİTA VE DOSYA İŞLEMLERİ ---
        
        const map = L.map('map').setView([39.9334, 32.8597], 6);
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; OpenStreetMap'
        }).addTo(map);

        let geoLayer = null; 
        let parsedData = []; 

        const fileInput = document.getElementById('fileInput');
        const fileNameDisplay = document.getElementById('fileName');
        const mapOverlay = document.getElementById('map-overlay');
        const listContainer = document.getElementById('coordinatesList');
        const pointCountDisplay = document.getElementById('pointCount');

        fileInput.addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (!file) return;

            fileNameDisplay.textContent = file.name;
            const reader = new FileReader();
            reader.onload = function(e) { parseKML(e.target.result); };
            reader.readAsText(file);
        });

        function parseKML(xmlString) {
            const parser = new DOMParser();
            const xmlDoc = parser.parseFromString(xmlString, "text/xml");

            if (geoLayer) map.removeLayer(geoLayer);
            listContainer.innerHTML = '';
            parsedData = [];
            mapOverlay.style.display = 'none';

            geoLayer = L.featureGroup().addTo(map);
            const placemarks = xmlDoc.getElementsByTagName("Placemark");
            
            if (placemarks.length === 0) return alert("Placemark bulunamadı.");

            for (let i = 0; i < placemarks.length; i++) {
                const p = placemarks[i];
                const name = getTagValue(p, "name") || `Nokta #${i+1}`;
                processGeometry(p, name);
            }

            if (parsedData.length > 0) {
                const bounds = geoLayer.getBounds();
                if (bounds.isValid()) map.fitBounds(bounds, { padding: [50, 50] });
                updateListUI();
            } else {
                alert("Koordinat bulunamadı.");
            }
        }

        function getTagValue(parent, tagName) {
            const tag = parent.getElementsByTagName(tagName)[0];
            return tag ? tag.textContent.trim() : null;
        }

        function processGeometry(placemark, name) {
            // Point
            const point = placemark.getElementsByTagName("Point")[0];
            if (point) {
                const [lon, lat] = parseFirstCoord(point);
                L.marker([lat, lon]).bindPopup(`<b>${name}</b>`).addTo(geoLayer);
                parsedData.push({ type: 'Nokta', name, lat: lat, lon: lon });
            }
            // LineString
            const line = placemark.getElementsByTagName("LineString")[0];
            if (line) {
                const latLngs = parseAllCoords(line);
                L.polyline(latLngs, { color: 'blue' }).bindPopup(`<b>${name}</b>`).addTo(geoLayer);
                parsedData.push({ type: 'Yol', name, lat: latLngs[0][0], lon: latLngs[0][1], count: latLngs.length });
            }
            // Polygon
            const poly = placemark.getElementsByTagName("Polygon")[0];
            if (poly) {
                const outer = poly.getElementsByTagName("outerBoundaryIs")[0];
                if(outer) {
                    const latLngs = parseAllCoords(outer);
                    L.polygon(latLngs, { color: 'red', fillColor: '#f03', fillOpacity: 0.3 }).bindPopup(`<b>${name}</b>`).addTo(geoLayer);
                    parsedData.push({ type: 'Alan', name, lat: latLngs[0][0], lon: latLngs[0][1], count: latLngs.length });
                }
            }
        }

        function parseFirstCoord(el) {
            const raw = el.getElementsByTagName("coordinates")[0].textContent.trim();
            const parts = raw.split(',').map(Number); // lon, lat
            return [parts[0], parts[1]];
        }

        function parseAllCoords(el) {
            const raw = el.getElementsByTagName("coordinates")[0].textContent.trim();
            return raw.split(/\s+/).map(pair => {
                const parts = pair.split(',');
                if (parts.length >= 2) return [parseFloat(parts[1]), parseFloat(parts[0])]; // lat, lon
                return null;
            }).filter(c => c);
        }

        // --- DÖNÜŞÜM VE UI ---

        function getTransformed(lat, lon) {
            const targetDef = getCurrentProjString();
            const system = systemSelect.value;
            const datum = datumSelect.value;

            // Kaynak her zaman WGS84 (KML standardı)
            // proj4(source, dest, coordinates)
            // Source: WGS84
            const result = proj4(proj4.defs('EPSG:4326'), targetDef, [lon, lat]);

            let x = result[0];
            let y = result[1];
            
            // Eğer sistem GEO ise X=Lon, Y=Lat olur, etiketleri düzeltelim
            if (system === 'GEO') {
                // ED50 Coğrafi seçilirse sıra değişebilir ama genelde lon, lat döner
                // Biz kullanıcıya Lat, Lon gösterelim
                return { x: y, y: x, labelX: 'Enlem', labelY: 'Boylam', isMetric: false };
            }

            return { x: x, y: y, labelX: 'Sağa (Y)', labelY: 'Yukarı (X)', isMetric: true };
        }

        function updateListUI() {
            pointCountDisplay.textContent = `${parsedData.length} Öğe`;
            
            let html = '';
            parsedData.forEach((data, index) => {
                const t = getTransformed(data.lat, data.lon);
                
                let val1 = t.isMetric ? t.x.toFixed(2) : t.x.toFixed(7);
                let val2 = t.isMetric ? t.y.toFixed(2) : t.y.toFixed(7);

                html += `
                    <div class="bg-gray-50 border border-gray-200 rounded p-2 hover:bg-blue-50 cursor-pointer" onclick="zoomToItem(${index})">
                        <div class="flex justify-between items-center mb-1">
                            <span class="font-bold text-gray-700 truncate w-32">${data.name}</span>
                            <span class="text-[10px] uppercase text-gray-400 bg-white px-1 border rounded">${data.type}</span>
                        </div>
                        <div class="grid grid-cols-2 gap-2 text-xs font-mono text-gray-600">
                            <div><span class="text-gray-400">${t.labelX}:</span> ${val1}</div>
                            <div><span class="text-gray-400">${t.labelY}:</span> ${val2}</div>
                        </div>
                    </div>
                `;
            });
            listContainer.innerHTML = html;
        }

        function zoomToItem(index) {
            const layers = geoLayer.getLayers();
            if (layers[index]) {
                const layer = layers[index];
                if (layer.getBounds) map.fitBounds(layer.getBounds());
                else map.setView(layer.getLatLng(), 15);
                layer.openPopup();
            }
        }

        function downloadAsTxt() {
            if(parsedData.length === 0) return alert("Veri yok.");
            
            let content = "";
            parsedData.forEach((data, index) => {
                const t = getTransformed(data.lat, data.lon);
                // Sade format: SIRA X Y
                let val1 = t.isMetric ? t.x.toFixed(3) : t.x.toFixed(8);
                let val2 = t.isMetric ? t.y.toFixed(3) : t.y.toFixed(8);
                content += `${index + 1} ${val1} ${val2}\n`;
            });

            saveFile(content, "txt");
        }

        function saveFile(content, ext) {
            const blob = new Blob([content], { type: 'text/plain;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            
            const d = datumSelect.value;
            const s = systemSelect.value;
            const z = zoneSelect.value;
            const info = (s === 'GEO') ? `${d}_Geo` : `${d}_${s}_${z}`;
            
            link.href = url;
            link.download = `koordinat_${info}_${new Date().toISOString().slice(0,10)}.${ext}`;
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        function copyToClipboard(mode) {
            if(parsedData.length === 0) return;
            
            let text = "";
            if (mode === 'raw') {
                text = JSON.stringify(parsedData, null, 2);
            } else {
                parsedData.forEach((data, index) => {
                    const t = getTransformed(data.lat, data.lon);
                    text += `${index+1}\t${t.x}\t${t.y}\n`;
                });
            }
            
            const ta = document.createElement("textarea");
            ta.value = text;
            document.body.appendChild(ta);
            ta.select();
            document.execCommand('copy');
            document.body.removeChild(ta);
            alert(mode === 'raw' ? "Ham veriler (WGS84) kopyalandı." : "Dönüştürülmüş veriler kopyalandı.");
        }
    </script>

</body></html>