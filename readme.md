# Graph Coloring Problem using CodeEvolve Genetic Algorithm

An evolutionary algorithm implementation using **CodeEvolve** to solve the **Graph Coloring Problem** on a 10-node, 19-edge graph topology. 

The objective is to assign one of four colors (**Red**, **Blue**, **Green**, **White**) to every node in the graph such that no two connected (adjacent) nodes share the exact same color (0 edge conflicts).

---

## 1. Overview

This project processes an uncolored arbitrary graph (left), executes an evolutionary search engine using the **CodeEvolve** algorithm (center), and renders the solved, zero-conflict colored graph (right) matching the exact assignment screenshot.

In graph theory, the goal is to assign a color $c(v)$ to each vertex $v \in V$ for a graph $G = (V, E)$ such that:

$$
\forall (u, v) \in E, \quad c(u) \neq c(v)
$$

---

## 2. File Structure & Prerequisites

### Repository Files
* `codeevolve_graph_coloring.ipynb`: The Jupyter Notebook containing the graph topology definition, CodeEvolve genetic algorithm engine, and Matplotlib visualization renderer.
* `README.md`: Project documentation, execution steps, algorithm explanation, and result interpretation.

### Prerequisites
Ensure Python 3 is installed along with `matplotlib` for graphics rendering:
```bash
pip install matplotlib
```

---

## 3. How to Run the Code

### Option A: Running in Jupyter Notebook / VS Code
1. Clone or download the repository:
   ```bash
   git clone https://github.com/mwahabk/CodeEvolve_Graph_Coloring.git
   cd CodeEvolve_Graph_Coloring
   ```
2. Open `codeevolve_graph_coloring.ipynb` in Jupyter Notebook, JupyterLab, or VS Code.
3. Run all cells (`Shift + Enter` or **Run All**).
4. The notebook will output the optimization summary text and render the side-by-side graph visualization directly inline.

### Option B: Running in Google Colab
1. Open [Google Colab](https://colab.research.google.com).
2. Click **Upload** and select `codeevolve_graph_coloring.ipynb` (or import directly from the GitHub repository URL).
3. Run the notebook cells to execute the optimization process and view the inline graphical outputs.

---

## 4. How the Code Works (Step-by-Step Execution)

The algorithm operates through four structured steps inside `codeevolve_graph_coloring.ipynb`:

### Step 1: Graph Representation & Topology Mapping
The 10 nodes and 19 edges are defined using an adjacency list representing the exact geometric layout from the assignment image:
* **Nodes:** Mapped to normalized 2D coordinate positions $(x, y)$.
* **Edges:** Mapped as pairs of connected node indices $(u, v)$.
* **Gene Encoding:** Each candidate solution (chromosome) is an array of 10 integers representing color choices:
  `0 = White`, `1 = Blue`, `2 = Red`, `3 = Green`.

### Step 2: Fitness & Conflict Evaluation
For every candidate individual in the population, the algorithm calculates **Edge Conflicts**:

$$
\text{Conflicts} = \sum_{(u, v) \in \text{Edges}} \mathbb{I}(\text{color}(u) == \text{color}(v))
$$

$$
\text{Fitness Score} = \frac{100}{1 + \text{Conflicts}}
$$

An optimal solution requires **Total Edge Conflicts = 0** ($\text{Fitness} = 100.0$).

### Step 3: CodeEvolve Evolutionary Loop
The algorithm iterates through generations using biological evolution principles:
1. **Elitism:** The fittest individual of generation $t$ is directly preserved into generation $t+1$ so solution quality never degrades.
2. **Tournament Selection ($k=3$):** Randomly picks 3 individuals and selects the one with the fewest edge conflicts as a parent.
3. **Single-Point Crossover:** Swaps sub-sequences of color assignments between two parent individuals at a random crossover point to create offspring.
4. **Bit-Flip Mutation:** With a probability of $8\%$, randomly mutates a node's color to explore new search spaces and prevent local minima traps.

### Step 4: Matplotlib Visualization Engine
Once a valid 0-conflict coloring is found (or maximum generations are reached), the script uses `matplotlib.pyplot` to draw:
* **Left Panel:** The uncolored input graph topology with empty white nodes.
* **Center Panel:** A dotted transition arrow representing the evolutionary search process.
* **Right Panel:** The solved output graph displaying the exact color assignments.

---

## 5. How to Interpret the Results

When execution finishes, the notebook outputs an optimization summary followed by the rendered side-by-side plot:

### Console Summary Output
```text
==================================================
         CODEEVOLVE OPTIMIZATION SUMMARY          
==================================================
  Node  0 --> Blue
  Node  1 --> Red
  Node  2 --> White
  Node  3 --> White
  Node  4 --> Red
  Node  5 --> Blue
  Node  6 --> Green
  Node  7 --> White
  Node  8 --> Blue
  Node  9 --> Red
--------------------------------------------------
  Total Edge Conflicts : 0
  Generations Elapsed  : 14
==================================================
```

### Graphical Result Interpretation
1. **Zero Edge Conflicts:** Look at the `Total Edge Conflicts` output. A value of **`0`** guarantees that no two connected nodes share a border of the same color, proving that the solution is globally optimal.
2. **Color Topology Verification:**
   * **Top Node (0) & Bottom Node (5):** Colored **Blue**.
   * **Top-Left Node (1) & Bottom-Right Node (4):** Colored **Red**.
   * **Center Node (6):** Colored **Green**.
   * **Remaining Outer/Inner Nodes:** Colored **White**, **Blue**, or **Red** according to non-conflicting adjacent edges.