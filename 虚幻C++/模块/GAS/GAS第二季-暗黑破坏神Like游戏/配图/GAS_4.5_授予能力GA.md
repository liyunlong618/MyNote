___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 4.5 授予能力GA
- <font color=#DC2D1E>**处理关键点**</font>
    - <font color=#DC2D1E>**1.只有服务器才能赋予技能**</font>
    - <font color=#DC2D1E>**2.学习技能时，先使用GA的Class创建FGameplayabilitySpec技能规范**</font>
        - <font color=#DC2D1E>**然后调用API:GiveAbilityAndActivateOnce(这里传入技能规范)才能学习**</font>
- 创建GA文件
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-816207-659845.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-964889-58254.png?raw=true)
- AAuraCharacterBase 中创建 存放 技能GA类的数组，并创建需要学习技能时调用的函数 `AddCharacterAbilities()`
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-622868-138872.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-479469-965246.png?raw=true)
- UAuraAbilitySystemComponent 中，创建 调用时 传入要学的GA类 **数组** （ **const引用** ）函数，并学习技能
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-112254-233365.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-978582-586363.png?raw=true)
- AAuraCharacter 中，当角色PossessedBy时，调用基类中的学习技能的函数 `AddCharacterAbilities()`
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-668086-400015.png?raw=true)
- 创建GA文件夹，并创建 测试用GA类继承自UAuraGameplayAbility
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-558686-802729.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-960664-574075.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-805801-892780.png?raw=true)
- 使用测试的GA 测试
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-552141-562667.png?raw=true)
    -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-177369-109541.png?raw=true)
    - 测试结果 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.5/GAS%204.5%20%E6%8E%88%E4%BA%88%E8%83%BD%E5%8A%9BGA-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-906951-983114.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________