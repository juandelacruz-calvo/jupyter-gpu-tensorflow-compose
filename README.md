# Jupyter Docker Compose

This repository contains a Docker Compose configuration for running a Jupyter notebook with TensorFlow and CUDA support. The setup allows you to easily start a Jupyter environment with GPU acceleration for machine learning tasks.

## Configuration

The `docker-compose.yml` file configures:
- A Jupyter notebook server with TensorFlow and CUDA support
- Port mapping from 8888 (container) to 8888 (host)
- Volume mounting from the local `./work` directory to `/your-path` in the container

## Usage

To start the Jupyter server:

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/jupyter-docker-compose.git
   cd jupyter-docker-compose
   ```

2. Start the container:
   ```bash
   docker-compose up -d
   ```

3. Access Jupyter:
   - The Jupyter server will be available at http://localhost:8888
   - Check the container logs to get the access token:
     ```bash
     docker logs jupyter
     ```

4. To stop the container:
   ```bash
   docker-compose down
   ```

## Working with Notebooks

- Your notebooks will be saved in the `./work` directory
- This directory is mounted to `/your-path` in the container
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

