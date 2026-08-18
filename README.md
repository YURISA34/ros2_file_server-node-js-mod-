# ros2_file_server-node-js-mod-

======================= LIMO / NODE-RED ROS2 SETUP =======================
        File deployment + AprilTag configuration  |  ROS2 Humble
============================================================================

HOW TO INSTALL
----------------------------------------------------------------------------

1. Download the files from GitHub.
   https://github.com/USERNAME/REPO/blob/main/action-client.js
   https://github.com/USERNAME/REPO/blob/main/controller_server.yaml
   https://github.com/USERNAME/REPO/blob/main/apriltag_pose.yaml
   (Will automatically save to ~/Downloads/)

2. Copy each file into its required location.

   cp ~/Downloads/action-client.js ~/.node-red/node_modules/@chart-sg/node-red-ros2/src/action-client/
   cp ~/Downloads/controller_server.yaml ~/ros2_ws/src/limo-training/limo_navigation/config/limo/
   cp ~/Downloads/apriltag_pose.yaml ~/ros2_ws/src/apriltag_pose/apriltag_pose/config/apriltag_pose.yaml

3. Confirm all three files landed correctly.

   ls ~/.node-red/node_modules/@chart-sg/node-red-ros2/src/action-client/
   ls ~/ros2_ws/src/limo-training/limo_navigation/config/limo/
   ls ~/ros2_ws/src/apriltag_pose/apriltag_pose/config/

============================================================================

APRILTAG CONFIGURATION
----------------------------------------------------------------------------

1. Open the config file (copied in step 2 above).
   ~/ros2_ws/src/apriltag_pose/apriltag_pose/config/apriltag_pose.yaml

2. Measure the BLACK TAG PATTERN ONLY — not the full printed page.
   (Example: 6.5cm printout, 5.2cm black tag)

3. Convert your measurement from cm to meters.
   5.2cm -> 0.052

4. Set the "size" field for each tag ID to your measured value (in meters).

   tag_config_yaml: |
     standalone_tags:
       - {id: 1, size: 0.052, name: "dock_left"}
       - {id: 2, size: 0.052, name: "dock_right"}

5. If you print new tags at a different size, remeasure and update "size"
   for that tag ID. A wrong size will throw off pose estimation distance.

============================================================================

REBUILD / RESTART
----------------------------------------------------------------------------

colcon build --packages-select apriltag_pose
source install/setup.bash
node-red-restart   # or: node-red

============================================================================
For issues, check the project repo or open a GitHub issue.
============================================================================
