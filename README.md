<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BOM Multi-Fruta | Uva & Arándano</title>
  <style>
    body { font-family: Calibri, Arial, sans-serif; margin: 20px; background: #f5f7fa; }
    .container { max-width: 1100px; margin: auto; background: white; padding: 25px; border-radius: 12px; box-shadow: 0 6px 20px rgba(0,0,0,0.1); }
    h1 { color: #1e3a8a; text-align: center; }
    select, input { padding: 8px; font-size: 16px; border-radius: 6px; border: 2px solid #06b6d4; }
    table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 15px; }
    th { background: #06b6d4; color: white; padding: 12px; }
    td { padding: 10px; border: 1px solid #ddd; }
    .nivel0 { background: #dbeafe !important; font-weight: bold; font-size: 1.2em; }
    .nivel1 { background: #fecaca; }
    .nivel2 { background: #fef3c7; }
    .nivel3 { background: #d9f99d; }
    .controles { text-align: center; margin: 20px 0; padding: 15px; background: #e0f2fe; border-radius: 10px; }
    .nota { font-style: italic; color: #64748b; text-align: center; }
  </style>
</head>
<body>
  <div class="container">
    <h1>BOM MULTI-FRUTA EXPORTACIÓN</h1>

    <div class="controles">
      <label><strong>Producto terminado:</strong></label>
      <select id="producto" onchange="cambiarProducto()">
        <option value="uva">Uva de mesa – Caja 8.2 kg</option>
        <option value="arandano">Arándano – Caja 4.5 kg (36 × 125 g)</option>
      </select>
      &nbsp;&nbsp;&nbsp;
      <label><strong>Cantidad de cajas:</strong></label>
      <input type="number" id="cajas" value="1" min="1" onchange="calcular()">
    </div>

    <table id="tablaBOM">
      <thead>
        <tr>
          <th>Nivel</th>
          <th>Código</th>
          <th>Descripción</th>
          <th>Cant. por caja</th>
          <th>Total requerido</th>
          <th>Unidad</th>
          <th>Notas</th>
        </tr>
      </thead>
      <tbody id="filas">
        <!-- Las filas se generan con JavaScript -->
      </tbody>
    </table>

    <p class="nota">Cambia el producto o la cantidad de cajas → todo se recalcula al instante</p>
  </div>

  <script>
    const bom = {
      uva: [
        ["0","A-8200","CAJA DE UVAS 8.2 KG LISTA",1,"cajas","114 cajas por pallet"],
        ["1","B-UVA","Uva fresca",8.200,"kg","Peso neto"],
        ["1","C-JABA","Jaba cartón 8.2 kg telescópica",1,"unid","≈480 g"],
        ["1","D-BOLSA","Bolsa PE perforada macro",1,"unid",""],
        ["1","E-PADSO2","Pad SO₂ doble fase (6 g)",1,"unid",""],
        ["1","F-ETIQ","Etiqueta principal + PLU",2,"unid",""],
        ["1","G-CINTA","Cinta adhesiva 48 mm",0.8,"metros",""],
        ["2","H-PALLET","Pallet madera ISPM-15",1/114,"unid",""],
        ["2","I-FILM","Film stretch 23 micras",12/114,"kg",""],
        ["2","J-ESQUIN","Esquineros cartón",4/114,"unid",""],
        ["2","K-ZUNCHO","Zuncho plástico 16 mm",8/114,"metros",""],
        ["3","L-SANIT","Sanitizante cuaternario",0.2/114,"litros","200 ml/pallet"],
        ["3","M-AGUA","Agua lavado mesas",5/114,"litros",""]
      ],
      arandano: [
        ["0","AR-4500","CAJA DE ARÁNDANOS 4.5 KG LISTA",1,"cajas","144 cajas por pallet"],
        ["1","AR-FRUTA","Arándano fresco calibre 14-20 mm",4.500,"kg","Peso neto"],
        ["1","AR-PUNNET","Clamshell ventilado 125 g",36,"unid","PET transparente"],
        ["1","AR-TAPA","Tapa clamshell 125 g",36,"unid",""],
        ["1","AR-ABSOR","Absorbedor de etileno (sachet)",1,"unid","por caja madre"],
        ["1","AR-PADSO2","Pad SO₂ arándano (4 g)",1,"unid",""],
        ["1","AR-ETIQ","Etiqueta caja madre + banda",2,"unid",""],
        ["1","AR-CINTA","Cinta adhesiva",0.6,"metros",""],
        ["2","AR-PALLET","Pallet madera 100×120 cm",1/144,"unid",""],
        ["2","AR-FILM","Film stretch",10/144,"kg","10 kg/pallet"],
        ["2","AR-ESQUIN","Esquineros cartón",4/144,"unid",""],
        ["2","AR-ZUNCHO","Zuncho plástico",6/144,"metros",""],
        ["3","AR-SANIT","Sanitizante",0.15/144,"litros","150 ml/pallet"]
      ]
    };

    function cambiarProducto() {
      calcular();
    }

    function calcular() {
      const producto = document.getElementById("producto").value;
      const cajas = parseFloat(document.getElementById("cajas").value) || 1;
      const datos = bom[producto];

      let html = "";
      datos.forEach(fila => {
        const cantidadPorCaja = parseFloat(fila[3]);
        const total = (cantidadPorCaja * cajas).toFixed(4).replace(/0+$/,'').replace(/\.$/,'');
        const clase = fila[0]==="0" ? "nivel0" : fila[0]==="1" ? "nivel1" : fila[0]==="2" ? "nivel2" : "nivel3";

        html += `<tr class="${clase}">
          <td>${fila[0]}</td>
          <td>${fila[1]}</td>
          <td>${fila[2]}</td>
          <td contenteditable="true" onblur="recalcular(this)">${cantidadPorCaja}</td>
          <td><strong>${total}</strong></td>
          <td>${fila[4]}</td>
          <td>${fila[5]}</td>
        </tr>`;
      });

      document.getElementById("filas").innerHTML = html;
    }

    // Permite editar la columna "Cant. por caja" y recalcular
    function recalcular(elemento) {
      calcular();
    }

    window.onload = calcular;
  </script>
</body>
</html>
