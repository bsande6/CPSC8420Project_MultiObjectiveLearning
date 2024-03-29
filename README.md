Brad Sanders
#CSPC8420 Project Phase 3
For this project I updated the existing PGMORL algorithm to select previously chosen tasks that demonstrated the best hypervolume and sparsity scores. The code for this can be found in the morl/morl.py file where the task selection algorithm is chosen as 'mix'. This calls the elite_prediction_guided_selection in the morl/population_2d.py file. The adjustments I made included tracking the fitness scores of the previous batch so that I could compare them to the newly selected batch chosen by the existing prediction guided selection. From here I could choose which of the previous elite tasks to keep by comparing the fitness scores. 

An example to run the new algorithm on the walker2d environment.

python scripts/walker2d-v2 --mix --num-seeds 1 --num-processes 1
 

# CPSC8420 Project Phase2
For this project I completed option B and extended an existing algorithm to a new environment.
This repository contains the implementation of the paper [Prediction-Guided Multi-Objective Reinforcement Learning for Continuous Robot Control] to the MountainCarContinuous environment from OPENAIGYM


## Installation

To run any mujuco environments please refer to the original repository at https://github.com/mit-gfx/PGMORL

#### Prerequisites

- **Operating System**: tested on Ubuntu 16.04 and Ubuntu 18.04.
- **Python Version**: >= 3.7.4.
- **PyTorch Version**: >= 1.3.0.

#### Install Dependencies

You can either install the dependencies in a conda virtual env (recomended) or manually. 

For conda virtual env installation, simply create a virtual env named **pgmorl** by:

```
conda env create -f environment.yml
```

## Run the Code

The training related code are in the folder `morl`. We provide the scripts in `scrips` folder to run our algorithm/baseline algorithms on each problem described in the paper, and also provide several visualization scripts in `scripts/plot` folder for you to visualize the computed Pareto policies and the training process. 

#### Train

The main entrance of the training code is at  `morl/run.py`. We provide a training script in `scripts` folder for each problem for you to easily start with. You can just follow the following steps to see how to run the training for each problem by each algorithm (our algorithm and baseline algorithms).

- Enter the project folder

  ```
  cd PGMORL
  ```

- Activate the conda env:

  ```
  conda activate pgmorl
  ```

- To run the algorithm on *Continuous_Mountain_Car-V2 for a single run:

  ```
  python scripts/continuous_mountain_car-v2 --pgmorl --num-seeds 1 --num-processes 1
  ```

  You can also set other flags as arguments to run the baseline algorithms (e.g. --ra, --moead, --pfa, --random). Please refer to the python scripts for more details about the arguments.

- By default, the results are stored in `results/[problem name]/[algorithm name]/[seed idx]`.

If an error regarding array dimensions occurs please uninstall and then reinstall numpy.

#### Visualization

- We provide a script to visualize the computed/downloaded Pareto results.

  ```
  python scripts/plot/ep_obj_visualize_2d.py --env MO-ContinuousMountainCar-v2 --log-dir ./results/Continuous_Mountain_Car-V2/pgmorl/0/
  ```

- We also provide a script to help you visualize the evolution process of the policy population.

  ```
  python scripts/plot/training_visualize_2d.py --env MO-ContinuousMountainCar-v2 --log-dir ./results/Continuous_Mountain_Car-V2/pgmorl/0/
  ```


## Acknowledgement
This code uses the repository  https://github.com/mit-gfx/PGMORL and extends it to the Continuous Mountain Car environment.
We use the implementation of [pytorch-a2c-ppo-acktr-gail](https://github.com/ikostrikov/pytorch-a2c-ppo-acktr-gail) as the underlying PPO implementation and modify it into our Multi-Objective Policy Gradient algorithm.



## Citation from PGMORL

@inproceedings{xu2020prediction,
  title={Prediction-Guided Multi-Objective Reinforcement Learning for Continuous Robot Control},
  author={Xu, Jie and Tian, Yunsheng and Ma, Pingchuan and Rus, Daniela and Sueda, Shinjiro and Matusik, Wojciech},
  booktitle={Proceedings of the 37th International Conference on Machine Learning},
  year={2020}
}



