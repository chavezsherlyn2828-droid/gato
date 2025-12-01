[index.html](https://github.com/user-attachments/files/23844773/index.html)
<!DOCTYPE html>
<html lang="es">
<head>
 <link rel="stylesheet" type="text/css" href="estilos.css">
<meta charset="UTF-8">
<title>3 en Raya</title>
</head>

<body>
<h5>las tres S (SaShSa)</h5> 
<h1>EL GATITO</h1>
<h2 id="mensaje ganador"></h2>
<p id="turno">Turno de: X</p>

<div id="tablero">
    <div class="casilla"></div>
    <div class="casilla"></div>
    <div class="casilla"></div>
    <div class="casilla"></div>
    <div class="casilla"></div>
    <div class="casilla"></div>
    <div class="casilla"></div>
    <div class="casilla"></div>
    <div class="casilla"></div>
</div>

<button onclick="reiniciar()">Reiniciar</button>

<script>
let casillas = document.querySelectorAll(".casilla");
let turno = "X"; 
let juegoTerminado = false;

/*dom*/
casillas.forEach( celda =>{
    celda.addEventListener("click", ()=>{
        if(celda.innerText=="" && !juegoTerminado){
            celda.innerText = turno;
            verificarGanador();
            turno = (turno=="X") ? "O" : "X";
            document.getElementById("turno").innerText="Turno de: "+turno;
        }
    });
});


function verificarGanador(){
    let c=[...casillas].map(i=>i.innerText);
    let combos=[
        [0,1,2], [3,4,5], [6,7,8], 
        [0,3,6], [1,4,7], [2,5,8], 
        [0,4,8], [2,4,6]           
    ];
    for(let combo of combos){
        if(c[combo[0]]!="" && c[combo[0]]==c[combo[1]] && c[combo[1]]==c[combo[2]]){
            juegoTerminado = true;
            document.getElementById("mensaje ganador").innerText="Ganadooor: "+c[combo[0]];

            return;
        }
    }
    if(!c.includes("")){
        juegoTerminado = true;
        document.getElementById("mensaje ganador").innerText="EMPATE, reinicia la jugada";
    }
}

function reiniciar(){
    casillas.forEach(celda => celda.innerText="");
    turno="X";
    juegoTerminado=false;
    document.getElementById("turno").innerText="Turno de: X";
    document.getElementById("mensaje ganador").innerText=" ";
}
</script>
</body>
</html>
