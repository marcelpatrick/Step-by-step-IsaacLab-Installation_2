# Step-by-step-IsaacLab-Installation_2

Source: https://github.com/isaac-sim/IsaacLab/discussions/3021

## Create a virtual environment
- Open Ubuntu CLI
- Create and Activate a Conda environment in Ubuntu with Python 3.11
```
conda create -n env_isaaclab python=3.11 -y
conda activate env_isaaclab
```

## Building Isaac Sim 5.0 from Source

- Clone the Isaac Sim repository
```
git clone https://github.com/isaac-sim/IsaacSim.git 
cd IsaacSim
```

- Install Git LFS and pull large files: Git LFS (Large File Storage) is an extension for Git that handles large binary files (like datasets, videos, models, or game assets) more efficiently.
```
sudo apt-get install git-lfs
git lfs install
git lfs pull
```

```
# Verify that GCC/G++ 11 is being used before building:
gcc --version
g++ --version
```

```
# Build
./build.sh
```

## Configs

- run the setup script which configures paths and dependencies
- You must run this every time you start a new terminal session before running Isaac Sim or Isaac Lab
- replace linux-x86_64 by your system's architecture
```
source _build/linux-x86_64/release/setup_conda_env.sh
```

## Using Isaac Lab with Isaac Sim 5.0

- Clone the IsaacLab repo inside the previously created IsaacSim folder
```
git clone https://github.com/isaac-sim/IsaacLab.git
cd IsaacLab
```

- Create a shortcut to the IsaacSim build
```
# Add symlink
ln -s ../IsaacSim/_build/linux-x86_64/release _isaac_sim
```

- Check and install all remaining dependencies, if any
```
sudo apt install cmake build-essential
```

- Install IsaacLab learning frameworks
```
./isaaclab.sh --install
```

## Create a new IsaacLab project

```
# From the Isaac Lab directory 
./isaaclab.sh --new
```
- Select task type (External/Internal), project path and name (myProject in this case) and resources to be used
```
External vs Internal: Determines if the project is meant to be built as a part of the isaac lab repository, or if it is meant to be loaded as an external extension.

Direct vs Manager: A direct task primarily contains all the implementation details within the environment definition, while a manager based project is meant to use our modular definitions for the different “parts” of an environment.

Framework: You can select more than one option here. This determines which RL frameworks you intend to natively use with your project (which specific algorithm implementations you want to use for training).
```

- to complete the installation process and register the environment, run:
```
# After following the steps prompted (see the Walkthrough for an example)
cd /root/IsaacSim/myProject
python -m pip install -e source/myProject
```

- Confirm that the environment was correctly setup in Isaac Lab
```
python scripts/list_envs.py
```
- this should print something like
```
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|                                                                   Available Environments in Isaac Lab                                                                    |
+--------+------------------------------+-------------------------------------------------------------+--------------------------------------------------------------------+
| S. No. | Task Name                    | Entry Point                                                 | Config                                                             |
+--------+------------------------------+-------------------------------------------------------------+--------------------------------------------------------------------+
|   1    | Template-Myproject-Direct-v0 | myProject.tasks.direct.myproject.myproject_env:MyprojectEnv | myProject.tasks.direct.myproject.myproject_env_cfg:MyprojectEnvCfg |
+--------+--------
```

## Test that the project was correctly created

### Classes and Configs
Source: https://isaac-sim.github.io/IsaacLab/main/source/setup/walkthrough/api_env_design.html

** When following the documentation, "isaac_lab_tutorial" should be replaced by your project name, in this case "myProject"

- Open an Ubuntu terminal
- Activate the conda environment created with Python 3.11 ```conda activate env_isaaclab```
- Navigate to ```cd ~/IsaacSim/myProject/source/myProject/myProject/tasks/direct/myproject```
- Check the environment configurations:
  - Open the config file (using Sublime in this example): ```subl myproject_env_cfg.py```
  - If you don't have sublime enabled, run: ```sudo snap install sublime-text --classic```
- Check the project environment file
  - Run ```subl myproject_env.py```




