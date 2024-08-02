___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)
___________________________________________________________________________________________
# GAS 2.7 项目MVC架构

___________________________________________________________________________________________

## 处理关键点:结构
### 下面是结构梳理：
1 MVC(Model->四大数据PC/PS/ASC/AS；
2 View->AuraUserWidget；Control->WidgetController)+使用发布更新的架构
3 1角色（这里是角色，也可以是别的）初始化时调用HUD，根据配置的class在堆区实例化OverlayWidgetController，
4 传入数据更新OverlayWidgetController中的数据（只在初始化时，创建包含四大数据的结构体，才给OverlayWidgetController传入指针数据，后续自行持有指针）


___________________________________________________________________________________________

### 架构 概述
- 每个UI的集合是Widget，不可能直接从模型Model中获取数据，所以使用一个WidgetController作为中间的数据载体，使用发布更新的架构，不用知道谁接收了数据。而WidgetController的职责就是从Model中获取数据并更新自身数据

___________________________________________________________________________________________

- [GAS 2.7 项目MVC架构](#gas-27-项目mvc架构)
	- [处理关键点:结构](#处理关键点结构)
		- [下面是结构梳理：](#下面是结构梳理)
		- [架构 概述](#架构-概述)
		- [创建WidgetController继承自UObject，并创建保存四大数据的结构体FWidgetControllerParams](#创建widgetcontroller继承自uobject并创建保存四大数据的结构体fwidgetcontrollerparams)
		- [Overlay控制器 : 创建OverlayWidgetController继承自AuraWidgetController](#overlay控制器--创建overlaywidgetcontroller继承自aurawidgetcontroller)
		- [UAuraUserWidget 中](#uaurauserwidget-中)
			- [设置并保存WidgetController](#设置并保存widgetcontroller)
			- [此时的逻辑结构整体梳理](#此时的逻辑结构整体梳理)
		- [HUD的作用](#hud的作用)
		- [AAuraHUD 中](#aaurahud-中)
		- [设置蓝图HUD](#设置蓝图hud)
		- [在角色AAuraCharacter中通过HUD初始化WidgetController中的结构体，从而完成对WidgetController中数据的初始化 ](#在角色aauracharacter中通过hud初始化widgetcontroller中的结构体从而完成对widgetcontroller中数据的初始化)
		- [关键点：结构](#关键点结构)
			- [下面是结构梳理：](#下面是结构梳理-1)
				- [MVC(Model-\>四大数据PC/PS/ASC/AS；View-\>AuraUserWidget；Control-\>WidgetController)+使用发布更新的架构](#mvcmodel-四大数据pcpsascasview-aurauserwidgetcontrol-widgetcontroller使用发布更新的架构)


___________________________________________________________________________________________
### 创建WidgetController继承自UObject，并创建保存四大数据的结构体FWidgetControllerParams

> UUAuraWidgetController中

​		 保存四大数据：PC/PS/ASC/AS

+ `头文件`中：
```cpp
class UAttributeSet;
class UAbilitySystemComponent;
创建结构体 保存四大数据：PC/PS/ASC/AS
USTRUCT(BlueprintType)
struct FWidgetControllerParams
{
	GENERATED_BODY()

	FWidgetControllerParams()
		: PlayerController(nullptr), PlayerState(nullptr), AbilitySystemComponent(nullptr), AttributeSet(nullptr)
	{
	}

	FWidgetControllerParams(APlayerController* PC, APlayerState* PS, UAbilitySystemComponent* ASC, UAttributeSet* AS)
		: PlayerController(PC), PlayerState(PS), AbilitySystemComponent(ASC), AttributeSet(AS)
	{
	}
	UPROPERTY(BlueprintReadOnly, Category="WidgetController")
	TObjectPtr<APlayerController> PlayerController;//结构体中的PC
	UPROPERTY(BlueprintReadOnly, Category="WidgetController")
	TObjectPtr<APlayerState> PlayerState;//结构体中的PS
	UPROPERTY(BlueprintReadOnly, Category="WidgetController")
	TObjectPtr<UAbilitySystemComponent> AbilitySystemComponent;//结构体中的ASC
	UPROPERTY(BlueprintReadOnly, Category="WidgetController")
	TObjectPtr<UAttributeSet> AttributeSet;//结构体中的AS
};

UCLASS()
class AURA_API UUAuraWidgetController : public UObject
{
	GENERATED_BODY()
public:
	UFUNCTION(BlueprintCallable)
	void SetWidgetControllerParams(const FWidgetControllerParams& WCParams);
protected:
	//WidgetController内部 保存四大数据：PC/PS/ASC/AS
	UPROPERTY(BlueprintReadOnly,Category="WidgetController")
	TObjectPtr<APlayerController> PlayerController;
	UPROPERTY(BlueprintReadOnly,Category="WidgetController")
	TObjectPtr<APlayerState> PlayerState;
	UPROPERTY(BlueprintReadOnly,Category="WidgetController")
	TObjectPtr<UAbilitySystemComponent> AbilitySystemComponent;
	UPROPERTY(BlueprintReadOnly,Category="WidgetController")
	TObjectPtr<UAttributeSet> AttributeSet;
};
```

&emsp;

+ `源文件`中：
```cpp
void UUAuraWidgetController::SetWidgetControllerParams(const FWidgetControllerParams& WCParams)
{
	PlayerController = WCParams.PlayerController;
	PlayerState = WCParams.PlayerState;
	AbilitySystemComponent = WCParams.AbilitySystemComponent;
	AttributeSet = WCParams.AttributeSet;
}
```

___________________________________________________________________________________________

### Overlay控制器 : 创建OverlayWidgetController继承自AuraWidgetController

```cpp
UOverlayWidgetController : public UUAuraWidgetController
```

>想要在蓝图中派生，需要加入BlueprintType宏

```cpp
UCLASS(BlueprintType)
```

&emsp;&emsp;

___________________________________________________________________________________________

### UAuraUserWidget 中

想要在蓝图中实现WidgetControllerSet函数(类似回调)

C++中调用SetWidgetController后，触发WidgetControllerSet函数&emsp;

+ `头文件`中：
```cpp
public:
	UFUNCTION(BlueprintCallable)
	void SetWidgetController(UObject* InWidgetController);
	UPROPERTY(BlueprintReadOnly)
	TObjectPtr<UObject> WidgetController;
protected:
	//调用上面的 SetWidgetController 函数后 触发此函数
	UFUNCTION(BlueprintImplementableEvent)
	void WidgetControllerSet();
```

&emsp;

+ `源文件`中：
```cpp
void UAuraUserWidget::SetWidgetController(UObject* InWidgetController)
{
	WidgetController = InWidgetController;
	//调用蓝图的 设置 WidgetController 函数
	WidgetControllerSet();
}
```

&emsp;

___________________________________________________________________________________________

#### 设置并保存WidgetController
___________________________________________________________________________________________

#### 此时的逻辑结构整体梳理
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.7/GAS%202.7%20%E9%A1%B9%E7%9B%AEMVC%E6%9E%B6%E6%9E%84-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-989651-714655.png?raw=true)
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.7/GAS%202.7%20%E9%A1%B9%E7%9B%AEMVC%E6%9E%B6%E6%9E%84-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-315785-520915.png?raw=true)
___________________________________________________________________________________________

### HUD的作用 

![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.7/GAS%202.7%20%E9%A1%B9%E7%9B%AEMVC%E6%9E%B6%E6%9E%84-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-435531-608578.png?raw=true)
___________________________________________________________________________________________

### AAuraHUD 中

&emsp;

+ `头文件`中：
```cpp
// Copyright belongs to Li Yunlong.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/HUD.h"
#include "Runtime/CoreUObject/Public/UObject/ObjectPtr.h"
#include "AuraHUD.generated.h"

class UAttributeSet;
class UAbilitySystemComponent;
class UOverlayWidgetController;
class UAuraUserWidget;

UCLASS()
class AURA_API AAuraHUD : public AHUD
{
	GENERATED_BODY()
public:
	//主UI的指针
	UPROPERTY()
	TObjectPtr<UAuraUserWidget> OverlayWidget;
    
	virtual void BeginPlay() override;
    
	//获取 WidgetController(第一次时需要传入结构体参数，根据参数进行初始化，后续传参数也没用)
	UOverlayWidgetController* GetOverlayWidgetController(const struct FWidgetControllerParams& WC_Params);
	//传入四大数据 初始化结构体 结构体传参到OverlayWidgetController
	void InitOverlay(APlayerController* PC, APlayerState* PS, UAbilitySystemComponent* ASC, UAttributeSet* AS);
    
private:
    
	//主UI Class
	UPROPERTY(EditAnywhere)
	TSubclassOf<UAuraUserWidget> OverlayWidgetClass;
    
	//OverlayWidgetController Class和指针
	UPROPERTY(EditAnywhere)
	TSubclassOf<UOverlayWidgetController> OverlayWidgetControllerClass;
	UPROPERTY()
	TObjectPtr<UOverlayWidgetController> OverlayWidgetController;
};
```

&emsp;

+ `源文件`中：
```cpp
// Copyright belongs to Li Yunlong.
#include "UI/HUD/AuraHUD.h"
#include "UI/Widget/AuraUserWidget.h"
#include "UI/WidgetController/OverlayWidgetController.h"

void AAuraHUD::BeginPlay()
UOverlayWidgetController* AAuraHUD::GetOverlayWidgetController(const FWidgetControllerParams& WC_Params)
{
	Super::BeginPlay();
	checkf(OverlayWidgetClass,TEXT("OverlayWidgetClass is nullptr!!! in:	AAuraHUD!!!"));
	if (OverlayWidgetController == nullptr)
	{
		checkf(OverlayWidgetControllerClass,TEXT("OverlayWidgetControllerClass is nullptr!!!	in: AAuraHUD!!!"))
		OverlayWidgetController = NewObject<UOverlayWidgetController>(this,OverlayWidgetControllerClass);
		OverlayWidgetController->SetWidgetControllerParams(WC_Params);
	}
	return OverlayWidgetController;
}
void AAuraHUD::InitOverlay(APlayerController* PC, APlayerState* PS, UAbilitySystemComponent* ASC, UAttributeSet* AS)
{
	checkf(OverlayWidgetClass,TEXT("OverlayWidgetClass is nullptr!!!	in: AAuraHUD!!!"))
	checkf(OverlayWidgetControllerClass,TEXT("OverlayWidgetControllerClass is nullptr!!!	in AAuraHUD!!!"))

	const TObjectPtr<UAuraUserWidget> Widget = CreateWidget<UAuraUserWidget>(GetWorld(),OverlayWidgetClass);
	OverlayWidget = Widget;

	const FWidgetControllerParams WidgetControllerParams(PC,PS,ASC,AS);
	UOverlayWidgetController* InitWidgetController = GetOverlayWidgetController(WidgetControllerParams);
	OverlayWidget->SetWidgetController(InitWidgetController);
	
	Widget->AddToViewport();
}
```

&emsp;

&emsp;

![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.7/GAS%202.7%20%E9%A1%B9%E7%9B%AEMVC%E6%9E%B6%E6%9E%84-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-247150-756138.png?raw=true)

___________________________________________________________________________________________

### 设置蓝图HUD
![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.7/GAS%202.7%20%E9%A1%B9%E7%9B%AEMVC%E6%9E%B6%E6%9E%84-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-403915-800792.png?raw=true)
___________________________________________________________________________________________

### 在角色AAuraCharacter中通过HUD初始化WidgetController中的结构体，从而完成对WidgetController中数据的初始化&emsp;
+ `AAuraCharacter头文件`中：
```cpp
protected:

	//自建 初始化技能信息 函数
	void InitAbilityActorInfo();
```

&emsp;

+ `AAuraCharacter源文件`中：
```cpp
void AAuraCharacter::InitAbilityActorInfo()
{
	TObjectPtr<AAuraPlayerState> AuraPlayerState = GetPlayerState<AAuraPlayerState>();
	check(AuraPlayerState);
	AuraPlayerState->GetAbilitySystemComponent()->InitAbilityActorInfo(AuraPlayerState,this);
	AbilitySystemComponent = AuraPlayerState->GetAbilitySystemComponent();
	AttributeSet = AuraPlayerState->GetAttributeSet();

	//在角色中通过HUD初始化 WidgetController
	if (AAuraPlayerController* AuraPlayerController = Cast<AAuraPlayerController>(GetController()))
	{
		if (AAuraHUD* AuraHUD = Cast<AAuraHUD>(AuraPlayerController->GetHUD()))
		{
			AuraHUD->InitOverlay(AuraPlayerController,AuraPlayerState,AbilitySystemComponent,AttributeSet);
		}
	}
}
```

&emsp;

![图片](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.7/GAS%202.7%20%E9%A1%B9%E7%9B%AEMVC%E6%9E%B6%E6%9E%84-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-494883-232298.png?raw=true)
___________________________________________________________________________________________

### 关键点：结构
#### 下面是结构梳理：
##### MVC(Model->四大数据PC/PS/ASC/AS；View->AuraUserWidget；Control->WidgetController)+使用发布更新的架构
___________________________________________________________________________________________

[返回最上面](#处理关键点:结构)

___________________________________________________________________________________________