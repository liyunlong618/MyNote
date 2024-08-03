___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 5.8 使用自定义AbilityTasks
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

  - 1.UFUNCTION宏的一些用法

    - UFUNCTION( meta = ( DisplayName = "TargetDataUnderMouse" ))          设置在蓝图编辑器中显示的函数名称

    - UFUNCTION( meta = ( Tooltip = "This is my custom function tooltip" ))   在蓝图编辑器中显示的提示信息，当鼠标悬停在函数或属性上时显示。

    - UFUNCTION( meta = ( HidePin="OwningAbility" ))                    隐藏特定的输入引脚（Pin）

    - UFUNCTION( meta = ( DefaultToSelf="OwningAbility" ))                   设置默认值。如果某个引脚没有被连接，蓝图将其值设置 为 self

    - UFUNCTION( meta = ( BlueprintInternalUseOnly = "true" ))                蓝图中仅限内部使用 宏

    - UFUNCTION( meta = ( DevelopmentOnly ))                          仅在开发版本中可见，发布版本中隐藏。

  - 2.UAbilityTask
    - 在蓝图中调用 UAbilityTask 的方法会被视为异步的，这是因为 UAbilityTask 类的设计本身就是为了处理异步任务。虽然在 C++ 代码中执行逻辑可能是同步的，但 UAbilityTask 的机制允许在蓝图中以异步方式使用它们。

- 视频链接

  - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 https://b23.tv/PRDsFB6

- 此时希望创建一个，触发GA时为我们获取数据的AbilityTask(比如获取鼠标点击时射线检测结果)

- 创建AbilityTask的C++类，取名TargetDataUnderMouse，保存鼠标点击时的射线检测结果数据

  - ![img](https://api2.mubu.com/v3/document_image/25165450_cad964a0-44e7-4766-b8d4-2948dc89d8a9.png)![img](https://api2.mubu.com/v3/document_image/25165450_09868c69-a5a8-4df9-a8fc-c7fa47f15136.png)

- UTargetDataUnderMouse中参考 蓝图的PlayMontageAndWait和WaitGameplayEvent，也创建一个 异步 的蓝图节点

  - 首先内部有一个静态函数，调用时创建一个自身的实例并返回

    - 

      

      - 宏的分别解释:

        - meta=() 括号内包含的是一些元数据参数

          - UFUNCTION( meta = ( DisplayName = "TargetDataUnderMouse" ))          设置在蓝图编辑器中显示的函数名称

          - UFUNCTION( meta = ( Tooltip = "This is my custom function tooltip" ))   在蓝图编辑器中显示的提示信息，当鼠标悬停在函数或属性上时显示。

          - UFUNCTION( meta = ( HidePin="OwningAbility" ))                    隐藏特定的输入引脚（Pin）

          - UFUNCTION( meta = ( DefaultToSelf="OwningAbility" ))                   设置默认值。如果某个引脚没有被连接，蓝图将其值设置 为 self

          - UFUNCTION( meta = ( BlueprintInternalUseOnly = "true" ))                蓝图中仅限内部使用 宏

          - UFUNCTION( meta = ( DevelopmentOnly ))                          仅在开发版本中可见，发布版本中隐藏。

    - 创建一个蓝图中可叫函数叫CreateTargetDataUnderMouse，分组"Ability|Tasks"，蓝图中命名为TargetDataUnderMouse，有一个参数UGameplayAbility* OwningAbility，蓝图中默参为self，对蓝图隐藏参数，蓝图中仅限内部使用 宏

    - ![img](https://api2.mubu.com/v3/document_image/25165450_cab175f2-f18f-4202-b66e-3a335e51b1a5.png)

    - 此时测试![img](https://api2.mubu.com/v3/document_image/25165450_400f87ea-6505-4293-8bc9-28bb072a9bf7.png)

  - 输出引脚均为多播委托

    - ![img](https://api2.mubu.com/v3/document_image/25165450_1bdce60d-d489-4817-b3da-a7b7355fef14.png)

    - 此时，输出引脚的这个不会执行，原因是没有广播该委托，也就不会收到信息![img](https://api2.mubu.com/v3/document_image/25165450_5ee14870-3bb4-41dc-facb-31ead0cb8af2.png)

  - 此时，需要重写父类中的虚函数Activate

    - 

      

      - 参考基类文件

        - 在基类的这里

          

          - 基类源文件中也只写了一个UElog![img](https://api2.mubu.com/v3/document_image/25165450_96f73818-8473-4104-ab84-6c2546e8162e.png)

    - 不用调用父类，因为父类啥也没写

      

      - 参考基类文件

        - 在基类的这里

          

          - 基类源文件中也只写了一个UElog![img](https://api2.mubu.com/v3/document_image/25165450_96f73818-8473-4104-ab84-6c2546e8162e.png)

- 小测试

  

  

  

  

  

  

  

  - 

    

    - ![img](https://api2.mubu.com/v3/document_image/25165450_ec9f4bd7-7cdc-417b-d801-946eb084d812.png)

    - 此时结果![img](https://api2.mubu.com/v3/document_image/25165450_035867d9-73ba-48c6-cb1f-169e1fe581c8.png)

  - 有一个bug就是只有本地可以收到，客户端本地没有问题，但是服务器上，位置是0,0,0点

    

    - 下节课处理这个问题

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________