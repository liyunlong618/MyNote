___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 3.3 拾取道具的小UI；HP和MP的滞后效果
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
  
    - <font color=#DC2D1E>**1.重写后处理函数PostGameplayEffectExecute，使用clamp限制**</font>
    
- 创建小UI 并 添加到屏幕
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-467859-735333.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-173053-807791.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-182466-385222.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-798384-646745.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-333787-583661.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-551622-875563.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-882976-176115.png?raw=true)
    - 加了一个 image 的IsVaild判断 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-693641-102197.png?raw=true)
    
- 创建小UI动画和设置销毁
    - ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-563304-829977.png?raw=true)
    
        gif
    
    - ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-239286-829790.gif?raw=true))
    
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-638566-686874.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-126400-127802.png?raw=true)
        
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-895122-300327.png?raw=true)
    
- 小测试：修改回调为Lambda表达式
    - 这些
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-176239-906839.png?raw=true)
    - 自己做一下
        - 头文件
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-542221-807520.png?raw=true)
        - 源文件
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-320357-593845.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-973140-103157.png?raw=true)
    
- UOverlayWidgetController 中新建一个总的属性多播，整理一下原来的多播种类
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-880172-305839.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-493672-129556.png?raw=true)
    
- 此时蓝图中出现报错
    - 基类中，修改变量类型 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-219391-468334.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-662203-147165.png?raw=true)
    - 子类HP中 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-675127-149809.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-586928-223458.png?raw=true)
    - 子类MP中 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-745992-118521.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-428986-565571.png?raw=true)
    
- 小测试：尝试制作 HP和MP的滞后效果 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-903809-875734.png?raw=true)
    - 自己尝试一下
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-68358-467300.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-231137-171233.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-653462-222332.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-807524-140717.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-330977-870845.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-894388-962006.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-357525-104251.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-747510-935390.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-561606-796078.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-196103-436756.png?raw=true)
    - tick打包成一个函数
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-257056-309009.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-60445-685590.png?raw=true)
    
- 有个小Bug，开始的时候，HP/MP也会有延迟的效果
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-371565-756472.png?raw=true)
    
- 此时效果gif

- ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-769563-447816.gif?raw=true)

- **此时有一个bug** ：当player拾取加血道具，使得血量远超过最大值时，正常应该是限制在了maxHP,也就是最大值，这时候，进入火堆，一段时间内不会掉血，此时断点查看属性
    - 也就是说加血会超出100，但只显示100
    - 发现只是显示时被夹在了0到MaxHP，实际上值还是在增加
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-751846-613810.png?raw=true)
    - 说明PreAttributeChange函数中修改的是只读参数，实际值并未发生改变。所以必须在PostGameplayEffectExecute函数(这个是处理后的函数)中进行Clamp和set属性
        - 在PostGameplayEffectExecute函数中进行Clamp和set属性 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-367399-347987.png?raw=true)
    
- 此时效果gif![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.3/GAS%203.3%20%E6%8B%BE%E5%8F%96%E9%81%93%E5%85%B7%E7%9A%84%E5%B0%8FUI%EF%BC%9BHP%E5%92%8CMP%E7%9A%84%E6%BB%9E%E5%90%8E%E6%95%88%E6%9E%9C-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-743511-941191.gif?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________