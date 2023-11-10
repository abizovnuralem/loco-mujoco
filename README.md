# LocoMuJoCo

![LocoMujoco7_small](https://github.com/robfiras/loco-mujoco/assets/69359729/6b3a6134-34e7-41a9-a75b-ce4f3e902601)


**LocoMuJoCo** is an **imitation learning benchmark** specifically targeted towards **locomotion**. It encompasses a diverse set of environments, including quadrupeds, bipeds, and musculoskeletal human models, each accompanied by comprehensive datasets, such as real noisy motion capture data, ground truth expert data, and ground truth sub-optimal data,
enabling evaluation across a spectrum of difficulty levels. 

**LocoMuJoCo** also allows you to specify your own reward function to use this benchmark for **pure reinforcement learning**! Checkout the example below!

### Key Advantages 
✅ Easy to use with [Gymnasium](https://github.com/Farama-Foundation/Gymnasium) or [Mushroom-RL](https://github.com/MushroomRL/mushroom-rl) interface \
✅ Many environments including humanoids and quadrupeds \
✅ Diverse set of datasets --> e.g., noisy motion capture or ground truth datasets with actions \
✅ Wide spectrum spectrum of difficulty levels \
✅ Built-in domain randomization \
✅ Many baseline algorithms for quick benchmarking 

---

## Installation

To install this repository, clone it and then run:

```bash
cd loco-mujoco
pip install -e . 
```

Now you have to download and install the datasets by running

```bash
python download_datasets.py
```

If you also want to run the baselines, you have to install our imitation learning library [imitation_lib](https://github.com/robfiras/ls-iq). You find example files for training the baselines for any LocoMuJoCo task [here](examples/imitation_learning).

To verify that everything is installed correctly, run the examples such as:

```bash
python examples/simple_mushroom_env/example_unitree_a1.py
```

To replay a dataset run:

```bash
python examples/replay_datasets/replay_Unitree.py
```
---
## Environments & Tasks
You want a quick overview of all **environments**, **tasks** and **datasets** available? [Here](/loco_mujoco/environments) you can find it.

![LocoMujoco7_2_compressed](https://github.com/robfiras/loco-mujoco/assets/69359729/73ca0cdd-3958-4d59-a1f7-0eba00fe373a)

And stay tuned! There are many more to come ...

---
## Examples
LocoMuJoCo is very easy to use. Just choose and create the environment, and generate the dataset belonging to this task and you are ready to go! 
```python
import numpy as np
import loco_mujoco
import gymnasium as gym


env = gym.make("LocoMujoco", env_name="HumanoidTorque.run")
dataset = env.create_dataset()
```
You want to use LocoMuJoCo for pure reinforcement learning? No problem! Just define your custom reward function and pass it to the environment!

```python
import numpy as np
import loco_mujoco
import gymnasium as gym
import numpy as np


def my_reward_function(state, action, next_state):
    return -np.mean(action)


env = gym.make("LocoMujoco", env_name="HumanoidTorque.run", reward_type="custom",
               reward_params=dict(reward_callback=my_reward_function))

```

LocoMuJoCo *natively* supports [MushroomRL](https://github.com/MushroomRL/mushroom-rl):

```python
import numpy as np
import loco_mujoco

env = LocoEnv.make("HumanoidTorque.run")
dataset = env.create_dataset()
```

You can find many more examples [here](examples)

---
## Citation
```
@inproceedings{alhafez2023b,
title={LocoMuJoCo: A Comprehensive Imitation Learning Benchmark for Locomotion},
author={Firas Al-Hafez and Guoping Zhao and Jan Peters and Davide Tateo},
booktitle={6th Robot Learning Workshop, NeurIPS},
year={2023}
```

