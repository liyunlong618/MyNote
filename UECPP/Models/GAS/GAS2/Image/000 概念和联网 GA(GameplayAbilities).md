# 000 概念和联网 GA(GameplayAbilities)
- **介绍**
    - **GameplayAbilities**
        - 使用的GA派生自UGameplayAbility
            -  ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-180255-78902.png)
        - 它定义了一个能力的作用以及可以使用该能力的条件。
        - 与使用简单函数执行操作不同，gas 游戏能力是一个异步运行的实例对
        - 这意味着它可以在某个时间点被激活，并运行可能跨越时间段的多阶段任务 ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-432377-224901.png)
        - 游戏能力具有内置的复制和预测支持，就像游戏效果一样 ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-811711-649994.png)
        - 游戏玩法能力还具有成本和冷却时间的内置概念属性资源必须以足够的数量存在以支付能力激活。
        - 在这门课程中，我们将使用法力作为资源来实现这种成本机制，但实际上可以是任何东西。 ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-316550-359461.png)
        -  ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-752306-437020.png)
        - **GameplayAbilities使用AbilityTask，尽管不一定需要**
    - **AbilityTask**
        - 使用的AbilityTask派生自UAbilityTask
            -  ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-857481-257854.png)
        - 这些在游戏能力执行期间执行异步工作。
        - 它们可以通过广播委托来影响执行流程。
        - 这些任务可以在C++中使用，但也可以以专门的蓝图节点的形式出现在蓝图中 ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-150252-700535.png)
        - 这些是根据开发人员确定的事件而进行的委托广播执行
        - 基本上，游戏中发生某事时，您的能力任务将广播一个委托。
        - 在蓝图中，这意味着任务节点上的特定输出执行引脚将被执行
        - 这使我们能够轻松地在蓝图中映射出一个能力的控制流程，同时仍然能够享受C++的最佳性能优势。
        - 由于任务所做的工作通常在C++端完成，尽管不一定非得如此。 ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-289145-241913.png)
        - 但是因为我们可以制作这些能力任务并让它们大部分工作在C++中，我们获得了灵活性，可以设计游戏能力的机制在能力的蓝图中，并允许那些无法访问C++领域的设计师更多地控制能力，而不会牺牲性能。
    - **联网！**
        - 要使用游戏能力，必须授予能力系统组件该能力
        - 当这种情况发生时，将创建一个游戏能力规范 **FGameplayAbilitySpec** ，该规范定义了与该特定能力相关的详细信息，包括游戏能力类本身、能力的级别以及可以在运行时更改的任何动态信息 ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-929126-220709.png)
        - 通常能力是在服务器上授予的，但当这种情况发生时，能力规范会复制到拥有客户端，以便他们可以从那里激活它。 ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-156058-241628.png)
        - **游戏能力** 具有 **激活** 的概念。一旦激活，能力被认为是处于活动状态， **直到** 它们被 **结束** 或 **取消** 。能力可以自行终止，也可以被外部取消。 ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-366758-680098.png)
        - 因此，简而言之，游戏能力是定义给定技能、法术或任何演员可以执行的能力的类。
        - 必须授予能力系统组件能力才能使用，我们在服务器上执行此操作，此时授予能力规范，并复制到拥有客户端。
        - 要使用一项能力，必须激活它。然后，它被视为处于活动状态，直到结束或取消。
        - 能力具有内置的成本和冷却概念
        - 能力可以异步运行，并且多个能力可以同时激活。
        - 能力可以运行能力任务，这些任务是将行为封装到各个类中的异步操作，每个类可以执行自己特定的工作。
        -  ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-753410-122850.png)
            -  ![图片](./000 概念和联网 GA(GameplayAbilities)-幕布图片-76019-853391.png)
- **也就是说，客户端调用TryActivateAbility函数后，会激活本地的ActivateAbility函数，同时后台发送RPC激活服务器端的RPC函数，假设服务器端检测通过为true，则会触发sendgameplayevent，然后对应的服务器端模拟的非主控端玩家的playerstate会接受到该tag，并在服务器上触发Wait Gameplay Event事件，生成开启replicated的actor，然后把结果同步给客户端？这样吗**
- 整个激活技能的流程
    - 完整流程总结
        - `**1.客户端调用TryActivateAbility**` ，本地检查并激活ActivateAbility（如果允许）。
        - **2.客户端发送RPC** 到服务器，调用ServerTryActivateAbility。
        - **3.服务器端检查条件** 并激活ActivateAbility。
        - `**4.服务器端触发Send Gameplay Event**` ，发送Gameplay Event Tag。
        - **5.服务器端捕捉到Gameplay Event** ，触发等待这个事件的Gameplay Ability。
        - **6.服务器端生成开启replicated的Actor** 。
        - **7.生成的Actor同步到所有客户端** 。
    - 关键点
        - **客户端和服务器同步** ：通过RPC和Gameplay Event机制，确保客户端和服务器端同步处理能力激活。
        - **服务器端主导** ：服务器端处理能力激活和生成Actor的逻辑，确保游戏状态一致。
        - **自动同步** ：开启replicated的Actor会自动同步到所有客户端，确保每个客户端都能看到相同的游戏状态。
        - 这个流程确保了能力激活和相关逻辑在客户端和服务器端的一致性，同时利用Gameplay Event和Replication机制保持游戏状态的同步。
    - 详细解释
        - 客户端调用 TryActivateAbility
        - `**1.客户端调用TryActivateAbility**` ：
            - 客户端调用 UAbilitySystemComponent::TryActivateAbility 函数。
            - 该函数会检查本地条件，如果可以在客户端本地激活（例如不需要服务器授权的能力），则会直接调用本地的 ActivateAbility 函数。
        - 后台发送RPC激活服务器端的 TryActivateAbility
        - `**2.RPC调用服务器端的ServerTryActivateAbility**` ：
            - 如果能力需要服务器端授权，客户端会发送一个RPC请求到服务器，调用 ServerTryActivateAbility 。
            - 服务器端收到这个RPC请求后，检查条件是否满足。
            - 如果服务器端条件满足，服务器端会调用 ActivateAbility 。
        - 服务器端处理
        - `**3.服务器端处理ActivateAbility**` ：
            - 在服务器端调用 ActivateAbility 函数。
            - 服务器端会进行一些必要的检查和初始化，然后执行能力的逻辑。
            - 这可能包括触发 Send Gameplay Event 来发送一个Gameplay Event Tag。
        - 处理Gameplay Event
        - **4.发送Gameplay Event** ：
            - 服务器端通过 Send Gameplay Event to Actor 发送一个Gameplay Event Tag。
            - 这个事件会在服务器端处理，并且可以在服务器端的非主控玩家的 PlayerState 中触发相应的事件。
        - 触发 Wait Gameplay Event
        - `**5.触发Wait Gameplay Event**` ：
            - 在服务器端，任何等待这个Gameplay Event Tag的 Gameplay Ability 会被激活。
            - Wait Gameplay Event 节点会捕捉到这个事件并继续执行相应的逻辑。
        - 生成Replicated的Actor
        - **6.生成Replicated的Actor** ：
            - 在服务器端处理 Wait Gameplay Event 的逻辑中，可能会生成一个开启replicated的Actor。
            - 这个Actor会在服务器端生成，并自动复制到所有客户端。
        - 同步到客户端
        - **7.同步到客户端** ：
            - 由于生成的Actor开启了replicated属性，服务器端生成的Actor会自动同步到所有客户端。
            - 客户端会接收到这个Actor的生成信息，并在本地创建相应的Actor副本。