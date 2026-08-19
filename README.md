<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Las Aventuras de Imad</title>

<style>

* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #38bdf8, #8b5cf6);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
}

.juego {
    background: white;
    width: 100%;
    max-width: 700px;
    border-radius: 30px;
    padding: 30px;
    text-align: center;
    box-shadow: 0 20px 50px rgba(0,0,0,0.25);
}

h1 {
    font-size: 42px;
    margin: 5px;
}

h2 {
    font-size: 30px;
}

.subtitulo {
    font-size: 20px;
}

.info {
    display: flex;
    justify-content: space-between;
    margin: 20px 0;
    font-size: 20px;
    font-weight: bold;
}

.caja {
    background: #eef2ff;
    padding: 10px 15px;
    border-radius: 15px;
}

.pregunta {
    font-size: 32px;
    font-weight: bold;
    margin: 30px 0;
}

.respuestas {
    display: grid;
    gap: 15px;
}

.respuesta {
    border: none;
    border-radius: 20px;
    padding: 18px;
    font-size: 21px;
    font-weight: bold;
    background: #e0e7ff;
    cursor: pointer;
    transition: 0.2s;
}

.respuesta:hover {
    transform: scale(1.03);
    background: #c7d2fe;
}

.correcta {
    background: #86efac !important;
}

.incorrecta {
    background: #fca5a5 !important;
}

.mensaje {
    min-height: 40px;
    margin: 20px;
    font-size: 22px;
    font-weight: bold;
}

.boton {
    border: none;
    border-radius: 20px;
    padding: 15px 25px;
    font-size: 21px;
    font-weight: bold;
    background: #7c3aed;
    color: white;
    cursor: pointer;
}

.boton:hover {
    background: #6d28d9;
}

.oculto {
    display: none;
}

.grande {
    font-size: 70px;
}

.mundo {
    font-size: 50px;
    margin: 10px;
}

.estrellas {
    font-size: 25px;
    margin: 15px;
}

</style>
</head>


<body>

<div class="juego">


<!-- PANTALLA PRINCIPAL -->

<div id="inicio">

    <div class="grande">🌟</div>

    <h1>Las Aventuras de Imad</h1>

    <p class="subtitulo">
        ¡Bienvenido, campeón!
    </p>

    <p>
        Elige una aventura:
    </p>

    <button class="boton" onclick="empezar(0)">
        🔢 Mundo de los Números
    </button>

    <br><br>

    <button class="boton" onclick="empezar(1)">
        🍄 Mundo de Aventuras
    </button>

    <br><br>

    <button class="boton" onclick="empezar(2)">
        🏊 Mundo de Natación
    </button>

</div>


<!-- JUEGO -->

<div id="juego" class="oculto">

    <div class="mundo" id="iconoMundo"></div>

    <h2 id="nombreMundo"></h2>

    <div class="info">

        <div class="caja">
            Pregunta
            <span id="numeroPregunta">1</span>/10
        </div>

        <div class="caja">
            ⭐ <span id="puntos">0</span>
        </div>

    </div>


    <div class="pregunta" id="pregunta"></div>


    <div class="respuestas" id="respuestas"></div>


    <div class="mensaje" id="mensaje"></div>


    <button
        id="siguiente"
        class="boton oculto">
        Siguiente ➜
    </button>

</div>


<!-- FINAL -->

<div id="final" class="oculto">

    <div class="grande">
        🏆
    </div>

    <h1>¡Bravo, Imad!</h1>

    <h2 id="resultado"></h2>

    <div class="estrellas">
        ⭐ ⭐ ⭐
    </div>

    <p id="comentario"></p>

    <br>

    <button
        class="boton"
        onclick="volverInicio()">
        🏠 Volver al menú
    </button>

</div>


</div>


<script>


/* =========================
   PREGUNTAS
========================= */


const mundos = [

{

    nombre: "Mundo de los Números",

    icono: "🔢",

    preguntas: [

        {
            pregunta: "¿Cuánto es 5 + 3?",
            respuestas: ["6", "7", "8", "9"],
            correcta: 2
        },

        {
            pregunta: "¿Cuánto es 10 - 4?",
            respuestas: ["5", "6", "7", "8"],
            correcta: 1
        },

        {
            pregunta: "¿Cuánto es 3 × 2?",
            respuestas: ["5", "6", "7", "8"],
            correcta: 1
        },

        {
            pregunta: "¿Qué número viene después del 19?",
            respuestas: ["18", "20", "21", "29"],
            correcta: 1
        },

        {
            pregunta: "¿Cuánto es 7 + 6?",
            respuestas: ["11", "12", "13", "14"],
            correcta: 2
        },

        {
            pregunta: "¿Cuál es mayor?",
            respuestas: ["12", "8", "15", "10"],
            correcta: 2
        },

        {
            pregunta: "¿Cuánto es 20 - 7?",
            respuestas: ["11", "12", "13", "14"],
            correcta: 2
        },

        {
            pregunta: "¿Cuánto es 4 × 3?",
            respuestas: ["10", "11", "12", "13"],
            correcta: 2
        },

        {
            pregunta: "Si tienes 5 monedas y ganas 4 más, ¿cuántas tienes?",
            respuestas: ["8", "9", "10", "11"],
            correcta: 1
        },

        {
            pregunta: "¿Cuánto es 15 + 5?",
            respuestas: ["18", "19", "20", "21"],
            correcta: 2
        }

    ]

},


{

    nombre: "Mundo de Aventuras",

    icono: "🍄",

    preguntas: [

        {
            pregunta: "¿Qué necesitas para saltar sobre un obstáculo?",
            respuestas: ["Saltar", "Dormir", "Nadar", "Comer"],
            correcta: 0
        },

        {
            pregunta: "¿Qué recoges normalmente para conseguir puntos en una aventura?",
            respuestas: ["Piedras", "Monedas", "Calcetines", "Cucharas"],
            correcta: 1
        },

        {
            pregunta: "¿Qué aparece normalmente al terminar un nivel?",
            respuestas: ["Una recompensa", "Una nevera", "Un sofá", "Un coche"],
            correcta: 0
        },

        {
            pregunta: "¿Cuál de estos es un animal?",
            respuestas: ["Dragón", "Gato", "Robot", "Coche"],
            correcta: 1
        },

        {
            pregunta: "¿Qué objeto sirve para proteger la cabeza?",
            respuestas: ["Casco", "Zapato", "Guante", "Cuchara"],
            correcta: 0
        },

        {
            pregunta: "¿Qué haces para superar un acertijo?",
            respuestas: ["Pensar", "Dormir", "Correr sin mirar", "Cerrar los ojos"],
            correcta: 0
        },

        {
            pregunta: "¿Cuál es un buen premio?",
            respuestas: ["Una estrella", "Una piedra", "Una basura", "Un calcetín mojado"],
            correcta: 0
        },

        {
            pregunta: "¿Qué puede aparecer en un mundo de aventuras?",
            respuestas: ["Tesoro", "Nevera voladora", "Cama gigante", "Lavadora"],
            correcta: 0
        },

        {
            pregunta: "¿Qué hace un héroe cuando encuentra un problema?",
            respuestas: ["Lo intenta resolver", "Se rinde siempre", "Se duerme", "Se esconde"],
            correcta: 0
        },

        {
            pregunta: "¿Qué palabra describe mejor una aventura?",
            respuestas: ["Aburrida", "Emocionante", "Dormida", "Silenciosa"],
            correcta: 1
        }

    ]

},


{

    nombre: "Mundo de Natación",

    icono: "🏊",

    preguntas: [

        {
            pregunta: "¿Dónde nadamos normalmente?",
            respuestas: ["Piscina", "Desierto", "Montaña", "Cueva"],
            correcta: 0
        },

        {
            pregunta: "¿Qué usamos para ver mejor bajo el agua?",
            respuestas: ["Gafas de natación", "Zapatos", "Sombrero de lana", "Guantes de cocina"],
            correcta: 0
        },

        {
            pregunta: "¿Qué animal vive en el agua?",
            respuestas: ["Delfín", "León", "Caballo", "Gato"],
            correcta: 0
        },

        {
            pregunta: "¿Qué debemos hacer antes de entrar en una piscina?",
            respuestas: ["Seguir las normas", "Correr", "Empujar", "Gritar"],
            correcta: 0
        },

        {
            pregunta: "¿Qué parte del cuerpo usamos mucho para nadar?",
            respuestas: ["Brazos", "Orejas", "Nariz solamente", "Pelo"],
            correcta: 0
        },

        {
            pregunta: "¿Qué animal es famoso por nadar muy rápido?",
            respuestas: ["Tiburón", "Gallina", "Jirafa", "Conejo"],
            correcta: 0
        },

        {
            pregunta: "¿Qué encontramos en una piscina?",
            respuestas: ["Agua", "Arena del desierto", "Nieve siempre", "Fuego"],
            correcta: 0
        },

        {
            pregunta: "¿Qué debemos hacer si estamos cansados nadando?",
            respuestas: ["Parar y descansar", "Nadar más rápido", "No decir nada", "Correr"],
            correcta: 0
        },

        {
            pregunta: "¿Qué animal tiene aletas?",
            respuestas: ["Pez", "Perro", "Elefante", "Gato"],
            correcta: 0
        },

        {
            pregunta: "¿Qué palabra está relacionada con nadar?",
            respuestas: ["Agua", "Desierto", "Fuego", "Hielo seco"],
            correcta: 0
        }

    ]

}

];


let mundoActual = 0;
let preguntaActual = 0;
let puntos = 0;
let bloqueado = false;


/* =========================
   EMPEZAR
========================= */


function empezar(mundo) {

    mundoActual = mundo;

    preguntaActual = 0;

    puntos = 0;

    document
        .getElementById("inicio")
        .classList.add("oculto");

    document
        .getElementById("final")
        .classList.add("oculto");

    document
        .getElementById("juego")
        .classList.remove("oculto");

    document
        .getElementById("nombreMundo")
        .textContent =
        mundos[mundo].nombre;

    document
        .getElementById("iconoMundo")
        .textContent =
        mundos[mundo].icono;

    mostrarPregunta();

}


/* =========================
   MOSTRAR PREGUNTA
========================= */


function mostrarPregunta() {

    bloqueado = false;

    const datos =
        mundos[mundoActual]
        .preguntas[preguntaActual];


    document
        .getElementById("numeroPregunta")
        .textContent =
        preguntaActual + 1;


    document
        .getElementById("puntos")
        .textContent =
        puntos;


    document
        .getElementById("pregunta")
        .textContent =
        datos.pregunta;


    document
        .getElementById("mensaje")
        .textContent = "";


    const contenedor =
        document.getElementById("respuestas");

    contenedor.innerHTML = "";


    document
        .getElementById("siguiente")
        .classList.add("oculto");


    datos.respuestas.forEach(
        function(respuesta, indice) {

            const boton =
                document.createElement("button");

            boton.className = "respuesta";

            boton.textContent = respuesta;

            boton.onclick = function() {

                comprobarRespuesta(
                    indice,
                    boton
                );

            };

            contenedor.appendChild(boton);

        }
    );

}


/* =========================
   COMPROBAR RESPUESTA
========================= */


function comprobarRespuesta(
    indice,
    boton
) {

    if (bloqueado) return;

    bloqueado = true;


    const datos =
        mundos[mundoActual]
        .preguntas[preguntaActual];


    const botones =
        document
        .querySelectorAll(".respuesta");


    botones.forEach(
        b => b.disabled = true
    );


    if (indice === datos.correcta) {

        puntos++;

        boton.classList.add("correcta");

        document
            .getElementById("mensaje")
            .textContent =
            "🎉 ¡CORRECTO! ¡Imad es un campeón!";

    }

    else {

        boton.classList.add("incorrecta");

        botones[datos.correcta]
            .classList.add("correcta");

        document
            .getElementById("mensaje")
            .textContent =
            "💡 ¡Casi! ¡Vamos con la siguiente!";

    }


    document
        .getElementById("puntos")
        .textContent =
        puntos;


    document
        .getElementById("siguiente")
        .classList.remove("oculto");

}


/* =========================
   SIGUIENTE
========================= */


document
    .getElementById("siguiente")
    .onclick = function() {

        preguntaActual++;


        if (
            preguntaActual <
            mundos[mundoActual].preguntas.length
        ) {

            mostrarPregunta();

        }

        else {

            terminar();

        }

    };


/* =========================
   FINAL
========================= */


function terminar() {

    document
        .getElementById("juego")
        .classList.add("oculto");

    document
        .getElementById("final")
        .classList.remove("oculto");


    document
        .getElementById("resultado")
        .textContent =
        `⭐ ${puntos} de 10`;


    let texto;


    if (puntos === 10) {

        texto =
        "🤩 ¡PERFECTO! ¡Imad ha conseguido todas!";

    }

    else if (puntos >= 8) {

        texto =
        "🚀 ¡INCREÍBLE! ¡Imad es un auténtico campeón!";

    }

    else if (puntos >= 6) {

        texto =
        "🌟 ¡Muy bien, Imad! ¡Sigue así!";

    }

    else {

        texto =
        "💪 ¡Buen intento, Imad! ¡La próxima partida será todavía mejor!";

    }


    document
        .getElementById("comentario")
        .textContent =
        texto;

}


/* =========================
   VOLVER AL INICIO
========================= */


function volverInicio() {

    document
        .getElementById("final")
        .classList.add("oculto");

    document
        .getElementById("inicio")
        .classList.remove("oculto");

}

</script>

</body>
</html>
