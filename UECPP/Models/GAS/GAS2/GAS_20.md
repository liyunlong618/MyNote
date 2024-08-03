___________________________________________________________________________________________
>[!!!!!!!!!!!返回项目根目录!!!!!!!!!!!](./_____Menu_____)
___________________________________________________________________________________________

# GAS 2.0 配置项目/设置Mesh/插槽/动画(创建和使用ABP模板)



___________________________________________________________________________________________

## 处理关键点

<font face="黑体" color=red size=3>1. 再C++中使用FName插槽名，将武器SK，绑定到角色SK上</font>

<font face="黑体" color=red size=3>2. 使用动画蓝图模板</font>

___________________________________________________________________________________________

~~[旧视频参考链接](https://www.bilibili.com/video/BV1fC411x7Af?p=2&vd_source=9e1e64122d802b4f7ab37bd325a89e6c)~~

[新视频参考链接](https://www.bilibili.com/video/BV1JD421E7yC?p=1&vd_source=9e1e64122d802b4f7ab37bd325a89e6c)

___________________________________________________________________________________________

- [GAS 2.0 配置项目/设置Mesh/插槽/动画(创建和使用ABP模板)](#gas-20-配置项目设置mesh插槽动画创建和使用abp模板)
  - [处理关键点：](#处理关键点)
    - [导入资源](#导入资源)
    - [参考3A制作规范 创建人物基类](#参考3a制作规范-创建人物基类)
    - [基类 AuraCharacterBase.h中删除不用的Tick和关闭Tick节约性能!](#基类-auracharacterbaseh中删除不用的tick和关闭tick节约性能)
    - [基类AuraCharacterBase.h中,创建武器  智能指针 ,cpp中绑定到插槽上](#基类auracharacterbaseh中创建武器--智能指针-cpp中绑定到插槽上)
        - [知识点：智能指针是什么？](#知识点智能指针是什么)
    - [创建敌人类文件夹](#创建敌人类文件夹)
    - [创建角色，配置角色和武器Mesh](#创建角色配置角色和武器mesh)
    - [选择武器Mesh后无法挂载，因为没有插槽，需要添加插槽，并调整插槽位置](#选择武器mesh后无法挂载因为没有插槽需要添加插槽并调整插槽位置)
    - [添加敌人](#添加敌人)
    - [配置角色动画蓝图](#配置角色动画蓝图)
    - [使用动画蓝图模板创建敌人的ABP](#使用动画蓝图模板创建敌人的abp)


___________________________________________________________________________________________

### 导入资源
[资源链接(百度云)](https://pan.baidu.com/s/1xySQ1kbKUm5zyFfr_5r4mQ?pwd=6666)
```cpp
https://pan.baidu.com/s/1xySQ1kbKUm5zyFfr_5r4mQ?pwd=6666
```

___________________________________________________________________________________________
### 参考3A制作规范 创建人物基类
![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/1.png)


___________________________________________________________________________________________

### 基类 AuraCharacterBase.h中删除不用的Tick和关闭Tick节约性能!
![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/4.png)

```CPP
    //构造中关闭tick,节约开销
    PrimaryActorTick.bCanEverTick = false;
```

___________________________________________________________________________________________


### 基类AuraCharacterBase.h中,创建武器  智能指针 ,cpp中绑定到插槽上

&emsp;

+ `头文件`中：
```cpp
//Combat 战斗
UPROPERTY(EditAnywhere, Category="Combat") 
TObjectPtr<USkeletalMeshComponent> Weapon;
```

&emsp;

+ `源文件`中：
```cpp
AAuraCharacterBase::AAuraCharacterBase()
{
 	//构造中关闭tick,节约开销
	PrimaryActorTick.bCanEverTick = false;

	//创建武器组件并绑定到插槽->WeaponSocket
	Weapon = CreateDefaultSubobject<USkeletalMeshComponent>("Weapon");
	Weapon->SetupAttachment(GetMesh(),FName("WeaponSocket"));
	Weapon->SetCollisionEnabled(ECollisionEnabled::NoCollision);
}
```

&emsp;

&emsp;

##### 知识点：智能指针是什么？

+ 是一个模板类，在生命周期结束时，自动对他进行内存管理，从而避免内存泄漏和悬垂指针的问题


>


### 创建敌人类文件夹
![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/8.png)

___________________________________________________________________________________________


### 创建角色，配置角色和武器Mesh
![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/9.png)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/10.png)

___________________________________________________________________________________________


### 选择武器Mesh后无法挂载，因为没有插槽，需要添加插槽，并调整插槽位置

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/11.png)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/12.png)

___________________________________________________________________________________________


### 添加敌人

+ 创建蓝图类继承自AuraEnemy

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/13.png)

+ 设置敌人和武器的Mesh

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/14.png)

+ 也需要搞一个叫WeaponSocket的骨骼插槽(已经有了，原插槽改名就可以)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/15.png)

___________________________________________________________________________________________

### 配置角色动画蓝图
+ 路径

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/16.png)

&emsp;

+ 创建动画状态机

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/17.png)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/18.png)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/19.png)

&emsp;

+ 动画蓝图初始化时保存角色变量和移动组件

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/20.png)

&emsp;

+ 获取Speed变量

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/21.png)

___________________________________________________________________________________________

### 使用动画蓝图模板创建敌人的ABP
+ 创建角色动画蓝图模板

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/22.png)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/23.png)

&emsp;

+ 因为没有选骨骼，所以可以给很多不同骨骼的对象使用

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/24.png)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/25.png)

&emsp; 

<font face="黑体" color=red size=5>关键操作！！！：通过混合空间播放器，后续可以在子类中调整播放混合空间</font>

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/26.png)

搞定！

&emsp;

&emsp;

使用动画模板给敌人创建ABP

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/27.png)

&emsp;

创建ABP

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/28.png)

&emsp;

使用模板创建

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/29.png)

&emsp;
在资产编辑器 给上动画

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/30.png)

&emsp;

给BP配置ABP

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/31.png)

&emsp;


参考上面的步骤，创建另一个敌人的ABP

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/32.png)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/33.png)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/34.png)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/35.png)

![](https://raw.githubusercontent.com/liyunlong618/MyNote/blob/master/UECPP/Models/GAS/GAS2/Image/GAS-2.0/36.png)

&emsp;

目前只在动画蓝图模板中GetSpeed并没有Set



___________________________________________________________________________________________

[返回最上面](#处理关键点)

___________________________________________________________________________________________