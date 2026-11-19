# Integración de memoria temporal de NPC

Este parche está dirigido al código fuente de `origami-ltd/wasm-revc`, que compila el motor reVC con Emscripten. No modifica las físicas, colisiones, vehículos ni controles.

## Comportamiento incluido

- La memoria dura 60 segundos de partida y no se guarda en disco.
- Solo se crea cuando el motor registra un robo de vehículo o un atropello causado por el jugador.
- El peatón debe estar cerca del incidente, tener visión del jugador y línea de visión despejada.
- Los peatones con más miedo que temperamento corren para alejarse.
- Los de temperamento más alto se alejan caminando mientras miran al jugador.
- Ver al jugador sin que haya ocurrido un incidente presenciado no crea memoria.

La reacción de confrontación física no está incluida en esta versión; el comportamiento de temperamento alto es una retirada cautelosa y no violenta.

## Prueba dentro del port

El workflow de GitHub compila una segunda versión independiente en `dist/npc-engine/`. Cuando la compilación termine correctamente, abre:

`/npc-engine/index.html`

Esta versión utiliza el port WebAssembly de reVC y requiere:
- Navegador compatible con WebGL 2 y SharedArrayBuffer.
- Servir la web por HTTPS o localhost.
- Seleccionar una instalación propia y compatible de GTA Vice City desde el selector del navegador.

El port DOS.Zone original permanece disponible en la raíz y no se reemplaza. El nuevo motor no usa el CDN de assets del port DOS.Zone.

## Compilación

El workflow descarga versiones fijadas del workspace `wasm.com.br` y `wasm-revc`, aplica este parche, compila con Emscripten y publica la interfaz y los binarios juntos. La salida JavaScript y WASM se mantiene como un par de la misma compilación para evitar incompatibilidades.
