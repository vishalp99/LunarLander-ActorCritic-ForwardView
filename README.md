# LunarLander-ActorCritic-ForwardView
This repository contains the implementation of the **Actor-Critic (Forward View)** reinforcement learning algorithm applied to the **LunarLander-v2/v3 environment** from OpenAI Gymnasium. 

## Project Overview

The goal of this project is to understand and apply the **policy gradient Actor–Critic method** to land a lunar module safely between two flags in the LunarLander environment.

The project includes:

- Exploration of the state and action space  
- Design and implementation of **Actor** (policy) and **Critic** (value) networks  
- Forward-view TD learning  
- Policy gradient updates  
- Performance evaluation and comparison with a baseline random policy  

---

## Environment Details

### **Environment:** `LunarLander-v2` / `LunarLander-v3`  
### **State Space (8-dimensional):**
- X and Y position  
- X and Y velocity  
- Lander angle & angular velocity  
- Leg contact indicators (left & right)

### **Action Space (Discrete – 4 actions):**
- `0` – Do nothing  
- `1` – Fire left engine  
- `2` – Fire main engine  
- `3` – Fire right engine  

### **Reward Highlights**
- Negative reward for fuel usage  
- Positive reward for moving toward landing zone  
- Large reward for successful landing  
- Negative reward for crashing  
- Positive reward if each leg touches the ground  

---

## Neural Network Architecture

### **Actor Network (Policy)**
- Input: 8-dim state  
- Two hidden layers: 128 neurons each (ReLU)  
- Output: 4 logits → Softmax → Action probabilities  

### **Critic Network (Value)**
- Input: 8-dim state  
- Two hidden layers: 128 neurons each (ReLU)  
- Output: Scalar value: `V(s)`  

Both networks use **Adam** optimizer.

---

## Training (Actor–Critic, Forward View)

For each episode (1000 episodes total):

1. Observe state  
2. Select action using stochastic sampling from actor’s policy  
3. Execute step → receive reward and next state  
4. Compute **TD Target**  
5. Compute **Advantage**  
6. Update **Critic** (MSE loss)  
7. Update **Actor** (policy gradient)  
8. Move to next state  

### **Hyperparameters**
| Parameter | Value |
|----------|-------|
| Actor LR | 0.0003 |
| Critic LR | 0.001 |
| Discount Factor γ | 0.99 |
| Episodes | 1000 |
| Max Steps/Episode | 1000 |

---

## Results

### **Trained Agent Performance (20-episode test)**
- **Mean Reward:** ~150–200  
- **Std Dev:** ~80–100  
- **Success Rate:** ~70–80%  

### **Baseline Random Policy**
- **Mean Reward:** −150 to −200  
- **Std Dev:** ~50–80  

Learning curves and comparison plots are included in the report.

---

## Challenges & Solutions

### **1. Catastrophic Forgetting**
Performance dropped after 300–400 episodes.  
✔ **Solution:** Lower learning rate → more stable updates.

### **2. Slow Critic Learning**
Critic values were unstable early in training.  
✔ **Solution:** Increased critic learning rate for faster convergence.

---

## Future Improvements

- Add batch normalization  
- Try different network sizes  
- Shared encoder for actor and critic  
- Parallel training environments (A2C style)  

---

## How to Run the Project

1. Clone the repository:

```bash
git clone <repo-url>
cd LunarLander-ActorCritic-ForwardView
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Start Jupyter Notebook:

```bash
jupyter notebook
```

4. Open the .ipynb file 

---