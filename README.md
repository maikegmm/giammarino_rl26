# Robotics Lab 2026 - Classwork 0

**Author:** Maike Giammarino  
**Program:** Master's Degree in Automation and Robotics Engineering - Università degli Studi di Napoli Federico II  

This repository contains the environment setup for the Robotics Lab 2026 course. It includes the Docker configuration required to run ROS 2 securely and persistently on a local Linux machine.

## Prerequisites
To run this environment, you must have the following installed on your host machine:
* A Linux environment (native Ubuntu 22.04, WSL2, or a Linux Virtual Machine, including those configured on Apple Silicon M1).
* **Docker**: Configured to build images and run containers.
* **Git**: For version control and repository management.

## How to Build and Run the Container

**1. Make the scripts executable**
Before running the environment for the first time, ensure the provided bash scripts have the correct execution permissions:
chmod +x docker_scripts/*.sh

**2. Build the Docker Image**
Build the ROS 2 Docker image using the provided script:

./docker_scripts/docker_build_image.sh

**3. Run the Container**
Start the container. This script will automatically mount the local src/ directory to the container's workspace to ensure code persistence:

./docker_scripts/docker_run_container.sh

**4. Connect an Additional Terminal**
To open an additional shell inside the running container, open a new host terminal window and execute:

./docker_scripts/docker_connect.sh

##Verification (Task 2 Completion)

Once inside the running container, you can verify that the environment has been set up successfully by following these steps.
**1. Verify ROS 2 Installation**

Check if the correct ROS 2 distribution is active:

echo $ROS_DISTRO

(Expected output: humble)

Verify that the ROS 2 packages are correctly installed:

ros2 pkg list

**2. Verify Host-Container Volume Persistence**

To prove that your code persists across container lifecycles, run the following commands inside the container terminal to create a test file:

touch /home/user/ros2_ws/src/test_persistence.txt
exit

After exiting, stop and remove the container from your host machine:

docker rm <container_name>
# or alternatively:
docker container prune -f

Finally, check the local src/ folder on your host machine. The file test_persistence.txt will still exist, demonstrating successful volume mounting.



