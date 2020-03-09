# Mapping and localization questions

## What is the meaning of the Kalman gain?

The Kalman gain determines to what extent the measurement error corrects the state.
It is computed based on the state uncertainty and the measurement uncertainty.

## How does the EKF work?

1. Update state by applying nonlinear motion function.
2. Update state uncertainty by applying linearized motion model and motion noise.
3. Compute Kalman gain using state uncertainty, linearized measurement model, and measurement noise.
4. Update state using difference between actual and expected measurement and Kalman gain.
5. Update state uncertainty by applying Kalman gain.

## What is the computational complexity of the KF?

The computational complexity of the Kalman filter is governed by the matrix inversion that occurs when computing the Kalman gain.
The most efficient inversion algorithms achieve a computational complexity of O(d^2.4), where d is the dimensionality of the state.

## What is the unscented transform?

The unscented transform is a way to pass a Gaussian probability distribution through a nonlinear function.

It works as follows:

1. Sample sigma points in source domain in and around mean.
2. Pass sigma points through nonlinear function.
3. Fit Gaussian to sigma points in target domain.

## How does the UKF work?

1. Update robot pose mean by applying nonlinear motion function.
2. Update robot pose covariance by applying unscented transform and adding motion noise.
3. Compute linearized measurement model by sampling robot poses and passing them through measurement function.
4. Compute measurement uncertainty using linearized measurement model and measurement noise.
5. Compute Kalman gain from pose uncertainty and measurement uncertainty.
6. Update robot pose mean using measurement error and Kalman gain.
7. Update robot pose covariance using Kalman gain.

## What are the advantages of UKF over EKF?

* The UKF does not require computation of the Jacobian and can hence be used for non-differentiable motion and measurement models.
* The UKF produces slightly more accurate results for nonlinear models.

## What is the Markov assumption?

The Markov assumption states that given the current state of a dynamic system, all following states are independent of all past states.

## What is Markov localization?

Markov localization describes localization algorithms that assume Markov independence between observations.
That means that all observations can be explained by a map.
Markov localization cannot explain unexpected observations.

## What problems are often encountered in particle filtering?

| Problem | Reason |
| --- | --- |
| No accurate estimate | Too few particles, maybe due to curse of dimensionality |
| Hallway effect | Too few distinctive features to localize |
| Particle deprivation | Measurement model too confident |
| Non-deterministic behavior | Random sampling |

## How does EKF localization work?

In EKF localization, the state consists of the robot pose and the landmark positions.
The algorithm follows the steps below:

1. Update robot pose by applying nonlinear motion model.
2. Update robot uncertainty by applying linearized motion model and motion noise.
3. For each landmark,
    * compute Kalman gain using robot uncertainty, landmark uncertainty, linearized measurement model, and measurement noise,
    * update robot pose and landmark position using Kalman gain,
    * update robot and landmark uncertainty by applying Kalman gain.

## How does FastSLAM work?

FastSLAM combines particle filtering and EKF localization to perform SLAM.
From the outside, FastSLAM looks like a particle filter.
On the inside, every particle represents an EKF.
The state space of the EKF consists of the current robot pose and the landmark positions.
In addition to the EKF, each particle also stores all previous robot poses.
That way, each particle represents a robot trajectory hypothesis and a corresponding map estimate.

The particle filter performs the following steps:

1. For each particle, extend the path by sampling a new pose.
2. Compute the particle weights based on how well the mapped landmarks explain the current measurement.
3. Resample.
4. For each particle, update the belief of the observed landmarks via EKF.

## What is hierarchical GraphSLAM?

Hierarchical GraphSLAM leverages two facts:

1. The robot moves continuously and is not teleported.
2. The robot sensors have finite range.

Consequently, it is sufficient to update only the part of the graph that is currently relevant.
In order to do that, the graph is structured hierarchically.
The hierarchy is formed by iteratively grouping adjacent nodes and creating a simplified graph out of them.

Hierarchical graphs are designed for online mapping and localization.
