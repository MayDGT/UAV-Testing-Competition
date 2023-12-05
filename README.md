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
<img src="/docs/algorithm.png" alt="our MCTS-based search algorithm" width="600"/>

Overall, our algorithm iteratively simulates the UAV and place obstacles on the trajectory of the UAV to block its way. Specifically, we manage our obstacle generation by using Monte-Carlo tree search (MCTS), in order to balance the exploration and exploitation during the search of the combinations of obstacles that can cause failures of the UAV. 

 

 
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
