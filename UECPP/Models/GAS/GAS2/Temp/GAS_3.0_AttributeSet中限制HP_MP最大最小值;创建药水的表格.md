___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 3.0 AttributeSet中限制HP/MP最大最小值；创建药水的表格
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
    - <font color=#DC2D1E>**1.**</font> **AuraAttributeSet** <font color=#DC2D1E>**中重写虚函数**</font> <font color=#DC2D1E>`**PreAttributeChange**`</font> <font color=#DC2D1E>**(属性更改前 预处理)限制属性最大最小值**</font>
    - <font color=#DC2D1E>**2.了解属性更改后处理虚函数**</font> <font color=#DC2D1E>`**PostGameplayEffectExecute**`</font>
    - <font color=#DC2D1E>**3.实参**</font> <font color=#DC2D1E>`**Data**`</font> <font color=#DC2D1E>**，几乎能拿到所有信息，拿信息**</font>
    - <font color=#DC2D1E>**4.给GE数值配表**</font>
- 修改属性 两种方法
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-284403-302695.png?raw=true)
    - **属性更改前 预处理**
        - 在 UAuraAttributeSet 中重写虚函数 `**PreAttributeChange**` **(属性更改前 预处理)** 限制属性最大最小值
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-474346-319493.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-863112-645119.png?raw=true)
    - **属性更改后触发(这里只做了解用，这一步不写逻辑)**
        - 在 UAuraAttributeSet 中重写虚函数 `**PostGameplayEffectExecute**` **(属性更改后触发)** 限制属性最大最小值
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-741502-140490.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-211693-116915.png?raw=true)
        - **这个函数的参数Data非常强大，几乎能拿到所有信息**
- **新建一个函数和结构体** ， **保存** 属性更改后，从PostGameplayEffectExecute函数的参数 **Data** 获得的，有用的 **信息**
    - 头文件
        - 创建结构体
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-445639-730038.png?raw=true)
        - 创建函数
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-133213-37722.png?raw=true)
    - 源文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-197308-395917.png?raw=true)
- 创建药水的表格
    - 创建药水的表格
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-675532-693538.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-951247-679919.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-898439-988052.png?raw=true)
    - 配置表格
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-848706-669579.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-525573-392949.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-48716-3372.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-40835-41843.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-108094-130640.png?raw=true)
    - 测试一下，此时拾取药水，恢复5HP，说明配置表格成功
    - 为 AAuraEffectActor 添加 物品等级(影响应用效果)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-214283-244082.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-105198-89587.png?raw=true)
    - **此物品等级可以为float！！！比如4.75** ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-252261-893626.png?raw=true)
    - 蓝图中测试修改物品等级
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-574359-584545.png?raw=true)
    - 测试效果
        - 说明成功了 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-201473-847215.png?raw=true) ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-636771-229774.png?raw=true) ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-286932-916063.png?raw=true)
        - 测试完，记得改回来
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-244522-360828.png?raw=true)
    - 修改曲线表格名字为 **CT_Potion，** 打算把所有药水的数据都存在这个表格上
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-916719-135802.png?raw=true)
    - 增加魔法药水的曲线
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-326861-868984.png?raw=true)
    - 为魔法药水配置 曲线表格
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-127554-921527.png?raw=true)
    - 测试一下
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.0/GAS%203.0%20AttributeSet%E4%B8%AD%E9%99%90%E5%88%B6HP_MP%E6%9C%80%E5%A4%A7%E6%9C%80%E5%B0%8F%E5%80%BC%EF%BC%9B%E5%88%9B%E5%BB%BA%E8%8D%AF%E6%B0%B4%E7%9A%84%E8%A1%A8%E6%A0%BC-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-625234-335073.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________