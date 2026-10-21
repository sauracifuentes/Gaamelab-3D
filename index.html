<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Juego 3D: Cruce Peligroso</title>
    <script src="https://code.playcanvas.com/playcanvas-stable.min.js"></script>
    <style>
        body { margin: 0; padding: 0; overflow: hidden; background-color: #000; }
        canvas { display: block; width: 100vw; height: 100vh; }
        #interfaz {
            position: absolute; top: 20px; left: 20px; color: white;
            font-family: system-ui, sans-serif; background: rgba(0,0,0,0.8);
            padding: 15px; border-radius: 8px; border: 2px solid #f5a623;
            box-shadow: 0 0 15px #f5a62344;
        }
        #puntos { color: #f5a623; font-size: 24px; font-weight: bold; }
        #mensajeOver {
            position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);
            font-family: system-ui, sans-serif; font-size: 32px; font-weight: bold;
            color: #ff4757; background: rgba(0,0,0,0.9); padding: 30px;
            border-radius: 10px; border: 3px solid #ff4757; display: none;
            text-align: center; cursor: pointer;
        }
    </style>
</head>
<body>
    <div id="interfaz">
        Cruces Exitosos: <span id="puntos">0</span><br>
        <span style="font-size: 14px; color: #a2aec9;">Usa Flechas para cruzar la calle</span>
    </div>
    <div id="mensajeOver" onclick="location.reload()">
        ¡ATROPELLADO!<br><span style="font-size:16px; color:#fff;">Haz clic para reiniciar</span>
    </div>
    <canvas id="mundo3D"></canvas>
    <script>
        const canvas = document.getElementById('mundo3D');
        const spanPuntos = document.getElementById('puntos');
        const divMensaje = document.getElementById('mensajeOver');
        const app = new pc.Application(canvas, { keyboard: new pc.Keyboard(window) });
        app.start();
        app.setCanvasFillMode(pc.FILLMODE_FILL_WINDOW);
        app.setCanvasResolution(pc.RESOLUTION_AUTO);
        window.addEventListener('resize', () => app.resizeCanvas());

        const camara = new pc.Entity();
        camara.addComponent('camera', { clearColor: new pc.Color(0.1, 0.1, 0.1) });
        camara.setPosition(0, 15, 10);
        camara.lookAt(0, 0, -5);
        app.root.addChild(camara);

        const luz = new pc.Entity();
        luz.addComponent('light', { type: 'directional', color: new pc.Color(1, 1, 1), intensity: 1.2 });
        luz.setEulerAngles(45, 30, 0);
        app.root.addChild(luz);

        // Suelo
        const suelo = new pc.Entity();
        suelo.addComponent('render', { type: 'plane' });
        suelo.setLocalScale(20, 1, 30);
        suelo.setPosition(0, 0, -5);
        const matSuelo = new pc.StandardMaterial();
        matSuelo.diffuse.set(0.2, 0.2, 0.2);
        matSuelo.update();
        suelo.render.material = matSuelo;
        app.root.addChild(suelo);

        // Jugador
        const jugador = new pc.Entity();
        jugador.addComponent('render', { type: 'box' });
        jugador.setPosition(0, 0.5, 8);
        const matJugador = new pc.StandardMaterial();
        matJugador.diffuse.set(0.2, 0.9, 0.2);
        matJugador.update();
        jugador.render.material = matJugador;
        app.root.addChild(jugador);

        // Enemigos (Coches)
        const coches = [];
        const matCoche = new pc.StandardMaterial();
        matCoche.diffuse.set(0.9, 0.2, 0.2);
        matCoche.update();

        const carriles = [-6, -3, 0, 3, 6]; // Posiciones Z de los carriles
        const velocidades = [5, -7, 6, -5, 8];

        function crearCoche(carrilIndex) {
            const coche = new pc.Entity();
            coche.addComponent('render', { type: 'box' });
            coche.setLocalScale(2, 1, 1); // Más largos que anchos
            
            let dir = velocidades[carrilIndex] > 0 ? -12 : 12;
            coche.setPosition(dir, 0.5, carriles[carrilIndex]);
            coche.render.material = matCoche;
            app.root.addChild(coche);
            coches.push({ ent: coche, vel: velocidades[carrilIndex] });
        }

        let temporizadorCoches = 0;
        let puntos = 0;
        let juegoActivo = true;
        let cooldownMovimiento = 0;

        app.on('update', function (dt) {
            if (!juegoActivo) return;

            // Controles de movimiento (Saltos discretos)
            cooldownMovimiento -= dt;
            if (cooldownMovimiento <= 0) {
                let posJ = jugador.getPosition();
                let movido = false;
                
                if (app.keyboard.isPressed(pc.KEY_UP) || app.keyboard.isPressed(pc.KEY_W)) {
                    jugador.setPosition(posJ.x, posJ.y, posJ.z - 3); movido = true;
                } else if (app.keyboard.isPressed(pc.KEY_DOWN) || app.keyboard.isPressed(pc.KEY_S)) {
                    if (posJ.z < 8) { jugador.setPosition(posJ.x, posJ.y, posJ.z + 3); movido = true; }
                } else if (app.keyboard.isPressed(pc.KEY_LEFT) || app.keyboard.isPressed(pc.KEY_A)) {
                    if (posJ.x > -8) { jugador.setPosition(posJ.x - 3, posJ.y, posJ.z); movido = true; }
                } else if (app.keyboard.isPressed(pc.KEY_RIGHT) || app.keyboard.isPressed(pc.KEY_D)) {
                    if (posJ.x < 8) { jugador.setPosition(posJ.x + 3, posJ.y, posJ.z); movido = true; }
                }

                if (movido) {
                    cooldownMovimiento = 0.2; // Evitar que se mueva súper rápido
                }
            }

            let posJ = jugador.getPosition();
            
            // Comprobar si llegó a la meta
            if (posJ.z < -8) {
                puntos++;
                spanPuntos.textContent = puntos;
                jugador.setPosition(0, 0.5, 8); // Reiniciar posición
                // Aumentar dificultad
                for(let i=0; i<velocidades.length; i++) {
                    velocidades[i] += (velocidades[i] > 0 ? 0.5 : -0.5);
                }
            }

            // Generar coches
            temporizadorCoches += dt;
            if (temporizadorCoches > 0.8) {
                temporizadorCoches = 0;
                let carrilAleatorio = Math.floor(Math.random() * carriles.length);
                crearCoche(carrilAleatorio);
            }

            // Mover coches y colisiones
            for (let i = coches.length - 1; i >= 0; i--) {
                let c = coches[i];
                c.ent.translate(c.vel * dt, 0, 0);
                let posC = c.ent.getPosition();

                // Destruir coches fuera de la pantalla
                if (posC.x > 15 || posC.x < -15) {
                    c.ent.destroy();
                    coches.splice(i, 1);
                    continue;
                }

                // Colisión
                let dx = posJ.x - posC.x;
                let dz = posJ.z - posC.z;
                if (Math.abs(dx) < 1.5 && Math.abs(dz) < 1.0) {
                    juegoActivo = false;
                    divMensaje.style.display = 'block';
                }
            }
        });
    </script>
</body>
</html>