# Jupyter Docker Compose

This repository contains a Docker Compose configuration for running a Jupyter notebook with TensorFlow and CUDA support. The setup allows you to easily start a Jupyter environment with GPU acceleration for machine learning tasks.

## Configuration

The `docker-compose.yml` file configures:
- A Jupyter notebook server with TensorFlow and CUDA support
- Port mapping from 8888 (container) to 8888 (host)
- Volume mounting from your local path to `/home/jovyan/work` in the container

## Usage

To start the Jupyter server:

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/jupyter-docker-compose.git
   cd jupyter-docker-compose
   ```


2. Update the volume path in `docker-compose.yml`:
   ```yaml
   volumes:
     - /your-path:/home/jovyan/work
   ```
   Replace `/your-path` with the absolute path to your local directory.

### About the "jovyan" User

The default user in Jupyter Docker images is named "jovyan". This name has a specific origin in the Jupyter community:

- The term "jovyan" refers to a citizen of the planet Jupyter
- It comes from Jovian (relating to the planet Jupiter)
- Jupiter is the namesake of Project Jupyter

According to the [official explanation](https://github.com/jupyter/docker-stacks/issues/358) from the Jupyter Docker Stacks maintainers:

> "Jovyan" is the name of the user ID in the Docker images. It's a play on Jovian (like Jovian planet) and was part of the naming scheme (e.g., Jovian moons) used by Project Jupyter in its early days. "Jovyan" is an unspoken pledge that containers will be built with user needs in mind.

The home directory for this user is `/home/jovyan`, which is why the volume mount in the docker-compose file uses this path.


3. Start the container:
   ```bash
   docker-compose up -d
   ```

4. Access Jupyter:
   - The Jupyter server will be available at http://localhost:8888
   - Check the container logs to get the access token:
     ```bash
     docker logs jupyter
     ```

5. To stop the container:
   ```bash
   docker-compose down
   ```

## Working with Notebooks

- Your notebooks will be saved in your specified local directory
- This directory is mounted to `/home/jovyan/work` in the container
- Any changes made in the container will persist on your local machine

## GPU Support

This configuration uses the `tensorflow-notebook:cuda-latest` image which includes CUDA support. To use GPU acceleration:

1. Ensure you have NVIDIA drivers installed on your host machine
2. Install the NVIDIA Container Toolkit (nvidia-docker)
3. Verify GPU access within the container:
   ```python
   import tensorflow as tf
   print("GPUs Available:", tf.config.list_physical_devices('GPU'))
   ```

## Customization

To customize this setup:
- Modify the `docker-compose.yml` file to change ports or volume mounts
- Add additional packages by creating a custom Dockerfile
