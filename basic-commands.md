# Basic Commands in ROS, from the ROSwiki tutorials 

## Making a catkin workspace

`mkdir -p ~/catkin_ws/src`\
`cd ~/catkin_ws/`\
`catkin_make`

Inside the 'devel' folder you can see that there are now several setup.*sh files. Sourcing any of these files will overlay this workspace on top of your environment. 
 	
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

The recommended method of working with catkin packages is using a catkin workspace
workspace_folder/        
  src/                   
    CMakeLists.txt       
    package_1/
      CMakeLists.txt     
      package.xml  

## Create new package in a workspace
`catkin_create_pkg beginner_tutorials std_msgs rospy roscpp`
Last three terms are the dependencies that need to be installed too! beignner_tutorials is the name of the package. 

To add the workspace to your ROS environment you need to source the generated setup file:
`source ~/catkin_ws/devel/setup.bash` 
(this is after running catkin_make, of course)

## Viewing Package Dependencies:
`rospack depends1 <beginner_tutorials>`
(Package name within the angular brackets)
	
depends1 means only its immediate dependencies, if we just do 'depends', it would recursively print all dependencies. 

Dependencies of Dependencie of the packages:
`rospack depends1 <rospy>` (for eg.)







 
