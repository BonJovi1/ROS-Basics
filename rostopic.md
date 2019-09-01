# Understanding ROS topics 

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
rostopic echo shows the data being published on a topic. Syntax is rostopic echo [topic]
`rostopic echo /turtle1/cmd_vel`

rostopic list, as the name suggests, lists down all the topics currently published and subscribed. 
`rostopic list`

### rosmsg 
Communication between nodes (punlisher and subcriber) takes place using messages, and more specifically, same type of messages! To see mesage type of any topic: syntax is rostopic type [topic]

`rostopic type /turtle1/cmd_vel`
Output is `geometry_msgs/Twist`

And now to see the details of the message, we use rosmsg
`rosmsg show geometry_msgs/Twist`

Or if we combine both, we can also do:
`rostopic type /turtle1/cmd_vel | rosmsg show`

## Using rostopic with messages

rostopic pub publishes data on to a topic currently advertised.
Syntax: rostopic pub [topic] [msg_type] [args]

`rostopic pub -1 /turtle1/cmd_vel geometry_msgs/Twist -- '[2.0, 0.0, 0.0]' '[0.0, 0.0, 1.8]'`

Breaking it down:
- rostopic pub: publishes message to a topic.
- -1: publish only one message, thrn exit. 
- /turtle1/cmd_vel: Topic name
- geometry_msgs/Twist: type of message, as outputted by rosmsg
- arguments are the message, syntax can be seen by `rosmsg show geometry_msgs/Twist`

Instead of one message at a time, we can publish continuosly like this, using pub -r:
`rostopic pub /turtle1/cmd_vel geometry_msgs/Twist -r 1 -- '[2.0, 0.0, 0.0]' '[0.0, 0.0, -1.8]'`
After -r, we write '1', which means that this publishes the velocity commands at a rate of 1 Hz on the velocity topic.

rostopic hz:
As the name suggests, it reports the rate at which data is published.
`rostopic hz /turtle1/pose`

### rqt_plot
rqt_plot displays a scrolling time plot of the data published on topics. Let's see the data being published on our turtle topic. 
`rosrun rqt_plot rqt_plot` (similar to rqt_graph syntax)
We can type the name of the topic, and we would see a plot of the data that's being currently published to it.









