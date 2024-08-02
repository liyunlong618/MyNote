___________________________________________________________________________________________
>[!!!!!!!!!!!返回项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)
___________________________________________________________________________________________
# GAS 2.4 GAS网络同步的 属性同步模式 类型 和 设置

___________________________________________________________________________________________

## <font color=red>处理关键点：</font>

<font face="黑体" color=red size=3>1. 角色PS中创建ASC组件，角色通过PS持有ASC组件和AS组件 </font>

<font face="黑体" color=red size=3>2. 调用ASC组件的初始化函数进行初始化（不能在构造中初始化！）</font>

<font face="黑体" color=red size=3>3. ASC组件——网络复制 属性同步模式，一共有3种类型:1.Minimal /2.Mixed /3.Full </font>

<font face="黑体" color=red size=3>4. 当PlayerState存在时 同步给所有客户端 的函数 </font>

___________________________________________________________________________________________

[TOC]

___________________________________________________________________________________________

### **<font color=yellow> Aura.Build.cs </font>**中导入模块

```CPP
"GameplayTags","GameplayTasks","GameplayAbilities"
```



![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.4/1.png?raw=true)

___________________________________________________________________________________________

### 创建c++类，分别继承自：PlayerState/AbilitySystemComponent组件/AttributeSet

- **<font color=yellow> PlayerState </font>**
  
  
  

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.4/2.png?raw=true)

- **<font color=yellow> AbilitySystemComponent </font>**组件
  

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.4/3.png?raw=true)

- **<font color=yellow> AttributeSet </font>**
  

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.4/4.png?raw=true)

___________________________________________________________________________________________

### **<font color=yellow> AAuraCharacterBase </font>**中创建两个智能指针，保存ASC技能组件和AS属性组件（敌人用）

- 头文件中声明两个变量，实现一下接口类的函数

  &emsp;

  + `头文件`中：
  ```cpp
  //引入ASC组件 用到的接口
  #include "AbilitySystemInterface.h"
  class UAbilitySystemComponent;
  class UAttributeSet;
  
  //UCLASS(Abstract) 表示这个类是一个抽象类，不能被实例化。
  //IAbilitySystemInterface 如果想要在该类中使用ASC组件，必须继承这个接口
  UCLASS(Abstract)
  class AURA_API AAuraCharacterBase
  	: public ACharacter
  	  , public IAbilitySystemInterface
  {
  	
  	GENERATED_BODY()
  
  public:
          virtual UAbilitySystemComponent* GetAbilitySystemComponent() const override;
  protected:
  	UPROPERTY()
  	TObjectPtr<UAbilitySystemComponent> AbilitySystemComponent;
  	UPROPERTY()
  	TObjectPtr<UAttributeSet> AttributeSet;
  }
  ```

  &emsp;

  + `源文件`中：
  ```cpp
  UAbilitySystemComponent* AAuraCharacterBase::GetAbilitySystemComponent() const
  {
  	return AbilitySystemComponent;
  }
  ```

  &emsp;

- 用智能指针的原因是，这两个变量会在函数中创建，防止内存泄漏

___________________________________________________________________________________________

### 敌人类**<font color=yellow> AAuraEnemy </font>**中创建 ASC技能组件 和 AS属性设置

&emsp;

+ `头文件`中：添加 构造函数
```cpp
	AAuraEnemy();
```

&emsp;

+ `源文件`中：
```cpp
//引入 头文件
#include "AbilitySystem/AuraAbilitySystemComponent.h"
#include "AbilitySystem/AuraAttributeSet.h"

AAuraEnemy::AAuraEnemy()
{
	//敌人中创建 ASC组件 和 AS组件
	AbilitySystemComponent = CreateDefaultSubobject<UAuraAbilitySystemComponent>("AbilitySystemComponent");
	AttributeSet = CreateDefaultSubobject<UAuraAttributeSet>("AttributeSet");
	//开启网络复制
	AbilitySystemComponent->SetIsReplicated(true);
}
```

&emsp;

&emsp;
___________________________________________________________________________________________
### 玩家Playerstate文件**<font color=yellow> AAuraPlayerState </font>**中,创建 ASC技能组件 和 AS属性设置

&emsp;

+ `头文件`中：
```cpp
class UAttributeSet;

//IAbilitySystemInterface 如果想要在该类中使用ASC组件，必须继承这个接口
UCLASS()
class AURA_API AAuraPlayerState
	: public APlayerState
	  , public IAbilitySystemInterface
{
	GENERATED_BODY()
public:
	
	AAuraPlayerState();

	virtual UAbilitySystemComponent* GetAbilitySystemComponent() const override;

	UAttributeSet* GetAttributeSet() const { return AttributeSet; }
	
protected:

	// Player需要在PS中保存 ASC组件 和 AS组件
	UPROPERTY()
	TObjectPtr<UAbilitySystemComponent> AbilitySystemComponent;
	UPROPERTY()
	TObjectPtr<UAttributeSet> AttributeSet;
	
};
```

&emsp;

+ `源文件`中：
```cpp
#include "PlayerState/AuraPlayerState.h"

#include "AbilitySystem/AuraAbilitySystemComponent.h"
#include "AbilitySystem/AuraAttributeSet.h"

AAuraPlayerState::AAuraPlayerState()
{
	//角色PS中创建 ASC组件 和 AS组件
	AbilitySystemComponent = CreateDefaultSubobject<UAuraAbilitySystemComponent>("AbilitySystemComponent");
	AttributeSet = CreateDefaultSubobject<UAuraAttributeSet>("AttributeSet");
	//开启网络复制
	AbilitySystemComponent->SetIsReplicated(true);
	AbilitySystemComponent->SetReplicationMode(EGameplayEffectReplicationMode::Mixed);
}
UAbilitySystemComponent* AAuraPlayerState::GetAbilitySystemComponent() const
{
	return AbilitySystemComponent;
}
```

&emsp;

&emsp;

___________________________________________________________________________________________

### GAS网络同步的属性同步模式


___________________________________________________________________________________________
- 玩家PS中开启网络同步

![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.4/5.png?raw=true)

### 玩家PS**<font color=yellow> AAuraPlayerState </font>**中,中设置属性网络同步模式

  &emsp;

    + `源文件`中：
    ```cpp
    AAuraPlayerState::AAuraPlayerState()
    {
    	AbilitySystemComponent = CreateDefaultSubobject<UAuraAbilitySystemComponent>("AbilitySystemComponent");
    	AttributeSet = CreateDefaultSubobject<UAuraAttributeSet>("AttributeSet");
    	AbilitySystemComponent->SetIsReplicated(true);
        //因为是多人模式，最高权限就是这个
    	AbilitySystemComponent->SetReplicationMode(EGameplayEffectReplicationMode::Mixed);
    	
    }
    ```

___________________________________________________________________________________________

  &emsp;

  ### 敌人基类**<font color=yellow> AAuraEnemy </font>**构造中设置属性网络同步模式

  &emsp;

  + `源文件`中：
  ```cpp
  AAuraEnemy::AAuraEnemy()
  {
  	AbilitySystemComponent = CreateDefaultSubobject<UAuraAbilitySystemComponent>("AbilitySystemComponent");
  	AttributeSet = CreateDefaultSubobject<UAuraAttributeSet>("AttributeSet");
  	AbilitySystemComponent->SetIsReplicated(true);
      //设置敌人为最小权限同步 因为玩家不必知道敌人的 GE 比如 CD
  	AbilitySystemComponent->SetReplicationMode(EGameplayEffectReplicationMode::Minimal);
  }
  ```

  &emsp;


___________________________________________________________________________________________


  ### 主角和敌人的ASC初始化：(多人模式下必须要做，单人可跳过这步)
___________________________________________________________________________________________
  ### 敌人类**<font color=yellow> AAuraEnemy </font>**中，重写BeginPlay，初始化ASC

-（不能在构造中初始化，有可能因为网络找不到，因为用断言，就直接崩了）使用模块写好的初始化API

  &emsp;

  + `头文件`中：
  ```cpp
  protected:
  	virtual void BeginPlay() override;
  ```

  &emsp;

  + `源文件`中：
  ```cpp
  void AAuraEnemy::BeginPlay()
  {
  	Super::BeginPlay();
      //断言检查ASC组件
  	check(AbilitySystemComponent);
      //使用ASC组件的初始化API 两个参数(谁是持有,谁是代理)
  	AbilitySystemComponent->InitAbilityActorInfo(this,this);
  }
  ```

  &emsp;

  &emsp;

___________________________________________________________________________________________

  ### 玩家角色类中**<font color=yellow> AAuraCharacter </font>**中初始化并同步到所有客户端，需要重写几个函数

  &emsp;

  + `头文件`中：
  ```cpp
  public:
  	//player被控制时调用的函数
  	virtual void PossessedBy(AController* NewController) override;
  	//ps回调函数
  	virtual void OnRep_PlayerState() override;
  protected:
  	//自建 初始化技能信息 函数
  	void InitAbilityActorInfo();
  ```

  &emsp;

  + `源文件`中：
  ```cpp
  #include "AbilitySystemComponent.h"
  #include "PlayerState/AuraPlayerState.h"
  
  void AAuraCharacter::PossessedBy(AController* NewController)
  {
  	Super::PossessedBy(NewController);
  	//初始化ASC信息
  	InitAbilityActorInfo();
  }
  
  void AAuraCharacter::OnRep_PlayerState()
  {
  	Super::OnRep_PlayerState();
  	//这一步是相当于在所有客户端上 调用这个初始化函数
  	InitAbilityActorInfo();
  }
  
  void AAuraCharacter::InitAbilityActorInfo()
  {
  	//第一步先拿到PS
  	TObjectPtr<AAuraPlayerState> AuraPlayerState = GetPlayerState<AAuraPlayerState>();
  	check(AuraPlayerState);
  	//这一步 使用ASC组件的初始化API 两个参数(谁是持有,谁是代理)多人时:PS持有ASC,玩家Pawn绑代理
  	AuraPlayerState->GetAbilitySystemComponent()->InitAbilityActorInfo(AuraPlayerState,this);
  	//这一步是将PS中的 ASC组件 变量 赋值给 AuraCharacterBase基类 中创建的变量
  	////主角通过PS持有 ASC组件 和 AS组件
  	AbilitySystemComponent = AuraPlayerState->GetAbilitySystemComponent();
  	AttributeSet = AuraPlayerState->GetAttributeSet();
  }
  ```

  &emsp;

  &emsp;

___________________________________________________________________________________________

  #### OnRep_PlayerState函数 来自AController

  ![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.4/6.png?raw=true)

  - InitAbilityActorInfo函数（自建 初始化技能信息 函数）

___________________________________________________________________________________________

  ### GM中设置PS

  ![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.4/7.png?raw=true)
___________________________________________________________________________________________

[返回最上面](#处理关键点：)

___________________________________________________________________________________________