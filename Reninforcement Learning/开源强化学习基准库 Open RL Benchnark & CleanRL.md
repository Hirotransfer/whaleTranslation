# 开源强化学习基准库 Open RL Benchnark @ 0.3.0

## Open RL Benchnark @ 0.3.0 发布

从Open RL Benchmark @ 0.3.0（http://benchmark.cleanrl.dev）发布以来，它以前所未有的透明度、开放性和可复用性对34歀以上的游戏进行了基准测试。

Open RL Benchmark检查了我们的单文件实现DRL算法的性能，如PPO、DQN、TD3和DDPG在各种不同游戏（Atari、Mujoco、Pybullet、自对弈领域、实时策略游戏）中的表现。

我们称它为Open RL Benchmark，因为它的所有内容都是开放的。你可以查看源代码，超参数，训练指标，如各种损失，日志，智能体在整个训练过程中玩游戏的视频。同时Open RL Benchmark确保我们的工作是高质量的。它是为个人研究和小型实验室而生的。

## CleanRL 助力 RL 算法的清晰实现

CleanRL致力于成为最人性化的强化学习库。它的实现清晰、简单、自成一体，你不必翻阅几十个文件就能明白是怎么回事。只需要阅读、打印出一些东西，你就可以轻松定制。CleanRL的单文件实现使得我们的代码库非常容易理解和定制研究。同时，CleanRL试图供给许多有利于研究的功能，如云实验管理、支持连续和离散的观察和行动空间、游戏玩法的视频记录等。这些功能对于做研究会有很大的帮助，尤其是视频录制功能，可以让你直观地检查智能体在训练的各个阶段的行为。 

## 研究 RL 所需考虑的五个方面

当我开始做DRL研究的时候，我很难找到一个合适的库来做RL研究。我主要考虑了以下五个方面：

- (1) 可理解性和可破解性
- (2) 质量
- (3) 速度
- (4) 实验管理
- (5) 可扩展性

一方面。类似于“大教堂”式的库，如openai/baselines、ray-project/ray的rlib、tensorflow/agents。它们通常质量高、速度快，满足（2,3）。

然而，要完全理解它们的代码和所有的活动部件通常是一件棘手的事情。openai/baselines在PPO上的实现就是一个例子，所有相关的实现细节都散落在11个文件中（参见https://costa.sh/blog-the-32-implementation-details-of-ppo.html）。

虽然作为库的设计者，重用许多功能可能是有意义的，但它的模块化设计很多时候可能会成为初学者理解的障碍。这可能会使它很难为研究而定制，不满足(1)。

另一方面，也有像seungeunrho/minimalRL、higgsfield/RL-Adventure这样的 "集市 "库。它们写得整齐、紧凑、易懂，满足(1)，但可能只适用于某一特定游戏，不满足(2)，有时也会满足(3)。

也许更重要的是，"大教堂 "和 "集市 "似乎并没有把太多的精力放在实验管理上（4）。也就是说，如果我有一个要测试的想法，我如何管理它的相关源代码(我是否要克隆repo?)和实验结果(我是否要保存在csv文件中?)。

这本质上是一个成熟的wrokflow的问题：如何快速从想法到验证和生产。此外，很少看到关于如何利用AWS等云服务商进行大规模实验的指南，没有妥善解决（5）。

CleanRL提供了高质量的DRL算法的单文件实现。由于所有的算法细节都自成一体，因此（1）得到了解决。由于我们在各种游戏上对算法进行了基准测试，所以解决了(2)。

由于我们使用`weights_biases`来记录实验，所以(4)得到了解决。它真的很神奇，我们确切地知道哪些文件是负责结果的，它的工具允许我们对实验进行分类、分组和过滤。挖掘洞察力和管理版本明显更容易。

最后，我们对`Docker`和`AWS Batch`的使用可以同时运行数千个实验，解决了（5）。同时，我们能够做一些以前无法想象的实验，这对工作流程来说是一个彻底的模式转变。

例如，我们现在实际上可以进行超参数调优，用更多的随机种子运行，用更多的游戏来检验稳定性。

总而言之，CleanRL让我们可以轻松地实验新的想法，管理实验，并扩展到做非凡的实验量。我们的Open RL Benchmark就是一个展示CleanRL强大潜力的例子。

我们希望更多有兴趣的研究者使用CleanRL进行RL研究，因为它提供了一个适合个人研究和小型实验室的良好工作流程。

## 项目亮点

> 该项目的WIP当前版本为0.2.1，预计会有重大更改。

这个项目是WIP，目前是0.2.1版本，预计会有突破性的变化。

这个repo的亮点特点是：

- 我们的实现在一个文件中自成一体. 关于算法的一切都在那里! 易于理解和做研究。
- 使用Tensorboard轻松记录训练过程，并与wandb.com集成，在云端记录实验。查看https://cleanrl.costa.sh。
- 能够直接在Python的交互式shell中进行调试(特别是如果你使用Anaconda的Spyder编辑器)。
- 简单的使用命令行参数进行超参数调整；不需要复杂的配置文件。

## 基准实现

我们的实现是经过基准测试的，以确保质量。我们使用 wandb 记录所有的基准实验，这样你就可以检查超参数、代理玩游戏的视频以及重现游戏的精确命令。参见https://cleanrl.costa.sh。

目前wandb的仪表盘不允许我们在同一个面板上显示所有游戏中的代理性能，所以你必须在https://cleanrl.costa.sh 中点击每个面板来查看基准化性能，这有时会很不方便。所以我们另外发布了使用seaborn的每款游戏的基准性能，如下所示（结果是使用benchmark/plot_benchmark.py（https://github.com/vwxyzjn/cleanrl/blob/master/benchmark/plot_benchmark.py）创建的。



<img src="http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/legend.svg">



|                 Benchmarked Learning Curves                  |                            Atari                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|               衡量标准、日志和录制的视频在☞：                | [cleanrl.benchmark/reports/Atari](https://app.wandb.ai/cleanrl/cleanrl.benchmark/reports/Atari--VmlldzoxMTExNTI) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/QbertNoFrameskip-v4.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/BeamRiderNoFrameskip-v4.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/SpaceInvadersNoFrameskip-v4.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/PongNoFrameskip-v4.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/BreakoutNoFrameskip-v4.svg) |                            &nbsp;                            |

|                         基准学习曲线                         |                            Mujoco                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|               衡量标准、日志和录制的视频在☞：                | [cleanrl.benchmark/reports/Mujoco](https://app.wandb.ai/cleanrl/cleanrl.benchmark/reports/Mujoco--VmlldzoxODE0NjE) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Reacher-v2.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/InvertedPendulum-v2.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Hopper-v2.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Pusher-v2.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Striker-v2.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Thrower-v2.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Ant-v2.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/HalfCheetah-v2.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Walker2d-v2.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Swimmer-v2.svg) |

![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Humanoid-v2.svg)

|                         基准学习曲线                         |                           Pybullet                           |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|               衡量标准、日志和录制的视频在☞：                | [cleanrl.benchmark/reports/PyBullet-and-Other-Continuous-Action-Tasks](https://app.wandb.ai/cleanrl/cleanrl.benchmark/reports/PyBullet-and-Other-Continuous-Action-Tasks--VmlldzoxODE0NzY) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/InvertedDoublePendulumBulletEnv-v0.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/MinitaurBulletDuckEnv-v0.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/AntBulletEnv-v0.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/HopperBulletEnv-v0.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/InvertedPendulumBulletEnv-v0.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/MinitaurBulletEnv-v0.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/PusherBulletEnv-v0.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Walker2DBulletEnv-v0.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/HalfCheetahBulletEnv-v0.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/HumanoidBulletEnv-v0.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Pendulum-v0.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/LunarLanderContinuous-v2.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/MountainCarContinuous-v0.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/BipedalWalker-v3.svg) |

|                         基准学习曲线                         |                           经典控制                           |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|               衡量标准、日志和录制的视频在☞：                | [cleanrl.benchmark/reports/Classic-Control](https://app.wandb.ai/cleanrl/cleanrl.benchmark/reports/Classic-Control--VmlldzoxODE0OTQ) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/CartPole-v1.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/Acrobot-v1.svg) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/LunarLander-v2.svg) | ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/MountainCar-v0.svg) |



|                         基准学习曲线                         |                       其他 (实验领域)                        |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|               衡量标准、日志和录制的视频在☞：                | [cleanrl.benchmark/reports/Others](https://app.wandb.ai/cleanrl/cleanrl.benchmark/reports/Others--VmlldzoxODg5ODE) |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/BipedalWalkerHardcore-v3.svg) | 这是一个相当具有挑战性的连续动作任务，通常需要100M以上的时间步数才能解决。 |
| ![](http://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/SlimeVolleySelfPlayEnv-v0.svg) | 这是一个来自https://github.com/hardmaru/slimevolleygym 的自对弈环境，所以它的情节奖励（`episode reward`）应该不会稳定增加。参看视频中智能体的实际表现（即去看看[cleanrl.benchmark/reports/Others](https://app.wandb.ai/cleanrl/cleanrl.benchmark/reports/Others--VmlldzoxODg5ODE)）。 |
| ![](https://microrts.s3.amazonaws.com/microrts/cleanrl/open-rl-benchmark/0.3/plots/MicrortsCombinedReward10x10F9BuildCombatUnits-v0.svg) | 这是一个MicroRTS环境，建立尽可能多的作战单位，参见https://github.com/vwxyzjn/gym-microrts。可通过运行https://github.com/vwxyzjn/gym-microrts/blob/master/experiments/ppo.py得到，另外还实现了无效的动作掩饰（`invalid action masking`）和处理PPO的多离散动作空间（`multi-discrete action space`）。 |

## 算法实现

- [x] ~~Advantage Actor Critic (A2C)~~
  * 由于A2C是PPO的特殊情况，当设置`update-epochs=1`时，被剪掉的目标实质上变成了A2C的目标，所以我们忽略了A2C的实现。出于教育的目的，后期可能会加入进来。但是，我们在`experiments`文件夹中保留了旧的A2C实现。
    * [experiments/a2c.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/experiments/a2c.py)
      * (不建议使用)用于离散动作空间。
    * [experiments/a2c_continuous_action.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/experiments/a2c_continuous_action.py)
      * (不建议使用)用于连续动作空间。
- [x] 深度Q学习 (DQN)
  * [dqn.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/dqn.py)
    * 对于离散的行动空间。
  * [dqn_atari.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/dqn_atari.py)
    * 用于玩`Atari`游戏。它使用卷积层和常见的基于`Atari`的预处理技术。
  * [dqn_atari_visual.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/dqn_atari_visual.py)
    * 为`dqn_atari.py`添加q值可视化。
- [x] 类别型 DQN (C51)
  * [c51.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/c51.py)
    * 对于离散的行动空间。
  * [c51_atari.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/c51_atari.py)
    * 用于玩`Atari`游戏。它使用卷积层和常见的基于`Atari`的预处理技术。
  * [c51_atari_visual.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/c51_atari_visual.py)
    * 为`dqn_atari.py`添加返回值和q值可视化。
- [x] 近似策略梯度(PPO) 
  * 以下所有的PPO实现都经过了一些代码级的优化。更多细节请参见https://costa.sh/blog-the-32-implementation-details-of-ppo.html。
  * [ppo.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/ppo.py)
    * 对于离散的行动空间。
  * [ppo_continuous_action.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/ppo_continuous_action.py)
    * 对于连续动作空间。还实现了Mujoco特有的代码级优化。
  * [ppo_atari.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/ppo_atari.py)
    * 用于玩`Atari`游戏。它使用卷积层和常见的基于`Atari`的预处理技术。
  * [ppo_atari_visual.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/ppo_atari_visual.py)
    * 为`ppo_atari.py`添加动作概率可视化。
  * [experiments/ppo_self_play.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/experiments/ppo_self_play.py)
    * 为https://github.com/hardmaru/slimevolleygym 实现了一个自对弈的智能体。
  * [experiments/ppo_microrts.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/experiments/ppo_microrts.py)
    * 为https://github.com/vwxyzjn/gym-microrts 实现无效的动作掩饰和处理多个离散动作空间。
  * [experiments/ppo_simple.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/experiments/ppo_simple.py)
    * (不建议使用)离散动作空间的Naive实现。我把它保留在这里是出于教育目的，因为我觉得如果大多数人只是读了论文就会实现这个，通常不知道调整好的PPO implmentation会有大量的实现细节。
  * [experiments/ppo_simple_continuous_action.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/experiments/ppo_simple_continuous_action.py)
    * (不建议使用)连续动作空间的Naive实现。
- [x] 软行为-评论家 (SAC)
  * [sac_continuous_action.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/sac_continuous_action.py)
    * 对于连续的行动空间。
- [x] 深度确定性策略梯度 (DDPG)
  * [ddpg_continuous_action.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/ddpg_continuous_action.py)
    * 对于连续的行动空间。
- [x] 双延时深度确定性策略梯度(TD3)
  * [td3_continuous_action.py](https://github.com/vwxyzjn/cleanrl/blob/master/cleanrl/td3_continuous_action.py)
    * 对于连续的行动空间。

##  CleanRL 与稳定的基准（baselines）进行比较

稳定的基准（stable-baselines）是openai/baselines repo的一次精彩重构，有更多的文档和更好的组织。

Stable-baselines 3计划对核心代码库进行更好的重构。CleanRL与stable-baselines和stable-baselines3有几个不同之处：

- （1）CleanRL提供了单文件实现，而他们的设计则明显更加模块化。虽然一般来说模块化受到高度评价，但我们的单文件实现使得实验管理和版本跟踪更加直接。也就是说，我们知道只有一个文件负责算法的结果，而不是整个repo中的几十个文件。此外，在单个文件的设置下，添加新的功能是相对容易的，因为我们不必适应现有的模块化设计。
- （2）CleanRL提供了一个意见实验管理范式，使用`权重`和`偏置`来记录所有指标和智能体玩游戏的视频。
- （3）CleanRL具有直接的`云端支持`。我们只需将脚本打包成docker容器，然后使用AWS Batch进行扩展，这也是稳定基准可以轻松做到的事情，但目前似乎还没有过多的开发。

Open RL Benchmark可以看作是类似于araffin/rl-baselines-zoo。Open RL Benchmark没有提供调整好的超参数和训练好的游戏模型，而是在整个训练过程中提供训练指标、系统使用情况、日志和一系列智能体玩游戏的视频。个人认为这些视频基本上是在做与训练模型相同的工作，以达到评估的目的。



参考链接：

https://www.reddit.com/r/MachineLearning/comments/i2bvrr/p_open_rl_benchmark_030_benchmarkcleanrldev_7/



视频展示：

https://streamable.com/cq8e62



Github网址：

https://github.com/vwxyzjn/cleanrl
