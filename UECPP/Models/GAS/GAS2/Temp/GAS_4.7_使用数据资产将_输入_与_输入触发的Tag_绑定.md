___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 4.7 使用数据资产将 输入 与 输入触发的Tag 绑定
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

- 视频链接：
    -  [4. Input Config Data Asset_哔哩哔哩_bilibili]("https://www.bilibili.com/video/BV1JD421E7yC?p=98&vd_source=9e1e64122d802b4f7ab37bd325a89e6c")
- 创建DataAsset资产
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-642769-247184.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-410923-196457.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-202904-219772.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-515680-316822.png?raw=true)
- FAuraGameplayTags中添加按键的Tag
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-945398-47968.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-701388-740906.png?raw=true)
- 此时运行项目 项目设置中查看GmeplayTag，若有标签说明操作没有问题
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-545045-24859.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-257128-598655.png?raw=true)
- 创建蓝图类数据资产继承自上面创建的c++类UAuraInputConfig取名DA_AuraInputConfig
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-99767-830475.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-274875-418315.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-694509-384866.png?raw=true)
- 创建对应的InputAction
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-912377-445925.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-198986-732893.png?raw=true)
- IMC_AuraContext中配置按键输入
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-750471-979129.png?raw=true)
- DA_AuraInputConfig中配置 FInputAction和FGameplaTag
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.7/GAS%204.7%20%E4%BD%BF%E7%94%A8%E6%95%B0%E6%8D%AE%E8%B5%84%E4%BA%A7%E5%B0%86%20%E8%BE%93%E5%85%A5%20%E4%B8%8E%20%E8%BE%93%E5%85%A5%E8%A7%A6%E5%8F%91%E7%9A%84Tag%20%E7%BB%91%E5%AE%9A-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-513286-200946.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________