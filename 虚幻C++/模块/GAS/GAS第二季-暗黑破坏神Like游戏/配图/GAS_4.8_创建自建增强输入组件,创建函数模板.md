___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 4.8 创建自建增强输入组件，创建函数模板
- <font color=#DC2D1E>**处理关键点：**</font>
    - <font color=#DC2D1E>**1.使用C++模板，创建了一个函数模板**</font>
    - <font color=#DC2D1E>**2.具体参考《C++模板》**</font>
        - 本人：在微信收藏里；
        - 别人：找我要，这里放不了，我百度云会员到期了，不想充
- 视频链接：
    -  [https://www.bilibili.com/video/BV1JD421E7yC?p=99&vd_source=9e1e64122d802b4f7ab37bd325a89e6c]("https://www.bilibili.com/video/BV1JD421E7yC?p=99&vd_source=9e1e64122d802b4f7ab37bd325a89e6c")
- 自建增强输入组件类
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.8/GAS%204.8%20%E5%88%9B%E5%BB%BA%E8%87%AA%E5%BB%BA%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5%E7%BB%84%E4%BB%B6%EF%BC%8C%E5%88%9B%E5%BB%BA%E5%87%BD%E6%95%B0%E6%A8%A1%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-773783-319168.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.8/GAS%204.8%20%E5%88%9B%E5%BB%BA%E8%87%AA%E5%BB%BA%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5%E7%BB%84%E4%BB%B6%EF%BC%8C%E5%88%9B%E5%BB%BA%E5%87%BD%E6%95%B0%E6%A8%A1%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-84474-284024.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.8/GAS%204.8%20%E5%88%9B%E5%BB%BA%E8%87%AA%E5%BB%BA%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5%E7%BB%84%E4%BB%B6%EF%BC%8C%E5%88%9B%E5%BB%BA%E5%87%BD%E6%95%B0%E6%A8%A1%E6%9D%BF-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-315109-100922.png?raw=true)
        - 模板参数
            - UserClass : 用于指定用户类的类型。
            - PressedFuncType , ReleasedFuncType , HeldFuncType : 用于指定按下、释放和按住事件的函数类型。
        - 函数参数
            - InputConfig : 指向 UAuraInputConfig 类型的指针，包含输入配置。
            - Object : 指向用户类实例的指针。
            - PressedFunc , ReleasedFunc , HeldFunc : 指向相应事件处理函数的指针。
        - <font color=#DC2D1E>**创建了一个函数模板，typename是声明一个类型，和class类似，但是class是一个类**</font>
        - <font color=#DC2D1E>**bindAction是可变参数模板，理论上来说，最后一个传参数类型**</font>

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________