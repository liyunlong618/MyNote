___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 5.5 创建抛射物类,蓝图继承并配置NS,替换地板
- <font color=#DC2D1E>**处理关键点:**</font>
    - <font color=#DC2D1E>**C++构造中设置碰撞通道和类型**</font>
    - <font color=#DC2D1E>**C++构造中设置抛射物组件参数**</font>
- 视频链接
    - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 [https://b23.tv/NcHDkEW]("https://b23.tv/NcHDkEW")
- 创建抛射物类，添加 **球形检测** ， **构造** 中设置 **碰撞检测通道** ；添加 **抛射物组件** ， **构造中** 设置： **速度/最大速度/受重力影响度** （这是一个归一化值，0为不受影响）
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.5/GAS%205.5%20%E5%88%9B%E5%BB%BA%E6%8A%9B%E5%B0%84%E7%89%A9%E7%B1%BB,%E8%93%9D%E5%9B%BE%E7%BB%A7%E6%89%BF%E5%B9%B6%E9%85%8D%E7%BD%AENS,%E6%9B%BF%E6%8D%A2%E5%9C%B0%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-240860-755504.png?raw=true-430439-516678.png?raw=true)
    - 头文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.5/GAS%205.5%20%E5%88%9B%E5%BB%BA%E6%8A%9B%E5%B0%84%E7%89%A9%E7%B1%BB,%E8%93%9D%E5%9B%BE%E7%BB%A7%E6%89%BF%E5%B9%B6%E9%85%8D%E7%BD%AENS,%E6%9B%BF%E6%8D%A2%E5%9C%B0%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-240860-755504.png?raw=true-778862-405905.png?raw=true)
    - 源文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.5/GAS%205.5%20%E5%88%9B%E5%BB%BA%E6%8A%9B%E5%B0%84%E7%89%A9%E7%B1%BB,%E8%93%9D%E5%9B%BE%E7%BB%A7%E6%89%BF%E5%B9%B6%E9%85%8D%E7%BD%AENS,%E6%9B%BF%E6%8D%A2%E5%9C%B0%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-240860-755504.png?raw=true-426364-671905.png?raw=true)
- 创建蓝图派生类，添加并配置NS
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.5/GAS%205.5%20%E5%88%9B%E5%BB%BA%E6%8A%9B%E5%B0%84%E7%89%A9%E7%B1%BB,%E8%93%9D%E5%9B%BE%E7%BB%A7%E6%89%BF%E5%B9%B6%E9%85%8D%E7%BD%AENS,%E6%9B%BF%E6%8D%A2%E5%9C%B0%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-240860-755504.png?raw=true-856165-167038.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.5/GAS%205.5%20%E5%88%9B%E5%BB%BA%E6%8A%9B%E5%B0%84%E7%89%A9%E7%B1%BB,%E8%93%9D%E5%9B%BE%E7%BB%A7%E6%89%BF%E5%B9%B6%E9%85%8D%E7%BD%AENS,%E6%9B%BF%E6%8D%A2%E5%9C%B0%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-240860-755504.png?raw=true-240860-755504.png?raw=true)
- 替换地板
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.5/GAS%205.5%20%E5%88%9B%E5%BB%BA%E6%8A%9B%E5%B0%84%E7%89%A9%E7%B1%BB,%E8%93%9D%E5%9B%BE%E7%BB%A7%E6%89%BF%E5%B9%B6%E9%85%8D%E7%BD%AENS,%E6%9B%BF%E6%8D%A2%E5%9C%B0%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-240860-755504.png?raw=true-616945-199950.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________