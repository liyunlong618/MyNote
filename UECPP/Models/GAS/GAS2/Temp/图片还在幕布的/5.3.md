___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 5.3 人物沿样条线运动 获取NaviMesh的Path导航路径上的点
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

- 处理关键点:

  - 1.样条线API

  - 2.获取NaviMesh的导航路径NaviPath上的点

- 视频链接

  - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 https://b23.tv/Wl5H4dP

- 创建AutoRun函数，只有bAutoRunninn=true才能进入；先拿到角色；调用样条线API:FindLocationClosestToWorldLocation传入位置返回最近的样条线上的点；调用样条线API:FindDirectionClosestToWorldLocation传入上面获取的样条线上的点;调用角色API:AddMovementInput传入Dir;创建float =  样条线上最近的点与角色要到达的地方的距离;判断，若距离小于最小距离的阈值，设置 bAutoRunning = false

  - ![img](https://api2.mubu.com/v3/document_image/25165450_d9d793bf-7c27-448f-afa4-1208627bb874.png)

- 此时在客户端上有bug无法实现点击移动，且 没有DebugSphere出现，原因是NaviMesh导航没有在客户端上开启。开启步骤:

  - GIF

    - GIF：客户端bAutoRunning = true表现![img](https://api2.mubu.com/v3/document_image/25165450_b01c9809-2074-4bc6-eeff-47c4e156ce1f.gif)

    - GIF：服务器bAutoRunning = true表现![img](https://api2.mubu.com/v3/document_image/25165450_92e5ec3b-016b-42f2-8933-2578c72a023a.gif)

  - NaviMesh导航配置，在客户端上开启

    - 英文版配置![img](https://api2.mubu.com/v3/document_image/ceffbe31-eceb-4b8e-88ce-7cef5e8c4999.jpg)

    - 中文版配置![img](https://api2.mubu.com/v3/document_image/25165450_a6726681-ea8d-4813-e5a4-45a929ec1f30.png)

- 此时有bug为，若点击无法到达的地点(比如障碍物正中心)会导致bAutoRunning变量无法设置为false。处理方法:

  - 第一步  因为点击是根据碰撞通道ECC_Visibility所以把障碍物的Visibility通道设为忽略
    - ![img](https://api2.mubu.com/v3/document_image/25165450_a6b20e49-1ae9-4f5f-ef69-5cf5cf88fc9e.png)

  - 第一步修复完后，还没有解决，因为目标地点还没有修改

  - 第二步 AbilityInputTagReleased函数中，处理要到达的地点:在之前计算获取目标地点时，使用的是被击中的地点作为终点，需要修改为，通过NaviPath路径获取最后一个点，并把这个点的位置给 要到达的地点CachedDestination
    - ![img](https://api2.mubu.com/v3/document_image/25165450_78d385c0-14c4-4e57-9e3e-dc5f42b46552.png)

- 完成，此时效果gif，人物会移动到最后一个NaviMesh点![img](https://api2.mubu.com/v3/document_image/25165450_396df62c-527b-4182-8b96-e7c7eef5f2be.gif)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________