<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BOM - Caja de Uvas 8.2 kg Exportación</title>
  <style>
    body { font-family: Calibri, Arial, sans-serif; margin: 20px; background: #f5f7fa; }
    .container { max-width: 1000px; margin: auto; background: white; padding: 25px; border-radius: 12px; box-shadow: 0 6px 20px rgba(0,0,0,0.1); }
    h1 { color: #1e3a8a; text-align: center; }
    h2 { color: #155e75; border-bottom: 2px solid #06b6d4; padding-bottom: 8px; }
    table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 15px; }
    th { background: #06b6d4; color: white; padding: 12px; }
    td { padding: 10px; border: 1px solid #ddd; }
    tr:nth-child(even) { background: #f8fafc; }
    .nivel0 { background: #dbeafe !important; font-weight: bold; font-size: 1.2em; }
    .nivel1 { background: #fecaca; }
    .nivel2 { background: #fef3c7; }
    .nivel3 { background: #d9f99d; }
    input { 
      width: 90px; padding: 6px; font-size: 15px; text-align: center; 
      border: 2px solid #06b6d4; border-radius: 6px; font-weight: bold;
    }
    .titulo { font-size: 18px; font-weight: bold; color: #1e40af; }
    .nota { font-style: italic; color: #64748b; margin-top: 20px; }
    .export { margin-top: 30px; text-align: center; }
    button { padding: 12px 24px; background: #16a34a; color: white; border: none; border-radius: 8px; font-size: 16px; cursor: pointer; }
    button:hover { background: #15803d; }
  </style>
</head>
<body>
  <div class="container">
    <h1>BOM – CAJA DE UVAS 8.2 KG EXPORTACIÓN</h1>
    <p style="text-align:center; color:#dc2626; font-weight:bold;">
      Cálculo basado en 114 cajas por pallet │ Configuración estándar Perú/Chile 2025
    </p>

    <h2>Cantidad a producir</h2>
    <table>
      <tr class="nivel0">
        <td class="titulo">Cajas de 8.2 kg deseadas</td>
        <td><input type="number" id="cajas" value="1" min="1" step="1" onchange="calcular()"></td>
        <td>→ <strong><span id="pallets">0.0088</span> pallets</strong></td>
      </tr>
    </table>

    <h2>Lista de Materiales (BOM)</h2>
    <table>
      <thead>
        <tr>
          <th>Nivel</th>
          <th>Código</th>
          <th>Descripción del Material</th>
          <th>Cant. por caja</th>
          <th>Total Requerido</th>
          <th>Unidad</th>
          <th>Notas</th>
        </tr>
      </thead>
      <tbody>
        <!-- NIVEL 0 -->
        <tr class="nivel0">
          <td>0</td>
          <td>A-8200</td>
          <td>CAJA DE UVAS 8.2 KG LISTA PARA EXPORTACIÓN</td>
          <td>1</td>
          <td id="tA">1.00</td>
          <td>cajas</td>
          <td>Palletizable (114 por pallet)</td>
        </tr>

        <!-- NIVEL 1 - Materia Prima y Envase Primario -->
        <tr class="nivel1">
          <td>1</td>
          <td>B-UVA</td>
          <td>Uva fresca calibre 18–24 mm (variedad según campaña)</td>
          <td>8.200</td>
          <td id="tB">8.200</td>
          <td>kg</td>
          <td>Peso neto</td>
        </tr>
        <tr class="nivel1">
          <td>1</td>
          <td>C-JABA</td>
          <td>Jaba de cartón corrugado 8.2 kg (tipo telescópica)</td>
          <td>1</td>
          <td id="tC">1</td>
          <td>unid</td>
          <td>Peso jaba ≈ 480 g</td>
        </tr>
        <tr class="nivel1">
          <td>1</td>
          <td>D-BOLSA</td>
          <td>Bolsa polietileno perforada macro (40x50 cm)</td>
          <td>1</td>
          <td id="tD">1</td>
          <td>unid</td>
          <td>Liner interior</td>
        </tr>
        <tr class="nivel1">
          <td>1</td>
          <td>E-PADSO2</td>
          <td>Pad generador SO₂ doble fase (6 g liberación)</td>
          <td>1</td>
          <td id="tPad">1</td>
          <td>unid</td>
          <td>Obligatorio EE.UU./Europa</td>
        </tr>
        <tr class="nivel1">
          <td>1</td>
          <td>F-ETIQ</td>
          <td>Etiqueta principal + PLU</td>
          <td>2</td>
          <td id="tEtiq">2</td>
          <td>unid</td>
          <td>Impresas full color</td>
        </tr>
        <tr class="nivel1">
          <td>1</td>
          <td>G-CINTA</td>
          <td>Cinta adhesiva de embalaje 48 mm</td>
          <td>0.80</td>
          <td id="tCinta">0.80</td>
          <td>metros</td>
          <td>2 vueltas por caja</td>
        </tr>

        <!-- NIVEL 2 - Embalaje Secundario (por pallet) -->
        <tr class="nivel2">
          <td>2</td>
          <td>H-PALLET</td>
          <td>Pallet de madera tratado ISPM-15 100x120 cm</td>
          <td>0.008772</td>
          <td id="tPallet">0.0088</td>
          <td>unid</td>
          <td>114 cajas/pallet</td>
        </tr>
        <tr class="nivel2">
          <td>2</td>
          <td>I-FILM</td>
          <td>Film stretch 500 mm 23 micras</td>
          <td>0.105</td>
          <td id="tFilm">0.105</td>
          <td>kg</td>
          <td>12 kg por pallet completo pallet</td>
        </tr>
        <tr class="nivel2">
          <td>2</td>
          <td>J-ESQUIN</td>
          <td>Esquineros de cartón 5x5x120 cm</td>
          <td>0.0351</td>
          <td id="tEsquin">0.035</td>
          <td>unid</td>
          <td>4 por pallet</td>
        </tr>
        <tr class="nivel2">
          <td>2</td>
          <td>K-ZUNCHO</td>
          <td>Zuncho plástico 16 mm</td>
          <td>0.070</td>
          <td id="tZuncho">0.070</td>
          <td>metros</td>
          <td>8 metros por pallet</td>
        </tr>

        <!-- NIVEL 3 - Insumos de limpieza y proceso -->
        <tr class="nivel3">
          <td>3</td>
          <td>L-SANIT</td>
          <td>Sanitizante cuaternario de amonio</td>
          <td>0.00175</td>
          <td id="tSanit">0.0018</td>
          <td>litros</td>
          <td>200 ml por pallet</td>
        </tr>
        <tr class="nivel3">
          <td>3</td>
          <td>M-AGUA</td>
          <td>Agua potable para lavado mesas</td>
          <td>0.044</td>
          <td id="tAgua">0.044</td>
          <td>litros</td>
          <td>5 litros por pallet</td>
        </tr>
      </tbody>
    </table>

    <div class="export">
      <button onclick="exportarExcel()">Descargar como Excel (próximamente)</button>
      <p class="nota">Solo cambia el número de cajas arriba y todo se recalcula al instante</p>
    </div>
  </div>

  <script>
    function calcular() {
      const cajas = parseFloat(document.getElementById("cajas").value) || 0;
      const palletFactor = cajas / 114;

      document.getElementById("pallets").textContent = palletFactor.toFixed(4);

      // Nivel 0 y 1
      document.getElementById("tA").textContent = cajas.toFixed(3);
      document.getElementById("tB").textContent = (cajas * 8.2).toFixed(3);
      document.getElementById("tC").textContent = cajas.toFixed(0);
      document.getElementById("tD").textContent = cajas.toFixed(0);
      document.getElementById("tPad").textContent = cajas.toFixed(0);
      document.getElementById("tEtiq").textContent = (cajas * 2).toFixed(0);
      document.getElementById("tCinta").textContent = (cajas * 0.8).toFixed(2);

      // Nivel 2 (por pallet)
      document.getElementById("tPallet").textContent = palletFactor.toFixed(4);
      document.getElementById("tFilm").textContent = (palletFactor * 12).toFixed(3);
      document.getElementById("tEsquin").textContent = (palletFactor * 4).toFixed(3);
      document.getElementById("tZuncho").textContent = (palletFactor * 8).toFixed(3);

      // Nivel 3
      document.getElementById("tSanit").textContent = (palletFactor * 0.2).toFixed(4);
      document.getElementById("tAgua").textContent = (palletFactor * 5).toFixed(3);
    }

    function exportarExcel() {
      alert("Función de exportación a Excel en desarrollo. Copia y pega la tabla por ahora");
    }

    window.onload = calcular();
  </script>
</body>
</html>
