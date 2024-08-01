___________________________________________________________________________________________
### [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)
___________________________________________________________________________________________
# GAS 2.2 通过(接口)实现(描边)效果

___________________________________________________________________________________________
# <font color=red>处理关键点：</font>

<font face="黑体" color=red size=3>1. 接口Interface的使用（比如权限和纯虚函数） </font>

<font face="黑体" color=red size=3>2. PlayerController中使用 获取鼠标的位置发射射线，返回结果 的函数（只识别block） </font>

<font face="黑体" color=red size=3>3. 自定义边缘发光深度材质 生效相关配置（Post Process Volume生效范围/后期处理材质配置） </font>

<font face="黑体" color=red size=3>4. 在项目文件中定义宏并使用 </font>

___________________________________________________________________________________________

### 创建C++接口类

<img src=".\\配图\\GAS_2.2\\1.png" width="60%">

### 创建两个(勾边/取消沟边)纯虚函数

-<font face="黑体" color=red size=4>方法需要public!!!!! </font>
  &emsp;

  + `头文件`中：
```cpp
  public:
  	//勾边 纯虚函数
  	virtual void HightLightActor() = 0;
  	virtual void UnHightLightActor() = 0;
```

  &emsp;

  &emsp;

### 在敌人的类  **<font color=yellow> AAuraEnemy </font>**中继承这个接口并实现这俩函数

&emsp;

+ `头文件`中：使用接口函数需要特别备注 Begin 和 End
```cpp
public:

	// Begin IEnemyInteraction
	virtual void HightLightActor() override;
	virtual void UnHightLightActor() override;
	// End IEnemyInteraction
```

&emsp;

+ `源文件`中：实现接口函数(便于调用给敌人勾边)
```cpp
void AAuraEnemy::HightLightActor()
{
}

void AAuraEnemy::UnHightLightActor()
{
}
```

&emsp;

___________________________________________________________________________________________

### **<font color=yellow> AAuraPlayerController </font>**中创建鼠标发射射线的函数和调用**<font face=" " color=orange size=5>PlayerTick </font> **使用API: **<font face=" " color=orange size=5>GetHitResultUnderCursor </font> **

&emsp;

+ `头文件`中：
```cpp
//前项声明
class IEnemyInteraction;
public:
	//相当于Tick 这个函数被每帧调用一次，用于处理玩家的输入、更新玩家状态、执行碰撞检测等与玩家相关的操作。
	virtual void PlayerTick(float DeltaTime) override;
private:
	void CursorTrace();

	//上一帧的对象和这一帧 鼠标悬停的对象
	//TScriptInterface<接口类> 指针；这是一个保存实现了该接口类的对象(若未实现，对象 = nullptr)
	UPROPERTY()
	TScriptInterface<IEnemyInteraction> LastActor;
	UPROPERTY()
	TScriptInterface<IEnemyInteraction> ThisActor;
```

&emsp;

+ `源文件`中：
```cpp
//引头文件
#include "Interaction/EnemyInteraction.h"
void AAuraPlayerController::CursorTrace()
{
	
	FHitResult HitResult;
	const bool bHit = GetHitResultUnderCursor(ECC_Visibility,false,HitResult);
	if (!bHit) return;
	LastActor = ThisActor;
	ThisActor = HitResult.GetActor();
	/*
	 *	===========================================================================
	 *	此时分为五种情况:
	 *	===========================================================================
	 *	1	LastActor 为空	/	ThisActor 为空
	 *		啥也不干
	 *	===========================================================================
	 *	2	LastActor 为空	/	ThisActor 不为空
	 *		ThisActor 勾边
	 *	===========================================================================
	 *	3	LastActor 不为空	/	ThisActor 为空
	 *		LastActor 取消勾边
	 *	===========================================================================
	 *	4	LastActor 不为空	/	ThisActor 不为空
	 *		LastActor 取消勾边 ThisActor勾边
	 *	===========================================================================
	 *	5	LastActor 不为空	/	ThisActor 不为空		/	且 LastActor = ThisActor
	 *	===========================================================================
	 *	下面是逻辑实现部分:
	 */
	
	if (LastActor == nullptr)
	{
		if (ThisActor == nullptr)
		{
			//情况1
		}
		else
		{
			//情况2
			ThisActor->HightLightActor();
		}
	}
	else
	{
		if (ThisActor == nullptr)
		{
			//情况3
			LastActor->UnHightLightActor();
		}
		else
		{
			if (LastActor != ThisActor)
			{
				//情况4
				LastActor->UnHightLightActor();
				ThisActor->HightLightActor();
			}
			else
			{
				//情况5
			}
		}
	}
}

void AAuraPlayerController::PlayerTick(float DeltaTime)
{
	Super::PlayerTick(DeltaTime);
	//每帧调用检测鼠标
	CursorTrace();
}
```

___________________________________________________________________________________________

- - 在 Unreal Engine 中，GetHitResultUnderCursor 使用的碰撞通道必须配置为阻挡（block）才能检测到碰撞。如果碰撞通道配置为重叠（overlap），则碰撞检测函数不会报告碰撞结果。

    - 解释原因
      - GetHitResultUnderCursor 函数依赖于碰撞通道配置的阻挡行为。当碰撞通道配置为重叠时，它仅用于生成重叠事件（如 OnOverlapBegin 和 OnOverlapEnd），而不是用于阻挡光线追踪或射线检测。因此，如果你希望在使用 GetHitResultUnderCursor 时检测到碰撞，你需要确保目标对象的碰撞通道配置为阻挡。
  
    - 解决方法
      - 确保你的 Pawn 或其他目标对象的碰撞设置正确配置为阻挡 ECC_Visibility 通道。

#### 知识点：PC中PlayerTick和Tick的区别？

- PlayerTick和Tick都是用于更新控制器状态和执行特定功能的函数。
- PlayerTick:

  - PlayerTick是PlayerController类的一个成员函数，用于处理与玩家直接相关的更新逻辑。

  - 这个函数被每帧调用一次，用于处理玩家的输入、更新玩家状态、执行碰撞检测等与玩家相关的操作。

  - 通常，PlayerTick函数用于处理与玩家控制相关的逻辑，例如检测玩家是否按下了特定的按键，或者更新玩家的位置和方向。
- Tick:

  - Tick函数是Actor类的一个成员函数，而PlayerController是Actor的子类，因此PlayerController也继承了Tick函数。

  - 与PlayerTick不同，Tick函数是Actor类的通用更新函数，被每帧调用一次，用于处理与Actor相关的更新逻辑。

  - 在PlayerController中，您可以重写Tick函数以处理与控制器状态相关的更新逻辑，例如更新UI、执行特定的事件处理等。
- PlayerTick函数用于处理与玩家控制相关的逻辑，而Tick函数则用于处理通用的Actor更新逻辑。___________________________________________________________________________________________

### 在敌人的类中创建bool变量来控制勾边的显示与否

- 头文件中声明一个bool
  
  &emsp;
  
  - 头文件`中：
  
  
  ```cpp
  protected:
  	//是否勾边
  	UPROPERTY(BlueprintReadOnly,Category="HightLight", meta=(AllowPrivateAccess))
  	bool bHightLight = false;
  ```
  
  &emsp;
  
  + `源文件`中：
  ```cpp
  void AAuraEnemy::HightLightActor()
  {
  	bHightLight = true;
  }
  
  void AAuraEnemy::UnHightLightActor()
  {
  	bHightLight = false;
  }
  ```
  
  &emsp;
  
  ___________________________________________________________________________________________

### 创建一个敌人的BP总基类

- 这样可以设置一些共有行为属性

- <img src=".\\配图\\GAS_2.2\\2.png" width="80%">

### 修改BP敌人的继承类

- <img src=".\\配图\\GAS_2.2\\3.png" width="80%">

- <img src=".\\配图\\GAS_2.2\\4.png" width="80%">

### 修改BP敌人的碰撞类型

- <img src=".\\配图\\GAS_2.2\\5.png" width="80%">

### 敌人BP基类中添加测试逻辑

- <img src=".\\配图\\GAS_2.2\\6.png" width="80%">

### 测试结果gif

- <img src=".\\配图\\GAS_2.2\\7.gif" width="100%">

  ___________________________________________________________________________________________

### 修改自定义边缘发光深度材质

- 把这两个设为变量，并创建实例，便于调整

  

  - <img src=".\\配图\\GAS_2.2\\8.png" width="80%">

- [关于此描边材质详细可以看这个链接](https://www.bilibili.com/video/BV1Ai4y177bZ/?spm_id_from=333.337.search-card.all.click)

### 拖入#<font color=red>PostProccessVolumes</font>设置全局生效，配置自定义边缘发光深度材质

- <img src=".\\配图\\GAS_2.2\\9.png" width="80%">

- <img src=".\\配图\\GAS_2.2\\10.png" width="80%">

### # <font color=red>项目设置中修改自定义渲染深度通道</font>

- <img src=".\\配图\\GAS_2.2\\11.png" width="80%">

### 在敌人的类中修改 描边函数，为开启和关闭自定义渲染深度（若开启还需给定 自定义深度 的值）&emsp;

+ `源文件`中：
```cpp
void AAuraEnemy::HightLightActor()
{
	bHightLight = true;
	//先打开 自定义深度渲染
	GetMesh()->SetRenderCustomDepth(true);
	//在设置自定义渲染深度Value
	GetMesh()->SetCustomDepthStencilValue(250.f);
}

void AAuraEnemy::UnHightLightActor()
{
	bHightLight = false;
	//关闭 自定义深度渲染
	GetMesh()->SetRenderCustomDepth(false);
}
```

&emsp;

___________________________________________________________________________________________

### 断开 敌人BP基类中 测试用的逻辑

- <img src=".\\配图\\GAS_2.2\\12.png" width="80%">

### 测试结果

- <img src=".\\配图\\GAS_2.2\\13.gif" width="100%">

### Bug：此时武器还没描边，武器也需要，下面解决

### 之前的宏定义的不规范，需要在整体项目中 定义这个宏，同时将武器描边

&emsp;

+ **<font color=yellow> Aura.h </font>**`头文件`中：
```cpp
#define CUSTOM_DEPTH_VALUE 250
```



- 敌人基类**<font color=yellow> AAuraEnemy </font>**中

  &emsp;

  + `源文件`中：
  ```cpp
  //需要引入项目头文件，定义的自定义通道常量宏 在这里
  #include "Aura/Aura.h"
  
  void AAuraEnemy::HightLightActor()
  {
  	bHightLight = true;
  	//先打开 自定义深度渲染
  	GetMesh()->SetRenderCustomDepth(true);
  	//在设置自定义渲染深度Value
  	GetMesh()->SetCustomDepthStencilValue(CUSTOM_DEPTH_VALUE);
  }
  
  void AAuraEnemy::UnHightLightActor()
  {
  	bHightLight = false;
  	//关闭 自定义深度渲染
  	GetMesh()->SetRenderCustomDepth(false);
  }
  ```

  


### 完成 描边效果

- 对比

  <img src=".\\配图\\GAS_2.2\\14.png" width="80%">