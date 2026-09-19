# ML-Agents in Unity

Followed along with the following course (during 2020): https://learn.unity.com/course/ml-agents-hummingbirds

This project uses Unity ML-Agents to train a hummingbird to fly through a 3D environment and collect nectar from flowers using Proximal Policy Optimization (PPO).

The agent learns entirely through interaction with the Unity physics environment rather than following a hard-coded path. It receives observations describing its orientation and the relative position of nearby flowers, then outputs continuous movement and rotation commands to control its flight.

The main parts of the project include:
- A 10-value observation space describing the bird's rotation, direction and distance to the nearest flower, and its alignment with the flower.
- A 5-value continuous action space controlling 3D movement, pitch, and yaw.
- Reward shaping that encourages the hummingbird to accurately position its beak inside a flower and penalizes leaving the environment.
- Randomized starting positions and flower orientations to improve generalization instead of allowing the policy to memorize a fixed environment.
- A PPO policy using a small neural network with LSTM memory for maintaining short-term information during an episode.
- Exporting the trained policy back into Unity so the hummingbird can run using real-time neural-network inference without the Python trainer.

The final environment includes a small game where a human-controlled hummingbird competes against the trained RL agent to collect nectar.

# Demo

Here is a [demo](https://drive.google.com/file/d/1-CSOH_CwHP10AW5N7tWk47Rv-1wR2vG2/view?usp=sharing) of me playing against the AI bird agent (I lose badly).
# Files

I uploaded some of the main files used to build and train the project, including the agent logic, environment scripts, training configuration, Unity scenes/assets, and trained model where applicable.

The most important files are:
- HummingbirdAgent.cs — observations, actions, rewards, and episode logic
- Flower.cs — flower and nectar behavior
- FlowerArea.cs — environment management and randomization
- GameManager.cs — game and episode control
- UIController.cs — UI logic
- trainer_config.yaml — PPO and neural-network training configuration
- Hummingbird.nn — trained policy used for inference

# Running the Project

The project was built with Unity 2020.3.25f1 and a compatible Unity ML-Agents setup, approximately ML-Agents Release 18 / Python mlagents 0.28.0.

To run the trained agent:
- Open the project in the compatible Unity version.
- Open the FlowerIsland scene.
- Make sure the trained Hummingbird.nn model is assigned to the ML-Agents Behavior Parameters component.
- Press Play in Unity.

To retrain the agent:
- Install the compatible Python mlagents package.
- Open the Training scene in Unity.

From the project directory, run: 

mlagents-learn config/trainer_config.yaml --run-id=hb_01

Once the trainer starts, press Play in Unity. 

ML-Agents will collect experience from the Unity simulation and train the PPO policy. 

The exported trained model can then be assigned back to the agent for inference inside Unity.
