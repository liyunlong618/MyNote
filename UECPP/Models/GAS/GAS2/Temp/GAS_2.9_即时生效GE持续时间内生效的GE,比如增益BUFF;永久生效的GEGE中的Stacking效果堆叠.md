___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 2.9 即时生效GE/持续时间内生效的GE(比如增益BUFF)/永久生效的GE/GE中的Stacking(效果堆叠)
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
- <font color=#DC2D1E>**处理关键点：**</font>
    - <font color=#DC2D1E>**1.此函数使用 UAbilitySystemBlueprintLibrary 函数库中的API (检查目标是否实现了IAbilitySystemInterface 接口/若未实现 返回nullptr)**</font>
    - <font color=#DC2D1E>**UAbilitySystemComponent* TargetASC = UAbilitySystemBlueprintLibrary::GetAbilitySystemComponent(TargetActor);**</font>
    - <font color=#DC2D1E>**2.道具类使用GE:**</font>
        -  <font color=#DC2D1E>**//步骤一：ASC中的API创建一个 FGameplayEffectcontextHandle（游戏效果上下文句柄）**</font>
        -  <font color=#DC2D1E>**//步骤二：为上下文添加Source**</font>
        -  <font color=#DC2D1E>**//步骤三： ASC中的API创建一个 FGameplayEffectSpecHandle 类型的（GE句柄）**</font>
        -  <font color=#DC2D1E>**//步骤四：ASC中的API使用GE句柄应用GE到Target或Self**</font>
    - <font color=#DC2D1E>**3.GE三种类型 一次性/持续（临时）/永久  的配置**</font>
    - <font color=#DC2D1E>**4.StackingType堆叠效果（此处是指增益堆叠）**</font>
    - <font color=#DC2D1E>**5.移除 GE 效果（返回时需要记录FActiveGameplayEffectHandle类变量）**</font>
    - <font color=#DC2D1E>**6.GE的Stacking(此处是指减益堆叠)**</font>
    - <font color=#DC2D1E>**7.数组中移除单个数据**</font>
- **优化原来的血瓶逻辑** —— AAuraEffectActor 中 **移除** (Mesh/SphereCollision/OnOverlap和碰撞通知绑定)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-91561-760897.png?raw=true)
    - 移除不用的 头文件 和 前项声明
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-534069-565843.png?raw=true)
    - 删除后
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-933996-582370.png?raw=true)
- BP_AuraEffectActor中创建StaticMesh组件和SphereCollision组件，并配置资产，调整缩放
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-870981-403956.png?raw=true)
- 了解用： ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-648354-745590.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-553564-848927.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-144635-366635.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-387235-671973.png?raw=true)
- 规范化文件夹
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-224981-684525.png?raw=true)
- **一次性生效GE**
    - 在AAuraEffectActor中，创建一个蓝图中设置的 **一次性生效GE** 类；再(如果被检测到的目标实现了IAbilitySystemInterface接口，就为他) **创建一个GE，并触发**
        - 头文件
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-812786-32177.png?raw=true)
        - 源文件
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-811469-729385.png?raw=true)
        - 蓝图中的参考
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-104241-677105.png?raw=true)
    - 创建HP药水的GE
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-706811-606433.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-567337-810171.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-872786-214518.png?raw=true)
    - 修改 AAuraEffectActor 中的InstantGameplayEffectClass为蓝图可读变量
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-9576-967655.png?raw=true)
    - BP_HealthPotion中SphereCollision触发BeginOverlap事件时添加调用逻辑
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-344189-524968.png?raw=true)
    - 因为BeginOverlap时触发的目标Target和原来的重名，所以需要修改C++类的Target为TargetActor
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-396484-279134.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-470228-233160.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-6342-779410.png?raw=true)
    - 小测试：制作MP药水
        - 自己尝试一下
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-512925-690192.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-97481-924266.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-365261-847433.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-180569-904824.png?raw=true)
- **持续时间内生效的GE**
    - 添加 持续治疗的道具(水晶)
        - 创建蓝图类继承自AAuraEffectActor
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-641825-222732.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-53782-665927.png?raw=true)
        - 创建并配置 持续时间内生效的 GE
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-885195-988828.png?raw=true)
    - 在 AAuraEffectActor 上 **增加持续时间内生效的GE(比如增益BUFF)变量**
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-740956-798407.png?raw=true)
    - 小测试：制作水晶
        - 自己尝试一下
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-147408-332414.png?raw=true)
        - 水晶效果gif ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-832477-870919.gif?raw=true)
    - 水晶使用了CapsuleCollision
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-965332-727931.png?raw=true)
    - **修改水晶的GE** 为持续时间内每隔 0.1 秒+ 1 HP
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-873659-434770.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-448090-504617.png?raw=true)
    - 拾取 水晶效果gif
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-521081-535452.gif?raw=true)
    - 小测试：制作持续回复法力的水晶
        - 自己尝试一下
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-620058-149865.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-316377-86306.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-924746-407180.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-305430-376287.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-889326-275234.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-895834-520611.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-999563-371050.png?raw=true)
    - GE中的Stacking(效果堆叠) ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-531361-954837.png?raw=true)
        - **StackingType**
            - **Stacking有三种：**
            - **None**
                - 不效果堆叠
            - **Aggregate by Target**
                -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-102327-219831.png?raw=true)
                - 意思是当设置了StackLimitCount为2时(此参数为生效对象上限)
                - **记录的是——每个生效的Target目标(此时为Player的ASC) 同时生效的同一效果最大为2**
                - 说人话就是：这个是每个 **人** 的生效上限为StackLimitCount
            - **Aggregate by Source**
                -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-758281-485034.png?raw=true)
                - 意思是当设置了StackLimitCount为2时(此参数为生效对象上限)
                - **记录的是——每个生效的Source来源(此时为水晶) 同时生效的同一效果 对同一Target 最大为2**
                - 说人话就是：这个是每件道具的 **GE类** 的生效上限为StackLimitCount
            - **举例帮助理解：此时StackLimitCount为2，对3个水晶应用此GE，人走过去一次捡起(此时结果相同，但过程不同)** ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-642219-223619.png?raw=true)
                - 当设置为： **Aggregate by Target** 时，因为每个Target(Player)只能生效2次，所以触发两次拾取水晶的效果
                    - gif ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-109841-354905.gif?raw=true)
                - 当设置为： **Aggregate by Source** 时，因为每个Source(同时间应用的GE类)只能生效2次，所以触发两次拾取水晶的效果
                    - gif ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-939102-199809.gif?raw=true)
        - **StackDurationRefreshPolicy堆栈持续时间刷新策略**
            - **StackDurationRefreshPolicy有两种：**
            - **RefreshOnSuccessfulApplication** 申请成功后刷新
            - **NeverRefresh** 永不刷新
            - **举例帮助理解：此时StackLimitCount为2，对3个水晶应用此GE，GE效果为每0.1秒生效一次，持续时间为2秒,如图所示，摆放水晶。操控Player先拾取一块水晶，当1.5秒后，拾取第二块水晶** ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-440799-285676.png?raw=true)
                - 当设置为： **RefreshOnSuccessfilApplication** 时，计算结果为： **15** (拾取第一块的加血量) **40** (拾取第二块时增长速度翻一番，且刷新第一块的持续时间) **= 55**
                    - gif ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-461659-413233.gif?raw=true)
                - 当设置为： **NeverRefresh** 时，计算结果为： **15** (拾取第一块的加血量) **10** (第一块的持续时间还剩5秒，此时间不刷新，所以第二块只生效5秒所以5+5=10) **= 25**
                    - gif ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-387077-387909.gif?raw=true)
    - 修改：生命水晶和魔法水晶的GE
        - 生命水晶GE
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-620795-929119.png?raw=true)
        - 魔法水晶GE
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-38863-937418.png?raw=true)
- **永久生效的GE**
    - 在 AAuraEffectActor 上 **永久生效的GE** 变量
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-92345-708470.png?raw=true)
    - 创建文件夹 **Crystal** (水晶) 把 相关文件 挪到这里
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-721501-308529.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-831864-354442.png?raw=true)
    - 创建文件夹 **Area** (区域)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-239774-604686.png?raw=true)
    - 创建BP继承自AuraEffectActor
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-576540-506448.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-441172-891492.png?raw=true)
    - 为 BP 添加 **BoxCollision组件** 和 **Niagara组件** 并改名，配置Niagara资产
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-265343-212746.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-3639-955321.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-140243-425431.png?raw=true)
    - 创建GE
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-463512-174608.png?raw=true)
    - 为BP_FireArea配置GE和重叠时触发的逻辑
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-167372-630457.png?raw=true)
    - BP_FireArea拖入场景
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-472669-439641.png?raw=true)
    - 此时触发逻辑后，会一直掉血 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-903675-717306.png?raw=true)
    - **移除** 永久生效的 **GE**  **效果** ，需要修改一下 AAuraEffectActor 中的逻辑
        - 头文件
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-67106-915467.png?raw=true)
        - 源文件
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-494991-703893.png?raw=true)
    - 设置 **BP_FireArea** 的枚举类型和开始/结束重叠调用事件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-189723-837057.png?raw=true)
    - 设置 **GE** 的Stacking(效果堆叠)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-5333-781240.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-549206-958434.png?raw=true)
        - 效果是，这个火焰掉血效果可以叠加，上限为3 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-432609-263540.png?raw=true)
    - **BUG：** 此时有个 **bug** 就是，当人物进入第三层掉血区域后，再进入第二层掉血区域，就不掉血了，原因是，离开单个区域会把所有的此类的Handle清除
        - 因为这个函数，后面的 **StacksToRemove** 为-1 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-155393-965126.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-150373-667830.png?raw=true)
        - **处理此Bug**
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-127884-738800.png?raw=true)
    - 调节一下 **BP_FireArea** 外观
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-979479-182292.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.9/GE%E4%B8%AD%E7%9A%84Stacking(%E6%95%88%E6%9E%9C%E5%A0%86%E5%8F%A0)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-85665-639207.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________