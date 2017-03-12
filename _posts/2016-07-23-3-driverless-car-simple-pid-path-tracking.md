---
layout: post
title: "3. Driverless Car - Simple PID - Path Tracking (variable desired speed)"
tags:
- Driverless Car
- PID controller
---

It is clear that if we properly slow down before taking a turn, we lower the
risk of driving out of the path. In order to achieve this, we need to be able to
change the desired speed by means of a speed recommendation.

Before implementing variable desired speed, I noticed the car length and
displacement per shaft revolution was measured wrong. I first corrected them and
then implemented a speed recommender. Each waypoint now has a desired speed. For
the time being, the speed recommender basically recommends these speeds as the
car moves from one waypoint to the next. The speed recommender can be further
extended with different sensors such as sonar, laser, camera, etc.

I also increased the steering PID loop frequency from 20 Hz to 40 Hz. Note that
the steering PID derivative coefficient in the real car slightly differs from
the simulation. This reduces the noise in steering.

<iframe width="560" height="315" src="https://www.youtube.com/embed/70_gBYIDxqU" frameborder="0" allowfullscreen></iframe>

To find out more how the car works, see [my git repository][2].

[2]: https://github.com/gokhanettin/driverless-car/tree/dec8ea910758346810a68bb474581f92bcb6ce48
