# Perception Aware Planning Based on Feature Density Field and Global Optimization

## Motivation

- Currently we usually ignore the yaw angle in planning.
- Minimize state estimation error is very important for aerial vehicle.
- It is necessary to consider both task at hand and perception quality.
- It is valuable for improving recall rate of loop closure in SLAM (by looking toward feature rich region).

## Main Gap

Most method adapt a receding horizon strategy or model predictive control. In these methods, different poses of camera are sampled and the perception quality is evaluated using some pre-defined metric. 
- This is a greedy strategy and thus does not take global information into account, because it only do local planning in every horizon.
- The planned result depends on the number of samples. If too much poses are sampled, it is computationally expensive to evaluate all of them; if too less, the result is poor.
- I have not seen (maybe there are some) any works aimed at improving recall rate of SLAM by planning.

## Plan
- Building _feature density field_(FDF), in which we can query the density of SLAM feature at every point (x,y,z). This can be done efficiently using kd-tree and near neighbor serach.
- Do _global_ planning using the information of FDF, considering both (x,y,z) and _yaw_ angle. At each (x,y,z,yaw), we can calculate the pose of the camera and evaluate the total information density in the field of view. This is similar to do optimization is signed distance field, which is a global non-linear optimization problem.

