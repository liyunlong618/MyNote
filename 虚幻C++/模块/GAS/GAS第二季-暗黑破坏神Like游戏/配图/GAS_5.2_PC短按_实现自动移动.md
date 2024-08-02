___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 5.2 PC短按 实现自动移动
- 视频链接
    -  [https://www.bilibili.com/video/BV1JD421E7yC?p=104&vd_source=9e1e64122d802b4f7ab37bd325a89e6c]("https://www.bilibili.com/video/BV1JD421E7yC?p=104&vd_source=9e1e64122d802b4f7ab37bd325a89e6c")
- 使用 **NaviMesh** 的 **API** 需要 **引模块** **"** <font color=#DC2D1E>**NavigationSystem**</font> **"**
    - 需要引模块" <font color=#DC2D1E>**NavigationSystem**</font> " ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.2/GAS%205.2%20PC%E7%9F%AD%E6%8C%89%20%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%8A%A8%E7%A7%BB%E5%8A%A8-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-113058-475192.png?raw=true)
- AAuraPlayerController 中
    - <font color=#FFAF38>**AbilityInputTagReleased**</font> **函数中,**
        - 如果不为左键点击tag，调用ASC组件的回调函数，然后return；若为左键点击时，if有目标，调用ASC组件的回调函数；没目标，这里才是需要处理的逻辑：
        - 先拿到控制的角色，若点击时间小于等于 阈值 且 控制角色不为空时，先清空样条线的所有点，通过 <font color=#75C940>**NaviMesh**</font> 的API： <font color=#FFAF38>**UNavigationSystemV1::FindPathToLocationSynchronously**</font> 拿到 <font color=#75C940>**NaviMesh**</font> 的导航路径，路径结构体中有个 <font color=#75C940>**PathPoints**</font> 数组保存了路径点的信息，遍历一下为样条线添加点，生成debug球体，然后 `bAutoRunning=true` ；然后设置记录鼠标点击时间的变量为0.f，设置 `bTargeting=false`
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.2/GAS%205.2%20PC%E7%9F%AD%E6%8C%89%20%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%8A%A8%E7%A7%BB%E5%8A%A8-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-637612-886080.png?raw=true)
            - 需要引模块" <font color=#DC2D1E>**NavigationSystem**</font> " ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.2/GAS%205.2%20PC%E7%9F%AD%E6%8C%89%20%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%8A%A8%E7%A7%BB%E5%8A%A8-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-711087-988406.png?raw=true)
- 小技巧：当你不知道一个函数的模块时，可以谷歌
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.2/GAS%205.2%20PC%E7%9F%AD%E6%8C%89%20%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%8A%A8%E7%A7%BB%E5%8A%A8-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-679958-782482.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.2/GAS%205.2%20PC%E7%9F%AD%E6%8C%89%20%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%8A%A8%E7%A7%BB%E5%8A%A8-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-259772-140573.png?raw=true)
    - 会定位到官方文档，哈哈哈，所以还是需要在文档里面找 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.2/GAS%205.2%20PC%E7%9F%AD%E6%8C%89%20%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%8A%A8%E7%A7%BB%E5%8A%A8-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-193824-382242.png?raw=true)
- 加入导航网格体 <font color=#DC2D1E>**Nav Mesh Bounds Volume**</font>
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.2/GAS%205.2%20PC%E7%9F%AD%E6%8C%89%20%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%8A%A8%E7%A7%BB%E5%8A%A8-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-273431-263758.png?raw=true)
- 我使用的是右键移动，此时短按右键，会Debug导航点

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________