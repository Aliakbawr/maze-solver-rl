## Project Structure

- **main.py**: The main script that initializes the environment, implements the Q-learning algorithm, and plots the results.
- **requirements.txt**: Lists the required Python packages for the project.

## Installation

1. **Clone the repository**:
    ```sh
    git clone https://github.com/yourusername/maze-solver-rl.git
    cd maze-solver-rl
    ```

2. **Create a virtual environment** (optional but recommended):
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3. **Install the required packages**:
    ```sh
    pip install -r requirements.txt
    ```

## Dependencies

- `numpy`: For numerical operations.
- `gym`: For creating the maze environment.
- `matplotlib`: For plotting the results.
- `gym_maze`: For the specific maze environment.

Install dependencies with:
```sh
pip install numpy gym matplotlib gym_maze
```

## Usage

Run the main script to start training the agent:
```sh
python main.py
```

The script performs the following steps:

1. **Environment Initialization**:
    ```python
    env = gym.make("maze-random-10x10-plus-v0")
    observation = env.reset()
    ```

2. **Q-table Initialization**:
    ```python
    num_actions = env.action_space.n
    Q = np.zeros((100, num_actions))
    ```

3. **Q-learning Parameters**:
    ```python
    alpha = 0.1  # Learning rate
    gamma = 0.9  # Discount factor
    epsilon = 0.99  # Epsilon-greedy parameter
    min_epsilon = 0.1  # Minimum epsilon value
    epsilon_decay = 0.99  # Epsilon decay rate
    ```

4. **Training Loop**:
    The agent is trained over `NUM_EPISODES` episodes. In each episode, the agent interacts with the environment, updates the Q-table, and decays the epsilon value.

5. **Plotting Results**:
    After training, the script plots the number of episodes between successful maze completions.

## Q-learning Algorithm

- **State Representation**: The state is represented as a single integer by combining the x and y coordinates of the agent's position in the maze.
    ```python
    state = int(state[0] * 10 + state[1])
    ```

- **Action Selection**: Actions are selected using an epsilon-greedy strategy. Initially, actions are chosen randomly to encourage exploration, but over time, the agent increasingly exploits its learned knowledge.
    ```python
    action = np.argmax(Q[state])  # Greedy action based on Q-values
    ```

- **Q-value Update**: The Q-value for the state-action pair is updated based on the reward received and the maximum Q-value of the next state.
    ```python
    Q[state][action] += alpha * (reward + gamma * np.max(Q[next_state]) - Q[state][action])
    ```

## Results

The winning rate is printed at the end of the training process, and a plot showing the episodes between successful completions is displayed.

## Closing the Environment

The environment is closed at the end of the script to free up resources:
```python
env.close()
```
