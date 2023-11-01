# Collision-Free Multi-UAV Path Finding (Fork from AMSwarm Repository)
这是一个基于MPC求解QP的方法，目的是快速生成2D/3D多智能体无碰撞轨迹（障碍物包括agent和obstacles）。为了更好地用这个方法对接到其它的工程中，我删掉了相应的ROS依赖、baselines（ACADO）代码，并且维护了直接将C++运行的采样结果可视化为gif动画的功能，便于查看轨迹效果。

## 基本使用方法
代码主要的依赖库安装
```sh
apt-get install nlohmann-json3-dev libeigen3-dev libboost-test-dev
```
写docker的同学可以参考这两句
```docker
RUN apt-get install -y doxygen graphviz libeigen3-dev libboost-test-dev
RUN cd /workspace && git clone --recursive https://github.com/superboySB/eigen-quadprog && cd eigen-quadprog && mkdir build && \
    cd build && cmake .. && make && make install && ln -s /usr/include/eigen3/Eigen /usr/include/Eigen
```
编译
```sh
mkdir -p build && cd build && cmake -DCMAKE_BUILD_TYPE=Release .. && make
```
运行MPC求解多机轨迹
```sh
./gen_traj
```
可视化轨迹
```sh
python animate_traj.py
```
## 默认运行效果
![](https://github.com/superboySB/AMSwarm/blob/main/docs/animate.gif)

## 注意事项
1. 经过检验，通常MPC的求解效果取决于两方面，一个是QP求解器的性能，还有一个是约束定义得是否合理，对于minimun snap trajectories来说，不合理的thrust配置很有可能会导致收敛变慢

## References
参考pybullet-drones的官方论文: Repository associated with paper titled "AMSwarm: An Alternating Minimization Approach for Safe Motion Planning of Quadrotor Swarms in Cluttered Environments", presented at IEEE ICRA 2023. [https://youtu.be/eIBcOKq5_Jk](https://youtu.be/eIBcOKq5_Jk)
