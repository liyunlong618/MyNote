___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 5.6 创建新的C++类继承自UAuraGameplayAbility重写ActivateAbility虚函数打印测试
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

- 视频链接
    - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 [https://b23.tv/XvDjaI1]("https://b23.tv/XvDjaI1")
- 创建新的C++类继承自 UAuraGameplayAbility
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.6/GAS%205.6%20%E5%88%9B%E5%BB%BA%E6%96%B0%E7%9A%84C++%E7%B1%BB%E7%BB%A7%E6%89%BF%E8%87%AAUAuraGameplayAbility%E9%87%8D%E5%86%99ActivateAbility%E8%99%9A%E5%87%BD%E6%95%B0%E6%89%93%E5%8D%B0%E6%B5%8B%E8%AF%95-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-514965-783.png?raw=true)
- UAuraProjectileSpell 中，重写基类中 <font color=#FFAF38>**ActivateAbility**</font> 这个虚函数
    - 头文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.6/GAS%205.6%20%E5%88%9B%E5%BB%BA%E6%96%B0%E7%9A%84C++%E7%B1%BB%E7%BB%A7%E6%89%BF%E8%87%AAUAuraGameplayAbility%E9%87%8D%E5%86%99ActivateAbility%E8%99%9A%E5%87%BD%E6%95%B0%E6%89%93%E5%8D%B0%E6%B5%8B%E8%AF%95-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-75614-580836.png?raw=true)
    - 源文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.6/GAS%205.6%20%E5%88%9B%E5%BB%BA%E6%96%B0%E7%9A%84C++%E7%B1%BB%E7%BB%A7%E6%89%BF%E8%87%AAUAuraGameplayAbility%E9%87%8D%E5%86%99ActivateAbility%E8%99%9A%E5%87%BD%E6%95%B0%E6%89%93%E5%8D%B0%E6%B5%8B%E8%AF%95-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-343261-406875.png?raw=true)
- 创建UAuraProjectileSpell的蓝图派生类 <font color=#40A8F5>***GA_FireBolt***</font>
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.6/GAS%205.6%20%E5%88%9B%E5%BB%BA%E6%96%B0%E7%9A%84C++%E7%B1%BB%E7%BB%A7%E6%89%BF%E8%87%AAUAuraGameplayAbility%E9%87%8D%E5%86%99ActivateAbility%E8%99%9A%E5%87%BD%E6%95%B0%E6%89%93%E5%8D%B0%E6%B5%8B%E8%AF%95-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-936274-277420.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.6/GAS%205.6%20%E5%88%9B%E5%BB%BA%E6%96%B0%E7%9A%84C++%E7%B1%BB%E7%BB%A7%E6%89%BF%E8%87%AAUAuraGameplayAbility%E9%87%8D%E5%86%99ActivateAbility%E8%99%9A%E5%87%BD%E6%95%B0%E6%89%93%E5%8D%B0%E6%B5%8B%E8%AF%95-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-372015-236754.png?raw=true)
- 在角色 <font color=#40A8F5>***BP_Aura***</font> 中配置，才能生效
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.6/GAS%205.6%20%E5%88%9B%E5%BB%BA%E6%96%B0%E7%9A%84C++%E7%B1%BB%E7%BB%A7%E6%89%BF%E8%87%AAUAuraGameplayAbility%E9%87%8D%E5%86%99ActivateAbility%E8%99%9A%E5%87%BD%E6%95%B0%E6%89%93%E5%8D%B0%E6%B5%8B%E8%AF%95-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-979458-823078.png?raw=true)
- 此时测试结果， <font color=#DC2D1E>**蓝图先打印，C++后打印**</font> ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.6/GAS%205.6%20%E5%88%9B%E5%BB%BA%E6%96%B0%E7%9A%84C++%E7%B1%BB%E7%BB%A7%E6%89%BF%E8%87%AAUAuraGameplayAbility%E9%87%8D%E5%86%99ActivateAbility%E8%99%9A%E5%87%BD%E6%95%B0%E6%89%93%E5%8D%B0%E6%B5%8B%E8%AF%95-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-227932-894669.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________