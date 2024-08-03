___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 4.2 创建蓝图函数库
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

- <font color=#DC2D1E>**处理关键点：UFUNCTION(BlueprintPure,Category="AuraAbilitySystemLibrary|WidgetController",meta=(WorldContext="WorldContextObject"))**</font>
    - <font color=#DC2D1E>**1.UFUNCTION(BlueprintPure)表示该函数可以在蓝图中被调用并且是一个纯函数。**</font>
    - <font color=#DC2D1E>**2.若形参中 有const UObject* WorldContextObject这个作为世界上下文，上面的宏UFUNCTION(meta=(WorldContext="WorldContextObject"))，可以自动识别函数的世界上下文**</font>
    - <font color=#DC2D1E>**3.拿数据：PS从PC拿，ASC和AS从PS拿（因为在PS中创建）**</font>
- 创建蓝图函数库 UAuraAbilitySystemLibrary
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-577386-387501.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-135225-59931.png?raw=true)
    - BlueprintPure表示该函数可以在蓝图中被调用并且是一个纯函数。 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-800750-847072.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-271010-698749.png?raw=true)
- 小测试：蓝图函数库中创建一个获取UAttributeMenuWidgetController的全局静态函数(HUD中也要创建获取的函数) ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-289417-487002.png?raw=true)
    - 自己试一下
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-787070-394238.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-592694-236280.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-407600-186471.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-375327-530500.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-127919-50697.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-841037-4783.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-800020-449492.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-577562-822938.png?raw=true)
        - 测试 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.2/GAS%204.2%20%E5%88%9B%E5%BB%BA%E8%93%9D%E5%9B%BE%E5%87%BD%E6%95%B0%E5%BA%93-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-963221-22014.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________