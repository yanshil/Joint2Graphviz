# Joint2Graphviz

### What this script for?

A Fusion 360 script to check the correctness of the assembled structure.

A valid assembled structure should has the following properties:
1. base_link should be the only root node.
2. Should be a DAG

### To run this script
1. Sometimes (Or saying it can get avoid of most errors) you need to set **"Do not capture design history"** before running the script.

2. Copy the content of the generated "graph.txt" and go to http://www.webgraphviz.com/

### Correct Example:

```
digraph G {  "base_link" -> "Finger1link_0.0_v11" [ label = "Finger1" ] 
  "base_link" -> "Finger2link_0.0_v11" [ label = "Finger2" ] 
  "base_link" -> "Finger3link_0.0_v11" [ label = "Finger3" ] 
  "base_link" -> "link_12.0_right_v11" [ label = "InHand" ] 
  "link_12.0_right_v11" -> "Finger4link_0.0_v11" [ label = "Finger4" ] 
  "Finger1link_0.0_v11" -> "Finger1link_1.0_v11" [ label = "Finger1_Link1" ] 
  "Finger1link_1.0_v11" -> "Finger1link_2.0_v11" [ label = "Finger1_Link2" ] 
  "Finger1link_2.0_v11" -> "Finger1link_3.0_v11" [ label = "Finger1_link3" ] 
  "Finger2link_0.0_v11" -> "Finger2link_1.0_v11" [ label = "Finger2_Link1" ] 
  "Finger2link_1.0_v11" -> "Finger2link_2.0_v11" [ label = "Finger2_Link2" ] 
  "Finger2link_2.0_v11" -> "Finger2link_3.0_v11" [ label = "Finger2_link3" ] 
  "Finger3link_0.0_v11" -> "Finger3link_1.0_v11" [ label = "Finger3_Link1" ] 
  "Finger3link_1.0_v11" -> "Finger3link_2.0_v11" [ label = "Finger3_Link2" ] 
  "Finger3link_2.0_v11" -> "Finger3link_3.0_v11" [ label = "Finger3_link3" ] 
  "Finger4link_0.0_v11" -> "Finger4link_1.0_v11" [ label = "Finger4_Link1" ] 
  "Finger4link_1.0_v11" -> "Finger4link_2.0_v11" [ label = "Finger4_Link2" ] 
  "Finger4link_2.0_v11" -> "Finger4link_3.0_v11" [ label = "Finger4_link3" ] 
}
```
![](https://github.com/yanshil/Joint2Graphviz/blob/master/imgs/Correct_graphviz.PNG)

### Wrong Example 1:

```
digraph G {  "R_BotPlate1" -> "R_MiddleCylinder1"
  "R_MiddleCylinder1" -> "R_TopPlate1"
  "R_TopPlate1" -> "base_link1"
  "R_TopPlate1" -> "Wheel_set1Roller1"
  "R_TopPlate1" -> "Wheel_set2Roller1"
  "R_TopPlate1" -> "Wheel_set3Roller1"
  "R_TopPlate1" -> "Wheel_set4Roller1"
  "R_TopPlate1" -> "Wheel_set6Roller1"
  "R_TopPlate1" -> "Wheel_set7Roller1"
  "R_TopPlate1" -> "Wheel_set8Roller1"
  "R_TopPlate1" -> "Wheel_set5Roller1"
  "Wheel_set1Roller1" -> "Wheel_set1Satellite_Wheel1"
  "Wheel_set2Roller1" -> "Wheel_set2Satellite_Wheel1"
  "Wheel_set3Roller1" -> "Wheel_set3Satellite_Wheel1"
  "Wheel_set4Roller1" -> "Wheel_set4Satellite_Wheel1"
  "Wheel_set5Roller1" -> "Wheel_set5Satellite_Wheel1"
  "Wheel_set6Roller1" -> "Wheel_set6Satellite_Wheel1"
  "Wheel_set7Roller1" -> "Wheel_set7Satellite_Wheel1"
  "Wheel_set8Roller1" -> "Wheel_set8Satellite_Wheel1"
}
```

Click Generate Graph and I get ![](https://github.com/yanshil/Joint2Graphviz/blob/master/imgs/Error_graphviz1.png)

Here I can find out 

1.  base_link is wrongly set as R_TopPlate's child
2. R_MiddleCylinder should be R_TopPlate's child but it's set as parent
3. R_BotPlate should be R_MiddleCylinder's child but it's set as parent.

### Wrong Example 2: 

```
digraph G {  "base_link" -> "Wheel_Motor_holder_v41" [ label = "Rigid31" ] 
  "base_link" -> "Wheel_Motor_holder_v42" [ label = "Rigid32" ] 
  "base_link" -> "Wheel_Motor_holder_v43" [ label = "Rigid33" ] 
  "base_link" -> "Wheel_Motor_holder_v44" [ label = "Rigid34" ] 
  "base_link" -> "Side_board1" [ label = "Rigid35" ] 
  "base_link" -> "Side_board2" [ label = "Rigid36" ] 
  "base_link" -> "Gear_Pan_Base1" [ label = "Rigid37" ] 
  "Gear_Pan_Base1" -> "carboat_bot1" [ label = "Rigid38" ] 
  "Gear_Pan_Base1" -> "carboat_21" [ label = "Rigid39" ] 
  "Servo11" -> "carboat_31" [ label = "Neck_servo" ] 
  "carboat_31" -> "Servo21" [ label = "Rigid42" ] 
  "carboat_21" -> "motor_support1" [ label = "Rigid43" ] 
  "motor_support1" -> "Servo11" [ label = "Rigid44" ] 
  "Servo21" -> "Gear_Pan_Neck1" [ label = "Top_servo" ] 
  "Gear_Pan_Neck1" -> "Camera_support1" [ label = "Rigid46" ] 
  "Camera_support1" -> "D3541" [ label = "Rigid47" ] 
  "Wheel_Motor_holder_v41" -> "Wheel_Motor1" [ label = "Rigid48" ] 
  "Wheel_Motor_holder_v42" -> "Wheel_Motor2" [ label = "Rigid49" ] 
  "Wheel_Motor_holder_v43" -> "Wheel_Motor3" [ label = "Rigid50" ] 
  "Wheel_Motor_holder_v44" -> "Wheel_Motor4" [ label = "Rigid51" ] 
  "Wheel_Motor1" -> "Right1Top_Base_r1" [ label = "RB_wheel" ] 
  "Wheel_Motor2" -> "Left1Top_Base1" [ label = "RF_wheel" ] 
  "Wheel_Motor4" -> "Left2Top_Base1" [ label = "LB_wheel" ] 
  "Wheel_Motor3" -> "Right2Top_Base_r1" [ label = "LF_wheel" ] 
  "Right1Plate_bot_r1" -> "Right1Middle_Cylinder_r1" [ label = "Right1_Rigid1" ] 
  "Right1Middle_Cylinder_r1" -> "Right1Plate_top_r1" [ label = "Right1_Rigid2" ] 
  "Right1Plate_top_r1" -> "Right1Top_Base_r1" [ label = "Right1_Rigid3" ] 
  "Right1Plate_top_r1" -> "Right1Wheel_sets_r1Roller1" [ label = "Right1_Rigid4" ] 
  "Right1Plate_top_r1" -> "Right1Wheel_sets_r2Roller1" [ label = "Right1_Rigid6" ] 
  "Right1Plate_top_r1" -> "Right1Wheel_sets_r3Roller1" [ label = "Right1_Rigid7" ] 
  "Right1Plate_top_r1" -> "Right1Wheel_sets_r4Roller1" [ label = "Right1_Rigid8" ] 
  "Right1Plate_top_r1" -> "Right1Wheel_sets_r6Roller1" [ label = "Right1_Rigid9" ] 
  "Right1Plate_top_r1" -> "Right1Wheel_sets_r7Roller1" [ label = "Right1_Rigid10" ] 
  "Right1Plate_top_r1" -> "Right1Wheel_sets_r8Roller1" [ label = "Right1_Rigid11" ] 
  "Right1Plate_top_r1" -> "Right1Wheel_sets_r5Roller1" [ label = "Right1_Rigid12" ] 
  "Right1Wheel_sets_r1Roller1" -> "Right1Wheel_sets_r1Satellite_Wheel1" [ label = "Right1Wheel_sets_r1_Rev5" ] 
  "Right1Wheel_sets_r2Roller1" -> "Right1Wheel_sets_r2Satellite_Wheel1" [ label = "Right1Wheel_sets_r2_Rev5" ] 
  "Right1Wheel_sets_r3Roller1" -> "Right1Wheel_sets_r3Satellite_Wheel1" [ label = "Right1Wheel_sets_r3_Rev5" ] 
  "Right1Wheel_sets_r4Roller1" -> "Right1Wheel_sets_r4Satellite_Wheel1" [ label = "Right1Wheel_sets_r4_Rev5" ] 
  "Right1Wheel_sets_r5Roller1" -> "Right1Wheel_sets_r5Satellite_Wheel1" [ label = "Right1Wheel_sets_r5_Rev5" ] 
  "Right1Wheel_sets_r6Roller1" -> "Right1Wheel_sets_r6Satellite_Wheel1" [ label = "Right1Wheel_sets_r6_Rev5" ] 
  "Right1Wheel_sets_r7Roller1" -> "Right1Wheel_sets_r7Satellite_Wheel1" [ label = "Right1Wheel_sets_r7_Rev5" ] 
  "Right1Wheel_sets_r8Roller1" -> "Right1Wheel_sets_r8Satellite_Wheel1" [ label = "Right1Wheel_sets_r8_Rev5" ] 
  "Left1Plate_bot1" -> "Left1Middle_Cylinder1" [ label = "Left1_Rigid1" ] 
  "Left1Middle_Cylinder1" -> "Left1Plate_top1" [ label = "Left1_Rigid2" ] 
  "Left1Plate_top1" -> "Left1Wheel_sets1Roller_8_11" [ label = "Left1_Rigid5" ] 
  "Left1Plate_top1" -> "Left1Wheel_sets8Roller_8_11" [ label = "Left1_Rigid6" ] 
  "Left1Plate_top1" -> "Left1Wheel_sets7Roller_8_11" [ label = "Left1_Rigid7" ] 
  "Left1Plate_top1" -> "Left1Wheel_sets6Roller_8_11" [ label = "Left1_Rigid8" ] 
  "Left1Plate_top1" -> "Left1Wheel_sets5Roller_8_11" [ label = "Left1_Rigid9" ] 
  "Left1Plate_top1" -> "Left1Wheel_sets4Roller_8_11" [ label = "Left1_Rigid10" ] 
  "Left1Plate_top1" -> "Left1Wheel_sets3Roller_8_11" [ label = "Left1_Rigid11" ] 
  "Left1Plate_top1" -> "Left1Wheel_sets2Roller_8_11" [ label = "Left1_Rigid12" ] 
  "Left1Plate_top1" -> "Left1Top_Base1" [ label = "Left1_Rigid13" ] 
  "Left1Wheel_sets1Roller_8_11" -> "Left1Wheel_sets1Satellite_Wheel_8_11" [ label = "Left1Wheel_sets1_Rev1" ] 
  "Left1Wheel_sets2Roller_8_11" -> "Left1Wheel_sets2Satellite_Wheel_8_11" [ label = "Left1Wheel_sets2_Rev1" ] 
  "Left1Wheel_sets3Roller_8_11" -> "Left1Wheel_sets3Satellite_Wheel_8_11" [ label = "Left1Wheel_sets3_Rev1" ] 
  "Left1Wheel_sets4Roller_8_11" -> "Left1Wheel_sets4Satellite_Wheel_8_11" [ label = "Left1Wheel_sets4_Rev1" ] 
  "Left1Wheel_sets5Roller_8_11" -> "Left1Wheel_sets5Satellite_Wheel_8_11" [ label = "Left1Wheel_sets5_Rev1" ] 
  "Left1Wheel_sets6Roller_8_11" -> "Left1Wheel_sets6Satellite_Wheel_8_11" [ label = "Left1Wheel_sets6_Rev1" ] 
  "Left1Wheel_sets7Roller_8_11" -> "Left1Wheel_sets7Satellite_Wheel_8_11" [ label = "Left1Wheel_sets7_Rev1" ] 
  "Left1Wheel_sets8Roller_8_11" -> "Left1Wheel_sets8Satellite_Wheel_8_11" [ label = "Left1Wheel_sets8_Rev1" ] 
  "Left2Plate_bot1" -> "Left2Middle_Cylinder1" [ label = "Left2_Rigid1" ] 
  "Left2Middle_Cylinder1" -> "Left2Plate_top1" [ label = "Left2_Rigid2" ] 
  "Left2Plate_top1" -> "Left2Wheel_sets1Roller_8_11" [ label = "Left2_Rigid5" ] 
  "Left2Plate_top1" -> "Left2Wheel_sets8Roller_8_11" [ label = "Left2_Rigid6" ] 
  "Left2Plate_top1" -> "Left2Wheel_sets7Roller_8_11" [ label = "Left2_Rigid7" ] 
  "Left2Plate_top1" -> "Left2Wheel_sets6Roller_8_11" [ label = "Left2_Rigid8" ] 
  "Left2Plate_top1" -> "Left2Wheel_sets5Roller_8_11" [ label = "Left2_Rigid9" ] 
  "Left2Plate_top1" -> "Left2Wheel_sets4Roller_8_11" [ label = "Left2_Rigid10" ] 
  "Left2Plate_top1" -> "Left2Wheel_sets3Roller_8_11" [ label = "Left2_Rigid11" ] 
  "Left2Plate_top1" -> "Left2Wheel_sets2Roller_8_11" [ label = "Left2_Rigid12" ] 
  "Left2Plate_top1" -> "Left2Top_Base1" [ label = "Left2_Rigid13" ] 
  "Left2Wheel_sets1Roller_8_11" -> "Left2Wheel_sets1Satellite_Wheel_8_11" [ label = "Left2Wheel_sets1_Rev1" ] 
  "Left2Wheel_sets2Roller_8_11" -> "Left2Wheel_sets2Satellite_Wheel_8_11" [ label = "Left2Wheel_sets2_Rev1" ] 
  "Left2Wheel_sets3Roller_8_11" -> "Left2Wheel_sets3Satellite_Wheel_8_11" [ label = "Left2Wheel_sets3_Rev1" ] 
  "Left2Wheel_sets4Roller_8_11" -> "Left2Wheel_sets4Satellite_Wheel_8_11" [ label = "Left2Wheel_sets4_Rev1" ] 
  "Left2Wheel_sets5Roller_8_11" -> "Left2Wheel_sets5Satellite_Wheel_8_11" [ label = "Left2Wheel_sets5_Rev1" ] 
  "Left2Wheel_sets6Roller_8_11" -> "Left2Wheel_sets6Satellite_Wheel_8_11" [ label = "Left2Wheel_sets6_Rev1" ] 
  "Left2Wheel_sets7Roller_8_11" -> "Left2Wheel_sets7Satellite_Wheel_8_11" [ label = "Left2Wheel_sets7_Rev1" ] 
  "Left2Wheel_sets8Roller_8_11" -> "Left2Wheel_sets8Satellite_Wheel_8_11" [ label = "Left2Wheel_sets8_Rev1" ] 
  "Right2Plate_bot_r1" -> "Right2Middle_Cylinder_r1" [ label = "Right2_Rigid1" ] 
  "Right2Middle_Cylinder_r1" -> "Right2Plate_top_r1" [ label = "Right2_Rigid2" ] 
  "Right2Plate_top_r1" -> "Right2Top_Base_r1" [ label = "Right2_Rigid3" ] 
  "Right2Plate_top_r1" -> "Right2Wheel_sets_r1Roller1" [ label = "Right2_Rigid4" ] 
  "Right2Plate_top_r1" -> "Right2Wheel_sets_r2Roller1" [ label = "Right2_Rigid6" ] 
  "Right2Plate_top_r1" -> "Right2Wheel_sets_r3Roller1" [ label = "Right2_Rigid7" ] 
  "Right2Plate_top_r1" -> "Right2Wheel_sets_r4Roller1" [ label = "Right2_Rigid8" ] 
  "Right2Plate_top_r1" -> "Right2Wheel_sets_r6Roller1" [ label = "Right2_Rigid9" ] 
  "Right2Plate_top_r1" -> "Right2Wheel_sets_r7Roller1" [ label = "Right2_Rigid10" ] 
  "Right2Plate_top_r1" -> "Right2Wheel_sets_r8Roller1" [ label = "Right2_Rigid11" ] 
  "Right2Plate_top_r1" -> "Right2Wheel_sets_r5Roller1" [ label = "Right2_Rigid12" ] 
  "Right2Wheel_sets_r1Roller1" -> "Right2Wheel_sets_r1Satellite_Wheel1" [ label = "Right2Wheel_sets_r1_Rev5" ] 
  "Right2Wheel_sets_r2Roller1" -> "Right2Wheel_sets_r2Satellite_Wheel1" [ label = "Right2Wheel_sets_r2_Rev5" ] 
  "Right2Wheel_sets_r3Roller1" -> "Right2Wheel_sets_r3Satellite_Wheel1" [ label = "Right2Wheel_sets_r3_Rev5" ] 
  "Right2Wheel_sets_r4Roller1" -> "Right2Wheel_sets_r4Satellite_Wheel1" [ label = "Right2Wheel_sets_r4_Rev5" ] 
  "Right2Wheel_sets_r5Roller1" -> "Right2Wheel_sets_r5Satellite_Wheel1" [ label = "Right2Wheel_sets_r5_Rev5" ] 
  "Right2Wheel_sets_r6Roller1" -> "Right2Wheel_sets_r6Satellite_Wheel1" [ label = "Right2Wheel_sets_r6_Rev5" ] 
  "Right2Wheel_sets_r7Roller1" -> "Right2Wheel_sets_r7Satellite_Wheel1" [ label = "Right2Wheel_sets_r7_Rev5" ] 
  "Right2Wheel_sets_r8Roller1" -> "Right2Wheel_sets_r8Satellite_Wheel1" [ label = "Right2Wheel_sets_r8_Rev5" ] 
}
```

![](https://github.com/yanshil/Joint2Graphviz/blob/master/imgs/Error_graphviz2.png)

Here I can find out 

1. Multiple root nodes appears.


Both examples cannot run successfully for the urdf generation code.