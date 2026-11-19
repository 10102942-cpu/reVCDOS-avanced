# Integración de memoria temporal de NPC

Este parche está aplicado al código fuente de `origami-ltd/wasm-revc` y compilado con Emscripten. La salida de prueba está en `dist/npc-engine/`. El port DOS.Zone original sigue en la raíz y no se reemplaza.

## Comportamiento incluido

- La memoria dura 60 segundos de partida y no se guarda en disco.
- Solo se crea cuando el motor registra un robo de vehículo o un atropello causado por el jugador.
- El peatón debe estar cerca del incidente, tener al jugador en su campo de visión y una línea de visión despejada.
- Los peatones con más miedo que temperamento corren para alejarse.
- Los de temperamento más alto se retiran caminando mientras miran al jugador.
- Ver al jugador sin un incidente presenciado no crea memoria.

Esta primera versión no incluye una reacción de combate. No se cambian físicas, colisiones, vehículos ni controles.

## Abrir la versión de prueba

Desde una copia local de esta rama:

```bash
python -m pip install -r requirements.txt
python server.py
```

Luego abre `http://localhost:8000/npc-engine/index.html`.

El servidor añade los encabezados de aislamiento necesarios para `SharedArrayBuffer` en esa ruta. También se puede alojar la carpeta `dist/` en un servidor HTTPS que conserve esos encabezados.

## Requisitos del motor de prueba

- Navegador compatible con WebGL 2 y SharedArrayBuffer.
- HTTPS o localhost.
- Una instalación local compatible de GTA Vice City que el usuario debe seleccionar desde el navegador.

Este motor alternativo no reutiliza los archivos que el port DOS.Zone descarga de su CDN; por eso necesita seleccionar los datos locales del juego.

## Compilación

El workflow `.github/workflows/build-npc-engine.yml` descarga versiones fijadas del workspace `wasm.com.br` y `wasm-revc`, aplica `npc-memory-reactions.patch`, compila el motor WebAssembly y publica la interfaz y los binarios juntos.
