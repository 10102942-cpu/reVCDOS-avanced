# Memoria temporal de los NPC

Este directorio contiene el primer parche de IA para el **motor C++ reVC**.

## Regla de memoria

Un peatón no recuerda al jugador solo por verlo o porque este se acerque. El recuerdo se crea únicamente cuando se cumplen todas estas condiciones:

1. El motor ha registrado un incidente atribuible al jugador (agresión, disparo, atropello, robo de vehículo, explosión u otro evento violento del juego).
2. El peatón estaba cerca del lugar del incidente.
3. El peatón tenía al jugador en su campo de visión.
4. La línea de visión entre ambos estaba despejada.

El recuerdo dura 60 segundos de partida y no se guarda en disco. Al volver a ver al jugador a corta distancia, el peatón decide según sus estadísticas existentes: temperamento alto puede enfrentarse; en caso contrario huye. No se modifica el movimiento, las colisiones ni la física.

## Importante sobre el port actual

`reVCDOS-avanced` contiene el lanzador web y un motor ya compilado en WebAssembly; no contiene los archivos C++ del motor. Por eso este parche todavía **no cambia el comportamiento del juego publicado**. Está preparado para el árbol fuente con soporte de compilación Emscripten de [origami-ltd/wasm-revc](https://github.com/origami-ltd/wasm-revc), que usa el mismo código reVC para los módulos de peatones y eventos.

Para aplicarlo en una copia local del árbol fuente compatible:

```bash
git apply engine-patches/npc-memory-reactions.patch
```

Después hay que compilar el motor WebAssembly y sustituir el WASM junto con el cargador compatible. No se debe reemplazar solo el archivo WASM del port DOS.Zone: los cargadores y las versiones del motor deben coincidir.

## Alcance de esta primera parte

Este parche implementa el recuerdo condicionado y la reacción al reencontrarse. El envío de denuncias a teléfonos y la búsqueda policial persistente son fases separadas; no se anuncian como implementadas aquí.
