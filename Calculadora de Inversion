<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Calculadora de Interés Compuesto</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <!-- Librerías para exportación -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.25/jspdf.plugin.autotable.min.js"></script>
  <script src="https://cdn.sheetjs.com/xlsx-0.19.3/package/dist/xlsx.full.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <style>
    :root {
      --fondo-claro: #f4f6f8;
      --texto-claro: #333;
      --primario: #2b6777;
      --secundario: #52ab98;
      --terciario: #c8d8e4;
      --hover: #1b4d5b;
      --boton-texto: #fff;
      --verde: #28a745;
      --verde-hover: #218838;
    }
  
    body.dark {
      --fondo-claro: #121212;
      --texto-claro: #e0e0e0;
      --primario: #3a9cb8;
      --secundario: #2d8273;
      --terciario: #5a6d80;
    }
  
    body {
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
      background-color: var(--fondo-claro);
      color: var(--texto-claro);
      padding: 15px;
      max-width: 1200px;
      margin: 0 auto;
      transition: background-color 0.4s, color 0.4s;
      font-size: 15px;
      line-height: 1.6;
      -webkit-text-size-adjust: 100%;
    }

    /* Logo hero */
    .logo-hero {
      width: 100%;
      max-width: 1200px;
      margin: 0 auto 30px;
      padding: 20px;
      display: flex;
      justify-content: center;
      align-items: center;
      background: transparent;
    }
    
    .hero-logo {
      width: 90%;
      max-width: 1000px;
      height: auto;
      object-fit: contain;
      border-radius: 20px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
      transition: all 0.3s ease;
      border: 1px solid rgba(0, 0, 0, 0.1);
    }
    
    body.dark .hero-logo {
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
      border-color: rgba(255, 255, 255, 0.1);
    }
    
    .hero-logo:hover {
      transform: translateY(-3px);
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
    }

    /* Botones de exportación */
    .export-buttons {
      display: flex;
      gap: 15px;
      margin: 20px 0;
    }
    
    .export-btn {
      padding: 12px 20px;
      border: none;
      border-radius: 8px;
      font-weight: 600;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 8px;
      transition: all 0.3s ease;
      font-size: 0.9rem;
      width: 100%;
      justify-content: center;
    }
    
    .pdf-btn {
      background-color: #e74c3c;
      color: white;
    }
    
    .pdf-btn:hover {
      background-color: #c0392b;
      transform: translateY(-2px);
    }
    
    .excel-btn {
      background-color: #2ecc71;
      color: white;
    }
    
    .excel-btn:hover {
      background-color: #27ae60;
      transform: translateY(-2px);
    }

    /* Estilos mejorados para tooltips */
    .tooltip-container {
      position: relative;
      display: inline-block;
      margin-left: 5px;
    }
    
    .tooltip-icon {
      color: var(--primario);
      cursor: help;
      font-size: 0.9rem;
      touch-action: manipulation;
    }
    
    .tooltip-text {
      visibility: hidden;
      width: 200px;
      background-color: var(--primario);
      color: white;
      text-align: left;
      border-radius: 6px;
      padding: 10px;
      position: absolute;
      z-index: 1000;
      bottom: 125%;
      left: 50%;
      transform: translateX(-50%);
      opacity: 0;
      transition: opacity 0.3s;
      font-size: 0.8rem;
      font-weight: normal;
      line-height: 1.4;
      box-shadow: 0 2px 10px rgba(0,0,0,0.2);
      word-wrap: break-word;
      white-space: normal;
    }
    
    body.dark .tooltip-text {
      background-color: var(--secundario);
    }
    
    .tooltip-container:hover .tooltip-text,
    .tooltip-container:focus .tooltip-text {
      visibility: visible;
      opacity: 1;
    }

    /* Estilos específicos para tooltips en móviles */
    @media (max-width: 768px) {
      .tooltip-text {
        width: 180px;
        font-size: 0.75rem;
        bottom: auto;
        top: 100%;
        left: 50%;
        transform: translateX(-50%);
        margin-top: 8px;
        max-width: 80vw;
      }
      
      .tooltip-container .tooltip-text.right {
        left: auto;
        right: 0;
        transform: none;
      }
      
      .tooltip-container .tooltip-text.left {
        left: 0;
        transform: none;
      }
    }
  
    .calculadora-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 15px;
    }
  
    .input-card, .result-card {
      background: white;
      border-radius: 8px;
      padding: 15px;
      margin-bottom: 15px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.05);
      border: 1px solid #e0e0e0;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    
    .input-card:hover, .result-card:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
  
    body.dark .input-card,
    body.dark .result-card,
    body.dark .chart-container,
    body.dark .table-wrapper {
      background: #1e1e1e;
      box-shadow: 0 2px 12px rgba(0,0,0,0.1);
      border-color: #333;
    }
  
    .input-card h3, .result-card h3 {
      margin-top: 0;
      color: var(--primario);
      padding-bottom: 6px;
      margin-bottom: 12px;
      font-size: 1.1rem;
      display: flex;
      align-items: center;
      gap: 6px;
      font-weight: 500;
      letter-spacing: 0.2px;
    }
  
    .input-card h3 i {
      font-size: 1rem;
    }
  
    .input-group {
      margin-bottom: 12px;
    }
  
    .input-group label {
      display: block;
      margin-bottom: 4px;
      font-weight: 500;
      font-size: 0.9rem;
    }
  
    input, select {
      width: 100%;
      padding: 10px 12px;
      border: 1px solid #ddd;
      border-radius: 6px;
      background-color: #fff;
      transition: all 0.3s;
      font-size: 0.95rem;
      -webkit-appearance: none;
    }
  
    body.dark input,
    body.dark select {
      background-color: #2a2a2a;
      color: #e0e0e0;
      border-color: #555;
    }
  
    /* Estilos para el resumen tipo infografía */
    .summary-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
      margin-top: 15px;
    }
    
    .summary-item {
      background: white;
      border-radius: 8px;
      padding: 15px;
      display: flex;
      align-items: center;
      gap: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.05);
      border-left: 4px solid var(--primario);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    
    body.dark .summary-item {
      background: #2a2a2a;
      box-shadow: 0 2px 12px rgba(0,0,0,0.1);
    }
    
    .summary-item:hover {
      transform: translateY(-3px);
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
    
    .summary-item.total {
      border-left-color: var(--verde);
      background-color: rgba(40, 167, 69, 0.05);
    }
    
    body.dark .summary-item.total {
      background-color: rgba(40, 167, 69, 0.1);
    }
    
    .summary-icon {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background-color: var(--terciario);
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--primario);
      font-size: 1.1rem;
      flex-shrink: 0;
    }
    
    body.dark .summary-icon {
      background-color: #3a3a3a;
    }
    
    .summary-item.total .summary-icon {
      background-color: rgba(40, 167, 69, 0.2);
      color: var(--verde);
    }
    
    .summary-content {
      flex-grow: 1;
    }
    
    .summary-label {
      font-size: 0.85rem;
      color: #666;
      margin-bottom: 5px;
    }
    
    body.dark .summary-label {
      color: #aaa;
    }
    
    .summary-value {
      font-size: 1.1rem;
      font-weight: 600;
      color: var(--texto-claro);
    }
    
    .summary-item.total .summary-value {
      color: var(--verde);
      font-size: 1.2rem;
    }
  
    .chart-container {
      background: white;
      padding: 15px;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.05);
      height: 300px;
      margin-bottom: 15px;
      border: 1px solid #e0e0e0;
    }
  
    canvas {
      width: 100% !important;
      height: 100% !important;
    }
  
    .dark-mode-btn {
      position: fixed;
      top: 20px;
      right: 20px;
      z-index: 1000;
      background-color: #2b2b2b;
      color: white;
      border: none;
      padding: 8px 16px;
      border-radius: 6px;
      cursor: pointer;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      font-size: 0.85rem;
      display: flex;
      align-items: center;
      gap: 4px;
      letter-spacing: 0.5px;
      text-transform: uppercase;
      font-weight: 500;
      transition: all 0.3s;
    }
    
    body.dark .dark-mode-btn {
      background-color: #f0f0f0;
      color: #2b2b2b;
    }
  
    .dark-mode-btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    }
  
    .whatsapp-btn {
      position: fixed;
      bottom: 20px;
      right: 20px;
      z-index: 999;
      background-color: #25D366;
      color: white;
      width: 50px;
      height: 50px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
      transition: all 0.3s;
    }
  
    .whatsapp-btn:hover {
      background-color: #128C7E;
      transform: scale(1.1);
    }
  
    .whatsapp-btn i {
      font-size: 25px;
    }
  
    .results-table-container {
      margin-top: 15px;
    }
    
    .table-wrapper {
      overflow-x: auto;
      max-height: 250px;
      overflow-y: auto;
      margin-top: 12px;
      border-radius: 6px;
      box-shadow: 0 1px 2px rgba(0,0,0,0.1);
      -webkit-overflow-scrolling: touch;
      border: 1px solid #e0e0e0;
    }
    
    #tablaResultados {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.85rem;
    }
    
    #tablaResultados th, 
    #tablaResultados td {
      padding: 10px 12px;
      text-align: right;
      border-bottom: 1px solid #eee;
    }
    
    #tablaResultados th {
      background-color: var(--primario);
      color: white;
      position: sticky;
      top: 0;
      text-align: center;
      font-size: 0.85rem;
      font-weight: 500;
    }
    
    #tablaResultados tr:nth-child(even) {
      background-color: #f9f9f9;
    }
    
    #tablaResultados tr:hover {
      background-color: #f1f1f1;
    }
    
    body.dark #tablaResultados th {
      background-color: var(--secundario);
    }
    
    body.dark #tablaResultados tr:nth-child(even) {
      background-color: #2a2a2a;
    }
    
    body.dark #tablaResultados tr:hover {
      background-color: #333;
    }
    
    body.dark #tablaResultados th, 
    body.dark #tablaResultados td {
      border-color: #444;
    }
  
    /* Estilos para select */
    select {
      background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='currentColor' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
      background-repeat: no-repeat;
      background-position: right 10px center;
      background-size: 1em;
    }
    
    body.dark select {
      background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23e0e0e0' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
    }
    
    /* Mensajes de error */
    .error-mensaje {
      color: #dc3545 !important;
      font-size: 0.8rem;
      margin-top: 5px;
    }
    
    body.dark .error-mensaje {
      color: #ff6b6b !important;
    }
    
    .warning-message {
      background-color: #fff3cd;
      color: #856404;
      padding: 10px;
      border-radius: 4px;
      margin-bottom: 15px;
      font-size: 0.9rem;
    }
    
    body.dark .warning-message {
      background-color: #343a40;
      color: #ffeeba;
    }
    
    /* Estilos para las preguntas frecuentes */
    .faq-item {
      margin-bottom: 10px;
      border-radius: 6px;
      overflow: hidden;
      border: 1px solid #e0e0e0;
    }
    
    body.dark .faq-item {
      border-color: #444;
    }
    
    .faq-question {
      width: 100%;
      padding: 12px 15px;
      text-align: left;
      background-color: var(--terciario);
      border: none;
      cursor: pointer;
      font-weight: 500;
      font-size: 0.95rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      transition: background-color 0.3s;
    }
    
    body.dark .faq-question {
      background-color: #3a3a3a;
    }
    
    .faq-question:hover {
      background-color: #d0d8e0;
    }
    
    body.dark .faq-question:hover {
      background-color: #4a4a4a;
    }
    
    .faq-question::after {
      content: '+';
      font-size: 1.2rem;
      transition: transform 0.3s;
    }
    
    .faq-question.active::after {
      content: '-';
    }
    
    .faq-answer {
      padding: 0;
      max-height: 0;
      overflow: hidden;
      transition: max-height 0.3s ease-out, padding 0.3s ease;
      background-color: white;
    }
    
    body.dark .faq-answer {
      background-color: #1e1e1e;
    }
    
    .faq-answer.show {
      padding: 15px;
      max-height: 1000px;
    }
    
    .faq-answer p {
      margin-top: 0;
      margin-bottom: 10px;
    }
    
    /* Responsive para pantallas más grandes */
    @media (min-width: 768px) {
      .calculadora-grid {
        grid-template-columns: 1.1fr 2fr;
      }
      
      .chart-container {
        height: 400px;
      }
      
      .export-buttons {
        flex-direction: row;
      }
    }
    
    /* Ajustes para móviles */
    @media (max-width: 768px) {
      body {
        padding: 10px;
        min-width: 100%;
        overflow-x: hidden;
      }
      
      .calculadora-grid {
        display: flex;
        flex-direction: column;
        gap: 10px;
      }
      
      .input-card, .result-card, .chart-container {
        width: 100%;
        box-sizing: border-box;
        margin-left: 0;
        margin-right: 0;
      }
      
      /* Ajuste para la tabla */
      .table-wrapper {
        width: 100%;
        overflow-x: auto;
        -webkit-overflow-scrolling: touch;
        display: block;
      }
      
      #tablaResultados {
        min-width: 600px;
      }
      
      /* Ajuste para el gráfico */
      .chart-container {
        height: 300px;
        padding: 10px;
      }
      
      /* Mejor disposición de los elementos de resumen */
      .summary-grid {
        grid-template-columns: 1fr 1fr;
        gap: 10px;
      }
      
      /* Ajuste para inputs */
      .input-group input, 
      .input-group select {
        font-size: 16px;
        padding: 12px;
      }
      
      /* Botones de exportación */
      .export-buttons {
        flex-direction: column;
      }
      
      .export-btn {
        width: 100%;
        margin-bottom: 10px;
      }
      
      /* Logo hero */
      .hero-logo {
        width: 100%;
        border-radius: 10px;
        margin-bottom: 15px;
      }
      
      /* FAQ responsive */
      .faq-item {
        margin-bottom: 8px;
      }
      
      .faq-question {
        padding: 10px;
        font-size: 0.9rem;
      }
    }

    /* Ajustes específicos para pantallas muy pequeñas (menos de 480px) */
    @media (max-width: 480px) {
      .summary-grid {
        grid-template-columns: 1fr;
      }
      
      .input-card, .result-card {
        padding: 12px;
      }
      
      .chart-container {
        height: 250px;
      }
      
      /* Reducir padding en móviles pequeños */
      body {
        padding: 8px;
      }
      
      /* Ajustar tamaño de fuente en inputs */
      input, select {
        font-size: 14px;
      }

      /* Estilos específicos para la tabla en móviles pequeños */
      #tablaResultados th, 
      #tablaResultados td {
        padding: 6px 4px;
        font-size: 12px;
      }
      
      #tablaResultados th {
        font-size: 11px;
        padding: 8px 4px;
      }
      
      .table-wrapper {
        -webkit-overflow-scrolling: touch;
        border: 1px solid #e0e0e0;
        border-radius: 6px;
        box-shadow: 0 1px 3px rgba(0,0,0,0.1);
      }
      
      body.dark .table-wrapper {
        border-color: #444;
      }
    }

    /* Prevenir desbordamiento horizontal en todos los elementos */
    * {
      max-width: 100%;
      box-sizing: border-box;
    }
    
    /* Asegurar que el contenedor principal no cause overflow */
    .calculadora-grid {
      width: 100%;
      overflow: hidden;
    }
  </style>
</head>
<body>
  <button class="dark-mode-btn" onclick="toggleDarkMode()"><i class="fas fa-moon"></i> Modo Oscuro</button>

  <!-- Logo hero -->
  <div class="logo-hero">
    <img src="ROBPAIERO_TUASESORDECONFIANZA.PNG" alt="Logo Roberto Palero" class="hero-logo">
  </div>

  <div class="calculadora-grid">
    <!-- Columna izquierda - Inputs -->
    <div class="input-section">
      <div class="input-card">
        <h3><i class="fas fa-coins"></i> Depósito inicial
          <div class="tooltip-container">
            <i class="fas fa-question-circle tooltip-icon"></i>
            <span class="tooltip-text">¿Con qué cantidad vas a comenzar tu inversión?</span>
          </div>
        </h3>
        <div class="input-group">
          <input type="text" id="capitalInicial" placeholder="$0">
        </div>
        <div class="input-group">
          <label for="tasa">Tasa de interés anual (%):
            <div class="tooltip-container">
              <i class="fas fa-question-circle tooltip-icon"></i>
              <span class="tooltip-text">Tasa de rendimiento anual que ofrece la institución financiera</span>
            </div>
          </label>
          <input type="number" id="tasa" step="0.01" placeholder="0">
        </div>
      </div>

      <div class="input-card">
        <h3><i class="far fa-calendar-alt"></i> Plazo para Invertir
          <div class="tooltip-container">
            <i class="fas fa-question-circle tooltip-icon"></i>
            <span class="tooltip-text">Periodo de tiempo que mantendrás tu inversión</span>
          </div>
        </h3>
        <div class="input-group">
          <label for="tipoPlazo">Tipo de plazo:</label>
          <select id="tipoPlazo">
            <option value="mensual">Periodo en Meses</option>
            <option value="anual">Periodo en Años</option>
          </select>
        </div>
        <div class="input-group">
          <label id="labelPlazo" for="plazo">Cantidad de años:
            <div class="tooltip-container">
              <i class="fas fa-question-circle tooltip-icon"></i>
              <span class="tooltip-text">Horizonte de tiempo para tu inversión</span>
            </div>
          </label>
          <input type="number" id="plazo" min="1" placeholder="0">
        </div>
        <div class="input-group">
          <label for="frecuencia">Frecuencia de capitalización:
            <div class="tooltip-container">
              <i class="fas fa-question-circle tooltip-icon"></i>
              <span class="tooltip-text">Con qué frecuencia se reinvertirán los intereses</span>
            </div>
          </label>
          <select id="frecuencia">
            <option value="12" selected>Mensual</option>
            <option value="4">Trimestral</option>
            <option value="2">Semestral</option>
            <option value="1">Anual</option>
          </select>
        </div>
      </div>

      <div class="input-card">
        <h3><i class="fas fa-hand-holding-usd"></i> Aportaciones adicionales
          <div class="tooltip-container">
            <i class="fas fa-question-circle tooltip-icon"></i>
            <span class="tooltip-text">Depósitos periódicos adicionales a tu inversión inicial</span>
          </div>
        </h3>
        <div class="input-group">
          <label for="aportacion">Monto:
            <div class="tooltip-container">
              <i class="fas fa-question-circle tooltip-icon"></i>
              <span class="tooltip-text">Cantidad que aportarás periódicamente</span>
            </div>
          </label>
          <input type="text" id="aportacion" placeholder="$0">
        </div>
        <div class="input-group">
          <label for="frecuenciaAportacion">Frecuencia de aportación:
            <div class="tooltip-container">
              <i class="fas fa-question-circle tooltip-icon"></i>
              <span class="tooltip-text">Con qué frecuencia realizarás aportaciones</span>
            </div>
          </label>
          <select id="frecuenciaAportacion">
            <option value="12" selected>Mensualmente</option>
            <option value="6">Bimestralmente</option>
            <option value="4">Trimestral</option>
            <option value="2">Semestral</option>
            <option value="1">Anualmente</option>
          </select>
        </div>
        
        <!-- Botones de exportación movidos aquí -->
        <div class="export-buttons">
          <button onclick="exportToPDF()" class="export-btn pdf-btn">
            <i class="fas fa-file-pdf"></i> Exportar a PDF
          </button>
          <button onclick="exportToExcel()" class="export-btn excel-btn">
            <i class="fas fa-file-excel"></i> Exportar a Excel
          </button>
        </div>
      </div>
    </div>

    <!-- Columna derecha - Resultados -->
    <div class="results-section">
      <div class="result-card">
        <h3><i class="fas fa-chart-pie"></i> Resumen de inversión</h3>
        <div class="summary-grid">
          <div class="summary-item">
            <div class="summary-icon">
              <i class="fas fa-piggy-bank"></i>
            </div>
            <div class="summary-content">
              <div class="summary-label">Depósito inicial</div>
              <div class="summary-value" id="res-inicial">$0.00</div>
            </div>
          </div>
          
          <div class="summary-item">
            <div class="summary-icon">
              <i class="fas fa-hand-holding-usd"></i>
            </div>
            <div class="summary-content">
              <div class="summary-label">Depósitos adicionales</div>
              <div class="summary-value" id="res-aportaciones">$0.00</div>
            </div>
          </div>
          
          <div class="summary-item">
            <div class="summary-icon">
              <i class="fas fa-chart-line"></i>
            </div>
            <div class="summary-content">
              <div class="summary-label">Interés acumulado</div>
              <div class="summary-value" id="res-intereses">$0.00</div>
            </div>
          </div>
          
          <div class="summary-item total">
            <div class="summary-icon">
              <i class="fas fa-coins"></i>
            </div>
            <div class="summary-content">
              <div class="summary-label">Total acumulado</div>
              <div class="summary-value" id="res-total">$0.00</div>
            </div>
          </div>
        </div>
      </div>

      <div class="chart-container">
        <canvas id="graficaBarras"></canvas>
      </div>
      
      <!-- Tabla de resultados detallados -->
      <div class="results-table-container">
        <div class="input-card">
          <h3><i class="fas fa-table"></i> Tabla Amortizada de Inversion</h3>
          <div class="table-wrapper">
            <table id="tablaResultados">
              <thead>
                <tr>
                  <th>Periodo</th>
                  <th>Depósito inicial</th>
                  <th>Aportaciones</th>
                  <th>Intereses</th>
                  <th>Total acumulado</th>
                </tr>
              </thead>
              <tbody>
                <!-- Aquí se insertarán las filas dinámicamente -->
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Sección de Preguntas Frecuentes -->
  <div class="faq-section" style="margin-top: 40px; margin-bottom: 60px;">
    <div class="input-card">
      <h3><i class="fas fa-question-circle"></i> Preguntas frecuentes</h3>
      
      <!-- Pregunta 1 - Actualizada -->
      <div class="faq-item">
        <button class="faq-question">¿Qué es y cómo funciona la frecuencia anual de interés?</button>
        <div class="faq-answer">
          <p>Número de veces al año que se agrega el interés al capital (interés compuesto), ejemplos:</p>
          
          <div class="table-wrapper" style="margin-top: 15px;">
            <table style="width: 100%; border-collapse: collapse;">
              <thead>
                <tr>
                  <th style="padding: 10px; background-color: var(--primario); color: white; text-align: left;">Tipo de interés</th>
                  <th style="padding: 10px; background-color: var(--primario); color: white; text-align: left;">Tiempo</th>
                  <th style="padding: 10px; background-color: var(--primario); color: white; text-align: left;">Repeticiones al año</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Anual</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Genera interés una vez al año.</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">1</td>
                </tr>
                <tr>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Mensual</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Genera interés cada mes.</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">12</td>
                </tr>
                <tr>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Quincenal</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Genera interés cada quince días.</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">24</td>
                </tr>
                <tr>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Semanal</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Genera interés cada 7 días.</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">52</td>
                </tr>
                <tr>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Diario</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Genera interés cada día.</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">365</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
      
      <!-- Pregunta 2 se mantiene igual -->
      <div class="faq-item">
        <button class="faq-question">¿Cómo funcionan las aportaciones adicionales?</button>
        <div class="faq-answer">
          <p>Son aportaciones adicionales al capital inicial. La frecuencia de estos depósitos será la misma que la que elijas en "Frecuencia anual de interés compuesto".
             Por ejemplo, si decides hacer depósitos adicionales de $100 y seleccionas una frecuencia mensual, estarás agregando $100 cada mes a tu inversión.:</p>
          
          <div class="table-wrapper" style="margin-top: 15px;">
            <table style="width: 100%; border-collapse: collapse;">
              <thead>
                <tr>
                  <th style="padding: 10px; background-color: var(--primario); color: white; text-align: left;">Tipo de interés</th>
                  <th style="padding: 10px; background-color: var(--primario); color: white; text-align: left;">Tiempo</th>
                  <th style="padding: 10px; background-color: var(--primario); color: white; text-align: left;">Total depositado al año</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Anual</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Genera interés una vez al año.</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">1 X 100 = $100 anuales</td>
                </tr>
                <tr>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Mensual</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Genera interés cada mes.</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">12 X 100 = $1,200 anuales</td>
                </tr>
                <tr>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Quincenal</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Genera interés cada quince días.</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">24 X 100 = $2,400 anuales</td>
                </tr>
                <tr>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Semanal</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Genera interés cada 7 días.</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">52 X 100 = $5,200 anuales</td>
                </tr>
                <tr>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Diario</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">Genera interés cada día.</td>
                  <td style="padding: 8px; border-bottom: 1px solid #ddd;">365 X 100 = $36,500 anuales</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Botón flotante de WhatsApp -->
  <a href="https://wa.me/523324967419?text=Hola,%20me%20interesa%20saber%20m%C3%A1s%20sobre%20inversiones%20%F0%9F%92%B0%F0%9F%93%88" class="whatsapp-btn" target="_blank" title="Contactar por WhatsApp">
    <i class="fab fa-whatsapp"></i>
  </a>

  <script>
    // Variables globales
    let chartBarras = null;
    let totalAportaciones = 0;
    let totalInteres = 0;
    let capital = 0;
    const MAX_PERIODOS_TABLA = 60; // Mostrar máximo 5 años en meses

    // Inicialización
    document.addEventListener('DOMContentLoaded', function() {
      // Configura eventos de input para cálculo automático
      document.querySelectorAll('input, select').forEach(input => {
        input.addEventListener('input', calcular);
      });

      // Configura formateo de moneda
      document.getElementById('capitalInicial').addEventListener('input', function() {
        formatearMoneda(this);
      });
      
      document.getElementById('aportacion').addEventListener('input', function() {
        formatearMoneda(this);
      });

      // Cambiar label de plazo según selección
      document.getElementById('tipoPlazo').addEventListener('change', function() {
        const labelPlazo = document.getElementById('labelPlazo');
        const tooltip = labelPlazo.querySelector('.tooltip-text');
        
        if (this.value === 'mensual') {
          labelPlazo.textContent = 'Cantidad de meses:';
          tooltip.textContent = '¿Cuántos meses vas a realizar la inversión?';
          document.getElementById('plazo').placeholder = '0';
        } else {
          labelPlazo.textContent = 'Cantidad de años:';
          tooltip.textContent = '¿Cuántos años vas a realizar la inversión?';
          document.getElementById('plazo').placeholder = '0';
        }
        
        // Asegurarse de mantener el icono de tooltip
        labelPlazo.innerHTML = labelPlazo.textContent + `<div class="tooltip-container">
          <i class="fas fa-question-circle tooltip-icon"></i>
          <span class="tooltip-text">${tooltip.textContent}</span>
        </div>`;
        
        calcular();
      });

      // Funcionalidad para desplegar las respuestas de FAQ
      document.querySelectorAll('.faq-question').forEach(button => {
        button.addEventListener('click', () => {
          const faqItem = button.parentElement;
          const answer = button.nextElementSibling;
          
          // Cerrar otros items abiertos
          document.querySelectorAll('.faq-answer').forEach(item => {
            if (item !== answer && item.classList.contains('show')) {
              item.classList.remove('show');
              item.previousElementSibling.classList.remove('active');
            }
          });
          
          // Alternar el actual
          button.classList.toggle('active');
          answer.classList.toggle('show');
        });
      });

      // Configurar tooltips para móviles
      const tooltips = document.querySelectorAll('.tooltip-container');
      
      tooltips.forEach(tooltip => {
        // Manejar clicks en móviles
        tooltip.addEventListener('click', function(e) {
          e.preventDefault();
          e.stopPropagation();
          const tooltipText = this.querySelector('.tooltip-text');
          const allTooltips = document.querySelectorAll('.tooltip-text');
          
          // Cerrar otros tooltips abiertos
          allTooltips.forEach(tt => {
            if (tt !== tooltipText) {
              tt.style.visibility = 'hidden';
              tt.style.opacity = '0';
            }
          });
          
          // Alternar este tooltip
          if (tooltipText.style.visibility === 'visible') {
            tooltipText.style.visibility = 'hidden';
            tooltipText.style.opacity = '0';
          } else {
            // Ajustar posición si no cabe
            tooltipText.style.visibility = 'visible';
            tooltipText.style.opacity = '1';
            
            // Verificar posición después de mostrarlo
            setTimeout(() => {
              const rect = tooltipText.getBoundingClientRect();
              
              if (rect.bottom > window.innerHeight) {
                tooltipText.classList.add('right');
              } else if (rect.left < 0) {
                tooltipText.classList.add('left');
              } else {
                tooltipText.classList.remove('right', 'left');
              }
            }, 10);
          }
        });
      });
      
      // Cerrar tooltips al tocar fuera
      document.addEventListener('click', function(e) {
        if (!e.target.closest('.tooltip-container')) {
          const allTooltips = document.querySelectorAll('.tooltip-text');
          allTooltips.forEach(tt => {
            tt.style.visibility = 'hidden';
            tt.style.opacity = '0';
          });
        }
      });

      // Ajustar tabla para móviles
      ajustarTablaParaMoviles();
      window.addEventListener('resize', ajustarTablaParaMoviles);

      // Calcular inicialmente
      calcular();
    });

    function toggleDarkMode() {
      document.body.classList.toggle("dark");
      const icon = document.querySelector('.dark-mode-btn i');
      if (document.body.classList.contains("dark")) {
        icon.classList.remove('fa-moon');
        icon.classList.add('fa-sun');
      } else {
        icon.classList.remove('fa-sun');
        icon.classList.add('fa-moon');
      }
      if (chartBarras) {
        chartBarras.update();
      }
    }

    function formatearMoneda(input) {
      // Guardar posición del cursor
      const cursorPosition = input.selectionStart;
      
      // Eliminar todos los caracteres no numéricos excepto el punto decimal
      let valor = input.value.replace(/[^0-9.]/g, '');
      
      // Si está vacío, dejar vacío
      if(valor === '') {
        input.value = '';
        return;
      }
      
      // Convertir a número y formatear
      const numero = parseFloat(valor);
      if (isNaN(numero)) {
        input.value = '';
        return;
      }
      
      // Formatear con $ y separadores de miles
      input.value = '$' + new Intl.NumberFormat('es-MX').format(numero);
      
      // Restaurar posición del cursor, ajustando por los caracteres añadidos
      const newCursorPosition = cursorPosition + (input.value.length - valor.length);
      input.setSelectionRange(newCursorPosition, newCursorPosition);
    }

    function calcular() {
      // Limpiar mensajes de error previos
      document.querySelectorAll('.error-mensaje').forEach(el => el.remove());
      
      // Obtener valores de los inputs
      const capitalInicial = parseFloat(document.getElementById('capitalInicial').value.replace(/[^0-9.]/g, '')) || 0;
      const tasaAnual = parseFloat(document.getElementById('tasa').value) || 0;
      const tipoPlazo = document.getElementById('tipoPlazo').value;
      const plazo = parseInt(document.getElementById('plazo').value) || 0;
      const frecuencia = parseInt(document.getElementById('frecuencia').value) || 12;
      const aportacion = parseFloat(document.getElementById('aportacion').value.replace(/[^0-9.]/g, '')) || 0;
      const frecuenciaAportacion = parseInt(document.getElementById('frecuenciaAportacion').value) || 12;

      // Validaciones
      if (capitalInicial < 0) {
        mostrarError('capitalInicial', 'El depósito inicial no puede ser negativo');
        return;
      }
      
      if (tasaAnual < 0) {
        mostrarError('tasa', 'La tasa de interés no puede ser negativa');
        return;
      }
      
      if (plazo <= 0) {
        mostrarError('plazo', 'El plazo debe ser mayor a cero');
        return;
      }
      
      if (aportacion < 0) {
        mostrarError('aportacion', 'Las aportaciones no pueden ser negativas');
        return;
      }

      // Convertir plazo a años si está en meses
      const plazoAnios = tipoPlazo === 'mensual' ? plazo / 12 : plazo;
      const totalMeses = tipoPlazo === 'mensual' ? plazo : plazo * 12;

      // Calcular valores
      let resultados = [];
      capital = capitalInicial;
      totalAportaciones = 0;
      totalInteres = 0;

      const tasaPeriodica = tasaAnual / 100 / frecuencia;
      const aportacionPeriodica = aportacion;
      const aportacionesPorAnio = 12 / frecuenciaAportacion;
      const totalAportacionesPeriodos = tipoPlazo === 'mensual' ? 
        (plazo / (12 / frecuenciaAportacion)) : 
        (plazo * aportacionesPorAnio);

      // Calcular por periodo (mes o año según selección)
      const periodos = tipoPlazo === 'mensual' ? totalMeses : plazo;
      const labels = tipoPlazo === 'mensual' ? 
        Array.from({length: periodos}, (_, i) => `Mes ${i+1}`) : 
        Array.from({length: periodos}, (_, i) => `Año ${i+1}`);

      for (let i = 1; i <= periodos; i++) {
        let interesPeriodo = 0;
        let aportacionPeriodo = 0;
        
        // Si es cálculo mensual
        if (tipoPlazo === 'mensual') {
          // Calcular interés mensual (dividimos la tasa anual entre 12)
          interesPeriodo = capital * (tasaAnual / 100 / 12);
          capital += interesPeriodo;
          totalInteres += interesPeriodo;
          
          // Aportaciones según frecuencia
          if (i % (12 / frecuenciaAportacion) === 0 || frecuenciaAportacion === 12) {
            capital += aportacionPeriodica;
            aportacionPeriodo = aportacionPeriodica;
            totalAportaciones += aportacionPeriodica;
          }
        } 
        // Si es cálculo anual
        else {
          // Calcular interés anual compuesto
          for (let p = 0; p < frecuencia; p++) {
            const interes = capital * tasaPeriodica;
            capital += interes;
            interesPeriodo += interes;
          }
          totalInteres += interesPeriodo;
          
          // Aportaciones anuales según frecuencia
          if (frecuenciaAportacion === 12) {
            // Aportaciones mensuales: sumamos 12 aportaciones al año
            aportacionPeriodo = aportacionPeriodica * 12;
          } else if (frecuenciaAportacion === 6) {
            // Aportaciones bimestrales: sumamos 6 aportaciones al año
            aportacionPeriodo = aportacionPeriodica * 2;
          } else if (frecuenciaAportacion === 4) {
            // Aportaciones trimestrales: sumamos 4 aportaciones al año
            aportacionPeriodo = aportacionPeriodica * 3;
          } else if (frecuenciaAportacion === 2) {
            // Aportaciones semestrales: sumamos 2 aportaciones al año
            aportacionPeriodo = aportacionPeriodica * 6;
          } else {
            // Aportaciones anuales: solo una aportación
            aportacionPeriodo = aportacionPeriodica;
          }
          
          capital += aportacionPeriodo;
          totalAportaciones += aportacionPeriodo;
        }

        resultados.push({
          periodo: i,
          capitalInicial: i === 1 ? capitalInicial : 0,
          aportaciones: aportacionPeriodo,
          intereses: interesPeriodo,
          total: capital
        });
      }

      // Actualizar resumen
      document.getElementById('res-inicial').textContent = formatCurrency(capitalInicial);
      document.getElementById('res-aportaciones').textContent = formatCurrency(totalAportaciones);
      document.getElementById('res-intereses').textContent = formatCurrency(totalInteres);
      document.getElementById('res-total').textContent = formatCurrency(capital);

      // Limitar visualización en tabla si son muchos periodos
      if (periodos > MAX_PERIODOS_TABLA) {
        const container = document.querySelector('.results-table-container');
        const existingWarning = document.querySelector('.warning-message');
        
        if (!existingWarning) {
          const warning = document.createElement('div');
          warning.className = 'warning-message';
          warning.innerHTML = `<i class="fas fa-info-circle"></i> Se muestran solo los primeros ${MAX_PERIODOS_TABLA} periodos. Usa el gráfico para ver el comportamiento completo.`;
          container.insertBefore(warning, container.firstChild);
        }
        
        resultados = resultados.slice(0, MAX_PERIODOS_TABLA);
      }

      // Generar gráfico y tabla
      generarGraficoBarras(resultados, labels);
      generarTabla(resultados, tipoPlazo === 'mensual');
    }

    function mostrarError(inputId, mensaje) {
      const input = document.getElementById(inputId);
      const existingError = input.parentNode.querySelector('.error-mensaje');
      
      if (!existingError) {
        const error = document.createElement('div');
        error.className = 'error-mensaje';
        error.innerHTML = `<i class="fas fa-exclamation-circle"></i> ${mensaje}`;
        input.parentNode.appendChild(error);
      }
    }

    function generarGraficoBarras(datos, labels) {
      const ctx = document.getElementById('graficaBarras').getContext('2d');
      const esMovil = window.innerWidth < 768;
      
      if (chartBarras) {
        chartBarras.destroy();
      }
      
      // Preparar datos para el gráfico (modificado para mostrar depósito inicial en todos los periodos)
      const datosInicial = datos.map(() => datos[0].capitalInicial);
      
      // Calcular valores acumulativos para aportaciones e intereses
      let acumuladoAportaciones = 0;
      let acumuladoIntereses = 0;
      
      const datosAportaciones = datos.map(item => {
        acumuladoAportaciones += item.aportaciones;
        return acumuladoAportaciones;
      });
      
      const datosIntereses = datos.map(item => {
        acumuladoIntereses += item.intereses;
        return acumuladoIntereses;
      });

      // Configuración base del gráfico
      const opcionesGrafico = {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          x: {
            stacked: true,
            grid: {
              display: false
            },
            ticks: {
              maxRotation: 45,
              minRotation: 45
            }
          },
          y: {
            stacked: true,
            ticks: {
              callback: (value) => formatCurrency(value)
            },
            grid: {
              color: (context) => context.tick.value === 0 ? '#888' : 'rgba(0, 0, 0, 0.1)'
            },
            beginAtZero: true
          }
        },
        plugins: {
          legend: {
            position: 'top',
            labels: {
              boxWidth: 12,
              padding: 20,
              usePointStyle: true,
              pointStyle: 'rect'
            }
          },
          tooltip: {
            callbacks: {
              label: (context) => {
                let label = context.dataset.label || '';
                if (label) {
                  label += ': ';
                }
                if (context.parsed.y !== null) {
                  label += formatCurrency(context.parsed.y);
                }
                return label;
              },
              footer: (items) => {
                const total = items.reduce((sum, item) => sum + item.parsed.y, 0);
                return `Total acumulado: ${formatCurrency(total)}`;
              }
            }
          }
        },
        interaction: {
          intersect: false,
          mode: 'index'
        }
      };

      // Configuración específica para móviles
      const opcionesMovil = {
        scales: {
          x: {
            ticks: {
              display: false // Ocultar etiquetas del eje X en móviles
            }
          }
        },
        plugins: {
          legend: {
            position: 'bottom'
          }
        }
      };

      chartBarras = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: labels,
          datasets: [
            {
              label: 'Depósito inicial',
              data: datosInicial,
              backgroundColor: 'rgba(43, 103, 119, 0.7)',
              stack: 'stack-1',
              borderColor: '#2b6777',
              borderWidth: 1
            },
            {
              label: 'Aportaciones',
              data: datosAportaciones,
              backgroundColor: 'rgba(82, 171, 152, 0.7)',
              stack: 'stack-1',
              borderColor: '#52ab98',
              borderWidth: 1
            },
            {
              label: 'Intereses',
              data: datosIntereses,
              backgroundColor: 'rgba(200, 216, 228, 0.7)',
              stack: 'stack-1',
              borderColor: '#c8d8e4',
              borderWidth: 1
            }
          ]
        },
        options: esMovil ? Object.assign({}, opcionesGrafico, opcionesMovil) : opcionesGrafico
      });
    }

    function generarTabla(datos, esMensual) {
      const tbody = document.querySelector('#tablaResultados tbody');
      tbody.innerHTML = '';
      
      datos.forEach((item, index) => {
        const fila = document.createElement('tr');
        
        const periodo = esMensual ? `Mes ${item.periodo}` : `Año ${item.periodo}`;
        
        fila.innerHTML = `
          <td style="text-align: center;">${periodo}</td>
          <td>${formatCurrency(item.capitalInicial)}</td>
          <td>${formatCurrency(item.aportaciones)}</td>
          <td>${formatCurrency(item.intereses)}</td>
          <td><strong>${formatCurrency(item.total)}</strong></td>
        `;
        
        if (esMensual && item.periodo % 12 === 0) {
          fila.style.backgroundColor = 'rgba(82, 171, 152, 0.2)';
          if (document.body.classList.contains('dark')) {
            fila.style.backgroundColor = 'rgba(82, 171, 152, 0.3)';
          }
        }
        
        tbody.appendChild(fila);
      });
      
      // Asegurarse de que la tabla se ajuste al dispositivo
      ajustarTablaParaMoviles();
    }

    function ajustarTablaParaMoviles() {
      const tabla = document.getElementById('tablaResultados');
      const contenedor = document.querySelector('.table-wrapper');
      const esMovil = window.innerWidth < 768;
      
      if (esMovil) {
        // Ajustar el ancho de la tabla al contenedor
        tabla.style.width = '100%';
        
        // Mostrar todas las columnas pero con mejor formato para móviles
        const columnasMostrar = [0, 1, 2, 3, 4]; // Todas las columnas
        const filas = tabla.querySelectorAll('tr');
        
        filas.forEach(fila => {
          const celdas = fila.querySelectorAll('td, th');
          celdas.forEach((celda, index) => {
            if (columnasMostrar.includes(index)) {
              celda.style.display = '';
              // Ajustar tamaño de fuente para móviles
              celda.style.fontSize = '12px';
              celda.style.padding = '6px 4px';
            } else {
              celda.style.display = 'none';
            }
          });
        });
        
        // Ajustar el contenedor de la tabla
        contenedor.style.overflowX = 'auto';
        contenedor.style.maxHeight = 'none';
        contenedor.style.border = '1px solid #e0e0e0';
        contenedor.style.borderRadius = '6px';
      } else {
        // Restaurar visualización en pantallas grandes
        const filas = tabla.querySelectorAll('tr');
        
        filas.forEach(fila => {
          const celdas = fila.querySelectorAll('td, th');
          celdas.forEach(celda => {
            celda.style.display = '';
            celda.style.fontSize = '';
            celda.style.padding = '';
          });
        });
      }
    }

    function formatCurrency(value) {
      return new Intl.NumberFormat('es-MX', { 
        style: 'currency', 
        currency: 'MXN',
        minimumFractionDigits: 2,
        maximumFractionDigits: 2
      }).format(value);
    }

    // Función para exportar a PDF
    async function exportToPDF() {
      const { jsPDF } = window.jspdf;
      const doc = new jsPDF({
        orientation: 'portrait',
        unit: 'mm',
        format: 'a4'
      });

      // Configuración de estilos
      const primaryColor = '#2b6777';
      const secondaryColor = '#52ab98';
      const accentColor = '#28a745';
      const textColor = '#333333';
      const lightGray = '#f5f5f5';
      
      // Margenes y dimensiones
      const margin = 15;
      const pageWidth = doc.internal.pageSize.getWidth();
      const contentWidth = pageWidth - margin * 2;
      let yPosition = margin;

      // 1. Encabezado del reporte
      doc.setFontSize(18);
      doc.setTextColor(primaryColor);
      doc.setFont('helvetica', 'bold');
      doc.text('Reporte de Proyección Financiera', pageWidth / 2, yPosition, { align: 'center' });
      
      doc.setFontSize(10);
      doc.setTextColor(100);
      doc.setFont('helvetica', 'normal');
      yPosition += 8;
      doc.text(`Generado el: ${new Date().toLocaleDateString('es-MX', { 
        year: 'numeric', 
        month: 'long', 
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
      })}`, pageWidth / 2, yPosition, { align: 'center' });
      
      yPosition += 15;

      // 2. Resumen Ejecutivo (4 cuadros en 2 filas)
      doc.setFontSize(14);
      doc.setTextColor(primaryColor);
      doc.text('Resumen Ejecutivo', margin, yPosition);
      doc.setDrawColor(primaryColor);
      doc.setLineWidth(0.3);
      doc.line(margin, yPosition + 2, margin + 40, yPosition + 2);
      
      yPosition += 10;

      const summaryData = [
        { 
          icon: '💰',
          label: 'Inversión Inicial', 
          value: document.getElementById('res-inicial').textContent,
          color: primaryColor
        },
        { 
          icon: '📥',
          label: 'Aportaciones', 
          value: document.getElementById('res-aportaciones').textContent,
          color: secondaryColor
        },
        { 
          icon: '📈',
          label: 'Intereses', 
          value: document.getElementById('res-intereses').textContent,
          color: '#6c757d'
        },
        { 
          icon: '🏦',
          label: 'Total Final', 
          value: document.getElementById('res-total').textContent,
          color: accentColor
        }
      ];

      // Diseño de 2x2 para los cuadros de resumen
      const boxWidth = contentWidth / 2 - 5;
      const boxHeight = 20;
      
      summaryData.forEach((item, i) => {
        const xPosition = margin + (i % 2 === 0 ? 0 : boxWidth + 10);
        const currentY = yPosition + (i > 1 ? boxHeight + 10 : 0);
        
        // Fondo del cuadro
        doc.setFillColor(255, 255, 255);
        doc.setDrawColor(220, 220, 220);
        doc.roundedRect(xPosition, currentY, boxWidth, boxHeight, 2, 2, 'FD');
        
        // Borde izquierdo de color
        doc.setFillColor(item.color);
        doc.rect(xPosition, currentY, 4, boxHeight, 'F');
        
        // Icono
        doc.setFontSize(12);
        doc.setTextColor(item.color);
        doc.text(item.icon, xPosition + 8, currentY + 12);
        
        // Texto
        doc.setFontSize(9);
        doc.setTextColor(100);
        doc.text(item.label, xPosition + 20, currentY + 8);
        
        // Valor
        doc.setFontSize(11);
        doc.setFont('helvetica', 'bold');
        doc.setTextColor(textColor);
        if (item.label === 'Total Final') doc.setTextColor(accentColor);
        doc.text(item.value, xPosition + 20, currentY + 15);
      });

      yPosition += boxHeight * 2 + 15;

      // 3. Gráfico de la inversión (capturamos el canvas como imagen)
      doc.setFontSize(14);
      doc.setTextColor(primaryColor);
      doc.text('Progresión de la Inversión', margin, yPosition);
      doc.setDrawColor(primaryColor);
      doc.line(margin, yPosition + 2, margin + 50, yPosition + 2);
      
      yPosition += 10;

      try {
        const canvas = document.getElementById('graficaBarras');
        const canvasImage = await html2canvas(canvas, {
          scale: 2,
          logging: false,
          useCORS: true,
          allowTaint: true
        });

        const imgData = canvasImage.toDataURL('image/png');
        const imgProps = doc.getImageProperties(imgData);
        const imgWidth = contentWidth;
        const imgHeight = (imgProps.height * imgWidth) / imgProps.width;
        
        // Ajustamos altura máxima para el gráfico
        const maxChartHeight = 80;
        const finalHeight = imgHeight > maxChartHeight ? maxChartHeight : imgHeight;
        
        doc.addImage(imgData, 'PNG', margin, yPosition, imgWidth, finalHeight);
        yPosition += finalHeight + 10;
      } catch (error) {
        console.error("Error al generar gráfico:", error);
        doc.setFontSize(10);
        doc.setTextColor('#dc3545');
        doc.text('No se pudo incluir el gráfico en el reporte', margin, yPosition);
        yPosition += 10;
      }

      // 4. Detalle de crecimiento (tabla)
      doc.setFontSize(14);
      doc.setTextColor(primaryColor);
      doc.text('Detalle por Periodos', margin, yPosition);
      doc.setDrawColor(primaryColor);
      doc.line(margin, yPosition + 2, margin + 40, yPosition + 2);
      
      yPosition += 10;

      // Preparamos datos para la tabla
      const tableData = [];
      const headers = ['Periodo', 'Inicial', 'Aportaciones', 'Intereses', 'Total'];
      const rows = document.querySelectorAll('#tablaResultados tbody tr');
      
      rows.forEach(row => {
        const cells = row.querySelectorAll('td');
        tableData.push([
          cells[0].textContent.trim(),
          cells[1].textContent.trim(),
          cells[2].textContent.trim(),
          cells[3].textContent.trim(),
          cells[4].textContent.trim()
        ]);
      });

      // Estilo de tabla profesional
      doc.autoTable({
        head: [headers],
        body: tableData,
        startY: yPosition,
        theme: 'grid',
        headStyles: {
          fillColor: primaryColor,
          textColor: 255,
          fontStyle: 'bold',
          fontSize: 9
        },
        bodyStyles: {
          fontSize: 8,
          cellPadding: 2
        },
        alternateRowStyles: {
          fillColor: lightGray
        },
        columnStyles: {
          0: { cellWidth: 'auto', halign: 'center' },
          1: { cellWidth: 'auto', halign: 'right' },
          2: { cellWidth: 'auto', halign: 'right' },
          3: { cellWidth: 'auto', halign: 'right' },
          4: { cellWidth: 'auto', halign: 'right', fontStyle: 'bold' }
        },
        margin: { left: margin, right: margin },
        tableWidth: contentWidth,
        styles: {
          overflow: 'linebreak',
          lineWidth: 0.1,
          lineColor: 200
        },
        didDrawPage: function(data) {
          // Footer en cada página
          doc.setFontSize(8);
          doc.setTextColor(150);
          doc.text(
            'Calculadora de Interés Compuesto - Herramienta profesional de proyección financiera',
            pageWidth / 2,
            doc.internal.pageSize.getHeight() - 10,
            { align: 'center' }
          );
        }
      });

      // Guardar el PDF
      doc.save(`Reporte_Financiero_${new Date().toISOString().slice(0,10)}.pdf`);
    }

    // Función para exportar a Excel
    function exportToExcel() {
      // Preparar datos
      const wb = XLSX.utils.book_new();
      
      // 1. Hoja de Resumen
      const summaryData = [
        ['REPORTE DE INVERSIÓN - INTERÉS COMPUESTO'],
        ['Generado el:', new Date().toLocaleDateString()],
        [],
        ['RESUMEN DE LA INVERSIÓN'],
        ['Depósito Inicial:', document.getElementById('res-inicial').textContent],
        ['Aportaciones:', document.getElementById('res-aportaciones').textContent],
        ['Intereses Acumulados:', document.getElementById('res-intereses').textContent],
        ['Total Acumulado:', document.getElementById('res-total').textContent],
        ['Tasa Anual:', document.getElementById('tasa').value + '%'],
        ['Plazo:', document.getElementById('plazo').value + ' ' + 
         (document.getElementById('tipoPlazo').value === 'mensual' ? 'meses' : 'años')],
        [],
        ['DETALLE DE PERIODOS']
      ];
      
      // 2. Datos de la tabla
      const tableHeaders = [];
      document.querySelectorAll('#tablaResultados thead th').forEach(th => {
        tableHeaders.push(th.textContent.trim());
      });
      
      const tableData = [tableHeaders];
      document.querySelectorAll('#tablaResultados tbody tr').forEach(row => {
        const rowData = [];
        row.querySelectorAll('td').forEach(cell => {
          rowData.push(cell.textContent.trim());
        });
        tableData.push(rowData);
      });
      
      // Combinar todos los datos
      const allData = [...summaryData, ...tableData];
      
      const ws = XLSX.utils.aoa_to_sheet(allData);
      
      // Aplicar estilos y formatos
      // 1. Fusionar celdas para títulos
      if(!ws['!merges']) ws['!merges'] = [];
      ws['!merges'].push({ s: { r: 0, c: 0 }, e: { r: 0, c: 4 } });
      ws['!merges'].push({ s: { r: 3, c: 0 }, e: { r: 3, c: 4 } });
      ws['!merges'].push({ s: { r: 11, c: 0 }, e: { r: 11, c: 4 } });
      
      // 2. Establecer anchos de columnas
      ws['!cols'] = [
        { wch: 15 }, // Periodo
        { wch: 20 }, // Depósito inicial
        { wch: 15 }, // Aportaciones
        { wch: 15 }, // Intereses
        { wch: 20 }  // Total acumulado
      ];
      
      XLSX.utils.book_append_sheet(wb, ws, "Reporte de Inversión");
      
      // Generar archivo
      XLSX.writeFile(wb, 'Reporte_Inversion.xlsx');
    }
  </script>
</body>
</html>
