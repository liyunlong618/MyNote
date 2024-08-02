___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 6.6 为火球添加GE；敌人设置和初始化AttributeSet；处理碰撞bug
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

  - 1.火球携带的不是GE而是FGameplayEffectSpecHandle，方便直接使用

  - 2.重温初始化AttributeSet的流程

- 视频链接

  - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 https://b23.tv/rjgs6gR

- 蓝图中创建一个GameplayEffect类

  - ![img](https://api2.mubu.com/v3/document_image/25165450_7e3794f8-9440-4c3f-c63a-f44ebb875dc8.png)

  - ![img](https://api2.mubu.com/v3/document_image/25165450_f004a599-320d-450e-ed8d-8fcccee43369.png)

  - ![img](https://api2.mubu.com/v3/document_image/25165450_068761b4-a1e4-4d3f-d027-6ee754ca2549.png)

- 想要 抛射物-火球 携带一个FGameplayEffectSpecHandle游戏效果规格手柄。![img](https://api2.mubu.com/v3/document_image/1fd23487-a206-43e5-b2e8-8447f0cdd1c3.jpg)

- 在抛射物火球中保存一个FGameplayEffectSpecHandle变量，设置为生成时公开，public 方便外部访问和调用

  - 

    

    - 如果报错，记得引头文件![img](https://api2.mubu.com/v3/document_image/25165450_c831b79d-ce62-4e1a-fcd1-63d1b4ef818d.png)

- 抛射物的GA中声明可以在蓝图中配置GE的变量

  - ![img](https://api2.mubu.com/v3/document_image/25165450_619013af-5c9c-4c97-8ff7-fa121f0c0f6a.png)

- UAuraProjectileSpell中SpawnProjectile生成火球的函数中，生成火球前，获取角色AvatarActor的ASC组件，生成FGameplayEffectSpecHandle给火球的实例SpecHandle赋值

  - ![img](https://api2.mubu.com/v3/document_image/25165450_fc251e89-f5a7-4049-86f1-fc105b1ec389.png)

- Overlap时权威端销毁前需要检查目标是否有ASC组件,然后使用FGameplayEffectSpecHandle应用伤害

  - ![img](https://api2.mubu.com/v3/document_image/25165450_2d70886f-977c-4ce2-f97c-e6a5280a950f.png)

- 在AS组件中，当属性发生变化时，UE_Log下

  - ![img](https://api2.mubu.com/v3/document_image/25165450_125051cd-0ce2-443d-e390-9a5995d04fc5.png)

- 这之前并没有为敌人初始化属性![img](https://api2.mubu.com/v3/document_image/dae0e689-481d-454c-84b7-2c648c0968c4.jpg)

- 为敌人初始化属性

  - ![img](https://api2.mubu.com/v3/document_image/25165450_e5569996-9352-4a2b-c4bd-4e130256b7b5.png)

- BP_EnemyBase为敌人的基类 赋值

  - ![img](https://api2.mubu.com/v3/document_image/25165450_eb127506-61c9-426b-e175-865708f58189.png)

- GA_FireBolt中配置要应用伤害的GE

  - ![img](https://api2.mubu.com/v3/document_image/25165450_282a7108-5f0a-45ff-90a7-e148a6389e28.png)

- 使用技能结束后，调用EndAbility

  - ![img](https://api2.mubu.com/v3/document_image/107696f6-7c8c-4d48-8dc4-0a369a091a34.jpg)

  - 我是这么干的![img](https://api2.mubu.com/v3/document_image/25165450_ab3fc116-f246-423d-8524-dba1652a3eeb.png)

- 此时测试UE_Log打印敌人血量

  - ![img](https://api2.mubu.com/v3/document_image/c22e82db-47ac-4fdc-ae2c-9d3535c098f4.jpg)

- 现在有bug，敌人不会初始化属性，主要属性正常，次要属性不对，原因是，敌人基类中，这个函数调错了![img](https://api2.mubu.com/v3/document_image/25165450_82db009d-4449-4160-96a5-94723ed03d9e.png)

- 这里之前有个bug，就是上一节在设置碰撞的问题，因为设置Mesh也检测，Capsule也检测，会触发两次检测，会有异常，解决办法是：设置Capsule关闭碰撞检测

  

  - C++中设置Capsule关闭碰撞检测![img](https://api2.mubu.com/v3/document_image/25165450_c561f420-a0d1-4e5a-b85c-5ed4e12ce81b.png)

- 此时LS模式的gif，客户端和服务器可以合作打怪了

  

  - ![img](https://api2.mubu.com/v3/document_image/25165450_3d37eb8c-2b20-4dc2-c116-81229833fa54.png)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________