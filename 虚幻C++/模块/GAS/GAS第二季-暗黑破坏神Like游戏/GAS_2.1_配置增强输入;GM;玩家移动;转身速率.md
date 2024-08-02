___________________________________________________________________________________________
>[!!!!!!!!!!!返回项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)
___________________________________________________________________________________________

# GAS 2.1 配置增强输入/GM/玩家移动/转身速率

___________________________________________________________________________________________

## <font color=red>处理关键点：</font>

<font face="黑体" color=red size=3>1. PlayerController配置鼠标相关设置</font>

<font face="黑体" color=red size=3>2. PlayerController配置增强输入</font>

<font face="黑体" color=red size=3>3. 增强输入配置</font>

<font face="黑体" color=red size=3>4. 增强输入移动形参类型</font>

<font face="黑体" color=red size=3>5. PlayerController的角色移动旋转计算</font>

<font face="黑体" color=red size=3>6. 转身速率配置</font>

<font face="黑体" color=red size=3>7. PlayerControllerRotation映射SpringArm旋转配置</font>

___________________________________________________________________________________________


[TOC]


___________________________________________________________________________________________

### 添加增强输入

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/1.png?raw=true)

&emsp;

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/2.png?raw=true)

&emsp;

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/3.png?raw=true)

&emsp;

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/4.png?raw=true)

&emsp;

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/5.png?raw=true)

___________________________________________________________________________________________
### 创建PlayerController

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/6.png?raw=true)

___________________________________________________________________________________________
### 在<font color=yellow>AAuraPlayerController</font>中配置增强输入

&emsp;

+ 头文件
```CPP
UCLASS()
class AURA_API AAuraPlayerController : public APlayerController
{
	GENERATED_BODY()
	
public:
	
	AAuraPlayerController();

protected:

	virtual void BeginPlay() override;
	
private:

	UPROPERTY(EditAnywhere,Category="Input")
	TObjectPtr<UInputMappingContext> AuraContext;

	UPROPERTY(EditAnywhere,Category="Input")
	TObjectPtr<UInputAction> MoveAction;
};
```

&emsp;

+ 源文件
```CPP
void AAuraPlayerController::BeginPlay()
{
	Super::BeginPlay();
	
	checkf(AuraContext,TEXT("AuraContext is nullptr!!! in:	AuraPlayerController!!!"))
	const TObjectPtr<UEnhancedInputLocalPlayerSubsystem> Subsystem =  ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(GetLocalPlayer());
	
	//这里修改的原因是服务器并没有这个Subsystem
	//checkf(Subsystem,TEXT("Subsystem is nullptr!!! in:	AuraPlayerController!!!"))
    
    //改用if判断
	if (Subsystem)
	{
		Subsystem->AddMappingContext(AuraContext,0);
	}
	
	//显示鼠标
	SetShowMouseCursor(true);
	//使用默认的鼠标样式(可以自定义鼠标样式)
	DefaultMouseCursor = EMouseCursor::Default;
	
	//创建一个 输入模式配置 文件
	FInputModeGameAndUI InputModeData;
	//鼠标不要锁定在屏幕正中间
	InputModeData.SetLockMouseToViewportBehavior(EMouseLockMode::DoNotLock);
	//在捕获过程中设置隐藏光标(false)
	InputModeData.SetHideCursorDuringCapture(false);
	//应用
	SetInputMode(InputModeData);
}
```

___________________________________________________________________________________________
### <font color=yellow>AAuraPlayerController</font>中添加移动功能

&emsp;

+ 头文件
```CPP
private:
	
	void Move(const FInputActionValue& InputActionValue);

protected:

	virtual void SetupInputComponent() override;
	
```

&emsp;

+ 源文件
```CPP
void AAuraPlayerController::SetupInputComponent()
{
	Super::SetupInputComponent();
	//断言类型检查
	const TObjectPtr<UEnhancedInputComponent> EnhancedInputComponent = CastChecked<UEnhancedInputComponent>(InputComponent);
	AuraInputComponent->BindAction(MoveAction,ETriggerEvent::Triggered,this,&AAuraPlayerController::Move);
}
```



```CPP
void AAuraPlayerController::Move(const FInputActionValue& InputActionValue)
{
	const FVector2D InputAxisVector2D = InputActionValue.Get<FVector2D>();
	const FRotator YawRotator = FRotator(0.0f, GetControlRotation().Yaw, 0.0f);

	const FVector ForwardDir = FRotationMatrix(YawRotator).GetUnitAxis(EAxis::Y);
	const FVector RightDir = FRotationMatrix(YawRotator).GetUnitAxis(EAxis::X);
	if (const TObjectPtr<APawn> ControlPawn = GetPawn())
	{
		ControlPawn->AddMovementInput(ForwardDir, InputAxisVector2D.Y);
		ControlPawn->AddMovementInput(RightDir, InputAxisVector2D.X);
	}
}
```
<font face="黑体" color=red size=5>这里有一个问题,上面 `AddMovementInput` 时XY填反了</font>

___________________________________________________________________________________________
### 创建文件夹/创建BP_PC/BP_Gamemode

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/7.png?raw=true)

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/8.png?raw=true)

___________________________________________________________________________________________
### 配置增强输入和GM

+  配置增强输入

因为断言的存在，不配置会崩溃

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/9.png?raw=true)

+ 配置GM

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/10.png?raw=true)


___________________________________________________________________________________________
### 玩家<font color=yellow>AAuraCharacter</font>身上，添加并配置弹簧臂

+ 添加

&emsp;

+ 头文件
```cpp

private:

	UPROPERTY(EditAnywhere,Category="Camera")
	TObjectPtr<USpringArmComponent> SpringArm;
	UPROPERTY(EditAnywhere,Category="Camera")
	TObjectPtr<UCameraComponent> Camera;
```

&emsp;

+ 源文件
```cpp
AAuraCharacter::AAuraCharacter()
{
	SpringArm = CreateDefaultSubobject<USpringArmComponent>("SpringArm");
	SpringArm->SetupAttachment(RootComponent);
	Camera = CreateDefaultSubobject<UCameraComponent>("Camera");
	Camera->SetupAttachment(SpringArm);
}
```

&emsp;

+ 旋转

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/11.png?raw=true)


&emsp;

#### 使用PC旋转并取消继承

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/12.png?raw=true)

&emsp;

### 调整角色转身速率

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/13.png?raw=true)

&emsp;

___________________________________________________________________________________________
<font face="黑体" color=red size=5>Bug：现在有一个角色一旦停下来，立刻进入Idle左右摆头的问题</font>

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/14.gif)

### 修复角色Idle左右摆头的问题

+  添加Idle动画

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/15.png?raw=true)

&emsp;

+  添加过度条件

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/16.png?raw=true)

&emsp;

+  设置过度条件

这样会稍微缓和转头的速率，毕竟加了个判定

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS-2.1/17.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#处理关键点：)
___________________________________________________________________________________________