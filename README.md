# ROS 2 Package Creation Template


This is a template for creating ROS 2 workspace **ros_ws** along with a custom package.

**<em>Note: </em>** If you do not have ROS 2 installed you can use my [Docker Container](#using-docker).

# Install

```bash
git clone https://github.com/jkoubs/ros2-development.git
cd ros2_ws
```
You now have a clean ROS2 workspace with a custom package to work with.

#### IMPORTANT EDIT:

Here I have called my custom package **robot_description**, so you just need to replace this name with your own package name in a few files. To do this you can easily use VS Code search bar and type in **robot_description** and make your changes accordingly.

# Using Docker
## Build Docker Images

We will build 2 images:
- <strong>galactic_tb_env</strong>: Allows to run turtlebot3 simulations in ROS 2 from a linux computer
- <strong>my_bot_ros2</strong>: Built on top of <strong>galactic_tb_env</strong> image to set up the **ros2_ws** for developing a ROS 2 project.

Open a new terminal and git clone the following repositories:

```bash
git clone https://github.com/jkoubs/ros2_galactic.git
git clone https://github.com/jkoubs/ros2-development.git
```
Then build the images:

```bash
cd ros2_galactic/docker
docker build -f Dockerfile -t galactic_tb_env .
cd ../..
cd ros2-development/docker
docker build -f Dockerfile -t my_bot_ros2 ../
```
<strong><em>Note</em></strong>: <strong>../</strong> represents the PATH context which sets the target context one level above to the <strong>my_bot_ros2</strong> directory in order to successfully execute the COPY command from the Dockerfile which will copy the <strong>ros2_ws</strong> inside the container.

## IMPORTANT REQUIREMENTS

**Before running the container you need to edit 2 main things:**

* Here I have called my custom package **robot_description**, so you just need to replace this name with your own package name in a few files. To do this you can easily use VS Code search bar and type in **robot_description** and make your changes accordingly.

* The docker-compose.yml file: Replace PROJECT_PATH with your local path to the project, by setting the  PROJECT_PATH environment variable on your host.**

## Launch Container

Next we will create the container:

<strong><em>Requirement</em></strong>: To run GUI applications in Docker on Linux hosts, you have to run <strong>"xhost +local:root"</strong>. To disallow, <strong>"xhost -local:root"</strong>. For Windows and Mac hosts please check : [Running GUI applications in Docker on Windows, Linux and Mac hosts](https://cuneyt.aliustaoglu.biz/en/running-gui-applications-in-docker-on-windows-linux-mac-hosts/). Can also found some more information about [Using GUI's with Docker](http://wiki.ros.org/docker/Tutorials/GUI).

```bash
xhost +local:root
```

We can now run the image as a container named <strong>my_bot_ros2_container</strong> using docker-compose :

```bash
docker-compose up
```

We are now <strong>inside the container</strong> and ready for executing our codes.

<u><strong><em>Note:</em></strong></u> For the next tasks we will consider that we are working from inside our container, in the <strong>ros2_ws</strong> workspace.
