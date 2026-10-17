# Graph Coloring Problem using CodeEvolve Genetic Algorithm

## 1. Overview
This project solves the **Graph Coloring Problem** using **CodeEvolve**, an evolutionary genetic algorithm framework. The objective is to assign colors (Red, Blue, Green, White) to a 10-node graph such that no two connected (adjacent) nodes share the exact same color.

The program processes an uncolored arbitrary graph (left), executes an evolutionary search engine (center), and renders the solved, zero-conflict colored graph (right) matching the exact assignment screenshot.

---

## 2. File Structure & Prerequisites

### Files Included in Zip
* `codeevolve_graph_coloring.py`: The complete Python script containing the graph topology, CodeEvolve genetic algorithm engine, and Matplotlib visualization renderer.
* `README.md`: Instructions on how to run the code, how the algorithm operates, and how to interpret the results.

### Prerequisites
Make sure Python 3 is installed along with `matplotlib` for graphics rendering:
```bash
pip install matplotlib
```

---

## 3. How to Run the Code

### Option A: Running Locally (Terminal / Command Prompt)
1. Unzip the submission file and navigate to the project directory.
2. Execute the Python script:
   ```bash
   python codeevolve_graph_coloring.py
   ```
3. A popup window will display the side-by-side graph figure, and the terminal will output the console solution summary.

### Option B: Running in Google Colab
1. Open [Google Colab](https://colab.research.google.com).
2. Create a new notebook and paste the contents of `codeevolve_graph_coloring.py` into a code cell.
3. Run the cell (`Shift + Enter`) to view the interactive output and rendered graphs directly inside the notebook cell.

---

## 4. How the Code Works (Step-by-Step Execution)

The algorithm operates through four structured steps inside `codeevolve_graph_coloring.py`:

### Step 1: Graph Representation & Topology Mapping
The 10 nodes and 19 edges are defined using an adjacency list representing the exact geometric layout from the assignment image:
* **Nodes:** Mapped to normalized 2D coordinate positions (x, y).
* **Edges:** Mapped as pairs of connected node indices (u, v).
* **Gene Encoding:** Each candidate solution (chromosome) is an array of 10 integers representing color choices:
  `0 = White`, `1 = Blue`, `2 = Red`, `3 = Green`.

### Step 2: Fitness & Conflict Evaluation
For every candidate individual in the population, the algorithm calculates **Edge Conflicts**:
$$\text{Conflicts} = \sum_{(u, v) \in \text{Edges}} \mathbb{I}(\text{color}(u) == \text{color}(v))$$
$$\text{Fitness Score} = \frac{100}{1 + \text{Conflicts}}$$
An optimal solution requires **Total Edge Conflicts = 0**.

### Step 3: CodeEvolve Evolutionary Loop
The algorithm iterates through generations using biological evolution principles:
1. **Elitism:** The fittest individual of generation t is directly preserved into generation t+1 so solution quality never degrades.
2. **Tournament Selection (k=3):** Randomly picks 3 individuals and selects the one with the fewest edge conflicts as a parent.
3. **Single-Point Crossover:** Swaps sub-sequences of color assignments between two parent individuals at a random crossover point to create offspring.
4. **Bit-Flip Mutation:** With a probability of 8%, randomly mutates a node's color to explore new search spaces and prevent local minima traps.

### Step 4: Matplotlib Visualization Engine
Once a valid 0-conflict coloring is found (or maximum generations are reached), the script uses `matplotlib.pyplot` to draw:
* **Left Panel:** The uncolored input graph topology with empty white nodes.
* **Center Panel:** A dotted transition arrow representing the evolutionary search process.
* **Right Panel:** The solved output graph displaying the exact color assignments.

---

## 5. How to Interpret the Results

When execution finishes, the console prints an optimization summary, and a side-by-side plot opens:

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