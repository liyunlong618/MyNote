___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 4.4 概念和联网 GA(GameplayAbilities)
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

- **介绍**
    - **GameplayAbilities**
        - 使用的GA派生自UGameplayAbility
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-539161-23139.png?raw=true)
        - 它定义了一个能力的作用以及可以使用该能力的条件。
        - 与使用简单函数执行操作不同，gas 游戏能力是一个异步运行的实例对
        - 这意味着它可以在某个时间点被激活，并运行可能跨越时间段的多阶段任务 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-161364-528138.png?raw=true)
        - 游戏能力具有内置的复制和预测支持，就像游戏效果一样 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-115591-411973.png?raw=true)
        - 游戏玩法能力还具有成本和冷却时间的内置概念属性资源必须以足够的数量存在以支付能力激活。
        - 在这门课程中，我们将使用法力作为资源来实现这种成本机制，但实际上可以是任何东西。 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-177024-116542.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-88229-677269.png?raw=true)
        - **GameplayAbilities使用AbilityTask，尽管不一定需要**
    - **AbilityTask**
        - 使用的AbilityTask派生自UAbilityTask
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-318393-451467.png?raw=true)
        - 这些在游戏能力执行期间执行异步工作。
        - 它们可以通过广播委托来影响执行流程。
        - 这些任务可以在C++中使用，但也可以以专门的蓝图节点的形式出现在蓝图中 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-399233-723203.png?raw=true)
        - 这些是根据开发人员确定的事件而进行的委托广播执行
        - 基本上，游戏中发生某事时，您的能力任务将广播一个委托。
        - 在蓝图中，这意味着任务节点上的特定输出执行引脚将被执行
        - 这使我们能够轻松地在蓝图中映射出一个能力的控制流程，同时仍然能够享受C++的最佳性能优势。
        - 由于任务所做的工作通常在C++端完成，尽管不一定非得如此。 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-130939-978088.png?raw=true)
        - 但是因为我们可以制作这些能力任务并让它们大部分工作在C++中，我们获得了灵活性，可以设计游戏能力的机制在能力的蓝图中，并允许那些无法访问C++领域的设计师更多地控制能力，而不会牺牲性能。
    - **联网！**
        - 要使用游戏能力，必须授予能力系统组件该能力
        - 当这种情况发生时，将创建一个游戏能力规范 **FGameplayAbilitySpec** ，该规范定义了与该特定能力相关的详细信息，包括游戏能力类本身、能力的级别以及可以在运行时更改的任何动态信息 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-626992-233060.png?raw=true)
        - 通常能力是在服务器上授予的，但当这种情况发生时，能力规范会复制到拥有客户端，以便他们可以从那里激活它。 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-825149-94465.png?raw=true)
        - **游戏能力** 具有 **激活** 的概念。一旦激活，能力被认为是处于活动状态， **直到** 它们被 **结束** 或 **取消** 。能力可以自行终止，也可以被外部取消。 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-254510-341009.png?raw=true)
        - 因此，简而言之，游戏能力是定义给定技能、法术或任何演员可以执行的能力的类。
        - 必须授予能力系统组件能力才能使用，我们在服务器上执行此操作，此时授予能力规范，并复制到拥有客户端。
        - 要使用一项能力，必须激活它。然后，它被视为处于活动状态，直到结束或取消。
        - 能力具有内置的成本和冷却概念
        - 能力可以异步运行，并且多个能力可以同时激活。
        - 能力可以运行能力任务，这些任务是将行为封装到各个类中的异步操作，每个类可以执行自己特定的工作。
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-196943-12435.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.4/GAS%204.4%20%E6%A6%82%E5%BF%B5%E5%92%8C%E8%81%94%E7%BD%91%20GA(GameplayAbilities)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-776900-362082.png?raw=true)
- **也就是说，我如果客户端调用TryActivateAbility函数后会激活本地的ActivateAbility函数，同时后台发送rpc激活服务器端的rpc函数，假设服务器端检测通过为true，则会触发sendgameplayevent，然后对应的服务器端模拟的非主控端玩家的playerstate会接受到该tag，并在服务器上触发Wait Gameplay Event事件，生成开启replicated的actor，然后把结果同步给客户端？这样吗**

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________