___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)

___________________________________________________________________________________________

# GAS 2.8 配置多播

___________________________________________________________________________________________

> UOverlayWidgetController中创建动态多播；此时当ASC组件调用->获取游戏属性值更改的委托（GetGameplayAttributeValueChangeDelegate）,然后绑定回调,回调时广播到UI中,这样就完成了发布更新的架构
___________________________________________________________________________________________

## 处理关键点
1. 动态单播,在c++中声明,蓝图中绑定回调

```CPP
AbilitySystemComponent->GetGameplayAttributeValueChangeDelegate(
    AuraAttributeSet->GetHealthAttribute()).AddUObject(this,&UOverlayWidgetController::HealthChanged);
```

2. ASC组件 调用 获取属性变化委托,传入特定类型属性,且 回调函数形参 必须为const FOnAttributeChangeData类型

```CPP
void HealthChanged(const FOnAttributeChangeData& Data);
```

___________________________________________________________________________________________

- [GAS 2.8 配置多播](#gas-28-配置多播)
	- [处理关键点](#处理关键点)
		- [UAuraWidgetController中写一个多播的虚函数,方便子类重写 ](#uaurawidgetcontroller中写一个多播的虚函数方便子类重写)
		- [UAuraWidgetController的子类UOverlayWidgetController中](#uaurawidgetcontroller的子类uoverlaywidgetcontroller中)
			- [创建动态多播 ](#创建动态多播)
			- [UOverlayWidgetController 中 重写多播的虚函数](#uoverlaywidgetcontroller-中-重写多播的虚函数)
		- [AAuraHUD 的 InitOverlay 函数中初始化时,广播属性](#aaurahud-的-initoverlay-函数中初始化时广播属性)
		- [配置完成](#配置完成)
		- [将HP和MP的小UI,变成变量](#将hp和mp的小ui变成变量)
		- [WBP\_Overlay中使用这两个变量调用SetWidgetController函数](#wbp_overlay中使用这两个变量调用setwidgetcontroller函数)
		- [把UOverlayWidgetController中类名需要 加上 蓝图可识别该类的宏Blueprintable](#把uoverlaywidgetcontroller中类名需要-加上-蓝图可识别该类的宏blueprintable)
		- [HP这个小UI中,WidgetController就可以Cast子类了](#hp这个小ui中widgetcontroller就可以cast子类了)
		- [梳理/帮助理解:](#梳理帮助理解)
		- [创建UOverlayWidgetController蓝图类](#创建uoverlaywidgetcontroller蓝图类)
		- [修改BP\_AuraHUD中的OverlayWidgetControllerClass类,为蓝图类BP\_OverlayWidgetController](#修改bp_aurahud中的overlaywidgetcontrollerclass类为蓝图类bp_overlaywidgetcontroller)
		- [HP小UI中绑定多播](#hp小ui中绑定多播)
		- [在小UI的基类中创建设置百分比的函数](#在小ui的基类中创建设置百分比的函数)
		- [HP小UI中调用 基类中设定百分比的函数](#hp小ui中调用-基类中设定百分比的函数)
		- [在UAuraWidgetController中创建一个绑定多播绑定在自身的函数](#在uaurawidgetcontroller中创建一个绑定多播绑定在自身的函数)
		- [在UOverlayWidgetController中创建并绑定 属性变化多播和回调](#在uoverlaywidgetcontroller中创建并绑定-属性变化多播和回调)
		- [现在需要在HUD初始化UOverlayWidgetController对象时绑定多播](#现在需要在hud初始化uoverlaywidgetcontroller对象时绑定多播)
		- [UAuraAttributeSet中暂时修改初始HP为50](#uauraattributeset中暂时修改初始hp为50)
		- [梳理/帮助理解:](#梳理帮助理解-1)
		- [此时效果gif,说明已经绑定了UI效果](#此时效果gif说明已经绑定了ui效果)
		- [考试题：参考HP的部分,制作一下蓝的部分,要求捡血瓶以后,掉MP,同步UI](#考试题参考hp的部分制作一下蓝的部分要求捡血瓶以后掉mp同步ui)
		- [参考HP的部分绑定MP的多播](#参考hp的部分绑定mp的多播)
			- [下面放一下我的UOverlayWidgetController代码：](#下面放一下我的uoverlaywidgetcontroller代码)
		- [此时,有一个问题就是,UP说可以运行联机模式,但是我运行联机模式时,EnhancedSubsystem报nullptr,断言后直接崩溃](#此时有一个问题就是up说可以运行联机模式但是我运行联机模式时enhancedsubsystem报nullptr断言后直接崩溃)
			- [2人联机模式下](#2人联机模式下)
				- [找到原因是,多人模式下,PlayerController中的BeginPlay,在服务器和客户端各调用一次,但此时,客户端还没有加载完毕,此时GetLocalPlayer为空(因为还没加载完)所以PC中的 `**EnhancedSubsystem = nullptr**` **,** 等加载完毕后(也就是LocalPlayer不为空),还会再调用一次服务器的PlayerController的BeginPlay,此时EnhancedSubsystem才可以正常获得,所以得出结论,2人联机模式下,服务器会调用两次PC的BeginPlay(因为重新申请地址)](#找到原因是多人模式下playercontroller中的beginplay在服务器和客户端各调用一次但此时客户端还没有加载完毕此时getlocalplayer为空因为还没加载完所以pc中的-enhancedsubsystem--nullptr--等加载完毕后也就是localplayer不为空还会再调用一次服务器的playercontroller的beginplay此时enhancedsubsystem才可以正常获得所以得出结论2人联机模式下服务器会调用两次pc的beginplay因为重新申请地址)
				- [三人联机模式下](#三人联机模式下)


___________________________________________________________________________________________

### UAuraWidgetController中写一个多播的虚函数,方便子类重写&emsp;

+ `头文件`中：
```cpp
public:
	//自建函数 初始化 值 
	virtual void BroadcastInitValues();
```

&emsp;

+ `源文件`中：
```cpp
void UUAuraWidgetController::BroadcastInitValues()
{
}
```

&emsp;

___________________________________________________________________________________________
### UAuraWidgetController的子类UOverlayWidgetController中

#### 创建动态多播&emsp;
+ `头文件`中：
```cpp
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnHealthChangedSignature, float, NewHealth);
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnMaxMaxHealthChangedSignature,float,NewMaxMaxHealth);
```
```cpp
public:
	UPROPERTY(BlueprintAssignable, Category = "GAS|Attributes")
	FOnHealthChangedSignature FOnHealthChanged;
	UPROPERTY(BlueprintAssignable,Category="GAS|Attributes")
	FOnMaxMaxHealthChangedSignature 
```
&emsp;

+ `源文件`中：
```cpp
这里是源文件代码这里是源文件代码这里是源文件代码这里是源文件代码这里是源文件代码这里是源文件代码
```


___________________________________________________________________________________________
#### UOverlayWidgetController 中 重写多播的虚函数

&emsp;

+ `头文件`中：重写多播的虚函数
```cpp
public:
	virtual void BroadcastInitValues() override;
```

&emsp;

+ `源文件`中：

```cpp
void UOverlayWidgetController::BroadcastInitValues()
{
	//Super::BroadcastInitValues();
	//检查是否绑定广播,然后广播
	if (!FOnHealthChanged.IsBound()) return;
	if (!FOnMaxMaxHealthChanged.IsBound()) return;
	
	const UAuraAttributeSet* AuraAttributeSet = CastChecked<UAuraAttributeSet>(AttributeSet);
    
	FOnHealthChanged.Broadcast(AuraAttributeSet->GetHealth());
	FOnMaxMaxHealthChanged.Broadcast(AuraAttributeSet->GetMaxHealth());
}
```

&emsp;

___________________________________________________________________________________________
### AAuraHUD 的 InitOverlay 函数中初始化时,广播属性

+ `源文件`中：
```cpp
void AAuraHUD::InitOverlay(APlayerController* PC, APlayerState* PS, UAbilitySystemComponent* ASC, UAttributeSet* AS)
{
	checkf(OverlayWidgetClass,TEXT("OverlayWidgetClass is nullptr!!!	in: AAuraHUD!!!"))
	checkf(OverlayWidgetControllerClass,TEXT("OverlayWidgetControllerClass is nullptr!!!	in AAuraHUD!!!"))
	const TObjectPtr<UAuraUserWidget> Widget = CreateWidget<UAuraUserWidget>(GetWorld(),OverlayWidgetClass);
	OverlayWidget = Widget;
	const FWidgetControllerParams WidgetControllerParams(PC,PS,ASC,AS);
	UOverlayWidgetController* InitWidgetController = GetOverlayWidgetController(WidgetControllerParams);
	OverlayWidget->SetWidgetController(InitWidgetController);
	
	//初始化时 广播属性
	InitWidgetController->BroadcastInitValues();
    
	Widget->AddToViewport();
}
```

___________________________________________________________________________________________

### 配置完成

___________________________________________________________________________________________

### 将HP和MP的小UI,变成变量

![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-13167-190666.png?raw=true)
___________________________________________________________________________________________
### WBP_Overlay中使用这两个变量调用SetWidgetController函数

![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-556372-433918.png?raw=true)
___________________________________________________________________________________________
### 把UOverlayWidgetController中类名需要 加上 蓝图可识别该类的宏Blueprintable

```cpp
UCLASS(Blueprintable)
```

![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-242039-824055.png?raw=true)
___________________________________________________________________________________________
### HP这个小UI中,WidgetController就可以Cast子类了

![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-434921-288783.png?raw=true)
___________________________________________________________________________________________
### 梳理/帮助理解:

>此时,因为HUD中已经调用了SetWidgetController函数,而调用这个函数就会触发相应AuraUserWidget中的WidgetController的WidgetControllerSet(在蓝图中实现的函数)
**首先有一个前提,就是根据UserWidget中的逻辑：**
**只要调用SetWidgetController,就会触发该UserWidget的WidgetControllerSet(在蓝图中实现的函数)**

**下面是** **步骤讲解**

1. HUD初始化时调用WBP_Overlay的SetWidgetController函数
   ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-250252-686462.png?raw=true)

___________________________________________________________________________________________
2. 此时触发WBP_Overlay的WidgetControllerSet函数；并调用HP和MP这两个小UI的SetWidgetController函数
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-729622-845867.png?raw=true)

___________________________________________________________________________________________
3. 此时触发WBP_GlobeProgressBar_HP的WidgetControllerSet函数
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-76013-34634.png?raw=true)

___________________________________________________________________________________________
### 创建UOverlayWidgetController蓝图类
 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-611290-473844.png?raw=true)
 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-845771-844253.png?raw=true)

___________________________________________________________________________________________
### 修改BP_AuraHUD中的OverlayWidgetControllerClass类,为蓝图类BP_OverlayWidgetController
 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-15170-897420.png?raw=true)
___________________________________________________________________________________________
### HP小UI中绑定多播

![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-766309-245257.png?raw=true)

 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-830430-915199.png?raw=true)
___________________________________________________________________________________________
### 在小UI的基类中创建设置百分比的函数

 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-594719-746796.png?raw=true)

 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-685100-804151.png?raw=true)
___________________________________________________________________________________________
### HP小UI中调用 基类中设定百分比的函数

 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-281154-459296.png?raw=true)

 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-223643-924199.png?raw=true)
___________________________________________________________________________________________
### 在UAuraWidgetController中创建一个绑定多播绑定在自身的函数

在UAuraWidgetController中创建一个外部调用就可以绑定多播绑定在自身的函数(以前都是写在BeginPlay里面,这里是规范化)
 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-932484-70683.png?raw=true)
 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-584566-475412.png?raw=true)
想在子类中,方便使用,所以在父类中创建虚函数,方便子类重写
___________________________________________________________________________________________
### 在UOverlayWidgetController中创建并绑定 属性变化多播和回调

+ `头文件`中：
```cpp
public:
	virtual void BindCallbackToDependencies() override;
	//多播的 回调函数
	void HealthChanged(const FOnAttributeChangeData& Data);
	void MaxHealthChanged(const FOnAttributeChangeData& Data);
```

&emsp;

+ `源文件`中：通过ASC组件获取  **当属性变化时进行委托的多播委托** 使用API 

'GetGameplayAttributeValueChangeDelegate'

```cpp
void UOverlayWidgetController::BindCallbackToDependencies()
{
	const UAuraAttributeSet* AuraAttributeSet = CastChecked<UAuraAttributeSet>(AttributeSet);
	AbilitySystemComponent->GetGameplayAttributeValueChangeDelegate(
        AuraAttributeSet->GetHealthAttribute()).AddUObject(this,&UOverlayWidgetController::HealthChanged);
	AbilitySystemComponent->GetGameplayAttributeValueChangeDelegate(
        AuraAttributeSet->GetMaxHealthAttribute()).AddUObject(this,&UOverlayWidgetController::MaxHealthChanged);
}
```

多播的 回调函数

```cpp
void UOverlayWidgetController::HealthChanged(const FOnAttributeChangeData& Data)
{
	FOnHealthChanged.Broadcast(Data.NewValue);
}
void UOverlayWidgetController::MaxHealthChanged(const FOnAttributeChangeData& Data)
{
	FOnMaxMaxHealthChanged.Broadcast(Data.NewValue);
}
```

&emsp;

&emsp

**效果是,在别处调用UOverlayWidgetController对象的BindCallbacksToDependencies函数,就能绑定多播到UOverlayWidgetController对象上,所以建议(这步操作在该对象初始化时调用一次)**

___________________________________________________________________________________________
### 现在需要在HUD初始化UOverlayWidgetController对象时绑定多播
 ![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-423828-856517.png?raw=true)
___________________________________________________________________________________________
### UAuraAttributeSet中暂时修改初始HP为50
+ `源文件`中：
```cpp
UAuraAttributeSet::UAuraAttributeSet()
{
	InitHealth(19.0f);
	InitMaxHealth(100.0f);
}
```

&emsp;

___________________________________________________________________________________________
### 梳理/帮助理解:

此时为 **发布更新设计模式** 当ASC属性更新时通过多播,广播给UOverlayWidgetController,再由UOverlayWidgetController多播,广播给UI

### 此时效果gif,说明已经绑定了UI效果

![](https://github.com/liyunlong618/虚幻C++/模块/GAS/GAS第二季-暗黑破坏神Like游戏/配图/GAS_2.8/GAS 2.8 配置多播-幕布图片-175010-650368.gif?raw=true)
___________________________________________________________________________________________
### 考试题：参考HP的部分,制作一下蓝的部分,要求捡血瓶以后,掉MP,同步UI

![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-592669-760682.png?raw=true)
___________________________________________________________________________________________

### 参考HP的部分绑定MP的多播

>在UOverlayWidgetController中
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-40767-940326.png?raw=true)
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-698148-199373.png?raw=true)

#### 下面放一下我的UOverlayWidgetController代码：

+ `头文件`中：
```cpp
// Copyright belongs to Li Yunlong.
#pragma once

#include "CoreMinimal.h"
#include "UI/WidgetController/UAuraWidgetController.h"
#include "OverlayWidgetController.generated.h"
struct FOnAttributeChangeData;
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnHealthChangedSignature, float, NewHealth);
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnMaxMaxHealthChangedSignature,float,NewMaxMaxHealth);
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnManaChangedSignature, float, NewMana);
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnMaxMaxManaChangedSignature,float,NewMaxMaxMana);

UCLASS(Blueprintable)
class AURA_API UOverlayWidgetController : public UUAuraWidgetController
{
	GENERATED_BODY()

public:
	
	UPROPERTY(BlueprintAssignable, Category = "GAS|Attributes")
	FOnHealthChangedSignature FOnHealthChanged;
	UPROPERTY(BlueprintAssignable,Category="GAS|Attributes")
	FOnMaxMaxHealthChangedSignature FOnMaxMaxHealthChanged;
	UPROPERTY(BlueprintAssignable, Category = "GAS|Attributes")
	FOnManaChangedSignature FOnManaChanged;
	UPROPERTY(BlueprintAssignable,Category="GAS|Attributes")
	FOnMaxMaxManaChangedSignature FOnMaxMaxManaChanged;

	virtual void BroadcastInitValues() override;
	virtual void BindCallbackToDependencies() override;
	
	//多播的 回调函数
	void HealthChanged(const FOnAttributeChangeData& Data);
	void MaxHealthChanged(const FOnAttributeChangeData& Data);
	void ManaChanged(const FOnAttributeChangeData& Data);
	void MaxManaChanged(const FOnAttributeChangeData& Data);
};
```

&emsp;

+ `源文件`中：
```cpp
// Copyright belongs to Li Yunlong.


#include "UI/WidgetController/OverlayWidgetController.h"

#include "AbilitySystem/AuraAttributeSet.h"

void UOverlayWidgetController::BroadcastInitValues()
{
	//Super::BroadcastInitValues();
	
	if (!FOnHealthChanged.IsBound()||!FOnMaxMaxHealthChanged.IsBound()||
        !FOnManaChanged.IsBound()||!FOnMaxMaxManaChanged.IsBound()) return;
    
	const UAuraAttributeSet* AuraAttributeSet = CastChecked<UAuraAttributeSet>(AttributeSet);
    
	FOnHealthChanged.Broadcast(AuraAttributeSet->GetHealth());
	FOnMaxMaxHealthChanged.Broadcast(AuraAttributeSet->GetMaxHealth());
	FOnManaChanged.Broadcast(AuraAttributeSet->GetMana());
	FOnMaxMaxManaChanged.Broadcast(AuraAttributeSet->GetMaxMana());
}

void UOverlayWidgetController::BindCallbackToDependencies()
{
	const UAuraAttributeSet* AuraAttributeSet = CastChecked<UAuraAttributeSet>(AttributeSet);
	AbilitySystemComponent->GetGameplayAttributeValueChangeDelegate(
        AuraAttributeSet->GetHealthAttribute()).AddUObject(this,&UOverlayWidgetController::HealthChanged);
	AbilitySystemComponent->GetGameplayAttributeValueChangeDelegate(
        AuraAttributeSet->GetMaxHealthAttribute()).AddUObject(this,&UOverlayWidgetController::MaxHealthChanged);
	AbilitySystemComponent->GetGameplayAttributeValueChangeDelegate(
        AuraAttributeSet->GetManaAttribute()).AddUObject(this,&UOverlayWidgetController::ManaChanged);
	AbilitySystemComponent->GetGameplayAttributeValueChangeDelegate(
        AuraAttributeSet->GetMaxManaAttribute()).AddUObject(this,&UOverlayWidgetController::MaxManaChanged);
}

void UOverlayWidgetController::HealthChanged(const FOnAttributeChangeData& Data)
{
	FOnHealthChanged.Broadcast(Data.NewValue);
}

void UOverlayWidgetController::MaxHealthChanged(const FOnAttributeChangeData& Data)
{
	FOnMaxMaxHealthChanged.Broadcast(Data.NewValue);
}

void UOverlayWidgetController::ManaChanged(const FOnAttributeChangeData& Data)
{
	FOnManaChanged.Broadcast(Data.NewValue);
}

void UOverlayWidgetController::MaxManaChanged(const FOnAttributeChangeData& Data)
{
	FOnMaxMaxManaChanged.Broadcast(Data.NewValue);
}
```
___________________________________________________________________________________________

我在基类中创建了保存BP OverlayWidgetController的变量
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-832956-792377.png?raw=true)
___________________________________________________________________________________________
这样小部件都可以直接Set和Get该变量
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-923776-638884.png?raw=true)
___________________________________________________________________________________________
UI中
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-381137-359704.png?raw=true)
___________________________________________________________________________________________

### 此时,有一个问题就是,UP说可以运行联机模式,但是我运行联机模式时,EnhancedSubsystem报nullptr,断言后直接崩溃

___________________________________________________________________________________________
#### 2人联机模式下
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-233118-382167.png?raw=true)
##### 找到原因是,多人模式下,PlayerController中的BeginPlay,在服务器和客户端各调用一次,但此时,客户端还没有加载完毕,此时GetLocalPlayer为空(因为还没加载完)所以PC中的 `**EnhancedSubsystem = nullptr**` **,** 等加载完毕后(也就是LocalPlayer不为空),还会再调用一次服务器的PlayerController的BeginPlay,此时EnhancedSubsystem才可以正常获得,所以得出结论,2人联机模式下,服务器会调用两次PC的BeginPlay(因为重新申请地址)
1. 服务器端在第一次调用 BeginPlay() 时,设置自己的增强输入子系统。
2. 客户端连接到服务器后,服务器发送一条特定的网络消息给客户端。
3. 客户端收到服务器发送的网络消息后,执行相应的操作,比如设置客户端的增强输入子系统。
___________________________________________________________________________________________
##### 三人联机模式下
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.8/GAS%202.8%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E6%92%AD-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-249109-355672.png?raw=true)
___________________________________________________________________________________________

[返回最上面](#处理关键点)
    

___________________________________________________________________________________________