# How to use

You need to allow docker services to open graphical interface on your current X11 server.
It is optional but used by _rqt_runtime_monitor_ and _rviz_.
```
xhost +local:docker
```

After that you can start the robot using
```
docker compose up
```

This command reads the `compose.yaml` file and start a docker container using the tirrex_workspace
docker image that contain a full ROS environment to drive several robots and their simulation.


## Open a terminal in the tirrex workspace

If you want to execute ROS commands like `ros2 topic list`, or `ros2 launch`, you can open a
terminal using the following command
```
docker compose run --rm bash
```

The option `--rm` allows to remove the container when you close the shell.
This container is temporary and does not retrieve any important data.


# Documentation

You can find a documentation about the configuration file in the [pdf of the tirrex_demo
package](https://github.com/Tirrex-Roboterrium/tirrex_demo/blob/main/doc/documentation.pdf).
