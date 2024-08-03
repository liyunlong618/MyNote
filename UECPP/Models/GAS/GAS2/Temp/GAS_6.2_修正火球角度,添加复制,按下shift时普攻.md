___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 6.2 修正火球角度，添加复制，按下shift时普攻
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
    - <font color=#DC2D1E>**1.使用：**</font> <font color=#DC2D1E>`**向量.Rotation();**`</font> <font color=#DC2D1E>**获取角度FRotator**</font>
    - <font color=#DC2D1E>**2.使用：**</font> <font color=#DC2D1E>`**角度.Quaternion();**`</font> <font color=#DC2D1E>**获取该角度的四元数**</font>
    - <font color=#DC2D1E>**3.C++中设置 碰撞通道**</font>
    - <font color=#DC2D1E>**4.**</font> <font color=#DC2D1E>**DS**</font> <font color=#DC2D1E>**/**</font> <font color=#DC2D1E>**LS网络复制相关**</font>
- 视频链接
    - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 [https://b23.tv/IGADhLV]("https://b23.tv/IGADhLV")
- 生成抛射物的函数 <font color=#FFAF38>**SpawnProjectile**</font> 中，
    - 头文件，添加形参，传入位置
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-961957-992405.png?raw=true)
    - 源文件，计算方向，设置Rotation
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-490988-422038.png?raw=true)
- GA蓝图 ***GA_FireBolt*** 中，获取HitResult后保存 <font color=#75C940>**Location**</font> ，传参
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-38746-241064.png?raw=true)
- 此时有个问题，一个角色会把另一个角色弹簧臂挡住，需要C++中设置一下角色capsule和mesh的碰撞通道，对camera为忽略
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-524165-147260.jpeg) ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-90885-151804.jpeg)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-930303-727834.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-487670-288832.png?raw=true) ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-240330-303387.png?raw=true)
- 此时希望添加一个功能，按下shift时，不用点到敌人，也可以发射普通攻击火球
    - **步骤**
        - 1.添加InputAction,并设置为1d输入
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-465808-918237.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-269944-514892.png?raw=true)
        - 2.配置InputAction
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-806636-765333.png?raw=true)
        - 3. AAuraPlayerController 中
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-194644-212719.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-200742-288778.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-354795-15479.png?raw=true) ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-434919-253064.png?raw=true)
        - ***BP_AuraPlayerController*** 中配置
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-741910-348769.png?raw=true)
- 记得火球 AAuraProjectile 中开启复制bReplicates，否则客户端无法看见
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-497501-850138.png?raw=true)
- 此时效果gif ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_6.2/GAS%206.2%20%E4%BF%AE%E6%AD%A3%E7%81%AB%E7%90%83%E8%A7%92%E5%BA%A6%EF%BC%8C%E6%B7%BB%E5%8A%A0%E5%A4%8D%E5%88%B6%EF%BC%8C%E6%8C%89%E4%B8%8Bshift%E6%97%B6%E6%99%AE%E6%94%BB-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-431364-932439.gif?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________