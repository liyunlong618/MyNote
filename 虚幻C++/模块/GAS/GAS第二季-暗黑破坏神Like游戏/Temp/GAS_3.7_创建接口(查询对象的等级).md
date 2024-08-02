___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 3.7 创建接口(查询对象的等级)
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
    - <font color=#DC2D1E>**1.属性同步 配置**</font>
    - <font color=#DC2D1E>**2.UE inline宏 FORCEINLINE**</font>
- 创建接口(查询对象的等级)写一个获取等级的虚函数
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-282703-251983.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-998498-662625.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-816160-521354.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-544376-522385.png?raw=true)
- AAuraCharacterBase 继承接口并实现接口虚函数
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-38424-760594.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-524657-671400.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-782363-8768.png?raw=true)
- 敌人 AAuraEnemy 中重写接口虚函数，并创建等级变量
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-952889-281213.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-135846-199363.png?raw=true)
- 玩家的PS AAuraPlayerState 中创建等级变量，并开启属性同步，配置相应函数创建一个public：获取等级的函数
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-487759-131990.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-707960-178620.png?raw=true)
- 角色 AAuraCharacter 中重写接口虚函数
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-358198-563925.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.7/GAS%203.7%20%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3(%E6%9F%A5%E8%AF%A2%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%AD%89%E7%BA%A7)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-236741-833839.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________