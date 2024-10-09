# Hierarchical Ad Hoc Agents (HAHA)
Code for [Hierarchical Reinforcement Learning for Ad Hoc Teaming](https://www.southampton.ac.uk/~eg/AAMAS2023/pdfs/p2337.pdf) and [Eyes on the Game: Deciphering Implicit Human Signals to Infer Human Proficiency, Trust, and Intent](https://arxiv.org/abs/2407.03298) Used to train a variety of agents for the overcooked domain and analyse their behavior through the lens of game play data and eye tracking data.  

Raw eye tracking and game play data can be found [here](https://o365coloradoedu.sharepoint.com/:f:/s/CS-HAI_Teaming_EyeGaze_Data/Eu2SJvmDzLlLvfAeNslGpwsBW0ytrFo9NYiZKQqt8jLGOQ?e=6PGD3B)

## Set up guide
1. Create conda environment:`conda create -n oai python=3.9`
2. Activate env: `conda activate oai`
3. Install [pytorch](https://pytorch.org/get-started/locally/) based on your use case
4. Run `pip install setuptools==65.5.0 pip==21`because gym 0.21 installation is broken with more recent versions
5. If using windows, run: `pip install pygetwindow`
6. Install overcooked-ai: `pip install git+https://github.com/StephAO/overcooked_ai.git`  
***Note***: The above repo is a modified version of the original [overcooked ai repo](https://github.com/HumanCompatibleAI/overcooked_ai)
7. Clone modified overcooked-ai repo: `git clone https://github.com/StephAO/HAHA.git'   
8. Move to repo dir: `cd HAHA`
9. Install this package: `pip install -e .`

## General Structure
- `oai_agents`: Main directory
  - `/agents`: Contains code related to creating and training agents: 
    - `/il.py`, `/rl.py`, and `/hrl.py` contain code for training an imitation learning, reinforcement learning, and hierarchical reinforcement learning respectively. 
    - `/base_agent.py` contains the abstract base class for the agent and trainer objects, including default save/load methods and interfacing methods
  - `/common`: Generally used functions and objects
    - `/arguments.py`: Code to parse cmd line args (and the defaults for many values)
    - `/networks.py`: All nn modules
    - `/overcooked_dataset.py`: Pytorch dataset wrapper for human play data used for il
    - `/state_encodings.py`: Code used to manipulate the state into agent obs
    - `/subtasks.py`: All code related to defining, identifying, and using subtasks
  - `/gym_environments.py`: Gym environments wrappers for main overcooked logic
    - `/base_overcooked_env.py`: Wrap main game logic with some additional functionality. Used to train rl agents.
    - `/manager_env.py`: Environment used to train manager component of hrl. Changes action space among other small things
    - `/worker_env.py`: Environment used to train worker component of hrl. Changes reward and start state among other small things
- `scripts`: Generally useful scripts
  - `/colosseum.py`: Have agents play with other agents for evaluation
  - `/run_overcooked_game.py`: Visualize agent-agent or human-agent team playing with each other
  - `/train_agents.py`: Functions to train different kinds of agents
- `eye_tracking_dataset_operations`: Scripts to process raw xdf files and likert scale files into useable datasets.

## Training agents
Refer to scripts/train_agents.py for examples on how to train different agent trainings.
If you've installed the package as above, you can run the script using:  
`python scripts/train_agents.py`

## Citation
If you use this repository in any way, please cite:  
```
@inproceedings{10.5555/3545946.3598926,
               author = {Aroca-Ouellette, St\'{e}phane and Aroca-Ouellette, Miguel and Biswas, Upasana and Kann, Katharina and Roncone, Alessandro},
               title = {Hierarchical Reinforcement Learning for Ad Hoc Teaming},
               year = {2023},
               isbn = {9781450394321},
               publisher = {International Foundation for Autonomous Agents and Multiagent Systems},
               address = {Richland, SC},
               abstract = {When performing collaborative tasks with new unknown teammates, humans are particularly adept at adapting to their collaborator and converging toward an aligned strategy. However, state of the art autonomous agents still do not have this capability. We propose that a critical reason for this disconnect is that there is an inherent hierarchical structure to human behavior that current agents lack. In this paper, we explore the use of hierarchical reinforcement learning to train an agent that can navigate the complexities of ad hoc teaming at the same level of abstraction as humans. Our results demonstrate that when paired with humans, our Hierarchical Ad Hoc Agent (HAHA) outperforms all baselines on both the team's objective performance and the human's perception of the agent.},
               booktitle = {Proceedings of the 2023 International Conference on Autonomous Agents and Multiagent Systems},
               pages = {2337–2339},
               numpages = {3},
               keywords = {ad hoc teaming, hierarchical reinforcement learning, human agent collaboration, mutual adaptation, zero-shot coordination},
               location = {London, United Kingdom},
               series = {AAMAS '23}
}
```
and
```
@misc{hulle2024eyesgamedecipheringimplicit,
      title={Eyes on the Game: Deciphering Implicit Human Signals to Infer Human Proficiency, Trust, and Intent}, 
      author={Nikhil Hulle and Stéphane Aroca-Ouellette and Anthony J. Ries and Jake Brawer and Katharina von der Wense and Alessandro Roncone},
      year={2024},
      eprint={2407.03298},
      archivePrefix={arXiv},
      primaryClass={cs.HC},
      url={https://arxiv.org/abs/2407.03298}, 
}
```
