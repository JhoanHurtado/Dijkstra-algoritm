
# Algoritmo de Dijkstra

Este proyecto implementa un grafo interactivo que permite visualizar y calcular rutas más cortas entre nodos utilizando el **algoritmo de Dijkstra**. La aplicación está construida en **HTML** y **JavaScript** y utiliza la biblioteca **Vis.js** para representar el grafo visualmente.

## Características del Proyecto

- *Agregar nodos y aristas dinámicamente*: Puedes añadir nodos y conectar entre sí mediante aristas con pesos específicos.
- *Configurar nombres de nodos y pesos de aristas*: Asigna nombres a los nodos y establece los pesos de las aristas según sea necesario.
- *Calcular camino más corto*: Selecciona un nodo de origen y otro de destino para que el algoritmo de Dijkstra calcule y visualice el camino más corto.
- *Mostrar matriz de adyacencia*: La aplicación genera y muestra una tabla con la matriz de adyacencia del grafo, con un diseño responsivo.

## Vista Previa

![image](https://github.com/user-attachments/assets/7a1c1636-b131-4576-a2ed-586e71b229e6)

## Instalación y Configuración

1. Clona este repositorio:
   ```bash
   git clone https://github.com/JhoanHurtado/Dijkstra-algoritm.git

2.	Abre el archivo index.html en un navegador para probar la aplicación localmente o visita la versión publicada en GitHub Pages.

3. Uso de la Aplicación

	 1. Agregar Nodos: Ingresa el nombre del nodo en el campo de texto y
	    presiona el botón “Agregar Nodo” para agregar un nuevo nodo al
	    grafo.
	  2. Conectar Nodos con Aristas: Ingresa el nombre de los nodos de inicio y fin y el peso de la arista, y presiona “Agregar Arista” para crear la conexión entre los dos nodos.
	3. Calcular el Camino Más Corto: Selecciona un nodo de inicio y otro de fin en los menús desplegables, y luego presiona el botón “Calcular Camino Más Corto” para visualizar la ruta más corta y su costo total.
	4. Ver la Matriz de Adyacencia: Después de agregar los nodos y aristas, puedes ver la matriz de adyacencia en la tabla generada, que muestra los pesos de cada conexión entre nodos.

## Código y Estructura

**HTML**

El archivo HTML contiene:

	1. Un contenedor para el grafo (`<div id="network">`).
	2. Controles de entrada para añadir nodos y aristas.
	3. Una tabla que muestra la matriz de adyacencia y un área de resultados para visualizar el camino más corto.

**JavaScript**

El archivo JavaScript define varias funciones clave:
	1.	Inicialización del Grafo: Utiliza la biblioteca Vis.js para generar un grafo interactivo en el contenedor.

    const nodes = new vis.DataSet();
    const edges = new vis.DataSet();
    const network = new vis.Network(container, { nodes, edges }, options);

2.Función **addNode()**: Agrega un nodo con un nombre específico.

    function addNode(nodeName) {
      nodes.add({ id: nodeIdCounter++, label: nodeName });
    }

3.Función **addEdge()**: Agrega una arista entre dos nodos con un peso definido por el usuario.

    function addEdge(fromNode, toNode, weight) {
      edges.add({ from: fromNode, to: toNode, label: weight.toString() });
    }


4.***Algoritmo de Dijkstra***:
		La función **dijkstra()** implementa el algoritmo para calcular el camino más corto. Calcula la ruta más corta en función de la distancia acumulada y genera el costo total y el camino.

    function dijkstra(startNode, endNode) {
      // Algoritmo de Dijkstra para encontrar la ruta más corta
    }


5.***Generar y Mostrar la Matriz de Adyacencia:***
		La función displayAdjacencyMatrix() construye la matriz y muestra una tabla de adyacencia con los pesos de las aristas.

    function displayAdjacencyMatrix() {
      // Genera y muestra la matriz de adyacencia
    }

# **Ejemplo de Uso**

***1.Agregar Nodos y Aristas:***
 - Agrega los nodos “A”, “B” y “C”.
 - Conecta “A” y “B” con una arista de peso 5 y “B” y “C” con una arista de peso 3.
	
***2.Calcular Camino Más Corto:***
 - Selecciona “A” como inicio y “C” como fin. El camino más corto debe
   mostrar A → B → C con un costo de 8.

***3.Matriz de Adyacencia:***

 - La tabla debe mostrar los valores de las conexiones directas entre
   nodos, con ∞ para indicar que no hay conexión.

***Tecnologías Utilizadas***
	

 - HTML y CSS para la estructura y el estilo.
 - JavaScript para la lógica y manipulación dinámica del DOM
 - Vis.js para la visualización de grafos interactivos.

### *Enlace al Proyecto en GitHub Pages*

[Previsualizar](https://jhoanhurtado.github.io/Dijkstra-algoritm/)



Notas y Mejoras Futuras

Este proyecto puede extenderse agregando:

 - Detección de ciclos en el grafo.
 - Opción para mostrar caminos alternativos en caso de existir múltiples
   rutas óptimas.
 - Guardado y carga de grafos predefinidos.

Contribuciones

¡Las contribuciones son bienvenidas! Si deseas mejorar este proyecto, abre un Pull Request o crea un Issue para discutir ideas.
```javascript
function dijkstra(startNode, endNode) {
  const distances = {};
  const previousNodes = {};
  const unvisitedNodes = new Set();

  // Initialize distances and previous nodes
  nodes.forEach(node => {
    distances[node.id] = Infinity;
    previousNodes[node.id] = null;
    unvisitedNodes.add(node.id);
  });

  distances[startNode] = 0;

  while (unvisitedNodes.size > 0) {
    let currentNode = null;
    let smallestDistance = Infinity;

    // Find the unvisited node with the smallest distance
    unvisitedNodes.forEach(node => {
      if (distances[node] < smallestDistance) {
        smallestDistance = distances[node];
        currentNode = node;
      }
    });

    unvisitedNodes.delete(currentNode);

    // Update distances of neighboring nodes
    edges.forEach(edge => {
      if (edge.from === currentNode && distances[currentNode] + parseInt(edge.label) < distances[edge.to]) {
        distances[edge.to] = distances[currentNode] + parseInt(edge.label);
        previousNodes[edge.to] = currentNode;
      }
    });
  }

  // Build the shortest path
  const path = [];
  let currentNode = endNode;
  while (currentNode !== null) {
    path.unshift(currentNode);
    currentNode = previousNodes[currentNode];
  }

  // Display the shortest path and its cost
  const pathCost = distances[endNode];
  const pathString = path.join(' → ');
  console.log(`Shortest path: ${pathString} (Cost: ${pathCost})`);
  document.getElementById('result').innerHTML = `Shortest path: ${pathString} (Cost: ${pathCost})`;
}

function displayAdjacencyMatrix() {
  const matrix = [];
  const nodeIds = nodes.getIds();

  // Initialize the matrix with zeros
  for (let i = 0; i < nodeIds.length; i++) {
    matrix[i] = [];
    for (let j = 0; j < nodeIds.length; j++) {
      matrix[i][j] = 0;
    }
  }

  // Populate the matrix with edge weights
  edges.forEach(edge => {
    const fromIndex = nodeIds.indexOf(edge.from);
    const toIndex = nodeIds.indexOf(edge.to);
    matrix[fromIndex][toIndex] = parseInt(edge.label);
  });

  // Display the matrix
  const matrixHtml = matrix.map(row => row.join(' ')).join('<br>');
  document.getElementById('adjacency-matrix').innerHTML = matrixHtml;
}
```
