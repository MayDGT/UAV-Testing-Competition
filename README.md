# UAV-Testing-Competition
## Overview
This project is a fork of [skhatiri/UAV-Testing-Competition](https://github.com/skhatiri/UAV-Testing-Competition). It is an implementation of the **Monte Carlo Tree Search** (MCTS) algorithm 
with the goal of generating multiple obstacles to challenge the flight of Unmanned Aerial Vehicles (UAVs).

## Getting Started

* Following [this guide](https://github.com/skhatiri/Aerialist#using-hosts-cli) to install Aerialist project

* Install Aerialist's python package:
     * `pip3 install git+https://github.com/skhatiri/Aerialist.git`
       
* `cd Aerialist/samples` and clone this project

* Create some necessary directories:
     * `cd UAV-Testing-Competition/snippets`
     * `sudo mkdir -p logs generated_tests results/logs`
 
* Run the experiment:
     * `python3 cli.py generate case_studies/mission1.yaml 100`

## Description of the Algorithm

Overall, our algorithm iteratively simulates the UAV and places obstacles on the trajectories of the UAV to block its way. Specifically, we manage our obstacle generation by using Monte-Carlo tree search (MCTS), in order to balance the exploration and exploitation during the search. The psuedo code of our algorithm is presented as below.

<img src="/docs/algorithm.png" alt="our MCTS-based search algorithm" width="600"/>

The algorithm uses a word (i.e., a sequence of letters) to denote a set of obstacles, where each letter denotes an obstacle. These words are organized by using a tree structure during the search, each word corresponding to a path (thus a node) of the tree. For each node of the tree, we maintain several attributes, including $traj$, the trajectory of the simulation with the set of obstacles identified by the node, $R$, the reward of the node, and $T$, the (sub-)tree with the node as its root. 

Initially, the case of no obstacle is denoted by an empty word $\epsilon$, which is the root of the search tree. We simulate the UAV in this case and obtain a trajectory. Then, we iteratively call MCTS with the root node, as long as the budget is not used up. 

The function MCTS has an argument $w$, which denotes a node of the tree. In MCTS, firstly, it decides whether a new child of $w$ should be created (namely, whether a new obstacle should be added in the obstacle set $w$), according to the *progressive widening* condition and the depth of $w$. 
* If yes, it will generate a new obstacle $a$ by placing it on the trajectory from the simulation with $w$; then $w\cdot a$ becomes a child of $w$, which is simulated to obtain a new trajectory. If it causes a failure, we record this case. Then, we update the reward of $w\cdot a$, and record this new node by initializing a new sub-tree $T(w\cdot a)$.
* Otherwise, it just select an existing child of $w$ by *UCB1*, and call MCTS with the child node.

In either of the cases, the reward of $w$ will be updated as the maximum reward of the children, and the sub-tree with the root $w$ will also be updated to include the newly created nodes.

Both *progressive widening* and *UCB1* are used to balance the exploration and exploitation during the search, but they work in different stages of the search. *Progressive widening* is used to decide whether a variant of an existing obstacle should be generated, or a new obstacle should be added. *UCB1* is used to decide, when we add a new obstacle, which combinations of obstacles should it be added to. 



## Authors

* **Shuncheng Tang**
     * Email: scttt@mail.ustc.edu.cn
     * Affiliation: University of Science and Technology of China, China

* **Zhenya Zhang**
     * Email: zhang@ait.kyushu-u.ac.jp
     * Affiliation: Kyushu University, Japan

* **Ahmet Cetinkaya**
     * Email: ahmet@shibaura-it.ac.jp
     * Affiliation: Shibaura Institute of Technology, Japan
 
* **Paolo Arcaini**
     * Email: arcaini@nii.ac.jp
     * Affiliation: National Institute of Informatics, Japan
