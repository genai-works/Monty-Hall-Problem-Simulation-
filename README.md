# Monty Hall Problem Simulation - Jupyter Notebook

## Introduction

The Monty Hall Problem is a famous probability puzzle named after the host of the game show *Let's Make a Deal*. In this problem, a contestant is asked to pick one of three doors. Behind one door is a car (the prize), and behind the other two doors are goats. Once the contestant picks a door, the host—who knows what’s behind each door—opens one of the remaining doors, revealing a goat. The contestant is then given the choice to either stick with their original door or switch to the other unopened door. 

The puzzle is whether switching doors improves the contestant's chances of winning the car. Although it may seem counterintuitive, switching doors gives the contestant a higher probability of winning.

This project simulates the Monty Hall Problem in Python using a Jupyter notebook to demonstrate the probability behind the problem. The simulation compares two strategies:
1. **Stay Strategy**: The contestant sticks with their initial choice.
2. **Switch Strategy**: The contestant switches to the other unopened door after the host reveals a goat.

Through repeated simulations, we can demonstrate that the **switch strategy** consistently results in a higher probability of winning the car.

## Project Structure

This project consists of a Jupyter Notebook and Python code that simulates the Monty Hall Problem for both strategies and visualizes the results.

### Files:
- `monty_hall_simulation.ipynb`: The Jupyter notebook where the Monty Hall Problem simulation is implemented step by step.
- `README.md`: This readme file explaining the project and its components.

## Simulation Details

The notebook is divided into several parts:

### 1. **Importing Required Libraries**

We begin by importing the necessary libraries:
- `numpy`: for numerical operations (not heavily used in this problem but included for potential future extensions).
- `random`: for generating random choices during the simulation.
  
This step is crucial to ensure we have all the tools needed for the simulation.

```python
import numpy as np
import random
```

### 2. **The Stay Strategy**

We define the `monty_hall_stay()` function to simulate the Monty Hall Problem when the contestant **stays** with their initial door choice. In this strategy, the contestant:
- Picks a random door.
- The host reveals a goat behind another door.
- The contestant does **not switch** their choice.
  
The function returns `True` if the contestant wins (i.e., if the door they initially chose had the car behind it) and `False` otherwise.

```python
def monty_hall_stay():
    doors = [0, 1, 2]  # Door numbers
    car_door = random.choice(doors)  # Randomly place the car behind one door
    player_choice = random.choice(doors)  # Player makes an initial random choice
    
    available_doors = [door for door in doors if door != player_choice and door != car_door]
    host_opens = random.choice(available_doors)  # Host opens a door showing a goat
    
    return player_choice == car_door  # Return True if player wins, False otherwise
```

### 3. **The Switch Strategy**

The `monty_hall_switch()` function simulates the Monty Hall Problem when the contestant **switches** their choice after the host reveals a goat. In this strategy:
- The contestant picks a random door.
- The host reveals a goat behind another door.
- The contestant **switches** to the remaining unopened door.
  
The function returns `True` if the contestant wins (i.e., if the car is behind the door they switched to) and `False` otherwise.

```python
def monty_hall_switch():
    doors = [0, 1, 2]  # Door numbers
    car_door = random.choice(doors)  # Randomly place the car behind one door
    player_choice = random.choice(doors)  # Player makes an initial random choice
    
    available_doors = [door for door in doors if door != player_choice and door != car_door]
    host_opens = random.choice(available_doors)  # Host opens a door showing a goat
    
    remaining_door = [door for door in doors if door != player_choice and door != host_opens][0]
    
    return remaining_door == car_door  # Return True if player wins, False otherwise
```

### 4. **Simulating Both Strategies**

We define the `simulate_monty_hall()` function to simulate the Monty Hall Problem multiple times for both the "stay" and "switch" strategies. This function runs the game `n_trials` times for each strategy and tracks the number of wins.

It returns the win percentages for both strategies.

```python
def simulate_monty_hall(n_trials):
    stay_wins = 0
    switch_wins = 0
    
    for _ in range(n_trials):
        if monty_hall_stay():
            stay_wins += 1
        if monty_hall_switch():
            switch_wins += 1
    
    stay_win_rate = (stay_wins / n_trials) * 100
    switch_win_rate = (switch_wins / n_trials) * 100
    
    return stay_win_rate, switch_win_rate
```

### 5. **Running the Simulation**

The next step is to set the number of trials (`n_trials`) and run the simulation for both strategies.

```python
n_trials = 10000  # Set the number of trials
stay_win_rate, switch_win_rate = simulate_monty_hall(n_trials)

print(f"After {n_trials} trials:")
print(f"Win rate if you stay with your initial choice: {stay_win_rate:.2f}%")
print(f"Win rate if you switch your choice: {switch_win_rate:.2f}%")
```

### 6. **Visualizing the Results (Optional)**

Finally, for a clearer comparison, we can visualize the win rates of both strategies using a bar chart. The bar chart helps to demonstrate visually that switching doors results in a much higher chance of winning.

```python
import matplotlib.pyplot as plt

# Data for visualization
strategies = ['Stay', 'Switch']
win_rates = [stay_win_rate, switch_win_rate]

# Create bar plot
plt.bar(strategies, win_rates, color=['blue', 'green'])
plt.title('Monty Hall Problem: Stay vs Switch Strategy')
plt.xlabel('Strategy')
plt.ylabel('Win Rate (%)')
plt.show()
```

### Example Output

Running the simulation for `10,000` trials typically produces results like this:
```
After 10000 trials:
Win rate if you stay with your initial choice: 33.32%
Win rate if you switch your choice: 66.70%
```
The results clearly show that switching doors almost doubles the probability of winning.

## How the Monty Hall Problem Works

The Monty Hall Problem leverages conditional probability and can be counterintuitive at first. Here’s a simplified explanation:

- If you **stay** with your initial choice, your chance of winning is 1/3 (because only one of the three doors has the car behind it).
- If you **switch** after the host reveals a goat, your chance of winning is 2/3. This is because the host’s action of revealing a goat provides additional information, which shifts the probability in favor of the remaining unopened door.

## Requirements

To run this notebook, you need:
- **Python** (version 3.6 or higher)
- **Jupyter Notebook** installed
- The following Python libraries:
  - `numpy`
  - `matplotlib` (for visualization)
  
You can install the required libraries via pip:

```bash
pip install numpy matplotlib
```

## How to Run

1. Clone or download this repository.
2. Open the `monty_hall_simulation.ipynb` file in Jupyter Notebook.
3. Run the notebook step by step to simulate the Monty Hall Problem and visualize the results.

## Conclusion

This project demonstrates the Monty Hall Problem using a simple Python simulation. The key takeaway is that **switching doors** gives the contestant a significantly higher chance of winning the car compared to sticking with their initial choice. This problem has broader implications for understanding probability, decision-making, and counterintuitive results in real-world scenarios.

Feel free to explore and adjust the number of trials to see how the win percentages stabilize with more simulations.
