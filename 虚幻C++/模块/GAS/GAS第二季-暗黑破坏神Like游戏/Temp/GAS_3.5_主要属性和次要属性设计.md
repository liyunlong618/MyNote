___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 3.5 主要属性和次要属性设计
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

-  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-771246-365218.png?raw=true)
-  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-284682-364358.png?raw=true)
- **Primary Attributes** 主要属性
    - **Strength** 力量
    - **Intelligence** 智力
    - **Resilience** 坚韧
    - **Vigor** 活力
- **Secondary Attributes** 次要属性
    - Armor - 护甲
        - Reduces damage taken, improves Block Chance - 减少受到的伤害，提高格挡几率
        - 受到什么属性影响
            - **Resilience** 坚韧
    - Armor Penetration - 护甲穿透
        - Ignores percentage of enemy Armor, increases Crit Hit Chance - 忽略敌方护甲的百分比，增加暴击几率
        - 受到什么属性影响
            - **Resilience** 坚韧
    - Block Chance - 格挡几率
        - Chance to cut incoming damage in half - 减少受到的伤害一半的几率
        - 受到什么属性影响
            - Armor - 护甲
    - Critical Hit Chance - 暴击几率
        - Chance to double damage plus critical hit bonus - 几率使伤害加倍并获得暴击加成
        - 受到什么属性影响
            - Armor Penetration - 护甲穿透
    - Critical Hit Damage - 暴击伤害
        - Bonus damage added when a critical hit is scored - 当暴击命中时增加的额外伤害
        - 受到什么属性影响
            - Armor Penetration - 护甲穿透
    - Critical Hit Resistance - 暴击抗性
        - Reduces critical hit chance of attacking enemies - 减少攻击敌人的暴击几率
        - 受到什么属性影响
            - Armor - 护甲
    - Health Regeneration - 生命值再生
        - Amount of Health regenerated every 1 second - 每秒回复的生命值数量
        - 受到什么属性影响
            - **Vigor** 活力
    - Mana Regeneration - 法力值再生
        - Amount of Mana regenerated every 1 second - 每秒回复的法力值数量
        - 受到什么属性影响
            - **Intelligence** 智力
    - Max Health - 最大生命值
        - Maximum amount of Health obtainable - 可获得的最大生命值数量
        - 受到什么属性影响
            - **Vigor** 活力
    - Max Mana - 最大法力值
        - Maximum amount of Mana obtainable - 可获得的最大法力值数量
        - 受到什么属性影响
            - **Intelligence** 智力
- 我的属性计算公式
    - 根据属性之间的关系，我们可以调整每个属性的Coefficient、Pre和Post值，使它们更符合游戏中的逻辑和平衡性：
    - **护甲（Armor）：**
        - 属性 = Coefficient * (Resilience + Pre) + Post
        - 设计：假设 Coefficient = 0.6，Pre = 1，Post = 5。这样设计可以使护甲的基础值比坚韧属性的值稍高，再加上一个常数来确保起始护甲值不太低。
    - **护甲穿透（Armor Penetration）：**
        - 属性 = Coefficient * (Resilience + Pre) + Post
        - 设计：假设 Coefficient = 0.7，Pre = 0.5，Post = 0。这样设计可以使护甲穿透的基础值比坚韧属性的值稍低，再加上一个常数来确保起始护甲穿透值不太低。
    - **格挡几率（Block Chance）：**
        - 属性 = Coefficient * (Armor + Pre) + Post
        - 设计：假设 Coefficient = 0.1，Pre = 0.2，Post = 5。这样设计可以使格挡几率的基础值不太高，再加上一个常数来确保起始格挡几率不太低。
    - **暴击几率（Critical Hit Chance）：**
        - 属性 = Coefficient * (Resilience + Pre) + Post
        - 设计：假设 Coefficient = 0.05，Pre = 0.3，Post = 3。这样设计可以使暴击几率的基础值不太高，再加上一个常数来确保起始暴击几率不太低。
    - **暴击伤害（Critical Hit Damage）：**
        - 属性 = Coefficient * (Armor Penetration + Pre) + Post
        - 设计：假设 Coefficient = 0.1，Pre = 0.1，Post = 8。这样设计可以使暴击伤害的基础值不太高，再加上一个常数来确保起始暴击伤害不太低。
    - **暴击抗性（Critical Hit Resistance）：**
        - 属性 = Coefficient * (Armor + Pre) + Post
        - 设计：假设 Coefficient = 0.2，Pre = 0.3，Post = 5。这样设计可以使暴击抗性的基础值比护甲和活力的值稍高，再加上一个常数来确保起始暴击抗性值不太低。
    - **生命值再生（Health Regeneration）：**
        - 属性 = Coefficient * (Vigor + Pre) + Post
        - 设计：假设Coefficient = 1.8，Pre = 0.2，Post = 0。这样设计可以使生命值再生的基础值适中，再加上一个常数来确保起始生命值再生不太低。
    - **法力值再生（Mana Regeneration）：**
        - 属性 = Coefficient * (Intelligence + Pre) + Post
        - 设计：假设 Coefficient = 1.5，Pre = 0.1，Post = 0。这样设计可以使法力值再生的基础值适中，再加上一个常数来确保起始法力值再生不太低。
    - **最大生命值（Max Health）：**
        - 属性 =Coefficient * (Vigor + Pre) + Post
        - 设计：假设 Coefficient = 18，Pre = 0.4，c_max_health = 0。这样设计可以使最大生命值的基础值适中，再加上一个常数来确保起始最大生命值不太低。
    - **最大法力值（Max Mana）：**
        - 属性 = Coefficient * (Intelligence + Pre) + Post
        - 设计：假设 Coefficient = 14，Pre = 0.3，c_max_mana = 0。这样设计可以使最大法力值的基础值适中，再加上一个常数来确保起始最大法力值不太低。
    - 以上的设计基于了角色属性之间的关系，以及属性的基础值，再加上一个常数来确保起始属性值不太低。你可以根据具体需求和平衡性进行微调。
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-21544-581181.png?raw=true)
- Up的计算公式
    - **护甲（Armor）：**
        - 属性 = Coefficient * (Resilience + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-771711-194159.png?raw=true)
    - **护甲穿透（Armor Penetration）：**
        - 属性 = Coefficient * (Resilience + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-73731-624595.png?raw=true)
    - **格挡几率（Block Chance）：**
        - 属性 = Coefficient * (Armor + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-862407-660069.png?raw=true)
    - **暴击几率（Critical Hit Chance）：**
        - 属性 = Coefficient * (Resilience + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-412314-930062.png?raw=true)
    - **暴击伤害（Critical Hit Damage）：**
        - 属性 = Coefficient * (Armor Penetration + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-880041-681742.png?raw=true)
    - **暴击抗性（Critical Hit Resistance）：**
        - 属性 = Coefficient * (Armor + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-180087-825114.png?raw=true)
    - **生命值再生（Health Regeneration）：**
        - 属性 = Coefficient * (Vigor + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-678454-352653.png?raw=true)
    - **法力值再生（Mana Regeneration）：**
        - 属性 = Coefficient * (Intelligence + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-212471-454158.png?raw=true)
    - **最大生命值（Max Health）：**
        - 属性 =Coefficient * (Vigor + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-30664-468223.png?raw=true)
    - **最大法力值（Max Mana）：**
        - 属性 = Coefficient * (Intelligence + Pre) + Post
        - Coefficient = 0.25，Pre = 2，Post = 6
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_3.5/GAS%203.5%20%E4%B8%BB%E8%A6%81%E5%B1%9E%E6%80%A7%E5%92%8C%E6%AC%A1%E8%A6%81%E5%B1%9E%E6%80%A7%E8%AE%BE%E8%AE%A1-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-652751-307887.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________