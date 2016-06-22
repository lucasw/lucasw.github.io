---
title: ROS with Arduino
layout: post
---

Ancient Arduino Diecimila 168


    sudo apt-get install arduino ros-jade-rosserial-arduino ros-jade-rosserial-python

http://wiki.ros.org/rosserial_arduino/Tutorials

```
~/Documents/sketches/libraries$ rosrun rosserial_arduino make_libraries.py .

Exporting to .
[urdf_tutorial]: Unable to find dependency: convex_decomposition
ROS path [0]=/opt/ros/jade/share/ros
ROS path [1]=/home/lucasw/catkin_ws/src
ROS path [2]=/opt/ros/jade/share
ROS path [3]=/opt/ros/jade/stacks. Messages cannot be built.

[testbot_gazebo_control]: Unable to find dependency: ros_control
ROS path [0]=/opt/ros/jade/share/ros
ROS path [1]=/home/lucasw/catkin_ws/src
ROS path [2]=/opt/ros/jade/share
ROS path [3]=/opt/ros/jade/stacks. Messages cannot be built.

Exporting rosserial_msgs

  Messages:
    TopicInfo,Log,

  Services:
    RequestParam,RequestServiceInfo,RequestMessageInfo,

Exporting std_srvs

  Services:
    Trigger,Empty,

Exporting std_msgs

  Messages:
    Int64,Bool,UInt8,UInt16MultiArray,Int32,Int64MultiArray,Int16MultiArray,MultiArrayLayout,Header,UInt8MultiArray,String,UInt64MultiArray,Char,Time,Float32MultiArray,Int8,Empty,ByteMultiArray,Float32,Int16,ColorRGBA,UInt32,UInt32MultiArray,UInt16,Float64,Duration,Byte,UInt64,Float64MultiArray,Int8MultiArray,Int32MultiArray,MultiArrayDimension,

Exporting geometry_msgs

  Messages:
    PoseWithCovarianceStamped,WrenchStamped,PolygonStamped,Pose2D,TwistWithCovarianceStamped,PointStamped,TransformStamped,PoseWithCovariance,Point,Wrench,InertiaStamped,PoseStamped,Vector3,Inertia,Quaternion,TwistWithCovariance,Twist,Vector3Stamped,Pose,AccelWithCovarianceStamped,AccelWithCovariance,QuaternionStamped,Point32,AccelStamped,TwistStamped,Transform,PoseArray,Accel,Polygon,

Exporting sensor_msgs

  Messages:
    RelativeHumidity,CompressedImage,JoyFeedbackArray,JointState,Imu,RegionOfInterest,MultiDOFJointState,PointCloud2,ChannelFloat32,Joy,FluidPressure,Image,NavSatStatus,CameraInfo,TimeReference,PointField,JoyFeedback,Range,Temperature,NavSatFix,Illuminance,LaserEcho,MagneticField,MultiEchoLaserScan,PointCloud,LaserScan,

  Services:
    SetCameraInfo,

Exporting marti_visualization_msgs

  Messages:
    TexturedMarker,TexturedMarkerArray,

Exporting uuid_msgs

  Messages:
    UniqueID,

Exporting shape_msgs

  Messages:
    SolidPrimitive,Plane,MeshTriangle,Mesh,

Exporting octomap_msgs

  Messages:
    OctomapWithPose,Octomap,

  Services:
    BoundingBoxQuery,GetOctomap,

Exporting controller_manager_msgs

  Messages:
    HardwareInterfaceResources,ControllerState,ControllersStatistics,ControllerStatistics,

  Services:
    ReloadControllerLibraries,UnloadController,ListControllerTypes,LoadController,SwitchController,ListControllers,

Exporting geographic_msgs

  Messages:
    GeographicMapChanges,KeyValue,RouteNetwork,BoundingBox,GeoPoint,GeoPose,MapFeature,RoutePath,WayPoint,RouteSegment,GeographicMap,

  Services:
    GetRoutePlan,GetGeographicMap,UpdateGeographicMap,

Exporting trajectory_msgs

  Messages:
    MultiDOFJointTrajectory,MultiDOFJointTrajectoryPoint,JointTrajectoryPoint,JointTrajectory,

Exporting gazebo_msgs

  Messages:
    WorldState,LinkStates,ContactState,ContactsState,ODEPhysics,ModelStates,ODEJointProperties,ModelState,LinkState,

  Services:
    GetModelProperties,DeleteModel,SetPhysicsProperties,GetLinkState,SetLinkProperties,ApplyJointEffort,GetPhysicsProperties,GetWorldProperties,ApplyBodyWrench,SetLinkState,GetJointProperties,JointRequest,SetModelState,SetJointTrajectory,SetJointProperties,GetModelState,SetModelConfiguration,BodyRequest,GetLinkProperties,SpawnModel,

Exporting stereo_msgs

  Messages:
    DisparityImage,

Exporting actionlib_msgs

  Messages:
    GoalID,GoalStatusArray,GoalStatus,

Exporting nav_msgs

  Messages:
    Path,GetMapActionGoal,GetMapActionResult,Odometry,GetMapResult,GetMapGoal,OccupancyGrid,GridCells,GetMapAction,GetMapActionFeedback,GetMapFeedback,MapMetaData,

  Services:
    GetMap,SetMap,GetPlan,

Exporting control_msgs

  Messages:
    FollowJointTrajectoryFeedback,JointTrajectoryAction,GripperCommandResult,JointTrajectoryFeedback,FollowJointTrajectoryResult,PointHeadAction,PointHeadActionGoal,SingleJointPositionActionFeedback,FollowJointTrajectoryActionResult,PointHeadFeedback,JointTrajectoryControllerState,GripperCommandGoal,JointTolerance,SingleJointPositionActionGoal,GripperCommand,FollowJointTrajectoryActionGoal,GripperCommandAction,PointHeadGoal,SingleJointPositionResult,SingleJointPositionGoal,SingleJointPositionActionResult,PointHeadActionFeedback,JointTrajectoryGoal,JointTrajectoryActionFeedback,FollowJointTrajectoryAction,JointControllerState,PointHeadActionResult,GripperCommandFeedback,FollowJointTrajectoryActionFeedback,SingleJointPositionFeedback,PointHeadResult,GripperCommandActionResult,SingleJointPositionAction,GripperCommandActionFeedback,GripperCommandActionGoal,JointTrajectoryActionGoal,JointTrajectoryResult,FollowJointTrajectoryGoal,JointTrajectoryActionResult,

  Services:
    QueryCalibrationState,QueryTrajectoryState,

Exporting move_base_msgs

  Messages:
    MoveBaseAction,MoveBaseActionFeedback,MoveBaseActionGoal,MoveBaseActionResult,MoveBaseFeedback,MoveBaseResult,MoveBaseGoal,

Exporting map_msgs

  Messages:
    PointCloud2Update,ProjectedMapInfo,OccupancyGridUpdate,ProjectedMap,

  Services:
    GetPointMapROI,GetMapROI,GetPointMap,SetMapProjections,SaveMap,ProjectedMapsInfo,

Exporting tf2_msgs

  Messages:
    LookupTransformActionGoal,TF2Error,LookupTransformResult,LookupTransformAction,LookupTransformActionFeedback,LookupTransformFeedback,LookupTransformActionResult,LookupTransformGoal,TFMessage,

  Services:
    FrameGraph,

Exporting bond

  Messages:
    Status,Constants,

Exporting visualization_msgs

  Messages:
    InteractiveMarkerPose,InteractiveMarker,InteractiveMarkerUpdate,MenuEntry,InteractiveMarkerControl,ImageMarker,Marker,InteractiveMarkerInit,InteractiveMarkerFeedback,MarkerArray,

Exporting smach_msgs

  Messages:
    SmachContainerInitialStatusCmd,SmachContainerStructure,SmachContainerStatus,

Exporting pcl_msgs

  Messages:
    ModelCoefficients,Vertices,PointIndices,PolygonMesh,

Exporting diagnostic_msgs

  Messages:
    KeyValue,DiagnosticStatus,DiagnosticArray,

  Services:
    SelfTest,

Exporting rosgraph_msgs

  Messages:
    Clock,TopicStatistics,Log,

Exporting test_roslib_comm

  Messages:
    SameSubMsg2,SameSubMsg1,TypeNameChange2,HeaderTest,TypeNameChangeComplex2,TypeNameChangeComplex1,FieldNameChange1,FieldNameChange2,FillSimple,TypeNameChangeArray2,FillEmbedTime,ArrayOfMsgs,TypeNameChange1,TypeNameChangeArray1,SameSubMsg3,

Exporting roscpp

  Messages:
    Logger,

  Services:
    GetLoggers,SetLoggerLevel,Empty,

Exporting joy_feedback_ros

  Messages:
    Rumble,Envelope,Periodic,

Exporting turtlesim

  Messages:
    Pose,Color,

  Services:
    Kill,TeleportRelative,SetPen,Spawn,TeleportAbsolute,

Exporting rospy_tutorials

  Messages:
    Floats,HeaderString,

  Services:
    AddTwoInts,BadTwoInts,

Exporting test_rosmaster

  Messages:
    TestHeader,Floats,RosmsgA,RosmsgC,String,TestPrimitives,Simple,TestArrays,Arrays,Empty,[test_rosmaster]: Unable to build messages: 'NoneType' object has no attribute '_md5sum'

Traceback (most recent call last):
  File "/opt/ros/jade/lib/python2.7/dist-packages/rosserial_client/make_library.py", line 574, in rosserial_generate
    MakeLibrary(p, path, rospack)
  File "/opt/ros/jade/lib/python2.7/dist-packages/rosserial_client/make_library.py", line 506, in MakeLibrary
    md5sum = roslib.message.get_message_class(package+'/'+f[0:-4])._md5sum
AttributeError: 'NoneType' object has no attribute '_md5sum'

Exporting test_rosservice

  Services:
    HeaderEcho,

Exporting test_rospy

  Messages:
    Floats,TransitiveMsg1,TransitiveImport,PythonKeyword,ArrayVal,TransitiveMsg2,Val,Empty,TestConstants,EmbedTest,HeaderVal,TestFixedArray,HeaderHeaderVal,

  Services:
    EmptySrv,MultipleAddTwoInts,TransitiveSrv,ListReturn,EmptyReqSrv,StringString,EmptyRespSrv,ConstantsMultiplex,

Exporting topic_tools

  Services:
    DemuxDelete,MuxSelect,MuxDelete,MuxAdd,DemuxSelect,DemuxAdd,DemuxList,MuxList,

Exporting dynamic_reconfigure

  Messages:
    SensorLevels,IntParameter,Config,ParamDescription,ConfigDescription,DoubleParameter,StrParameter,BoolParameter,Group,GroupState,

  Services:
    Reconfigure,

Exporting test_rostopic

  Messages:
    Floats,Simple,ArrayVal,Val,Arrays,Embed,TVals,

Exporting driver_base

  Messages:
    ConfigValue,SensorLevels,ConfigString,

Exporting roscpp_tutorials

  Services:
    TwoInts,

Exporting actionlib

  Messages:
    TwoIntsActionFeedback,TestRequestResult,TestResult,TestRequestActionResult,TestFeedback,TwoIntsResult,TwoIntsFeedback,TwoIntsActionGoal,TwoIntsActionResult,TestActionGoal,TestRequestActionFeedback,TestGoal,TwoIntsAction,TestRequestAction,TestActionFeedback,TestRequestGoal,TestActionResult,TestRequestActionGoal,TwoIntsGoal,TestAction,TestRequestFeedback,

Exporting turtle_actionlib

  Messages:
    ShapeFeedback,ShapeActionFeedback,ShapeResult,ShapeGoal,ShapeAction,ShapeActionResult,Velocity,ShapeActionGoal,

Exporting actionlib_tutorials

  Messages:
    FibonacciGoal,AveragingResult,FibonacciActionGoal,FibonacciFeedback,FibonacciResult,AveragingActionFeedback,AveragingAction,FibonacciActionFeedback,AveragingFeedback,FibonacciAction,AveragingActionGoal,AveragingGoal,AveragingActionResult,FibonacciActionResult,

Exporting theora_image_transport

  Messages:
    Packet,

Exporting nodelet

  Services:
    NodeletLoad,NodeletList,NodeletUnload,

Exporting polled_camera

  Services:
    GetPolledImage,

Exporting control_toolbox

  Services:
    SetPidGains,

Exporting tf

  Messages:
    tfMessage,

  Services:
    FrameGraph,

Exporting bullet_server

  Messages:
    Impulse,SoftBody,[bullet_server]: Unable to build messages: 'NoneType' object has no attribute '_md5sum'

Traceback (most recent call last):
  File "/opt/ros/jade/lib/python2.7/dist-packages/rosserial_client/make_library.py", line 574, in rosserial_generate
    MakeLibrary(p, path, rospack)
  File "/opt/ros/jade/lib/python2.7/dist-packages/rosserial_client/make_library.py", line 506, in MakeLibrary
    md5sum = roslib.message.get_message_class(package+'/'+f[0:-4])._md5sum
AttributeError: 'NoneType' object has no attribute '_md5sum'

Exporting laser_assembler

  Services:
    AssembleScans2,AssembleScans,

Exporting rosserial_arduino

  Messages:
    Adc,

  Services:
    Test,

Exporting keyboard

  Messages:
    Key,

Exporting costmap_2d

  Messages:
    VoxelGrid,

Exporting base_local_planner

  Messages:
    Position2DInt,

Exporting navfn

  Services:
    MakeNavPlan,SetCostmap,

Exporting opencv_apps

  Messages:
    Flow,Contour,RectArrayStamped,CircleArray,RotatedRectStamped,Rect,RectArray,Moment,Size,Face,RotatedRectArrayStamped,FaceArrayStamped,MomentArrayStamped,Circle,CircleArrayStamped,LineArrayStamped,FlowStamped,RotatedRectArray,RotatedRect,ContourArray,FlowArray,Point2DArrayStamped,ContourArrayStamped,MomentArray,Point2DStamped,FaceArray,Line,LineArray,Point2D,FlowArrayStamped,Point2DArray,



*** Warning, failed to generate libraries for the following packages: ***
    urdf_tutorial (missing dependency: convex_decomposition)
    testbot_gazebo_control (missing dependency: ros_control)
    test_rosmaster ('NoneType' object has no attribute '_md5sum')
    bullet_server ('NoneType' object has no attribute '_md5sum')
Traceback (most recent call last):
  File "/opt/ros/jade/share/rosserial_arduino/make_libraries.py", line 91, in <module>
    rosserial_generate(rospack, path+"/ros_lib", ROS_TO_EMBEDDED_TYPES)
  File "/opt/ros/jade/lib/python2.7/dist-packages/rosserial_client/make_library.py", line 584, in rosserial_generate
    raise Exception("Failed to generate libraries for: " + str(failed))
Exception: Failed to generate libraries for: ['urdf_tutorial (missing dependency: convex_decomposition)', 'testbot_gazebo_control (missing dependency: ros_control)', "test_rosmaster ('NoneType' object has no attribute '_md5sum')", "bullet_server ('NoneType' object has no attribute '_md5sum')"]
```

Download hello world from the IDE (right arrow button).
Did that save it permanently?
Orange led blinked for a while then stopped when uploading was finished.

```
rosrun rosserial_python serial_node.py /dev/ttyUSB0
[INFO] [/serial_node] [/opt/ros/jade/lib/rosserial_python/serial_node.py]:[47] [ROS Serial Python Node]
[INFO] [/serial_node] [/opt/ros/jade/lib/rosserial_python/serial_node.py]:[79] [Connecting to /dev/ttyUSB0 at 57600 baud]
[ERROR] [/serial_node] [/opt/ros/jade/lib/python2.7/dist-packages/rosserial_python/SerialClient.py]:[421] [Unable to sync with device; possible link problem or link software version mismatch such as hydro rosserial_python with groovy Arduino]
...
```

    Binary sketch size: 8,676 bytes (of a 14,336 byte maximum)
