# Basic Commands in ROS, from the ROSwiki tutorials 

## Making a catkin workspace

`mkdir -p ~/catkin_ws/src`\
`cd ~/catkin_ws/`\
`catkin_make`

Inside the 'devel' folder you can see that there are now several setup.sh files. 
Sourcing any of these files will overlay this workspace on top of your environment. 
 	
`source devel/setup.bash`\
`echo $ROS_PACKAGE_PATH`

/home/youruser/catkin_ws/src:/opt/ros/kinetic/share

### rospack
`rospack find {package-name}`
This tells you where exactly the package is installed on the machine. 
In my case, /opt/ros/kinetic/....

### roscd 
`roscd <package-name>`
As the name suggests, it takes you directly to the package! But only within ROS_PACKAGE_PATH

To see environment variables, do 
`printenv | grep ROS`

### rosls
`rosls <package-name>`
Would return the list of files inside that directory 

## Packages

The simplest possible package might have a structure which looks like this:
CMakeLists.txt
package.xml

The recommended method of working with catkin packages is using a catkin workspace\
workspace_folder/        
	src/                   
		CMakeLists.txt       
	package_1/
		CMakeLists.txt     
		package.xml  

## Create new package in a workspace
`catkin_create_pkg beginner_tutorials std_msgs rospy roscpp`\
Last three terms are the dependencies that need to be installed too! beignner_tutorials is the name of the package. 

To add the workspace to your ROS environment you need to source the generated setup file:\
`source ~/catkin_ws/devel/setup.bash` 
(this is after running catkin_make, of course)

## Viewing Package Dependencies:
`rospack depends1 <beginner_tutorials>`
(Package name within the angular brackets)
	
depends1 means only its immediate dependencies, if we just do 'depends', it would recursively print all dependencies. 

Dependencies of Dependencies of the packages:
`rospack depends1 <rospy>` 

## ROS Graph Concepts

- A node is an executable that uses ROS to communicate with the other nodes. 
- Message is the ROS data type used when subscribing or publishing a topic. 

So basically, nodes publish messages to a topic, and also, they subscribe to a topic to receive messages. 
These ROSnodes use a ROS client library to communicate with other nodes. These client libraries allow nodes written in different languages to communicate with one another. For instance, rospy is in python and roscpp in CPP. 

### roscore
The FIRST THING WE RUN while using ROS. 

### rosnode
This diplays information of all the nodes that are currently running. 
`rosnode list`
If we run `roscore` followed by `rosnode list` we get the output as `/rosout`. rosout is a node that's always running. This collects and logs all the outputs of the nodes. 
`rosnode info /rosout` returns information about the specified node, in this case, rosout. 

### rosrun 
rosrun allows us to use the package name. We can directly run a node within a package, without having to know the package path! 
`rosrun <package-name> <node-name<`
For instance, `rosrun turtlesim turtlesim_node`

We can also reassign names to our nodes. 
`rosrun turtlesim turtlesim_node __name:=tortoise`
Now when we do rosnode list, we will get output as '/rosout' and '/tortoise'. 

Use 'ping' to check if the node is up and running. 
`rosnode ping tortoise`









 
