___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 5.1 PC实现点击移动-参考官方 俯视角游戏模板
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
    - <font color=#DC2D1E>**1.了解官方俯视角游戏DS/LS框架下的问题**</font>
    - <font color=#DC2D1E>**2.梳理点击移动的逻辑**</font>
- 视频链接
    - 原理解析: [https://www.bilibili.com/video/BV1JD421E7yC?p=102&vd_source=9e1e64122d802b4f7ab37bd325a89e6c]("https://www.bilibili.com/video/BV1JD421E7yC?p=102&vd_source=9e1e64122d802b4f7ab37bd325a89e6c")
    - 课程链接: [https://www.bilibili.com/video/BV1JD421E7yC?p=103&vd_source=9e1e64122d802b4f7ab37bd325a89e6c]("https://www.bilibili.com/video/BV1JD421E7yC?p=103&vd_source=9e1e64122d802b4f7ab37bd325a89e6c")
- AAuraPlayerController中
    - 头文件中创建几个变量
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.1/GAS%205.1%20PC%E5%AE%9E%E7%8E%B0%E7%82%B9%E5%87%BB%E7%A7%BB%E5%8A%A8-%E5%8F%82%E8%80%83%E5%AE%98%E6%96%B9%20%E4%BF%AF%E8%A7%86%E8%A7%92%E6%B8%B8%E6%88%8F%E6%A8%A1%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-198225-532153.png?raw=true)
        - `**FVector：CachedDestination目标地点**`
        - `**float：ShortPressThreshold鼠标 短按/长按 区分的时间阈值**`
        - `**float：FollowTime鼠标 短按/长按 记录时间**`
        - `**bool：bAutoRunning是否可以自动奔跑**`
        - `**bool：bTargeting是否有目标（敌人）**`
        - `**float：AutoRunAcceptanceRadius与目的地的距离**`
        - `**组件：Spline样条线组件**`
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.1/GAS%205.1%20PC%E5%AE%9E%E7%8E%B0%E7%82%B9%E5%87%BB%E7%A7%BB%E5%8A%A8-%E5%8F%82%E8%80%83%E5%AE%98%E6%96%B9%20%E4%BF%AF%E8%A7%86%E8%A7%92%E6%B8%B8%E6%88%8F%E6%A8%A1%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-389897-312219.png?raw=true)
        - 配置默认值 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.1/GAS%205.1%20PC%E5%AE%9E%E7%8E%B0%E7%82%B9%E5%87%BB%E7%A7%BB%E5%8A%A8-%E5%8F%82%E8%80%83%E5%AE%98%E6%96%B9%20%E4%BF%AF%E8%A7%86%E8%A7%92%E6%B8%B8%E6%88%8F%E6%A8%A1%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-206031-286271.png?raw=true)
    - 源文件中
        - 构造中 创建样条线组件
        - 鼠标按下时， <font color=#FFAF38>**AbilityInputTagPressed**</font> 函数中，若传进来的tag是LMB的Tag（说明短按下左键），如果 `ThisActor == nullptr` ， `bTargeting=false` ； `ThisActor != nullptr` ， `bTargeting=true` ；此时不是长按的触发时机，所以 `bAutoRunning = false` ；
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.1/GAS%205.1%20PC%E5%AE%9E%E7%8E%B0%E7%82%B9%E5%87%BB%E7%A7%BB%E5%8A%A8-%E5%8F%82%E8%80%83%E5%AE%98%E6%96%B9%20%E4%BF%AF%E8%A7%86%E8%A7%92%E6%B8%B8%E6%88%8F%E6%A8%A1%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-298057-721158.png?raw=true)
                - 之前在勾边时，创建过一个ThisActor指针（指向当前鼠标正在指向的Actor）若该目标没有实现接口，就是nullptr
        - 鼠标长按时， <font color=#FFAF38>**AbilityInputTagHeld**</font> 函数中，如果传进来的tag不是LMB的Tag（说明不是长按的左键），此时执行检查ASC组件，调用ASC组件中的回调函数（旧逻辑）然后返回；下面是按左键的逻辑，若 `bTargeting == true` 说明左键点击了敌人，此时执行检查ASC组件，调用ASC组件中的回调函数（旧逻辑）然后返回；else说明左键没有点击敌人即 `bTargeting == false` 此处处理的才是长按点击移动的逻辑： `FollowTime+=DeltaTime` 发射一条射线，如果击中物体, `CachedDestination目标地点 = 击中点` ，如果能拿到控制的角色，先计算 <font color=#75C940>**Dir**</font> ，然后 <font color=#FFAF38>**AddMovementInput**</font>
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.1/GAS%205.1%20PC%E5%AE%9E%E7%8E%B0%E7%82%B9%E5%87%BB%E7%A7%BB%E5%8A%A8-%E5%8F%82%E8%80%83%E5%AE%98%E6%96%B9%20%E4%BF%AF%E8%A7%86%E8%A7%92%E6%B8%B8%E6%88%8F%E6%A8%A1%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-359080-13488.png?raw=true)
                - 想要达到，短按左键，自动跑 = true
- 此时效果gif ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.1/GAS%205.1%20PC%E5%AE%9E%E7%8E%B0%E7%82%B9%E5%87%BB%E7%A7%BB%E5%8A%A8-%E5%8F%82%E8%80%83%E5%AE%98%E6%96%B9%20%E4%BF%AF%E8%A7%86%E8%A7%92%E6%B8%B8%E6%88%8F%E6%A8%A1%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-291019-98446.gif?raw=true)
- 

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________