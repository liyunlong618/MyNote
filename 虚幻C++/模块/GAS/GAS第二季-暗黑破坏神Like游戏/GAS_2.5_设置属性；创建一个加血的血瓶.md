___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)
___________________________________________________________________________________________
# GAS 2.5 设置属性；创建一个加血的血瓶


___________________________________________________________________________________________

## 处理关键点：
1. GetLifetimeReplicatedProps 此函数在U0bject中 开启 属性复制(RepNotify)后 需要重写这个函数!//此函数规定了:1.哪些参数同步 以及 2.同步的条件
2. 根据AttributeSet基类中写好的宏Get/set/lnit 属性；
3. 为每个属性创建属性复制和相关函数；调用同步函数，设置同步参数；DOREPLIFETIME_CONDITION_NOTIFY宏使用（在UnrealNetwork.h中）
4. GAS调试debug命令showdebug abilitysystem
5. overlap委托和回调绑定
6. 使用const_cast把const变量转化为非const变量

___________________________________________________________________________________________

- [GAS 2.5 设置属性；创建一个加血的血瓶](#gas-25-设置属性创建一个加血的血瓶)
	- [处理关键点：](#处理关键点)
		- [属性 的 结构体介绍](#属性-的-结构体介绍)
		- [设置属性UAuraAttributeSet](#设置属性uauraattributeset)
				- [DOREPLIFETIME\_CONDITION\_NOTIFY 宏](#doreplifetime_condition_notify-宏)
				- [GAMEPLAYATTRIBUTE\_REPNOTIFY宏](#gameplayattribute_repnotify宏)
					- [GAS调试debug命令](#gas调试debug命令)
		- [创建一个血瓶Actor](#创建一个血瓶actor)
			- [AuraEffectActor](#auraeffectactor)
			- [删除不用的Tick，并在构造中关掉Tick](#删除不用的tick并在构造中关掉tick)
			- [重叠时，把收到的 UAttributeSet 类型转化为 UAuraAttributeSet 类型](#重叠时把收到的-uattributeset-类型转化为-uauraattributeset-类型)
			- [创建蓝图类继承自AAuraEffectActor](#创建蓝图类继承自aauraeffectactor)
				- [拖入场景](#拖入场景)
				- [此阶段测试结果](#此阶段测试结果)
			- [设置Mesh](#设置mesh)
			- [改成加血/加血后Destroy](#改成加血加血后destroy)


___________________________________________________________________________________________
### 属性 的 结构体介绍
- 一共有两个参数:
	- 'BaseValue' 
	- 'CurrentValue'
- 这俩参数的区别
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/1.png?raw=true)
- ![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/2.png?raw=true)


___________________________________________________________________________________________
### 设置属性UAuraAttributeSet
1. ##### 先写网络属性复制
+ `头文件`中：
	
	&emsp;
	
	+ `头文件`中：
	```cpp
	#include "AbilitySystemComponent.h"
	public:
		//此函数规定了:	1.哪些参数同步 以及 2.同步的条件			此函数在UObject中 开启 属性复制(RepNotify)后 需要重写这个函数!
		virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;
	
		//ReplicatedUsing = OnRep_Health  :当前属性 Health 发生变化时 自动调用 OnRep_Health 这个回调函数
		UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_Health, Category="Vita|Attribute")
		FGameplayAttributeData Health;
		ATTRIBUTE_ACCESSORS(UAuraAttributeSet,Health);//AS组件源码中 帮助 Get / Set / Init 属性的宏
		
		UFUNCTION()
		void OnRep_Health(const FGameplayAttributeData& OldHealth);//在每个回调函数中 需要做 网络同步 相关的事
	```
	
	&emsp;
	
	+ `源文件`中：
	```cpp
	void UAuraAttributeSet::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const
	{
		Super::GetLifetimeReplicatedProps(OutLifetimeProps);
		//此函数在 UnrealNetwork.cpp 中 需要提供的参数(哪个类中,哪个参数,同步条件,什么时候同步数据)
			DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,Health,COND_None,REPNOTIFY_Always);
		}
		
	void UAuraAttributeSet::OnRep_Health(const FGameplayAttributeData& OldHealth)
	{
		//此函数在 ASC组件中 但是可以在AS组件 UAttributeSet 中找到使用方法
		GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Health,OldHealth);
	}
	```
	
	&emsp;

##### DOREPLIFETIME_CONDITION_NOTIFY 宏

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/5.png?raw=true)

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/6.png?raw=true)

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/7.png?raw=true)

> [CSDN链接参考:ue4-Network相关-变量同步](https://blog.csdn.net/sinat_28941165/article/details/83183034)

##### GAMEPLAYATTRIBUTE_REPNOTIFY宏
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/8.png?raw=true)



2. ##### 使用官方宏，用于Get/set/Init 属性值


&emsp;

+ `头文件`中：
```cpp
//从AS组件源码中找到的帮助 Get / Set / Init 属性的宏
#define ATTRIBUTE_ACCESSORS(ClassName, PropertyName) \
	GAMEPLAYATTRIBUTE_PROPERTY_GETTER(ClassName, PropertyName) \
	GAMEPLAYATTRIBUTE_VALUE_GETTER(PropertyName) \
	GAMEPLAYATTRIBUTE_VALUE_SETTER(PropertyName) \
	GAMEPLAYATTRIBUTE_VALUE_INITTER(PropertyName)

```

> ATTRIBUTE_ACCESSORS(该属性所在的类,属性名);

```cpp
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_Health, Category="Vita|Attribute")
	FGameplayAttributeData Health;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet,Health);//AS组件源码中 帮助 Get / Set / Init 属性的宏
```

&emsp;


3. ##### 构造函数中初始化 属性值

&emsp;

+ `头文件`中：
```cpp
public:
	UAuraAttributeSet();
```

&emsp;

+ `源文件`中：
  + 这里 自己并没有写这些函数但是现在多出来 还可以用的原因是 用了上面的ATTRIBUTE_ACCESSORS宏
```cpp
UAuraAttributeSet::UAuraAttributeSet()
{
	InitHealth(89.0f);
	InitMaxHealth(100.0f);
	InitMana(189.0f);
	InitMaxMana(250.0f);
}
```
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/11.png?raw=true)

&emsp;

&emsp;



4. ##### 如果报错，这里是我用到的头文件
###### 		UAuraAttributeSet.h 
```cpp
#include "CoreMinimal.h"
#include "AbilitySystemComponent.h"
#include "AttributeSet.h"
#include "AuraAttributeSet.generated.h"
```
###### 		UAuraAttributeSet.cpp
```cpp
#include "AbilitySystem/AuraAttributeSet.h"
#include "AbilitySystemComponent.h"
#include "Net/UnrealNetwork.h"
```
___________________________________________________________________________________________
###### 		GAS调试debug命令
```cpp
showdebug abilitysystem
```
​	也可以是
```cpp
showdebug ability
```


![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/13.png?raw=true)


___________________________________________________________________________________________
### 创建一个血瓶Actor
#### AuraEffectActor
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/14.png?raw=true)
#### 删除不用的Tick，并在构造中关掉Tick
```cpp
AAuraEffectActor::AAuraEffectActor()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = false;
}

```
#### 重叠时，把收到的 UAttributeSet 类型转化为 UAuraAttributeSet 类型

&emsp;

+ `头文件`中：
```cpp
class USphereComponent;
class UStaticMeshComponent;

protected:
	UPROPERTY(VisibleAnywhere)
	TObjectPtr<USphereComponent> Sphere;
	UPROPERTY(VisibleAnywhere)
	TObjectPtr<UStaticMeshComponent> Mesh;

	UFUNCTION()//重叠 回调事件
	void OnOverlap(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp,
	               int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);
```

&emsp;

+ `源文件`中：
```cpp
AAuraEffectActor::AAuraEffectActor()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = false;

	Mesh = CreateDefaultSubobject<UStaticMeshComponent>("Mesh");
	SetRootComponent(Mesh);
	Sphere = CreateDefaultSubobject<USphereComponent>("Sphere");
	Sphere->SetupAttachment(Mesh);
}

// Called when the game starts or when spawned
void AAuraEffectActor::BeginPlay()
{
	Super::BeginPlay();
    //这里绑定overlap回调
	Sphere->OnComponentBeginOverlap.AddDynamic(this,&AAuraEffectActor::OnOverlap);
}

void AAuraEffectActor::OnOverlap(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor,
                                 UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep,
                                 const FHitResult& SweepResult)
{
	TScriptInterface<IAbilitySystemInterface> ASC_Interface = OtherActor;
	if (!ASC_Interface)return;
	if (const UAuraAttributeSet* AuraAttributeSet = Cast<UAuraAttributeSet>(
		ASC_Interface->GetAbilitySystemComponent()->GetAttributeSet(UAuraAttributeSet::StaticClass())))
	{
		//TODO 下面是测试用的逻辑:使用const_cast把const转化为非const变量 然后直接设置值！！！
		UAuraAttributeSet* TestAttributeSet = const_cast<UAuraAttributeSet*>(AuraAttributeSet);
		TestAttributeSet->SetHealth(TestAttributeSet->GetHealth() - 25.0f);
		//测试打印
		UE_LOG(UELOG_AuraEffectActor, Warning, TEXT("Health:%f"), TestAttributeSet->GetHealth())
	}
}

```

&emsp;&emsp;

#### 创建蓝图类继承自AAuraEffectActor

暂时取消隐藏

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/18.png?raw=true)
##### 拖入场景

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/19.png?raw=true)

##### 此阶段测试结果

##### 

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/20.png?raw=true)



#### 设置Mesh

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.5/21.png?raw=true)

#### 改成加血/加血后Destroy

+ `源文件`中：
```cpp

void AAuraEffectActor::OnOverlap(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor,
                                 UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep,
                                 const FHitResult& SweepResult)
{
	TScriptInterface<IAbilitySystemInterface> ASC_Interface = OtherActor;
	if (!ASC_Interface)return;
	if (const UAuraAttributeSet* AuraAttributeSet = Cast<UAuraAttributeSet>(
		ASC_Interface->GetAbilitySystemComponent()->GetAttributeSet(UAuraAttributeSet::StaticClass())))
	{
		UAuraAttributeSet* TestAttributeSet = const_cast<UAuraAttributeSet*>(AuraAttributeSet);
		TestAttributeSet->SetHealth(TestAttributeSet->GetHealth() - 25.0f);
		UE_LOG(UELOG_AuraEffectActor, Warning, TEXT("Health:%f"), TestAttributeSet->GetHealth())
         //这里摧毁
         Destroy();
	}
}

```



___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________

[页内自由跳转]: 