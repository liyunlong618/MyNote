___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 5.7 GA中在服务器端生成火球
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

  - 1.只有服务器才能生成火球；

  - 2.GA中，使用API：GetAvatarActorFromActorInfo 拿到使用该GA的Actor。

  - 3.GA中，使用API：GetOwningActorFromActorInfo 获取Owner

  - 4.使用 GetWorld()->SpawnActorDeferred 延时生成Actor(延时生成还需要调用 FinishSpawning )

  - 5.GA中通过WaitGamePlayEvent，接收事件的Tag，发送时使用SendGameplayEventToActor，发送事件Tag

- 视频链接

  - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 https://b23.tv/YGFNaih

  - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 https://b23.tv/8CmnhX9

  - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 https://b23.tv/4G4lRhv

- UAuraProjectileSpell中，创建抛射物体Class在GA中配置

  - ![img](https://api2.mubu.com/v3/document_image/25165450_712b6e12-689b-4e76-824c-5425d0b4abbe.png)

- 因为角色的基类中共同继承了接口ICombatInterface,在该接口类中，创建虚函数：获取插槽Location

  - ![img](https://api2.mubu.com/v3/document_image/25165450_231cde4b-bfee-4043-b0a2-362d66fddbf7.png)

  - ![img](https://api2.mubu.com/v3/document_image/25165450_2be042b4-a8f5-40df-922c-0953513e1eb9.png)

- 角色基类中添加一个FName的变量，用来标注要发射的插槽名字，重写接口虚函数，返回该FName的位置

  - ![img](https://api2.mubu.com/v3/document_image/25165450_96db9d6f-94b3-41eb-b00a-cf8e542997fb.png)

  - ![img](https://api2.mubu.com/v3/document_image/25165450_063e3d26-7f53-4a73-cc2f-52424dd33395.png)

- 只有服务器才能生成火球；使用API：GetAvatarActorFromActorInfo 拿到使用该GA的Actor。判断该Actor是否实现了接口类，若实现了，获取插槽位置，设置Transform,使用 SpawnActorDeferred 延时生成Actor(延时生成还需要调用 FinishSpawning )，使用API：GetOwningActorFromActorInfo 获取Owner

  - ![img](https://api2.mubu.com/v3/document_image/25165450_fc607991-ab78-4d72-f912-2651a7a5a137.png)

- 蓝图中配置

  - ![img](https://api2.mubu.com/v3/document_image/25165450_bb886772-80c4-407d-d659-01d5439ba348.png)![img](https://api2.mubu.com/v3/document_image/25165450_15bd2e0a-c631-43c7-d9a8-0294726426d4.png)![img](https://api2.mubu.com/v3/document_image/25165450_d692e49c-f29c-4435-9b8e-5aa01a6ee55d.png)

- 在项目设置game play tag里面加入Event.Montage.Tag

  - ![img](https://api2.mubu.com/v3/document_image/25165450_8f39863b-a15a-49bd-d67a-1ecb64c49d24.png)

  - ![img](https://api2.mubu.com/v3/document_image/25165450_6e671305-e597-4233-ca6a-b5faf5bccde0.png)

- GA中使用蓝图节点 WaitGamePlayEvent

  - ![img](https://api2.mubu.com/v3/document_image/25165450_dbdccf6a-f0dc-4c9c-ae16-76ae3a612f12.png)

- 创建蒙太奇，记得检查插槽

  - ![img](https://api2.mubu.com/v3/document_image/25165450_dc0cd16d-8e42-4baf-8bf6-3a0694c176f1.png)![img](https://api2.mubu.com/v3/document_image/25165450_cd0269e1-b7b7-4da9-9814-8d909ac32ede.png)![img](https://api2.mubu.com/v3/document_image/25165450_09b37919-091a-499e-fe89-c8d0f2e2d8dd.png)

- 创建动画通知，重写函数，使用SendGameplayEventToActor，Tag创建变量，便于在外面设置

  - ![img](https://api2.mubu.com/v3/document_image/25165450_bb5898d5-d78a-4230-82f4-7b544a4d5162.png)![img](https://api2.mubu.com/v3/document_image/25165450_eea63f46-bb15-4d74-add4-c3d51a2488df.png)![img](https://api2.mubu.com/v3/document_image/25165450_d2a69995-13b9-4cd0-f53b-d7a8f0fbd87f.png)![img](https://api2.mubu.com/v3/document_image/25165450_578e78c8-9c93-4cc3-e0f9-8f89167f51b0.png)![img](https://api2.mubu.com/v3/document_image/25165450_d3cc5042-c079-4856-a6a0-7279943730d3.png)![img](https://api2.mubu.com/v3/document_image/25165450_ed18c8a3-a2cb-417e-a37f-8003c7646002.png)

- 触发时打印测试

  - ![img](https://api2.mubu.com/v3/document_image/25165450_78cea46e-e13b-4413-be5a-33cc1d6619d8.png)

  - 改完记得改回来！！！！！
    - ![img](https://api2.mubu.com/v3/document_image/25165450_8375d135-cbe1-4098-e7a1-8129b2fd8849.png)

- 测试结果gif，流程：点击鼠标后，播放动画蒙太奇到指定时机发送AnimNotify发送Tag，受到Tag时，屏幕左上角打印（火球暂时还没修改）![img](https://api2.mubu.com/v3/document_image/25165450_4c115136-a834-4575-8ed6-20aceb7260ac.gif)

- 小测试:

  

  

  

  

  - ![img](https://api2.mubu.com/v3/document_image/8c411d8c-3021-4c2f-9623-e1a026365dbd.jpg)![img](https://api2.mubu.com/v3/document_image/ea1f82a5-b30e-49a0-b425-299ca5a24c36.jpg)![img](https://api2.mubu.com/v3/document_image/809079a6-eade-40da-aeff-4ec2f0e2ea40.jpg)

- 此时有一个bug点击没有cd，这个先不管，先修正方向![img](https://api2.mubu.com/v3/document_image/3040d5fc-f473-406e-b1dd-3172810fdbe0.jpg)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________