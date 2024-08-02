___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 6.3 使用MotionWarping插件，进行角色FaceTo功能
___________________________________________________________________________________________
## 处理关键点
1. 这里是关键点
2. 这里是关键点
3. 这里是关键点
4. 这里是关键点
5. 这里是关键点
6. 这里是关键点
7. 这里是关键点
8. 这里是关键点
9. 这里是关键点
10. 这里是关键点
___________________________________________________________________________________________

[TOC]

___________________________________________________________________________________________

- 处理关键点：

  - 1.MotionWarping插件使用流程

    - //1.开启插件

    - //2.角色上添加组件

    - //3.检查动画是否为根动画

    - //4.动画蒙太奇中添加MotionWarping通知状态，并配置相关设置

    - //5.在使用时，使用组件->AddOrUpdateWarpTargetFromLocation函数传入要转向的位置(插件内自动计算角度并根据动画状态时长设置旋转速率)

- 使用插件MotionWarping

  - ![img](https://api2.mubu.com/v3/document_image/073022ca-d07f-4884-bdca-b43f4e3d5309.jpg)

- 视频链接

  - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 https://b23.tv/1vjh96a

- 此时直接搜搜不到MotionWarping组件

  - ![img](https://api2.mubu.com/v3/document_image/25165450_d47b7584-ecde-4ca1-c01e-6d9930634920.png)

- 需要开启插件MotionWarping

  - ![img](https://api2.mubu.com/v3/document_image/25165450_241cf0b3-d4fe-45d3-89ce-e8b1513752c8.png)

- BP_Aura中添加MotionWarping组件

  - ![img](https://api2.mubu.com/v3/document_image/25165450_516a30a5-86e1-4112-c380-ee79e2d39299.png)

- 该动画文件必须启用根运动！！！！

  - ![img](https://api2.mubu.com/v3/document_image/25165450_3fdd75bf-2fce-4c13-91f1-64128439e1e3.png)![img](https://api2.mubu.com/v3/document_image/25165450_14e53b77-1e74-48cf-a570-a1fe00ec079e.png)

- 1.蒙太奇AM_Cast_FireBolt添加动画统治状态MotionWarping

  - 添加一个动画通知轨道，修改轨道名字
    - ![img](https://api2.mubu.com/v3/document_image/25165450_9c5159f2-f885-4fb4-8dd9-b20ea61adcf5.png)

  - MotionWarping轨道上添加动画统治状态MotionWarping

    - ![img](https://api2.mubu.com/v3/document_image/25165450_7bf6b193-ef2f-4cdb-ae3b-aac5b68f147b.png)

    - ![img](https://api2.mubu.com/v3/document_image/25165450_b94f3770-6d19-477b-9370-f7e71c02a7c9.png)

- 2.设置MotionWarping参数，设置名字，不用位移，只要旋转，设置转向目标

  - 我们的动画将旋转我们的根骨骼以面向我们的目标，我们称之为面向目标。![img](https://api2.mubu.com/v3/document_image/25165450_9384b2ab-3b00-42f2-ba83-34013c4cdab2.png)![img](https://api2.mubu.com/v3/document_image/25165450_2ab8a7e7-9068-4272-a152-097e57354b4e.png)![img](https://api2.mubu.com/v3/document_image/25165450_39312ce5-c077-48ab-bf09-f84ee329fef7.png)

- 3.蓝图中创建自定义事件SetFacingTarget，设置MotionWarping组件的location参数

  - ![img](https://api2.mubu.com/v3/document_image/25165450_7b032b86-2412-4e63-aca5-1b97e169fcbd.png)

- 4.GA_FireBolt中，播放蒙太奇前获取角色，调用设置location函数SetFacingTarget

  - ![img](https://api2.mubu.com/v3/document_image/25165450_d3c64820-9738-4b85-fc25-6d8f9e8698b7.png)

- 小测试

  

  - ICombatInterface接口中，创建返回FVector的虚函数，蓝图实现
    - ![img](https://api2.mubu.com/v3/document_image/25165450_eaa48e4b-a2fd-4326-dac3-33c77d84520f.png)

  - 蓝图BP_Aura中实现，替换自定义事件
    - ![img](https://api2.mubu.com/v3/document_image/25165450_faaed9b2-8982-4413-eb39-f98e483cc1da.png)

  - 此时 Cast 搜不到 接口类

    - 此时cast搜不到接口类![img](https://api2.mubu.com/v3/document_image/25165450_d002b66a-6c4b-4eeb-9dbe-f41bf0242d3d.png)

    - 需要加上蓝图类的宏![img](https://api2.mubu.com/v3/document_image/25165450_7bba3417-3319-4ed4-802a-3091306a3049.png)

  - 获取该接口类虚函数，找不到

    - 获取该接口类虚函数，找不到![img](https://api2.mubu.com/v3/document_image/25165450_b0d0315f-85ff-494f-a5ed-27efe3682dc5.png)

    - 加上蓝图可叫 宏![img](https://api2.mubu.com/v3/document_image/25165450_a723f487-0212-4e76-98dd-a68d6aff7cb5.png)

  - 可以使用了

    - ![img](https://api2.mubu.com/v3/document_image/25165450_1d2da472-1bab-4131-c1b0-1c7a40d9c2d3.png)

    - ![img](https://api2.mubu.com/v3/document_image/25165450_56692627-8a4b-49f7-94d9-36d959eb7bcd.png)

- 此时效果gif![img](https://api2.mubu.com/v3/document_image/25165450_4a7b7915-ba30-41fa-d769-6f685452d5a7.gif)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________