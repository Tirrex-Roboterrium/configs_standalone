# Running

## Prerequisites

You need to install `rsync` and `inotify-tools`.
For deb-based distributions you can execute:
```
sudo apt install rsync inotify-tools
```

You also need to connect your computer to the robot using the ethernet cable.
It is also possible to connect to it using wifi (SSID: `ROMEA_adap2e`) but it is not recommanded.


## Synchronize config files on the robot

You need to send the `config` directory and the `compose.yaml` file on the robot every time you
change the values locally.
You can do that automatically using the following program:
```
./autosync_config
```
This program keeps listening every changes on these files and uploads them to the robot.


## Start the programs on the robot

Open a shell on the robot using ssh
```
ssh -X guest@pombasic
```

After that you have to go in the `standalone` directory
```
cd standalone
```

Then, you can start everything
```
docker compose up
```


## Open a shell in the tirrew workspace

If you want to execute ROS commands like `ros2 topic list`, or `ros2 launch`, you can open a shell
using the following command
```
docker compose run --rm bash
```

The option `--rm` allows to remove the container when you close the shell.
This container is temporary and does not retrieve any important data.


## Advanced docker compose commands

By default the command `docker compose up` starts all the docker services defined in the
`compose.yaml` file that are not marked as optional.
It is possible to start manually one or several services by specifying them on the command line.
For example, if you want to start only `robot` and `localisation`, you can write
```
docker compose up robot localisation
```

It is possible to start the program in the background to immediately regain control of the prompt
```
docker compose up -d robot
```

After this command, the service `robot` continues to run and you can start other services when you
want.
If you want to check the output messages of the service, you can use
```
docker compose logs -f robot
```
The option `-f` allows to follow the new line in real time.
You can interrupt the logs with `CTRL+C` but the program continues to run.
If you want to stop it, you can use
```
docker compose stop robot
```

You can also stop all the default services if you don't specify any
```
docker compose stop
```

But this command does not stop optional services (like rviz).
If you want to stop everything, you have to use
```
docker compose --profile '*' stop
```


# Download the recorded data

The service `record` is used to save the current configuration and sensor topics in a rosbag file.
The configuration of the recording is specified in the `config/records.yaml` file.
You can download these data on your computer using
```
./download_data
```
This script will synchronize the `data` directory of the robot onto the local one.
It will only transfer new files, so you can execute it regularly if you want to check the result
during an experimentation.
