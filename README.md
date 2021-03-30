# setup for HITL simulation
## load parameter to Pixhawk 4
1. use QGround Control, connect PC to Pixkawk 4 via USB
2. select Vehicle Setup tab > Parameters > Tools > Load from file...
3. navigate to and select px4-hitl-simulation.params
4. select Tools > Reboot vehicle > OK
5. repeat steps 2 to 4 once again
6. disconnect USB and close QGC
## modify model iris.sdf
1. open iris.sdf (at Firmware/Tools/sitl_gazebo/models/iris/)
2. scroll down to `<plugin name='mavlink_interface' filename='libgazebo_mavlink_interface.so'>` section
3. change 
  ```xml
  <serialEnabled>0</serialEnabled>
  <hil_mode>0</hil_mode>
  ```
   to
  ```xml
  <serialEnabled>1</serialEnabled>
  <hil_mode>1</hil_mode>
  ```
4. save and close iris.sdf
5. open iris.world (at Firmware/Tools/sitl_gazebo/worlds)
6. comment this block to remove asphalt background by change
  ```xml
  <include>
      <uri>model://asphalt_plane</uri>
  </include>
  ```
  to
  ```xml
  <!--<include>
      <uri>model://asphalt_plane</uri>
  </include>-->
  ```
7. save and close iris.world
## simulation
1. in PC
- connect to Pixhawk via USB
- run command
  ```
  gazebo *path/to/Firmware*/Tools/sitl_gazebo/world/iris.world
  ```
2. in onboard computer (jetson)
- *terminal 1*
  ```bash
  # connect jetson to pixhawk
  cd ros/bash/script/bash
  sh connect_px4.sh
  ```
- *termial 2* run code
- ...
3. use RC to **ARM**, switch **FLIGHT MODE** and **CONTROL** drone in simulation

# setup for PRACTICE flight
## load parameter to Pixhawk 4
1. use QGround Control, connect PC to Pixkawk 4 via USB
2. select Vehicle Setup tab > Parameters > Tools > Load from file...
3. navigate to and select **px4-practice.params**
4. select Tools > Reboot vehicle > OK
5. repeat steps 2 to 4 once again
6. disconnect USB and close QGC
7. follow [flight test](https://husteduvn-my.sharepoint.com/:b:/g/personal/quang_nguyenanh_hust_edu_vn/ER92PwI_aVBIq-ZB6Ls9zwYBxY7xHP34cfgBBbwq-X6S4w?e=Nf0FrE) guide
