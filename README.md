# Problema de las 8 Reinas

Implementaciones del problema clásico de las ocho reinas mediante búsqueda en profundidad (DFS) con retroceso (*backtracking*). El material entregado está distribuido en archivos ZIP y contiene dos variantes independientes: un solucionador de consola en C# y un visualizador web en React.

## Contenido de las entregas

| Archivo | Contenido | Uso |
|---|---|---|
| `part1.zip` | Archivos de entorno y compilación de Visual Studio; no incluye archivos fuente `.cs`, `.csproj` ni una solución utilizable. | No es necesario para ejecutar las aplicaciones. |
| `part2.zip` | Proyecto C# `EightQueensAI`, dirigido a .NET 9. | Resolver e imprimir soluciones en consola. |
| `part2nodemod.zip` | Aplicación React y solucionador JavaScript, con dependencias declaradas en `package.json`. | Explorar visualmente las soluciones en el navegador. |
| `part3.zip` | Archivo `.sln` y un README de referencia. La solución hace referencia al proyecto C# de `part2.zip`. | Puede usarse al reunir las entregas, respetando la estructura esperada. |

> Los ZIP contienen proyectos separados, no una carpeta de aplicación integrada. Para trabajar con el solucionador C#, extrae `part2.zip`. Para usar el visualizador, extrae `part2nodemod.zip`.

## El problema

El objetivo es colocar ocho reinas en un tablero de ajedrez de 8 × 8 de modo que ninguna comparta fila, columna o diagonal con otra. El algoritmo construye posiciones fila por fila y descarta cada posición que entra en conflicto con las reinas colocadas anteriormente. La búsqueda recorre las opciones válidas en profundidad y retrocede cuando ya no puede avanzar.

## Aplicación C#

### Requisitos

- .NET 9 SDK

### Ejecución

Extrae `part2.zip`, abre una terminal en la carpeta extraída y ejecuta:

```bash
dotnet run --project EightQueensAI/EightQueensAI.csproj
```

El programa imprime los tableros encontrados y, al final, muestra el total de soluciones y los nodos recorridos por DFS. En Windows, la aplicación espera que se presione una tecla antes de cerrarse.

### Componentes principales

- `Program.cs`: inicia el solucionador y presenta el resumen.
- `EightQueensSolver.cs`: recorre el grafo, cuenta nodos y reconstruye cada tablero.
- `Queen.cs`: representa una reina como estado de búsqueda y comprueba conflictos.
- `Graph.cs` e `IGNode.cs`: implementan el recorrido genérico en profundidad.

## Visualizador React

### Requisitos

- Node.js y npm

### Ejecución

Extrae `part2nodemod.zip`, abre una terminal en la carpeta que contiene `package.json` y ejecuta:

```bash
npm install
npm start
```

La aplicación estará disponible normalmente en [http://localhost:3000](http://localhost:3000). Pulsa **Resolver** para calcular las soluciones y usa **Anterior** y **Siguiente** para recorrerlas. La interfaz presenta el tablero actual, el índice de solución y las métricas del recorrido.

### Componentes principales

- `src/App.js`: interfaz, controles de navegación y estadísticas.
- `src/Chessboard.js`: representación del tablero.
- `src/EightQueensSolver.js`: DFS y validación de posiciones en JavaScript.
- `src/*.css`: estilos de la aplicación y el tablero.

## Algoritmo y resultados

Cada estado conserva la fila y columna de una reina, junto con una referencia al estado padre. `firstChild()` busca una posición válida en la fila siguiente; `nextSibling()` busca otra columna válida en la fila actual. El recorrido DFS usa esas operaciones para explorar el espacio de búsqueda. Cuando se alcanza la última fila, las referencias a los padres permiten reconstruir el tablero completo.

Para un tablero de 8 × 8, el problema tiene 92 soluciones. Las aplicaciones calculan sus resultados al ejecutarse y muestran el conteo de nodos explorados.

## Estructura esperada al combinar entregas

El ZIP de la solución de Visual Studio espera que el proyecto C# esté junto a ella con esta disposición:

```text
proyecto/
├── EightQueensAI/
│   ├── EightQueensAI.csproj
│   ├── Program.cs
│   ├── Queen.cs
│   ├── Graph.cs
│   ├── IGNode.cs
│   └── EightQueensSolver.cs
└── Problema de las 8 reinas.sln
```

Si extraes `part2.zip` y `part3.zip` por separado, coloca la carpeta `EightQueensAI` junto al archivo `.sln` para que la referencia relativa de la solución funcione.

## Alcance

Las variantes C# y React resuelven el mismo problema de forma independiente; el visualizador no consume resultados del programa C#. `part1.zip` no es necesario para ninguna de las instrucciones anteriores. No se especifica una licencia en los archivos fuente incluidos.
