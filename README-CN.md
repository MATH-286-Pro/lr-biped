# 双足机器人

## 1.环境配置
- 1.1 添加虚拟环境 + 激活虚拟环境
    ```  
    virtualenv micro-507 --python=python3
    cd micro-507
    source Scripts/activate
    cd ..
    ```
- 1.2 安装依赖
    ```
    pip install matplotlib
    pip install pybullet
    pip install qpsolvers  
    pip install osqp  
    python qp.py  测试安装
    出现 QP solution: x = [ 0.3076548  -0.69232615  1.38448776] 则安装成功
    ```
- 1.3 可以使用如下命令退出虚拟环境   
  ```
  deactivate
  ```

## 2.知识
- LIP (Linear Inverted Pendulum) 模型
  - 线性倒立摆模型
  - 运动学模型，计算加速度，公式如下：
  $$ \ddot{x} = \frac{g}{z_0}(x(t)-x_{base}) $$
  $$ x(t) = Ae^{-\omega t}+Be^{\omega t}+x_{base}$$
- DCM (Divergent Componrnt of Motion) 模型
  - 规划下一步落点  
  $$ d = x + \frac{\dot{x}}{\omega}$$  

## 3.代码
- **DCM-Locomotion.ipynb**
  - 所有模拟代码在此文件中运行
  - 第一部分 = Toy机器人仿真
  - 第二部分 = ATLAS双足机器人仿真
- **DCMTrajectoryGenerator.py**
  - 定义类 
    - def getCoM(self):
        $$ \dot{x}_{CoM} = \omega (x_{DCM}-x_{CoM}) $$
        $$ x_{CoM}(t+dt) = x_{CoM}(t) + \dot{x}_{CoM} \cdot dt $$
    - def planDCMTrajectory(self,time):
