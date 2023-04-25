# VariBAD

Code for the paper "[ContraBAR: Contrastive Bayes-Adaptive Deep RL]

```

```

> ! Important !
> 
> If you use this code with your own environments, 
> make sure to not use `np.random` in them 
> (e.g. to generate the tasks) because it is not thread safe 
> (and not using it may cause duplicates across threads).
> Instead, use the python native random function. 
> For an example see
> [here](https://github.com/lmzintgraf/varibad/blob/master/environments/mujoco/ant_goal.py#L38).

### Requirements

We use PyTorch for this code, and log results using TensorboardX.

The main requirements can be found in `requirements.txt`. 

For the MuJoCo experiments, you need to install MuJoCo.
Make sure you have the right MuJoCo version:
- For the Cheetah and Ant environments, use `mujoco150`. 
(You can also use `mujoco200` except for AntGoal, 
because there's a bug which leads to 80% of the env state being zero).
- For Walker/Hopper, use `mujoco131`.

For `mujoco131`, use: `gym==0.9.1 gym[mujoco]==0.9.1 mujoco-py==0.5.7`

### Overview

The main training loop for ContraBAR can be found in `metalearner_cpc.py`,
the models are in `models/`, the CPC set-up and losses are in `cpc.py` and the RL algorithms in `algorithms/`.

There's quite a bit of documentation in the respective scripts so have a look there for details.

### Running an experiment

To train ContraBAR on the gridworld from the paper, run

`python main.py --env-type gridworld_varibad`

which will use hyperparameters from `config/gridworld/args_grid_varibad.py`. 

To train contraBAR on the MuJoCo experiments use:
```
python main.py --env-type cheetah_dir_contrabar
python main.py --env-type cheetah_vel_contrabar
python main.py --env-type ant_dir_contrabar
python main.py --env-type walker_contrabar
```


The results will by default be saved at `./logs`, 
but you can also pass a flag with an alternative directory using `--results_log_dir /path/to/dir`.

The default configs are in the `config/` folder. 
You can overwrite any default hyperparameters using command line arguments.

Results will be written to tensorboard event files, 
and some visualisations will be printed every now and then.

