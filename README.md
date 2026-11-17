# RutaGenetica — Optimizador de Rutas (TSP) con Algoritmos Genéticos

> **Enlaces del proyecto**

**Link:** ` `

**Repositorio en GitHub:** ` `

> 📝 **Nota:** este proyecto tiene los **mismos archivos** que el repositorio de GitLab
> (`index.html`, `styles.css`, `app.js`, `README.md`). Solo cambia la plataforma de alojamiento.

---

## Descripción

RutaGenetica resuelve el Problema del Agente Viajero (TSP) sobre un mapa interactivo y compara dos metaheurísticas: **Algoritmo Genético (GA)** y **Recocido Simulado (SA)**. Usa solo HTML5, CSS3 y JavaScript ES6+ sin dependencias.

Funciones: agregar, mover y eliminar ciudades en el canvas; presets (círculo de 16 nodos, 25 ciudades con semilla 42, 30 aleatorias); modos "Solo Genético", "Solo Recocido" y "Carrera simultánea"; controles Iniciar, Pausar, Paso y Reiniciar; gráfica de convergencia en tiempo real; exportación a JSON.

## Algoritmos

- **Order Crossover (OX):** se copia un tramo de ruta del padre 1 y los nodos restantes se completan en el orden en que aparecen en el padre 2, empezando después del tramo. Garantiza permutaciones válidas sin nodos repetidos.
- **Mutación 2-opt (inversión de segmento):** con probabilidad `mut` se invierte un tramo aleatorio de la ruta, lo que elimina cruces entre aristas. El GA además usa selección por torneo (k=5) y elitismo (2 mejores pasan intactos).
- **Recocido Simulado:** parte de la ruta inicial y propone vecinos 2-opt. Acepta siempre una mejora y, si empeora, con probabilidad `exp(-Δ/T)`. La temperatura baja geométricamente (`T ← T·α`) hasta `T < 0.01`, así que explora al inicio y refina al final.
- **Línea base:** distancia de la ruta en orden de creación y de la heurística voraz Vecino Más Cercano.

## Ejecución

1. Guarda `index.html`, `styles.css`, `app.js` y `README.md` en una misma carpeta.
2. Abre `index.html` en un navegador moderno. No requiere servidor ni instalación.
3. Elige un preset o haz clic en el mapa, selecciona el modo y pulsa **Iniciar**.

## Pruebas Verificables

Con el preset **Círculo Óptimo (16 nodos, R=200px)** los puntos son vértices de un polígono regular de 16 lados y la ruta óptima es recorrerlos en orden.

```
Perímetro = 2 · n · R · sin(π / n)
          = 2 · 16 · 200 · sin(π / 16)
          = 6400 · 0.195090...
          ≈ 1248.58 px
```

Cada lado mide 2·R·sin(π/16) ≈ 78.04 px. Si el algoritmo converge, la "Mejor distancia" debe llegar a **≈ 1248.58 px** (con tolerancia de redondeo) y la ruta no debe tener cruces. Compara con el Vecino Más Cercano y con la ruta inicial para ver la mejora.
