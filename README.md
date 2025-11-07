# 🤖 AI Search Algorithm Visualizer

A single-file, interactive web tool built with vanilla JavaScript and Tailwind CSS (via CDN) to visually demonstrate and compare how various uninformed search algorithms explore a fixed, directed, and weighted graph.

## ✨ Features

* **Six Algorithms:** Visualize **BFS**, **DFS**, **DLS**, **IDDFS**, **UCS**, and **Bidirectional Search**.
* **Step-by-Step Visualization:** Watch nodes change color as they are visited, become the current node, or are placed in the frontier queue/stack.
* **Dynamic Graph State:** The control panel updates in real-time, showing the current state of the frontier (queue/stack/priority queue) and the path cost/depth.
* **Clear Results:** Displays the final path found and the total cost.

## 🚀 How to Run the Tool

Since this tool is a single HTML file and uses only client-side JavaScript, the setup is delightfully simple.

1.  **Save the Code:** Copy the entire code block I provided (the one that starts with `<!DOCTYPE html>`) and save it into a file named **`index.html`**.
2.  **Open in Browser:** Double-click the `index.html` file.

That's it! No server or complicated dependencies are required. It should open immediately in your default web browser.

## 💻 How to Use the Visualizer

1.  **Select Algorithm:** Choose the search strategy from the "Select Algorithm" dropdown (e.g., Uniform Cost Search).
2.  **Set Nodes:** Select the **Start Node** and **Goal Node** (defaults are A and M).
3.  **Adjust Settings (if necessary):**
    * For **DLS** and **IDDFS**, set the **Depth Limit**.
4.  **Start the Search:** Click the **`Start Search`** button.
    * The visualization will proceed automatically, highlighting the nodes as the algorithm explores the graph.
    * The process will pause when the goal is found or the search fails.
5.  **Review Results:** Check the **Final Result** section for the shortest path and total cost.
6.  **Reset:** Click **`Reset`** to clear the canvas and run a new search with different parameters or algorithms.

## 🛠️ Code Structure Overview

The code is organized into one monolithic file (`index.html`), but the JavaScript is modularized for clarity:

| Section | Description | Key Structures |
| :--- | :--- | :--- |
| **`graph` Object** | Defines the fixed graph, including node coordinates (`nodes`) and the directed, weighted edges (`edges`). | `{ nodes: {}, edges: {} }` |
| **`QueueItem` Class** | A simple class representing a state in the search: `node`, `path` array, `cost`, and `depth`. | `class QueueItem` |
| **`PriorityQueue` Class** | A custom implementation of a Priority Queue specifically used for **Uniform Cost Search** (prioritized by lowest cost). | `class PriorityQueue` |
| **`initializeSearchState()`** | Sets up the initial state, including the empty `visited` sets and the starting `frontier` structure (Array or Priority Queue) based on the selected algorithm. | `frontier` (Array/PQ), `visited` (Set) |
| **`stepSingleDirectional()`** | The core logic loop for BFS, DFS, DLS, and UCS. It handles dequeuing, goal checking, depth checking, and expanding neighbors. | `shift()`, `pop()`, `dequeue()` |
| **`stepIDDFS()`** | Handles the special loop logic for IDDFS, calling `stepSingleDirectional()` repeatedly and increasing the depth limit upon failure. | `currentIDDSLimit` |
| **`stepBidirectional()`** | Handles the alternating expansion logic for the forward and backward searches, and path reconstruction upon intersection. | `biStartQueue`, `biGoalQueue`, `biParents` |
| **`drawGraph()`** | Handles all canvas drawing logic, using `currentState` properties to determine node and edge colors (Visited, Frontier, Current, Path, Goal). | `ctx.arc()`, color logic |
| **`nextStep()` & `startSearch()`** | Controls the animation interval and flow of the program. | `setInterval` |

## Demo
https://swapnilgopale.github.io/Search-Algo-Visualizer/
