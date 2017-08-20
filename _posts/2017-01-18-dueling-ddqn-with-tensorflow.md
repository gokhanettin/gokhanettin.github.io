---
layout: post
title: "An artificial agent that can learn any game"
tags:
- Deep Learning
---

I have implemented a [Dueling Double Deep Q-Network][1]
using [TensorFlow][2] + [TFLearn][3] as a course project. It can learn
different [Atari 2600 games][4] from raw pixels and achieve a human-level success.
Furthermore, it does all these with no adjustment to the learning algorithm or
hyperparameters.

For those who have not heard about Deep Q-Networks (DQN), as [DeepMind][5]
states it is the first demonstration of a general-purpose agent that is able to
continually adapt its behavior without any human intervention, a major technical
step forward in the quest for general AI.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Ma1b6EeHlV0" frameborder="0" allowfullscreen></iframe>

To find out more, see [my git repository][6].

[1]: https://arxiv.org/pdf/1511.06581.pdf
[2]: https://www.tensorflow.org/
[3]: http://tflearn.org/
[4]: https://gym.openai.com/envs#atari
[5]: https://deepmind.com/research/dqn/
[6]: https://github.com/gokhanettin/dddqn-tf
