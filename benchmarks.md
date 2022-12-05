---
layout: page
title: Benchmarks
permalink: /benchmarks/
---

Twenty benchmark cases are released for the initial stage of the competition. Participants may download the benchmark cases [here](https://github.com/libai1943/TPCAP_benchmarks).

Each benchmark case is recorded in a file named “CaseX.csv,” where X ranges from 1 to 20. Each file contains an N-row-one-column vector, presenting the initial/goal pose of the ego vehicle together with the scenario layout. The details are presented as follows.

The first six rows of the vector record the initial and goal poses of the to-be-parked vehicle. Suppose the vector is V, and the element in its i-th row is V[i] (note that the index i begins from 1 rather than 0). We have x0 = V[1], y0 = V[2], θ0 = V[3], xf = V[4], yf = V[5], and θf = V[6]. As depicted in the figure below, (x0, y0) refers to the location of the vehicle’s rear-axle midpoint at the initial moment of the parking process; θ0 refers to the yaw angle of the vehicle at the beginning. Similar definitions are provided for xf, yf, and θf, which determine the vehicle poses at the end of the parking process.

![profile](/images/profile.jpg)

The seventh row of the vector, i.e., V[7], records the total number of obstacles in the parking scenario. The number of vertexes in the i-th obstacle is recorded in V[7 + i], where the index i ranges from 1 to V[7]. After that, the vertexes of each obstacle are presented by their 2D coordinate values in the x and y axes. Let us take the above figure as an example, the parking scenario containing two obstacles is defined by the vector V listed in the following table.

| Vector Index | Value |
| :----------: | :---: |
|     ...      |  ...  |
|     V[7]     |   2   |
|     V[8]     |   4   |
|     V[9]     |   4   |
|    V[10]     |  x11  |
|    V[11]     |  y11  |
|    V[12]     |  x12  |
|    V[13]     |  y12  |
|    V[14]     |  x13  |
|    V[15]     |  y13  |
|    V[16]     |  x14  |
|    V[17]     |  y14  |
|    V[18]     |  x21  |
|    V[19]     |  y21  |
|    V[20]     |  x22  |
|    V[21]     |  y22  |
|    V[22]     |  x23  |
|    V[23]     |  y23  |
|    V[24]     |  x24  |
|    V[25]     |  y24  |

In the aforementioned example, V[25] is the last element of the vector, thus N = 25.

To further assist in understanding the data format of the benchmark files, we provide scripts to display the obstacles and initial/goal poses for each benchmark case. The scripts are written in [Matlab](https://github.com/libai1943/TPCAP_demo_Matlab) or [Python](https://github.com/libai1943/TPCAP_demo_Python). Running the "RunMe" file in either repository would generate 20 figures like the following ones.

![benchmarks](/images/benchmarks.jpg)

Note the following:

(1) Vertexes of each obstacle are recorded in a sequence. Thus, connecting each vertex to its successor (successor of the last vertex is regarded as the first vertex) renders the contour of a polygonal obstacle. The vertexes in some obstacles are recorded in the clockwise direction while others are recorded in the counterclockwise direction. 

(2) Some polygonal obstacles are convex while others are concave. 

(3) Only static obstacles are introduced in this competition because handling moving obstacles involves trajectory prediction-related issues, which are not the focus of this competition. The absence of moving obstacles does not necessarily indicate that planning a path rather than a trajectory is enough. For example, a curvature-discontinuous path might still be feasible if an appropriate velocity profile is attached to it. Hence, simply scoring on paths is unfair. 

(4) The ego vehicle should avoid colliding to obstacles, but traveling far away from obstacles is unnecessary and thus is ignored in our score rules. At this point, requiring that the ego vehicle keeps far away from obstacles is useful when the obstacle location cannot be accurately obtained but this competition holds the assumption of perfect perception. 
