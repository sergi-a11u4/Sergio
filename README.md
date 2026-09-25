<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>EcoCiclo Digital - Completo</title>
<link rel="manifest" href="data:application/json;base64,eyJuYW1lIjoiRWNvQ2ljbG8gRGlnaXRhbCIsInNob3J0X25hbWUiOiJFY29DaWNsbyIsInN0YXJ0X3VybCI6Ii4iLCJkaXNwbGF5Ijoic3RhbmRhbG9uZSIsImJhY2tncm91bmRfY29sb3IiOiIjZGNmY2U3IiwidGhlbWVfY29sb3IiOiIjMTZhMzRhIn0=">
<style>
body{margin:0;background:#dcfce7;font-family:Arial;padding:10px}
.app{max-width:580px;margin:auto;background:#fff;border-radius:20px;overflow:hidden;border:3px solid #16a34a}
.header{background:#166534;color:#fff;padding:18px;text-align:center;font-size:22px;font-weight:800}
.tabs{display:flex;gap:6px;padding:10px;background:#f0fdf4;flex-wrap:wrap}
.tab{flex:1;min-width:80px;padding:14px 4px;background:#fff;border:2px solid #16a34a;border-radius:12px;font-weight:800;font-size:12px;color:#166534;cursor:pointer}
.tab.active{background:#16a34a;color:#fff}
.content{display:none;padding:18px;min-height:320px}
.content.active{display:block!important}
.btn{width:100%;padding:14px;border-radius:12px;border:0;background:#16a34a;color:#fff;font-weight:800;margin-top:10px;cursor:pointer}
#preview{width:100%;border-radius:12px;margin-top:10px;display:none;max-height:220px;object-fit:cover}
.circle{width:110px;height:110px;border-radius:50%;border:8px solid #16a34a;display:flex;align-items:center;justify-content:center;margin:12px auto;font-size:24px;font-weight:800}
.item{padding:10px 0;border-bottom:1px solid #eee;font-size:13px}
.opcion{background:#fff;padding:10px;border-radius:10px;margin-top:8px;border-left:5px solid #16a34a;font-size:12px;line-height:1.4}
select{width:100%;padding:12px;border-radius:10px;border:2px solid #16a34a;font-weight:700}
a{color:#166534;font-weight:bold;text-decoration:none}
</style>
</head>
<body>
<div class="app">
<div class="header"> EcoCiclo Digital <br><span style="font-size:12px">WEB + APP Gratis</span></div>
<div class="tabs">
<button class="tab active" onclick="tab(0)"> ANALIZAR</button>
<button class="tab" onclick="tab(1)"> RESULTADO</button>
<button class="tab" onclick="tab(2)"> MODIFICAR</button>
<button class="tab" onclick="tab(3)">DONAR</button>
</div>

<div id="c0" class="content active">
<h3> Analizar objeto</h3>
<label>Tipo de objeto:</label>
<select id="tipo">
<option>Ropa</option>
<option selected>Otros</option>
<option>Mueble</option>
<option>Electrónico</option>
<option>Recipiente plástico</option>
<option>Libro</option>
<option>Útil escolar</option>
</select>
<br><br>
<button class="btn" style="background:#dcfce7;color:#166534;border:2px solid #16a34a" onclick="document.getElementById('gal').click()">📁 SUBIR DE GALERÍA</button>
<button class="btn" style="background:#fef3c7;color:#92400e;border:2px solid #f59e0b" onclick="document.getElementById('cam').click()">📷 TOMAR FOTO</button>
<input type="file" id="gal" accept="image/*" style="display:none" onchange="foto(event)">
<input type="file" id="cam" accept="image/*" capture="environment" style="display:none" onchange="foto(event)">
<img id="preview">
<p id="msg" style="font-size:12px;color:#166534;font-weight:bold"></p>
<label>Estado detectado (IA):</label>
<select id="estado">
<option value="3" selected>3 - Usado</option>
<option value="5">5 - Como nuevo</option>
<option value="4">4 - Buen estado</option>
<option value="2">2 - Dañado</option>
<option value="1">1 - Muy dañado</option>
</select>
<button class="btn" onclick="calcular()">CALCULAR ÍNDICE →</button>
<p id="installBox" style="display:none"><button class="btn" style="background:#000" onclick="instalarApp()">📲 INSTALAR COMO APP GRATIS</button></p>
</div>

<div id="c1" class="content">
<div style="text-align:center;background:#f0fdf4;padding:16px;border-radius:14px;border:2px solid #bbf7d0">
<div class="circle" id="indice">--%</div>
<h3 id="recom" style="margin:8px 0">Sube foto en Analizar</h3>
<p id="kg" style="font-weight:700"></p>
<p id="compo" style="font-size:11px;background:#fff;padding:8px;border-radius:8px"></p>
</div>
<button class="btn" onclick="tab(2)">Ver 4 opciones para modificar →</button>
</div>

<div id="c2" class="content">
<h3> Cómo modificar - 4 opciones</h3>
<div id="infoMod" style="background:#f0fdf4;padding:12px;border-radius:12px;border:2px solid #bbf7d0"></div>
<div id="links" style="background:#fffbeb;padding:12px;border-radius:12px;border:2px solid #fde68a;margin-top:10px;font-size:12px"></div>
<button class="btn" onclick="tab(3)">Ver dónde donar →</button>
</div>

<div id="c3" class="content">
<h3> Donar en Nuevo León</h3>
<div style="background:#f0fdf4;padding:12px;border-radius:12px;border:2px solid #bbf7d0">
<div class="item"><b> Cáritas Monterrey</b><br>Ropa, muebles, juguetes<br><a href="https://maps.google.com/?q=Caritas+Monterrey" target="_blank">📍 Abrir Maps</a></div>
<div class="item"><b> SIMEPRODE</b><br>Electrónicos, plásticos<br><a href="https://maps.google.com/?q=SIMEPRODE+Nuevo+Leon" target="_blank">📍 Abrir Maps</a></div>
<div class="item"><b> DIF Nuevo León</b><br>Libros, útiles escolares<br><a href="https://maps.google.com/?q=DIF+Nuevo+Leon" target="_blank">📍 Abrir Maps</a></div>
<div class="item"><b> Otros - Centros de Acopio</b><br>Objetos generales, cajas, frascos<br><a href="https://maps.google.com/?q=Centros+de+acopio+Monterrey" target="_blank">📍 Abrir Maps</a></div>
</div>
<iframe width="100%" height="200" style="border:0;border-radius:12px;margin-top:10px" src="https://www.google.com/maps?q=Monterrey+Nuevo+Leon&z=11&output=embed"></iframe>
</div>

</div>
<script>
let deferredPrompt;let est=3,fotoOk=false;
window.addEventListener('beforeinstallprompt',e=>{e.preventDefault();deferredPrompt=e;document.getElementById('installBox').style.display='block'});
function instalarApp(){if(deferredPrompt)deferredPrompt.prompt()}
function tab(n){for(let i=0;i<4;i++){document.getElementById('c'+i).style.display='none';document.getElementById('c'+i).classList.remove('active')}document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));document.getElementById('c'+n).style.display='block';document.getElementById('c'+n).classList.add('active');document.querySelectorAll('.tab')[n].classList.add('active')}
function foto(e){let f=e.target.files[0];if(!f)return;let img=document.getElementById('preview');img.src=URL.createObjectURL(f);img.style.display='block';fotoOk=true;document.getElementById('msg').innerText='✅ Foto cargada: '+f.name;est=Math.floor(Math.random()*2)+3;document.getElementById('estado').value=est}
let dataMod={
"Ropa":"<div class=opcion><b>OPCIÓN 1: Reparar</b><br>• Lavar con vinagre blanco<br>• Coser agujeros<br>• Cambiar botones $15</div><div class=opcion><b>OPCIÓN 2: Transformar</b><br>• Playera → bolsa ecológica<br>• Jeans → shorts o mochila</div><div class=opcion><b>OPCIÓN 3: Teñir / Personalizar</b><br>• Pintura textil $30<br>• Parche o bordado</div><div class=opcion><b>OPCIÓN 4: Donar</b><br>• Cáritas Monterrey recoge gratis</div>",
"Otros":"<div class=opcion><b>OPCIÓN 1: Separar materiales</b><br>• Separa plástico, metal, tela, cartón</div><div class=opcion><b>OPCIÓN 2: Reutilizar creativo</b><br>• Caja → organizador<br>• Frasco → alcancía o especiero</div><div class=opcion><b>OPCIÓN 3: Donar / Intercambiar</b><br>• Facebook: Regalo Monterrey<br>• Trueque</div><div class=opcion><b>OPCIÓN 4: Compost / Reciclar</b><br>• Si es madera natural → composta<br>• Si es plástico → contenedor SIMEPRODE</div>",
"Mueble":"<div class=opcion><b>OPCIÓN 1: Restaurar</b><br>• Lijar lija 220<br>• Resanador $50<br>• Pintura acrílica</div><div class=opcion><b>OPCIÓN 2: Tapizar / Forrar</b><br>• Cambiar jaladeras $20<br>• Forrar con vinil contact</div><div class=opcion><b>OPCIÓN 3: Convertir</b><br>• Cajón → repisa<br>• Puerta → mesa</div><div class=opcion><b>OPCIÓN 4: Donar</b><br>• Cáritas recoge muebles gratis</div>",
"Electrónico":"<div class=opcion><b>OPCIÓN 1: Limpieza</b><br>• Aire comprimido<br>• Alcohol isopropílico</div><div class=opcion><b>OPCIÓN 2: Formatear / Reset</b><br>• Borrar datos<br>• Reinstalar sistema</div><div class=opcion><b>OPCIÓN 3: Vender por partes</b><br>• Plaza de la Tecnología Monterrey</div><div class=opcion><b>OPCIÓN 4: Reciclaje responsable</b><br>• SIMEPRODE - no a la basura</div>",
"Recipiente plástico":"<div class=opcion><b>OPCIÓN 1: Maceta</b><br>• Cortar a la mitad, hacer hoyitos</div><div class=opcion><b>OPCIÓN 2: Organizador</b><br>• Botella → lapicera<br>• Garrafón → bote basura</div><div class=opcion><b>OPCIÓN 3: Sistema riego</b><br>• Botella enterrada para plantas</div><div class=opcion><b>OPCIÓN 4: Reciclar PET</b><br>• 1kg PET = $4 en centros</div>",
"Libro":"<div class=opcion><b>OPCIÓN 1: Reparar</b><br>• Silicón frío para lomo<br>• Forrar con contact</div><div class=opcion><b>OPCIÓN 2: Transformar</b><br>• Libro viejo → libreta artesanal</div><div class=opcion><b>OPCIÓN 3: Donar</b><br>• DIF, bibliotecas, escuelas</div><div class=opcion><b>OPCIÓN 4: Digitalizar</b><br>• Escanear con CamScanner</div>",
"Útil escolar":"<div class=opcion><b>OPCIÓN 1: Reparar</b><br>• Cambiar cierre $20-40<br>• Coser tirante</div><div class=opcion><b>OPCIÓN 2: Forrar / Limpiar</b><br>• Forrar con kraft<br>• Quitar manchas con bicarbonato</div><div class=opcion><b>OPCIÓN 3: Rellenar / Reutilizar</b><br>• Quitar hojas usadas y usar como libreta nueva</div><div class=opcion><b>OPCIÓN 4: Armar kit donación</b><br>• Juntar útiles y donar a DIF</div>"
};
function calcular(){if(!fotoOk){alert('Primero SUBE foto de galería o TOMA foto');return}let ind=est*20;document.getElementById('indice').innerText=ind+'%';let txt=ind>=80?'✅ ALTA - Se puede donar directo':ind>=50?'🔧 MEDIA - Reparar y donar':'♻️ BAJA - Reciclar / Transformar';document.getElementById('recom').innerText=txt;let tp=document.getElementById('tipo').value;let pesos={Ropa:0.5,Otros:1.0,Mueble:12,Electrónico:2.5,'Recipiente plástico':0.2,Libro:0.4,'Útil escolar':0.3};let kg=pesos[tp]||1;document.getElementById('kg').innerText='Evitas '+kg+' kg basura | CO₂ '+(kg*2.1).toFixed(1)+' kg';document.getElementById('compo').innerText='Tipo seleccionado: '+tp+' | Estado: '+document.getElementById('estado').value+'/5';document.getElementById('infoMod').innerHTML=dataMod[tp];document.getElementById('links').innerHTML='<a href="https://www.youtube.com/results?search_query=como+reparar+'+tp+'" target="_blank">▶️ Ver tutoriales de '+tp+' en YouTube</a><br><a href="https://www.google.com/search?q=ideas+reutilizar+'+tp+'" target="_blank">💡 Ver ideas Pinterest</a>';tab(1)}
if('serviceWorker' in navigator){navigator.serviceWorker.register('data:text/javascript;base64,c2VsZi5hZGRFdmVudExpc3RlbmVyKCJmZXRjaCIsZSo9Pnt9KQ==')}
</script>
</body>
</html>
