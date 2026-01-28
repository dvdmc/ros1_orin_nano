# ros1_orin_nano

IMPORTANT: Configure the ROS_MASTER_URI and ROS_IP in `docker-compose.yaml`.

## Basic launch commands

Open the terminal in the directory where `docker-compose.yaml` is (this repository's top directory). Then:

Build Docker image (if needed):
```bash
sudo docker build
```

Start Docker container:
```bash
sudo docker compose up -d
```

Attach the terminal to the container:
```bash
sudo docker exec -it ros1_orin_nano /bin/bash
```

Move to the `drone_ws` directory inside the container:
```bash
cd drone_ws
```

Run tmuxinator:
```bash
tmuxinator start -p start_drone.yaml
```

### Tmuxinator quickguide

- Use `Ctrl+B` to enter the command node. Then, move between windows (shown below in bright green) with `0 / 1 / 2 ...`. 
- You can split panes using `Ctrl+B` and then `%`(horizontal) or `"`(vertical). 
- To exit the tmux session using the script `stop_tmuxinator.sh` in any of the terminals (this not only kills the session but also run `Ctrl+C` in every terminal to stop ROS). Otherwise, use `Ctrl+B` then `:` and type `kill-session`.

## Shutting down

Once you are out of tmux, use `exit` to go out of the container and:
```bash
sudo docker compose down
```

