___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 5.4 优化PC中的逻辑 运行时勿重复获取结果 精简代码 考虑可能出现的bug
- <font color=#DC2D1E>**处理关键点:**</font>
    - <font color=#DC2D1E>**1.优化逻辑步骤**</font>
        - <font color=#DC2D1E>**检查有无重复获取的结果，保存变量，节约运行时开销**</font>
        - <font color=#DC2D1E>**检查冗余代码，精简，抽象 逻辑**</font>
        - <font color=#DC2D1E>**考虑可能出现的情况和bug,  检查优化逻辑，并修复，参考《防御式编程》**</font>
        - <font color=#DC2D1E>**没问题后 去掉Debug和调试**</font>
    - <font color=#DC2D1E>**2.C++中的RPC**</font>
- 视频链接
    - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 [https://b23.tv/p193q3c]("https://b23.tv/p193q3c")
- 优化 AAuraPlayerController 中的逻辑
    - 目前有两处获取碰撞检测结果，保存变量，优化为一处获取，节约运行时开销
        - 自己找吧
            - 两处 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.4/GAS%205.4%20%E4%BC%98%E5%8C%96PC%E4%B8%AD%E7%9A%84%E9%80%BB%E8%BE%91%20%E8%BF%90%E8%A1%8C%E6%97%B6%E5%8B%BF%E9%87%8D%E5%A4%8D%E8%8E%B7%E5%8F%96%E7%BB%93%E6%9E%9C%20%E7%B2%BE%E7%AE%80%E4%BB%A3%E7%A0%81%20%E8%80%83%E8%99%91%E5%8F%AF%E8%83%BD%E5%87%BA%E7%8E%B0%E7%9A%84bug-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-734105-910533.png?raw=true)
    - 勾边逻辑部分，过于冗余，优化清晰逻辑
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.4/GAS%205.4%20%E4%BC%98%E5%8C%96PC%E4%B8%AD%E7%9A%84%E9%80%BB%E8%BE%91%20%E8%BF%90%E8%A1%8C%E6%97%B6%E5%8B%BF%E9%87%8D%E5%A4%8D%E8%8E%B7%E5%8F%96%E7%BB%93%E6%9E%9C%20%E7%B2%BE%E7%AE%80%E4%BB%A3%E7%A0%81%20%E8%80%83%E8%99%91%E5%8F%AF%E8%83%BD%E5%87%BA%E7%8E%B0%E7%9A%84bug-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-492041-878455.png?raw=true)
    - 此时有一个bug：客户端无法生成UI，之前处理的链接： ​ ​  ，原因为:ASC组件中的 <font color=#DC2D1E>**OnGameplayEffectAppliedDelegateToSelf委托**</font> 只能在Server上调用。处理方法:将回调改成RPC Client事件，这样自动在服务器调用，在客户端执行 [GAS 3.2 绑定GE委托，通过收到的的资产标签，广播信息结构体，触发UI中绑定的WidgetController回调，UI中拿到生成MessageUI的信息]("https://mubu.com/doc7RVlZQFR2M0")
        - **原因**
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.4/GAS%205.4%20%E4%BC%98%E5%8C%96PC%E4%B8%AD%E7%9A%84%E9%80%BB%E8%BE%91%20%E8%BF%90%E8%A1%8C%E6%97%B6%E5%8B%BF%E9%87%8D%E5%A4%8D%E8%8E%B7%E5%8F%96%E7%BB%93%E6%9E%9C%20%E7%B2%BE%E7%AE%80%E4%BB%A3%E7%A0%81%20%E8%80%83%E8%99%91%E5%8F%AF%E8%83%BD%E5%87%BA%E7%8E%B0%E7%9A%84bug-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-206525-325574.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.4/GAS%205.4%20%E4%BC%98%E5%8C%96PC%E4%B8%AD%E7%9A%84%E9%80%BB%E8%BE%91%20%E8%BF%90%E8%A1%8C%E6%97%B6%E5%8B%BF%E9%87%8D%E5%A4%8D%E8%8E%B7%E5%8F%96%E7%BB%93%E6%9E%9C%20%E7%B2%BE%E7%AE%80%E4%BB%A3%E7%A0%81%20%E8%80%83%E8%99%91%E5%8F%AF%E8%83%BD%E5%87%BA%E7%8E%B0%E7%9A%84bug-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-219709-853356.png?raw=true)
        - **回调改成RPC Client事件** 
        - ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.4/GAS%205.4%20%E4%BC%98%E5%8C%96PC%E4%B8%AD%E7%9A%84%E9%80%BB%E8%BE%91%20%E8%BF%90%E8%A1%8C%E6%97%B6%E5%8B%BF%E9%87%8D%E5%A4%8D%E8%8E%B7%E5%8F%96%E7%BB%93%E6%9E%9C%20%E7%B2%BE%E7%AE%80%E4%BB%A3%E7%A0%81%20%E8%80%83%E8%99%91%E5%8F%AF%E8%83%BD%E5%87%BA%E7%8E%B0%E7%9A%84bug-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-203696-312742.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.4/GAS%205.4%20%E4%BC%98%E5%8C%96PC%E4%B8%AD%E7%9A%84%E9%80%BB%E8%BE%91%20%E8%BF%90%E8%A1%8C%E6%97%B6%E5%8B%BF%E9%87%8D%E5%A4%8D%E8%8E%B7%E5%8F%96%E7%BB%93%E6%9E%9C%20%E7%B2%BE%E7%AE%80%E4%BB%A3%E7%A0%81%20%E8%80%83%E8%99%91%E5%8F%AF%E8%83%BD%E5%87%BA%E7%8E%B0%E7%9A%84bug-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-779336-466726.png?raw=true)
            -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.4/GAS%205.4%20%E4%BC%98%E5%8C%96PC%E4%B8%AD%E7%9A%84%E9%80%BB%E8%BE%91%20%E8%BF%90%E8%A1%8C%E6%97%B6%E5%8B%BF%E9%87%8D%E5%A4%8D%E8%8E%B7%E5%8F%96%E7%BB%93%E6%9E%9C%20%E7%B2%BE%E7%AE%80%E4%BB%A3%E7%A0%81%20%E8%80%83%E8%99%91%E5%8F%AF%E8%83%BD%E5%87%BA%E7%8E%B0%E7%9A%84bug-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-280720-194416.png?raw=true)
    - <font color=#DC2D1E>**没问题后 去掉Debug和调试**</font>
        -  ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_5.4/GAS%205.4%20%E4%BC%98%E5%8C%96PC%E4%B8%AD%E7%9A%84%E9%80%BB%E8%BE%91%20%E8%BF%90%E8%A1%8C%E6%97%B6%E5%8B%BF%E9%87%8D%E5%A4%8D%E8%8E%B7%E5%8F%96%E7%BB%93%E6%9E%9C%20%E7%B2%BE%E7%AE%80%E4%BB%A3%E7%A0%81%20%E8%80%83%E8%99%91%E5%8F%AF%E8%83%BD%E5%87%BA%E7%8E%B0%E7%9A%84bug-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-180159-706291.png?raw=true)
- **完成！此时客户端和服务器都会有拾取UI**

___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________