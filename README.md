This code implements an AI-driven architectural design tool that uses Deep Reinforcement Learning (DRL) to automatically generate residential floor plans.

Unlike a simple random generator, this script acts as a "mini-architect" that learns over time how to arrange rooms to be as compact and accessible as possible.



 🧠 Core Components

 1. The Reward Shaper (`CompactAccessibleRewardShaper`)

This is the "brain" of the operation. It defines the rules of what makes a house "good" using a scoring system:

 Compactness: High scores for using most of the plot area and minimizing "wasted" gaps between rooms.
 Accessibility: Points are awarded for connectivity (shared walls) and the creation of a central hub (like a hallway or living room) that connects many rooms.
 Residential Logic: It uses "Architectural DNA" to reward logical pairings—like putting the Kitchen near the Dining Room or the Bedroom near the Bathroom—while penalizing illogical ones.
 Penalties: It heavily docks points for overlapping rooms or creating extremely thin, "un-livable" room shapes.

 2. The AI Agent (`DQNAgent` & `LayoutQNetwork`)

If PyTorch is installed, the code initializes a Deep Q-Network (DQN).

 State: The AI looks at the current layout (what rooms are placed, how much space is left, and what room is next).
 Action: It decides on the best coordinates  on a  grid to place the next room.
 Learning: Through "episodes" (trial-and-error runs), the agent stores its successes and failures in memory to improve its placement strategy in the next round.

 3. The Layout Engine (`CompactHouseGenerator`)

This manages the physical constraints of the house:

 Automatic Sizing: You don't have to specify room dimensions. It calculates "Target Areas" based on the total plot size (e.g., a Kitchen is usually ~12% of a house).
 Validation: It ensures no room is placed outside the plot boundaries and handles the sorting of rooms (placing larger rooms first to optimize "packing").



 🛠 How It Works (The Workflow)

1. Input: You provide the total plot area (e.g., 1200 sq ft) and the list of rooms you want (e.g., 2 Bedrooms, 1 Kitchen).
2. Training: The AI runs hundreds of simulations (Episodes). In early episodes, the layouts are messy. By the later episodes, the trend-line usually rises as the AI discovers that clustering rooms together yields higher rewards.
3. Output:  JSON Data: A structured list of room coordinates and sizes.
 Visualization: A colorful floor plan map showing room placements and generated doors (represented by circles) where rooms share a wall.





 🚀 Key Features

 Adaptive Design: It can handle various plot aspect ratios (Square, 4:3, 3:2, etc.).
 Functional Zoning: It attempts to separate "Private" zones (Bedrooms) from "Public" zones (Living rooms).
 Fallbacks: If you don't have PyTorch, it falls back to a rule-based random placement strategy, though this is significantly less "intelligent."
