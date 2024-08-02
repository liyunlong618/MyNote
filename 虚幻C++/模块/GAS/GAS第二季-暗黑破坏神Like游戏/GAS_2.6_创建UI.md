___________________________________________________________________________________________
> [!!!!!!!!!!!项目根目录!!!!!!!!!!!](./!!!!!!!!!!!项目目录!!!!!!!!!!!.md)
___________________________________________________________________________________________
# GAS 2.6 创建UI


___________________________________________________________________________________________

- [GAS 2.6 创建UI](#gas-26-创建ui)
		- [玩家HP UI基类 继承自UserWidget( **这部分架构在2.7 MVC中解释** )](#玩家hp-ui基类-继承自userwidget-这部分架构在27-mvc中解释-)
			- [创建继承自UserWidget类的C++类](#创建继承自userwidget类的c类)
			- [创建子蓝图类](#创建子蓝图类)
			- [创建各种调节参数的函数](#创建各种调节参数的函数)
				- [默认值 ](#默认值-)
		- [添加显示血量和魔法的UI](#添加显示血量和魔法的ui)
			- [创建子类，继承自上面创建的UMG](#创建子类继承自上面创建的umg)
			- [配置子类](#配置子类)
			- [子类显示基类的变量](#子类显示基类的变量)
		- [创建显示玩家信息的UMG](#创建显示玩家信息的umg)
		- [创建HUD](#创建hud)
		- [创建蓝图类继承自，自建的HUD](#创建蓝图类继承自自建的hud)
			- [因为断言的存在，这里不配置会崩溃](#因为断言的存在这里不配置会崩溃)
		- [UI创建完成](#ui创建完成)


___________________________________________________________________________________________
### 玩家HP UI基类 继承自UserWidget( **这部分架构在2.7 MVC中解释** )
#### 创建继承自UserWidget类的C++类
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-852830-512962.png?raw=true)
___________________________________________________________________________________________
#### 创建子蓝图类
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-380868-695927.png?raw=true)
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-740501-767185.png?raw=true)
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-235501-997195.png?raw=true)
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-795105-406230.png?raw=true)
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-189583-26968.png?raw=true)
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-666738-118476.png?raw=true)
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-71635-817276.png?raw=true)
___________________________________________________________________________________________
#### 创建各种调节参数的函数
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-800866-196968.png?raw=true)
___________________________________________________________________________________________
- UpdateBoxSize
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-448892-777351.png?raw=true)
___________________________________________________________________________________________
- UpdateBackGround
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-539495-94194.png?raw=true)
___________________________________________________________________________________________
- UpdateGlobePadding
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-562783-521572.png?raw=true)
___________________________________________________________________________________________
- SetGlobeImage
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-588664-555685.png?raw=true)
___________________________________________________________________________________________
- UpdateGlassPadding
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-836114-832674.png?raw=true)
___________________________________________________________________________________________
- UpdateGlassImage
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-485340-796810.png?raw=true)
___________________________________________________________________________________________

##### 默认值 ![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-331360-186444.png?raw=true)
___________________________________________________________________________________________
### 添加显示血量和魔法的UI
#### 创建子类，继承自上面创建的UMG
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-580206-259970.png?raw=true)
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-94014-196371.png?raw=true)
___________________________________________________________________________________________
#### 配置子类
___________________________________________________________________________________________
#### 子类显示基类的变量
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-218988-31744.png?raw=true)
___________________________________________________________________________________________
### 创建显示玩家信息的UMG
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-969321-580705.png?raw=true)
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-312150-117385.png?raw=true)

___________________________________________________________________________________________
### 创建HUD
&emsp;

+ `头文件`中：
```cpp
public:
	UPROPERTY()
	TObjectPtr<UAuraUserWidget> OverlayWidget;
	virtual void BeginPlay() override;
private:
	UPROPERTY(EditAnywhere)
	TSubclassOf<UAuraUserWidget> OverlayWidgetClass;
```

&emsp;

+ `源文件`中：
```cpp
void AAuraHUD::BeginPlay()
{
	Super::BeginPlay();
	checkf(OverlayWidgetClass,TEXT("OverlayWidgetClass is nullptr!!! in:	AAuraHUD!!!"));//断言检查下
	const TObjectPtr<UAuraUserWidget> Widget = CreateWidget<UAuraUserWidget>(GetWorld(),OverlayWidgetClass);
	Widget->AddToViewport();
}
```

&emsp;

&emsp;

___________________________________________________________________________________________
### 创建蓝图类继承自，自建的HUD
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-482158-87807.png?raw=true)
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-991211-195041.png?raw=true)
#### 因为断言的存在，这里不配置会崩溃 
![](https://github.com/liyunlong618/MyNote/blob/master/%E8%99%9A%E5%B9%BBC++/%E6%A8%A1%E5%9D%97/GAS/GAS%E7%AC%AC%E4%BA%8C%E5%AD%A3-%E6%9A%97%E9%BB%91%E7%A0%B4%E5%9D%8F%E7%A5%9ELike%E6%B8%B8%E6%88%8F/%E9%85%8D%E5%9B%BE/GAS_2.6/GAS%202.6%20%E5%88%9B%E5%BB%BAUI-%E5%B9%95%E5%B8%83%E5%9B%BE%E7%89%87-856418-88042.png?raw=true)
___________________________________________________________________________________________
### UI创建完成 
___________________________________________________________________________________________

[返回最上面](#处理关键点)
___________________________________________________________________________________________