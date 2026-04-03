# Search Flights Engine

> **Project**
> <br />
> Course Unit: [Algoritmos e Estruturas de Dados](https://sigarra.up.pt/feup/pt/UCURR_GERAL.FICHA_UC_VIEW?pv_ocorrencia_id=501673), 2nd year
> <br />
> Course: Software Engineering / Computer Science
> <br />
> Faculty: **FEUP** (Faculty of Engineering of the University of Porto)
> <br />
> [Project Guidelines](https://github.com/franciscopana/Project2_AED2022/files/10368958/aed2223_trabalho2.pdf)
> <br />
> Project evaluation: **20**/20

---

## Project Goals

This project consists of a flight management system capable of processing and querying a dataset of global flights, airports, and airlines. The goal was to build an efficient search engine using **Graph Data Structures** to help users find optimal travel routes, analyze airport connectivity, and discover reachable destinations based on specific constraints (e.g., maximum layovers, preferred airlines, geographical radius).

## Technical approach

### 1. Graph Representation
* **Nodes (Airports):** Implemented via a hash table (`unordered_map`) for $O(1)$ lookup times. Each node holds an `Airport` object (containing coordinates, city, and country data) and a list of outgoing edges.
* **Edges (Flights):** Represent directed flights between airports. Each edge contains the destination airport, the distance between the two points, and a set of airlines that operate that specific route.

### 2. Search Algorithms & Routing
* **BFS (Breadth-First Search):** To find the best routes between two points, we implemented a BFS algorithm. This calculates the route with the **minimum number of flights**. If multiple routes have the same number of layovers, they are then sorted by the total distance covered. 
* **Haversine Formula:** Used to calculate the great-circle distance between coordinates, allowing the system to accurately measure flight distances and find nearby airports within a specific radius (e.g., 120km).
* **Flexible Origin/Destination Inputs:** The engine is highly flexible. Users can input:
  * Exact airport codes (e.g., `OPO`, `CDG`).
  * City names (finds all airports in or near the city).
  * Geographical coordinates (finds airports within a 120km radius).

### 3. Architectural Decisions
During development, we initially implemented **Dijkstra's Algorithm** to find the absolute shortest path by physical distance. However, we realized this lacked real-world applicability: Dijkstra would often suggest a route with 4 or 5 short flights just to save a few kilometers, instead of a direct flight. 

To solve this, we pivoted to a BFS-based approach that prioritizes **minimizing layovers first**, and then uses distance as a tie-breaker, which aligns much better with actual user preferences when booking flights.

### 4. Features & Interface
* **Flight Search:** Find routes between any two locations, optionally filtering by a specific set of airlines.
* **Airport Statistics:** Query detailed metrics for any airport, such as:
  * Number of flights departing.
  * Number of unique airlines operating.
  * Reachable cities/countries within a user-defined maximum number of layovers ($N$ flights).

## Running the code

**Setup & Compilation:**
The project uses CMake for building.

```bash
# Clone the repository
git clone https://github.com/yourusername/flight-search-engine
cd flight-search-engine

# Create a build directory and compile
mkdir build
cd build
cmake ..
make

# Run the executable
./trabalho2
```

*(Note: Ensure the `dataset` folder containing `airports.csv`, `airlines.csv`, `flights.csv`, and `worldcities.csv` is in the correct relative path when executing).*

## Tech stack

* **C++17** - Core logic and data structures.
* **CMake** - Build system.
* **Doxygen** - For generating API documentation.

## Team (Grupo 49)

* Adriano Machado
* Francisco Pires da Ana
* José Pedro Evans
