___________________________________________________________________________________________
### [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)
___________________________________________________________________________________________
# GAS 2.2 通过(接口)实现(描边)效果

___________________________________________________________________________________________
# <font color=red>处理关键点：</font>

<font face="黑体" color=red size=3>1. 再C++中使用FName插槽名，将武器SK，绑定到角色SK上</font>

<font face="黑体" color=red size=3>xxxxxx</font>
1. 接口Interface的使用（比如权限和纯虚函数）

2. PlayerController中使用 获取鼠标的位置发射射线，返回结果 的函数（只识别block）

3. 自定义边缘发光深度材质 生效相关配置（Post Process Volume生效范围/后期处理材质配置）

4. 在项目文件中定义宏并使用
___________________________________________________________________________________________

- 创建C++接口类

  - ![img](https://api2.mubu.com/v3/document_image/25165450_56867690-f06c-4cfe-b0bf-324e0d3b5a6c.png)

- 创建两个(勾边/取消沟边)纯虚函数

  - 方法需要public!!!!![img](https://api2.mubu.com/v3/document_image/25165450_743b0c24-fce0-4a91-b9e1-540ef56cc19e.png)

- 在敌人的类中继承这个接口并实现这俩函数

  - ![img](https://api2.mubu.com/v3/document_image/25165450_d3decf2c-1466-4dc2-e37e-48033b1ae712.png)

- PC中创建鼠标发射射线的函数和调用PlayerTick

  - 头文件
    - ![img](https://api2.mubu.com/v3/document_image/25165450_dc865240-c726-4027-94ef-6e2ce1606412.png)

  - 源文件

    - 

      

      - 在 Unreal Engine 中，GetHitResultUnderCursor 使用的碰撞通道必须配置为阻挡（block）才能检测到碰撞。如果碰撞通道配置为重叠（overlap），则碰撞检测函数不会报告碰撞结果。

        - 解释原因
          - GetHitResultUnderCursor 函数依赖于碰撞通道配置的阻挡行为。当碰撞通道配置为重叠时，它仅用于生成重叠事件（如 OnOverlapBegin 和 OnOverlapEnd），而不是用于阻挡光线追踪或射线检测。因此，如果你希望在使用 GetHitResultUnderCursor 时检测到碰撞，你需要确保目标对象的碰撞通道配置为阻挡。

        - 解决方法
          - 确保你的 Pawn 或其他目标对象的碰撞设置正确配置为阻挡 ECC_Visibility 通道。

  - 知识点：PC中PlayerTick和Tick的区别？

    - PlayerTick和Tick都是用于更新控制器状态和执行特定功能的函数。

    - PlayerTick:

      - PlayerTick是PlayerController类的一个成员函数，用于处理与玩家直接相关的更新逻辑。

      - 这个函数被每帧调用一次，用于处理玩家的输入、更新玩家状态、执行碰撞检测等与玩家相关的操作。

      - 通常，PlayerTick函数用于处理与玩家控制相关的逻辑，例如检测玩家是否按下了特定的按键，或者更新玩家的位置和方向。

    - Tick:

      - Tick函数是Actor类的一个成员函数，而PlayerController是Actor的子类，因此PlayerController也继承了Tick函数。

      - 与PlayerTick不同，Tick函数是Actor类的通用更新函数，被每帧调用一次，用于处理与Actor相关的更新逻辑。

      - 在PlayerController中，您可以重写Tick函数以处理与控制器状态相关的更新逻辑，例如更新UI、执行特定的事件处理等。

    - PlayerTick函数用于处理与玩家控制相关的逻辑，而Tick函数则用于处理通用的Actor更新逻辑。

- 在敌人的类中创建bool变量来控制勾边的显示与否

  - 头文件中声明一个bool
    - ![img](https://api2.mubu.com/v3/document_image/25165450_c6ce4271-26b2-4a93-87ed-45ba07ae349a.png)

  - 源文件
    - ![img](https://api2.mubu.com/v3/document_image/25165450_b0cb5480-312a-4b52-c4f6-22cc8255571d.png)

- 创建一个敌人的BP总基类

  - 这样可以设置一些共有行为属性

  - ![img](https://api2.mubu.com/v3/document_image/25165450_43cd7158-d6d7-44d2-e84e-59c2497ee9c0.png)

- 修改BP敌人的继承类

  - ![img](https://api2.mubu.com/v3/document_image/25165450_ac8d47b6-3a74-4911-a9a2-941ddcd0ccd2.png)

  - ![img](https://api2.mubu.com/v3/document_image/25165450_6d657962-1e93-4772-a02a-c7d8c70b4322.png)

- 修改BP敌人的碰撞类型

  - ![img](https://api2.mubu.com/v3/document_image/25165450_4a9211d3-3ddd-47d4-b493-594e959e3e11.png)

- 敌人BP基类中添加测试逻辑

  - ![img](https://api2.mubu.com/v3/document_image/25165450_6ab5c800-a668-48ef-f733-eb1c39a672ff.png)

- 测试结果

  - ![img](https://api2.mubu.com/v3/document_image/25165450_33949dae-084a-47ee-f799-1c6bcf45897b.gif)

- 修改自定义边缘发光深度材质

  - 把这两个设为变量，并创建实例，便于调整

    

    - ![img](https://api2.mubu.com/v3/document_image/25165450_52b6908d-1b42-4324-80ba-788b085b698e.png)

  - 关于此描边材质详细可以看这个链接https://www.bilibili.com/video/BV1Ai4y177bZ/?spm_id_from=333.337.search-card.all.click

- 拖入PostProccessVolumes设置全局生效，配置自定义边缘发光深度材质

  - ![img](https://api2.mubu.com/v3/document_image/25165450_291e1aa8-95ff-431b-e000-f2c21574bbb2.png)

  - ![img](https://api2.mubu.com/v3/document_image/25165450_803fa260-19be-4ed8-b24e-39e042585306.png)

- 项目设置中修改自定义渲染深度通道

  - ![img](https://api2.mubu.com/v3/document_image/25165450_85102695-4deb-4269-aa30-b2c11968d6e7.png)

- 在敌人的类中修改 描边函数，为开启和关闭自定义渲染深度（若开启还需给定 自定义深度 的值）

  - ![img](https://api2.mubu.com/v3/document_image/25165450_c51a10b4-9016-4e6c-cbcb-82ba97399f57.png)

- 断开 敌人BP基类中 测试用的逻辑

  - ![img](https://api2.mubu.com/v3/document_image/25165450_4f5218cf-39b4-4004-ed9f-4856a29b0ebd.png)

- 测试结果

  - ![img](https://api2.mubu.com/v3/document_image/25165450_1c0f6af9-48a0-4676-9ab2-aca2d790512c.gif)

- Bug：此时武器还没描边，武器也需要，下面解决

- 之前的宏定义的不规范，需要在整体项目中 定义这个宏，同时将武器描边

  - ![img](https://api2.mubu.com/v3/document_image/25165450_6f9d9c02-8e26-4ee3-dccb-09589a97449f.png)

  - 敌人基类中需要引入这个项目的头文件![img](https://api2.mubu.com/v3/document_image/25165450_ebd95b3a-1c63-4e99-9b6f-5aaf5873231a.png)

- 完成 描边效果

  - 对比![img](https://api2.mubu.com/v3/document_image/25165450_350dc7ea-cb21-48b7-bef1-1c2c0a6cd05c.png)