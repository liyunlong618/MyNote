___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 4.9 AAuraPlayerController中为自建增强输入组件创建并绑定按键回调，引擎中配置增强输入
- <font color=#DC2D1E>**处理关键点：**</font>
    - <font color=#DC2D1E>**1.引擎中配置增强输入：项目设置->输入->默认输入组件类**</font>
- 视频链接：
    -  [6. Callbacks for Ability Input_哔哩哔哩_bilibili]("https://www.bilibili.com/video/BV1JD421E7yC?p=100&vd_source=9e1e64122d802b4f7ab37bd325a89e6c")
- **AAuraPlayerController** 中，添加了：1.输入与Tag绑定用 蓝图配置 数据资产2.按键触发的三个回调，分别对应：开始按下/持续按下/松开
    - 头文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.9/GAS%204.9%20AAuraPlayerController%E4%B8%AD%E4%B8%BA%E8%87%AA%E5%BB%BA%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5%E7%BB%84%E4%BB%B6%E5%88%9B%E5%BB%BA%E5%B9%B6%E7%BB%91%E5%AE%9A%E6%8C%89%E9%94%AE%E5%9B%9E%E8%B0%83%EF%BC%8C%E5%BC%95%E6%93%8E%E4%B8%AD%E9%85%8D%E7%BD%AE%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-534434-883396.png?raw=true)
    - 源文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.9/GAS%204.9%20AAuraPlayerController%E4%B8%AD%E4%B8%BA%E8%87%AA%E5%BB%BA%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5%E7%BB%84%E4%BB%B6%E5%88%9B%E5%BB%BA%E5%B9%B6%E7%BB%91%E5%AE%9A%E6%8C%89%E9%94%AE%E5%9B%9E%E8%B0%83%EF%BC%8C%E5%BC%95%E6%93%8E%E4%B8%AD%E9%85%8D%E7%BD%AE%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-553399-972094.png?raw=true)
            - 具体修改 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.9/GAS%204.9%20AAuraPlayerController%E4%B8%AD%E4%B8%BA%E8%87%AA%E5%BB%BA%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5%E7%BB%84%E4%BB%B6%E5%88%9B%E5%BB%BA%E5%B9%B6%E7%BB%91%E5%AE%9A%E6%8C%89%E9%94%AE%E5%9B%9E%E8%B0%83%EF%BC%8C%E5%BC%95%E6%93%8E%E4%B8%AD%E9%85%8D%E7%BD%AE%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-956779-668163.png?raw=true)
- 生效需要配置
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.9/GAS%204.9%20AAuraPlayerController%E4%B8%AD%E4%B8%BA%E8%87%AA%E5%BB%BA%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5%E7%BB%84%E4%BB%B6%E5%88%9B%E5%BB%BA%E5%B9%B6%E7%BB%91%E5%AE%9A%E6%8C%89%E9%94%AE%E5%9B%9E%E8%B0%83%EF%BC%8C%E5%BC%95%E6%93%8E%E4%B8%AD%E9%85%8D%E7%BD%AE%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-344566-941554.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.9/GAS%204.9%20AAuraPlayerController%E4%B8%AD%E4%B8%BA%E8%87%AA%E5%BB%BA%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5%E7%BB%84%E4%BB%B6%E5%88%9B%E5%BB%BA%E5%B9%B6%E7%BB%91%E5%AE%9A%E6%8C%89%E9%94%AE%E5%9B%9E%E8%B0%83%EF%BC%8C%E5%BC%95%E6%93%8E%E4%B8%AD%E9%85%8D%E7%BD%AE%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-507444-237172.png?raw=true)
- 此时效果gif ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.9/GAS%204.9%20AAuraPlayerController%E4%B8%AD%E4%B8%BA%E8%87%AA%E5%BB%BA%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5%E7%BB%84%E4%BB%B6%E5%88%9B%E5%BB%BA%E5%B9%B6%E7%BB%91%E5%AE%9A%E6%8C%89%E9%94%AE%E5%9B%9E%E8%B0%83%EF%BC%8C%E5%BC%95%E6%93%8E%E4%B8%AD%E9%85%8D%E7%BD%AE%E5%A2%9E%E5%BC%BA%E8%BE%93%E5%85%A5-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-99466-992348.gif?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________