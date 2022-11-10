# Where Am I ?

<p align="center">
  <img src="amcl.gif" alt="animated" style="width: 100%" />
</p>

This project showcases the application of Adaptive Monte Carlo Localization ROS package. AMCL is a particle filter algorithm that estimates the robot’s state and hence localises it in the global frame at any given time using the information provided to it about its environment in the form of a 2D map, odometery and a 2D Lidar sensor measurements

The Key idea of particles is that the probability density function of a robot’s pose can be very nonlinear and therefore Kalman filters cannot be used since it assumes gaussian distribution around the pose of the robot. This is where particle filters are helpful which allow us to approximate the probability distribution of robot’s on a map using  a finite number of pose estimate particles. 

Algorithm starts off by uniformly distributing the particles across the map where each particle is an independent estimate of the robot’s pose. When the robot moves, we estimate the robot’s new pose using the odometry and the robot model to estimate its new position a.k.a. dead reckoning. The new position is expected to get a certain measurement from the LIDAR sensor, which is then compared to what each particle sees from the position they are estimating. The particles whose estimated measurement is   closest to the actual measurement of the robot, are weighted higher than the other particles. The new weights of the particles help us better approximate the new estimated probability distribution of the pose on the map.

A new set of random particles are sampled( and hence Monte Carlo)from the new found approximate probability distribution which better predicts the actual position of the robot on a map. Each cycle of the sampling process produces more and more accurate estimates. 

After a few cycles, the probability distribution goes from being uniform all across the map to being a multimodal distribution of pose estimation. It therefore requires less number of particles to approximate the distribution across the map. The “Adaptive” word comes from the fact that AMCL is able to adjust the number of filter particles according to how certain it's about the particles pose i.e. the distribution goes from being uniform to multimodal to being bimodal and finally being unimodal. This adaptive nature helps algorithms to run faster as the computation decreases.

For more info check <http://wiki.ros.org/amcl>
