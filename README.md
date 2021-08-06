# Pushsrc

機能システム学特論レポート
<br>
授業内にて使用したwsの利用手順を下記に示す．
<br>
なお，実行環境はUbuntu 18.04＋ROS-melodicである．
# 1.	Gazeboを用いたマニピュレータのシミュレーション
作成したマニピュレータのモデル動作確認を行うには下記コマンドを実行する．
```
$ roslaunch sixdofarm sixdofarm.launch
$ rosrun rviz rviz
```
上記コマンドを実行するとrvizが立ち上がるがロボットモデルが表示されていない．
<br>
そこで画面上に表示されている”Add”ボタンをクリックし，出現するウィンドウから”RobotModel”を追加する．
<br>
つづいて，rviz画面左に表示されている”Fixed Frame”を”map”から”base”へ変更する．
<br>
すると，rviz上に6自由度のマニピュレータが現れる．
<br>
また，別ウィンドウで”joint_state_publisher_gui”が立ち上がっている．
<br>
このウィンドウではマニピュレータの各関節を回転させることができる．
<br>
ロボットアームのモデル利用をするには下記のコマンドを実行する
```
$ roslaunch sixdofarm_moveit_config demo.launch
```
上記コマンドを実行すると6自由度のマニピュレータが立ち上がる．
<br>
このマニピュレータの先端についているボールをドラッグすることで姿勢が変更可能である．
<br>
rviz上の”Plannning”タブにある”Plan”を押すことで，変更後の姿勢への計画を行う．
<br>
さらに，”Execure”を押すことで実行する．
<br>
また，” Plannning& Execure”を押すことで計画と実行を同時に行う．

# 2.	Gazebo上の移動ロボットモデル操作確認
Moveit! と gazebo の接続を確認するため，下記コマンドを実行する．
```
$ roslaunch sixdofarm_moveit_config sixdofarm_moveit.launch
```
上記コマンドでrviz，gazebo，”joint_state_publisher_gui”が立ち上がる．
<br>
1.に記述したように，rviz上の”Plannning”タブにある”Plan”を押すことで，変更後の姿勢への計画を行う．
<br>
さらに，”Execure”を押すことで実行する．
<br>
また，” Plannning& Execure”を押すことで計画と実行を同時に行う．
<br>
今回はgazebo上のマニピュレータも連動して動作することが確認できる．
<br>
また，実行時にはロボットモデルのみ存在しているが，gazeboの”Insert”タブから複数オブジェクトを選べる．

# 3.	移動ロボットのナビゲーション
移動ロボットがrviz，gazebo上で動作するかを確認する．
<br>
下記コマンドでrviz，gazebo上に移動ロボットが存在することが確認できる．
```
$ roslaunch wheel_robot wheel_robot_control.launch
```
また，下記コマンドで出現した移動ロボットを移動させることができる．
```
$ rqt
```
rqtを起動させた後，”Plugins”→”Robot Tools”→”Robot Steering”を選ぶと前後速度指令，回転指令をすることができる．
<br>
また，下記コマンドを実行することで移動ロボットをキーボード操作で動かすことも可能である．
```
$ rosrun wheel_robot_control key_teleop.py
```

# 4.	移動ロボットで地図の作成（slam gmapping)
移動ロボットを用いて地図作成を行う．
<br>
下記コマンドで地図作成が可能である．
```
$ roslaunch wheel_robot wheel_robot.launch
```
※↑このコマンドでgazebo起動後，障害物となるオブジェクトを配置する必要がある．
```
$ roslaunch wheel_robot_gmapping wheel_robot_gmapping.launch
$ rqt
$ rosrun rviz rviz
```
※↑rviz起動後，”Add”ボタンをクリックし，出現するウィンドウから”RobotModel”，”Map”を追加する．その後，”Map”タブ内のTopicを”/map”と設定する．

なお，3.同様，下記コマンドを実行することで移動ロボットをキーボード操作で動かすことも可能である．
```
$ rosrun wheel_robot_control key_teleop.py
```
これで地図を作成可能な状態となる．
<br>
地図の保存方法を下記コマンドで示す．保存される地図は下記コマンドを実行したディレクトリに入る．また，末尾の”test”は保存時のファイルネームとなる．
```
$ rosrun map_server map_saver -f test
```
# 5.	差動二輪移動ロボットの確認
ここでは差動二輪ロボットをgazebo，rviz上で確認する．
<br>
下記コマンドで二輪ロボットが確認できる．移動ロボットと部屋のオブジェクトが配置されている．
```
$ roslaunch diff_mobile_robot diff_mobile_gazebo.launch
$ rosrun rviz rviz
```
rviz起動後，”Add”ボタンをクリックし，出現するウィンドウから”RobotModel”を追加する． 
 
# 6.	差動２輪移動ロボットのナビゲーション
移動ロボットを用いて地図作成を行う．下記コマンドで地図作成が可能である．
<br>
gazebo上には立ち上げ後，移動ロボットと部屋のオブジェクトが配置されている．
```
$ roslaunch diff_mobile_robot diff_mobile_gazebo.launch
$ roslaunch wheel_robot_gmapping wheel_robot_gmapping.launch
$ rosrun rviz rviz
```
※↑rviz起動後，”Add”ボタンをクリックし，出現するウィンドウから”RobotModel”，”Map”を追加する．その後，”Map”タブ内のTopicを”/map”と設定する．
<br>
また，3.同様，下記コマンドで出現した移動ロボットを移動させることができる．
```
$ rqt
```
rqtを起動させた後，”Plugins”→”Robot Tools”→”Robot Steering”を選ぶと前後速度指令，回転指令をすることができる．
<br>
また，下記コマンドを実行することで移動ロボットをキーボード操作で動かすことも可能である．
```
$ rosrun wheel_robot_control key_teleop.py
```
これで移動ロボットを動かすことで地図作成が可能となった．
<br>
地図の保存方法を下記コマンドで示す．保存される地図は下記コマンドを実行したディレクトリに入る．また，末尾の”test”は保存時のファイルネームとなる．
```
$ rosrun map_server map_saver -f test
```
続いて，amclによる自己位置推定が可能であることを確認する．
```
$ roslaunch diff_mobile_robot diff_mobile_gazebo.launch
$ roslaunch diff_mobile_robot amcl.launch
$ rosrun rviz rviz
```
※↑rviz起動後，”Add”ボタンをクリックし，出現するウィンドウから
<br>
”RobotModel”，”Map”，”PoseArray”
<br>
を追加する．
<br>
その後，”Map”タブ内のTopicを”/map”に設定する．また，”PoseArray” タブ内のTopicを”/particlecloud”に設定する．
<br>
ここで，rviz上の2D Nav Goalをクリックし，ロボットのゴールを決めると，ロボットが移動を始める，amclによる自己位置推定の様子は”PoseArray”の赤い矢印で確認できる．
<br>
次に，waypoint作成手順を示す．
<br>
下記コマンドを実行することでwaypointが作成できる．
```
$ roslaunch diff_mobile_robot diff_mobile_gazebo.launch
$ roslaunch wheel_robot_gmapping wheel_robot_gmapping.launch
$ rosrun rviz rviz
$ rosrun odom_listener odom_listener
```
下記コマンドはどちらかで良い．
```
$ rqt
or
$ rosrun wheel_robot_control key_teleop.py
```
これで，odom_listenerを実行したディレクトリにwaypoints.yamlが生成される．
<br>
また，今回生成されたyamlファイルをDiff Waypoints.yamlにリネームした．
<br>
さらに，Diff Waypoints.yamlを下記のディレクトリに移動させる必要がある．
<br>
~/catkin_ws/src/wheel_robot_nav/waypoints
<br>
waypointを用いたナビゲーション手順を以下に示す．
<br>
先ほど作成したDiff Waypoints.yamlを使用する．
<br>
ナビゲーションには下記コマンドを実行することで可能となる．
```
$ roslaunch diff_mobile_robot diff_mobile_gazebo.launch
$ roslaunch wheel_robot_gmapping wheel_robot_gmapping.launch
$ rosrun rviz rviz
```
※↑rviz起動後，”Add”ボタンをクリックし，出現するウィンドウから”RobotModel”，”Map”を追加する．
<br>
その後，”Map”タブ内のTopicを”/map”と設定する．
<br>
```
$ roslaunch wheel_robot_nav wheel_robot_nav.launch
```
※↑のlaunchファイルは差動二輪ロボットのwaypoint（Diff Waypoints.yaml）を読み込むために一部変更を加えてある．
<br>
これで先ほど作成したDiffWaypoints.yamlに従ってロボットが移動を始める．
<br>
また，各waypointを確認するには，rviz上の”Add”ボタンをクリックし，出現するウィンドウの”By topic”タブから” vizualization_marker”，を追加する．
<br>
また，同様に”By topic”タブから”/move_base/current_goal/Pose”を追加することでロボットの移動方向が視覚的に分かる．
<br>
更に，”/ move_base/NavfnROS/plan/Path”を追加するとゴールまでの経路計画が視覚的に確認できる．
