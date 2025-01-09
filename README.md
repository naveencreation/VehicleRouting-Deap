
# Vehicle Routing Problem (VRP) Solver using Genetic Algorithm

![VRP Solver Banner](https://via.placeholder.com/1200x400?text=Vehicle+Routing+Problem+Solver+%7C+Genetic+Algorithm)

## Overview
This project solves the **Vehicle Routing Problem (VRP)** using a **Genetic Algorithm (GA)** implemented with the DEAP Python library. It efficiently assigns a set of locations to multiple vehicles starting and ending at a central depot, minimizing the total distance traveled and ensuring balanced workload distribution among vehicles.

## Features
- **Genetic Algorithm**: Implements selection, crossover, and mutation to find optimized routes.
- **Multi-Objective Optimization**: Minimizes total distance and balances the workload among vehicles.
- **Dynamic Visualization**: Displays optimized routes with clear demarcation for each vehicle.
- **Customizable Parameters**: Easily adjust the number of vehicles, locations, and generations.

## Project Workflow
1. Randomly generate locations and assign a central depot.
2. Use a Genetic Algorithm to evolve population-based solutions.
3. Evaluate solutions based on total distance and workload balance.
4. Plot the best solution.

![Result Screenshot](result_screenshot.png)

## Installation

### Prerequisites
- Python 3.7+
- Libraries: `matplotlib`, `deap`, `numpy`

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/vrp-genetic-algorithm.git
   ```
2. Navigate to the project directory:
   ```bash
   cd vrp-genetic-algorithm
   ```
3. Install dependencies:
   ```bash
   pip install matplotlib deap numpy
   ```
4. Run the script:
   ```bash
   python vrp_solver.py
   ```

## Code Breakdown

### Key Components
1. **Locations and Depot**:
   - Randomly generated (x, y) coordinates for locations.
   - Central depot fixed at (50, 50).

2. **Genetic Algorithm Setup**:
   - **Fitness Function**: Minimizes total distance and balances vehicle workloads using standard deviation.
   - **Operators**: Uses partially matched crossover (PMX), shuffle mutation, and tournament selection.

3. **Visualization**:
   - Plots vehicle routes with unique colors and markers for each vehicle.

### Example Code Snippet
```python
# Genetic Operators
toolbox.register("mate", tools.cxPartialyMatched)  # PMX crossover
toolbox.register("mutate", tools.mutShuffleIndexes, indpb=0.05)  # Shuffle mutation

def evalVRP(individual):
    total_distance = 0
    distances = []
    for i in range(num_vehicles):
        vehicle_route = [depot] + [locations[individual[j]] for j in range(i, len(individual), num_vehicles)] + [depot]
        vehicle_distance = sum(np.linalg.norm(np.array(vehicle_route[k+1]) - np.array(vehicle_route[k])) for k in range(len(vehicle_route)-1))
        total_distance += vehicle_distance
        distances.append(vehicle_distance)
    balance_penalty = np.std(distances)
    return total_distance, balance_penalty
```

## Results
The Genetic Algorithm successfully finds an optimized set of routes for the vehicles, minimizing the total travel distance and balancing the workload. Below is a visual representation of the best solution:

![Best Route](result_screenshot.png)

## Usage
You can adjust the following parameters:
- `num_locations`: Number of locations (default: 20).
- `num_vehicles`: Number of vehicles (default: 4).
- `num_generations`: Number of generations for GA (default: 300).

## Roadmap
- [ ] Add support for real-world distance metrics (e.g., Google Maps API).
- [ ] Enhance visualization with interactive maps (e.g., Plotly).
- [ ] Implement time window constraints for advanced VRP.

## Contributing
Contributions are welcome! Feel free to fork the repository and submit a pull request.

## License
This project is licensed under the MIT License.

## Acknowledgments
- [DEAP Library](https://deap.readthedocs.io/)
- Genetic Algorithm concepts from [Wikipedia](https://en.wikipedia.org/wiki/Genetic_algorithm)

---

Made with ❤️ by [Your Name](https://github.com/yourusername)
