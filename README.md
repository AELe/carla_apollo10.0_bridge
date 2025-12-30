To make it compatible with Apollo 10.0, I have modified the original repository: https://github.com/guardstrikelab/carla_apollo_bridge.
Additionally, the environment configuration has also been changed.

You can configure it by following the steps below:

Prerequisite: A running Apollo Docker container must already be deployed


1.Environment Variable Configuration

Enter the Apollo container and modify /home/$USER/.bashrc.
Append the following to the end of the file:

export PYTHONPATH=$PYTHONPATH/opt/apollo/neo/lib/cyber

export PYTHONPATH=$PYTHONPATH:/opt/apollo/neo/lib/cyber/python/internal

export PYTHONPATH=$PYTHONPATH:/apollo_workspace/modules/carla_apollo_bridge

export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/apollo/neo/lib

export PYTHONPATH=$PYTHONPATH:/opt/apollo/neo/lib/cyber/python

export PYTHONPATH=$PYTHONPATH:/apollo

export PYTHONPATH=$PYTHONPATH:/apollo/modules

export PYTHONPATH=$PYTHONPATH:/apollo_workspace/bazel-bin


2.Install the dependencies required for carla_bridge

Execute the following commands within the Apollo container:

pip3 install "numpy<2.0" -i https://pypi.tuna.tsinghua.edu.cn/simple

pip3 install carla==0.9.15 -i https://pypi.tuna.tsinghua.edu.cn/simple

pip3 install opencv-python -i https://pypi.tuna.tsinghua.edu.cn/simple


3.Download CARLA_0.9.15.tar.gz
https://github.com/carla-simulator/carla/releases


Running Instructions:

2.Inside the container, start the three Apollo modules: planning, prediction, and control.

2.Outside the container, launch CarlaUE4 with the specified port:

./CarlaUE4.sh -carla-port=2000

3.Inside the container, start the carla_bridge:

python3 carla_apollo_bridge/carla_bridge/main.py






