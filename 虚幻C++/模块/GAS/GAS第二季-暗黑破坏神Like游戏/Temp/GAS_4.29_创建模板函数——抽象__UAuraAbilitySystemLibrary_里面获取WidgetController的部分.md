___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 4.29 创建模板函数——抽象  UAuraAbilitySystemLibrary 里面获取WidgetController的部分
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
    - <font color=#DC2D1E>**1.模板函数的使用**</font>
    - <font color=#DC2D1E>**2.if constexpr 是一种条件编译语句，它允许在编译时进行条件检查，并且只有满足条件的分支代码会被编译。这与普通的 if 语句不同，普通的 if 语句是在运行时进行条件检查。示例：**</font>
        - <font color=#DC2D1E>`**if constexpr (std::is_same_v<T, UOverlayWidgetController>){Ptr = HUD->GetOverlayWidgetController(Params);}else if constexpr (std::is_same_v<T, UAttributeMenuWidgetController>){Ptr = HUD->GetAttributeMenuWidgetController(Params);}**`</font>
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.29/GAS%204.29%20%E5%88%9B%E5%BB%BA%E6%A8%A1%E6%9D%BF%E5%87%BD%E6%95%B0%E2%80%94%E2%80%94%E6%8A%BD%E8%B1%A1%20%20UAuraAbilitySystemLibrary%20%E9%87%8C%E9%9D%A2%E8%8E%B7%E5%8F%96WidgetController%E7%9A%84%E9%83%A8%E5%88%86-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-732700-202225.png?raw=true)
            - /*这部分代码使用了 C++17 引入的 if constexpr 语句和 std::is_same_v 类型特征来在编译时进行类型检查和选择性地编译代码分支。 *  * if constexpr 语句: * if constexpr 是一种条件编译语句，它允许在编译时进行条件检查，并且只有满足条件的分支代码会被编译。这与普通的 if 语句不同，普通的 if 语句是在运行时进行条件检查。 *  * std::is_same_v<T, UOverlayWidgetController>: * std::is_same_v 是 std::is_same 的简化形式，用于比较两个类型是否相同。 * std::is_same_v<T, UOverlayWidgetController> 在编译时会检查模板参数 T 是否等于 UOverlayWidgetController。如果相等，这个表达式的值为 true。 * * 通过使用 if constexpr 和 std::is_same_v，你可以在编译时根据模板参数类型选择性地编译不同的代码分支。 * 这在编写模板代码时非常有用，因为它允许你在编译时做出决定，从而避免了在运行时进行不必要的类型检查和分支判断，提高了代码的性能和类型安全性。 *  * 具体来说，在这个例子中: * 如果 T 是 UOverlayWidgetController，编译器会编译 Ptr = HUD->GetOverlayWidgetController(Params);，并忽略 else 分支。 * 如果 T 是 UAttributeMenuWidgetController，编译器会编译 Ptr = HUD->GetAttributeMenuWidgetController(Params);，并忽略 if 分支。 * 这种方式确保了模板函数在不同的类型参数下具有正确的行为。 */
- 蓝图函数库UAuraAbilitySystemLibrary中，使用if constexpr 语句
    - 头文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.29/GAS%204.29%20%E5%88%9B%E5%BB%BA%E6%A8%A1%E6%9D%BF%E5%87%BD%E6%95%B0%E2%80%94%E2%80%94%E6%8A%BD%E8%B1%A1%20%20UAuraAbilitySystemLibrary%20%E9%87%8C%E9%9D%A2%E8%8E%B7%E5%8F%96WidgetController%E7%9A%84%E9%83%A8%E5%88%86-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-719988-993402.png?raw=true)
            - /*这部分代码使用了 C++17 引入的 if constexpr 语句和 std::is_same_v 类型特征来在编译时进行类型检查和选择性地编译代码分支。 *  * if constexpr 语句: * if constexpr 是一种条件编译语句，它允许在编译时进行条件检查，并且只有满足条件的分支代码会被编译。这与普通的 if 语句不同，普通的 if 语句是在运行时进行条件检查。 *  * std::is_same_v<T, UOverlayWidgetController>: * std::is_same_v 是 std::is_same 的简化形式，用于比较两个类型是否相同。 * std::is_same_v<T, UOverlayWidgetController> 在编译时会检查模板参数 T 是否等于 UOverlayWidgetController。如果相等，这个表达式的值为 true。 * * 通过使用 if constexpr 和 std::is_same_v，你可以在编译时根据模板参数类型选择性地编译不同的代码分支。 * 这在编写模板代码时非常有用，因为它允许你在编译时做出决定，从而避免了在运行时进行不必要的类型检查和分支判断，提高了代码的性能和类型安全性。 *  * 具体来说，在这个例子中: * 如果 T 是 UOverlayWidgetController，编译器会编译 Ptr = HUD->GetOverlayWidgetController(Params);，并忽略 else 分支。 * 如果 T 是 UAttributeMenuWidgetController，编译器会编译 Ptr = HUD->GetAttributeMenuWidgetController(Params);，并忽略 if 分支。 * 这种方式确保了模板函数在不同的类型参数下具有正确的行为。 */
    - 源文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.29/GAS%204.29%20%E5%88%9B%E5%BB%BA%E6%A8%A1%E6%9D%BF%E5%87%BD%E6%95%B0%E2%80%94%E2%80%94%E6%8A%BD%E8%B1%A1%20%20UAuraAbilitySystemLibrary%20%E9%87%8C%E9%9D%A2%E8%8E%B7%E5%8F%96WidgetController%E7%9A%84%E9%83%A8%E5%88%86-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-122441-18049.png?raw=true)
- 错误示范！！！：HUD **AAuraHUD** 中这么干，无法判断空指针，每次都会实例化
    - 头文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.29/GAS%204.29%20%E5%88%9B%E5%BB%BA%E6%A8%A1%E6%9D%BF%E5%87%BD%E6%95%B0%E2%80%94%E2%80%94%E6%8A%BD%E8%B1%A1%20%20UAuraAbilitySystemLibrary%20%E9%87%8C%E9%9D%A2%E8%8E%B7%E5%8F%96WidgetController%E7%9A%84%E9%83%A8%E5%88%86-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-113702-587283.png?raw=true)
    - 源文件
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_4.29/GAS%204.29%20%E5%88%9B%E5%BB%BA%E6%A8%A1%E6%9D%BF%E5%87%BD%E6%95%B0%E2%80%94%E2%80%94%E6%8A%BD%E8%B1%A1%20%20UAuraAbilitySystemLibrary%20%E9%87%8C%E9%9D%A2%E8%8E%B7%E5%8F%96WidgetController%E7%9A%84%E9%83%A8%E5%88%86-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-845243-221712.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________