___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 5.0 GA中配置Tag，并在按下和松开按键时的回调函数中设置，保证释放GA时，触发并持有该Tag
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
    - <font color=#DC2D1E>**1.赋予角色技能时，给 技能GA 添加 动态标签DynamicAbilityTag**</font>
    - <font color=#DC2D1E>**2.调用 ASC组件中的API: GetActivatableAbilities()可以拿到所以可以激活的GA的Spec**</font>
    - <font color=#DC2D1E>**3. GA的Spec 中 有一个动态技能标签 DynamicAbilityTags 若技能激活时 会拥有该 Tag**</font>
    - <font color=#DC2D1E>**4.调用 ASC组件中的API: AbilitySpecInputPressed(AbilitySpec);会 标记技能的输入状态为已按下**</font>
    - <font color=#DC2D1E>**5.使用 ASC组件中的API: TryActivateAbility(AbilitySpec.Handle);尝试激活该技能 若激活技能 会把 AbilitySpec 标记为已激活 IsActive**</font>
    - <font color=#DC2D1E>**6.**</font> <font color=#DC2D1E>`**if (AbilitySpec.IsActive())**`</font> <font color=#DC2D1E>**判断该技能GA是否被激活**</font>
    - <font color=#DC2D1E>**7.使用AbilitySpec.Handle 激活该技能TryActivateAbility(AbilitySpec.Handle);**</font>
- 视频链接：
    -  [6. Callbacks for Ability Input_哔哩哔哩_bilibili]("https://www.bilibili.com/video/BV1JD421E7yC?p=100&vd_source=9e1e64122d802b4f7ab37bd325a89e6c")
- UAuraGameplayAbility 中，内部持有 `**GameplayTag**` 变量
    - 内部持有GameplayTag变量 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.0/GAS%205.0%20GA%E4%B8%AD%E9%85%8D%E7%BD%AETag%EF%BC%8C%E5%B9%B6%E5%9C%A8%E6%8C%89%E4%B8%8B%E5%92%8C%E6%9D%BE%E5%BC%80%E6%8C%89%E9%94%AE%E6%97%B6%E7%9A%84%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%B8%AD%E8%AE%BE%E7%BD%AE%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%87%8A%E6%94%BEGA%E6%97%B6%EF%BC%8C%E8%A7%A6%E5%8F%91%E5%B9%B6%E6%8C%81%E6%9C%89%E8%AF%A5Tag-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-121074-517762.png?raw=true)
- UAuraAbilitySystemComponent 中，赋予角色技能时，给 技能GA 添加 动态标签DynamicAbilityTag，创建两个松开后的回调函数，传入tag
    - 在赋予角色技能时，可以给 技能GA 添加 动态标签DynamicAbilityTag ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.0/GAS%205.0%20GA%E4%B8%AD%E9%85%8D%E7%BD%AETag%EF%BC%8C%E5%B9%B6%E5%9C%A8%E6%8C%89%E4%B8%8B%E5%92%8C%E6%9D%BE%E5%BC%80%E6%8C%89%E9%94%AE%E6%97%B6%E7%9A%84%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%B8%AD%E8%AE%BE%E7%BD%AE%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%87%8A%E6%94%BEGA%E6%97%B6%EF%BC%8C%E8%A7%A6%E5%8F%91%E5%B9%B6%E6%8C%81%E6%9C%89%E8%AF%A5Tag-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-427853-834671.png?raw=true)
    - 创建两个松开后的回调函数，传入tag ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.0/GAS%205.0%20GA%E4%B8%AD%E9%85%8D%E7%BD%AETag%EF%BC%8C%E5%B9%B6%E5%9C%A8%E6%8C%89%E4%B8%8B%E5%92%8C%E6%9D%BE%E5%BC%80%E6%8C%89%E9%94%AE%E6%97%B6%E7%9A%84%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%B8%AD%E8%AE%BE%E7%BD%AE%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%87%8A%E6%94%BEGA%E6%97%B6%EF%BC%8C%E8%A7%A6%E5%8F%91%E5%B9%B6%E6%8C%81%E6%9C%89%E8%AF%A5Tag-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-178833-734865.png?raw=true)
- AAuraPlayerController 中
    - 持有asc组件和创建内部获取的方法 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.0/GAS%205.0%20GA%E4%B8%AD%E9%85%8D%E7%BD%AETag%EF%BC%8C%E5%B9%B6%E5%9C%A8%E6%8C%89%E4%B8%8B%E5%92%8C%E6%9D%BE%E5%BC%80%E6%8C%89%E9%94%AE%E6%97%B6%E7%9A%84%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%B8%AD%E8%AE%BE%E7%BD%AE%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%87%8A%E6%94%BEGA%E6%97%B6%EF%BC%8C%E8%A7%A6%E5%8F%91%E5%B9%B6%E6%8C%81%E6%9C%89%E8%AF%A5Tag-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-810568-769206.png?raw=true)
        - **get** ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.0/GAS%205.0%20GA%E4%B8%AD%E9%85%8D%E7%BD%AETag%EF%BC%8C%E5%B9%B6%E5%9C%A8%E6%8C%89%E4%B8%8B%E5%92%8C%E6%9D%BE%E5%BC%80%E6%8C%89%E9%94%AE%E6%97%B6%E7%9A%84%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%B8%AD%E8%AE%BE%E7%BD%AE%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%87%8A%E6%94%BEGA%E6%97%B6%EF%BC%8C%E8%A7%A6%E5%8F%91%E5%B9%B6%E6%8C%81%E6%9C%89%E8%AF%A5Tag-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-375492-734600.png?raw=true)
    - 开始按下和松开的回调函数中调用ASC组件中创建的开始按下和松开的回调函数 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.0/GAS%205.0%20GA%E4%B8%AD%E9%85%8D%E7%BD%AETag%EF%BC%8C%E5%B9%B6%E5%9C%A8%E6%8C%89%E4%B8%8B%E5%92%8C%E6%9D%BE%E5%BC%80%E6%8C%89%E9%94%AE%E6%97%B6%E7%9A%84%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%B8%AD%E8%AE%BE%E7%BD%AE%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%87%8A%E6%94%BEGA%E6%97%B6%EF%BC%8C%E8%A7%A6%E5%8F%91%E5%B9%B6%E6%8C%81%E6%9C%89%E8%AF%A5Tag-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-529970-651798.png?raw=true)
- UAuraAbilitySystemComponent 中
    - 参考
        - 基类ASC组件中的参考（这里是对于 默认没有实例化的GA的操作） ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.0/GAS%205.0%20GA%E4%B8%AD%E9%85%8D%E7%BD%AETag%EF%BC%8C%E5%B9%B6%E5%9C%A8%E6%8C%89%E4%B8%8B%E5%92%8C%E6%9D%BE%E5%BC%80%E6%8C%89%E9%94%AE%E6%97%B6%E7%9A%84%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%B8%AD%E8%AE%BE%E7%BD%AE%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%87%8A%E6%94%BEGA%E6%97%B6%EF%BC%8C%E8%A7%A6%E5%8F%91%E5%B9%B6%E6%8C%81%E6%9C%89%E8%AF%A5Tag-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-375713-800460.png?raw=true)
        - 基类GA中的参考，虚函数可以重写 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.0/GAS%205.0%20GA%E4%B8%AD%E9%85%8D%E7%BD%AETag%EF%BC%8C%E5%B9%B6%E5%9C%A8%E6%8C%89%E4%B8%8B%E5%92%8C%E6%9D%BE%E5%BC%80%E6%8C%89%E9%94%AE%E6%97%B6%E7%9A%84%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%B8%AD%E8%AE%BE%E7%BD%AE%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%87%8A%E6%94%BEGA%E6%97%B6%EF%BC%8C%E8%A7%A6%E5%8F%91%E5%B9%B6%E6%8C%81%E6%9C%89%E8%AF%A5Tag-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-659059-266506.png?raw=true)
    - <font color=#DC2D1E>**下面是关键步骤**</font>
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.0/GAS%205.0%20GA%E4%B8%AD%E9%85%8D%E7%BD%AETag%EF%BC%8C%E5%B9%B6%E5%9C%A8%E6%8C%89%E4%B8%8B%E5%92%8C%E6%9D%BE%E5%BC%80%E6%8C%89%E9%94%AE%E6%97%B6%E7%9A%84%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%B8%AD%E8%AE%BE%E7%BD%AE%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%87%8A%E6%94%BEGA%E6%97%B6%EF%BC%8C%E8%A7%A6%E5%8F%91%E5%B9%B6%E6%8C%81%E6%9C%89%E8%AF%A5Tag-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-822520-105846.png?raw=true)
- ***GA*** 中配置tag
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.0/GAS%205.0%20GA%E4%B8%AD%E9%85%8D%E7%BD%AETag%EF%BC%8C%E5%B9%B6%E5%9C%A8%E6%8C%89%E4%B8%8B%E5%92%8C%E6%9D%BE%E5%BC%80%E6%8C%89%E9%94%AE%E6%97%B6%E7%9A%84%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%B8%AD%E8%AE%BE%E7%BD%AE%EF%BC%8C%E4%BF%9D%E8%AF%81%E9%87%8A%E6%94%BEGA%E6%97%B6%EF%BC%8C%E8%A7%A6%E5%8F%91%E5%B9%B6%E6%8C%81%E6%9C%89%E8%AF%A5Tag-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-165062-732171.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________