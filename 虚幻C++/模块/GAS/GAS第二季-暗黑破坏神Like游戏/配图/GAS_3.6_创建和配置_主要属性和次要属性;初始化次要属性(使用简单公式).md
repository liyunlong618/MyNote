___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 3.6 创建和配置 主要属性和次要属性；初始化次要属性(使用简单公式)
- 创建主要属性和次要属性，并打开属性复制
    - 头文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-354941-332773.png?raw=true)
    - 源文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-867210-489404.png?raw=true)
- 初始化次要属性
    - AAuraCharacterBase 中添加蓝图可配置GE类变量，重构初始化函数，抽象功能
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-751305-49722.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-684318-272959.png?raw=true)
    - AAuraCharacterBase 中 `InitAbilityActorInfo()` 函数中调用初始化函数
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-498248-537295.png?raw=true)
    - UAuraAttributeSet 的构造中移除多余的属性
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-602699-495173.png?raw=true)
    - AbilitySystem/GameplayEffects下的PrimaryAttributes **文件夹改名** 成 **DefaultAttributes**
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-994695-688957.png?raw=true)
    - AbilitySystem/GameplayEffects/DefaultAttributes下 **创建GE**
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-772353-819462.png?raw=true)
    - 给 **BP_Aura** 配置 次要属性GE
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-628836-702026.png?raw=true)
    - 设置次要属性GE
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-905761-566664.png?raw=true)
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-300828-919720.png?raw=true)
- Up的计算公式
    - **护甲（Armor）：**
        - 属性 = Coefficient * (Resilience + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-46187-410826.png?raw=true)
    - **护甲穿透（Armor Penetration）：**
        - 属性 = Coefficient * (Resilience + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-685417-764324.png?raw=true)
    - **格挡几率（Block Chance）：**
        - 属性 = Coefficient * (Armor + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-400264-32343.png?raw=true)
    - **暴击几率（Critical Hit Chance）：**
        - 属性 = Coefficient * (Resilience + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-410179-1296.png?raw=true)
    - **暴击伤害（Critical Hit Damage）：**
        - 属性 = Coefficient * (Armor Penetration + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-945351-683502.png?raw=true)
    - **暴击抗性（Critical Hit Resistance）：**
        - 属性 = Coefficient * (Armor + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-241590-660499.png?raw=true)
    - **生命值再生（Health Regeneration）：**
        - 属性 = Coefficient * (Vigor + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-779061-818513.png?raw=true)
    - **法力值再生（Mana Regeneration）：**
        - 属性 = Coefficient * (Intelligence + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-125962-384640.png?raw=true)
    - **最大生命值（Max Health）：**
        - 属性 =Coefficient * (Vigor + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-982467-217346.png?raw=true)
    - **最大法力值（Max Mana）：**
        - 属性 = Coefficient * (Intelligence + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-752983-440131.png?raw=true)
- 运行游戏 此时可以看到设置好的数值 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.6/GAS%203.6%20%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%EF%BC%9B%E5%88%9D%E5%A7%8B%E5%8C%96%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7(%E4%BD%BF%E7%94%A8%E7%AE%80%E5%8D%95%E5%85%AC%E5%BC%8F)-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-705193-513961.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________