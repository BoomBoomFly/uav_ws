# uav_ws

> 本仓库为 [BoomBoomFly](https://github.com/BoomBoomFly/BoomBoomFly) 主仓库中 UAV 子系统的独立镜像/发布工作区，日常主线研发请以主仓库为准。

## 目录结构

- `src/uav_interfaces`：共享状态与飞行命令接口（`VehicleState`、`FlightCommand`）
- `src/uav_bridge`：OpenVINS 里程计安全门控与 IMU 桥接
- `src/uav_control`：PX4 DDS 与 MAVROS 统一控制节点
- `src/uav_mission`：非阻塞起飞、悬停与降落状态机
- `src/uav_bringup`：统一启动入口 `uav.launch.py` 与配置 `uav.yaml`
- `sim/`：PX4 SITL 启动入口与历史测试记录
- `repos/uav_thirdparty.repos`：OpenVINS、MAVROS、`px4_msgs` 外部依赖清单

## 构建与启动

```bash
# 可选：拉取外部依赖
mkdir -p src/thirdparty
vcs import src/thirdparty < repos/uav_thirdparty.repos

source /opt/ros/humble/setup.bash
colcon build --symlink-install --packages-up-to uav_bringup
source install/local_setup.bash
ros2 launch uav_bringup uav.launch.py
```