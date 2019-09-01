# Understandig ROS topics 

## Let's run ROS turtlesim
In 3 different terminal windows:
`roscore`
`rosrun turtlesim turtlesim_node`

`rosrun turtlesim turtle_teleop_key`
Now we can drive the turtle around using arrow keys! But what's really happening?
As ROSwiki describes it, the turtlesim_node and the turtle_teleop_key node are communicating with each other over a ROS Topic. turtle_teleop_key is publishing the key strokes on a topic, while turtlesim subscribes to the same topic to receive the key strokes. 

### rqt_graph
rqt_graph creates a dynamic graph of what's going on in the system. Let's use rqt_graph which shows the nodes and topics currently running.

`rosrun rqt_graph rqt_graph`
This will show a graph of both the nodes and the topic name which in this case, is /turtle1/cmd_vel

### rostopic
This allows us to get information about ROS topics. 
rostopic echo shows the data published on a topic. Syntax is rostopic echo [topic]
`rostopic echo /turtle1/cmd_vel`

rostopic list, as the name suggests, lists down all the topics currently published and subscribed. 
`rostopic list`

### rosmsg 
Communication between nodes (punlisher and subcriber) takes place using messages, and more specifically, same type of messages! To see mesage type of any topic: syntax is rostopic type [topic]

`rostopic type /turtle1/cmd_vel`
Output is `geometry_msgs/Twist`

And now to see the details of the message, we use rosmsg
`rosmsg show geometry_msgs/Twist`

## Using rostopic with rosmsg 







