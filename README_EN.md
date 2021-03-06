<div style="align: center">
<img src="https://upload-images.jianshu.io/upload_images/5632003-14498d8a6c786224.png"/>
</div>

<p style="align: center">
    <a href="https://github.com/tigerAndBull/TABAnimated">
       <img src="https://img.shields.io/badge/platform-iOS-blue.svg?style=plastic">
    </a>
    <a href="https://github.com/tigerAndBull/TABAnimated">
       <img src="https://img.shields.io/badge/language-objective--c-blue.svg">
    </a>
    <a href="https://cocoapods.org/pods/TABAnimated">
       <img src="https://img.shields.io/badge/cocoapods-supported-4BC51D.svg?style=plastic">
    </a>
    <a href="https://github.com/tigerAndBull/TABAnimated">
       <img src="https://img.shields.io/badge/support-ios%208%2B-orange.svg">
    </a>
</p>

## What is the skeleton screen?

Find the comrades here, and more or less have an understanding of the skeleton screen. Skeleton Screen is a solution to optimize the user's weak network experience, which can effectively alleviate the anxiety of users waiting.

## What is TABAnimated?

TABAnimated is a solution for iOS developers to automatically generate skeleton screens. Developers can configure the already developed views to configure some global/local parameters through TABAnimated to automatically generate a skeleton screen that is consistent with their length.  
Of course, TABAnimated will help you manage the lifecycle of the skeleton screen.

## Catalog

* [Integration Advantage] (# Integration Advantage)
* [Effect display] (# effect display)
* [demo process] (# demo process)
* [Integration Steps] (# Integration Step)
* [Question Search] (# Question Search)
* [Last emphasis] (# last emphasis)

## Features

- Highly automated
- Low coupling
- High performance
- Suitable for various scenarios
- High degree of customization

## Preview

| Dynamic Animation | Card View | Bin Animation |
| ------ | ------ | ------ |
| ![动态动画.gif](https://upload-images.jianshu.io/upload_images/5632003-56c9726a027ca5e2.gif?imageMogr2/auto-orient/strip) | ![卡片投影.gif](https://upload-images.jianshu.io/upload_images/5632003-fd01c795bb3f9e1a.gif?imageMogr2/auto-orient/strip) | ![呼吸灯.gif](https://upload-images.jianshu.io/upload_images/5632003-683062be0a23d5b8.gif?imageMogr2/auto-orient/strip) | 

| Shimmer Animation | Segmented View | Drop Animation |
| ------ | ------ | ------ |
| ![闪光灯改版.gif](https://upload-images.jianshu.io/upload_images/5632003-93ab2cf6950498ab.gif?imageMogr2/auto-orient/strip)| ![分段视图.gif](https://upload-images.jianshu.io/upload_images/5632003-4da2062be691cf0b.gif?imageMogr2/auto-orient/strip) | ![豆瓣.gif](https://upload-images.jianshu.io/upload_images/5632003-3ed9d6cc317891a3.gif?imageMogr2/auto-orient/strip) | 

**Dark Mode**

| Toolbox Switching | setting page switching |
| ------ | ------ |
| ![工具箱切换.gif](https://upload-images.jianshu.io/upload_images/5632003-cf5c4f50eac6fe6c.gif?imageMogr2/auto-orient/strip) | ![setting设置切换.gif](https://upload-images.jianshu.io/upload_images/5632003-2d1fb96ec07d6bca.gif?imageMogr2/auto-orient/strip) | 

## Installation

- CocoaPods

```
Pod 'TABAnimated'
```

- Carthage

```
Github "tigerAndBull/TABAnimated"
```

- Drag the TABAnimated folder into your project

**Note: The demo demo downloaded on github, in order to simulate the real application scenario well, uses some familiar third parties, but TABAnimated does not depend on them.**

## Usage

### I. global parameter initialization

Initialize `TABAimated` in `didFinishLaunchingWithOptions`

```
[[TABAnimated sharedAnimated] initWithOnlySkeleton];
[TABAnimated sharedAnimated].openLog = YES;
```

**Note: There are other animation types, global properties, and comments in the framework.**

### II. Control view initialization

**Control view: If it is a list view, then it is UITableView/UICollectionView, there are documents to explain.**

`NewsCollectionViewCell` is the cell used in your list, of course, you have to bind other cells, it is also possible!

```
_collectionView.tabAnimated =
[TABCollectionAnimated animatedWithCellClass:[NewsCollectionViewCell class]
cellSize:[NewsCollectionViewCell cellSize]];
```

**Note**

- **There are other initialization methods, such as a variety of common cells, there are comments in the framework**
- **There are local properties for this control view, there are comments in the framework**

### III. Control skeleton screen switch

Open animation

```
[self.collectionView tab_startAnimation];
```

2. Turn off the animation

```
[self.collectionView tab_endAnimation];
```

### VI. Just said, how to use pre-processing callback + chain syntax?

```
_tableView.tabAnimated.adjustBlock = ^(TABComponentManager * _Nonnull manager) {
    Manager.animation(1).down(3).radius(12);
    Manager.animation(2).height(12).width(110);
    Manager.animation(3).down(-5).height(12);
};
```

#### 1. Some people see the above, they may be scared at once, is integration so complicated?

A: It does not need to be adjusted asynchronously. It needs to be adjusted to what extent, and it is related to your own constraints and product requirements. Therefore, it does not automatically generate the effect that any product, anyone is completely satisfied immediately.
You can rest assured that launching this feature will help developers adjust the results they want more quickly.**

#### 2. `manager.animation(x)`, what is x?

A: In the appDelegate set TABAnimated's `openAnimationTag` attribute to YES, the framework will automatically indicate for you, what is x?
```
[TABAnimated sharedAnimated].openAnimationTag = YES;
```

#### 3. Learn a few examples (pre-processing callback + chain syntax)

- If the height and width of the 0th element are not appropriate
```
Manager.animation(0).height(12).width(110);
```
- If the first element needs to use a placeholder
```
Manager.animation(1).placeholder(@"bitmap name.png");
```
- If the 1, 2, and 3 elements are all 50 in width
```
Manager.animations(1,3).width(50);
```
- If the 1, 5, and 7 elements need to move down 5px
```
manager.animationWithIndexs(1,5,7).down(5);
```

![Subscript diagram.png](https://upload-images.jianshu.io/upload_images/5632003-2842bd54e80dd9ef.png?imageMogr2/auto-orient/strip%7CimageView2/3/w/300)

#### Form integration must see

(1) Before you integrate the table view, be sure to clarify your own view structure:

Divided into the following three

+ One-to-one correspondence between section and cell style in section
+ view has only 1 section, but corresponds to multiple cells
+ dynamic section: the number of your sections is obtained by the network

(2) Understand your own needs:

+ Set multiple sections/rows to start animation together
+ Set multiple sections/rows, partially open animations

(3) Finally, find the corresponding initialization method and start the animation method in the framework!

## Demonstration process

Let's take a closer look at TABAnimated with a small example.

#### 1. Tom and Jack have a view like this, which needs to integrate the skeleton screen.

![Requirements.png](https://upload-images.jianshu.io/upload_images/5632003-8bb0895de7690f79.png?imageMogr2/auto-orient/strip%7CimageView2/3/w/300)

#### 2. The following is the effect generated by TABAnimated automation.

![自动化生成.png](https://upload-images.jianshu.io/upload_images/5632003-f10c2427f8b149ba.png?imageMogr2/auto-orient/strip%7CimageView2/3/w/300)

#### 3. Jack is doing this demand, I am very satisfied with this effect, then Jack’s work is over. But Tom said, I feel that the length and height are similar to the original view, but I am not satisfied with the animation effect, not refined enough. So, he quickly made the following adjustments through (pre-processing callback + chain syntax).

![Adjusted effect.png](https://upload-images.jianshu.io/upload_images/5632003-0affe19065135d31.png?imageMogr2/auto-orient/strip%7CimageView2/3/w/300)

## Q&A

**Of course, in practical applications, we also have a variety of views, TABAnimated has experienced many products, all can be dealt with.
But the above knowledge is certainly not enough. The following is a more detailed description of the document.**

- You'd better have to (must) read the documentation:

> + [Cache Policy and Threading] (https://github.com/tigerAndBull/TABAnimated/blob/master/Documents/%E7%BC%93%E5%AD%98%E7%AD%96%E7%95 %A5%E5%92%8C%E7%BA%BF%E7%A8%8B%E5%A4%84%E7%90%86.md)

- The document you are most likely to use:

> + [Preprocessing callback animation element subscript issue] (https://github.com/tigerAndBull/TABAnimated/blob/master/Documents/%E5%8A%A8%E7%94%BB%E5%85%83% E7%B4%A0%E4%B8%8B%E6%A0%87%E9%97%AE%E9%A2%98.md)
> + [Question Q&A Document] (https://github.com/tigerAndBull/TABAnimated/blob/master/Documents/%E9%97%AE%E9%A2%98%E7%AD%94%E7%96%91 %E6%96%87%E6%A1%A3.md)
> + [global: local attribute, chained syntax api] (https://github.com/tigerAndBull/TABAnimated/blob/master/Documents/%E5%85%A8%E5%B1%80:%E5%B1% 80%E9%83%A8%E5%B1%9E%E6%80%A7%E3%80%81%E9%93%BE%E5%BC%8F%E8%AF%AD%E6%B3%95api. Md)

- Accessibility tools, techniques and other documentation you may use

> + [Live Preview Tool] (https://github.com/tigerAndBull/TABAnimated/blob/master/Documents/%E5%AE%9E%E6%97%B6%E9%A2%84%E8%A7%88 %E5%B7%A5%E5%85%B7.md)
> + [Detailed Douban Animation] (https://github.com/tigerAndBull/TABAnimated/blob/master/Documents/%E8%B1%86%E7%93%A3%E5%8A%A8%E7%94%BB %E8%AF%A6%E8%A7%A3.md)
> + [no more hook setDelegate and setDataSource] (https://github.com/tigerAndBull/TABAnimated/blob/master/Documents/%E4%B8%8D%E5%86%8Dhook%20setDelegate%E5%92%8CsetDataSource. Md)

**If you still can't solve the problem, you can contact me as soon as possible, I believe TABAnimated can solve 99% of the demand**

## License

MIT License

Copyright (c) 2018 tigerAndBull

Permission is hereby granted, free of charge, to any person obtaining a copy
Of this software and associated documentation files (the "Software"), to deal
In the Software without restriction, including without limitation the rights
To use, copy, modify, merge, publish, distribute, sublicense, and/or sell
Copies of the Software, and to permit persons to whom the Software is
Furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
Copys or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.